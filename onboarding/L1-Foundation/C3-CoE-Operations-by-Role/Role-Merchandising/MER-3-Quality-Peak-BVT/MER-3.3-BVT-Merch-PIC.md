# MER-3.3 BVT for the Merchandising PIC

> Nguồn: page 2483224936 · 50 phút (Study 18' · Demo 10' · Quiz 10' · Practice 12') · Lecture + demo một trang BVT mẫu; facilitator: Merch Lead hoặc BVT Coordinator (hiện là một Tech Sub-Lead) · Cần xong G6.1, G2.3. Chỉ cần Confluence BiPlus để tạo draft; trước BVT thật cần xin: Jira EMBT & SAM, Backoffice staging, WDS QA Auth (MER-2.5).

## Mục tiêu
Chuẩn bị access, môi trường, test data trước ngày 1 cửa sổ BVT; dựng trang BVT 6 phần và file Excel theo chuẩn CM-12; viết test case, defect, comment trên enhancement ticket đúng template và nhịp hằng ngày; áp điều kiện sign-off và quy trình khi nhận thông báo BVT ngoài giờ.

## Thuật ngữ
**BVT Coordinator** (người điều phối BVT phía CoE; hiện là Tech Sub-Lead, chờ CEO xác nhận); **EMBT, SAM** (hai Jira project cần access cho BVT; vendor cũ log defect ở đó); **`getcookie.html`** (trang đặt cookie môi trường test); **Trang `BVT-[ticket] [scope]`** (trang Confluence của một vòng BVT, 6 phần A–F); **Test case `TC-COE-[market]-[number]`**; **DEF-nn**; **Comment E1–E8** (template trong CM-12 App. A: E3 bắt đầu, E5 defect, E8 blocker); **4 status case:** Not run, Pass, Fail, Blocked (không dùng Blocked để che case fail).

## Nội dung
### 1. Merch PIC là ai và chuẩn bị gì
Merch PIC (Sub-Lead hoặc Market Owner) nhận BVT đụng promotion, coupon, price, product setup, buying page, add-on page, AEM, Shop App CMS. VD Checkout 2.0: Sign in, AEM, Cart, Shop App UI và EPP/SMB/EA checkout là Merch; Estore web checkout và order flow là Tech. Mỗi team đúng 1 PIC + backup; RHQ có thể báo trước vài ngày và Confluence access mất 2–3 ngày nên Lead chỉ chọn PIC từ **BVT-ready pool** (người đã certified và có access sẵn) — giữ access cập nhật để ở trong pool (CM-12 §3.2, §7.2).
**Chuẩn bị trước kickoff (09 READ ME):** xin Jira EMBT & SAM; account Backoffice staging qua Jenkins job USER-BO-SELF-PORTAL (S1–S3 cho cluster SMS, S4 cho SMA), reset mật khẩu bằng USER-BO-SELF-PASSWORD-RESET; mở `getcookie.html` của môi trường trước khi xem trang; thêm giỏ nhanh bằng `/ng/p4v1/addToCart?products[0].productCode=…`; test data: SKU có trong N-ERP, có giá MAP và tồn đúng kho ("Pre-check Before Place Order"); chỉ test tính năng subsidiary đã bật; chỉ dùng test account.

### 2. Cửa sổ BVT và nhịp hằng ngày
Thường 3–5 ngày làm việc. Ngày 1 bắt đầu sau handover; cuối ngày 1 phải chạy ≥50% case; mọi case chạy ít nhất một lần trong nửa đầu cửa sổ; retest ngay trong ngày khi fix tới; test report xong trong 4 giờ làm việc sau khi case cuối pass. Thứ tự case: rủi ro cao trước (tiền, order, payment), rồi case theo market, case nhiều bước, UI đơn giản sau cùng. **Một ngày BVT:** 08:00 xác nhận kế hoạch; 08:30–15:30 chạy case; trước **15:30 giờ VN (16:30 SGT)** upload Excel và cập nhật tiến độ. Ghi evidence ngay sau mỗi case; log defect trong ngày; blocker báo ngay.

### 3. Comment Jira, trang BVT, evidence
Trên Jira CoE **không đổi status** Enhancement Request, chỉ comment: bắt đầu (E3), defect (E5), kết thúc (E6, E7), blocker >nửa ngày (E8); mỗi comment 4 phần Status, Evidence, Next step, Next update (giờ SGT). Trang `BVT-[ticket] [scope]` có 6 phần: A General information, B Test cases, C Evidence, D Daily progress, E Defects, F Test report & sign-off. **Excel là bản gốc:** chỉ làm trên workstation CoE; không gửi email/Mattermost, không đưa vào AI; không xóa dòng hay run cũ. Caption screenshot: `Case ID | Run | dd-Mon hh:mm SGT | Environment | Market store | Result` (VD `TC-COE-SG-03 | Run 2 | 09-Dec 14:20 SGT | S2 | sg | Pass`).

### 4. Defect, retest, sign-off
Log mỗi defect bằng template với ID DEF-nn; dev team không phản hồi sau 4 giờ làm việc thì Coordinator nhắc BA Spoke. Retest chỉ khi fix đã lên môi trường test; chạy lại các case liên quan và ghi run mới. Dev trả lời "by design" → yêu cầu xác nhận bằng văn bản, không tự đổi expected result.
**Sign-off phía CoE:** PIC đề xuất, Lead xác nhận khi **100% case pass**, không còn Blocked/Not run, defect đã đóng, có test report và User Acceptance; RHQ sign-off cuối. CoE không xin gia hạn hay "conditional go-live". **Vi phạm BVT (RFP 3.4):** đánh PASS khi chưa chạy; dùng lại screenshot; đổi expected result không có xác nhận văn bản; bỏ một ngày cập nhật; giấu blocker; báo cáo trễ do CoE.

### 5. Thông báo BVT ngoài giờ và ước lượng giờ
Ngoài giờ, trong 15': Shift Leader điền section 9 của handoff note, nhắn Merch Lead và Tech Lead trên kênh `coe-leads`, trả lời RHQ một câu (E1). **Không** gọi QA on-call, không hứa tên PIC, không bàn ngày; sáng làm việc kế tiếp Lead chọn PIC trước 10:00.
Ước lượng giờ BVT (CM-12 §7.1): chạy lần đầu 20'/case; retest ~25% số case × 20'; 20'/defect dự kiến; hỗ trợ subsidiary 1h/ngày; cập nhật trang & Excel 45'/ngày; kickoff 1h + call 15'/ngày; test report & User Acceptance 2h; rồi + 20% dự phòng. Ticket SEAO dùng chung nhân 8 các phần chạy lần đầu, retest, defect, hỗ trợ. Các hệ số là giả định lập kế hoạch tới khi Lead review sau 3 vòng BVT đầu.

### Điểm đáng nhớ từ KT
Tài liệu BVT Merch: khi được giao làm gì, cập nhật kết quả, raise defect, ai đóng — theo CM-12 (CoE chỉ comment E3–E8; Excel và trang BVT là bản gốc). Có hướng dẫn nội dung không được nhập vào data hệ thống → chỉ dùng test account và data mô phỏng. Staging access tự tạo/kích hoạt lại được. Mỗi nước có hai bộ test data (S2 và môi trường khác: account, payment, URL) → giữ trên Confluence Samsung, không chép sang hệ thống BiPlus (CM-13 §18.1). AEM author copy / pre-QA AEM: tự đăng ký QA Auth trên WDS, không chọn PREPRD (MER-2.5).

## Quiz (đáp án)
1 Cuối cửa sổ pass 49/50, case cuối chờ fix → **không sign-off; RHQ quyết** (go-live cần 100%). 2 Enhancement đổi màn setup coupon trong Backoffice → **Merch cung cấp BVT PIC**. 3 CoE làm gì với status Enhancement Request → **không đổi, chỉ comment**. 4 Hạn upload Excel hằng ngày → **15:30 giờ VN (16:30 SGT)**. 5 Case không chạy được vì môi trường hỏng nhưng nghi tính năng cũng lỗi → **Blocked kèm lý do, báo ngay**. 6 20:15 tối thứ Sáu RHQ báo cửa sổ BVT tuần sau → **Shift Leader viết handoff note và báo cả hai Lead** (không gọi QA on-call, không hứa tên PIC).

## Practice
- **PR-MER-3.3-1** (5'): tạo trang `BVT-DEMO-7001 coupon cart` đủ 6 phần A–F; phác Excel 2 sheet (Test case, Defect) với 3 dòng mẫu Pass/Fail/Blocked, mỗi dòng có caption đúng format. Pass: đủ 6 phần; case ID đúng format; mỗi case một expected result; caption có giờ SGT và environment; không data thật hay password.
- **PR-MER-3.3-2** (7'): viết 2 case tiếng Anh cho enhancement "đổi khối tổng tiền trong giỏ" (một SG, một ID; khía cạnh theo market: tiền tệ, thuế, stacking); ước lượng giờ cho 40 case trong cửa sổ 4 ngày, dự kiến 5 defect. Kết quả ≈ **35h12'**: first run 13h20', retest (10 case) 3h20', defect 1h40', hỗ trợ 4h, trang & Excel 3h, kickoff + call 2h, test report 2h → tổng 29h20' + 20% (5h52'); nhận xét: nhiều hơn một người làm được trong 4 ngày nên phải chia case cho backup.
