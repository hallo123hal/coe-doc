# QA-3.1 Coached practice on old tickets (shadowing)

> Nguồn: page 2483258179 · 120 phút (Study 20' · Demo/thảo luận 35' · Quiz 10' · Practice 55') · Mentor mở ticket cũ và nói to từng quyết định, học viên ghi chú; sau đó mỗi người làm lại một QA check trên giấy cho ticket khác và mentor sửa; một mentor kèm tối đa 3 học viên (Lead xác nhận trước cohort); facilitator: QA Lead hoặc QA Sub-Lead có L2 · Cần xong toàn bộ QA-1, QA-2; quyền đọc Samsung Jira các project Shop Merchandising của 8 market (G2.8) — không có thì mentor share màn hình/PDF đã che PII, hoặc dùng bộ ticket mô phỏng QA Lead viết từ ví dụ QA-02. Mentor chọn trước 3 ticket/học viên và kiểm không có dữ liệu nhạy cảm. Mang shadowing log (giấy hoặc file trên CoE workstation, không dùng sổ cá nhân mang về).

## Mục tiêu
Dựng timeline một ticket Shop Merchandising cũ từ History tab và comment; chỉ ra khác biệt giữa cách vendor hiện tại và process BiPlus trên cùng ticket; làm lại QA check trên giấy cho ticket promotion cũ (QCL-00, các test run cần, kết luận); viết lại kết luận bằng A.3/A.4 với defect category + RC code.

## Thuật ngữ
**Shadowing** (người mới quan sát người có kinh nghiệm làm việc thật, chưa tự quyết); **Mentor**; **Think-aloud** (mentor nói to suy nghĩ khi đọc ticket); **History tab (Activity)**; **Ticket timeline**; **Redo on paper**; **Shadowing log** (ghi ticket key, quyết định, lý do, câu hỏi; không có dữ liệu khách).

## Nội dung
### 1. Vì sao shadowing
Bài học cho luật, ticket thật cho thấy dữ liệu lộn xộn thế nào. Theo QA-01, BiPlus tiếp quản QA từng bước: Sprint 1 (02–08/11) QA Team chỉ quan sát vendor kiểm; Sprint 2 (09–15/11) làm 60%; Sprint 3–4 làm 100%; tiếp quản chính thức **30/11/2026**. Buổi này là luyện lớp học trước giai đoạn đó.

### 2. Quy tắc khi xem ticket thật
Chỉ đọc: không comment, không đổi status/field/Assignee. Không tải attachment (xem trong Jira); không chụp bằng điện thoại. Shadowing log chỉ chứa ticket key, **không ghi tên, email, số điện thoại** khách hay nhân sự subsidiary (G1.3). Mentor chọn 3 ticket/người: (a) promotion PASS QA ngay lần đầu; (b) ticket có label `QA_Returned`; (c) special price hoặc merchandising text. Ticket đã ở LAUNCH VERIFICATION hoặc CLOSED, trong 3 tháng gần nhất. Gợi ý các ticket vendor dùng làm ví dụ trong KB: SPHME-11594, AUME-18453, VNME-25924 (QA Returned Policy), VNME-10358, VNME-11556 (Merchandising Text) — mentor kiểm trước còn mở được và không nhạy cảm.

### 3. Đọc ticket ở 5 chỗ và dựng timeline
5 chỗ: **Description** (brief, priority, component); **danh sách attachment**; **Comments** (internal check, QA comment, câu hỏi subsidiary); **History tab** (khi nào đổi status, ai đổi); **Labels và Assignee** (`QA_Returned`, `qa=<knoxid>` — G2.8). Timeline mỗi dòng gồm giờ + time zone, status cũ → mới, người làm, hành động chính; từ đó tính thời gian ở QA REVIEW và số vòng trả.

| Giờ (ICT, ví dụ mô phỏng) | Status | Ai | Hành động |
|---|---|---|---|
| 09:12 | APPROVED-ES → STG SETUP | Merch PIC | Nhận ticket, comment phản hồi đầu |
| 14:40 | STG SETUP → QA REVIEW | Merch PIC | Setup xong, đính 2 ảnh self-check |
| 16:05 | QA REVIEW → STG SETUP | QA | Gắn `QA_Returned`: sai discount |
| 17:20 | STG SETUP → QA REVIEW | Merch PIC | Fix xong |
| 18:00 | QA REVIEW → LAUNCH VERIFICATION | QA | PASS, comment "QA done" (cách cũ của vendor) |

### 4. So với process BiPlus
4 câu hỏi: input có đủ 4 mục bắt buộc của QA-02 không; QA chạy những test nào, có negative test không; kết quả trả thế nào (comment, label, status); với OLA BiPlus ticket có kịp QA due không.
Khác biệt thường gặp:
- Vendor PASS rồi chuyển thẳng LAUNCH VERIFICATION. BiPlus: QA REVIEW → PRD SETUP (Shift Leader duyệt và chuyển) → REVIEW SETUP (owner hand-back kèm evidence, clock dừng) → PENDING LAUNCH (QA again trên production mỗi wave) → LAUNCH VERIFICATION sau wave cuối.
- Vendor nói SLA 1, 2, 3 ngày làm việc; BiPlus theo CM-13: 4, 16 hoặc 24 giờ, chỉ tính ở STG SETUP, QA REVIEW, PRD SETUP, ON HOLD COE.
- FAIL lần 2 cùng ticket: QA BiPlus báo QA Lead ngay (CM-05 §5.5), Shift Leader ghi root cause lên ticket (CM-03 §7.3).
- Evidence của vendor có thể là ảnh rời; BiPlus dùng PowerPoint theo template.

Timeline BiPlus tham chiếu (CM-05 §8.5, DEMO-4105, hai promotion, mô phỏng):
| Giờ (VN) | Status | Ai | Việc |
|---|---|---|---|
| 13:05 | QA REVIEW | Market Owner | Setup xong trên production, publish vào simulator, chuyển QA kèm evidence và ghi chú |
| 13:40 | STG SETUP | QA TM | Thiếu data (exclusion list); trả lại, QA gặp Market Owner trực tiếp |
| 14:00–15:30 | QA REVIEW | QA TM | Simulator, test cart, stacking, time zone: PASS; evidence PowerPoint trên CoE workstation |
| 15:45 | PRD SETUP | Shift Leader | Duyệt (brief, internal check, checklist, evidence, QA PASS) và chuyển ticket |
| 16:00 | REVIEW SETUP | Market Owner | Đính evidence, xin subsidiary duyệt, nêu cut-off 23:59; clock dừng |
| 00:00–00:30 wave 1 | REVIEW SETUP | Ca đêm, second checker certified | Không có duyệt trước 23:59 nên publish như đã hẹn; QA again trên production |
| 09:30 thứ Hai | PENDING LAUNCH | Subsidiary | Duyệt; ticket chờ wave 2 |
| 00:00 wave 2 | PENDING LAUNCH | Ca đêm | Publish promotion 2, QA again |
| 08:30 | LAUNCH VERIFICATION | Shift Leader ca ngày | Mọi wave live và đã kiểm |

### 5. Think-aloud, làm lại trên giấy, viết lại kết luận
- **Think-aloud:** mentor mở ticket (a) và nói to 4 quyết định: data đủ chưa; dùng checklist nào; chạy test run nào; kết luận gì và viết comment ra sao. Học viên ghi từng quyết định + lý do, hỏi "why" khi chưa rõ.
- **Làm lại trên giấy:** từ brief ticket cũ, chấm QCL-00, viết T1–T7 với expected, rồi đối chiếu evidence vendor đính kèm: vendor chạy case nào, thiếu case nào. Không mở lại setup trên production; chỉ dùng thông tin trên ticket.
- **Viết lại theo BiPlus:** vendor ghi "Wrong discount amount, QA_Returned" → A.4: `1. Promotion logic, RC-ENT: discount configured 10%; approved brief says 15%.` + câu "Re-check scope" + giờ đã nói với Doer.
- **Lỗi hay gặp:** đánh giá người trước thay vì học cách họ nghĩ; copy data ticket ra ngoài; coi SLA cũ là SLA hiện hành; vô tình comment lên ticket. Câu hỏi chưa có đáp án ghi vào trang câu hỏi cohort trên Samsung Confluence kèm ticket key, để QA Lead trả lời ở KT.

## Quiz (đáp án)
1 Thấy lỗi gõ SKU trong comment của Doer khi shadowing → **A: ghi shadowing log, hỏi mentor** (chỉ đọc). 2 File evidence trên ticket cũ → **B: xem trong Jira, không tải** (không ảnh điện thoại, không gửi kênh khác). 3 Ticket cũ QA PASS rồi chuyển thẳng LAUNCH VERIFICATION; theo BiPlus sau PASS ticket ở → **C: QA REVIEW, giao Shift Leader duyệt**. 4 Vendor ghi "Wrong discount amount" (rule 10%, brief duyệt 15%) → **D: Promotion logic, `RC-ENT`** (Doer nhập sai so với brief đúng; `RC-BRF` chỉ khi brief sai). 5 Muốn biết ticket nằm ở QA REVIEW bao lâu → **B: History tab**. 6 Ticket cũ chỉ có evidence cho cart đủ điều kiện → **D: thiếu negative test**.

## Practice
- **PR-QA3.1-1** (15', Jira chỉ đọc): với ticket (a), dựng bảng timeline như ví dụ, tính tổng thời gian ở QA REVIEW, đếm số vòng trả, trả lời 4 câu so sánh. Pass: mọi lần đổi status có giờ + time zone; thời gian ở QA REVIEW đúng (mentor kiểm trong History); ≥3 khác biệt so với QA-02. Không có access: mentor share History tab hoặc PDF đã che PII.
- **PR-QA3.1-2** (25', giấy/Confluence nháp): với ticket promotion mentor đưa, chỉ dùng thông tin trên ticket: (1) chấm QCL-00 dòng 0.1, 0.3, 0.4, 0.5, 0.8; (2) viết T1–T7 với input/expected theo brief; (3) đánh dấu case nào vendor có evidence, case nào thiếu; (4) viết kết luận BiPlus bằng A.3 hoặc A.4. Pass: QCL-00 có lý do từng dòng; 7 run có expected theo brief, giờ theo giờ market; xác định đúng case thiếu; comment theo template. Mentor sửa bằng cách so với cách họ làm (khác với QA-02 thì QA-02 thắng và mentor ghi lại khoảng chênh cho QA Lead).
- **PR-QA3.1-3** (15', giấy): với ticket có `QA_Returned`, liệt kê từng lỗi vendor ghi, xếp vào nhóm tiêu chí A–G của vendor, quy đổi sang defect category + RC code BiPlus, rồi viết lại thành **một** comment A.4. Pass: mỗi lỗi đúng một category và một code chính; dùng `RC-BRF` hoặc `RC-CHG` nếu ticket cho thấy brief sai hoặc subsidiary đổi yêu cầu; comment có "Re-check scope". Không có access: dùng ví dụ A.4 ở QA-02 Appendix A với 3 lỗi mentor đưa.
