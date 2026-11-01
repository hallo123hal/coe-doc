# TEC-3.2 Integration, external services and 3PD middleware

> Nguồn: page 2483191937 · 75 phút (Study 25' · Demo 15' · Quiz 10' · Practice 25') · Lecture + đọc KB có hướng dẫn + bài phân loại lỗi; facilitator: PIC 3PD hoặc Tech Sub-Lead · Cần xong G3.2, G4.2, TEC-2.3, TEC-3.1. Backoffice + HAC staging cho bài kiểm cấu hình; không cần quyền Logicbroker (xin qua AUTEU khi được giao 3PD).

## Mục tiêu
Vẽ bản đồ tích hợp: kênh bán, middleware, Hybris, NERP, payment gateway, service partner, kho; phân loại lỗi Logicbroker theo 4 mức và nêu ai sửa; giải thích cấu hình trade-in, overtrade, SC+ và các status clawback; nêu ranh giới việc của PIC 3PD và Level 1, loại duyệt cho thay đổi data 3PD.

## Thuật ngữ
**Logicbroker (LB)** (một trong 4 middleware nối Hybris với marketplace: Lazada, Shopee, TikTok, eBay, Woolworths…); **SamsungBifrost API** (API LB gọi vào Hybris để đẩy order); **Custom Lookup** (bảng tra trong LB, VD mã ISO region, cách tách SKU bundle); **LB error levels L1–L4** (KB 3PD nhóm lỗi theo người sửa — *không phải* certification L0–L3 hay Samsung L2/L3; viết đầy đủ "LB error level L4"); **External Service Type** (loại add-on phải khai báo trên mỗi nước: ACCESSORIES, BENEFIT, TRADE-IN…); **T-SKU** (SKU máy cũ do partner trade-in cung cấp, cronjob tạo); **AssessmentCriteria / AssessmentCriteriaAnswer** (câu hỏi đánh giá máy cho trade-in); **Clawback status** (NEW, WAIT, RECEIVED, CANCELED, TRADEIN_TIMEOUT, CLOSED, COMPLETED).

## Nội dung
### 1. Bản đồ tích hợp và phạm vi CoE ở 3PD
Kênh bán (eStore, EPP, SMB, O2O, Shop App, marketplace) nói chuyện với Hybris; **chỉ marketplace đi qua middleware**. Sau Hybris là NERP, OMS, payment gateway, service partner, kho/3PL. Lỗi code, deploy, hạ tầng, phía NERP thuộc SDS India qua Maintenance Request. **CM-13 ch.15:** CoE không vận hành marketplace, chỉ quản luồng order, stock, product data giữa Hybris và 4 middleware. PIC 3PD làm 100% 3PD, có backup certified; ticket 3PD vào COEC giao PIC 3PD; PIC 3PD đổi data 3PD trên production qua flow PC (CM-13 §15.2); nếu cần ImpEx/Groovy thì áp dụng TEC-2.2 (L2 cho service đó, header line, PC duyệt — Lead xác nhận ai chạy script khi PIC 3PD không có L2). **Level 1** chỉ nhận ticket, chuyển ASSIGNED, thu thập evidence và giao PIC 3PD qua Sub-Lead; không đăng nhập middleware.

### 2. Logicbroker chuyển order và stock thế nào
Order tạo trên marketplace đi qua LB vào Hybris ngay qua SamsungBifrost API. Muốn sửa/trả order thì subsidiary nhờ CS agent làm trên Hybris. Muốn ngừng bán sản phẩm thì Merch unapprove trên Hybris. Stock (và product data cho SEAU, SENZ) được cronjob đẩy sang LB — tìm bằng từ khóa `marketplacestocksync`.

### 3. Mức lỗi Logicbroker và lỗi điển hình
**4 mức:** L1 – subsidiary sửa (stock, giá, delivery mode, SKU inactive, ISO code); L2 – cần COEC ticket; L3 – cần COEC và LB; L4 – cần RHQ (Bifrost, site locale, delivery mode chưa bật cho marketplace). Thứ tự ưu tiên: Order failed, rồi Shipment doc failed, Return doc failed, Acknowledgement failed.
Lỗi điển hình: `missing values for [warehouse]` → hết tồn hoặc sai delivery mode trên order line: thêm stock trên Hybris rồi push lại từ LB; `UnknownIdentifierError` → SKU inactive; `No region with the code MY-1` → ISO region cần 2 chữ số (MY-01), sửa ở Custom Lookup; `Parameter usedUnit can not be null` → đổi Sales Unit thành "Pieces"; `No delivery options found` → SKU mới thiếu 3PD delivery mode hoặc base price; bundle báo "Breakout SKU count…" → cột Splits phải cộng đủ 100.

### 4. External Service Type và SC+
Mỗi nước Hybris phải khai báo: ACCESSORIES, BENEFIT, TRADE-IN (MX), TRADE-UP (CE khi dùng), INSURANCE (MX khi dùng), WARRANTY (CE khi dùng); sản phẩm phải khai báo external service trước khi bán kèm. **SC+ Standalone MX** có 2 variant: Normal (NORMAL, PURCHASABLE_NOT_VISIBLE, digital delivery mode, có price row) và EXT (EXTERNAL_SERVICE, ARCHIVED, giá 0). Tắt SC+ Standalone: **đổi Approval sang Check, không đổi Sales status.** CE SC+ Standalone: Manufacturer `GCIC_STANDALONE`; Tech cấu hình ConfigParameter `standaloneSMCMapping` trên Base Store. Sai PID ("INVALID BILL DATA" trong Kibana): sửa Manufacturer AID rồi rerun `processExternalServicesAction` (qua PC).

### 5. Trade-in, overtrade, clawback
Trade-in, overtrade, trade-up dùng cùng flow. VD PH Bolttech: Tokoconfig `toko.boltech.*`; cronjob `ph-boltechTradeInImportData` và `ph-boltech-product-price-imports` tạo T-SKU; câu hỏi đánh giá máy ở `AssessmentCriteria`/`AssessmentCriteriaAnswer` nạp bằng ImpEx. Overtrade dùng type `ExternalServiceDiscountConfig` và key `toko.overtrade.compute.upto.price.new.<store>`; subsidiary có overtrade: SENZ, SME, SEIN, SEPCO, TSE.
**Clawback** = thu hồi giảm giá trade-in khi khách không gửi máy cũ hoặc máy không đúng khai báo. 7 status: NEW, WAIT, RECEIVED (chờ máy/đã nhận); CANCELED (thu hồi toàn bộ giảm giá); **TRADEIN_TIMEOUT** (khách không gửi máy đúng hạn → thu hồi toàn bộ); CLOSED (hệ thống không làm gì thêm); COMPLETED (xong). Order >45 ngày cần clawback bằng script (TEC-3.1).

### 6. Access và ranh giới
Access Logicbroker xin qua AUTEU, RHQ Online Platform Lead duyệt; audit hằng tháng; account không đăng nhập 30 ngày tự khóa. External SSO và hashed access code cho EPP là việc Tech (TEC-EPP-05, Mandatory + TL); trang KB Hash_accesscode chứa shared secret — **không copy, không gửi**.

## Quiz (đáp án)
1 LB báo order failed `missing values for [warehouse]` → **không có stock hoặc sai delivery mode; sửa Hybris rồi push lại**. 2 "No region with the code MY-1 found" → **đổi ISO region thành MY-01 ở Custom Lookup**. 3 Lỗi LB liên quan Bifrost/site locale → **L4, RHQ sửa**. 4 06:00 Level 1 nhận ticket lỗi stock sync 3PD → **nhận, thu thập evidence, giao PIC 3PD qua Sub-Lead**. 5 Tắt SC+ Standalone → **đổi Approval sang Check**. 6 Khách trade-in không gửi máy đúng hạn → **TRADEIN_TIMEOUT, thu hồi toàn bộ giảm giá**. 7 T-SKU Bolttech mới không thấy trên Hybris → **chạy cronjob Bolttech trade-in data và price import (qua PC)**.

## Practice
- **PR-TEC-3.2-1** (giấy, 15'): phân loại 8 lỗi — bên sửa/mức, ai trong CoE nhận (Level 1, Level 2, PIC 3PD), có cần PC không, COEC chờ ở status nào: (1) `missing values for [warehouse]`; (2) `UnknownIdentifierError`; (3) `No region with the code MY-1`; (4) `No delivery options found` ở SKU mới; (5) lỗi Bifrost; (6) SC+ "INVALID BILL DATA"; (7) CompAsia trả null ở WAITING_FOR_CAPTURE_RESULT; (8) khách trade-in gửi máy trễ và subsidiary hỏi vì sao bị thu hồi giảm giá. Pass ≥6/8; mọi fix data production ghi PC; lỗi cần RHQ ở ON HOLD HQ; lỗi code ở SYSTEM SUPPORT qua Level 2; mục (8) giải thích TRADEIN_TIMEOUT.
- **PR-TEC-3.2-2** (staging, 10'): Backoffice mở SKU `SMC-XX-STANDALONE-...` và bản `-EXT` (facilitator đưa code), so Product Type, Sales Status, Approval, delivery mode; tìm cronjob có từ khóa `marketplacestocksync`, ghi Result và End time lần chạy cuối; HAC liệt kê item `AssessmentCriteria` (kiểm tên attribute ở System › Types trước; lọc base store `ph` nếu type có attribute store). Pass: bảng so sánh khớp KB External Service; ghi đúng kết quả cronjob; query chạy hoặc đúng cú pháp.
