# GP3.1 A shift from start to end

> Nguồn: page 2484240761 · 60 phút (Study 15' · Demo/thảo luận 10' · Quiz 5' · Practice 30') · Thực hành theo case trên practice ticket; facilitator: Shift Leader hoặc Sub-Lead · Capability C3 · Cần xong G2.4 (mã ca, giờ bàn giao, handoff note 13 mục) và G2.8 (filter COE-F, dashboard COE Watch); mang bảng SLA tier của G2.3 (phút tại 50/70/85/95% mỗi priority). Truy cập: Jira SCOE (queue luyện tập) + Confluence (đọc CM-04, CM-09). Không có access: facilitator đưa queue giấy, handoff note trước và mẫu handoff note trống.

## Mục tiêu
Đọc handoff note theo thứ tự rủi ro và trong 15' nói được mình sở hữu ticket nào, mỗi ticket cần gì tiếp; lập kế hoạch ca bằng cách sắp ticket theo due time và SLA tier, nêu ai hành động ở mỗi tier; chạy các filter bắt buộc đúng tần suất và xử lý đúng khi trúng COE-F02, COE-F03; viết handoff note để ca sau hành động được mà không phải hỏi (mỗi ticket có next action, owner, giờ); liệt kê các mục daily report mà trụ của mình đóng góp.

## Thuật ngữ
**Acknowledgement signature** (Shift Leader nhận ca ghi tên + giờ vào handoff note; trách nhiệm chỉ chuyển lúc này, VD "Acknowledged: Sub-Lead 2, 08:00"); **Risk order** (thứ tự đọc handoff note: High và incident trước, rồi ticket >70% và ON HOLD COE, rồi go-live, rồi approval, rồi Samsung L2/L3 và PC ticket, rồi staffing); **Shift plan** (kế hoạch ngắn viết trên Samsung Confluence sau stand-up: headcount, người trực intake, phân market, mốc thời gian, lịch nghỉ); **Shift clock** (bảng kiểm cố định của CM-04: priority filter mỗi 5', cả queue mỗi 15', không owner mỗi 30', cân tải mỗi giờ); **COE-F02** (ticket ở ON HOLD SUBS mà Assignee vẫn là người CoE: CoE quên giao subsidiary, hoặc subsidiary đã trả lời); **COE-F03A** ("owner off shift": Assignee là người CoE không trong ca này; Shift Leader cập nhật danh sách đầu mỗi ca); **Exit criteria** (điều kiện phải đúng trong 30' cuối ca); **Jira Issues macro** (macro Confluence hiện kết quả filter live (F01, F02, F04, F06, F10, F11, F12, F16) trong handoff note, không gõ/copy danh sách); **Daily SLA report** (trang hằng ngày do Shift Leader ca D và Tech Sub-Lead chuẩn bị: ticket theo alert tier, SLA breach và nguyên nhân, incident).

## Nội dung
### 1. Nhận ca: đọc theo thứ tự rủi ro rồi nhận quyền sở hữu
L1 học giờ bàn giao; L2 bạn tự chạy 15' đầu. Đến trước giờ ca, đăng nhập Jira, Confluence, Mattermost, Samsung email và mở dashboard role (COE Watch: Merchandising Shift, Tech, QA hoặc My work). Không đăng nhập được thì báo Shift Leader ngay; không bao giờ mượn account. Đọc handoff note trước theo thứ tự này; **không bắt đầu ticket mới trước khi đọc mục 2 đến 8**:
| Thứ tự | Mục note | Tìm gì |
|---|---|---|
| 1 | 1. High và incident đang mở | Ticket nào của tôi; giờ update RHQ kế |
| 2 | 1. >70% SLA; 4. ON HOLD COE chờ COEC | Thời gian còn, chờ ai, ai chase Tech |
| 3 | 1. Go-live check; 23:59 publishing | Giờ, market, ai kiểm |
| 4 | 1. Chờ duyệt; 8. Urgent request | Shift Leader/Lead duyệt, ticket chờ Knox từ khi nào |
| 5 | 1. Samsung L2/L3, PC ticket; 9. Ngoài khung giờ Tech, BVT | Hạn follow-up kế, PC chờ duyệt |
| 6 | 1. Staffing | Ai vắng, ai cover |
| 7 | 1. Notes | Known error mới, lời hứa với subsidiary |
Sau đó mở từng ticket được giao và đọc **comment cuối trên Jira**, không chỉ dòng tóm tắt. Hỏi người giao trong lúc overlap, rồi đổi Assignee trên Jira thành mình.
**Ví dụ (CM-04 §6.6, mô phỏng):** note N→D 23/11/2026 liệt kê DEMO-1201 (AU, High) ở ON HOLD SUBS còn 2h10, và DEMO-1207 (MY, Medium) ở ON HOLD COE còn 9h vẫn đang chạy. Market Owner AU nhận DEMO-1201 và chuyển ngay về STG SETUP khi subsidiary trả lời. Market Owner MY nhận việc chase COEC liên kết DEMO-5031 và hỏi Tech Level 1 trước 09:00.
> CM-04 §4.1 chưa chốt overlap 15' đặt trước (ca nhận đến sớm) hay sau giờ đổi ca (ca giao ở lại). Tạm thời ca nhận có mặt 15' trước giờ bắt đầu, trách nhiệm chuyển khi Shift Leader nhận ký. Workforce Lead quyết ở CO-02.

### 2. Stand-up và shift plan
Shift Leader (Merch) hoặc Sub-Lead (Tech, QA) chủ trì buổi đứng ≤15'. Đầu ra duy nhất là shift plan; không ai giải ticket trong stand-up.
| Phút | Nội dung | Kết quả |
|---|---|---|
| 0–2 | Điểm danh theo roster; vắng, thay thế, bench | Headcount thật |
| 2–5 | Ticket High, incident, giờ update RHQ kế | Mỗi High có owner và giờ update |
| 5–8 | Ticket >50% và >70%; ON HOLD COE chờ COEC; ON HOLD SUBS với Assignee CoE | Next action, Doer, người chase Tech |
| 8–10 | Go-live, approval, urgent request, publishing 23:59, BVT, freeze | Danh sách mốc thời gian |
| 10–13 | Người trực intake, overflow, người nói Thái/Bahasa, nghỉ so le | Shift plan |
| 13–15 | Known error mới, nhắc an ninh thông tin, người mới cần coach | Bức tranh chung |
Lập kế hoạch theo **due time**, không theo tuổi ticket. Dùng bảng tier: Medium (16h) chạm 70% ở phút 672 và 85% ở phút 816; High/P0 (4h) 70% là phút 168. Ticket sẽ chạm 70% trong ca đặt đầu plan và nêu tên Doer. Ca khác nhau: ca đêm N chỉ 2 người nên stand-up 5–10' và không nghỉ trùng; Tech T4 04:00 đọc on-call log trước và chuyển COEC NEW qua đêm sang ASSIGNED. Shift Leader viết shift plan trên Samsung Confluence; không ghi dữ liệu Samsung ngoài hệ thống Samsung.

### 3. Quét queue: filter và shift clock
Ba dashboard RHQ yêu cầu phải có trước ticket thật đầu tiên: APPROVED-ES chờ nhận, ON HOLD SUBS với Assignee CoE, COEC NEW. CoE thêm ON HOLD COE chờ Tech, PC ticket pending, last-minute request trong tuần.
| Tần suất | Filter/kiểm | Ai |
|---|---|---|
| Mỗi 5' | F01 chờ ghi nhận; F04 High đang mở; SLA 85% và 95% | Shift Leader, người trực intake |
| Mỗi 15' | Cả queue theo SLA còn lại; F14 QA queue; F15 chờ duyệt | Shift Leader |
| Mỗi 30' | F03 không owner, F03A owner off shift, F02 ON HOLD SUBS với Assignee CoE | Shift Leader |
| Mỗi giờ | F16 go-live trong 8 giờ tới; cân tải | Shift Leader, Market Owner |
| Mỗi 2 giờ | F09 chờ subsidiary; F10 Merch chờ Tech; F12 PC ticket pending | Market Owner, người tạo COEC, Tech Lead |
| Sau mỗi task, ít nhất mỗi giờ | Queue của riêng mình theo SLA deadline | Mọi owner |
**Hành động khi trúng.** F02 có hai trường hợp: CoE quên giao subsidiary → kiểm câu hỏi đã nằm trong comment và đặt Assignee = requester; subsidiary đã comment trả lời mà không đổi status → clock đang dừng sai: chuyển ngay về STG SETUP (COEC: IN PROGRESS). F03: giao lại ngay và comment "Reassigned to [name] because [reason]. Next update by [time SGT]." Ticket đã quá 70% thì xử lý thêm như SLA alert.
F05–F08 là filter thay thế: tính từ APPROVED-ES (hoặc tạo COEC) và gồm cả thời gian dừng nên báo sớm; khi trúng thì mở ticket kiểm thời gian đã dùng thật trước khi hành động.
> Tên filter và JQL trong CM-09 là mẫu; Atlassian Platform Engineer chốt trên Samsung Jira và RHQ tạo CoE user group vì CoE không có quyền admin Jira. Trên project SCOE facilitator đưa filter tương đương.
Hai kiểm tra hằng ngày khác: Merchandising đọc báo cáo inactive promotion hằng ngày — rule đã publish có thể inactive mà không bị đổi; cách xử lý là republish, submit Knox lại và nhờ QA kiểm lại live (MER-INC-01, KE-MER-INC-01-13). Tech chạy vòng order monitoring 05:15, 13:30, 18:15 giờ VN, không có ticket (TEC-MON-01).

### 4. Hành động trong ca: alert và điều phối lại
| Mức | Ai | Làm gì | Hạn |
|---|---|---|---|
| 50% | Owner; Shift Leader | Nhắc owner; ghi next action | Trong vòng quét 15' |
| 70% | Shift Leader (Merch) hoặc Sub-Lead (Tech, QA) | Giao lại, thêm người; chase Tech với ON HOLD COE | 15' |
| 85% | Team Lead (on-call ngoài giờ) | Tiếp quản, workaround, escalate Samsung L2/L3, update requester | 30' |
| 95% | COE Lead; báo SDM | Báo RHQ trước breach kèm nguyên nhân và ETA | 1 giờ |
**Ví dụ (CM-04 §5.8):** 14:20 filter 15' cho thấy DEMO-2210 (SG, Medium, một promotion) ở 71%. Market Owner SG còn 6 ticket khác và setup xong 60%. Trong 15' Shift Leader giao lại cho Team Member rotating certified service, kèm comment bàn giao, và báo QA dispatcher có ticket R3 tới trước 15:30. QA REVIEW 15:25, QA PASS 15:50, Shift Leader duyệt và PRD SETUP 15:58. Thời gian ở QA REVIEW vẫn tính nên dispatcher đặt đầu queue.
Là owner, thấy ticket gần 50% mà chưa có plan thì báo Shift Leader ngay. Golden Rule 8: báo sớm.

### 5. Exit criteria và bàn giao
Ca kết thúc khi exit criteria đúng, hoặc mỗi ngoại lệ có trong handoff note với owner và next action. Shift Leader kiểm trong 30' cuối.
- **Mọi ca Merch:** dashboard APPROVED-ES trống hoặc mọi ticket nhận đúng hạn; dashboard ON HOLD SUBS với Assignee CoE trống; mọi ticket ON HOLD COE có người chase ở ca sau; urgent request đã comment và gắn `LastMinRequest`.
- **Ca D:** không ticket >50% mà thiếu next action; setup cần QA đã gửi QA REVIEW trước 17:00.
- **Ca E:** nội dung Thái/Bahasa có native speaker hoặc ghi chờ 08:00; promotion go-live ngày mai chưa có duyệt thì publish đúng giờ và comment trước 23:59.
- **Tech T11:** P0–P2 và PC ticket chờ duyệt giao layer 1 on-call lúc 19:00, cc Shift Leader.
Countdown cố định: −30' owner cập nhật next action mọi ticket và người tạo COEC giao việc chase; −20' Shift Leader chạy lại filter no-owner và SLA, điền note; −15' ca nhận đọc, hai Shift Leader walkthrough theo risk order, mỗi Team Member giao từng ticket cho người nhận có tên và đổi Assignee; lúc đổi ca Shift Leader nhận ký, chuyển COE hotline (một cuộc gọi thử). Ca giao chỉ rời khi filter no-owner trống và note đã ký.

### 6. Viết handoff note và mục daily report
Tạo trang từ template "Handoff note" ở nhánh Shift operations trên Samsung Confluence, tên theo ngày + ca, VD `HO-2026-11-03-E-MER`. Không gõ danh sách ticket: chèn Jira Issues macro với F01, F02, F04, F06, F10, F11, F12, F16. Chỉ viết tay cái filter không cho thấy: bước kế của ticket nóng, incident đang chạy, BVT notification chờ PIC, P0/P1 ngoài khung Tech nơi on-call được gọi, staffing, ghi chú đào tạo. Không bỏ trống mục: ghi "None". Phép thử: người nhận hành động được mà không hỏi. Mỗi dòng có **ticket, status, thời gian còn, next action, owner, giờ**.
| Yếu | Hành động được |
|---|---|
| "DEMO-1188 in progress" | "DEMO-1188 (SG, Medium): 3 h 10 min left, at QA REVIEW, result before 09:00; new owner SG Market Owner." |
| "Waiting for Tech" | "DEMO-1207 (MY, Medium) ON HOLD COE, linked COEC DEMO-5031 at ASSIGNED, 9 h left and running; MY Market Owner asks Tech Level 1 before 09:00." |
Note Tech và QA (11:00 và 19:00) có 8 mục: ca và người, P0–P2, monitoring và alert, queue, PC ticket chờ duyệt (giờ gửi, dự kiến duyệt; cộng ~3 giờ khi approver PC vắng), BVT, overnight, acknowledgement.
**Daily report:** Daily SLA report do Shift Leader ca D và Tech Sub-Lead chuẩn bị (QA Sub-Lead thêm OLA QA nội bộ): ticket theo alert tier, SLA breach và nguyên nhân, incident. Số liệu lấy từ Jira qua macro Jira Issues hoặc Jira Chart; không export sang spreadsheet ngoài hệ thống Samsung.
> CM-04 §6.1 dùng giờ bàn giao QA 04:00, 11:00–12:00, 19:00 của deck v08Oct. Nếu quyết định theo đề xuất v9.4 thì QA bàn giao lúc 08:00, 16:00, 24:00. Tới khi quyết, theo CM-04. **Under review (D11):** giờ ca QA chưa cố định.

## Quiz (đáp án)
1 Bắt đầu ca D 08:00, note có 1 High, 2 ticket >70%, 5 APPROVED-ES mới → **B: đọc mục 2–8 của note, rồi comment cuối trên Jira của từng ticket được giao, nhận Assignee** (A hấp dẫn vì initial response đang chạy nhưng người trực intake lo APPROVED-ES và luật đặt handoff note trước). 2 10:30 COE-F02 hiện DEMO-1192 (VN, Low) ở ON HOLD SUBS, Assignee là VN Market Owner, subsidiary đã đính banner trong comment 09:50 → **C: chuyển ngay về STG SETUP và làm tiếp** (B là cách sửa cho trường hợp CoE quên giao subsidiary). 3 Ticket Medium chạm 70% lúc 14:20 ca D → **B: Shift Leader, trước 14:35** (C là mức 85%). 4 15:30 F03A hiện hai ticket của Team Member về nhà ốm từ 13:00 → **B: giao lại ngay, comment "Reassigned to [name] because [reason]. Next update by [time SGT]."** (ON HOLD COE ở C là hold giả). 5 07:45 ca N, filter no-owner còn 1 ticket, Shift Leader nhận chưa ký → **B: ca đêm chỉ rời khi filter trống và note đã ký**. 6 Dòng note hành động được → **C: "DEMO-1207 (MY, Medium) ON HOLD COE, linked COEC DEMO-5031 at ASSIGNED, 9 h left and running; MY Market Owner asks Tech Level 1 before 09:00."** 7 Đưa danh sách ticket vào note → **C: chèn Jira Issues macro với filter chung, chỉ viết tay các bước kế** (export Excel bị cấm).

## Practice
**PR-GP3.1-1. Ca mô phỏng trên SCOE** (35'; queue SCOE do facilitator chuẩn bị kèm handoff note trước; vai Shift Leader ca D). Queue 6 ticket đủ trạng thái, dựng như ví dụ CM-04 §6.6: một High ở ON HOLD SUBS đã có trả lời trong comment; một Medium 71%; một ON HOLD COE có ticket Tech liên kết; một ticket có Assignee off shift; một go-live trong ca; một APPROVED-ES mới. Việc: nhận ca (đọc note theo risk order, nhận Assignee); viết shift plan 5 dòng sắp theo due time; chạy F01, F02, F03A và các filter SLA, hành động theo từng hit kèm Jira comment; ở −20' viết handoff note cho ca sau bằng template 13 mục. **Pass:** không ticket nào thiếu owner hay next action; High chuyển về STG SETUP (đã có trả lời); ticket 70% được giao lại hoặc tăng người trong 15' kèm comment; ticket ON HOLD COE có người chase Tech có tên và giờ; ticket off-shift giao lại với comment "Reassigned to … because … Next update by …"; APPROVED-ES chuyển STG SETUP trong target initial response; handoff note đủ 13 mục ("None" khi trống) và facilitator, đóng vai Shift Leader kế, ký mà không hỏi gì. Không có access: dùng queue giấy, viết Jira comment và handoff note trên giấy.
