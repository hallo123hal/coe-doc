# MER-2.1 Product: SKU setup, flags, product references, add-on, benefit

> Nguồn: page 2483224910 · 90 phút (Study 25' · Demo 12' · Quiz 8' · Practice 45') · Facilitator demo từng thao tác trên Backoffice staging; learner làm cặp (một người thao tác, một người đối chiếu worksheet); facilitator: Sub-Lead/Market Owner certified PRD & PRF.
> Cần xong G3.3, G5.1, MER-1.3. Dùng account staging s2 có quyền edit child catalog `vn` B2C (Staged) + Product Cockpit. Lead chưa xác nhận learner có tự sync 1 SKU được không (KB Product Price nói sync được từng sản phẩm); không sync được thì facilitator chạy, bạn kiểm. **Luật staging G5.1 áp dụng cả MER-2:** chỉ đổi object mình tạo/được giao, tiền tố `TRAINING_<NAME>_`, không cronjob/ImpEx/Initialization/Update, không sync cả catalog version, screenshot đưa thẳng vào ticket training/trang bài tập và xóa bản local. Facilitator chuẩn bị 1 SKU điện thoại training/learner (Normal, Approved, Purchasable, không phải flagship embargo) + 1 SKU ốp lưng cùng model.

## Mục tiêu
Tạo/kiểm/xóa product reference ở Staged child catalog và xác minh Online sau sync; điền đúng 1 dòng benefit PDP trong template PRODUCT_BENEFITS và nhận flag sai guideline; kiểm `AEM_` category của SKU và nêu cách thêm SKU vào add-on page; chọn đúng field Stock Level cho pre-order/overselling/quà/always-in-stock và chặn import trước khi nhập tay; áp dụng luật RHQ về SKU mới, flag, GSCM flag, benefit, add-on page, backorder, Ring kit, auto-add và nhận ra request phải từ chối.

## Thuật ngữ
**PRODUCT_REFERENCES** (template bulk upload ở Product Cockpit: SourceCode, ReferenceType, Active, targetCode, start/endDate); **PRODUCT_BENEFITS**; **Benefit BC / PD / Cart** (dòng benefit trên Buying Configurator / PDP / giỏ; cart benefit chỉ là thông tin, không lưu vào order); **DO_NOT_DELETE** (benefit do RHQ quản — CoE không sửa/xóa); **Supercategory `AEM_…`** (quyết định SKU hiện ở tab nào của add-on page; 1 SKU tối đa 1 `AEM_`); **APPEND** (upload thêm vào cuối list, không ghi đè); **Backorder** (cho đặt khi hết hàng trong N tuần rolling); **OLD Hybris / NEW Hybris** (nước quản flag ở Hybris: AU, NZ, SG, MY, TH, VN / nước quản flag ở AEM: ID, PH); **`promoStockAvailable`**; **Stock Level File Upload** (file `XX-prod_StokLevel`); **GSCM flags** (4 flag chặn cập nhật từ hệ thống ngoài; với SKU MX phải FALSE).

## Nội dung
### 1. Tạo SKU mới và status khởi đầu
Tạo SKU bằng upload = bước "create SKU" trong 8 bước ở G3.3. Template ở Product Cockpit › Product, đặt tên `<cc>ProductCatalog`, 4 cột: ModelCode, ModelName, Category, Unit. Sau import: Super Sync (DOTCOM, PRICE, STOCK, IMAGE), approve, sync Master → Staged child → Online; **active base code trước, rồi mới SKU**. Chỉ nhận template SKU Registration mới nhất của RHQ; file subsidiary sai thì trả lại, không tự sửa. Status khởi đầu bổ sung cho bảng G3.3: Z-code quà = Purchasable Not Visible + Approved; F-code = Purchasable; **SKU 3PD mới = UNAPPROVED + ARCHIVED**, chỉ chuyển APPROVED/PURCHASABLE khi có Jira ticket yêu cầu. Lỗi hay gặp: sửa ở Master hoặc Online thay vì Staged child; quên sync.

### 2. Stock do Merch quản
`availableAmount` được Super Sync copy từ N-ERP — không sửa tay; cần nhập tay thì **chặn stock import trước** (Stock Import Override hoặc Block stock import), nếu không cronjob ghi đè; với SKU MX bật flag chặn import cần RHQ duyệt. Bulk upload bằng nút "Stock Level File Upload" ở Base Commerce › Stock Level, file `XX-prod_StokLevel` (VD `PH-prod_StokLevel`). Pre-order và overselling không sync từ GERP nên phải upload; một sản phẩm chỉ theo một flow (pre-order bật thì overselling vô hiệu).
**4 GSCM flag của SKU MX phải FALSE:** Block Status Update from ExternalSystem, Block Updates from External Systems, Is blocked for Stock Import, Is blocked for GSCM Stock Import; đặt TRUE cần RHQ D2C Platform duyệt; stock override chỉ cho ID và PH với SKU CE (06 GSCM Sync).

| Field Stock Level | Dùng khi | Ví dụ |
|---|---|---|
| `safetyStock` | giữ lại một phần không bán | Sellable = available − reserved − safetyStock |
| `maxPreOrder` | giới hạn slot pre-order | mở 200 slot |
| `oversellingAmount` | cho bán vượt tồn; Hybris không ghi đè | oversell 50 máy |
| `promoStockAvailable` | giữ tồn quà trong bundle; free gift CHECK_PROMO_STOCK đọc field này | giữ 500 tai nghe làm quà |
| `inStockStatus` | ép FORCEINSTOCK / FORCEOUTOFSTOCK | Knox Manage luôn còn hàng |

### 3. Product reference
Nối SKU này với SKU khác (VD điện thoại → ốp lưng). Luôn tạo ở Staged child catalog rồi sync; tạo tay ở tab References hoặc bulk PRODUCT_REFERENCES; có start/end date; cronjob dọn reference hết hạn/inactive.

| Cần | ReferenceType |
|---|---|
| Gợi ý ốp/sạc | ACCESSORIES |
| SC+ khách tự thêm, T-Code trade-in, SIM plan, Knox Manage | AVAILABLE_SERVICE (SC+ bắt buộc: AUTO_ADDED_SERVICE) |
| Lắp đặt tủ lạnh MY tự vào giỏ; AC dàn lạnh + dàn nóng | MUST_PURCHASE_WITH |
| TV kèm SKU lắp đặt; quà FOC trong bundle | CONSISTS_OF |
| Mua điện thoại tặng tai nghe giá tốt (PWP) | SELECTION_OF_BUNDLE |
| "Frequently Bought Together" trên trang BC | SELECTION_OF_RECOMMEND |
| Chọn quà trên add-on page | SELECTION_OF_GIFT (cần thêm AEMAdditionalInfoTypeData, MER-2.5) |
| Mini add-on cho VD | DISPLAY_OF_PDP |

### 4. Add-on page — được thêm, không được bỏ sót
Mỗi flagship có hướng dẫn add-on page từ HQ (~5 tab bắt buộc, mỗi tab có SKU bắt buộc). Thêm SKU vào supercategory `AEM_…`: mở category ở Master → Download Excel làm backup → thêm SKU **vào cuối list** → Upload Products ở chế độ **APPEND** → sync Online. Không cho 1 SKU >1 `AEM_` category (sẽ hiện 2 lần). Không dùng DA mini add-on để hiển thị SKU MX.

### 5. Flag và benefit
- **Merchandising flags** (06 Flags, 06 Merchandizing Flags): chỉ dùng màu HEX thương hiệu — New #2189ff, Hot #EF3434, Best Seller #F66700, User Key-In #00838F; **tối đa 18 ký tự**; không số (AEM không hiện), không dấu phẩy, không HTML. Flag Hybris áp dụng cho nước OLD Hybris; ID và PH quản flag ở AEM; có cả AEM và Hybris thì Hybris thắng, chỉ hiện 1 flag.
- **Benefit** (06 Benefits 2025): BC page hỗ trợ HTML, dùng field Description; PD là 1 dòng, không HTML/ảnh, dùng field Title; text ≤62 ký tự (có CTA ≤53). Benefit "Offers" của AEM trên BC page ngừng dùng từ 25/06/2026. **Cột `site` của PRODUCT_BENEFITS không được trống** (trống = hiện ở mọi nước cùng cluster). Dòng PDP: `code` bắt đầu bằng mã nước (VD `NZ_B2C_NZHME9924_PD_A56A36_NZD80`), ngày giờ theo UTC; showOnPDP=TRUE, showOnPLP=FALSE, showOnCart=FALSE, productsAction=APPEND, isNewDescription=TRUE; priority cao hiện trên; PD chỉ hiện 2 benefit. Upload xong vào Administration Cockpit, tìm "benefit", so số dòng với file. **Không sửa/xóa benefit DO_NOT_DELETE** (RHQ quản).

### 6. Luật RHQ: từ chối gì, risk tier, QA gate
- Auto-add vào giỏ chỉ cho item **FOC**; RHQ Legal cấm auto-add hàng có giá, kể cả 1 USD. **Không tắt backorder** (rolling 6 tuần; ngoại lệ duy nhất Store Pickup có timeslot, hiện TH). Chỉ TH và MY được bán Ring Sizing Kit riêng.
- Risk/QA gate: PRD-01…03 R2 Sampling; PRD-04 Z-code R2 Mandatory; PRD-05 F-code R3; BYP-01 add-on R2 Sampling; flag & text R1; PRF-04 R2 Mandatory; PRF-05 PWP R3. Product setup không qua Knox.
- Tóm tắt lỗi hay gặp: sửa Master/Online thay vì Staged child; quên sync; nhập stock tay trước khi chặn import; `site` benefit trống; flag có số; SKU nằm 2 `AEM_` category.

## Quiz (đáp án)
1 Flag đúng guideline → **"Hot Deal"**. 2 Bulk upload PDP benefit để trống `site` → **hiện ở mọi nước trong cluster**. 3 Subsidiary muốn tự thêm cáp sạc 1 USD vào giỏ → **từ chối: auto-add chỉ cho FOC**. 4 MY: dịch vụ lắp đặt tự vào giỏ cùng tủ lạnh → **MUST_PURCHASE_WITH**. 5 SKU thuộc 2 `AEM_` category hiện 2 lần → **giữ 1 category, bỏ cái kia, sync** (không bỏ cả hai vì sẽ làm mất SKU bắt buộc). 6 SKU mới cho catalog 3PD → **UNAPPROVED + ARCHIVED**. 7 Sửa text benefit DO_NOT_DELETE → **không sửa; chuyển RHQ**. 8 Giữ 500 tai nghe làm quà → **`promoStockAvailable`**.

## Practice
- **PR-MER-2.1-1** (giấy, 9'): TH ra mắt điện thoại 3 màu × 2 dung lượng (6 SKU), có embargo, trade-in, SC+ khách tự thêm, ốp gợi ý, special price 2 tuần. Pass: trước launch SKU ở Purchasable Not Visible + virtual stock được subsidiary xác nhận, chưa bật Purchasable sớm; T-Code & SC+ dùng AVAILABLE_SERVICE, ốp dùng ACCESSORIES; các bước gồm sync Master → Staged child → Online và kiểm PDP.
- **PR-MER-2.1-2** (staging, 14'): tìm SKU training, mở dòng child catalog `vn` B2C **Staged** (không Master/Online), ghi số reference hiện có + screenshot (before); tạo reference ACCESSORIES → SKU ốp, Active, end date +2 ngày, Save; sync (bạn hoặc facilitator, không sync cả catalog); kiểm bản Online có reference; **dọn**: xóa reference ở Staged, sync lại, kiểm đã biến mất. Pass: tạo ở Staged; Online khớp sau sync; có screenshot before/after; số reference sau dọn = before. Không có access: xem demo và điền 1 dòng PRODUCT_REFERENCES trên giấy.
- **PR-MER-2.1-3** (10'): (a) tìm lỗi 5 flag — "Save 20%" (có số), "Free gift, limited" (có dấu phẩy), "Exclusive online bonus offer" (>18 ký tự), "<i>New</i>" (HTML), "Hot Deal" (đúng) → 4 sai; (b) tải template PRODUCT_BENEFITS (chỉ tải, không Import), điền 1 dòng PDP cho SKU training: code bắt đầu `VN_`, site `vn`, hiệu lực từ 01/12/2026 00:00 ICT viết theo UTC = **30/11/2026 17:00 UTC** (Lead xác nhận format cột ngày), showOnPDP=TRUE…, text tiếng Anh ≤62 ký tự (đã đếm).
- **PR-MER-2.1-4** (5'): mở SKU flagship có add-on page ở Master, tab Categories, đếm category bắt đầu `AEM_` (phải đúng 1, nếu khác thì báo); tìm nút Download Excel/Upload Products (không bấm); viết 4 bước thêm 1 SKU: backup → thêm cuối list → APPEND → sync Online.
- **PR-MER-2.1-5** (7'): (a) Stock Level: available 40, reserved 12, safety 5 → bán được **23**; mở 200 slot pre-order bằng **`maxPreOrder`** (sau khi chặn import; sửa available sẽ bị Super Sync ghi đè); oversell 50 máy bằng **`oversellingAmount`** (không bị ghi đè); Knox Manage luôn còn hàng = `inStockStatus` FORCEINSTOCK; giữ 500 tai nghe làm quà = `promoStockAvailable`; file stock PH = `PH-prod_StokLevel` + nút Stock Level File Upload. (b) mở Stock Level của SKU training, ghi 6 field mỗi kho, phân biệt field cronjob ghi và field Merch quản; không Save.
