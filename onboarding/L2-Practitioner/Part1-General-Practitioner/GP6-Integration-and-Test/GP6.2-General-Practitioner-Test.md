# GP6.2 General Practitioner test

> Nguồn: page 2483945897 · 60 phút (Study 15' · Demo/thảo luận 10' · Quiz 5' · Practice 30') · Bài test đóng sách, tình huống; facilitator: Shift Leader hoặc Sub-Lead (marker) · Capabilities C1, C5, C6 · Cần xong G6.3 (Final General test, L1), GP1–GP5 với quiz ≥80% và ca giám sát GP6.1. Mang bút và máy tính; đóng sách: không ghi chú, không điện thoại, không Confluence. Trước ngày thi đọc các mục trong Study materials. Không có Confluence: facilitator in các mục cần ôn và chạy bản giấy.

## Mục tiêu
Mô tả bốn phần của test, luật đạt và chuyện xảy ra sau khi rớt; tính SLA due time và thời điểm alert có khoảng dừng trong điều kiện đóng sách; phân loại case theo process, priority, risk tier và quyết định hành động tuân thủ trong compliance case; viết nhanh một ticket reply tiếng Anh đạt rubric T2 dưới áp lực thời gian.

## Thuật ngữ
**General Practitioner test** (bài thoát L2 Part 1: 60', đóng sách, theo tình huống, phủ C1, C5, C6); **Critical case** (câu bắt buộc đúng để đạt bất kể tổng điểm, VD "change production Tech không có PC ticket đã duyệt"); **Pass mark** (≥80% tổng, mọi critical case đúng, và bài viết đạt rubric T2); **Scenario item** (câu dựng trên tình huống ticket có giờ, status, giá trị, phải tính hoặc quyết định chứ không nhớ định nghĩa); **Retake** (thi bản thay thế sau khi coaching phần yếu); **Weak-topic list** (các chủ đề marker ghi trên phiếu kết quả sau khi rớt, dùng để coaching trước khi thi lại).

## Nội dung
### 1. Test kiểm gì và nằm ở đâu
L2 Part 1 kết thúc bằng hai bằng chứng: ca giám sát GP6.1 (Shift Leader/Sub-Lead ký) và bài test này. Hoàn tất Part 1 cần mọi quiz session ≥80%, ký GP6.1 và đạt test. Test phủ ba năng lực L2:
| Năng lực | Test hỏi gì | Dạy ở |
|---|---|---|
| C1 Service Management | SLA clock, priority, case thuộc process nào (request, incident, change, problem) | GP1.1–GP1.3 |
| C5 Compliance | Yêu cầu export dữ liệu, deadline đụng rule, tuân thủ PC ticket và Knox | GP4.1–GP4.3 |
| C6 Kỹ năng cá nhân | Một update hay reply đầy đủ đúng giọng và template | GP1.4, GP5.1, GP5.2 |
Mô hình theo test Academy trong CM-11: đóng sách, mức đạt 80%, critical item tự làm rớt. Người dưới mức đạt không bao giờ làm một mình.
> CM-11 định nghĩa T1–T8 nhưng không có test "General Practitioner" của L2. Format dưới theo outline chương trình L2 (test tình huống có tính SLA, phân loại, compliance case và bài viết; 80% và mọi critical case đúng). Format thi L2 còn chờ quyết định của Process and Knowledge Lead; trọng số các phần chưa cố định. **Under review (D12):** trong mapping CT trên program hub, GP6.2 phủ CT01 (C1) cộng case C5 và C6 mà chưa có CT exam; form CT chưa viết, format (CT: 40 câu / 45') nằm trong D12.

### 2. Format và phạm vi: bốn phần
| Phần | Làm gì | Ôn ở |
|---|---|---|
| A. Tính SLA | Tính SLA đã dùng, due time và giờ alert 50/70/85/95% có khoảng dừng | CM-03 1.4, 1.7, 2.9, 5.2 |
| B. Phân loại | Process (Service Request, Incident, Problem, Change), priority (High/Medium/Low; P0–P4), risk tier R1, R2, R3 và E4 | CM-11 3.2.1; CM-07 2.3, 2.4 |
| C. Compliance case | Chọn hành động tuân thủ: Knox lại, PC ticket, PII và yêu cầu dữ liệu, urgent, freeze, ON HOLD SUBS, strike | CM-13 ch.3, 8, 9, 10, 12, 17 |
| D. Bài viết | Viết một ticket reply hay update tiếng Anh từ template | CM-08 ch.4; rubric T2 |
Câu theo tình huống. VD Part A cho timeline ticket (Medium, STG SETUP 09:00, ON HOLD SUBS 11:00–14:30, về STG SETUP) và hỏi due time và giờ mốc 70%. Part C cho một yêu cầu ("gia hạn promotion này 2 ngày, không cần Knox") và hỏi bạn làm gì. Mọi số liệu là mô phỏng.
**Ví dụ Part A:** Medium, 16 giờ. Đã dùng 2 giờ trước 11:00; dừng 3 giờ 30 ở ON HOLD SUBS; quay lại 14:30 còn 14 giờ: due 04:30 hôm sau. Mốc 70% là đã dùng 11 giờ 12': sau 14:30 thêm 9 giờ 12' = 23:42; Shift Leader hành động trong 15'.

### 3. Chấm điểm và critical case
- **Đạt:** ≥80% tổng, **và** mọi critical case đúng, **và** bài viết đạt rubric T2 (không tiêu chí nào 1 điểm, tổng ≥10/15).
- **Critical case** đánh dấu trên giấy, lấy từ danh sách critical error CM-11 và critical item G6.3 của L1: change production Tech không có PC ticket đã duyệt (kể cả rollback); bỏ Knox cho giá/promotion, hoặc không xin lại khi action, condition, website hay date đổi; đưa dữ liệu ra ngoài hệ thống Samsung hoặc gửi PII qua email; dùng ON HOLD SUBS chỉ để dừng clock; bypass QA gate hoặc tự duyệt. Lab thêm một: setup trong freeze không có evidence duyệt = 0 điểm ở TRN-029.
> **Under review (D1, D2):** tới khi chốt, hai trường hợp không chấm critical: ticket ở ON HOLD SUBS với Doer là Assignee khi chờ Knox (D1) và rule chỉ-quà publish không Knox (D2). Không câu thi nào được chấm hai trường hợp này.
- **Marker** là Shift Leader/Sub-Lead chạy session; kết quả ghi trên phiếu như phiếu kết quả T3 của CM-11: điểm từng phần, tổng và %, kết quả, chủ đề yếu cần coaching, marker, ngày.

### 4. Luật thi lại
CM-11 xử lý bài rớt hai bước:
| Test | Rớt lần 1 | Rớt lần 2 |
|---|---|---|
| T3 knowledge test (mô hình gần nhất cho Part A–C) | Thi lại Day 6 sau coaching phần yếu | Thêm một tuần foundation; làm việc live lùi một sprint |
| T2 writing work-sample (mô hình cho Part D) | Coaching, thi lại trong 2 ngày làm việc | Không gửi RHQ; chuyển sang vai không tiếp xúc subsidiary, hoặc thay bằng ứng viên thứ hai |
Với General Practitioner test áp dụng cùng hai bước tới khi Lead đặt rule riêng: rớt lần đầu, marker ghi chủ đề yếu lên phiếu, bạn học lại các GP session tương ứng với buddy, rồi thi bản thay thế. Critical case sai là rớt dù tổng 90%. Trong lúc đó vẫn làm việc có giám sát: không certification, không làm một mình.
> Luật thi lại cho General Practitioner test chưa viết trong CM-11. Quy tắc hai bước trên là đề xuất của tác giả khoá học dựa trên hàng T3 và T2 của CM-11 §3.1; Process and Knowledge Lead phải xác nhận thời gian chờ trước khi thi lại và hậu quả của lần rớt thứ hai.

### 5. Chuẩn bị tuần cuối
- **Part A:** làm lại bài tập CM-03 có khoảng dừng; luôn ghi time zone; nhớ comment không đổi clock và ON HOLD COE vẫn tính.
- **Part B:** luyện ngân hàng câu hỏi CM-11, câu 1–25 và 46–53 (Service Management, Merchandising, Jira workflow); với E4 nhớ ba trigger (exposure ≥10,000 USD, >5 market, price file ≥500 SKU) và "không tính được exposure = E4".
- **Part C:** luyện câu 54–68 (luật RHQ theo CM-13). Mỗi câu nói rule và chương nguồn.
- **Part D:** viết ba reply bấm giờ (10 phút mỗi cái) và chấm theo rubric T2 với buddy.

## Quiz (đáp án) — mẫu phong cách đề; đề thật nhiều câu hơn mỗi phần
1 **Part A.** Ticket Medium vào STG SETUP 09:00, sang ON HOLD SUBS (đã hỏi, giao subsidiary) 11:00, về STG SETUP 14:30; due → **B: 04:30 hôm sau** (đã dùng 2h; dừng 3h30; còn 14h từ 14:30; A bỏ qua 2h, D quên khoảng dừng). 2 **Part A.** Ticket Tech P1 (8 giờ) NEW → ASSIGNED 21:00, ở status tính; chạm 70% lúc nào, ai hành động → **A: 02:36; Tech Sub-Lead hành động trong 15' (ngoài khung Tech là layer 1 on-call)** (B là mức 85%). 3 **Part B.** Cùng lỗi hiển thị giá xảy ra 4 lần trong tháng trên các ticket khác nhau; mở gì → **C: Problem record tìm root cause**. 4 **Part B.** Price file 650 SKU cho một market; tier và duyệt → **D: R3 chạm E4: internal check, price sanity, QA, Shift Leader, thêm Merch Lead hoặc Deputy (critical)**. 5 **Part C (critical).** Promotion đã publish phải đổi 10% → 15%, subsidiary viết "không cần Knox, cùng promotion" → **B: đổi được; lần publish kế phải Knox lại vì action đổi** (C là cách bypass Knox, bị cấm). 6 **Part C (critical).** Subsidiary xin email khách đã mua sản phẩm để gửi EDM → **D: từ chối mặc định; không bao giờ gửi PII qua email từ Hybris**. 7 **Part C.** Tình huống TRN-029: xin gia hạn PWP trong Ops CoE setup stop và Hybris soft freeze, không PUMI, label Urgent_Request → **B: không setup; chuyển ON HOLD RHQ với một comment nêu freeze, khoảng hết hạn, Knox lại, nhu cầu QA và đề xuất giờ sau freeze**. 8 **Part D.** Reply đạt T2 cho ticket chờ một end date thiếu → **B: "Hello [Name], to proceed with the MY promotion we need the end date and time (local time). We have prepared everything else and can finish within 1 hour of your reply. This ticket is now assigned to you; please reply here."**

## Practice
**PR-GP6.2-1. General Practitioner test** (đóng sách, 60', cá nhân, không điện thoại; facilitator phát đề (Part A–D) và phiếu kết quả). Làm cả bốn phần; ở Part D viết một reply hoặc update tiếng Anh theo đúng template. **Pass:** ≥80% tổng điểm; mọi câu đánh dấu critical đúng; bài Part D đạt rubric T2 (không tiêu chí nào 1 điểm, ≥10/15). Marker ghi điểm từng phần, kết quả và chủ đề yếu lên phiếu. Bản giấy; không cần truy cập hệ thống.
