# QA-2.3 Checking special channels: EPP/SMB/O2O, Shop App, AEM

> Nguồn: page 2483258141 · 60 phút (Study 20' · Demo/thảo luận 10' · Quiz 10' · Practice 20') · Demo một EPP site trên Backoffice staging + Shop App trên BlueStacks, rồi thực hành cá nhân; facilitator: QA Sub-Lead cùng Merch PIC phụ trách EPP · Cần xong G4.2, G5.1, QA-2.2; tài khoản Backoffice staging, tài khoản test EPP do facilitator cấp (không bao giờ ghi access code vào bài làm); Shop App cần APK hoặc BlueStacks, AEM cần QA Auth — thành viên mới thường chưa có nên phần Shop App/AEM có bản giấy.

## Mục tiêu
Đọc cấu hình EPP site và dự đoán khách EPP thấy gì về login, quota, giá; kiểm `QCL-MST-01`, đặc biệt giá EPP không rò sang B2C; kiểm điều kiện promotion in-store trên Shop App; liệt kê quyền truy cập cần cho Shop App/AEM và xin ở đâu.

## Thuật ngữ
**EPP site ID** (country code chữ thường + gạch dưới + tên, VD `sg_test_epp`); **SSO_DOMAIN** (đăng nhập bằng email domain công ty); **SSO_ACCESSCODE_OTP** (access code + OTP qua SMS/email); **Hash_accesscode** (qua SSO portal của partner, link chỉ sống ~10 giây); **Customer Purchase Quota**; **Cart Restriction** (Multistore › EPP site › Cart Restriction); **TokoPromoQuota** (quota theo category trong một kỳ); **BlueStacks** (chạy Android trên PC để mở Shop App); **In-store mode**; **QA Auth, P6** (đăng ký quyền xem AEM ở môi trường QA; P6 là link AEM QA); **WMC** (Website Management Center).

## Nội dung
### 1. Thứ tự ưu tiên multistore và duyệt EPP site
Nhắc G5.1: delivery mode và payment mode lấy theo thứ tự **Multistore → Website → Base Store**. VD khách EPP ở MY không thấy Samsung Rewards dù Base Store có, vì multistore có danh sách payment mode riêng. EPP site mới hoặc kích hoạt lại cần **email duyệt của subsidiary đính kèm** và ticket đã qua ON HOLD RHQ; thiếu một trong hai thì QA không kiểm, trả `RC-EVD`. Login type verification code không được dùng cho site mới trừ khi có thêm một lớp hạn chế.

### 2. Các loại login EPP
- **SSO_DOMAIN:** khách báo "invalid email" → kiểm domain filter của multistore; email có ký tự đặc biệt cần regex trong domain filter.
- **SSO_ACCESSCODE:** không đăng nhập được dù đã dùng code → thường chưa xong bước verify; kiểm `customer.multistorelinks`.
- **SSO_ACCESSCODE_OTP:** lần đầu nhập access code, rồi số điện thoại hoặc email, rồi OTP; từ lần sau chỉ cần OTP. SMS OTP dùng ở PH, VN; email OTP ở MY, ID.

### 3. Customer Purchase Quota
Backoffice › Multistore › chọn EPP site › Cart Restriction. VD Cart Quantity Limit = 5 → thêm món thứ 6 không checkout được, báo lỗi quota; Cart Purchase Limit = 500 → cart 650 cũng bị chặn. Quota có thể reset hằng tháng, quý, nửa năm, năm. Quota theo category (TokoPurchaseLimit) và promotional quota (TokoPromoQuota) giới hạn số lượng/giá trị mua trong một category (VD Mobile_Quota). Mỗi site loại trừ tối đa 75 sản phẩm và 7 category.

### 4. QCL-MST-01 và O2O
`QCL-MST-01` kiểm: store, channel, price group, customer group khớp brief; phần Tech (COEC) đã xong; SKU bị loại trừ không mua được ở store đích; **giá EPP/SMB không xuất hiện ở B2C**. Cách kiểm: mở cùng SKU ở B2C và EPP (SF-1) rồi so giá. Lỗi tốn kém nhất: giá EPP rò sang B2C, hoặc merge site làm nhân viên mất quyền truy cập. O2O: account `XX_pos_adm_o2o` là super admin; `XX_pos_adm_ZZZ` thuộc partner; Endless Aisle là nhân viên cửa hàng đặt hộ khách; BOPIS là mua online, nhận tại cửa hàng.

### 5. Shop App
Promotion in-store cần **hai điều kiện**: Qualifying Sales Application IN MOBILEAPP **và** Qualifying Sites đặt là in-store site. G3.4: promotion chỉ giới hạn một nền tảng (chỉ app hoặc chỉ web) bị cấm từ 1/12/2025; in-store là ngoại lệ vì nhắm in-store site chứ không phải B2C. Promotion chỉ-app trên B2C site vẫn bị cấm (QA Lead đối chiếu trang RHQ trước cohort). QA mở app bằng BlueStacks trên PC; **không chọn thiết bị Samsung** trong settings (login lỗi); cài Samsung Shop từ Play Store; đổi country phải login lại; dùng Wi-Fi hoặc hotspot. APP-1 so nội dung app với web của cùng campaign: nội dung giống, deep link đúng, kích thước ảnh đúng.

### 6. Quyền truy cập Shop App và AEM
- **Shop App:** APK mới xin qua AUTEU; user cũ xin lại qua Knox chat với RHQ platform PIC; cấm dùng chung account. Trên Shop App CMS, Ops CoE có VIEW, EDIT, REQUEST-APPROVAL, PUBLISH; **chỉ RHQ có APPROVE**.
- **AEM:** đăng ký qua link "QA Auth" trên wds.samsung.com, có quyền sau ~24 giờ; kiểm thay đổi AEM trên link P6 cần thêm WMC.
- **AEM-1:** so bản author, preview, published; lịch on/off theo giờ market; link, CTA, T&C đúng như subsidiary gửi; kiểm desktop và mobile. Nội dung Thái và Bahasa so từng ký tự, **không dịch**.

## Quiz (đáp án)
1 Base Store 7 delivery mode, Website 9, EPP multistore chỉ `my-schedule-delivery` → khách EPP thấy **A: chỉ `my-schedule-delivery`**. 2 Site ID EPP mới đúng chuẩn → **B: `sg_bankx_epp`**. 3 Cart Quantity Limit = 5, thêm món 6 → **C: checkout bị chặn, báo lỗi quota**. 4 SSO_ACCESSCODE_OTP lần thứ hai → **D: chỉ nhập OTP**. 5 Ticket tạo EPP site mới không có email duyệt của subsidiary → **A: không kiểm, trả `RC-EVD`** (Doer lẽ ra không build: CM-13 §13 đưa ticket sang ON HOLD SUBS trước khi build). 6 Vì sao không chọn thiết bị Samsung trong BlueStacks → **B: login lỗi redirect**. 7 Quyền chỉ RHQ có trên Shop App CMS → **C: APPROVE** (và SECURE-FREEZE-EXCEPTION). 8 Kiểm AEM trên link P6 cần → **D: WMC**. 9 Promotion chỉ cho Shop App in-store → **D: Sales Application IN MOBILEAPP + Sites là in-store site**.

## Practice
- **PR-QA2.3-1** (8', Backoffice staging chỉ xem): Multistore › mở site `sg_…_epp` facilitator chỉ định. Ghi login type + Multi Login Type List (tab Properties), otpConfig nếu có (tab Administration), Cart Quantity Limit, Cart Purchase Limit, Start/End, Recurrence (Cart Restriction), Category Purchase Limit, TokoPromoQuota, danh sách loại trừ. Dự đoán 3 hành vi: vượt giới hạn số lượng, vượt giới hạn giá trị, vượt quota category. Không lưu. Pass: bảng đủ field + 3 dự đoán có lý do. Không có access: đọc từ bản in tab Properties và Cart Restriction.
- **PR-QA2.3-2** (7'): getcookie.html, đăng nhập EPP staging bằng account được cấp; thêm số lượng vượt Cart Quantity Limit, ghi thông báo lỗi; thử SKU trong danh sách loại trừ; mở cùng SKU ở B2C và EPP staging so giá. Pass: 3 kết quả khớp dự đoán PR-QA2.3-1 hoặc ghi rõ khác biệt; che thông tin account trong ảnh; kết luận theo `QCL-MST-01`. Bản giấy: Cart Quantity Limit 5, giá B2C 1,299 SGD, giá EPP 1,099 SGD → viết kết quả khi thêm 6 món, và kết luận nếu trang B2C hiện 1,099 SGD (Defect, giá EPP rò sang B2C).
- **PR-QA2.3-3** (5'): mở rule in-store facilitator chỉ, xác nhận hai điều kiện; nếu đã có Shop App trên BlueStacks thì so app với web của cùng campaign theo `QCL-SAC-01`, nếu chưa thì viết kế hoạch APP-1 4 bước và liệt kê 5 quyền cần xin, xin ở đâu. Pass: nêu đúng hai điều kiện; có ảnh hoặc kế hoạch APP-1 đầy đủ; danh sách quyền có AUTEU cho APK, QA Auth trên wds.samsung.com cho AEM, và đầu mối từ QA Onboarding Access Checklist cho phần còn lại.
