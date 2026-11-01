# MER-P1.2 Super Sync, virtual stock, pre-order

> Nguồn: page 2484011230 · 90 phút (Study 20' · Demo 15' · Quiz 10' · Practice 45') · Facilitator: Shift Leader/Sub-Lead · Capabilities C2, C4 · Cần xong MER-2.1, G3.3 và MER-P1.1. Mang TRN-044 (SCOE-50) + TRN-002 (SCOE-8) hoặc TRN-003 (SCOE-9), lịch có số tuần ISO. Staging Backoffice el3-s2 (Product Cockpit, Administration Cockpit); Merch không có HAC. Chỉ bấm Product Sync sau khi trainer comment `SYNC OK TRN044`; không cronjob, không ImpEx. Không có access: đi giấy qua ba runbook, trainer đóng vai Backoffice.

## Mục tiêu
Chạy Super Sync STOCK/PRICE đúng danh sách SKU, so với nguồn và giải thích từng SKU lỗi; dừng sync gây hại (SKU còn pre-order, RRP không qua price sanity); set/đổi/gỡ virtual stock đúng warehouse trong cam kết bằng văn bản, kèm ngày handback; mở và hủy pre-order đúng ngày, time zone, tuần, maximum và không để lại dữ liệu pre-order.

## Thuật ngữ
**Products Sync Selector** (icon Product Sync ở Product Cockpit › Products (master catalog); chạy Super Sync cho SKU chọn theo loại DOTCOM, PRICE, STOCK, IMAGE); **Source ready** (xác nhận bằng văn bản stock NERP đã ở storage location / RRP mới có hiệu lực trên NERP / nội dung AEM đã publish; không có thì không sync); **`VirtualWarehouse-<cc>`** (kho ảo của market; chỉ đọc để xem reserved; không gõ virtual stock ở đây — số lượng đặt trên kho NERP phục vụ sau khi chặn stock sync); **Written commitment** (số lượng bằng văn bản của subsidiary trên ticket; virtual stock và max pre-order không bao giờ vượt); **"Set to" hay "change by"** (số là tổng mới hay delta; "tăng 1" trên available 4 là 5, không phải 1); **maxPreOrder / preOrder** (Max PreOrder là trần bạn gõ; Pre Order là số đã nhận do hệ thống điền); **Pre-order weeks** (YYYYWW; overselling start = initial end + 1, không chồng: initial 202642–202643, overselling 202644–202645); **Handback** (trả SKU từ virtual/pre-order stock về stock NERP, MER-STK-01 V2, có due date và comment "Go-live schedule").

## Nội dung
### 1. Ba service stock và cách nối
Cùng status path và SLA (Low, 24h, initial response 2h) nhưng khác kiểm soát:
| Service | Title điển hình | Checker | Duyệt |
|---|---|---|---|
| MER-STK-01 Super Sync | "[TV] SKU Activate & Sync Warehouse Stock", "Supersync SKU" | Peer/Shift Leader; QA lấy mẫu V3 (RRP) | Không |
| MER-STK-02 Virtual stock | "[DA] SKU Dummy Setup", "SAVINA-DA Set virtual stock SKUs" | QA Team 100% trước khi bán | Cam kết văn bản; Shift Leader ở PRD SETUP; Sub-Lead khi ≥500 unit |
| MER-STK-03 Pre-order | "[TSE] Set pre Order Skus [date]", "Set Pre-order [date]" | QA Team trước khi mở window và sau mỗi thay đổi | Như STK-02 |
Nối một chiều: virtual stock và pre-order kết thúc bằng **handback** về stock NERP (MER-STK-01 V2). Gỡ pre-order theo MER-STK-03 **trước** mọi Super Sync STOCK. Virtual stock và overselling (backorder) không bao giờ cùng một SKU (virtual stock vô hiệu overselling). Stock luôn được làm trong freeze; ngày và tuần pre-order cũng nằm trong danh sách hard-freeze cho phép.
Cả ba bắt đầu giống nhau: tách action line, export before (flag ở tab Administration mỗi catalog version, Stock Level mỗi warehouse), hỏi một câu gộp khi thiếu nguồn, cam kết, "set to/change by", time zone hay kế hoạch kết thúc (ON HOLD SUBS, subsidiary là Assignee).
Known error thuộc lòng: KE-MER-STK-01-02 sync không ra stock (import còn bị chặn ở một catalog, hoặc có override); KE-MER-STK-02-03 gấp đôi số lượng ("change by" đọc thành "set to"); KE-MER-STK-02-07 đã set available nhưng vẫn hết hàng (reserved trên kho ảo: COEC cho TEC-MON-02); KE-MER-STK-03-03 window mở lệch vài giờ (chưa đổi time zone).

### 2. Super Sync: stock và RRP từ NERP
Đường: Backoffice › Product Cockpit › Products › master catalog (VD `myProductCatalog`) › chọn SKU › **Products Sync Selector** › loại dữ liệu › Start Sync. Rồi sync master → child Staged → Online. Import theo lịch `<cc>-tokoStockImportUpdateJob` cũng ~mỗi 30'; Super Sync là chạy tay do operator Merch; không ImpEx.
**MER-STK-01 V1 (stock), V3 (RRP):** (1) source ready — requester xác nhận stock ở location NERP / RRP hiệu lực, có reference trên ticket; (2) before export — flag block mỗi catalog version, Stock Level mỗi warehouse, price row RRP; (3) bẫy — không có pre-order trên SKU, stock import đã gỡ chặn, ghi chú `blockPriceUpdatesFromExternalSystems`, PS-03/PS-04 với RRP; (4) chạy STOCK, hoặc PRICE vào/sau giờ hiệu lực, liệt kê SKU lỗi kèm lý do; (5) so available với số NERP, RRP với danh sách; master → child → Online; sau PRICE kiểm PriceInfoChange có row VALID; (6) V3: gắn cờ special price hoặc promotion có giá bán dịch chuyển.
**TRN-044 (MY), 4 line:**
- Line 1 `EF-BX620PBEGWW` stock: flag FALSE, không override: chạy STOCK.
- Line 2 `EF-XF966SBEGWW` RRP 349 → 379 MYR: tỷ lệ 1.09, qua sanity; chạy PRICE chỉ sau 18/11 00:00 MYT, rồi kiểm 379 ở `myProductCatalog`, `myEstoreProductCatalog` Staged và Online, `myb2bProductCatalog`.
- Line 3 `EP-DA705BWEGWW`: Stock Level preOrder 18/max 20 trên `SETOnline`. **Dừng**: không Super Sync STOCK trên SKU pre-order (lỗi NZ B7Q7 chính là lỗi người này).
- Line 4 `SM-R420NZKAXME` 499 → 4990: tỷ lệ 10, PS-03 fail. **Dừng** và hỏi (requester đáp 599 mới đúng).
Line 3, 4 vào một câu hỏi, ON HOLD SUBS. Line 2 sang QA REVIEW lấy mẫu; line stock không cần QA Team. Cùng SKU vẫn FAIL sau 1–2 lần thử thì reporter kiểm NERP/AEM: một comment kèm SKU lỗi và message, ON HOLD SUBS, giữ ticket mở. COEC cho TEC-TSP-06 chỉ khi job lỗi, không cho lỗi dữ liệu. Không bao giờ "sửa" RRP bằng price upload: đó là MER-PRC-01 có Knox.
> RRP sync từ NERP không phải upload. Sau khi chạy mở Price Settings › Prices › PriceInfoChange, Status VALID cho SKU đó; có row thì submit Knox như special price. RRP upload tay luôn cần Knox (ID CE, SKU không có trong NERP).

### 3. Virtual stock: bán trước rồi handback
MER-STK-02 ~80 ticket/tháng, MY ~70%. Virtual stock chỉ CE. Chặn NERP stock import, rồi gõ số lượng lên kho NERP phục vụ (MY MX `WC11-S506`, PH CE `WCOL-S513`, TH `WC03`; nhiều kho thì subsidiary chỉ định), không bao giờ vượt cam kết. `VirtualWarehouse-<cc>` chỉ đọc (reserved). Dummy line MX không set: hỏi Shift Leader, ON HOLD RHQ.
**V1:** (1) cam kết viết, số lượng nằm trong đó; ≥500 unit là hold PS-14; (2) before export (flag mỗi catalog version, Stock Level mỗi warehouse kèm reserved, xác định kho phục vụ); (3) CE: "Is blocked for Stock Import" TRUE ở master rồi sync, ba flag kia giữ nguyên; MX: cả bốn FALSE, TRUE chỉ khi có reference RHQ duyệt (ON HOLD RHQ); (4) Base Commerce › Stock Level › SKU + kho phục vụ › Available Amount vào giờ bắt đầu thỏa thuận (Stock Level không có catalog version: có hiệu lực ngay); (5) storefront: PDP bán được, số lượng vượt virtual stock bị từ chối; (6) handback: due date = tuần hàng về, comment "Go-live schedule" kèm ngày và owner.
V2 đổi: "change by" = hiện tại ± delta; "set to" = tổng nêu. Không bao giờ <0; số đã bán vượt cam kết bị giảm thì dừng và báo requester ngay. V6 gỡ: Available = 0 trên kho phục vụ đang giữ virtual quantity; giữ chặn tới khi handback. Về stock NERP là MER-STK-01 V2.
**TRN-002 (MY), Part 1 ngày D0:** ba SKU DA là CE. "Is blocked for Stock Import" TRUE ở `myProductCatalog` và sync, tìm kho phục vụ (tab Product Stock › Find Stock Levels for Product), set `VS15A60AGR5/ME` = 5 và `RT47CB66448AME` = 3; `WA17CG6886BVFQ` đã dummy 4, "tăng 1" ra 5 (gõ 1 là RC-ENT). Ticket không có cam kết viết nên comment đầu hỏi cam kết và "current + 1". Shipment notice là line MER-DLV-02. **Part 2 ngày D+7:** release `VS15A60AGR5/ME` (Available 0 trên kho phục vụ, notice đã hết), và `QA83S90HAEXXM` gỡ dummy (100) rồi archive ở mọi child catalog kể cả 3PD (MER-PRD-01 V3).

### 4. Pre-order: mở, đổi, hủy
MER-STK-03 ~44 ticket/tháng, TH ~72%. Doer đặt field product theo catalog version và trần theo warehouse:
1. Before export (field pre-order và bốn flag block mỗi catalog version, Stock Level mỗi warehouse). Cả bốn flag block phải FALSE trước khi set; TRUE chặn set-up GSCM.
2. Catalog › Products › SKU (Staged) › tab **Pre-order Settings**: Pre-Order Date Range (start, end), Pre-order Delivery Date to Storefront (`preOrderDeliveryDate`), và bốn tuần nếu category dùng. Lặp ở mọi catalog trong scope.
3. Sync Staged → Online (export: Online = Staged).
4. Base Commerce › Stock Level › SKU + kho phục vụ › **Max PreOrder** = số lượng cam kết. Không gõ Pre Order. Lỗi "Initial pre-order max limit": dừng, SKU nuôi bởi GSCM (V5; không vượt giới hạn GSCM).
5. QA REVIEW trước khi mở window; lúc bắt đầu kiểm CTA "Pre-order now", ngày giao, và số lượng vượt maximum bị từ chối.
6. Ghi kết thúc: ngày giờ hai zone và hành động kế (MER-STK-01 V2, MER-STK-02 V5 hay dừng).
**Hủy (V4/V6):** kiểm đã có pre-order chưa (có thì lấy quyết định fulfilment trước), rồi xóa date range, delivery date, tuần và Max PreOrder ở mọi catalog version và sync. Không đổi inStockStatus. Pre-order chỉ live khi start ở quá khứ và end ở tương lai; start tương lai thì SKU chưa vào pre-order.
**TRN-003 (TH, EPP-D2C):** hai catalog `thEstoreProductCatalog` và `thb2bProductCatalog`, kho `WC11-S501`, zone ICT. Tuần ISO: 09/11/2026 = 202646, 27/11 = 202648, 04/12 = 202649. Bảng đặt overselling start = initial end (202648/202648) phá luật +1 và không có cam kết: hỏi một lần. Sau trả lời: `WW11CGP44DSBST` 09/11 00:00 → 27/11 23:59, RDD 27/11, tuần 202646/202648/202649/202649, max 5; `QA75QN900DKXXT` tới 04/12, max 5; `QA85QN900DKXXT` max 3. Hủy `QA65QN1EHAKXXT` và `HW-LS60D/XT` ở cả hai catalog, Max PreOrder 0.
> Cột "RDD DATE" của TSE ánh xạ sang `preOrderDeliveryDate`; `preOrderRDD` trống trên el3-s2. Ghi start và end ở cả hai zone (market và GMT) trong internal check và so với export.

## Quiz (đáp án)
1 MY xin Super Sync STOCK, Stock Level preOrder 18, maxPreOrder 20 trên `SETOnline` → **C: không chạy; hỏi pre-order có kết thúc trước theo MER-STK-03 không**. 2 Super Sync RRP mới 4,990 MYR cho SKU RRP 499 → **B: dừng: tỷ lệ 10 (PS-03); hỏi một lần xác nhận RRP và NERP đã cập nhật** (price upload là MER-PRC-01 có Knox). 3 "Increase dummy qty with 1 unit" cho SKU CE Available 4, cam kết đủ → đặt **C: 5**. 4 Virtual stock đúng nhưng PDP vẫn hết hàng, Stock Level reserved 3 trên kho ảo → **B: COEC liên kết cho TEC-MON-02; không tự xóa reserved**. 5 Bảng pre-order TH: Initial End 202648 và Overselling Start 202648 → **D: hỏi trong câu gộp: overselling start phải = initial end + 1**. 6 Gõ trần pre-order 5 cho `WW11CGP44DSBST` ở đâu → **A: Stock Level › SKU + `WC11-S501` › Max PreOrder**. 7 Gỡ SKU pre-order "mọi kênh" nhưng Stock Level cho thấy đã có pre-order → **B: lấy quyết định fulfilment từ requester; dừng nếu chưa rõ**.

## Practice
**PR-MER-P1.2-1. Ticket stock** (45'; staging el3-s2, Jira SCOE; TRN-044 cộng TRN-002 hoặc TRN-003; chỉ bấm Product Sync sau comment `SYNC OK TRN044`). Làm TRN-044 trọn vẹn (triage, before export, các line được chạy, một câu hỏi cho các line còn lại, internal check, bàn giao QA). Rồi làm Part 1 của TRN-002, hoặc các line set và hủy của TRN-003. Rollback cuối. **Pass:**
- TRN-044: line 1, 2 xong; RRP `EF-XF966SBEGWW` = 379 MYR ở master, `myEstoreProductCatalog` Staged và Online, `myb2bProductCatalog`, chạy sau 18/11 00:00 MYT; PriceInfoChange kiểm sau PRICE và ghi kết quả (row VALID đi Knox); line 3, 4 không chạy (preOrder vẫn 18, RRP `SM-R420NZKAXME` vẫn 499) và gom trong một câu hỏi; ticket ON HOLD SUBS giao subsidiary.
- TRN-002: "Is blocked for Stock Import" TRUE ở mọi catalog version của ba SKU DA; Available 5/3/5 trên kho phục vụ mỗi SKU (không phải `VirtualWarehouse-my`); kho khác và reserved không đổi; overSelling 0, đã hỏi cam kết, ngày handback trong comment "Go-live schedule".
- TRN-003: ba SKU set ở cả hai catalog với Online = Staged, overselling start = initial end + 1 sau trả lời, Max PreOrder 5/5/3 trên `WC11-S501`; hai SKU hủy không còn date range, delivery date, tuần, Max PreOrder 0.
- Evidence đủ; sau rollback không còn dummy, override hay pre-order (export Backoffice sau rollback khớp export before).
Không có access: đi giấy qua MER-STK-01 V1/V3, MER-STK-02 V1, MER-STK-03 V1 với giá trị ticket; viết bảng before/after và câu hỏi gộp.
