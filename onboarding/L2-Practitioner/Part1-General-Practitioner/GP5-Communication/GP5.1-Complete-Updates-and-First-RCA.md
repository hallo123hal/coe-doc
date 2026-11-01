# GP5.1 Complete updates and a first RCA

> Nguồn: page 2483945877 · 60 phút (Study 15' · Demo/thảo luận 10' · Quiz 5' · Practice 30') · Thực hành theo case; facilitator: Shift Leader hoặc Sub-Lead · Capability C6 · Cần xong G2.7 và G2.8 (L1); mang 12 mẫu reply CM-08 ch.4 và template Merch A.1–A.13 của MR-04 Appendix A (in hoặc mở trên CoE workstation). Viết trên giấy hoặc Word trên CoE workstation, không bao giờ trên công cụ cá nhân hay AI. Đọc ticket luyện tập SCOE-43 (TRN-037) và SCOE-47 (TRN-041) nếu có Jira; không có thì facilitator in text ticket và các mục cần đọc.

## Mục tiêu
Viết ticket update theo 6 phần của comment tốt và đúng template trong A.1–A.13 hoặc CM-08; viết incident update theo template CM-06 với giờ ICT và SGT và đúng nhịp; tách fact khỏi assumption trong timeline, đánh dấu mỗi assumption cần xác nhận; viết RCA 5 Whys có root cause, mục "vì sao không bị chặn" và bảng CAPA có owner và deadline; tự chấm văn bản theo rubric T2 trước khi gửi.

## Thuật ngữ
**Status update** (comment ticket nêu status, đã làm gì, bước kế, khi nào; VD "next update by 13:00 SGT" trong comment đầu TRN-037); **Next update time** (giờ bạn hứa comment kế, luôn theo ICT và giờ địa phương hoặc SGT; gửi kể cả khi không có gì đổi); **Incident update #n** (update đánh số gửi RHQ trong incident: mỗi 30' với Critical, mỗi 2h với High, tới khi phục hồi; không có tin vẫn gửi "No change since the last update"); **Fact và assumption** (fact có evidence (kết quả query, comment, ảnh); assumption chưa có, đánh dấu "to be confirmed"); **5 Whys** (hỏi "vì sao" liên tiếp, mỗi câu đáp có evidence, tới nguyên nhân mà sửa nó thì sự kiện không lặp); **CAPA** (hành động khắc phục và phòng ngừa: mỗi hành động có mô tả kiểm chứng được, một owner theo vai trò, deadline và cách kiểm tra hiệu quả); **T2 rubric** (5 tiêu chí — Clear, Complete, Tone, Language, Template và process — chấm 1–3; đạt khi không tiêu chí nào 1 và tổng ≥10/15).

## Nội dung
### 1. Ticket update: status, done, next, when
Mỗi comment một mục đích. CM-08 có bảy nguyên tắc: một comment một mục đích; câu ≤20 từ, không "pls", "asap", "thx"; luôn nêu bước kế và giờ theo giờ VN và giờ địa phương; hỏi một lần, đủ, đánh số; nêu sự thật không đổ lỗi; không hứa vượt thẩm quyền (không deadline ngắn hơn SLA, không gọi mục tiêu nội bộ là "SLA"); giữ chuyên nghiệp.
Comment tốt có 6 phần: lời chào (tên người nhận, giới thiệu lần đầu); context (yêu cầu trong một câu); status (đã làm gì, kết quả); bước kế và giờ (ai làm gì, khi nào); yêu cầu (câu hỏi đánh số nếu có); kết (owner, cảm ơn khi hợp).
**Ví dụ TRN-037 (SCOE-43):** SEIN tạo COEC cho 5 order stuck. Comment Tech đầu sau khi NEW → ASSIGNED đã có status, owner, update kế và câu hỏi đánh số:
```
Hi [requester name], thank you. We have received your request for 5 orders (service: order remediation, priority P2).
Handler: CoE Tech (Level 2). Next step: read-only analysis of each order; next update by 13:00 SGT.
Questions: (1) ID261017-26876093: should we proceed after confirming the tax value on the entry, or cancel?
(2) ID260617-23039188: payment not captured - please advise cancel or wait for PG confirmation.
Note: ID261022-26950388 already has a sales order number in NERP, so it cannot be re-pushed.
```

### 2. Chọn đúng template
Không viết từ đầu. Merch dùng A.1–A.13 trong MR-04 Appendix A; trả lời chung là 12 template (và 13–22) của CM-08 ch.4. Khi khác nhau, CM-13 Appendix B thắng.
| Tình huống | Template |
|---|---|
| Chuyển ticket sang STG SETUP | A.1 Ghi nhận: service, priority, go-live giờ địa phương và ICT, owner, update kế |
| Brief thiếu hoặc mâu thuẫn | A.2 Câu hỏi gộp; rồi ON HOLD SUBS và Assignee = subsidiary |
| Setup xong, QA pass | A.3 Mời review QA evidence (REVIEW SETUP) |
| Không có phản hồi lúc 23:59 trước go-live | A.4 "Published as aligned for go-live at [date time]. No feedback received at the time of publishing." |
| Chờ Tech | A.6 "Tech support needed. COEC ticket [key] has been raised and linked." (ON HOLD COE) |
| Mỗi wave go-live | A.7 Lặp kết quả QA mỗi wave |
| Trễ do CoE | A.9 Giải thích: "This was on our side", giờ mới và hành động phòng ngừa |
| Đã gửi Knox | A.13 Giờ submit và đường duyệt như trong brief |
| Ticket sẽ trễ | CM-08 Template 4 Delay notice: lý do, giờ hoàn thành mới theo ICT và địa phương, đang làm gì, update kế |
**Ca thường: delay notice.** Template 4 dùng trước deadline, thường ở cảnh báo 85% khi Lead quyết update requester. Lead hoặc Shift Leader duyệt văn bản. Không đổ lỗi cho requester hay Samsung L2/L3. Ở 95% COE Lead báo RHQ riêng.
**Ví dụ TRN-041 (SCOE-47):** ticket Merch THAME-TRN041 chờ COEC ở ON HOLD COE. Owner Merch đăng A.6 với "What is needed: Tech investigation of PR01 and PR02 on test_smb_th. Next update: [date hh:mm local time]." Clock Merch vẫn chạy ở ON HOLD COE nên owner phải update theo các cảnh báo SLA.
> A.1–A.13 là template Merchandising (MR-04 Appendix A). Tech dùng template CM-08 và CM-06. CM-13 Appendix B thắng khi lời văn khác nhau.

### 3. Incident update
Incident update không phải comment ticket dài hơn. Có header cố định và nhịp cố định.
| Severity | Thông báo đầu | Update |
|---|---|---|
| Critical | 30' từ T0 (nội bộ; RFP 2h) | Mỗi 30' tới khi phục hồi |
| High | 2h từ T0 (RFP) | Mỗi 2h |
| Giá/promotion sai trên production | 30', tới RHQ và subsidiary | Theo severity |
| Medium, Low | Comment ticket | Theo nhịp ticket |
Gửi trên Mattermost tới RHQ Platform team, dán vào incident channel và ticket, đăng bản ngắn cho subsidiary dưới dạng Jira comment. Cấu trúc (CM-06 Template 2, CM-08 Template 10): dòng tiêu đề `[INCIDENT][severity][market] Update n | ticket`; giờ ICT và SGT; Status; Since the last update; Next steps; Impact; Next update.
**Ví dụ (TC-01 case A.7, mô phỏng):** Critical `DEMO-5678`, khách AU không trả bằng thẻ được từ ~01:50 ICT. 03:30 ICT Update 2:
```
[INCIDENT][Critical][AU] Update 2 | DEMO-5678
Update 2 at 03:30 ICT (04:30 SGT). Status: not yet restored.
Since the last update: the AU card payment configuration was overwritten
by a sync job at 01:40 ICT. A PC ticket (DEMO-PC-0470) to restore the
previous configuration was raised at 03:20 ICT and is waiting for approval.
Next steps: apply the change as soon as it is approved; verify with test orders.
Impact (estimate): unchanged; customers in AU cannot pay by card.
Next update: by 04:00 ICT (05:00 SGT), or earlier if the status changes.
```
TC-01 chấm: tiêu đề theo template, giờ ICT và SGT, Status rõ, sự kiện không đoán không đổ lỗi, PC ticket đang chờ, bước kế cụ thể, impact, update kế đúng nhịp, không dữ liệu khách.

### 4. Fact, assumption và timeline
RCA bắt đầu từ timeline sự kiện. Mỗi dòng có giờ kèm time zone và nguồn. Câu không có nguồn là assumption: viết ra, nhưng đánh dấu "to be confirmed" và nói sẽ xác nhận bằng cách nào.
**Ví dụ TRN-041:** COEC báo hai rule trên site EPP test `test_smb_th`: PR01 (`TRAINING_<NAME>_TRN041_PR01`, 10% off `SM-S938BZKBTHL`) PUBLISHED nhưng cart test hiện giá đầy đủ; PR02 (8% off `SM-S921BLGCTHL`) KNOXAPPROVED từ D-2 09:30 nhưng chưa live lúc D0 14:00 (GMT+7).
| Giờ (GMT+7) | Sự kiện | Fact/assumption | Nguồn |
|---|---|---|---|
| D-2 09:30 | PR02 được Knox duyệt | Fact | Rule status, evidence-case-B.csv |
| D0 10:20 | Requester thấy PR01 không áp dụng lần đầu | Fact | Text ticket |
| D0 sau triage | Promotion group mặc định của site là `test_smb_thPromotionGroup`; website của PR01 là `thPromotionGroup` | Fact | HAC query Q1, Q2 |
| D0 sau triage | PR01 chưa bao giờ áp dụng trên site này (PromotionResult = 0) | Fact | Q4, Q5 |
| D0 sau triage | PR02 có hai version KNOXAPPROVED của một rule | Fact | Publish log, known error KE-TEC-TSP-01-01 |
| ? | Doer chọn group B2C vì internal check line không có giá trị promotion group | Assumption | Cần xác nhận từ comment internal check và setup |
> Dòng cuối là assumption minh họa do tác giả khoá học viết; ticket không nói vì sao PR01 nằm sai group. Trong RCA của bạn giữ đánh dấu cho đến khi evidence setup xác nhận hoặc bác bỏ.

### 5. RCA 5 Whys và CAPA
Luật CM-07: RCA trung thực, không đổ lỗi, không che giấu. "Người đó nhầm" không bao giờ là điểm dừng; câu kế là "vì sao hệ thống để một người nhầm mà không bị chặn?". Hạn: incident Critical và High 48h sau phục hồi, tối đa 72h, bản nháp review nội bộ ở 36h; lỗi cấu hình Merch trên production theo hạn incident, và QA Lead review vì sao checklist không chặn được. English Coach review RCA trước khi gửi RHQ.
Template RCA 10 mục: thông tin chung; tóm tắt (3–5 câu); timeline (ICT và SGT); impact; direct cause; root cause (5 Whys kèm evidence); vì sao không phát hiện/chặn sớm hơn (price sanity, internal check, Knox, QA, approval, post-change check, order monitor); CAPA; bài học và kiến thức; duyệt.
**Khung 5 Whys cho PR01 (TRN-041):** (1) vì sao cart test hiện giá đầy đủ? PR01 chưa bao giờ áp dụng trên `test_smb_th` (Q4, Q5). (2) vì sao? Website của PR01 là `thPromotionGroup`, site dùng `test_smb_thPromotionGroup` (Q1, Q2); rule phải nằm trong promotion group mặc định của site. (3) vì sao chọn sai group? Cần xác nhận từ comment setup và internal check. (4) vì sao internal check và QA không chặn? Cần xác nhận: internal check line có ghi promotion group không, và checklist QA có test cart trên từng site trong scope không? (5) vì sao template hay checklist bỏ sót? Chỉ trả lời bằng evidence (lịch sử trang, version runbook).
Mỗi CAPA có mô tả kiểm chứng được (không bao giờ "be more careful"), một owner theo vai trò, deadline (sửa checklist và rule trong 3 ngày làm việc), cách kiểm hiệu quả, và status theo dõi tới khi đóng.
> PR02 trong TRN-041 là lỗi publish của nền tảng (hai version approved, KE-TEC-TSP-01-01) và đi tới Samsung L2/L3 bằng Maintenance Request mà chỉ Tech Level 2 tạo. Không trộn hai nguyên nhân vào một chuỗi RCA: viết một 5 Whys cho mỗi nguyên nhân.

### 6. Tự kiểm bằng rubric T2
Trước khi gửi update hay RCA, tự chấm 5 tiêu chí: Clear (người đọc biết phải làm gì), Complete (ticket, giá trị, giờ kèm time zone, hành động kế), Tone (lịch sự, chuyên nghiệp, không đổ lỗi), Language (không lỗi làm đổi nghĩa), Template và process (đúng template, không hứa ngoài process). Mỗi tiêu chí 1 (chưa đạt), 2 (đạt) hoặc 3 (tốt). Đề xuất đạt: không tiêu chí nào 1 điểm và tổng ≥10/15. Với Lead và Sub-Lead T2 là một RCA viết; với Tech là một incident update viết; với Market Owner và Team Member là 5 ticket mẫu. Trong 4 tuần đầu mọi tin gửi subsidiary hoặc RHQ được Shift Leader hoặc buddy duyệt trong 15' trước khi gửi (T8).

## Quiz (đáp án)
1 14:00 ticket Medium chạm 85%, Lead quyết báo requester sẽ trễ → **B: "I am sorry to inform you that this setup will be later than planned. Reason: the QA check found two errors to fix. New expected completion: 18:00 ICT (19:00 local). I will update you again by 17:00 ICT."** (A đổ lỗi QA và dùng "asap"; C gọi lời hứa là "SLA"; D im lặng). 2 Bridge incident Critical thanh toán AU, Update 2 gửi 03:30 ICT, 04:00 ICT không đổi → **B: gửi Update 3 lúc 04:00 ICT (05:00 SGT): "No change since the last update", bước hiện tại và update kế 04:30 ICT** (C là nhịp của High). 3 TRN-037, subsidiary xin "re-push to NERP" order ID261022-26950388 đã có SO number → **C: "This order already has a sales order number in NERP, so it cannot be re-pushed. Please check delivery in NERP."** (A, B sẽ tạo order trùng trên NERP). 4 Timeline TRN-041 bạn viết "Doer chọn thPromotionGroup vì internal check line không có promotion group", chưa xem internal check → **B: ghi là assumption đánh dấu "to be confirmed" kèm evidence sẽ kiểm**. 5 Chuỗi 5 Whys dừng ở "Team Member nhầm" → **C: dừng ở con người; câu kế là vì sao hệ thống (internal check, checklist QA, runbook) không chặn được** (D nhầm RCA với quyết định strike của RHQ). 6 Dòng CAPA đúng CM-07 → **B: "Add 'promotion group = site default group' as a blocking item in the promotion internal check template; owner: Process and Knowledge Lead; within 3 working days; check: 100% of R3 internal checks for 30 days include the line."** 7 Reply điểm Clear 3, Complete 2, Tone 3, Language 1, Template 3 → **B: không đạt, một tiêu chí ở 1 điểm** (tổng 12/15 chưa đủ).

## Practice
- **PR-GP5.1-1. Năm update** (15'; giấy/Word trên CoE workstation; text ticket SCOE-43 TRN-037, SCOE-47 TRN-041 và kịch bản TC-01 A.7): viết (1) comment đầu TRN-037 sau NEW → ASSIGNED với hai câu hỏi; (2) update TRN-037 cho cả 5 order sau phân tích (một dòng mỗi order); (3) comment A.6 trên ticket Merch THAME-TRN041 khi chờ COEC; (4) delay notice Template 4 cho THAME-TRN041 ở 85%; (5) Update 2 của incident TC-01 A.7 lúc 03:30 ICT. **Pass:** mỗi update ≥2 điểm trên mọi tiêu chí T2 (Clear, Complete, Tone, Language, Template); update 2 nói ID261022-26950388 không re-push và ID260617-23039188 chờ quyết định của subsidiary; update 5 có giờ ICT và SGT, nêu PC ticket DEMO-PC-0470 đang chờ và update kế trước 04:00 ICT (05:00 SGT); không update nào chứa tên, email, số điện thoại khách. Không cần truy cập hệ thống.
- **PR-GP5.1-2. RCA cho TRN-041 (promotion published but not applied)** (15'; text ticket TRN-041 và kết quả query facilitator đưa (giá trị Q1, Q2, Q4, Q5 từ ticket)): viết RCA một trang cho PR01 theo template CM-07 10.5: tóm tắt, timeline có fact và assumption đánh dấu, direct cause, 5 Whys, "vì sao không bị chặn", bảng CAPA ≥3 hành động. Thêm một dòng nói PR02 là nguyên nhân riêng do Tech xử lý qua Maintenance Request. **Pass:** direct cause nêu website PR01 là `thPromotionGroup` trong khi `test_smb_th` dùng `test_smb_thPromotionGroup`; chuỗi không dừng ở con người; ít nhất một assumption đánh dấu "to be confirmed"; mỗi CAPA có một owner theo vai trò, deadline và cách kiểm hiệu quả; rubric T2 ≥2 mỗi tiêu chí do facilitator chấm. Không cần truy cập hệ thống.
