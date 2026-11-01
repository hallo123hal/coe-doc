# GP6.1 Capstone: one supervised shift

> Nguồn: page 2484404331 · 120 phút (Study 30' · Demo/thảo luận 20' · Quiz 10' · Practice 60') · Thực hành theo case trên staging và practice ticket; facilitator: Shift Leader hoặc Sub-Lead · Capabilities C1–C6 · Cần xong G6.2 (L1) và toàn bộ GP1–GP5. Truy cập: staging Backoffice (el3-s2), thêm HAC staging chỉ cho Tech; Jira SCOE, Confluence (đọc). Kiểm login từ hôm trước: lỗi login trong ngày là bắt đầu thất bại, không phải lý do bỏ bước. Mang mẫu handoff note (CM-04 6.5.1 cho Merch, 6.5.2 cho Tech và QA), checklist vai trò CM-04 ch.10 và runbook các service trong queue. Chưa có access thì không chạy được session này; lên lịch sau khi có access.

## Mục tiêu
Chạy một ca đầy đủ trên ticket SCOE: đọc handoff, lập plan, nhận intake, giữ SLA, làm và kiểm ticket, escalate và bàn giao; phản hồi mọi ticket mới bằng đổi status trong target nội bộ (15, 30 hoặc 78'); ghi mọi cảnh báo SLA, escalation và câu hỏi lên ticket ngay lúc xảy ra; viết handoff note đầy đủ không ticket nào thiếu owner; kết thúc ca không có critical error để observer ký.

## Thuật ngữ
**Supervised shift** (ca đầy đủ bạn tự chạy trên ticket SCOE trong khi Shift Leader/Sub-Lead quan sát bằng checklist và chỉ can thiệp để ngăn critical error); **Observer** (Shift Leader/Sub-Lead quan sát, ghi evidence vào checklist ký xác nhận; không phải Checker của ticket bạn); **Critical error** (lỗi tự nó làm rớt session, VD dùng ON HOLD SUBS chỉ để dừng clock, hoặc build R3 mà ticket không có internal check); **Exit criteria**; **Shift plan**; **Absent-assignee filter** (filter Shift Leader chạy mỗi 30'; mục tiêu: không ticket nào thiếu owner quá 1 giờ); **Comment `[SLA 70%]`** (bản ghi một dòng của alert trên ticket: thời gian còn, status, hành động, lần kiểm kế).

## Nội dung
### 1. Capstone chạy thế nào
120 phút của một ca mô phỏng. Facilitator nạp queue ticket luyện tập SCOE cho role của bạn (VD Merch: queue VN SCOE-7 TRN-001, SCOE-13 TRN-007, SCOE-28 TRN-022, SCOE-42 TRN-036; Tech: SCOE-43 TRN-037 và SCOE-47 TRN-041) và một handoff note ngắn từ "ca trước". Trong ca facilitator chèn sự kiện: subsidiary trả lời, ticket chạm 70%, request sát go-live.
| Thời gian | Bạn làm gì | Observer nhìn gì |
|---|---|---|
| 0–15' | Đọc handoff note, nhận Assignee, mini stand-up với observer | Mọi ticket được giao có bạn là assignee và next action |
| 15–90' | Intake, làm, kiểm, escalate, trả lời sự kiện chèn | Đổi status, comment, tuân thủ rule |
| 90–110' | Exit criteria, handoff note | Mọi ticket mở có owner và next action có tên |
| 110–120' | Debrief và ký | Checklist đủ, không critical error |
Luật staging của lab: chỉ làm trên đối tượng ticket giao; ghi before values trước; đặt tên đối tượng mới `TRAINING_<NAME>_<TICKET>_…`; không sync Online, chạy cronjob hay submit Knox trừ khi trainer cho phép; rollback cuối buổi. Staging el3-s2 dùng chung với BVT.
Live có giám sát trong Academy theo cùng kỷ luật: 100% output được kiểm, mọi tin gửi subsidiary hay RHQ được Shift Leader/buddy duyệt trong 15' trước khi gửi, và học viên theo mọi shift rule (stand-up, handoff note, SLA alert).

### 2. Đầu ca: handoff và stand-up
Đọc handoff note trước giờ ca, rồi comment cuối từng ticket nhận, rồi nhận Assignee trên Jira. Stand-up ≤15' ra shift plan, không giải ticket: phút 0–2 điểm danh theo roster (headcount thật); 2–5 ticket High, incident, giờ update RHQ kế (mỗi High có owner và giờ update); 5–8 ticket >50% và >70%, ON HOLD COE chờ COEC, ON HOLD SUBS có Assignee CoE (next action, Doer, người chase Tech); 8–10 go-live, approval, urgent request, publish 23:59, BVT, freeze (mốc thời gian của ca); 10–13 người intake, overflow, người nói ngôn ngữ địa phương, nghỉ (shift plan); 13–15 known error mới, nhắc an ninh, người mới (cùng bức tranh).
**Ví dụ TRN-007 (SCOE-13):** handoff note liệt kê SAVINA VD (Low, R2) ở APPROVED-ES từ 10:30 ICT chưa ai nhận. Đó là việc đầu tiên: target initial response ticket Low là 78' nên phải sang STG SETUP trước 11:48 ICT. Viết internal check line, giao VN Market Owner, rồi mới đọc chi tiết (3 TV hide trên mọi site, 2 soundbar unblock, 1 TV unhide, `HW-S800B/XV` sang "Mua ở đâu" chỉ D2C).

### 3. Trong ca: intake, SLA và nhịp mỗi giờ
- **Initial response là đổi status:** Merch APPROVED-ES → STG SETUP; Tech NEW → ASSIGNED. P0 và High 15', P1 30', còn lại 78' (nội bộ; RFP 2 giờ). Comment không tính.
- **Request ngoài Jira** vào Jira trong 5'.
- **R3 (giá, discount, promotion, coupon):** internal check line trên ticket trước khi build, rồi price sanity rule.
- **Hỏi một lần:** chỉ khi brief thiếu hoặc mâu thuẫn; một comment gộp, ON HOLD SUBS, Assignee = subsidiary.
- **Cần Tech:** COEC mới, issue link, ticket Merch sang ON HOLD COE; clock Merch vẫn chạy; bạn chase Tech.
| Tần suất | Việc |
|---|---|
| Liên tục | Dashboard APPROVED-ES (Merch); COEC NEW (Tech) |
| Mỗi 15' | SLA còn lại mọi ticket mở; hành động theo cảnh báo |
| Mỗi 30' | Filter absent-assignee; dashboard ON HOLD SUBS với Assignee CoE |
| Sau mỗi task, tối thiểu mỗi giờ | Queue riêng theo SLA deadline; comment mới trên ticket ON HOLD SUBS; chase COEC |
| Lúc go-live | Go-live check; second checker R3 trong 30' |
**Alert:** 50% nhắc Assignee và ghi next action; 70% Shift Leader (Merch) hoặc Sub-Lead (Tech) hành động trong 15'; 85% Lead quyết trong 30'; 95% COE Lead báo RHQ trước breach. Ghi dạng `[SLA 70%] Remaining … Status … Action … Next check …`.
**Ví dụ TRN-022 (SCOE-28):** ticket FOC ghi "You can skip the QA step". Nó đến CoE sáng D0 cho go-live D+1 00:00 nên không phải last-minute theo ngưỡng nội bộ 17:00: giữ QA, giải thích lịch sự, gửi QA REVIEW trước 17:00.

### 4. Escalation và incident trong ca
Báo Shift Leader (trong capstone: observer đóng Shift Leader) khi ticket gần 50% mà không có đường đi, khi nhận request gấp, hay thấy dấu hiệu High hoặc incident. Dấu hiệu incident báo ngay; không bao giờ sửa lặng lẽ. Merch High là ảnh hưởng an ninh dữ liệu hoặc mất doanh thu >10,000 USD; chưa biết thiệt hại trên SKU traffic cao thì coi là High tới khi ước tính cho thấy khác. Ngoài khung Tech, COEC NEW được layer 1 Tech on-call quét mỗi 5'; Merch Shift Leader gọi Tech on-call khi thấy P0/P1, không chuyển hay sửa ticket COEC.

### 5. Cuối ca: exit criteria, handoff note, daily report
30' cuối kiểm exit criteria. Mọi ca Merch: dashboard APPROVED-ES trống hoặc mọi ticket nhận đúng hạn; dashboard ON HOLD SUBS với Assignee CoE trống; ticket ON HOLD COE có người chase Tech ở ca sau; urgent request đã comment và gắn `LastMinRequest`.
Rồi viết handoff note. Note Merch 13 mục, không mục nào để trống: ca và người; High và incident; ticket >70%; ON HOLD COE chờ COEC; Samsung L2/L3 và PC ticket; go-live check và publish 23:59; chờ duyệt (gồm Knox: giờ gửi, đường duyệt); urgent request; ngoài khung Tech và BVT; ticket mở theo market; staffing; notes (lời hứa với subsidiary, known error mới); ký nhận của hai Shift Leader. Handoff note là một trang mỗi ca trên Samsung Confluence và là bản ghi viết của ca bạn. Giai đoạn chuyển giao, SDM còn gửi RHQ scoreboard hằng ngày lúc 08:00 (từ 03/11); urgent request của đêm được tính trong đó.
**Ví dụ TRN-036 (SCOE-42):** lúc bàn giao ticket merch text chờ subsidiary ở dòng 3, 4, 6 (vượt giới hạn 300 byte 315 byte; `text-align` không hỗ trợ trên EPP; `fpt` có trong cả excludedSites và includedSites). Dòng 1, 2, 5 xong. Dòng handoff: ticket, Low R1, đã xong gì, chờ gì, Assignee = subsidiary, follower có tên, giờ nhắc kế theo giờ địa phương và ICT.

### 6. Quan sát và ký xác nhận
Observer dùng checklist dựng từ tiêu chí tuần giám sát T6 và checklist vai trò CM-04. Observer chỉ can thiệp để ngăn critical error; can thiệp được ghi lại và có nghĩa mục đó trượt.
| # | Mục | Evidence |
|---|---|---|
| 1 | Đọc handoff; mọi ticket nhận có next action | Assignee Jira, comment nhận |
| 2 | Initial response bằng đổi status trong 15, 30 hoặc 78' | Jira history |
| 3 | Priority và risk level đúng; internal check trước mọi build R3 | Comment ticket |
| 4 | Hỏi một lần, ON HOLD SUBS với Assignee = subsidiary; trả lời thì chuyển về STG SETUP | Ticket history |
| 5 | SLA warning được ghi và báo đúng người đúng giờ | Comment `[SLA nn%]` |
| 6 | Doer, Checker, Approver khác nhau; không tự duyệt | Ticket history |
| 7 | Giữ luật staging: ghi before values, chỉ đổi đối tượng giao, đã rollback | Evidence before/after |
| 8 | Tin nhắn qua rubric T2 | Comment |
| 9 | Exit criteria đúng; handoff note đủ; mọi ticket có owner có tên | Handoff note |
| 10 | Không critical error | Ghi chú observer |
**Critical error (một là rớt; từ danh sách T4 CM-11):** sai giá hoặc giá trị promotion; sai market, site, store; sai time zone làm lệch thời điểm hiệu lực; bypass QA gate hoặc tự duyệt; build R3 mà ticket không có internal check; giá/promotion không Knox; hành động trên production; đưa dữ liệu ra ngoài hệ thống Samsung; ON HOLD SUBS chỉ để dừng clock; với Tech, change production không có PC ticket đã duyệt hoặc ImpEx/Groovy thiếu dòng header (`#NOTE ITGC_JIRA:PC-xxxxx (COEC-xxxxx)`, `//NOTE …` trong Groovy). Học viên Merch hay QA chạy query HAC cũng là lỗi: Merch và QA không có HAC. Cần query thì Tech chạy trên COEC liên kết.
> **Under review (D1, D2):** tới khi chốt, hai trường hợp không chấm critical: ticket giữ ở ON HOLD SUBS với Doer là Assignee khi Knox pending, như runbook sửa đổi dạy (D1); và rule chỉ-quà publish không Knox (D2). Dùng ON HOLD SUBS chỉ để dừng clock ở mọi trường hợp khác vẫn là critical.
> CM-11 không có form ký cho capstone L2. Checklist trên do tác giả khoá học lắp từ CM-11 §3.3, 3.5, 4.4 và checklist CM-04 ch.10. Process and Knowledge Lead phải xác nhận trước cohort đầu. Nếu observer phải can thiệp, học viên làm lại capstone; làm lại sớm bao lâu cũng chưa đặt (CM-11 dùng "một tuần giám sát nữa" cho T6).

## Quiz (đáp án)
1 Bắt đầu ca 08:00, handoff liệt kê SCOE-13 (Low) ở APPROVED-ES từ 07:20 chưa nhận → **B: chuyển STG SETUP ngay: target 78' hết lúc 08:38** (comment không tính). 2 10:15 ticket Medium bạn giữ chạm 70% → **C: ghi `[SLA 70%]` với thời gian còn, status, hành động, lần kiểm kế, và báo Shift Leader, người hành động trong 15'** (B là mức 85%; D là dùng ON HOLD SUBS sai). 3 Subsidiary đã trả lời bằng comment trên ticket ON HOLD SUBS nhưng để nguyên status, assigned cho bạn → **B: chuyển ngay về STG SETUP và làm tiếp**. 4 SCOE-28 (promotion FOC) đến buổi sáng cho go-live 00:00 ngày mai và ghi "skip the QA step" → **C: giữ QA: không phải last-minute; giải thích lịch sự và gửi QA REVIEW trước 17:00**. 5 Trong ca thấy promotion live trên storefront với discount lớn hơn nhiều so với brief → **B: báo Shift Leader ngay như incident khả dĩ; không sửa lặng lẽ**. 6 Cuối ca, điều kiện nào đúng với mọi ca Merch → **B: dashboard ON HOLD SUBS với Assignee CoE trống, và ticket ON HOLD COE có người chase Tech ở ca sau**. 7 Observer can thiệp khi bạn sắp build thay đổi giá mà ticket không có internal check → **B: mục trượt; build R3 không internal check là critical error nên capstone không được ký**.

## Practice
**PR-GP6.1-1. Ca có giám sát** (120'; queue SCOE + staging el3-s2; facilitator chuẩn bị handoff note và 4–6 ticket SCOE cho role bạn và chèn ít nhất ba sự kiện: subsidiary trả lời trên ticket ON HOLD SUBS, ticket chạm 70%, request sát go-live; Shift Leader hoặc Sub-Lead quan sát với checklist ký xác nhận ở mục 6). Tự chạy ca từ lúc đọc handoff note tới lúc viết handoff note của mình. Observer chỉ can thiệp để ngăn critical error. Rollback mọi thay đổi staging cuối buổi và ghi trên ticket. **Pass:** đủ 10 mục checklist và observer ký; mọi initial response trong 15, 30 hoặc 78' bằng đổi status; mọi sự kiện chèn được xử lý bằng comment ticket và status đúng (trả lời → STG SETUP; 70% → `[SLA 70%]` và báo Shift Leader trong 15'; sát go-live → áp đúng QA cut-off hoặc rule urgent request); handoff note đủ 13 mục và không ticket nào thiếu owner có tên; staging đã rollback có evidence before/after; không critical error và không can thiệp. Chưa có access: không làm được; lên lịch sau khi có access.
