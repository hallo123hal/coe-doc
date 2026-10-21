# CM-03 SLA handbook: hiểu và giữ SLA

> Tóm tắt trang Confluence CM-03 (v0.2, bản nháp 21/10/2026). Đây là **nguồn duy nhất về SLA** của cả bộ tài liệu Ops CoE; khi mâu thuẫn số liệu SLA, số trong CM-03 là số đúng. Người đọc: toàn đội Ops CoE (Merchandising, Tech, QA).

## 1. SLA hợp đồng theo RFP 3.3
**Vì sao quan trọng**: (1) tiền – Composite quý < 97% bị trừ 1–5% giá trị hợp đồng quý; (2) niềm tin – RFP Key Challenge 3 "SLA targets have not been met consistently"; (3) quyền ở lại – proposal v9.4 cho RHQ quyền chấm dứt hợp đồng không phạt nếu Composite **tháng 12/2026 < 92%** hoặc **quý 1/2027 < 95%**. Takeover 30/11/2026; tháng 12 đo & báo cáo đầy đủ (mục tiêu ≥ 97%) nhưng **khấu trừ chỉ áp dụng từ 1/2027** (quý đầu: T1–T3/2027).

**Hai thời hạn mỗi ticket**: Initial Response (2h mọi priority) và Resolution (theo priority). Cả hai chỉ đếm khi ticket ở trạng thái thuộc CoE.

| Tech (COEC) | Resolution | | Merchandising/QA | Resolution |
|---|---|---|---|---|
| P0 Major Incident (bảo mật dữ liệu, không truy cập được; mất > 500 USD) | 4h kể cả ngoài giờ | | High (bảo mật dữ liệu; mất > 10.000 USD) | 4h kể cả ngoài giờ |
| P1 Urgent (100–500 USD) | 8h | | Medium (1 promotion; multistore EPP/SMB/O2O/3PD, access code, GNB AEM, referral, các loại discount, BOGO, cross-sell, SC+, eVoucher…) | 16h |
| P2 High (khẩn; lỗi đơn do cấu hình; báo cáo quản trị gấp) | 16h | | Low (> 2 promotion, product setup, buying page, special price, discount row, text/flag, delivery mode, stock, voucher, banner/CMS…) | 24h |
| P3 Medium (vận hành hằng ngày, báo cáo, sửa dữ liệu hàng loạt) | 40h | | | |
| P4 Low (câu hỏi, nghiên cứu) | 120h | | | |

- Bảng "Merchandising, QA" = SLA **ticket Merchandising gồm cả bước QA**; RHQ không đo SLA riêng cho QA; QA Team chỉ QA việc Merch hằng ngày, không BVT, không QA Tech.
- Đếm số promotion khi tiếp nhận (1 = Medium, > 2 = Low). Đúng 2 promotion: RFP không nói → tạm Medium (chặt hơn), ghi lý do. Priority sai: Shift Leader/Sub-Lead sửa trong 30 phút.
- **Ngưỡng tháng**: Resolution ≥ 97% và Initial Response ≥ 97%, tính chung 8 thị trường.
- **3 chỉ số BVT** (tổng 10% Composite): Test Case Pass Rate 6% (100% test case đã chạy phải đạt), Test Report Completion 3% (báo cáo đúng hạn sau khi BVT đạt 100%), User Acceptance 1%. RHQ báo cửa sổ BVT (BVT notification) trước tối đa 1 tuần, ngày không thương lượng; **100% pass mới go-live (99% là không)**; lỗi → bug ticket cho đội phát triển (sửa 2–3 ngày) rồi retest; PIC BVT = Merch hoặc Tech (không QA Team); RHQ kiểm bằng chứng trên Confluence. Chi tiết: CM-12.
- **Composite tháng = Resolution×75% + Response×15% + Pass Rate×6% + Report Completion×3% + User Acceptance×1%** (làm tròn 1 số lẻ); **Composite quý = trung bình 3 tháng**; một điểm chung cho 3 trụ & 8 thị trường (cách hiểu của BiPlus, chờ RHQ). Resolution giảm 1 điểm → Composite giảm 0,75.
- **Khấu trừ** (trên Composite quý, vào giá trị hợp đồng quý, bằng credit note ở hóa đơn đầu quý sau): ≥ 97,0% không trừ; 95,0–96,9% trừ 1%; 94,0–94,9% 2%; 93,0–93,9% 3%; 92,0–92,9% 4%; < 92,0% 5%. Ví dụ 98,2/97,4/94,9 → 96,8% → trừ 1%.
- **Theo dõi ticket ở Samsung L2/L3** (Maintenance Request, ticket COEC sang SYSTEM SUPPORT): CoE vẫn giữ ownership; nhịp tối thiểu RFP (dù đồng hồ dừng): High (P0–P2, High) **2 ngày làm việc/lần**, Medium (P3, Medium) **4 ngày làm việc**, Low (P4, Low) **hằng tuần**; mỗi lần = 1 comment Jira + cập nhật requester.
- **Cam kết RFP vs mục tiêu nội bộ** (không được gọi mục tiêu nội bộ là "SLA" khi viết cho RHQ): phản hồi 2h vs 78' (P0/High 15', P1 30'); Resolution 97% vs xong trong **65% ngân sách**; Composite 97% vs **98,5%**; tháng < 97% → cam kết bổ sung gửi RHQ kế hoạch khắc phục trong 5 ngày làm việc + CEO dự họp tuần; < 98,5% → kế hoạch nội bộ 5 ngày; **100% ticket vỡ phải có ≥ 3 cảnh báo đã ghi trước đó**; Composite lũy kế quý công bố hằng tuần.

## 2. Đồng hồ SLA – chỉ chạy khi việc ở phía CoE
- Chuyển **trạng thái** mới ảnh hưởng đồng hồ; comment thì không. **SLA đã dùng = tổng thời gian ở trạng thái tính SLA. Hạn chót = giờ bắt đầu + ngân sách + tổng thời gian dừng.**
- Nhóm trạng thái: **Tính** (Merch: STG SETUP, QA REVIEW, PRD SETUP, ON HOLD COE; Tech: ASSIGNED, IN REVIEW, IN PROGRESS, QA REVIEW, WAITING QA); **Dừng** (Merch: ON HOLD SUBS, ON HOLD RHQ, REVIEW SETUP; Tech: ON HOLD SUBSIDIARY, SYSTEM SUPPORT, ON HOLD HQ, ON HOLD ES); **Chưa tính/không tính** (PLANNING, PLANNING REVIEW; PENDING LAUNCH, LAUNCH VERIFICATION, CLOSED, INVALID).
- Giờ lịch hay giờ làm việc cho priority ngoài P0/High: chưa rõ → **tạm tính giờ lịch 24/7**. Thời gian ở APPROVED-ES/NEW có cộng vào Resolution không: chờ RHQ; tài liệu tính từ APPROVED-ES/NEW (an toàn).
- Yêu cầu qua Mattermost/hotline: tạo ticket trong 5 phút, ghi "First contact: 14:05 ICT via Mattermost"; sự cố P0/High lập kế hoạch từ giờ liên hệ đầu.
- **Workflow Shop Merchandising** (chung 8 nước): PLANNING → PLANNING REVIEW → APPROVED-ES → STG SETUP → (QA REVIEW) → PRD SETUP → REVIEW SETUP → PENDING LAUNCH → LAUNCH VERIFICATION → CLOSED. NOT APPROVED không vào hàng đợi CoE. STG SETUP không phải môi trường staging. L.V. APPROVAL chưa được trình bày, không dạy như bước bắt buộc.
- **COEC**: NEW → ASSIGNED (Tech Lead) → IN REVIEW/IN PROGRESS → QA REVIEW/WAITING QA (tự QA staging) → LAUNCH VERIFICATION (giao người tạo). Chờ PC ticket: chuyển ON HOLD HQ + comment "PC ticket pending" (nếu không, đồng hồ vẫn chạy); Oliver duyệt xong chuyển ticket về IN PROGRESS, đồng hồ chạy lại ngay kể cả ngoài giờ Tech. SYSTEM SUPPORT dừng nhưng vẫn follow-up RFP.
- **Quy trình ON HOLD SUBS** (RACI: owner R, Shift Leader A, Market Owner C): liệt kê toàn bộ thông tin thiếu trong **một** comment đánh số → chuyển ON HOLD SUBS → đổi Assignee sang subsidiary (cả ba cùng lúc) → làm phần làm được → subsidiary trả lời (thường chỉ comment) → chuyển ngay về STG SETUP, giao lại người CoE → Shift Leader quét dashboard mỗi 30'. Hạn chót chỉ cộng thời gian dừng đến lúc subsidiary **trả lời**, không đến lúc chuyển lại.
- **ON HOLD COE + ticket liên kết** (vd 500.000 voucher cần ImpEx): tạo COEC mới + issue link; ticket Merch ở ON HOLD COE **vẫn chạy**; hai SLA song song; ví dụ: COEC chỉ dùng 12% ngân sách Tech nhưng ticket Merch đã dùng 54% → người tạo COEC phải đôn đốc Tech ngay từ đầu. Ticket nhầm team: *move* chính ticket (SLA theo team mới; chờ RHQ xác nhận).
- **Điểm dừng**: Initial Response dừng khi người CoE **chuyển trạng thái** (comment, email tự động, bot không tính); Resolution dừng khi **hand-back** (Merch: REVIEW SETUP kèm bằng chứng QA; Tech: LAUNCH VERIFICATION giao người tạo). Đang ở QA REVIEW / chờ Shift Leader / ON HOLD COE **không** phải điểm dừng.
- **Go-live tương lai**: setup + QA + duyệt xong thì chuyển ngay REVIEW SETUP; ngay cả nhiều đợt go-live → PENDING LAUNCH → QA lại production mỗi đợt → LAUNCH VERIFICATION. Go-live ngày mai mà 23:59 chưa duyệt → vẫn publish & comment "đã publish như đã thống nhất, chưa nhận phản hồi". **Due date = mốc sớm hơn giữa hạn SLA và (go-live − thời gian QA/kiểm)**; để ticket ở STG/PRD SETUP chờ go-live thì đồng hồ chạy và vỡ.
- **Reopen**: giữ priority, đồng hồ chạy tiếp ngân sách còn lại, **không reset**, không tạo ticket mới. **Hủy** = INVALID (đóng hẳn, ghi lý do; làm lại phải clone); ticket trùng: giữ ticket trước, link, INVALID ticket sau "Duplicate of …". Cấm INVALID để né SLA.
- **Tính hạn chót 6 bước**: priority → giờ bắt đầu (ICT) → cộng ngân sách theo giờ lịch → cộng thời gian dừng (ON HOLD COE, QA REVIEW không cộng) → đổi giờ địa phương → tính các mốc 65% và 50/70/85/95%. Tính lại mỗi khi ticket ra khỏi trạng thái dừng. SLA plug-in của Samsung chạy từ **1/12/2026**.
- **Múi giờ** (đến đầu 4/2027): VN/TH/ID UTC+7; SG/MY/PH UTC+8 (+1h); AU Sydney AEDT UTC+11 (+4h); NZ NZDT UTC+13 (+6h); từ đầu tháng 4/2027 AU/NZ về giờ chuẩn (+3h/+5h). RHQ dùng SGT. Đặt múi giờ Jira cá nhân là giờ VN; trả lời requester ghi cả hai giờ ("by 10:45 AEDT Wednesday (06:45 ICT)").
- 10 ví dụ tính hạn chót (Merch High/Medium/Low, Tech P0–P4 có dừng ở ON HOLD SUBS/HQ/SYSTEM SUPPORT/ES) trong tài liệu gốc – chủ yếu minh họa: Chủ nhật Tech chỉ on-call nên việc phải xong trước 19:00 thứ Bảy; ON HOLD COE chờ Tech ăn thẳng vào ngân sách Merch.

## 3. Phản hồi đầu tiên
- **Initial response = lần chuyển trạng thái đầu tiên bởi người CoE** (APPROVED-ES→STG SETUP; NEW→ASSIGNED), đặt Assignee là người thật. Chiếm 15% Composite. Mục tiêu nội bộ: 78' (= 65% của 2h, đệm 42'), P0/High 15', P1 30'.
- Thứ tự: đọc nhanh (đúng team? service, thị trường, priority, đủ thông tin?) → **chuyển trạng thái** → comment 5 phần (chào/ai; nhắc lại yêu cầu 1 câu; priority đã đọc; bước tiếp + giờ; thông tin thiếu hỏi một lần) → nếu thiếu thông tin: ON HOLD SUBS và giao subsidiary. Mẫu tiếng Anh: CM-08.
- Ai phản hồi: Merchandising – TM trực intake / Market Owner (24/7); Tech – Level 1 04:00–19:00 T2–T7, Tech Lead phân công; BVT notification – Merch/Tech Lead chỉ định PIC (ngoài giờ: handoff note + nhắn hai Lead). QA không có ticket riêng; BVT không phải ticket SLA của CoE.
- **COEC ở NEW ngoài giờ Tech** (19:00–04:00, CN, lễ): chưa rõ ai được chuyển ASSIGNED và cách đo. Quy trình tạm: Shift Leader xem dashboard NEW mỗi 5', filter Open High mỗi 15'; P0/P1 → **gọi Tech on-call lớp 1 ngay** (on-call chuyển ASSIGNED); P2–P4 → ghi handoff note cho Tech L1 04:00 + có thể comment "Tech acknowledgement"; 04:00 Tech L1 nhận NEW theo hạn sớm nhất; Shift Leader không xử lý ticket Tech.
- Lỗi hay gặp: comment nhưng quên chuyển trạng thái; xử lý trên Mattermost không ticket; comment "Noted/Checking"; ca bận dồn APPROVED-ES (phân 1 người intake, quét 5'); chuyển STG SETUP mà chưa đọc (nhận nhầm team); COEC NEW ngoài giờ không ai ghi.

## 4. Ngân sách thời gian & mốc nội bộ
- **% đã dùng = SLA đã dùng ÷ ngân sách**; **còn lại = ngân sách − đã dùng**. Mục tiêu nội bộ: **xong trong 65% ngân sách** (đến mốc 65% phần build phải xong, đang ở QA/duyệt).
- Mốc (ngân sách → 65% → dự phòng): 4h→2h36→1h24; 8h→5h12→2h48; 16h→10h24→5h36; 24h→15h36→8h24; 40h→26h→14h; 120h→78h→42h.
- **OLA nội bộ theo bước** (Merchandising có QA gate): nhận ticket ≤ 78' (High 15'); build xong trước 65% trừ thời gian QA+duyệt; QA High 30', loại khác 2h làm việc cho 1–2 mục (thiếu dữ liệu → trả ngay); Shift Leader duyệt High 15', khác 30'; **QA + duyệt tối đa 25% ngân sách còn lại** tại thời điểm chuyển QA; hand-back REVIEW SETUP ngay sau duyệt.
- **Due date**: người nhận điền khi chuyển STG SETUP/ASSIGNED; có go-live → mốc sớm hơn; tính lại sau khi ra khỏi dừng. Giúp Shift Leader sắp queue theo hạn thật.
- **Mốc nội bộ 98,5%/tháng** = vùng an toàn 1,5 điểm (peak Black Friday 27/11, 12.12, Tết, flagship có thể kéo 2–3 điểm; khấu trừ tính trên trung bình quý; số RHQ và CoE có thể lệch). **Error budget** (~2.200 ticket/tháng: Merch ~1.500, Tech ~700): mỗi ticket vỡ ≈ −0,045 Resolution, −0,034 Composite; Composite 98,5% (Response 99,5%, BVT 100%) cho phép ≤ ~41 ticket vỡ/tháng (~1,4/ngày); nếu Response chỉ 97% còn ~30 → phản hồi 78' là cách rẻ nhất bảo vệ Composite.
- Dưới 98,5%: SDM lập kế hoạch nội bộ trong 5 ngày làm việc; dưới 97%: COE Lead + CEO gửi RHQ kế hoạch (nguyên nhân, hành động, owner, ngày) trong 5 ngày làm việc, CEO dự họp tuần đến khi lên lại 97%; quý < 97% khấu trừ bằng credit note, QBR có CEO.

## 5. Bốn mức cảnh báo 50/70/85/95%
(Proposal gọi T1–T4; nội bộ gọi theo % để không nhầm với bài T1–T8 của Academy.) Nguyên tắc: báo sớm không bị phạt; **mỗi ticket vỡ phải có ≥ 3 cảnh báo đã ghi**, nếu không là lỗi quy trình.
| Mức | Ai | Làm gì | Thời gian |
|---|---|---|---|
| 50% | Assignee; Shift Leader | Nhắc; ghi next action (ai, đến mấy giờ) | trong vòng giám sát ca |
| 70% | Shift Leader (Merch, gồm QA REVIEW); Sub-Lead trực (Tech) | Rà soát: kéo về/giao lại/thêm người/huy động (bench, ca sau đến sớm, on-call); chờ Tech thì đôn đốc COEC; ở QA REVIEW thì báo dispatcher | 15 phút |
| 85% | Lead team (ngoài giờ on-call) | Workaround, leo thang L2/L3 kèm evidence pack, hoặc cập nhật requester | 30 phút |
| 95% | COE Lead (SDM thay đến khi bổ nhiệm); báo SDM | Báo RHQ **trước khi vỡ** kèm nguyên nhân + ETA | trong 1 giờ, luôn trước hạn |
| 100% | Lead | Ghi nguyên nhân (người/runbook/trạng thái sai/chờ Tech/bàn giao), rà tuần | 1 ngày làm việc |
- Giờ từng mức (giờ SLA đã dùng): 4h → 50%=2h, 70%=2h48, 85%=3h24, 95%=3h48 (còn 12'); 8h → 4h/5h36/6h48/7h36; 16h → 8h/11h12/13h36/15h12; 24h → 12h/16h48/20h24/22h48; 40h → 20h/28h/34h/38h; 120h → 60h/84h/102h/114h. P0/High: báo RHQ ngay khi chạm 95%, quy trình sự cố chạy song song.
- Cảnh báo tính trên thời gian SLA đã dùng: trạng thái dừng không lên mức mới; ON HOLD COE & QA REVIEW vẫn tăng. Ghi cảnh báo trên Jira theo mẫu `[SLA 70%] Remaining 4h48 (due 03:20 ICT). Status: …. Action: …. Next check: …. Owner/Shift Leader`. Viết trung tính, không đổ lỗi. Handoff note phải nêu các ticket đã > 70%.
- Ngoài giờ: 85% Merch → Merchandising Lead on-call (Deputy tuần 4); Tech → on-call lớp 1. On-call trả lời 15', có mặt trung tâm 60', không remote.

## 6. Filter & dashboard trên Jira Samsung
- Không dùng hệ thống BiPlus; chỉ filter, dashboard, subscription, automation trên Jira Samsung. JQL thật & tên chốt trong CM-09 (Atlassian Platform Engineer).
- **3 dashboard bắt buộc trước ticket thật đầu tiên**: (1) Merch ở APPROVED-ES (5' ca đông/15' khác); (2) ON HOLD SUBS có Assignee CoE (30', cùng lần lọc không owner); (3) COEC ở NEW (Tech L1 15'; Shift Leader 5'). Người dựng: Tech Lead + Atlassian Platform Engineer.
- **Bộ filter**: không owner (30'); Open High (5'; email 15' ngoài giờ); theo priority/hạn chót; cảnh báo 50/70/85/95; Merchandising chờ Tech; chờ subsidiary > 2h làm việc; PC ticket pending; theo dõi L2/L3 (follow-up cuối quá 2/4 ngày làm việc/1 tuần); go-live trong ca; yêu cầu gấp (label); vỡ SLA trong tháng. Filter cảnh báo phải dùng trường SLA plug-in (không dùng giờ tạo) vì đồng hồ dừng; trước plug-in dùng due date.
- **Lọc ticket không owner mỗi 30' mọi ca** (mục tiêu: không ticket nào không owner > 1h): xử lý ticket chưa assignee, assignee hết ca/nghỉ (comment "Reassigned from [name] (off shift) to [name]"), ON HOLD SUBS có Assignee CoE; báo người nhận thời gian còn lại; ghi nhật ký ca.
- **4 dashboard**: Shift Control, Team Lead, RHQ Service Overview, Escalations. RHQ xem cùng số liệu với CoE.
- Vòng giám sát Shift Leader: đầu ca đọc handoff; 5' APPROVED-ES/Open High; 15' toàn queue + 85%/95%; 30' không owner/ON HOLD SUBS/70%/COEC NEW ngoài giờ; đầu & giữa ca Merch chờ Tech; cuối ca handoff note.

## 7. Những việc làm vỡ SLA
- 3 lỗi trạng thái nguy hiểm nhất: quên chuyển APPROVED-ES→STG SETUP (NEW→ASSIGNED); để ticket ở ON HOLD SUBS sau khi subsidiary đã trả lời; hỏi subsidiary mà không giao ticket; ticket Merch ở ON HOLD COE chờ Tech mà không đôn đốc. Còn: chờ PC ticket mà không chuyển ON HOLD HQ, ticket không owner, việc ngoài Jira, sai priority, hỏi lắt nhắt, QA dồn cuối ca, duyệt chậm, bàn giao thiếu, ticket vắt cuối tuần/lễ, chuyển L2/L3 thiếu evidence pack, không follow-up SYSTEM SUPPORT, ticket giữ ở PRD SETUP chờ go-live, QA trả nhiều lần, ca thiếu người/peak.
- **Hỏi subsidiary đúng cách**: kiểm đủ thông tin ngay khi nhận; hỏi một lần đủ ý; ON HOLD SUBS + giao; làm phần làm được; nhắc qua comment Jira (tag requester) sau 2h làm việc của subsidiary hoặc sớm hơn nếu go-live gần; trả lời đến thì chuyển ngay; sau 3 ngày làm việc không phản hồi → COE Lead nêu với RHQ (Mattermost/họp tuần).
- **QA trong SLA Merch**: build xong & chuyển QA trước 65%; QA+duyệt ≤ 25% ngân sách còn lại; dispatch 15'; thiếu dữ liệu → trả & gặp trực tiếp; **cut-off nội bộ 17:00** cho go-live cùng tối. **Last-minute request**: promotion nên gửi trước 2–3 ngày làm việc (chờ RHQ); gửi sát giờ → nhận diện (sau 17:00 / muộn hơn hạn tối thiểu) → gắn label → comment đúng câu "Last minute request, please QA on your own when it goes live. If any issue, please contact us." → vẫn setup đúng runbook & chuyển trạng thái (vẫn chạy SLA) → đứng chờ hỗ trợ lúc go-live → đếm & báo họp tuần RHQ. CoE không phải hỗ trợ 24/7/365 cho mọi yêu cầu sát giờ nhưng phải giải trình nếu nút thắt phía CoE.
- **Tuyệt đối không**: chuyển ON HOLD (SUBS/RHQ/SUBSIDIARY/HQ/ES) chỉ để dừng đồng hồ; để ticket ở trạng thái chờ khi bên kia đã trả lời; dùng ON HOLD COE để "gửi" ticket; đổi priority để né SLA; INVALID/đóng/hand-back khi việc chưa xong; tạo ticket mới thay cho reopen hoặc move; comment rỗng; xử lý qua chat không ticket. Vi phạm xử lý theo CO-05 (RHQ đối chiếu lịch sử Jira).
- **Khi ticket đã vỡ**: không giấu, không sửa lịch sử; trong 1 ngày làm việc Lead ghi nguyên nhân (people, runbook, trạng thái sai, chờ Tech, bàn giao, khác); kiểm lịch sử ≥ 3 cảnh báo; nguyên nhân do người → mức L1 people-risk ladder (kèm cặp, giảm WIP nửa, chứng nhận lại 5 ngày làm việc; CO-05); hằng tuần phân tích → problem record (CM-07).

## 8. Báo cáo SLA
| Nhịp | Báo cáo | Nội dung chính |
|---|---|---|
| Mỗi ca | Handoff note (00/08/16 Merch; 11–12 Tech; 19:00 sang on-call) + stand-up 15' | High, >70%, chờ Tech, PC pending/SYSTEM SUPPORT, COEC NEW chờ 04:00, go-live ca sau, BVT notification |
| Ngày | SLA stand-up team; Leads sync 08:30 (SDM chủ trì); daily scoreboard gửi RHQ 08:00 (transition từ 3/11); báo cáo SLA ngày 2 tuần đầu hypercare | ticket vỡ, 85%/95%, rủi ro |
| Tuần | Weekly Service Review với RHQ (thứ Tư 10:00 SGT, pack gửi thứ Ba; COE Lead chủ trì); weekly status thứ Sáu 17:00 (transition) | SLA theo priority/thị trường, Composite QTD, leo thang, FPY/escaped defect/reopen, CSAT, BVT, last-minute request, nhân sự |
| Tháng | Monthly Service Review (báo cáo trước ngày làm việc thứ 5) | Composite vs 97%/98,5%, kế hoạch khắc phục, sự cố/RCA, capacity |
| Quý | QBR (COE Lead, CEO, CSM) | Composite quý tính khấu trừ, rà catalogue, skill matrix |
- **QTD**: tháng đã đóng dùng điểm đã chốt, tháng đang chạy dùng MTD; điểm tháng 3 cần đạt tối thiểu **= 3×97,0 − A − B** (vd T1 98,6 + T2 95,8 → T3 ≥ 96,6; đạt 98,5% quý cần 101,1 = không thể).
- **Nguồn chính thức**: SLA plug-in từ 1/12/2026; CoE không giữ bảng số riêng; đối chiếu đầu tháng, tranh chấp: SDM → COE Lead → CEO; thời gian dừng chỉ hợp lệ khi ticket thật sự chờ bên ngoài. Báo cáo nằm trên Confluence Samsung, không export. Lịch họp MT-01…MT-20: CO-07.

## 9. Ví dụ tính & bài tập (tóm tắt)
- Tháng tốt (T1/2027, 2.200 ticket): Resolution 98,82%, Response 99,50%, BVT 100% → Composite 99,0%. Tháng xấu (T2/2027: Resolution 94%, Response 96%, Pass 95%, Report 50%, UA 100%) → **93,1%**; một báo cáo BVT trễ mất 1,5 điểm ≈ 44 ticket vỡ. Quý 99,0/93,1/97,6 → **96,6% → trừ 1%**; để quý đạt 97% tháng 3 cần ≥ 98,9%.
- Đáp án mẫu: Composite với Resolution 97,5/Response 98 + BVT 100 = 97,8%; 97,2/96,4/97,1 → 96,9% (trừ 1%); 95,0/92,3/93,9 → 93,7% (trừ 3%); T1 96,0 & T2 97,5 → T3 ≥ 97,5%; Resolution tối thiểu để Composite 98,5% khi Response & BVT 100% = 98,0%; 2.000 ticket (50 vỡ, 30 trễ, BVT đạt) → 97,9%.
- Phụ lục A: 15 câu trắc nghiệm + 5 tình huống (P0 ngoài giờ → Shift Leader gọi on-call lớp 1, hạn 05:30, sửa khẩn vẫn cần PC ticket qua Oliver; không hạ priority để "có thêm giờ"; vỡ mà không có cảnh báo = lỗi quy trình; RFP 2h ≠ nội bộ 78'; 3 ticket ON HOLD SUBS có Assignee CoE → đọc comment cuối rồi chuyển về/giao đúng). Đáp án chính: P2=16h; 4 promotion=Low 24h; 96,9% quý→trừ 1%; 92,0% quý→trừ 4%; SYSTEM SUPPORT→đồng hồ dừng; ON HOLD COE→chạy; 95%→COE Lead báo RHQ; lọc không owner 30'; ticket Low đã dùng 18h bị trả lại→còn 6h; P3 ở SYSTEM SUPPORT→follow-up 4 ngày làm việc.

## Phụ lục C. Điểm chờ chốt (tổng hợp)
1. Giờ lịch vs giờ làm việc (priority ngoài P0/High) – tạm 24/7 (COE Lead, SDM với RHQ). 2. L.V. APPROVAL. 3. Ngoài giờ Tech: ai chuyển COEC NEW→ASSIGNED, cách đo (COE Lead với RHQ). 4. Giờ ca QA; người kiểm queue Tech/QA CN 09:00 & 17:00 (anh David). 5. Đúng 2 promotion: Medium hay Low. 6. Composite: tháng không có BVT, Pass Rate lần chạy cuối hay mọi lần, ticket vắt hai tháng, một điểm chung cho ba trụ. 7. Hạn gửi promotion (2 hay 3 ngày làm việc), mốc last-minute (tạm cut-off 17:00).
