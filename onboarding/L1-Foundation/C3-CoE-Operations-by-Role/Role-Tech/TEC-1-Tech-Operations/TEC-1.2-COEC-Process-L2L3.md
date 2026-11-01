# TEC-1.2 COEC process and working with Samsung L2/L3

> Nguồn: page 2483388417 · 90 phút (Study 35' · Demo 15' · Quiz 10' · Practice 30') · Lecture + demo Jira COEC + tính clock theo cặp; facilitator: Tech Sub-Lead · Tài liệu chính: TC-03. Cần xong TEC-1.1, G2.2 (13 status COEC), G2.3, G2.7.

## Mục tiêu
Làm 8 bước intake và trả lời 7 câu hỏi intake Tech cho COEC mới; chọn đúng status kế tiếp ở IN REVIEW cho 6 loại request; tính deadline "safe planning" cho ticket có hai khoảng chờ; chuẩn bị evidence pack 8 phần và mở Maintenance Request khi đủ 3 điều kiện; đóng ticket theo Definition of Done và giao LAUNCH VERIFICATION đúng người.

## Thuật ngữ
**Intake** (8 bước nhận COEC từ NEW tới khi bắt đầu làm); **Standing assignment table** (bảng cố định của Tech Lead: loại ticket nào giao ai để ticket không nằm ở ASSIGNED); **Safe planning** (CoE tự đặt deadline: đếm từ NEW, theo giờ lịch 24/7, chỉ trừ thời gian chờ tới khi phía kia trả lời); **Internal due date** (deadline nội bộ của linked COEC: sớm hơn giữa SLA COEC và ngày Merch ticket cần); **Definition of Done**; **Hand-back comment** (comment trả việc cho người tạo ticket, 4 phần: Status, Evidence, Next step, Next update).

## Nội dung
### 1. Ai giữ ticket ở mỗi status
Status nào đếm/dừng clock đã học ở G2.3. Điểm mới: **ở mọi status đang đếm, Assignee luôn là người CoE.** Assignee chỉ rời CoE ở hai nơi: ON HOLD SUBSIDIARY (assign requester) và LAUNCH VERIFICATION (assign creator).

### 2. Intake 8 bước (VD ticket "[SG] Cancel 2 orders")
1) Đọc hết ticket; mở attachment **trong Jira, không download**. 2) Kiểm đúng team; toàn bộ là việc Merch thì move ticket (G2.2). 3) Đối chiếu priority với bảng RFP; **không tự đổi** — đề xuất trong comment, Sub-Lead đổi trong 30'. 4) Tìm service code & runbook (`TEC-ORD-02`, `RB-TEC-ORD-02`); kiểm bạn có certification cho service đó. 5) Chọn Assignee từ standing assignment table. 6) Chuyển **ASSIGNED** — đây là mốc initial response; target nội bộ NEW → ASSIGNED: **P0 15', P1 30', P2–P4 78'** (CM-13 §4.1; RFP cho 2h mọi priority, 97%/tháng; 78' = 65% của 2h theo CM-03); ngoài giờ Tech do on-call layer 1 làm bước này. 7) Comment xác nhận: priority, team, owner, giờ update kế (SGT); thiếu thông tin hỏi một lần, gộp. 8) Chuyển IN REVIEW hoặc IN PROGRESS.
**7 câu hỏi intake Tech** (từ 7 quyết định intake CM-05 §3.1): service; priority P0–P4; market & team; incident hay request; có ticket liên quan không; có thay đổi production không (chỉ đọc thì ghi lý do; report cần PUMI); due date.

### 3. Standing assignment table
P0: Sub-Lead và Tech Lead (Tech Lead là Incident Manager). P1: Sub-Lead. Việc có runbook cho Level 1: người Level 1 đang trực. Việc ngoài runbook (sửa data order, bulk fix, ImpEx/Groovy, NERP, FI, base store): Team Member trong tuần Level 2 của cùng team. Câu hỏi tư vấn P4: Sub-Lead hoặc Tech Lead. Ticket 3PD: PIC 3PD.

### 4. Chọn đường ở IN REVIEW và luật chờ
- Có runbook và có thay đổi → IN PROGRESS, chuẩn bị PC. Chỉ đọc data → IN PROGRESS, không cần PC, ghi lý do. Report → có PUMI thì IN PROGRESS; chưa có thì ON HOLD SUBSIDIARY với template "PUMI needed". EPP site mới → có email RHQ thì ON HOLD HQ, không có thì ON HOLD SUBSIDIARY. Vấn đề code/deployment/hạ tầng/NERP → SYSTEM SUPPORT (chỉ Level 2 chuyển). Việc team Samsung khác → ON HOLD ES. Requester rút lại bằng văn bản → INVALID.
- Luật chờ của Tech (ngoài G2.2): chỉ vào status chờ khi *toàn bộ* việc còn lại ở ngoài CoE; mỗi lần vào ghi comment: chờ gì, chờ ai, khi nào check lại; hết chờ quay về status làm việc trước đó; **P0 và P1 không dùng ON HOLD SUBSIDIARY**; subsidiary im lặng không phải lý do INVALID.

### 5. Safe planning
Deadline = thời điểm tạo (NEW) + budget priority + tổng thời gian dừng; thời gian dừng chỉ tính tới khi phía kia trả lời, không phải tới khi CoE đổi status. VD P3 (40h) tạo 10:00 T2; ON HOLD SUBSIDIARY 11:00, subsidiary trả lời 14:00 (dừng 3h); ON HOLD HQ 15:30 T2 → 09:30 T3 (dừng 18h): 10:00 T2 + 40h = 02:00 T4; cộng 21h → **23:00 T4**.

### 6. Chuyển việc cho SDS India (Samsung L2/L3)
Phải đủ **3 điều kiện**: CoE đã dùng hết runbook & quyền; nguyên nhân ở phần CoE không được sửa (code, hạ tầng, phía NERP); Tech Team Level 2 đồng ý (Sub-Lead với P0–P2, Tech Lead cũng được báo với P0–P1). **Evidence pack 8 phần** (TC-03 §6.3): Summary; Context; Already checked; Impact; Steps/expected/actual; Evidence; Hypothesis; Request (kèm ngày cần + câu ownership, VD "BiPlus Ops CoE keeps ownership of COEC-xxxx and will verify on production after your fix."). Khi mở Maintenance Request dán nội dung vào CM-08 Template 7 (cùng dữ kiện, khác thứ tự). Mở Maintenance Request ở Jira project của market, priority khớp COEC, issue link; COEC sang SYSTEM SUPPORT, Assignee vẫn là người Level 2 của CoE.
SDS India hỏi → COEC về IN PROGRESS lúc chuẩn bị trả lời rồi về SYSTEM SUPPORT sau khi gửi; SDS India báo đã fix → về IN PROGRESS, tự kiểm trên production trước khi báo requester. Nhịp follow-up nội bộ chặt hơn RFP: P2 mỗi ngày làm việc, P3 mỗi 2 ngày, P4 hằng tuần.

### 7. Đóng ticket: Definition of Done và LAUNCH VERIFICATION
Done = đủ scope; có PC nếu có thay đổi; đã kiểm trên production; đính evidence; đã báo Merch ticket liên kết; đã post hand-back comment; Assignee là creator. LAUNCH VERIFICATION giao cho: người tạo (subsidiary → requester; Merch PIC → Merch PIC; QA → QA TM; HQ/RHQ → người ở field Reporter); ticket CoE tự mở (VD từ healthcheck) → Sub-Lead của team (người làm không tự xác nhận). **CoE không bao giờ tự chuyển CLOSED.**

### Điểm đáng nhớ từ KT
COEC dùng issue type "Maintenance Request" *trong project COEC* (filter vendor cũ lọc theo type này) — khác Maintenance Request Level 2 mở ở project market cho SDS India (CM-13 §2.2, §4.4); Tech Lead xác nhận issue type và filter. Component/sub-category bắt buộc nhưng subsidiary hay chọn sai → sửa ở intake, không move ticket chỉ vì sai component. Priority P0–P4 khác Shop Merch; người xử lý không đổi priority. Assignee tùy chọn, ticket về mailbox chung, Tech Lead (hoặc người được ủy quyền) chuyển ASSIGNED theo bảng. Subsidiary hay chỉ gửi screenshot → hỏi một lần gộp; ON HOLD SUBSIDIARY chỉ khi toàn bộ việc còn lại ở phía họ. Link ticket cũ cho lỗi lặp lại (intake câu 5).

## Quiz (đáp án)
1 Ticket có file Excel danh sách order → **mở trong Jira, không download**. 2 Subsidiary chọn P2 nhưng theo RFP là P1 → **đề xuất trong comment, Sub-Lead đổi**. 3 10:00 T3 cần Groovy sửa data, không runbook → **Team Member tuần Level 2**. 4 Subsidiary xin báo cáo bán hàng tháng chưa có PUMI → **ON HOLD SUBSIDIARY, comment "PUMI needed"**. 5 Không phải điều kiện mở Maintenance Request → **ticket đã dùng >50% SLA**. 6 P3 tạo 10:00 T2, ON HOLD SUBSIDIARY 11:00–14:00, ON HOLD HQ 15:30 T2 → 09:30 T3 → **23:00 T4**. 7 COEC ở SYSTEM SUPPORT, SDS India xin thêm log → **IN PROGRESS khi trả lời, rồi về SYSTEM SUPPORT**. 8 COEC CoE tự mở từ healthcheck đã xong → **LAUNCH VERIFICATION giao Sub-Lead team**. 9 P1 tạo 10:00 → **ASSIGNED muộn nhất 10:30**.

## Practice
- **PR-TEC-1.2-1** (giấy, cặp, 15'): DEMO-3201, MY, P2 (16h). T2: tạo 09:00; ASSIGNED 09:30; IN REVIEW 09:40; ON HOLD SUBSIDIARY 10:30; subsidiary trả lời 13:00 nhưng Tech chỉ về IN PROGRESS lúc 13:45; QA REVIEW 15:00; ON HOLD HQ 15:30; Oliver duyệt và về IN PROGRESS 18:30; LAUNCH VERIFICATION 19:10. Tính: (a) initial response **30'**; (b) safe planning deadline **06:30 T3** (09:00 + 16h + 2h30 + 3h); (c) SLA đã dùng lúc 19:10 theo safe planning **4h40' (~29%)**, theo Jira (từ ASSIGNED, dừng theo status) **3h25' (~21%)**; (d) nếu sau 18:30 chưa xong, chạm 70% lúc **01:42 T3**. Giải thích được hai nguồn chênh lệch: NEW 09:00–09:30 và 45' CoE trễ đổi status.
- **PR-TEC-1.2-2** (15'): order MY DEMO-ORD-5501 kẹt ORDER_SPLIT từ 08:10, NERP báo thiếu sold-to mapping, CoE đã kiểm ERP Config & ERP FI Config không thấy lỗi, Sub-Lead đồng ý chuyển. Viết evidence pack 8 phần tiếng Anh, comment chuyển COEC sang SYSTEM SUPPORT và comment update cho requester. Pass: đủ 8 phần, câu ownership, nêu rõ đủ 3 điều kiện, không PII, có giờ ICT & SGT và "Next update by".
