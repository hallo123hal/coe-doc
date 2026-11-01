# TEC-4.1 Enhancement, release and BVT for Tech

> Nguồn: page 2483191995 · 60 phút (Study 20' · Demo 10' · Quiz 10' · Practice 20') · Lecture rồi đọc một ENH mẫu theo thứ tự tài liệu; facilitator: Tech Sub-Lead đang làm BVT Coordinator tạm · Cần xong G6.1, TEC-2.1, TEC-2.3; chỉ cần đọc Confluence BiPlus (Jira EMBT/SAM chỉ khi nhận BVT thật). Chưa có Confluence: xin bản in trang MYME-24491 Production readiness và CM-12 ch.3.

## Mục tiêu
Đọc ENH theo thứ tự FRD, TDD, Unit Test, Production readiness và chỉ ra các việc của Tech; phân biệt BVT trên staging (không cần PC) với bật cấu hình/chạy ImpEx production sau release (cần PC); viết test case phía Tech đúng format, mỗi case một expected result; theo nhịp ngày BVT và luật 100% pass khi Tech là PIC.

## Thuật ngữ
**FRD** (functional requirement: user story, acceptance criteria dạng GIVEN/WHEN/THEN, assumption); **TDD** (technical design: giải pháp, ImpEx, config, extension bị ảnh hưởng); **Production readiness** (trang liệt kê bước bật tính năng trên production sau deploy và ai làm); **Dormant / Active** (Dormant: code đã deploy nhưng tính năng chưa bật; Active: đã bật); **RC** (release build `ENH-<số>-RC<n>`, VD ENH-84-RC-1); **Hub / Spoke** (Hub: ticket global HGE; Spoke: dev team cho nhóm market); **Trang `BVT-[ticket key] [scope]`**; **Case ID `TC-COE-[market]-[number]`**.

## Nội dung
### 1. Tech tham gia ENH ở đâu
Nhắc G6.1: ENH đi từ Local Review tới Closed; Spoke viết code; CoE không đổi status Enhancement ticket. Tech tham gia ở 3 chỗ: đọc tài liệu để hiểu thay đổi; làm BVT PIC khi scope kỹ thuật; bật cấu hình hoặc tạo data trên production khi Production readiness giao bước đó cho CoE. Lỗi hay gặp: nghĩ "ENH đã duyệt" nghĩa là CoE được đổi production trực tiếp — **mỗi bước CoE trên production vẫn cần PC riêng** (TEC-2.1).

### 2. Đọc ENH đúng thứ tự (VD MYME-24491 CE SC+ Standalone Monthly)
FRD: đọc user story và AC GIVEN/WHEN/THEN — mỗi AC thường thành một test case BVT. TDD: tìm danh sách ImpEx, config, Tokoconfig, extension bị ảnh hưởng — cho biết cái gì phải bật sau release. Unit Test: xem dev đã test gì để khỏi test trùng. Production readiness: ai làm bước nào sau deploy.
**Việc CoE trong Production readiness MYME-24491:** subsidiary tạo COEC xin tạo data; Spoke tạo PC để bật cấu hình Hybris; CoE tạo data SKU theo COEC; Ops/CoE kiểm PC của Spoke đã chạy trên production chưa — chưa thì CoE chạy ImpEx qua PC riêng. Mọi bước CoE trên production vẫn qua đủ 8 bước PC (TEC-2.1).

### 3. Release, Dormant/Active, ENH có PII
Release tên `ENH-<số>-RC<n>`, có thể tách theo cluster SMS/SMA; HQ công bố lịch release hằng tháng. Bảng release đánh dấu mỗi ENH là Dormant hay Active; ImpEx release nằm ở `tokodeployment/.../import/release/<ENH-xx-RC-n>/<cc>/`. ENH có PII (03-13) có 4 field: Personal Information Related, Security_PII, Security Scope, Security Test Status và 3 checklist: Security_PII_SA, _Dev, _QA — test case BVT **không dùng data khách thật**. Lỗi hay gặp: đọc "deployed" trong bảng release thành "đã live cho khách" — kiểm cột Dormant/Active trước.

### 4. Scope BVT của Tech và nhịp ngày BVT
Scope Tech: checkout, payment, order, invoice, cancel & return, EPP access, report, integration, middleware 3PD và cấu hình Back Office kỹ thuật. Tech PIC là Sub-Lead hoặc TM đang tuần Level 2 (VD trang BVT Checkout 2.0: "Checkout Web Estore" và "Order flow" thuộc Tech). Một ngày trong cửa sổ BVT (CM-12): 08:30–15:30 chạy case, ưu tiên case rủi ro cao (tiền, order, payment); **trước 15:30 ICT (16:30 SGT)** upload Excel test case/defect và cập nhật trang `BVT-[ticket key] [scope]` (6 phần: A General information, B Test cases, C Evidence, D Daily progress, E Defects, F Test report & sign-off).

### 5. Viết test case và chuẩn bị test data
Format: ID `TC-COE-[market]-[number]`, **một expected result mỗi case**, tiếng Anh. VD tốt: "TC-COE-MY-012. Precondition: a device SKU that exists in NERP, has a MAP price and has stock in the right warehouse; a test credit card for the MY PSP. Steps: 1. Add the device with SC+ Standalone Monthly to the cart. 2. Pay with the test card. 3. Open the order in Backoffice. Expected: the order has one SC+ Standalone Monthly line next to the device." Kiểm consignment là case riêng TC-COE-MY-013. Case bị bỏ thì ghi "Out of scope, agreed at kickoff", không xóa dòng.
Chuẩn bị data (READ ME BVT): mở `getcookie.html` của staging trước khi vào site; dùng SKU có trong NERP, có giá MAP và tồn đúng kho (Product Warehouse Map); dùng thẻ test đúng PSP; test order kẹt >1h thì kiểm consignment và cronjob liên quan (TEC-2.3).

### 6. Case fail, luật 100%, ranh giới PC
Case fail: log defect ở sheet E kèm evidence; dev team phân loại; BA phía Spoke chase fix; retest khi fix được deploy. **Chỉ 100% pass mới go-live; 99% không đủ**; CoE không xin gia hạn, không xin "conditional go-live"; đánh PASS cho case chưa chạy, dùng lại screenshot cũ, giấu blocker là vi phạm và có thể bị yêu cầu thay người. **Ranh giới PC:** BVT trên staging không cần PC; bật cấu hình, chạy ImpEx enablement hay sửa data production sau release vẫn cần PC do Oliver duyệt.

## Quiz (đáp án)
1 Hết cửa sổ BVT, pass 33/34, 1 case chờ dev fix → **không đề xuất sign-off; báo đúng sự thật, RHQ quyết**. 2 Release table ghi "Dormant" → **code đã deploy nhưng tính năng chưa bật**. 3 Production readiness giao Spoke tạo PC bật cấu hình, bạn thấy production vẫn tắt → **kiểm PC của Spoke; nếu CoE làm thì qua đủ 8 bước PC**. 4 Ngày BVT đầu chạy case nào trước → **rủi ro cao: tiền, order, payment**. 5 Test case đúng chuẩn CM-12 → `TC-COE-MY-012: Order with SC+ Monthly. Expected: PAYMENT_CAPTURED.` 6 Hạn upload Excel và cập nhật trang BVT hằng ngày → **trước 15:30 ICT (16:30 SGT)** (trang Checkout 2.0 ghi "4pm" nhưng CM-12 ưu tiên). 7 Test order BVT kẹt ORDER_SPLIT >1h → **kiểm consignment và cronjob kho** (`xx-tokoTransferConsignmentToWarehouseJob`).

## Practice
**PR-TEC-4.1-1** (20'): đọc trang MYME-24491 Production readiness và phần user story + AC của trang Requirement (~5', facilitator chỉ phần cần đọc). Chuẩn bị: (a) danh sách cấu hình/ImpEx cần bật, ai làm, CoE cần PC riêng không; (b) 4 test case phía Tech (order, payment, invoice, cancel/return) dạng `TC-COE-MY-[số]` mỗi case một expected result tiếng Anh; (c) cronjob cần theo dõi khi đẩy test order qua các status trên staging. Pass: phân việc Spoke / CoE / subsidiary đúng; mọi bước production của CoE đánh dấu "PC ticket"; 4 case đúng format; ít nhất 1 cronjob đúng.
