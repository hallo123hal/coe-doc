# QA-2.2 Checking products, prices and stock in Backoffice and on the frontend

> Nguồn: page 2483258121 · 75 phút (Study 25' · Demo/thảo luận 10' · Quiz 10' · Practice 30') · Demo ngắn trên Backoffice staging + DevTools rồi thực hành cá nhân; facilitator: QA Sub-Lead cùng Market Owner · Cần xong G3.3, G5.1; tài khoản Backoffice/frontend staging như QA-2.1; Chrome/Edge trên CoE workstation để mở DevTools. Chưa có access: dùng ảnh PDP, kết quả API, bảng data in sẵn (PR-QA2.2-3 và -4 làm hoàn toàn trên giấy được).

## Mục tiêu
Dự đoán CTA khách thấy từ trạng thái SKU và xác nhận bằng PDP + ATC API; kiểm special price trên ba lớp và quy đổi validity sang GMT đúng; review price file bằng `QCL-PRC-01` + price sanity rule, bắt lỗi nhập giá theo nghìn đồng; tính sellable quantity từ Stock Level và biết field nào không sửa tay.

## Thuật ngữ
**CTA** (nút hành động trên PDP: "Buy now", "Get Stock Alert"); **ATC API** (link thêm SKU vào cart; mã trả về cho biết SKU có bán/còn hàng); **resultCode** (`0000` còn hàng, `0001` hết hàng hoặc archived); **DevTools** (F12, tab Network); **SIMPLE_INFO** (tham số API storefront trả giá, stock, sales status); **Three-layer price check** (Backoffice, simulator, storefront); **validityFrom/validityTo** (hiệu lực special price trong template, theo GMT); **PS-01…PS-14**; **Diff file** (so giá cũ/mới từng SKU, bắt buộc khi file >100 dòng); **Stock Level** (availableAmount, reserved, safetyStock, maxPreOrder, oversellingAmount, promoStockAvailable, inStockStatus); **Super Sync** (cronjob sync availableAmount từ N-ERP, sửa tay available sẽ bị ghi đè).

## Nội dung
### 1. Vì sao kiểm giá ba lớp
Backoffice cho thấy giá đã lưu; simulator cho giá cuối sau promotion; storefront cho thấy khách thật sự thấy gì ở PDP, category page, cart. Giá có thể đúng ở Backoffice mà web sai vì chưa sync, cache, hoặc promotion khác đè. Nhắc G3.3: sửa bản **Staged** rồi sync sang **Online**, web đọc Online — web không đổi thì kiểm sync trước.

### 2. Từ trạng thái SKU tới CTA, và ATC API
| SKU trên staging | CTA trên PDP | ATC API |
|---|---|---|
| Purchasable, Approved, còn hàng | Buy now | `0000` / SUCCESS |
| Purchasable, Approved, hết hàng, không pre-order | Get Stock Alert | `0001` / SUCCESS |
| Archived | Không có nút mua (Where To Buy) | `0001` / "Sorry, there is no stock…" |
| Purchasable Not Visible, Approved (gift Z-Code) | Không tìm thấy trong search | Không mua riêng được |

- VD: SKU Purchasable + Approved nhưng Stock Level trống và chưa mở pre-order → PDP "Get Stock Alert", không phải "Buy now".
- **ATC API** là cách QA kiểm nhiều SKU nhanh: mở `/<country code>/ng/p4v1/addToCart?products[0].productCode=<SKU>&products[0].quantity=1` trên staging storefront (multistore thêm `/multistore/<site>/` trước `ng`), đọc resultCode; cart kẹt thì thêm `&clearCart=true`.
- Xem data trang tải: F12 › Network › lọc Fetch/XHR; gọi `tokocommercewebservices/v2/<site>/products/<SKU>?fields=SIMPLE_INFO` xem giá, stock, salesStatus; thêm `/offers` xem benefit và promotion khả dĩ.

### 3. Special price template và QCL-PRC-01
- Mỗi dòng template có `modelCode` và chỉ **một** trong hai cột `price` hoặc `discountPercent`, không bao giờ cả hai. `cmsSite` chữ thường, phân cách dấu phẩy, không dấu cách. `validityFrom/To` format `YYYY-MM-DD HH:MM:SS` **theo GMT**.
- VD: MY bắt đầu 01-Dec 00:00 giờ MY (GMT+8) → ghi `2026-11-30 16:00:00`. ID, TH, VN là GMT+7. AU, NZ phụ thuộc giờ mùa hè.
- Điểm blocking của `QCL-PRC-01`: đúng template, market, currency, dấu thập phân; số dòng bằng brief; không trùng SKU, không ô trống/0; file >100 dòng có diff file và mỗi dòng có sanity flag có trả lời bằng văn bản của subsidiary; giá Backoffice của SKU mẫu bằng giá mới trong diff file; special price có ngày kết thúc. Một SKU sai = FAIL cả file.

### 4. Price sanity rules (PS-01…14)
Chạy hai lần: Doer chạy trên brief/file trước build, QA chạy lại cả 14 rule trên kết quả build trước PASS (MER-3.1, MR-06 §2.2). Hay gặp nhất: PS-01…04 cho price file, PS-06 và PS-08 cho promotion/coupon, PS-09 trade-in, PS-10 ngày/time zone, PS-12 store scope, PS-13 bulk file.

| Mã | Rule | Ngưỡng mặc định (đề xuất) |
|---|---|---|
| PS-01 | Giá cuối dưới sàn | Theo trang rule của market; không có thì <50% RRP |
| PS-02 | Giảm mạnh so với giá bán hiện tại | ≥20% cần xác nhận bằng văn bản |
| PS-03 | Sai bậc độ lớn (thiếu số 0, currency, dấu thập phân) | Giá mới/giá cũ <0.5 hoặc >2; khác số chữ số |
| PS-04 | Hiển thị giá phi logic | Giá bán > RRP; giá gạch ngang < giá bán; giá 0 hoặc trống |
| PS-05 | Discount ngoài khoảng của category | Không có khoảng thì ≥30% là hold |
| PS-06 | Stacking, xung đột promotion | Stacking không có trong brief là hold |
| PS-07 | Quà giá trị cao | Landed cost ≥100 USD: xác nhận và tính exposure |
| PS-08 | Coupon | Vượt cap; không giới hạn tổng; thiếu giới hạn/khách khi brief đòi |
| PS-09 | Trade-in, overtrade | Cao hơn bảng giá partner đã xác nhận |
| PS-10 | Ngày, giờ, time zone | Ngày đã qua; dài hơn 90 ngày; thiếu hoặc sai time zone |
| PS-11 | Freeze, BVT | Đổi trong freeze không có bằng chứng duyệt; phụ thuộc enhancement chưa BVT sign-off |
| PS-12 | Store scope, số market | Phải khớp brief; >5 market là E4 |
| PS-13 | Bulk file | >100 dòng cần diff file; không trùng SKU, không ô trống |
| PS-14 | Virtual stock, pre-order | ≥500 unit, hoặc vượt mức subsidiary cam kết |

Cái bẫy kinh điển: file ghi 25,990 thay vì 25,990,000 (nhập theo nghìn đồng) — PS-01, PS-02, PS-03 và diff file đều bắt được.

### 5. Stock Level
Base Commerce › Stock Level, mỗi kho một dòng. **availableAmount** (đồng bộ từ N-ERP bởi Super Sync), **reserved** (giữ cho order chưa ship), **safetyStock** (giữ lại không bán), **maxPreOrder** (slot pre-order), **oversellingAmount** (được bán vượt tồn, Hybris không ghi đè), **promoStockAvailable** (giữ cho quà promotion), **inStockStatus** (NOTSPECIFIED, `FORCEINSTOCK` luôn hiện còn hàng, `FORCEOUTOFSTOCK` luôn hiện hết hàng).
**Sellable = available − reserved − safetyStock** (VD 40 − 12 − 5 = 23). Mở pre-order bằng `maxPreOrder` sau khi chặn stock import; **không sửa available trực tiếp** vì Super Sync ghi đè. Cập nhật stock luôn được phép, kể cả lúc freeze.

### 6. Z-Code, F-Code, customer journey, test order
- Gift Z-Code (`QCL-PRD-02`): không tìm được trong search, không mua riêng, chỉ đi kèm main device. F-Code: đúng thành phần, số lượng, giá bundle. Quà có cost ≥100 USD cần tính exposure (PS-07).
- Kiểm theo customer journey 4 bước: list/PDP → add to cart → checkout tới trước thanh toán → ghi evidence. Dùng cho sản phẩm mới, SC+, trade-in, mọi promotion.
- Chỉ đặt test order khi runbook market cho phép; trước đó kiểm Product Warehouse Map và tồn đúng kho. Map sai thì ERP trả "Material … does not exist in storage location …".

## Quiz (đáp án)
1 Coupon 30 USD, 1 lần/khách, total trống, hiệu lực 01/12/2026–31/03/2027 → **C: PS-08 và PS-10** (không giới hạn tổng + >90 ngày). 2 MY bắt đầu 00:00 01/12/2026 giờ MY → validityFrom **A: 2026-11-30 16:00:00**. 3 available 40, reserved 12, safetyStock 5 → bán được **B: 23**. 4 Giá cũ 25,990,000 → mới 25,990 → **D: PS-01, PS-02, PS-03**. 5 Giá Backoffice đúng nhưng PDP staging vẫn giá cũ → **B: kiểm Staged đã sync sang Online chưa**. 6 Template một SKU điền cả price lẫn discountPercent → **A: Defect, mỗi dòng chỉ dùng một cột**. 7 Gift Z-Code hiện trong search → **C: Defect, phải ẩn khỏi search**.

## Practice
- **PR-QA2.2-1** (10'): 3 SKU `vn` (còn hàng, hết hàng không pre-order, archived). Mỗi SKU: Catalog › Products › child catalog B2C, bản Online → ghi Sales status, Approval; Stock Level ghi available; dự đoán CTA theo bảng; mở getcookie.html, PDP, link ATC, ghi resultCode. Pass: dự đoán khớp thực tế cả 3 hoặc giải thích được lệch (chưa sync, cache); có ảnh PDP + resultCode mỗi SKU.
- **PR-QA2.2-2** (8'): facilitator tạo SPECIAL price row bản Staged cho 1 SKU `vn`, thấp hơn RRP 10%, hiệu lực từ ngày mai, internal check ghi giá + ngày giờ ICT. Bạn đọc price row ở Staged và Online trước/sau sync, quy đổi validity sang GMT (ICT − 7h), chạy PS-01…04, xem giá bán và giá gạch ngang ở PDP. Pass: ảnh trước/sau sync; GMT đúng; kết luận PASS/FAIL theo `QCL-PRC-01`; facilitator xóa row và sync lại sau bài.
- **PR-QA2.2-3** (6', giấy): diff file VN 5 dòng: DEMO-01 25,990,000→23,990,000; DEMO-02 25,990,000→25,990; DEMO-03 8,490,000→6,490,000; DEMO-04 3,990,000→9,990,000; DEMO-05 1,290,000→1,190,000. Pass: DEMO-02 vi phạm PS-01/02/03 (nhập theo nghìn đồng); DEMO-03 giảm 23.6% → PS-02, cần trả lời bằng văn bản của subsidiary; DEMO-04 tỷ lệ >2 → PS-03, cần xác nhận; DEMO-01 và DEMO-05 không flag. Kết luận FAIL cả file vì DEMO-02 sai; mã DEMO-02 là `RC-ENT` hoặc `RC-FIL` (đáp án tham khảo, Lead xác nhận).
- **PR-QA2.2-4** (6'): đọc Stock Level SKU được giao ở mỗi kho: available, reserved, safetyStock, maxPreOrder, oversellingAmount, promoStockAvailable, inStockStatus; tính sellable; trả lời: mở 200 slot pre-order đổi field nào, luôn hiện còn hàng dùng giá trị nào, vì sao không sửa available tay. Không lưu. Pass: tính đúng; trả lời `maxPreOrder` (sau khi chặn import), `FORCEINSTOCK`, Super Sync ghi đè available. Không có access: dùng số 40/12/5.
