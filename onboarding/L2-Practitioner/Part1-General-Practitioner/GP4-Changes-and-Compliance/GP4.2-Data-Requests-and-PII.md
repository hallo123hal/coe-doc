# GP4.2 Data requests and PII

> Nguồn: page 2484175222 · 45 phút (Study 10' · Demo/thảo luận 5' · Quiz 5' · Practice 25') · Thực hành theo case; facilitator: Shift Leader hoặc Sub-Lead · Capability C5 · Cần xong G1.3 (10 Golden Rules, đã đạt test T1); đọc trước hai ticket SCOE-25 (TRN-019: voucher VIP kèm danh sách khách) và SCOE-23 (TRN-017: export bank redemption). Chỉ cần Confluence (đọc CM-10, CM-13 ch.12, TC-05 §3.2.1). Không có access: facilitator in bảng data CM-13 và text hai ticket (bản in không chứa dữ liệu Samsung, thu lại cuối buổi).

## Mục tiêu
Phân loại dữ liệu: Samsung confidential, PII khách, BiPlus internal, thông tin vận hành CoE hay công khai; với mỗi yêu cầu dữ liệu quyết định làm, từ chối hay route đi duyệt kèm đúng đường duyệt; chuẩn bị evidence chứng minh change mà không lộ dữ liệu cá nhân và chỉ giữ trên hệ thống Samsung; viết câu trả lời ngắn lịch sự nêu rule, cái giao được, cái requester phải làm; nhận ra yêu cầu dữ liệu đã thành security incident và báo trong 1 giờ.

## Thuật ngữ
**PII** (họ tên, số điện thoại, địa chỉ, email của khách; danh sách đầy đủ ở trang RHQ, Tech phải thuộc lòng); **PUMI** (form yêu cầu dữ liệu subsidiary tạo và được duyệt trước mọi report/trích xuất dữ liệu; CoE sau đó gửi PC ticket; nghĩa đầy đủ chờ RHQ xác nhận); **EDM** (email marketing gửi khách; yêu cầu lấy email khách để gửi EDM mặc định bị từ chối); **Do, refuse or route** (ba đáp án cho yêu cầu dữ liệu: làm ngay, từ chối mặc định, hay chuyển sang đường duyệt cần thiết (PUMI rồi PC ticket)); **Investigation query** (query chỉ đọc để tìm nguyên nhân ticket; không PC ticket nhưng ghi lý do (số ticket) lên ticket và chỉ lấy cột cần); **Evidence screenshot** (chụp chỉ trên CoE workstation, chỉ phần cần chứng minh, không dữ liệu cá nhân, đính thẳng Jira rồi xóa khỏi máy); **Security incident** (mọi sự kiện đã hoặc có thể lộ dữ liệu Samsung/khách; nghi ngờ là đủ, báo cáo viết trong 1 giờ); **Email-restricted coupon** (coupon nhiều code, mỗi code chỉ dùng được cho một email trong danh sách, một lần; VD voucher VIP RM300 trong TRN-019).

## Nội dung
### 1. Cái gì được rời khỏi hệ thống Samsung
Dữ liệu Samsung chỉ có một nơi: hệ thống Samsung. Bốn loại:
| Loại | Ví dụ | Được giữ ở đâu |
|---|---|---|
| Samsung confidential và dữ liệu cá nhân khách | Ticket, brief, price file, SKU, promotion/sản phẩm chưa công bố, order, tên/điện thoại/địa chỉ/email khách | Chỉ hệ thống Samsung: Jira, Confluence, email dự án, Hybris Backoffice, AEM, Shop App CMS; Mattermost với RHQ (tối thiểu) |
| BiPlus internal | Hồ sơ HR, lý do nghỉ, tài liệu Academy không chứa dữ liệu Samsung | Hệ thống BiPlus, không được chứa dữ liệu Samsung |
| Thông tin vận hành CoE mà RHQ yêu cầu | Danh sách Lead, roster, lịch nghỉ, ngày nghỉ (không lý do), danh sách team | Trang CoE trên Samsung Confluence; không số điện thoại cá nhân |
| Công khai | Trang Samsung.com | Ai cũng xem được; không comment thay Samsung |
Vì vậy hàng đầu không được rời đi: không export/tải về máy, USB, Google Drive, email cá nhân hay hệ thống BiPlus; không in; không ảnh điện thoại; không công cụ AI. Subsidiary cần danh sách thì gửi **link** trang Samsung Confluence trong Jira comment, không file export. Report gửi tới người nhận ghi trong PUMI đã duyệt, không bao giờ "đính kèm như mọi khi" mặc định.
**Ví dụ TRN-017:** subsidiary SG xin file redemption của bank promotion rule `SG_BIN_CC_0903` ("$80 off min spend $1,200") ngày 15/11/2026, kèm email khách và 4 số cuối thẻ, "đính vào ticket như mọi khi". Email là PII; 4 số cuối thẻ là dữ liệu thanh toán. Report, kể cả hằng ngày, là trích xuất dữ liệu nên áp dụng đường route (mục 3).
> 4 số cuối thẻ không có trong danh sách PII mà lab ticket trích, nhưng là dữ liệu thanh toán. TRN-017 nói không export cho tới khi RHQ hướng dẫn. Coi là bị loại.

### 2. Che và chia sẻ evidence
Ảnh evidence và file QA evidence là ngoại lệ có kiểm soát của "không bản sao". Chỉ được khi đủ bốn điều kiện: (1) tạo chỉ trên CoE workstation trong khu secure; (2) đính thẳng vào Jira ticket của task; (3) xóa ngay bản trên máy sau khi đính, gồm thư mục downloads và recycle bin; (4) không ảnh điện thoại; không gửi qua kênh khác (Mattermost, email, chat, hệ thống BiPlus).
Chụp **chỉ phần cần chứng minh**, tránh vùng có dữ liệu khách. Trong comment, thông báo, PC ticket gọi order bằng số ("order DEMO-ORD-009"), không bao giờ bằng tên hay địa chỉ khách. PC ticket: scope là danh sách mã; ảnh before che dữ liệu cá nhân; danh sách chứa dữ liệu cá nhân thì đính file, không đặt vào description. Không video làm evidence.
**Ví dụ TRN-019:** subsidiary MY dán bảng 12 khách VIP (tên, email, mobile) vào description, đính file Excel không bảo vệ, và nhờ CoE "email trực tiếp code cho từng khách" và "dán danh sách code vào ticket này". CoE không được copy bảng, trích trong comment, tải file về thiết bị cá nhân hay dán vào AI để "làm sạch email". CoE không liên hệ khách cuối và không bao giờ gửi PII hay code qua email từ Hybris. Danh sách code không đính ticket; theo lab ticket chỉ gửi cho reporter, trong file có mật khẩu.
> Cách gửi code list của TRN-019 (file có mật khẩu chỉ cho reporter, mật khẩu gửi riêng) lấy từ lab ticket và vault notes; CM-10 không mô tả. CM-10 rule 2 (dữ liệu ở lại hệ thống Samsung) thắng: hỏi Shift Leader kênh được duyệt nào trước khi gửi bất kỳ file.
Hai luật đúng với mọi kênh: không bao giờ dán code hay email khách vào Jira comment, và đặt định danh khách vào field được bảo vệ của COEC, không vào description (A.II.1 và A.II.2).
> **Under review (D8):** runbook sửa đổi gửi file code và email list trả lại cùng cách subsidiary gửi (trên ticket, qua email, mã hóa nếu của họ mã hóa). Handover 29/10 nói email list không được nằm trên ticket. Kênh trả về không chấm tới khi D8 chốt.

### 3. Do, refuse hay route
Dùng bảng này cho mọi yêu cầu dữ liệu. CM-13 ch.12 là rule.
| Yêu cầu | Trả lời | Cần gì |
|---|---|---|
| Query chỉ đọc để điều tra ticket | **Do** | Lý do (số ticket) ghi trên ticket; chỉ cột cần; kết quả ở lại công cụ Samsung |
| Thêm/bớt field không PII trong report có sẵn | **Do** | Được phép |
| Report (VD doanh số từ 1/1 đến nay cho audit) | **Route** | Subsidiary tạo PUMI; duyệt đính Jira; CoE gửi PC ticket |
| Report cronjob mới; thêm/bớt người nhận; dữ liệu lịch sử/một lần | **Route** | PUMI rồi PC ticket; không bao giờ tự tạo trên production |
| Dữ liệu chứa PII | **Route** (chỉ ngoại lệ) | Chỉ audit, theo process riêng |
| Email khách để gửi EDM | **Refuse** mặc định | Trả lời trên ticket, báo Shift Leader hoặc Lead |
| Gửi PII qua email từ Hybris | **Refuse** luôn | Không bao giờ; nếu đã xảy ra là security incident |
| Sửa database do RHQ quản lý | **Refuse** luôn | CoE không bao giờ sửa |
| Gửi dữ liệu qua FTP | **Route** | Process FTP riêng trên trang RHQ |
Yêu cầu report đến mà không có PUMI thì không bắt đầu. Đăng Template 21: "Production data can only be provided with an approved PUMI. Please raise the PUMI, attach the approval to this ticket, and we will proceed with the approval process." CoE không thể tạo PUMI thay subsidiary.
**Áp dụng TRN-017:** đây là report nên là việc Tech trên COEC và cần PUMI. Bỏ email và số cuối thẻ khỏi scope. Đề nghị field không PII: số order, ngày giờ order (SGT), status, promotion rule, discount, tổng order. Vì yêu cầu hằng ngày, đề xuất report cronjob không PII (một PUMI + một PC ticket) thay vì ticket hằng ngày. Hỏi một lần, chuyển ticket sang ON HOLD SUBS giao requester.
> Open points: RHQ chưa xác nhận đầy đủ nghĩa PUMI, ai duyệt, mất bao lâu, ticket chờ PUMI ở status nào, hay chạy lại query đã lưu có cần PUMI (CM-13 ch.12; TC-05 §3.2.1). TRN-017 gợi ý ON HOLD SUBS khi subsidiary chưa tạo PUMI và ON HOLD HQ khi RHQ đang duyệt; dùng cách đó tới khi RHQ trả lời.

### 4. Khi yêu cầu đã là incident
Đôi khi thiệt hại đã xảy ra khi ticket đến: PII dán rõ trong description, danh sách order gửi tới hộp thư cá nhân, file gửi qua email từ Hybris. Đó là **security incident**: mọi sự kiện đã hoặc có thể lộ dữ liệu. Nghi ngờ là đủ. Năm bước trong giờ đầu:
1. **Dừng** hành động: không gửi thêm, không bấm thêm.
2. **Giữ nguyên hiện trạng**: không xóa, không "tự sửa".
3. **Báo miệng ngay** cho Shift Leader hoặc Lead và DevSecOps Engineer (ngoài giờ: SDM hotline).
4. **Viết báo cáo trong 1 giờ**, mô tả dữ liệu và vị trí bằng lời, không đính kèm.
5. **Làm theo chỉ dẫn**; không bàn trên kênh chung; không tự liên hệ RHQ hay subsidiary. COE Lead hoặc SDM báo RHQ.
**Áp dụng TRN-019:** đầu tiên initial response (APPROVED-ES → STG SETUP). Rồi dừng và báo Shift Leader ngay: ticket chứa PII rõ và file không bảo vệ. Shift Leader quyết cấp báo (DevSecOps, RHQ). CoE không tự sửa description của requester; yêu cầu requester xóa PII. Setup tiếp tục sau với email-restricted coupon (12 × RM300, exposure ~800 USD: R3, không E4).
> Vi phạm an ninh thông tin chưa tính vào strike RHQ (Samsung chưa có yêu cầu chính thức, CM-08 §1.7) nhưng vẫn xử lý theo CM-10. Báo cáo viết gửi qua email dự án hay kênh Mattermost DevSecOps còn chờ ở CO-04.

### 5. Trả lời bằng văn bản
Mọi câu trả lời nằm trên Jira ticket, tiếng Anh, trong một comment gồm bốn phần: rule trong một câu, cái bạn **có thể** giao, cái requester phải làm, status bạn đặt. Không giảng đạo; luôn đưa phương án tuân thủ nhanh nhất.
**Từ chối (email EDM):** "Hi [Name], thank you for your request. Customer email lists for marketing emails cannot be provided by the Ops CoE (RHQ data rule). If you need a campaign audience, please check with RHQ D2C Platform on the approved process. Ticket owner: [name]."
**Route (report không có PUMI, theo TRN-017):** "Hi [Name], this is a data report, so it needs an approved PUMI before we can extract data. Please attach the approved PUMI listing recipients, fields and schedule. Customer email and card digits cannot be included (PII and payment data); we will provide order number, order date and time (SGT), status, promotion rule, discount and order total. Since this is requested daily, we suggest a non-PII report cronjob. Status ON HOLD SUBS, assigned to you."
**PII trong ticket (theo TRN-019):** "Hi [Name], for data protection we cannot copy, forward or email customer details, and the CoE does not contact customers directly. Please remove the customer table from this ticket and send the email list through the approved channel. We will set up one email-restricted code per customer and share the code list with you only."
> Câu từ chối EDM do tác giả khoá học viết; không nguồn nào cho câu chuẩn. CM-08 Template 6 nói chỉ dùng từ chối sau khi Shift Leader hoặc Lead xác nhận.

## Quiz (đáp án)
1 Tech Level 1 chạy query chỉ đọc trên production xem vì sao order DEMO-ORD-009 stuck → **C: lý do (số ticket) ghi trên ticket, chỉ cột cần, kết quả giữ trong công cụ Samsung** (PUMI/PC cho report và trích xuất, không cho điều tra). 2 Subsidiary AU xin email khách đã mua sản phẩm để gửi EDM, nói "campaign là của chúng tôi" → **B: từ chối mặc định: trả lời trên ticket và báo Shift Leader/Lead** (PUMI không biến từ chối mặc định thành được phép). 3 TRN-017 đến không có PUMI, xin email khách và 4 số cuối thẻ → **C: Template 21, liệt kê field không PII giao được, loại email và số thẻ, đề xuất cronjob không PII, ON HOLD SUBS giao requester** (B trông tuân thủ nhưng report không PII vẫn cần PUMI trước; CoE không tự tạo PUMI). 4 Mở TRN-019 thấy tên, email, mobile của 12 khách rõ trong description → sau initial response **C: dừng, giữ nguyên, báo Shift Leader ngay; Shift Leader quyết cấp báo cáo**. 5 Cần QA evidence cho setup coupon, trang checkout hiện tên khách test → **B: chỉ chụp phần chứng minh coupon, tránh dữ liệu cá nhân, trên CoE workstation; đính Jira; xóa bản local**. 6 Subsidiary xin thêm người nhận mới vào report hằng ngày có sẵn → **B: route: PUMI rồi PC ticket**. 7 Đồng nghiệp email report có số điện thoại khách từ Hybris 20 phút trước → **B: báo miệng ngay cho Shift Leader/Lead và DevSecOps, báo cáo viết trong 1 giờ từ lúc phát hiện** (COE Lead/SDM báo RHQ, không phải bạn).

## Practice
**PR-GP4.2-1. Sáu yêu cầu dữ liệu** (20', giấy, làm một mình rồi so theo cặp). Sáu yêu cầu: (1) SCOE-25 TRN-019, voucher VIP cho 12 khách, bảng khách dán trong ticket và xin email code trực tiếp; (2) SCOE-23 TRN-017, export bank redemption hằng ngày với email khách và số cuối thẻ, không PUMI; (3) query chỉ đọc của Tech tìm vì sao một order stuck; (4) subsidiary xin email khách để gửi EDM; (5) subsidiary xin thêm field không PII (order status) vào report đã duyệt; (6) subsidiary xin thêm người nhận mới vào report có sẵn. Việc: mỗi yêu cầu quyết định do, refuse hay route; nêu approval cần và Jira status; viết reply tiếng Anh (3–5 dòng) cho yêu cầu 1, 2, 4. **Pass:** 6/6 quyết định đúng — (1) dừng và báo Shift Leader (PII đã lộ, có thể là incident), không copy, không email khách, code list không đưa vào ticket; setup chỉ sau khi PII đã bị xóa; (2) route: Template 21, loại PII và số thẻ, đề xuất field không PII, gợi ý cronjob, ON HOLD SUBS giao requester; (3) do, lý do trên ticket, không PC ticket; (4) refuse mặc định và báo Shift Leader/Lead; (5) do (đổi field không PII được phép); (6) route: PUMI rồi PC ticket. Mỗi reply lịch sự, nêu rule trong một câu, đề xuất cái làm được, không chứa dữ liệu khách. Không cần truy cập hệ thống.
