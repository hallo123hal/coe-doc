# MER-P1.1 SKU status by channel, CTA, block stock, delivery mode

> Nguồn: page 2484175242 · 120 phút (Study 30' · Demo 20' · Quiz 10' · Practice 60') · Thực hành trên staging + practice ticket; facilitator: Shift Leader/Sub-Lead · Capabilities C2, C4 · Cần xong MER-2.1 và MER-1.3 (L1). Mang TRN-001 (SCOE-7) và TRN-007 (SCOE-13) + log before/after TRN-001. Truy cập staging Backoffice el3-s2, Jira SCOE, Confluence; **Merch không có HAC** — kiểm bằng Advanced Search và Export. Staging dùng chung với BVT: chỉ đổi SKU pool được giao, ghi before, rollback, không chạy cronjob, ImpEx để Tech. Không có access: dùng ảnh MER-PRD-01, làm Checker trên giấy.

## Mục tiêu
Tách ticket SKU hỗn hợp thành action line và route sang MER-PRD-01, MER-STK-01, MER-STK-02, MER-DLV-01; map "D2C", "EPP", "all sites", danh sách 30 site ID sang đúng child catalog và hide/unhide/archive chỉ ở đó; dự đoán CTA từ salesStatus, approvalStatus, stock rồi chứng minh bằng storefront + add-to-cart; block/unblock stock import có ghi before, biết khi nào cần RHQ approval hay hỏi trước; thêm/bớt delivery mode trên SKU ở mọi catalog trong scope và kiểm mode đã active trên site.

## Thuật ngữ
**Action line** (một dòng việc: một SKU, một catalog, một action; TRN-001 có 5 hide, 6 unhide, 2 block, 1 unblock); **Shared catalog** (một child catalog phục vụ nhiều site; status ở `myb2bProductCatalog` áp cho cả 19 EPP site MY); **Where to buy** (CTA khi PURCHASABLE nhưng unapproved; VN "Mua ở đâu", không mua online được); **ATC resultCode** (`0000` active và còn hàng; `0001` + "Sorry, there is no stock for this product." = archived/không mua được); **Is blocked for Stock Import** (`blockStockUpdatesFromExternalSystems`; TRUE thì NERP import không ghi đè stock SKU); **GSCM Sync block-flag rule** (RHQ: SKU MX giữ 4 block flag FALSE; TRUE cần RHQ D2C Platform duyệt, ticket ở ON HOLD RHQ); **Deliverable mode** (mode có trên SKU và active trên site; không có thì checkout không có option giao — KE-MER-DLV-01-01).

## Nội dung
### 1. MER-PRD-01 trong một lượt
MER-PRD-01 là service SKU bận nhất (~246 ticket/tháng): V4 file status định kỳ ~37%, V1 đăng ký ~12%, V3 archive/hide ~11%; V2 activate nằm trong file V4. Priority Low: 24h, initial response 2h (APPROVED-ES → STG SETUP). High (4h) chỉ qua MER-INC-01 khi status sai đang live gây thiệt hại >10,000 USD. Standard change, không PC ticket; Normal change có Sub-Lead review khi archive nguyên category, >200 dòng SKU-catalog (ngưỡng BiPlus, runbook còn ghi mở) hoặc đổi base product/product type SKU live.
Trước hết tách action line: line pre-order → MER-STK-03; virtual stock và block → MER-STK-02/01; delivery text → MER-DLV-02. Từ mơ hồ ("remove", "block stock") gom vào một câu hỏi.
| Bước | Doer | Checker |
|---|---|---|
| 1. Tách và map | Một line mỗi SKU, catalog, action; route stock/pre-order | Mỗi line một kết quả (done, routed, blocked); line routed có link |
| 1. Dependency (V3) | Tìm F-code, quà/add-on reference, promotion đang chạy, lọc theo promotion group của site | Requester đã được báo trước khi archive |
| 1. Before export | Catalog › Products › Export Excel/CSV (approval, sales status mỗi catalog version) | File before mỗi catalog đã đính |
| 1. Áp dụng ở child Staged | Approval và Sales Status mỗi line; Bulk Edit hoặc Update Sales Status cho danh sách | After khớp từng dòng; không SKU/catalog ngoài yêu cầu bị đổi |
| 1. Sync | Staged → Online, mỗi catalog | Online = Staged |
| 1. Storefront | Chờ index và cache, PDP + add to cart một site mỗi loại catalog | Mẫu mỗi loại catalog |
| 1. Bàn giao | Internal check line "Matches approved brief" | Khớp brief |
Known error: KE-04 activate nhưng không mua được (chưa sync, index pending, hết stock, bị loại trừ, thiếu delivery mode — kiểm theo thứ tự); KE-05 sau hide vẫn hiện trên D2C (chỉ đổi một catalog); KE-09 Bulk Edit bỏ SKU (khoảng trắng trong mã: trim và so số dòng); KE-10 line pre-order bị đặt thành activation.

### 2. Channel → catalog
"Channel" là child catalog, không phải flag. Đổi salesStatus và approvalStatus ở bản **Staged** của từng child catalog trong scope rồi sync Online; sửa Online trực tiếp không phải đường chuẩn. Trên el3-s2 master VN chỉ có Staged; child có Staged và Online. STG SETUP là Jira status: ticket thật làm trên production Backoffice. Status ở shared catalog áp cho mọi site của nó: áp **theo catalog, không theo tên site**; ẩn một site là MER-MST-02.
**TRN-005 (MY archive):** requester liệt kê Shopee, TikTok, Lazada, `mysmeProductCatalog`, 19 EPP site, 9 EA site cho SKU `SM-S948BLBQXME`, `EF-XF966SBEGWW`.
| Nhóm trong ticket | Catalog trên el3-s2 |
|---|---|
| eStore (`my`) | `myEstoreProductCatalog` |
| 19 EPP site (VD `eppsme`) | `myb2bProductCatalog` |
| `mysmeProductCatalog` | catalog SME |
| Shopee, Lazada, TikTok | catalog 3PD MY |
| 9 EA site | catalog mặc định mỗi site (EA đọc catalog B2B) |
| Không có trong ticket | `myProductCatalog` = master, chỉ Staged: không đổi sales status |
Chỉ đổi catalog có SKU; catalog khác ghi "not registered in [catalog]". SKU là đích của reference đang active hoặc trong promotion đang chạy thì hỏi trước khi archive.
**"All sites" ở VN (TRN-007):** D2C `vnEstoreProductCatalog`, EPP `vnProductCatalog` (default của site `savina`), `vnEppProductCatalog`, `vnsmeProductCatalog`, `vn3pdProductCatalog`, `vnRefurbishedProductCatalog`, EaRetail. 3PD và Refurbished có process riêng: SKU ở đó thì hỏi "all sites" có gồm không (đáp án lab: không gồm marketplace).

### 3. Status → CTA: dự đoán rồi chứng minh
| Sales status | Approval | Điều kiện khác | CTA |
|---|---|---|---|
| PURCHASABLE | approved | còn hàng | Buy now |
| PURCHASABLE | approved | trong cửa sổ pre-order | Pre-order now |
| PURCHASABLE | approved | hết hàng | Notify me / Get stock alert |
| PURCHASABLE | unapproved | – | Where to buy (VN "Mua ở đâu"), không mua được |
| ARCHIVED | check hoặc unapproved | – | eStore: không CTA; EPP: không tìm thấy SKU |
| – (trong AEM, không Hybris) | – | – | Coming Soon |
Cặp chuẩn: activate = approved + PURCHASABLE; archive = check (hoặc unapproved) + ARCHIVED. Vài loại SKU khác (KB "Product Active/Archive"): quà Z-code active = PURCHASABLE_NOT_VISIBLE + approved; SKU trade-in T-code giữ ARCHIVED. Chứng minh CTA hai cách: PDP và kết quả add-to-cart.
**TRN-007 item 4:** "HW-S800B/XV → hiện 'Mua ở đâu' chỉ D2C": ở `vnEstoreProductCatalog` Staged đặt approval `unapproved`, giữ PURCHASABLE, không đụng EPP. Đặt ARCHIVED là lỗi kinh điển (RC-ENT). `QA85LS03BAKXXV` unhide với stock 0 nên "notify khi có hàng" là đúng — nói trong reply. TRN-004 cùng bẫy (`SM-X610NLIAXTC`, `SM-R900NZAAASA`): báo trong ghi nhận và vẫn làm.
> **SKU embargo trước go-live (MER-PRD-01 V1 bước 12):** giữ check hoặc unapproved + ARCHIVED tới khi requester (flagship: RHQ) báo go-live. Approved + PURCHASABLE_NOT_VISIBLE trước launch chỉ khi subsidiary đồng ý bằng văn bản để QA test promotion. Cặp bất thường (unapproved + Purchasable ở TRN-010) hỏi trong câu hỏi gộp.

### 4. Block và unblock stock import
"Block stock" ở ticket SAVINA nghĩa là flag **Is blocked for Stock Import** (`blockStockUpdatesFromExternalSystems`): TRUE thì NERP import không ghi đè stock SKU. Có ba flag liên quan (GSCM Stock Import, Updates from External Systems, Status Update from External System).
- **CE hay MX trước:** SKU CE có virtual (dummy) stock, flag TRUE là bước setup bình thường (MER-STK-02). **Luật RHQ GSCM Sync:** SKU MX bốn flag đều FALSE; đặt TRUE cần RHQ D2C Platform duyệt — không có reference duyệt trên ticket thì chuyển ON HOLD RHQ. SAVINA (VN) có duyệt PUMI không dùng GSCM.
- **Mơ hồ:** "block stock" có thể là "block và giữ stock" hoặc "block và đặt 0". Xem trang market rules VN, không thì hỏi một lần và làm tiếp các line khác.
- **Ở đâu:** đặt flag trên SKU ở master catalog (tab Administration) rồi sync xuống child. Kiểm flag ở mọi catalog version (tab Administration hoặc Backoffice export). Unblock = FALSE ở mọi catalog version.
**Unblock = trả về cho NERP** (MER-STK-01 V2): flag FALSE, không còn virtual quantity hay override, kiểm reserved (reserved stock kẹt: COEC cho TEC-MON-02, Merch không bao giờ tự xóa). Trên production stock theo NERP từ lần import kế (`<cc>-tokoStockImportUpdateJob`, ~mỗi 30') hoặc Super Sync STOCK; trên staging chỉ ghi chú.
**TRN-001:** làm item 1, 2, 4; hỏi item 3: "(a) block import và giữ stock hiện tại, hay (b) block và đặt stock 0". Đáp (a): ghi stock ở Base Commerce › Stock Level, đặt flag TRUE cho `SM-X710NZAAXXV`, `SM-X510NZSAXXV` ở `vnMasterProductCatalog` Staged (trainer đóng vai RHQ duyệt); stock giữ 105 và 32. Unblock `SM-R630NZAAXXV` và không đụng flag GSCM (lỗi của TRN-007).
> 3,443 SKU eStore VN Online trên staging mang TRUE. Đừng bắt chước. CE: TRUE ở master rồi sync là bình thường cho virtual stock. MX: FALSE trừ khi có reference RHQ duyệt; hỏi Shift Leader trước khi flag MX thành TRUE.

### 5. Delivery mode và installation trên SKU (MER-DLV-01)
~20 ticket/tháng (TH nhiều nhất); V2 set mode cho SKU mới, V1 đổi cho SKU có sẵn. Mode/phí/base cost mới (TEC-CFG-02) hay mode thiếu trên site (TEC-SIT-05) là việc Tech: COEC liên kết, ticket Merch ON HOLD COE, không bao giờ hỏi subsidiary.
V1 ca thường: (1) xác nhận từng mã có trên site và active: Base Commerce › Base Store › (store) › Administration › Delivery Modes; mức site ở WCMS › Website › (site) › Administration; multistore nếu có; Is Active ở Price Settings › Delivery Costs (site lấy danh sách từ multistore, không thì website, không thì base store); (2) export before (deliveryModes mỗi SKU, catalog, version); (3) mở SKU ở Staged › Administration › Delivery Modes thêm/bớt; danh sách dùng Bulk Edit › Delivery Modes › "Append to existing". **Luôn tick Append khi thêm: không tick thì mọi mode hiện có bị thay bằng mode mới.** Không có template bulk upload cho delivery mode; ImpEx production là Tech (COEC + PC ticket); (4) lặp cho mọi catalog: B2C, EPP, SMB, EA, 3PD tách riêng, Staged và Online khác nhau mỗi catalog; (5) sync lúc go-live, rồi checkout với postcode trong vùng PINMAP.
Staged `th-delivery-bkk-AC-calendar` khác Online `th-delivery-standard-ce` = chưa sync (KE-03). Site 3PD chỉ dùng mode marketplace (`th-marketplace-delivery-standard`). Installation (V3) phải hiện đúng một cart line (hai line: KE-02; service flag là Tech, chỉ đọc). Free delivery/installation (V4) là promotion rule có Knox và QA 100%.
> VN (SAVINA): mode set theo SKU và catalog, theo danh sách PIC SAVINA. Gán theo category trong KB "Delivery mode documentations…" (2025-10) không còn áp dụng (MER-DLV-01, handover Flagship 30/10). SKU pool trên staging cho thấy: `vn-ce-parcel-express(-d2c)` ở mức product trong mọi catalog VN.

## Quiz (đáp án)
1 PH dòng "Deactivate" `EF-RX510CBEGWW` trên "both ESTORE & EPP Catalog" → **B: check + ARCHIVED trong `phEstoreProductCatalog` và `phEppProductCatalog` Staged rồi sync từng cái**. 2 VN "HW-S800B/XV → hiện 'Mua ở đâu' chỉ D2C" → **A: approval unapproved, sales status giữ PURCHASABLE, chỉ catalog D2C** (ARCHIVED là RC-ENT). 3 MY archive ghi 19 EPP site ID, bao nhiêu catalog → **C: một — `myb2bProductCatalog`**. 4 TRN-001 item 3 "Block stock" cho hai tablet, market rules VN không định nghĩa → **B: làm item 1, 2, 4; hỏi một lần giữ hay đặt 0; ON HOLD SUBS giao subsidiary**. 5 Unblock stock import một SKU trên staging, requester hỏi bao giờ stock mới hiện → **D: từ lần NERP import kế (~30') hoặc Super Sync STOCK trên production; trên staging không chạy job**. 6 Sau activate `SM-X610NLIAXTC` hiện "Get stock alert" trên `ph`, stock pool 0 → **B: đúng hành vi: approved + PURCHASABLE không stock; lẽ ra phải báo requester**. 7 Ticket delivery mode TH xin `th-delivery-standard-ce` cho 4 SKU nhưng mã chưa active trên base store `th` → **C: COEC liên kết cho TEC-SIT-05, ticket Merch ON HOLD COE, báo requester**.

## Practice
**PR-MER-P1.1-1. Hai ticket SAVINA** (70'; staging el3-s2, Jira SCOE; TRN-001 và TRN-007 với giá trị pool VN; chung `QA85LS03BAKXXV` nên trainer đổi một SKU nếu chạy cùng lúc). Làm cả hai ticket một mình như Doer (triage, action line, câu hỏi làm rõ, before log, setup ở child Staged, sync, internal check line). Đổi với partner làm Checker bằng export Backoffice theo catalog version (Catalog › Products › Export; flag ở tab Administration). Rollback. **Pass:**
- TRN-001: 5 hide line (D2C: `SM-S928BLBQXXV`, `SM-S928BLBWXXV`, `EP-T1510NBEGWW`; EPP `vnProductCatalog`: hai SKU S928) = check + ARCHIVED; 6 unhide line (`SM-W620NZKAXXV`, `QA85LS03BAKXXV`, `SM-R800NZSAXXV` trên D2C và EPP) = approved + PURCHASABLE; `EP-T1510NBEGWW` vẫn PURCHASABLE trên EPP; một câu hỏi về "block stock" với lựa chọn (a)/(b), ON HOLD SUBS giao subsidiary; sau đáp (a): flag TRUE trên `SM-X710NZAAXXV`, `SM-X510NZSAXXV` stock không đổi (105 và 32), flag FALSE trên `SM-R630NZAAXXV`; reply nêu hai SKU unhide stock 0 hiện "Get stock alert".
- TRN-007: ba TV ARCHIVED ở mọi catalog trong scope nhưng không 3PD (sau câu hỏi marketplace); `QA85LS03BAKXXV` approved + PURCHASABLE; `HW-S800B/XV` unapproved + PURCHASABLE chỉ D2C, EPP không đổi; `HW-T420/XV`, `HW-Q600C/XV` flag block FALSE, không đổi flag GSCM.
- Online = Staged mọi line đã đổi; before/after ghi lại; internal check line trên mỗi ticket; không chạy cronjob; rollback xong và export Backoffice sau rollback khớp export before.
Không có access: dùng ảnh MER-PRD-01; viết bảng action-line cho hai ticket với giá trị before và target mỗi catalog, làm bước Checker trên giấy theo tiêu chí trên.
