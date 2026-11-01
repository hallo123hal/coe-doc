# MER-1.4 Intake duty: the first minutes of a Merchandising ticket

> Nguồn: page 2492793245 · 50 phút (Study 18' · Demo 8' · Quiz 7' · Practice 17') · Talk + xem dashboard APPROVED-ES (live hoặc screenshot), drill intake theo cặp; facilitator: Shift Leader (Sub-Lead) · Cần xong MER-1.1, 1.2, 1.3 (+ G2.2, G2.3); mở sẵn bảng MR-05 §1.3 và MR-04 Appendix A; facilitator in 4 item mô phỏng của PR-MER-1.4-1 và phát đúng giờ ghi trên đó.

## Mục tiêu
Nêu việc người trực intake theo dõi, nhịp, khi nào gọi Shift Leader; xử lý request đến ngoài Jira trong 5 phút không tạo trùng; initial response bằng đổi status kèm comment đủ 5 điểm trong target nội bộ; phân loại ticket mới theo 7 mục và đề xuất tier/E4/QA gate; nhận ra dấu hiệu incident, last-minute, sai team ngay tại intake.

## Thuật ngữ
**Intake duty** (nhận việc mới trong ca; Shift Leader chỉ định ở stand-up, ghi vào shift plan; ca ngày có thể chia 2 người theo khung giờ); **APPROVED-ES dashboard** (ticket subsidiary đã duyệt, giao CoE, chưa sang STG SETUP; quét mỗi 5'); **Initial response** (chuyển APPROVED-ES → STG SETUP; comment không dừng clock); **Classification** (7 quyết định: loại ticket & team, service, market & kênh, priority, risk tier & E4, QA gate, due date); **E4 flag**; **Golden Rule 4** (mọi request vào Jira trong 5').

## Nội dung
### 1. Ai trực intake và theo dõi gì
Merch không có "intake desk" — Shift Leader chỉ định 1 TM ở stand-up; mọi TM đều luân phiên. Theo dõi: dashboard APPROVED-ES (mỗi 5'); comment mới của subsidiary trên Jira; mailbox chung CoE và Mattermost (≥ mỗi 5'). Hotline do Shift Leader nghe rồi chuyển bạn log. Thấy dấu hiệu ticket High hoặc incident → báo Shift Leader ngay, không chờ vòng sau.

### 2. Request đến ngoài Jira: 5 phút
Jira là bản ghi duy nhất; request chỉ nằm trên Mattermost/email coi như chưa nhận (không ai thấy trong queue, ca sau không biết, CoE không có gì chứng minh khi tranh chấp).
- **Việc Merch:** bạn *không tự tạo* ticket Shop Merchandising vì bước PLANNING REVIEW thuộc subsidiary → trả lời requester, yêu cầu họ tạo ticket, ghi request + giờ vào handoff note tới khi ticket xuất hiện.
- Đã có ticket (cùng requester, cùng nội dung, 7 ngày gần nhất) → comment lên ticket đó, không tạo trùng.
- **Việc Tech:** tạo COEC ticket với requester đúng và summary `[Market] [Service] [Short content]`, gửi mã ticket cho requester trong cùng thread.
- File ở lại Jira/Confluence Samsung; không lưu máy hay hệ thống BiPlus.

### 3. Initial response: status trước, comment sau
Clock bắt đầu khi ticket vào APPROVED-ES, chỉ dừng khi sang STG SETUP; "Noted"/"Received" không dừng. Target nội bộ: **High 15'; Medium/Low 78'**; hợp đồng 2 giờ, ≥97%/tháng.
- Viết first-response comment (A.1) cùng lúc đổi status, đủ **5 điểm**: yêu cầu là gì (bằng lời bạn); service & priority; owner; bước kế tiếp + giờ update kế (SGT); câu hỏi làm rõ (tất cả trong 1 comment). Có hỏi → chuyển ON HOLD SUBS và assign requester (MER-1.2).
- **Owner:** ca ngày đề xuất Market Owner của market (quá tải thì Shift Leader chọn TM luân phiên); ca E/N đề xuất TM trong ca; Shift Leader xác nhận mọi assignment.
- Trước khi gửi, chạy intake checklist: requester & market, việc cần làm, scope, giá trị, thời gian + time zone, approval, Knox path trong brief, file, acceptance criteria, phụ thuộc. Thiếu gì đưa vào cùng comment thành câu hỏi đánh số. 4 tuần đầu (hoặc tới khi 50 message đạt chuẩn) Shift Leader/buddy đọc message trước khi bạn gửi.

### 4. Phân loại 7 mục

| # | Quyết định | Cách làm | Ai quyết |
|---|---|---|---|
| 1 | Loại ticket & team | Service Request / incident / BVT / câu hỏi; Merch hay Tech | Bạn; Shift Leader khi nghi incident hoặc sai team |
| 2 | Service | Tra catalogue MR-05, không chọn service chung chung cho nhanh | Bạn |
| 3 | Market & kênh | 1 trong 8 market; B2C/EPP/SMB/O2O/3PD; kiểm market thứ hai | Bạn |
| 4 | Priority | Mặc định theo service, chỉnh theo tác động thật (1 promotion: theo catalogue; 2: Medium; ≥3: Low) | Bạn; Shift Leader sửa sai trong 30' |
| 5 | Risk tier & E4 | R1/R2/R3 theo catalogue & CM-07; E4 khi đủ 1 trong 3 điều kiện; đếm SKU trong price file | Bạn đề xuất; Shift Leader xác nhận |
| 6 | QA gate | Mandatory/sampling/none theo catalogue; R1 không bao giờ qua QA Team | Theo catalogue |
| 7 | Due date | Sớm hơn giữa SLA deadline và (go-live − thời gian check) | Bạn; owner xác nhận |

Ghi thêm lên ticket: giờ go-live từng promotion (giờ market + VN), số wave, ngôn ngữ nội dung. Ticket nhiều thay đổi lấy tier cao nhất; không hạ tier/priority để nhanh. Bulk >100 dòng cần diff file bất kể tier. Không ước lượng được exposure → đề xuất E4 để Shift Leader quyết và ghi lý do.

### 5. Cái gì không phải request bình thường
3 câu hỏi trước khi coi là Service Request: có gì sai trên production ảnh hưởng khách/doanh thu (sai giá, sai promotion, không đặt được hàng)? có dấu hiệu lộ data/vi phạm bảo mật? có hệ thống không truy cập được? — một "có" là báo Shift Leader ngay; Shift Leader quyết có mở incident không.
- **Last-minute:** ticket R3 (hoặc R2 có QA gate) được duyệt sau 17:00 VN để go-live đêm nay → báo Shift Leader ngay để xét QA còn thời gian không; QA chỉ bị bỏ khi không kịp (MER-1.2).
- **Sai team:** toàn bộ việc là Tech → move chính ticket sang COEC; Merch còn việc → giữ ticket + linked COEC.
- **Trùng:** link tới ticket gốc, comment "Duplicate of DEMO-xxxx, all updates will be on that ticket", chuyển INVALID với lý do Duplicate.
Ví dụ (CM-05): 10:05 Thứ Ba ticket AU DEMO-3110 vào APPROVED-ES (15% off tai nghe, "start Wednesday midnight"); TM intake chuyển STG SETUP lúc 10:12 (initial response 7'); brief thiếu time zone & end date; 10:20 viết 1 câu hỏi 2 ý, ON HOLD SUBS, assign requester; 13:05 requester trả lời không đổi status; 13:08 owner đưa về STG SETUP. Go-live 20:00 giờ VN cùng ngày → Shift Leader coi là last-minute, QA vẫn kịp, setup phải tới QA trước 17:00.

## Quiz (đáp án)
1 14:02 RHQ PIC nhờ đổi banner SG trên Mattermost → **yêu cầu tạo ticket Shop Merchandising và ghi vào handoff note**. 2 High vào APPROVED-ES 09:40, 09:48 comment "Received" → **chưa xong; clock chỉ dừng ở STG SETUP**. 3 Ai đặt risk tier → **intake đề xuất, Shift Leader xác nhận**. 4 Special price 12 SKU + flag Hot Deal → **R3 (tier cao nhất)**. 5 Coupon 40 USD, 300 lượt, 1 market → **R3 và E4 (40×300 = 12.000 USD ≥ 10.000)**. 6 17:40 R3 VN go-live 00:00 → **báo Shift Leader ngay để kiểm thời gian QA**. 7 Ca ngày ticket VN mới → **đề xuất VN Market Owner; Shift Leader xác nhận**.

## Practice
- **PR-MER-1.4-1 Intake desk drill** (12'): bạn trực intake ca ngày Thứ Hai từ 09:00 với 4 item: (1) 09:02 DEMO-5201 MY, buy 2 get 15% off 30 SKU, bắt đầu 05/12 00:00, thiếu time zone end date, chi phí ~3.000 USD, đã có cột approval path; (2) 09:04 RHQ PIC nhờ đổi banner SG hôm nay, không T&C; (3) 09:06 DEMO-5203 TH, special price file 620 dòng, 08/12 00:00 ICT; (4) 09:09 DEMO-5204 PH: giỏ hiển thị 0 PHP cho Galaxy Watch từ 08:30. Pass: (4) xử lý trước — báo Shift Leader ngay vì giống sai giá trên production, Shift Leader quyết incident; (2) trả lời trước 09:09 yêu cầu tạo ticket, ghi handoff; sau khi có ticket là AEM-04, R1, SL checks; (1) PRM-01, Medium, R3, QA Mandatory, không E4; chuyển STG SETUP rất sớm trong 78'; comment đủ 5 điểm + 1 câu hỏi đánh số về time zone kết thúc; ON HOLD SUBS, Assignee = requester; đề xuất MY Market Owner; (3) PRC-02, Low, R3, QA Mandatory, **E4 vì ≥500 SKU**; ghi diff file + dry run (>100 dòng) và báo Shift Leader cần Lead/Deputy duyệt cấp 2.
- **PR-MER-1.4-2** (cặp, 5'): đổi chéo first-response comment; đối tác đóng vai Shift Leader, tick đủ 5 điểm rồi xác nhận/đổi tier, E4, owner của DEMO-5201 và DEMO-5203 kèm một dòng lý do cho mỗi thay đổi. Pass: tìm ra mọi điểm thiếu; không có kiểu "Noted" thiếu bước kế và giờ update SGT.
