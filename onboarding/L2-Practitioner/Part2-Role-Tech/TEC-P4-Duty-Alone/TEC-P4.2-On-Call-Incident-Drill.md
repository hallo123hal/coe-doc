# TEC-P4.2 On-call and incident drill

> Nguồn: page 2484044225 · 60' (Study 15' · Demo 10' · Quiz 5' · Practice 30') · Facilitator: Shift Leader/Sub-Lead · Capabilities C1, C3, C6 · Cần xong TEC-1.4 (Tech on-call: giờ và hai layer) và G2.5 (Incidents và on-call: severity matrix, bước I1–I9, Incident Manager). Mang đồng hồ/điện thoại cho observer, phiếu chấm drill CM-06 (§8.4) in sẵn, thẻ bỏ túi TC-04 (Phụ lục A). Không cần staging; drill chỉ dùng ticket mô phỏng `DEMO-xxxx`.

## Mục tiêu
Áp dụng call tree và ba mốc on-call cho P0 ban đêm, nói ai hành động ở từng phút; xử lý COEC ở NEW ngoài giờ: ai chuyển ASSIGNED, gì vào bàn giao 04:00; lên giờ thông báo RHQ cho Critical và High từ T0, biết nhịp không dừng; chạy emergency change ban đêm theo 10 bước (rollback viết trước, PC duyệt trước khi chạy gì); qua incident drill (scenario A hoặc B) theo phiếu chấm CM-06.

## Thuật ngữ
**T0** (lúc CoE phát hiện/được báo incident; mọi deadline tính từ đây, VD thông báo Critical trong 30 phút); **T-confirm** (lúc on-call xác nhận severity qua điện thoại; bridge đến hạn 15 phút, PIC 30 phút sau đó); **T-restore** (lúc RHQ xác nhận dịch vụ trở lại; deadline RCA 48h mục tiêu, 72h tối đa tính từ đây); **Ba mốc on-call** (trả lời trong 15 phút từ cuộc gọi đầu; xác nhận severity trong 30 phút từ T0; có mặt ở workstation trong 60 phút từ cuộc gọi đầu); **Call tree 0, 10, 15, 20** (layer 1; phút 10 layer 2; phút 15 Tech Lead (hoặc Sub-Lead A); phút 20 hotline SDM); **Acting Incident Manager** (Shift Leader giữ vai Incident Manager và PIC tới khi Tech on-call đến và nhận); **Night PC ticket** (PC khẩn cho P0/P1 ban đêm: staging, self-QA, second checker, ON HOLD HQ, nhắn Mattermost cho đầu mối duyệt chỉ định, không chạy gì trước duyệt); **Drill** (diễn tập scenario A hoặc B có observer, chấm trên phiếu CM-06; đạt khi 7 tiêu chí thời gian pass và tối đa 1 tiêu chí khác cần cải thiện).

## Nội dung
### 1. Thói quen on-call: giờ, layer, ba mốc
Tech ở trung tâm: Level 1 04:00-12:00 và 11:00-19:00, Thứ Hai-Thứ Bảy; Level 2 08:00-18:00. Ngoài các khung này Tech on-call: 19:00-04:00 ngày thường, và từ 19:00 Thứ Bảy tới 04:00 Thứ Hai (khối 33 giờ). Chủ nhật layer 1 vào trung tâm 09:00 và 17:00 kiểm queue. Layer 1 là một lead mỗi tuần; layer 2 là Team Member tuần Level 2 cùng team.
| Mốc | Chuẩn | Bằng chứng |
|---|---|---|
| Trả lời | 15 phút từ cuộc gọi đầu của Shift Leader | On-call log: giờ gọi và giờ trả lời |
| Xác nhận severity | 30 phút từ T0; thực tế trước phút 25 để thông báo kịp giờ | "Confirmed by Tech on-call by phone at …" |
| Có mặt ở workstation | 60 phút từ cuộc gọi đầu, gồm đi lại; chuyển COEC sang ASSIGNED | Giờ đến; lịch sử ticket |
Không làm việc từ xa: chỉ làm trên hệ thống Samsung tại workstation CoE. Rời nhà trong 10 phút sau cuộc gọi.
**Call tree.** Shift Leader gọi điện, không nhắn tin, nêu 4 ý: ticket, market, impact, cần gì. Layer 1 không trả lời thì gọi lại trong 10 phút; phút 10 gọi layer 2; phút 15 Tech Lead (hoặc Sub-Lead A nếu Tech Lead là layer 1); phút 20 hotline SDM. Layer 2 trả lời không kết thúc tree: Team Member không làm Incident Manager hay quyết emergency change. On-call không trả lời trong 15 phút là vi phạm quy trình.
> Thời gian trả lời on-call là 15 phút từ cuộc gọi đầu (TC-04 §3.1). Xác nhận severity 30 phút ngoài giờ làm việc và 15 phút trong giờ (CM-06 §8.4). Với P0 trong khung 04:00-08:00 và 18:00-19:00, TC-04 đề xuất Level 1 gọi cả Sub-Lead và lead layer 1; chờ Tech Lead quyết.

### 2. Làm việc ban đêm: COEC ở NEW, 60 phút đầu, bàn giao 04:00
Ngoài khung Tech, COEC ở NEW là việc của on-call, không phải Shift Leader. Phản hồi đầu vẫn là NEW → ASSIGNED và chỉ làm được tại workstation CoE.
| COEC ở NEW ngoài giờ | Điều xảy ra |
|---|---|
| P0, P1, hoặc đọc như incident | Shift Leader gọi layer 1 ngay; on-call đến trong 60 phút và chuyển ASSIGNED |
| P2-P4 | On-call chuyển ASSIGNED khi ở workstation và đăng comment "Tech acknowledgement"; không thì giữ NEW cho Level 1 lúc 04:00, hạn sớm nhất trước |
| Ghi P0/P1 nhưng thực tế thường | Shift Leader vẫn gọi; on-call đánh giá bằng giọng nói và quyết |
**60 phút đầu của P0** (phút từ T0): 0 Shift Leader ghi T0; 0-5 reproduce, kiểm market khác, tạo COEC `[INCIDENT]` P0 để ở NEW; 5 gọi layer 1; trước 25 on-call xác nhận P0 và duyệt nội dung thông báo; trước 30 Shift Leader gửi thông báo đầu; 15 phút sau T-confirm bridge được vào/mở và Shift Leader là PIC tạm; tới 65 on-call có mặt ở workstation, chuyển ticket ASSIGNED, IN PROGRESS và nhận vai Incident Manager và PIC. Khi ở workstation giữ nhịp 5 phút cho ticket NEW khác, hoặc nhờ layer 2.
04:00 on-call bàn giao cho Level 1 ca sớm: on-call log, ticket đã ASSIGNED hay còn NEW, PC duyệt qua đêm và ai chạy.
> TC-04 ghi điểm mở: với P0, phản hồi đầu thường 45-60 phút: trong 2 giờ RFP nhưng vượt target nội bộ 15 phút. Ticket P2-P4 tạo lúc 19:30 ngày thường có thể chờ tới 04:00 (8h30). Chưa có cách thống nhất bảo đảm 2 giờ cho các ticket này; ghi từng cái vào on-call log (giờ tạo, giờ ASSIGNED, on-call có ở trung tâm không). Người quyết: Tech Lead và COO.

### 3. Thông báo và nhịp
| Severity | Thông báo đầu | Update | Đóng |
|---|---|---|---|
| Critical (Tech P0) | 30 phút từ T0 (nội bộ; RFP 3.9 nói 2 giờ) | Mỗi 30 phút tới khi khôi phục | Khi gửi RCA (48h mục tiêu, 72h tối đa) |
| High (Tech P1) | 2 giờ từ T0 | Mỗi 2 giờ | Khi gửi RCA một trang (72h tối đa) |
Nhịp tính theo giờ lịch và **không dừng** khi COEC ở ON HOLD HQ hay SYSTEM SUPPORT. Gửi update kể cả không đổi: "No change since the last update." Comment giờ đã gửi lên ticket và đặt nhắc cho lần kế.
**Ví dụ (TC-04).** P0 có T0 22:50: thông báo đầu trước 23:20 ICT (00:20 SGT); update trước 23:50, 00:20, 00:50 và mỗi 30 phút tới khi khôi phục. High T0 20:30: thông báo đầu trước 22:30; update trước 00:30, 02:30…
SLA clock và impact khách là hai con số khác nhau. Ở scenario B SLA clock dùng 139 phút (2h19) vì dừng ở ON HOLD HQ và SYSTEM SUPPORT, trong khi khách VN không trả thẻ được từ 22:50 đến 02:45. Thông báo RHQ báo impact khách; báo cáo SLA dùng clock.

### 4. Night PC ticket: emergency change
Mọi thay đổi Tech trên production cần PC duyệt, ban đêm cũng vậy. Approver là RHQ PC approver (hiện Oliver Leung, cluster SEAO). P0/P1 gấp dùng đầu mối duyệt chỉ định trên on-call sheet của Tech Lead (A.II.2). COE Lead không duyệt PC thay được.
1. **Quyết** cách xử lý (rollback, workaround, fix); workaround đổi trải nghiệm khách thì xin RHQ đồng ý và ghi tên, giờ. 2. **Viết rollback trước** trên COEC. 3. **Staging**, ticket IN PROGRESS. 4. **Self-QA** ở QA REVIEW. 5. **Another set of eyes:** người thứ hai cert L2/L3 đúng service viết comment "Second check". 6. **Soạn PC:** thay đổi, lý do kèm link COEC và mức P, kết quả staging, rollback, người chạy và người check, giờ chạy; thêm bước re-enable nếu có thể theo sau. 7. **ON HOLD HQ** với "PC ticket pending: …". 8. **Nhắn đầu mối duyệt** trên Mattermost từ workstation (chỉ P0, P1). 9. **Báo** Incident Manager và bridge; update RHQ kế ghi "waiting for PC ticket approval". 10. **Sau duyệt**, về IN PROGRESS, chạy checklist, chạy, second checker verify, comment, update RHQ.
Approver vắng: dự kiến chờ ~3 giờ; theo TC-04 §6.4 từ phút 0, báo COE Lead, giữ nhịp RHQ, nói thẳng khách vẫn bị ảnh hưởng. Template T6 xin RHQ giúp liên hệ approver, không thay duyệt.
> Việc Oliver có duyệt bước re-enable/rollback cùng PC đầu tiên không còn chờ quyết định (TC-04 bước 6, CM-07). Ở scenario B CM-06, bước re-enable dùng PC thứ hai. Tới khi RHQ quyết, hỏi trong PC đầu và chuẩn bị PC thứ hai.

### 5. Drill: scenario A hoặc B
Drill dùng dữ liệu mô phỏng và ticket `DEMO-xxxx`. Không đổi production, không gửi RHQ thật, không tạo PC hay Maintenance Request thật, không nhắn Oliver thật. Observer đóng RHQ và Oliver; một người đóng SDS India. Observer ghi giờ thực của từng mốc và status ticket, chấm phiếu, và họp debrief 30 phút.
| Scenario | Tình huống | Đường chính |
|---|---|---|
| A | Chủ nhật 02:00, khách SG không đặt hàng được sau deployment nền tảng lúc 01:45 | Shift Leader là acting Incident Manager; thông báo 02:28; on-call đến 02:55; SDS India rollback qua Maintenance Request (SYSTEM SUPPORT); T-restore 04:30; không PC vì CoE không đổi gì |
| A2 | Layer 1 không trả lời | Call tree tới Tech Lead ở phút 15; thông báo vẫn trước 02:30 |
| B | Thứ Bảy 23:00, thanh toán thẻ VN lỗi (certificate gateway) | BiPlus mở bridge 23:30; ẩn payment mode thẻ dưới PC `DEMO-PC-01` (duyệt 01:05); re-enable dưới `DEMO-PC-02` (duyệt 02:30); T-restore 02:45 |
| B2, B3 | Incident Merch cần Tech; Oliver vắng | COEC liên kết và ON HOLD COE; PC chờ ~3 giờ |
**Chấm.** 7 tiêu chí thời gian: ticket trong 5 phút từ T0; xác nhận severity (30 phút ngoài giờ); on-call trả lời trong 15 phút với call tree đúng thứ tự; bridge trong 15 phút và PIC trong 30 phút từ T-confirm; thông báo Critical trong 30 phút từ T0 kèm giờ ICT và SGT; update đúng nhịp; on-call có mặt trong 60 phút. Tiêu chí còn lại: emergency change, status Jira, verify, hồ sơ và tiếng Anh.
Handover liên quan: Working Session P1 (23/10: workflow COEC, status tính/dừng SLA, đổi priority); Kibana Log (28/10: lấy log khi incident; giữ ~3 tuần); All SEAO Cronjob (30/10: không rerun cronjob ban đêm hay ban ngày khi chưa RHQ duyệt hoặc subsidiary yêu cầu).

## Quiz (đáp án)
1 Sub-Lead B giữ layer 1 tuần này; 01:30 Shift Leader gọi P0, 01:35 gọi lại không ai nghe; 01:40 và 01:45 → **B: 01:40 Team Member Team B tuần Level 2; 01:45 Tech Lead** (hotline SDM ở phút 20). 2 Ở câu 1 layer 2 trả lời lúc 01:41, Shift Leader dừng call tree được không → **B: Không: Team Member không làm Incident Manager hay quyết emergency change; Tech Lead vẫn được gọi ở phút 15**. 3 T0 22:50 cho Critical; thông báo đầu và hai update kế → **B: 23:20; rồi 23:50, 00:20** (C là nhịp High). 4 00:38 COEC sang ON HOLD HQ chờ PC; update 3 đến hạn 00:58 → **B: gửi: "waiting for PC ticket approval", và nói khách vẫn bị ảnh hưởng** (nhịp RHQ không dừng khi clock dừng). 5 00:30 workaround (ẩn payment mode thẻ VN) sẵn và đã test staging, Oliver chưa duyệt → **C: tạo PC, COEC sang ON HOLD HQ, nhắn đầu mối duyệt chỉ định; không chạy gì trước duyệt** (COE Lead không phải approver). 6 COEC P3 tạo 20:10 ngày thường, layer 1 ở nhà không việc khác → **C: giữ NEW; Level 1 04:00 chuyển ASSIGNED, hạn sớm nhất trước, on-call log ghi lại**. 7 Scenario A on-call chuyển `DEMO-1234` ASSIGNED 02:55, ticket tạo 02:05 → **A: 50 phút: trong 2 giờ RFP nhưng vượt target nội bộ P0 15 phút; ghi vào debrief**. 8 Drill pass cả 7 tiêu chí thời gian, nhưng emergency change và hồ sơ đều "cần cải thiện" → **B: Không: tối đa một tiêu chí còn lại được cần cải thiện**.

## Practice
**PR-TEC-P4.2-1. Incident drill** (40'; drill giấy; vai: Shift Leader, on-call layer 1, on-call layer 2 là học viên; facilitator là observer và đóng RHQ, Oliver; một người đóng SDS India; chỉ ticket `DEMO-xxxx`, không gửi người thật). Chạy scenario A (checkout SG sập, Chủ nhật 02:00) hoặc B (thẻ VN lỗi, Thứ Bảy 23:00). Facilitator chèn một biến thể: A2 (layer 1 không trả lời), B2 (incident Merch cần Tech) hoặc B3 (Oliver vắng). Học viên viết ticket, call log, thông báo đầu và update bằng tiếng Anh, chọn status Jira ở mỗi bước, và với B soạn cả hai PC với rollback viết trước. Rồi debrief 10 phút theo câu hỏi debrief của scenario. **Pass:** 7 tiêu chí thời gian pass (ticket trong 5 phút từ T0; severity xác nhận trong 30 phút; on-call trả lời trong 15 phút và call tree đúng thứ tự; bridge trong 15 phút và PIC trong 30 phút từ T-confirm; thông báo Critical trong 30 phút từ T0 kèm ICT và SGT; update đúng nhịp không bỏ lần nào; on-call có mặt trong 60 phút) và tối đa 1 tiêu chí khác cần cải thiện (CM-06 §8.4). Không chạy gì trên production trước PC duyệt; ON HOLD HQ mang "PC ticket pending"; SYSTEM SUPPORT có Maintenance Request. Không cần access hệ thống.
