# TEC-P4.1 Level 1 shift and healthcheck

> Nguồn: page 2484240821 · 75' (Study 20' · Demo 10' · Quiz 10' · Practice 35') · Facilitator: Shift Leader/Sub-Lead · Capability C3 · Cần xong TEC-1.3 (ca sáng/chiều, dashboard COE Watch: Tech, mục đích healthcheck). Mang attachment TRN-039 (`healthcheck-queries.sql`, `healthcheck-log-template.csv`, `known-stuck-register.csv`, `coec-handoff-draft.md`) và template TC-02 A1, A4, D. Access: staging Backoffice + HAC el3-s2, Jira SCOE-45; vòng kiểm là read-only: không chạy cronjob, không restart process, không sửa order, không export dữ liệu khách. **Kibana (từ session này):** tài khoản cá nhân cho URL STG/production ở trang Kibana Monitoring; SAP ID Service + 2FA; tenant Global, Discover, index `logs-json-*`; VDI/LAN văn phòng có thể treo → Proxy Request với SSL Bypass; test login STG trước; log giữ ~3 tuần, cũ hơn cần ticket L2 label `COEC_logs_extract`. Không access: làm giấy với kết quả query in sẵn ngày 24/10/2026.

## Mục tiêu
Chạy vòng healthcheck sáng cho một market với query version cố định, đổi tuổi sang giờ market và lọc noise; quyết định cho từng kết quả: nil, comment trên ticket đã biết, một COEC mới mỗi market và loại lỗi, hay spike; tiếp nhận một ticket COEC qua 8 bước từ đọc tới comment đầu trong target nội bộ; viết hand-off đầy đủ cho TEC-MON-02 và part D cho ca sau, không tự sửa gì.

## Thuật ngữ
**Round (R1, R2, R3)** (một lượt healthcheck theo lịch: sáng đầy đủ 05:15-06:00, trưa nhanh 13:30-14:00, tối nhanh 18:15-18:40, giờ VN); **HC-01 đến HC-08** (danh sách healthcheck đề xuất; VD HC-01 order chưa gửi NERP sau >2h, HC-05 cronjob tích hợp lỗi); **Intermediate status** (status order giữa tạo và bàn giao NERP, VD CREATED, ORDER_SPLIT; ngưỡng 2h, WAITING_FOR_SEND_FINANCIAL 4h (đề xuất)); **Query version** (nhãn cố định của bộ query dùng trong vòng, VD `HC-VN-v0.1-lab`; chỉ Tech Lead đổi query/ngưỡng); **Known-stuck register** (danh sách order đã có ticket mở; chỉ comment "still stuck, day n", không ticket mới); **Noise** (kết quả không phải finding, VD process ERROR trên order COMPLETED do bước phụ như email, KE-TEC-MON-01-02); **Spike** (≥10 order một market, cùng dấu hiệu ở 2 market, ≥20 ở một status, hoặc không có SO 1 giờ khi vẫn có order được tạo); **Nil result** (dòng log "0 new stuck orders"; vòng không có finding vẫn ghi log, không bỏ); **Part B / Part D** (phần của trang bàn giao ca: part B cho Level 2 lúc 08:00, part D cho layer 1 on-call lúc 19:00).

## Nội dung
### 1. Healthcheck: kiểm gì và khi nào
Healthcheck là kiểm tra chủ động, read-only, theo lịch, tìm vấn đề trước khi subsidiary hay khách báo. Khác ticket: không ai yêu cầu, không đổi gì, không cần PC. Trong vòng kiểm **không được sửa gì**, "kể cả khi thấy cách sửa chỉ 5 giây". Mỗi finding thành một ticket COEC; danh sách order chỉ ở Jira.
| Mã | Kiểm gì | Ngưỡng đề xuất |
|---|---|---|
| HC-01 | Order chưa gửi NERP, export lỗi hoặc bị từ chối | Order đã thanh toán chưa gửi sau 2h; mọi lần bị từ chối |
| HC-02 | Order kẹt ở intermediate status | >2h cùng status |
| HC-03 | Lệch payment và order | Mọi trường hợp |
| HC-04 | Huỷ/return chưa gửi NERP | >24h |
| HC-05 | Cronjob tích hợp lỗi hay chạy lâu | Job export order: một lần là đủ; job khác: 2 lần lỗi liên tiếp |
| HC-06 | Smoke check storefront tới bước chọn payment | Bước nào lỗi với nhiều user: dấu hiệu P0 |
| HC-07 | Cảnh báo hệ thống từ Samsung | Cảnh báo có ảnh hưởng kinh doanh |
| HC-08 | Invoice chưa phát hành | >24h |
Giờ chạy (giờ VN): sáng đầy đủ 05:15-06:00 (HC-01 đến HC-08, NZ và AU trước); trưa 13:30-14:00 và tối 18:15-18:40 (HC-01, 02, 05, 06); ngày cao điểm mỗi 2 giờ. Team A phủ VN, TH, ID, NZ; Team B phủ SG, MY, PH, AU.
> Danh sách HC-01…08, ngưỡng, tên status/job và vị trí log là đề xuất; Tech Lead quyết sau KT. Level 1 chưa có quyền xem HAC trên production (hỏi RHQ ở KT): trên staging tập với HAC; trên production dùng Backoffice Orders và CronJobs trong quyền RHQ cấp.

### 2. Chạy vòng với TEC-MON-01
TEC-MON-01 là service Tech lớn nhất theo khối lượng, ~155 ticket/tháng. Doer: Tech Level 1. Checker: Tech Sub-Lead review log trước 10:00 VN, cộng engineer thứ hai chạy lại mù một market mỗi tuần. COEC không có QA Team.
| Bước | Doer | Checker |
|---|---|---|
| Mở log | Một dòng mỗi market và vòng; query version; giờ bắt đầu theo giờ market; ghi lệch đồng hồ HAC | Mỗi market và vòng có dòng; đúng query version |
| Query | Intermediate status quá ngưỡng; process ERROR chỉ trên intermediate status; kiểm sau SO | Ngưỡng áp đúng trên 3 dòng mẫu; ngày theo giờ market |
| Cronjob và log | Bốn job NERP Active, FINISHED, SUCCESS; Kibana cho action lỗi | Đã query, kiểm cronjob, xem log |
| De-duplicate và phân loại | Order đã biết: "still stuck, day n"; dòng mới có category (repush, financial, post-SO, SC+, 3PD, data, unknown) | Không order nào trên hai ticket mở; mọi dòng có category |
| Quyết định | Nil, COEC mỗi market và loại lỗi, hay spike | COEC NEW → ASSIGNED trong 30 phút; đã kiểm spike |
**TRN-039, vòng sáng VN.** Query version `HC-VN-v0.1-lab`, look-back 14 ngày. Ngày 24/10/2026 VN: ORDER_SPLIT 17, WAITING_FOR_SEND_FINANCIAL 10, CREATED 8; consignment WAITING_FOR_TRANSFER 20 không SO. Process ERROR trên order COMPLETED (10) và SHIPPING_REQUESTED (8) là noise: ghi "excluded, KE-02". Số SO nằm trên consignment (`gerpSalesOrderNr`), không phải order. Hai ORDER_SPLIT cũ nhất `VN261013-26729003` và `VN261016-26832002` có trong known-stuck register: chỉ comment. CronJobs: `vn-tokoTransferConsignmentToWarehouseJob`, `vn-tokoFinancialInitialUpdateJob`, `vn-bulkFetchConsignmentUpdateJob`, `vn-tokoFinancialCompletionJob` đều active, FINISHED/SUCCESS. Staging có Kibana riêng (URL STG, index `logs-json-*`): mở log view cho khung giờ của vòng; nếu login chưa sẵn, ghi "Kibana access pending", không đoán. Staging không có NERP thật nên ORDER_SPLIT luôn thiếu SO và số lớn hơn production: dùng số để tập, không rút kết luận vận hành.

### 3. Từ finding tới ticket, và khi nào là spike
- Không có dòng mới: log nil result bằng template A ("New stuck orders: 0. Known orders still open: [k], in [ticket]").
- Có dòng mới: một COEC mỗi market và mỗi loại lỗi, P2, label `COE_Order_Monitoring`, nhận NEW → ASSIGNED ngay. Summary như `[VN] [TEC-MON-02] ORDER_SPLIT without sales order > 2h (n orders)`. Description theo template B kèm bảng (store, order, created, status, tuổi theo giờ market, lỗi, category, known?). Link ticket subsidiary nếu có.
- Đủ tiêu chí spike: dừng hand-off từng order (re-push lúc outage có thể tạo SO trùng), gọi Sub-Lead, mở incident qua TEC-TSP-01 (COE-INC-01 nếu P0), đăng template C.
Ticket finding là P2: 16h, nội bộ 65% = 10h24. Comment đầu có 4 phần: Status, Evidence (kèm query version và giờ chạy), Next step (hand-off TEC-MON-02; mọi re-push hay restart cần PC duyệt), Next update.
**Spike trên staging.** HC-Q6 ngày 24/10: id 42, sg 46, nz 79, vn 40: đủ tiêu chí ở nhiều market. Nguyên nhân đã biết (staging không NERP, tải BVT), nên trong lab bạn viết template C để tập và không mở incident thật. Trên production cùng số này nghĩa là gọi Sub-Lead ngay.
| Dấu hiệu | Mức thường gặp | Hành động ngay |
|---|---|---|
| Checkout, payment hay login lỗi với đa số khách một market | Critical (P0) | Gọi Sub-Lead và Lead on-call layer 1; COEC P0 |
| Order không tới NERP hàng loạt; tiền bị trừ không có order | High (P1), Critical nếu rộng | Gọi Sub-Lead; mở incident |
| Cùng dấu hiệu ở ≥2 market | Theo impact | Gọi Sub-Lead và Tech Lead |
| Một job lỗi, ít order, có workaround | Medium (P2) | Ticket thường theo runbook |
> TC-02 §4.5 nói nhận finding ticket "ngay lập tức"; checklist Checker TEC-MON-01 chấp nhận NEW → ASSIGNED trong 30 phút. Nhận ngay; 30 phút là giới hạn ngoài. Finding ticket vào project COEC loại Maintenance Request (bộ lọc CoE chỉ nhặt loại này) với label `COE_Order_Monitoring`; tạo trong 30 phút từ lúc phát hiện (TEC-MON-01 sửa đổi 01/11). Tiêu chí spike và ngưỡng status là đề xuất RHQ chưa xác nhận.

### 4. Tiếp nhận COEC: 8 bước
Phản hồi đầu là chuyển NEW → ASSIGNED; comment "received" một mình không tính. Quét COEC NEW ít nhất mỗi 5 phút. Target nội bộ: P0 15 phút, P1 30 phút, còn lại 78 phút; hợp đồng: 2 giờ, 97% mỗi tháng.
1. **Đọc hết:** Summary, Description, Reporter, market, attachment (mở trong Jira, không tải), issue link, comment cuối.
2. **Đúng team?** Nếu toàn bộ là việc Merch, báo Sub-Lead chuyển chính ticket; không tạo ticket mới. Ticket từ Merch PIC phải có issue link tới ticket Shop Merch.
3. **Đọc priority** (RFP 3.3). Dấu hiệu P0: dừng, gọi Sub-Lead, theo CM-06. Priority có vẻ sai thì đề xuất trong comment; Sub-Lead đổi trong 30 phút.
4. **Tìm service và runbook**, kiểm certification của bạn.
5. **Chọn Assignee** (chính bạn cho runbook đã cert; Level 2 cho việc ngoài runbook 08:00-18:00; trước 08:00 hoặc sau 18:00 giữ và thu bằng chứng; nhận P0/P1 ngay).
6. **Chuyển NEW → ASSIGNED.**
7. **Comment** template A1: priority, team, owner, giờ update kế theo SGT; thiếu thông tin thì hỏi một lần, câu hỏi đánh số.
8. **Bắt đầu:** IN REVIEW rồi IN PROGRESS; chỉ subsidiary mở được thì ON HOLD SUBSIDIARY với requester là Assignee.
Lỗi thường gặp: comment không đổi status; ASSIGNED hàng loạt không đọc (P0 lẫn trong ticket thường); tự đổi priority; giao cho người chưa vào ca.

### 5. Bàn giao: sang TEC-MON-02, Level 2, ca sau
**Sang TEC-MON-02.** Sửa không phải việc của bạn trong vòng kiểm. Mọi re-push, restart process hay script chạy dưới TEC-MON-02 với PC duyệt; COEC sang ON HOLD HQ khi chờ (clock Tech dừng). Order đã có SO thì không bao giờ re-push. Tuổi: >2 ngày báo owner và Sub-Lead; >5 ngày báo Tech Lead; cùng nguyên nhân 3 lần/tháng mở COE-PRB-01.
**Sang Level 2 lúc 08:00.** 07:30 điền part B: P0-P2 và incident; ticket ngoài runbook; finding healthcheck; PC; ticket SYSTEM SUPPORT tới hạn follow-up (COE-F11); COEC chặn Merch; thông báo BVT qua đêm. Stand-up 08:00, tối đa 30 giây mỗi ticket, đổi Assignee sang người Level 2 Tech Lead chỉ định.
**Sang ca chiều, 11:00-12:00.** Duyệt ticket theo rủi ro: P0-P2; ticket ≥70%; PC; ticket Merch liên kết; ticket đang chờ có follow-up tới hạn; finding healthcheck; BVT; còn lại. Đổi Assignee; ca chiều ký part C trước 12:00.
**Sang layer 1 on-call lúc 19:00.** Part D (template D) xong trước 18:50: P0-P2 đang mở; vòng tối; ticket quá 50% có SLA chạy qua đêm và lúc đạt 85%; Assignee qua đêm; PC đang chờ và ai chạy; lời hứa với requester. Gọi on-call mỗi ngày, chuyển tiếp điện thoại trực bằng cuộc gọi thử, lấy "Received by" và "Seen by" của Shift Leader. Tự nhận mọi ticket NEW tạo trước 18:45.
Handover liên quan: Kibana Log (28/10: truy cập, proxy request, index `logs-json-*`; filter, trace threadId, tag NERP, retention ~3 tuần); Order Remediation (27/10: luồng status order/consignment bình thường; cronjob cập nhật status chỉ kiểm khi nhiều order kẹt); All SEAO Cronjob (30/10: đọc job trong Backoffice, không rerun khi chưa duyệt; job từ chối PayTo AU, KE-TEC-MON-01-10); Working Session P1 (23/10: loại issue COEC, label workflow, status SLA, dashboard Tech).

## Quiz (đáp án)
1 Vòng sáng VN, HC-Q2 cho process ERROR trên 10 order COMPLETED và 8 SHIPPING_REQUESTED → **B: noise từ bước phụ như email: ghi "excluded, KE-02", không phải finding**. 2 Hai order ORDER_SPLIT đã có trong known-stuck register với ticket mở → **B: thêm comment "still stuck, day n" vào ticket cũ**. 3 Vòng thấy 6 order VN ORDER_SPLIT không SO >2h và 3 order VN CREATED >2h → **C: hai ticket: mỗi market và loại lỗi một, P2, label `COE_Order_Monitoring`**. 4 Production: HC-01 thấy 23 order AU chưa gửi NERP, HC-05 thấy job export order AU lỗi từ 22:35 → **B: một nguyên nhân chung: một COEC P2, gọi Sub-Lead; job không thuộc runbook Level 1**. 5 Ticket COEC đến 06:40, P3, ngoài runbook, Level 2 bắt đầu 08:00 → **B: chuyển ASSIGNED, giữ, comment template A1, thu bằng chứng, đưa vào part B cho 08:00**. 6 Requester đặt P1 nhưng theo RFP 3.3 giống P3 → **C: đề xuất P3 trong comment kèm lý do và báo Sub-Lead, người quyết trong 30 phút**. 7 18:50 PC cho remediation P2 vẫn chờ duyệt, part D phải ghi → **B: số PC, ticket gốc và ai chạy nếu duyệt: Level 1 ca sớm từ 04:00** (P2-P4 ca sớm chạy; P0, P1 do on-call quyết). 8 Trong vòng thấy order kẹt có thể re-push một click → **B: ghi như finding; fix chạy dưới TEC-MON-02 với PC duyệt**.

## Practice
**PR-TEC-P4.1-1. Ca Level 1 (TRN-039)** (45'; staging el3-s2 read-only + SCOE-45; facilitator chạy query trước và đặt 2 ticket COEC NEW mô phỏng trong queue). Làm: (1) chạy vòng sáng VN R1 với `HC-VN-v0.1-lab`, look-back 14 ngày: HC-Q1, Q2, Q3, Q5, bốn cronjob NERP và log view STG Kibana ("Kibana access pending" nếu login chưa sẵn); (2) điền dòng log chỉ có số lượng; (3) de-duplicate với `known-stuck-register.csv`; (4) đánh giá tiêu chí spike bằng số; (5) soạn một hand-off COEC (template B) cho TEC-MON-02; (6) tiếp nhận 2 ticket NEW bằng 8 bước; (7) viết part D cho bàn giao 19:00. **Pass:** kiểm tra xong: dòng log có query version, giờ ICT, số lượng, không mã order; ERROR trên COMPLETED và SHIPPING_REQUESTED loại như KE-02; `VN261013-26729003` và `VN261016-26832002` chỉ comment; kiểm 4 cronjob; spike đánh giá bằng số và nêu nguyên nhân staging (không incident thật). COEC đúng: summary `[VN] [TEC-MON-02] …`, P2, label `COE_Order_Monitoring`, comment 4 phần, không fix. Hai ticket NEW chuyển ASSIGNED với template A1 và đúng Assignee. Bàn giao đủ: part D điền D1–D8. Facilitator chấm theo lưới TRN-039 (triage 3, round 4, checker 2, evidence 1). Không access: làm giấy với kết quả in sẵn 24/10/2026, cùng tiêu chí pass.
