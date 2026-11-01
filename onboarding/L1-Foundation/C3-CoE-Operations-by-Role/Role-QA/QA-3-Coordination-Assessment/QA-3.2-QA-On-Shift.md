# QA-3.2 QA on shift: handover, on-call, go-live waves and incident re-checks

> Nguồn: page 2492891457 · 60 phút (Study 20' · Demo/thảo luận 10' · Quiz 10' · Practice 20') · Lecture ngắn, walk-through ticket hai wave và một handover note thật, rồi hai bài giấy; facilitator: QA Sub-Lead 1 (trưởng ca chiều) cùng một Merch Shift Leader · Cần xong QA-1, QA-2, QA-3.1; ôn QA-1.2 chủ đề 2 (đường đi sau PASS) và G2.5; chỉ cần Confluence + giấy; mang timeline DEMO-4105 từ QA-3.1.

## Mục tiêu
Nêu các điểm bàn giao QA (04:00, 11:00–12:00, 19:00), mỗi điểm giao gì, và viết handover note 19:00 theo template 6.5.2; quyết định ticket ngoài giờ QA chờ Q4 hay gọi QA on-call và theo đúng call chain; thực hiện QA again cho một wave go-live (ai kiểm, comment A.6, evidence template G, status sau wave); re-check một fix Merch trong incident và ghi kết quả lên ticket gốc.

## Thuật ngữ
**Q4, Q11** (ca QA tạm thời: Q4 ca sớm 04:00–12:00, Q11 ca chiều 11:00–19:00, thứ Hai–thứ Bảy; CM-04 §2.1; chờ quyết định CEO); **QA on-call** (QA Lead, Sub-Lead 1 hoặc 2 trực ngoài giờ QA: 19:00–04:00 và cả Chủ nhật, mỗi người 1 tuần trong 3); **Handover note 6.5.2** (note bàn giao Tech & QA lúc 11:00 và 19:00); **Exit criteria** (điều kiện để ca được rời, CM-04 §5.8); **Go-live wave** (một mốc go-live trong ticket; 3 promotion bắt đầu 3 ngày = 3 wave); **QA again**; **Template A.6** (comment "Go-live batch n/N QA re-check"); **Template G** (file evidence ngắn cho một wave, `<ticket>_GL_batch<n>.pptx`); **Second checker** (người Merch certified, không phải Doer, kiểm R3 go-live trên storefront trong 30' / E4 15'); **Re-check after a fix** (kiểm lại setup Merch đã fix trước khi bật lại, CM-06 §2.7).

## Nội dung
### 1. Ngày làm việc của QA và các điểm bàn giao
Giờ QA chưa chốt; tạm theo mô hình deck v08Oct (CM-04 §1.3, §2.1). Đề xuất v9.4 sẽ dùng 08:00–16:00 và 16:00–24:00 và mọi giờ dưới đây sẽ dịch theo.

| Giờ | Ai giao | Giao cho | QA giao gì |
|---|---|---|---|
| 04:00 | Merch Shift Leader ca đêm | Q4 (dispatcher: Sub-Lead 2) | Ticket High qua đêm, R3 go-live đêm QA phải kiểm lại, các cuộc gọi on-call; Q4 kiểm các go-live đã liệt kê trước |
| 11:00–12:00 | Q4 | Q11 (Sub-Lead 1) | Queue QA REVIEW theo QA due và giờ go-live; incident đang chạy; những gì đã hứa. Gặp trực tiếp, không qua chat; biên bản trên Samsung Confluence |
| 19:00 | Q11 | Merch Shift Leader ca tối; QA on-call nếu còn ticket High mở | Ticket High cần QA gate, go-live đêm cần QA, điều đã hứa qua đêm. Dùng template 6.5.2 |
| 08:00 thứ Hai | On-call tuần trước | On-call tuần này | Incident mở, R3 go-live trong khung 19:00–04:00, launch trong tuần |

- **Exit criteria Q4/Q11 (CM-04 §5.8):** setup của ca tối được kiểm trước khi market mở/go-live; mọi ticket QA REVIEW đã giao trong 15'; queue còn lại bàn giao theo thứ tự deadline. Ca sớm chỉ rời sau khi ca chiều xác nhận; ca chiều đến muộn thì ca sớm ở lại và báo Sub-Lead.
- **Thứ Bảy:** Q4 có 2 người (một là dispatcher certified), Sub-Lead 1 dẫn Q11. **Chủ nhật:** không có ca QA; Merch Shift Leader chạy QA queue filter lúc 09:00 và 17:00 và gọi QA on-call khi ticket phải xử lý trước thứ Hai (CM-04 §2.3; ai chạy filter còn chờ chốt).

| Mục template 6.5.2 | QA viết gì |
|---|---|
| 1. Shift and people | Ngày, ca, người giao, người nhận (19:00: Shift Leader ca tối, cc QA on-call) |
| 2. High-priority tickets | Ticket Merch High cần QA gate: status, bước tiếp, owner |
| 4. Queue | Queue QA REVIEW theo QA due và giờ go-live |
| 7. Overnight (chỉ 19:00) | Go-live đêm cần QA again, điều đã hứa, ticket cần gọi on-call nếu xấu đi |
| 8. Acknowledgement | Người giao, người nhận, giờ |
Mục 3, 5, 6 của template là phần Tech; QA ghi "None". Không chép giá, price file, dữ liệu khách vào note; chỉ link Jira ticket (CM-04 chương 6).

### 2. Ngoài giờ QA và QA on-call
- On-call phủ 19:00–04:00 ngày thường, tối thứ Bảy và cả Chủ nhật; QA Lead, Sub-Lead 1, Sub-Lead 2 mỗi người một tuần trong ba; tuần chạy từ 08:00 thứ Hai tới 08:00 thứ Hai sau (CM-04 §2.7).
- On-call chỉ nhận hai loại: ticket Merch High cần QA gate, và re-check setup Merch sau fix incident. Không BVT, không QA cho Tech (CM-06 §4.2).
- Ticket Medium/Low vào QA REVIEW lúc 21:00 chờ Q4 lúc 04:00. **Clock vẫn chạy**, nên note 19:00 phải liệt kê nếu sẽ breach hoặc go-live trước 04:00. **Không bao giờ chuyển ON HOLD SUBS để dừng clock.**
- Shift Leader gọi; on-call nghe máy trong 15' và có mặt tại trung tâm Hà Nội, khu secure, trong 60'. Trên đường chỉ nghe và tư vấn; không dùng hệ thống Samsung từ điện thoại hay PC ở nhà. Mọi cuộc gọi ghi vào on-call log.
- Không trả lời sau hai cuộc gọi trong 10': gọi QA Lead (nếu QA Lead đang là on-call thì Sub-Lead 1), rồi SDM hotline (CM-06 §4.4).
- Đến nơi, on-call tự dispatch ticket cho mình bằng A.1 và kiểm như ticket khác; sau PASS Shift Leader duyệt và chuyển PRD SETUP như ban ngày.

### 3. QA again trên production ở mỗi wave go-live
Simulator chứng minh setup trước go-live, nhưng không thấy được cache, sync trễ, promotion khác bật cùng SKU, hay trang AEM publish lệch giờ. Nên mỗi wave kiểm lại trên storefront thật (CM-13 §3.7, CM-05 §6.4).
- Sau PASS + Shift Leader duyệt, owner hand-back ở REVIEW SETUP kèm evidence. Subsidiary chưa duyệt đến 23:59 hôm trước go-live thì shift publish đúng giờ và comment (CM-13 §3.6).
- Sau khi subsidiary duyệt, ticket chờ ở PENDING LAUNCH; ngày giờ từng wave ghi trên ticket và trong mọi note bàn giao đến khi xong.
- Mỗi wave Merch shift publish live và kiểm Knox đã có. **QA không publish.**
- QA kiểm lại và comment A.6. Còn wave: ticket ở lại PENDING LAUNCH. **Không chuyển về STG SETUP, QA REVIEW, PRD SETUP chỉ để kiểm lại** (các status này chạy SLA clock).
- Wave cuối pass: QA comment A.6 cuối và mention owner; owner hoặc Shift Leader chuyển LAUNCH VERIFICATION. **Không chuyển LAUNCH VERIFICATION giữa các wave**: RHQ đóng hàng loạt các ticket này và wave sau sẽ không bao giờ được kiểm.

| Go-live | Ai kiểm | Khi nào |
|---|---|---|
| R3, hoặc R2 có gate, trong giờ QA | QA TM do dispatcher giao (không phải Doer) | ≤30' sau go-live (E4: 15') |
| R3 ngoài giờ QA (đêm, Chủ nhật) | Second checker certified của Merch shift, theo checklist go-live; nghi ngờ thì gọi QA on-call | ≤30' (E4: 15'); QA Team kiểm lại ở ca QA kế, từ 04:00 |
| R2 có gate ngoài giờ QA | Doer kiểm storefront; QA kiểm lại ở ca QA kế | Lúc go-live, rồi đầu ca QA kế |
| Ticket High, go-live đêm, thấy bất thường | Shift Leader gọi QA on-call | Ngay lập tức |

Cách kiểm một wave (QA-02 §7.3): đọc comment "Go-live schedule" và mở lại evidence trước go-live; xác nhận shift đã publish; kiểm như khách hàng trên CoE workstation, incognito, desktop và mobile (giá ở PDP, category, search; cart và ngưỡng; giới hạn coupon; stacking; store scope; tổng checkout; text banner); so với kết quả simulator đã pass; viết A.6 và đính template G. VD: `Go-live batch 2/3 QA re-check: checker Chi, 07-Dec 09:12 ICT (10:12 SGT). PDP, cart, coupon limit, mobile checked. Result: PASS. Evidence DEMO-QA-310_GL_batch2.pptx.` Theo dõi order anomaly 2 giờ sau R3 go-live là việc của Merch shift, không phải QA.

### 4. QA again phát hiện lỗi trên production
Không phải FAIL thường: setup đang live, khách thấy được (QA-02 §7.5). Báo Shift Leader ngay, trực tiếp, ghi giờ phát hiện lên ticket. **Không tự sửa, không tự tắt promotion.** Shift Leader xác nhận impact trong 15': có rủi ro tiền → incident theo CM-06, containment trong 30' trên chính Shop Merchandising ticket gốc; không impact (VD sai một từ trong banner) → Shift Leader quyết định cách sửa, ticket còn ở PENDING LAUNCH thì về STG SETUP và clock chạy lại. Ghi defect category + RC; lỗi của CoE phát hiện sau QA PASS là escaped defect trong báo cáo chất lượng tuần.

### 5. Re-check fix Merch trong incident
Khi giá/promotion sai đang live: Doer containment trước bằng kill switch và second checker xác nhận đã chặn; sau đó Doer sửa đúng. QA vào cuộc ở bước này (CM-06 §2.7, §6.2):
- **Ai gọi:** Incident Manager hoặc Shift Leader; trong giờ QA là QA Team đang ca, ngoài giờ là QA on-call.
- **Kiểm gì:** setup đã sửa theo checklist service, đủ scope như setup mới; đọc internal check mới và giá trị trước/sau. Ticket đi qua QA REVIEW trước khi bật lại promotion.
- **Không kiểm:** thay đổi của Tech. Fix cần ImpEx trên COEC liên kết thì Tech tự kiểm; QA kiểm phần Merch sau Merch PIC.
- **Knox:** fix đổi action/condition/website/dates thì Doer gửi Knox mới song song; QA không kiểm Knox.
- **Ghi ở đâu:** QA comment trên ticket Shop Merchandising gốc chứa comment `[INCIDENT]`, kèm evidence như PASS/FAIL thường. Sau khi Shift Leader duyệt và bật lại, QA kiểm lại trên production.
- Sau incident, QA Lead giải thích trong RCA vì sao checklist không chặn được lỗi; checklist sửa trong 3 ngày làm việc; Doer và Checker được certify lại.

## Quiz (đáp án)
1 21:00 thứ Tư, ticket Merch High cần QA gate vào QA REVIEW → **B: Shift Leader gọi QA on-call**. 2 Gọi on-call hai lần trong 10' không ai nghe, QA Lead không trực → **A: QA Lead, rồi SDM hotline**. 3 R3 go-live 23:00 ICT thứ Ba, ai kiểm storefront trước → **D: second checker certified của Merch shift**. 4 Wave 1/2 pass lúc 00:20, đồng nghiệp muốn chuyển LAUNCH VERIFICATION "cho gọn board" → **B: giữ ở PENDING LAUNCH tới khi wave 2 được kiểm**. 5 19:00 Q11 hết ca, bàn giao cho ai → **A: Shift Leader ca tối, note 6.5.2**. 6 Doer đã sửa discount sai trong incident, ai kiểm trước khi bật lại → **C: QA đang ca, hoặc QA on-call ngoài giờ**.

## Practice
- **PR-QA3.2-1** (10', giấy): DEMO-QA-310 (SG, R3, Medium, không E4). QA PASS thứ Năm 03/12/2026, Shift Leader duyệt, REVIEW SETUP 16:00, subsidiary duyệt 18:00. Ba promotion: wave 1 lúc 00:00 SGT thứ Sáu 04/12; wave 2 10:00 SGT thứ Hai 07/12; wave 3 00:00 SGT Chủ nhật 13/12. Với mỗi wave viết: giờ VN và thứ; ai kiểm storefront và khi nào; QA Team có kiểm lại không và khi nào; tiêu đề comment A.6; tên file template G; status sau wave. Đáp án: **Wave 1** 23:00 ICT thứ Năm 03/12, ngoài giờ QA → second checker của Merch ca tối trong 30', Q4 kiểm lại từ 04:00 thứ Sáu; `Go-live batch 1/3 QA re-check`; `DEMO-QA-310_GL_batch1.pptx`; PENDING LAUNCH. **Wave 2** 09:00 ICT thứ Hai 07/12, trong ca Q4 → QA TM do dispatcher giao trong 30'; batch 2/3; `_GL_batch2`; PENDING LAUNCH. **Wave 3** 23:00 ICT thứ Bảy 12/12, ngoài giờ QA và Chủ nhật không có ca QA → second checker trong 30', gọi QA on-call chỉ khi có bất thường; Q4 kiểm lại từ 04:00 thứ Hai; batch 3/3; `_GL_batch3`; sau đó owner hoặc Shift Leader chuyển LAUNCH VERIFICATION.
- **PR-QA3.2-2** (10'): thứ Ba 18:40. Queue: DEMO-QA-401 (MY, High, R3 price, còn 1h50 SLA, Checker An, còn ~30' việc); DEMO-QA-402 (AU, Medium, R3 promotion, vào QA REVIEW 18:30, go-live 00:00 AEDT tối nay); DEMO-QA-403 (VN, Low, còn 18h). Một R3 promotion TH go-live 00:00 ICT và bạn đã hứa với subsidiary là QA kiểm vào sáng. Viết note template 6.5.2 và nói gọi ai trước khi về. Pass: mục 1 ghi Shift Leader ca tối là người nhận; mục 2 liệt kê DEMO-QA-401 kèm bước tiếp + owner và gọi QA on-call vì còn High mở; mục 4 xếp queue theo QA due; DEMO-QA-402 được flag: go-live 20:00 ICT tối nay mà không ai kiểm được sau 19:00 nên Shift Leader quyết ngay (R3 không go-live nếu thiếu QA PASS; báo QA on-call theo đề xuất QA-02 §6.4); mục 7 liệt kê go-live TH cho second checker và Q4 re-check, cùng lời hứa với subsidiary; phần Tech ghi "None"; không chép giá hay dữ liệu khách; mục 8 có người giao, người nhận, giờ.
