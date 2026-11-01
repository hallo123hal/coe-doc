# GP1.2 The SLA clock in practice

> Nguồn: page 2484011210 · 75 phút (Study 20' · Demo/thảo luận 10' · Quiz 10' · Practice 35') · Thực hành theo case trên staging và practice ticket; facilitator: Shift Leader hoặc Sub-Lead · Capabilities C1, C4 · Cần xong G2.3 (budget theo priority, ví dụ DEMO-8101, 4 mức alert) và G2.2 (status tính/dừng/không tính); mang spreadsheet (mỗi cột một lần đổi status, giờ ICT) và bảng alert CM-03 §5.3. Chỉ cần Confluence (đọc CM-03, CM-09). Không có Confluence: facilitator in 3 lịch sử ticket + CM-03 §2.9, 5.3, 5.5.

## Mục tiêu
Tính due time và các mốc 50/65/70/85/95% của ticket có khoảng dừng, sai số ±5'; lập kế hoạch ticket Merch chờ COEC liên kết và nói người tạo COEC phải làm gì ở mỗi level; tiếp tục clock đúng sau reopen và nhận ra thay đổi priority không được phép; viết alert comment 50/70/85% đúng mẫu và nói ai hành động ở mỗi mức.

## Thuật ngữ
**Paused time** (phút ở ON HOLD SUBS, ON HOLD RHQ, REVIEW SETUP (Merch) hoặc ON HOLD SUBSIDIARY, SYSTEM SUPPORT, ON HOLD HQ, ON HOLD ES (COEC); mỗi phút dừng đẩy deadline và mọi mốc muộn đi một phút); **Answer time** (lúc subsidiary trả lời, không phải lúc bạn chuyển ticket lại; reply 13:00 chuyển lại 13:25 vẫn tính tới 13:00); **Provisional deadline**; **Two parallel clocks** (ticket Merch ở ON HOLD COE vẫn chạy khi COEC liên kết có clock riêng, có thể đang dừng); **Remaining budget** (ticket Low reopen đã dùng 15h tiếp tục với 9h, không bao giờ 24h); **Alert comment**; **Substitute filter** (filter JQL COE-F05…F08 tính từ APPROVED-ES kể cả thời gian dừng nên báo sớm hơn thực tế); **OLA per step**.

## Nội dung
### 1. Due time khi có khoảng dừng
**Due = start + budget + tổng thời gian dừng.** Start là lúc vào APPROVED-ES (Merch) hoặc tạo ở NEW (COEC), theo ICT. Hiện tại tính giờ lịch 24/7 (mẹo: 16h = "+1 ngày −8h"; 40h = "+2 ngày −8h"). 6 bước CM-03: (1) priority và budget; (2) start ICT; (3) deadline ban đầu; (4) cộng mọi khoảng dừng; (5) quy đổi giờ địa phương requester; (6) tính mốc 65% và 4 mức alert, cũng dời muộn đi theo thời gian dừng trước đó. **ON HOLD COE và QA REVIEW không cộng thêm: chúng được tính.**
**Ví dụ CM-03 B1:** Medium vào APPROVED-ES 13:00 thứ Tư, ON HOLD SUBS 15:00–17:00 → 50% 23:00 Wed (đã dùng 8h); 65% 01:24 Thu (10h24); 70% 02:12 Thu (11h12); 85% 04:36 Thu (13h36); 95% 06:12 Thu (15h12); deadline 07:00 Thu (16h). Mốc 50% rơi vào ca tối, phần còn lại ca đêm nên note bàn giao 16:00 và 00:00 đều phải nhắc ticket này; mốc 85% ngoài giờ làm việc thì người nhận là Merch Lead on-call.
Khi hỏi subsidiary phải làm ba việc cùng lúc: comment câu hỏi, ON HOLD SUBS, Assignee = subsidiary. Subsidiary trả lời (thường chỉ comment) thì chuyển lại ngay. Shift Leader quét "ON HOLD SUBS có Assignee là CoE" mỗi 30'.
> CM-03 lập kế hoạch từ APPROVED-ES "cho an toàn". Theo CM-13 Resolution clock chỉ đếm ở STG SETUP, QA REVIEW, PRD SETUP, ON HOLD COE trong khi slide handover 23/10 cũng liệt kê APPROVED-ES là đếm. Khi lập kế hoạch bắt đầu từ APPROVED-ES; khi đo theo CM-13. Medium/Low tính giờ lịch hay giờ làm việc còn mở với RHQ; lập kế hoạch 24/7.
> **Under review (D6):** cơ sở SLA còn mở: giờ RFP hay guideline ngày làm việc của SDSAP/RHQ (High 1, Medium 2, Low 3 ngày). Tạm thời làm theo giờ RFP (mục tiêu ngắn hơn).

### 2. COEC liên kết và ON HOLD COE: lập kế hoạch cả hai clock
Khi một phần việc cần Tech: giữ ticket Merch, tạo COEC với issue link, chuyển ticket Merch sang ON HOLD COE kèm comment. COEC chạy SLA Tech; ticket Merch **vẫn chạy** SLA của nó. COEC ở ON HOLD HQ (chờ PC ticket) hoặc SYSTEM SUPPORT thì chỉ clock Tech dừng. Người tạo COEC chase Tech ngay từ đầu.
**Ví dụ DEMO-1240 (AU, Medium, mô phỏng):** APPROVED-ES 06:00 thứ Tư (10:00 AEDT), deadline 22:00. 06:10 STG SETUP; 06:30 tạo DEMO-1241, DEMO-1240 sang ON HOLD COE. Tech nhận 06:45, test staging, gửi PC 10:00 (ON HOLD HQ, clock Tech dừng). DEMO-1240 vẫn chạy: 14:00 mức 50% — Shift Leader ca ngày ghi bước kế "waiting for PC ticket; afternoon Tech runs the ImpEx as soon as approved; QA scheduled"; 17:12 mức 70% — Shift Leader ca tối báo Tech Lead và QA dispatcher giữ người sẵn sàng; 17:30 PC duyệt, chạy ImpEx, DEMO-1241 sang LAUNCH VERIFICATION 18:15; 19:10 (82%) kiểm xong, QA pass, duyệt, REVIEW SETUP — trước mức 85% (19:36) 26 phút. Nếu duyệt PC chậm ~3 giờ (approver vắng) thì DEMO-1240 vượt 85% và sát deadline 22:00. Filter CM-09 COE-F10 liệt kê ticket Merch ở ON HOLD COE có COEC liên kết; ON HOLD COE không có link là chờ thỏa thuận nội bộ, Shift Leader quyết trong ca.
> **Under review (D7):** workflow COEC 2026 tại handover dùng nhãn khác: SUBSIDIARY thay ON HOLD SUBSIDIARY, ON HOLD RHQ thay ON HOLD HQ, không có WAITING QA. Dùng nhãn Jira hiển thị.

### 3. Hand-back, reopen, thay đổi priority
Resolution dừng ở **hand-back**: Merch chuyển REVIEW SETUP kèm evidence QA; Tech chuyển LAUNCH VERIFICATION và giao người tạo. Không dừng khi ticket ở QA REVIEW, chờ Shift Leader duyệt, hay ON HOLD COE. Setup, QA, duyệt xong cho go-live tương lai thì chuyển REVIEW SETUP ngay: để ở STG SETUP hay PRD SETUP chờ ngày go-live thì clock chạy và sẽ breach.
**Reopen:** subsidiary trả ticket từ REVIEW SETUP về bước làm hoặc báo kết quả sai. Giữ priority gốc và tiếp tục với **budget còn lại**, không reset. VD Low đã dùng 15h trước REVIEW SETUP, trả lại 09:00 còn 9h → deadline 18:00; 65% (15h36) tới lúc 09:36, gần như ngay.
**Cancel/duplicate:** INVALID đóng hẳn và phải có lý do; muốn làm lại thì clone. Duplicate: giữ ticket đầu, link ticket sau và chuyển INVALID "Duplicate of …".
**Đổi priority:** chỉ sửa khi phân loại sai so bảng RFP, bởi Shift Leader hoặc Sub-Lead, có lý do trên ticket. Nâng khi impact thực sự đổi (VD subsidiary báo ảnh hưởng doanh thu lớn hơn). Không hạ/nâng để tránh SLA, không vì ca bận: dùng thang alert và đòn bẩy huy động (giao lại, điều người giữa các market, gọi bench/on-call).
> Nguồn chưa nói SLA plug-in mang thời gian đã dùng thế nào khi priority sửa giữa chừng (open point cho Lead và Atlassian Platform Engineer). Tạm thời ghi giờ sửa + lý do, tính lại deadline với Shift Leader và đưa vào note bàn giao.
**Không được "làm đẹp số":** ON HOLD giả để dừng clock; đổi priority để tránh SLA; INVALID rồi clone; tách ticket để reset clock; ticket mới thay vì reopen; PENDING LAUNCH để tránh SLA.
**Được phép (runbook sửa đổi + handover 27/10):** senior tách ticket lớn gộp thành sub-ticket liên kết cho Doer/Checker khác (ticket chính giữ, tiến độ comment ở đó); PENDING LAUNCH cho go-live xa (raise trước vài tuần/tháng; setup khoảng một tuần trước go-live vì làm sớm thường phải làm lại; luôn comment lý do; RHQ kiểm status này, không dùng để dừng clock; QA kiểm lại ngày go-live); ticket đã đóng mà subsidiary mở lại thì không làm, xin ticket mới; INVALID không bao giờ mở lại mà clone.
> **Under review (D15):** handover cho phép ticket mới khi subsidiary đổi scope sau khi QA bắt đầu hoặc sau khi Knox đã submit (đổi nhỏ: làm ngay; đổi lớn: xin ticket mới và giải thích SLA). Ai quyết nhỏ hay lớn chưa chốt; hỏi Shift Leader.

### 4. Mục tiêu 65% và budget theo bước
Mục tiêu nội bộ là xong mỗi ticket ở **65%** budget: High/P0 2h36, P1 5h12, Medium/P2 10h24, Low 15h36, P3 26h, P4 78h. BiPlus chia budget Merch thành OLA nội bộ:
| Bước | Giới hạn (OLA nội bộ) |
|---|---|
| APPROVED-ES → STG SETUP | 78' (High 15'); priority sai sửa trong 30' |
| Build (STG SETUP) | Xong trước 65%, không tính QA và duyệt |
| QA REVIEW | High 30'; khác 2 giờ làm việc cho 1–2 item |
| Shift Leader duyệt | High 15'; khác 30' |
| QA + duyệt cộng lại | Tối đa 25% budget còn lại khi ticket chuyển QA |
| Knox (giá, promotion) | Gửi ngay sau khi Shift Leader duyệt; không có Jira status, clock vẫn chạy (D1, D5 under review) |
> **Under review (D1, D5):** runbook sửa đổi giữ ticket ở ON HOLD SUBS với Doer là Assignee trong lúc chờ Knox, comment mỗi 2–3 ngày làm việc vì chỉ người submit thấy bước duyệt. Với promotion còn yêu cầu subsidiary green light ở REVIEW SETUP trước khi submit Knox; với giá thì Knox trước. Mục chờ Knox không chấm tới khi D1 chốt.
**Ví dụ CM-03 4.3 (MY, Medium):** APPROVED-ES 10:00; STG SETUP 10:12; ON HOLD SUBS 10:20–11:30 (reply 11:30, chuyển lại 11:35). Deadline mới 03:10, 65% 21:34. QA REVIEW 15:00 đã dùng 3h50, còn 12h10, 25% ≈ 3 giờ nên QA + duyệt xong trước 18:00. REVIEW SETUP 16:45 sau 5h35 (~35%).

### 5. Alert 50/70/85/95%: hành động và ghi lại
| Mức | Ai hành động | Trong | Comment phải thêm |
|---|---|---|---|
| 50% | Assignee | – | Thời gian còn lại, status, bước kế và giờ |
| 70% | Shift Leader (Merch) hoặc Sub-Lead (Tech, QA) | 15' | Quyết định: giao lại, thêm người, chase COEC liên kết |
| 85% | Lead; Lead on-call ngoài giờ | 30' | Quyết định của Lead (workaround, ETA cho subsidiary) |
| 95% | COE Lead báo RHQ (SDM trước 01/12/2026) | Trước breach, trong 1 giờ | Giờ báo RHQ, nguyên nhân, ETA |
Alert theo SLA **đã dùng**: ticket đang dừng không chạm mức mới. Ticket Merch ở ON HOLD COE đi qua đủ 4 mức. Ticket 4 giờ thì thang bị nén: ở 85% chỉ còn 36', ở 95% chỉ còn 12', và incident process chạy song song.
Alert chỉ tính khi ghi trên Samsung Jira, tiếng Anh, theo mẫu:
```
[SLA 70%] Remaining 4h48 (due 03:20 ICT). Status: QA REVIEW.
Action: reassigned to [name], QA dispatcher informed. Next check: 23:00 ICT.
Owner: [name]. Shift Leader: [name].
```
Requester và RHQ đọc được các comment này nên viết trung tính, không đổ lỗi; không viết "SLA is paused" trong comment gửi subsidiary. Khi SLA plug-in chưa chạy, filter COE-F05 (50%) … COE-F08 (95%) tính từ APPROVED-ES kể cả thời gian dừng nên báo sớm: mở ticket kiểm thời gian đã dùng thật trước khi hành động. Ticket breach phải có ≥3 alert đã ghi trước đó; không có thì là lỗi process, ghi nguyên nhân trong 1 ngày làm việc.

## Quiz (đáp án)
1 Low vào APPROVED-ES 14:00 thứ Hai, 16:00 hỏi subsidiary (ON HOLD SUBS, assigned), subsidiary comment trả lời 18:30, bạn chuyển lại 19:10 → deadline **B: 16:30 thứ Ba** (24h + 2h30 tới answer time; C sai vì cộng cả 40' bạn chậm). 2 Ticket Merch Medium ở ON HOLD COE, COEC liên kết P3 chuyển ON HOLD HQ → **B: Merch chạy, COEC dừng**. 3 Low đã dùng 15h trước REVIEW SETUP, trả về STG SETUP 09:00 → **A: 65% lúc 09:36, deadline 18:00**. 4 20:30 Medium chạm 70%, assignee bận ticket High → **B: Shift Leader trong 15' post `[SLA 70%] Remaining 4h48 (due 01:18 ICT)…` kèm giao lại** (C, D bị cấm). 5 P2 COEC đã dùng 9h chuyển SYSTEM SUPPORT 12:00 thứ Tư; 20:00 thứ Năm → **B: vẫn 56%, không alert mới, nhưng follow up theo nhịp RFP (P2: mỗi 2 ngày làm việc, tới 12:00 thứ Sáu)**. 6 High bắt đầu 09:00 không dừng, 12:48 vẫn mở → **C: còn 12'; COE Lead báo RHQ ngay, incident process song song** (đã dùng 3h48 = 95%). 7 Hành động được phép → **C: chuyển REVIEW SETUP ngay khi setup, QA, duyệt xong dù go-live tuần sau**.

## Practice
**PR-GP1.2-1. Ba ticket giống thật** (35', spreadsheet; giờ ICT, giờ lịch 24/7, start = APPROVED-ES hoặc NEW):
- **Ticket A (MY, Medium, 1 promotion):** APPROVED-ES 09:20 thứ Hai; STG SETUP 09:35; ON HOLD SUBS từ 11:00 (assign subsidiary); subsidiary comment trả lời 13:00; chuyển lại STG SETUP 13:25.
- **Ticket B (VN, Low, product status):** APPROVED-ES 08:00 thứ Ba; STG SETUP 08:30; QA REVIEW 14:00–15:00; PRD SETUP 15:00; REVIEW SETUP 16:00. Thứ Tư 10:00 subsidiary trả về STG SETUP (còn một SKU hiện).
- **Ticket C (SG, High, giá sai đang live):** APPROVED-ES 09:00; STG SETUP 09:10; 09:40 tạo COEC P2 liên kết sửa data Tech, Ticket C sang ON HOLD COE. COEC: NEW 09:45, ASSIGNED 10:00, ON HOLD HQ (PC) 10:30–11:30, LAUNCH VERIFICATION 12:00. Ticket C: về STG SETUP 12:05, QA REVIEW 12:20–12:50, PRD SETUP 12:50, REVIEW SETUP 12:58.
Việc: mỗi ticket tính SLA đã dùng lúc hand-back, due time, mốc 65% và 50/70/85/95%; viết comment 70% cho A và C; với C cho thêm SLA COEC đã dùng. **Pass** (sai số ±5', do tác giả khoá học tính, cần Lead xác nhận): **A** dừng 2h00 (11:00–13:00, không phải 13:25); due 03:20 thứ Ba; 50% 19:20, 65% 21:44, 70% 22:32, 85% 00:56, 95% 02:32; **B** 8h00 đã dùng lúc REVIEW SETUP, còn 16h sau reopen; due 02:00 thứ Năm; 50% 14:00, 65% 17:36, 70% 18:48, 85% 22:24 (thứ Tư), 95% 00:48 thứ Năm; **C** không có thời gian dừng (ON HOLD COE tính); due 13:00; 50% 11:00, 65% 11:36, 70% 11:48, 85% 12:24, 95% 12:48; 3h58 đã dùng lúc hand-back (99%); comment 70% nêu COEC liên kết và status (ON HOLD HQ, PC pending); COEC dùng 1h15/16h (8%). Không đề xuất hành động bị cấm (không ON HOLD SUBS không câu hỏi, không đổi priority, không ticket mới cho B).
