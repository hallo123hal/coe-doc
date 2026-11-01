# GP3.2 Escalation and the call tree

> Nguồn: page 2484371868 · 45 phút (Study 10' · Demo/thảo luận 5' · Quiz 5' · Practice 25') · Role-play theo cặp, 4 drill; facilitator: Shift Leader hoặc Sub-Lead · Capabilities C3, C6 · Cần xong G2.7 (kênh, mẫu comment tiếng Anh) và G2.5 (on-call phản hồi 15' và 60', Incident Manager); mang bảng alert SLA G2.3. Chỉ cần Confluence (đọc CM-08, CM-04). Không có access: facilitator in CM-08 §1.2, 1.3, 1.8, 3.2 và thẻ liên hệ của tuần (chỉ vai trò).

## Mục tiêu
Quyết định tình huống cần functional hay hierarchical escalation và nêu đúng người theo trụ và theo giờ; áp dụng thời hạn phản hồi (15, 30, 60') và luật "15' không trả lời thì gọi người kế"; chọn đúng kênh (Jira comment, Mattermost, điện thoại, hotline); viết escalation message tiếng Anh gồm context, status, cần gì, đến khi nào; giữ vững một rule (Knox, RHQ approval) khi requester ép, và escalate quyết định thay vì tự quyết.

## Thuật ngữ
**Functional escalation** (chuyển cho người chuyên môn sâu hơn: Tech Level 1 → Level 2; Merch tạo COEC liên kết); **Hierarchical escalation** (báo lên cấp có thẩm quyền quyết, VD Shift Leader gọi Merch Lead duyệt thay đổi E4); **Call tree** (thứ tự gọi cố định khi không ai trả lời: Tech P0 02:00 — layer 1 phút 0, layer 2 phút 10, Tech Lead phút 15, SDM hotline phút 20); **Layer 1 / layer 2 Tech on-call** (ngoài khung Tech: layer 1 (Tech Lead, Sub-Lead A hoặc B, mỗi người 1 tuần trong 3) xử lý ticket; layer 2 là Team Member Level 2 phối hợp); **SDM hotline 24/7** (điện thoại escalation của Service Delivery Manager: nghe máy trong 15', huy động team trong 30'); **Event ladder** (bảng escalation theo loại sự kiện: incident, complaint, quality, violation, strike — tách khỏi thang SLA từng ticket); **Escalation Log** (ghi mọi escalation từ cấp 2 trở lên trên Samsung Confluence); **Call summary** (note ngắn viết lên ticket trong 15' sau mỗi cuộc gọi: đã thống nhất, còn mở kèm owner và giờ, update kế).

## Nội dung
### 1. Functional và management escalation
Escalate là chuyển vấn đề lên người có năng lực hoặc thẩm quyền hơn. Hỏi trước: **tôi cần kiến thức hay cần một quyết định?**
| Loại | Dùng khi | Ví dụ |
|---|---|---|
| Functional | Cần kỹ năng sâu hơn | Merch cần ImpEx: tạo COEC liên kết. Tech Level 1 chuyển Level 2. Tech Level 2 tạo Maintenance Request cho Samsung L2/L3 |
| Hierarchical | Cần quyết định trên cấp mình | Shift Leader gọi Merch Lead cho thay đổi E4. Tech Lead nhắn RHQ về PC ticket P0 gấp. COE Lead báo RHQ trước SLA breach |
Bốn nguyên tắc: (1) **báo sớm** — báo sớm được ghi nhận, giấu lỗi là vi phạm nghiêm trọng; (2) **escalate không phải đẩy việc** — bạn vẫn là owner tới khi có người nhận rõ ràng trên Jira; người tạo COEC tiếp tục chase Tech; (3) **15' không trả lời thì gọi người kế** — gọi hai lần trong 10', không ai nghe thì sang cấp kế; (4) **mọi escalation để lại dấu vết**: comment ticket, shift log hay on-call log; từ cấp 2 trở lên ghi thêm Escalation Log. Chỉ Tech Level 2 liên hệ Samsung L2/L3; Tech Level 1 và Shift Leader thì không. Chuyển ticket cho Samsung L2/L3 không chuyển quyền sở hữu.

### 2. Call tree của trụ mình, trong và ngoài giờ
Giờ escalation Merch: 08:00–17:00 Thứ Hai–Sáu. Khung Tech: 04:00–19:00 Thứ Hai–Bảy cho Level 1 (Level 2: 08:00–18:00).
| Cấp | Merchandising | Tech (trong / ngoài khung) | QA (giờ QA / ngoài) |
|---|---|---|---|
| 0 | Team Member hoặc Market Owner giữ ticket | Tech Level 1 / layer 1 on-call quét COEC NEW mỗi 5' | QA Team Member / Merch Shift Leader |
| 1 | Shift Leader (luôn tại chỗ, 24/7) | Team Sub-Lead / layer 1 on-call | Sub-Lead trực / QA on-call |
| 2 | Merch Lead; ngoài giờ Lead on-call (Deputy Lead tuần thứ tư) | Tech Lead / layer 2 on-call và Tech Lead | QA Lead |
| 3 | SDM (hotline 24/7) | SDM hotline | SDM hotline |
| 4 | COE Lead | COE Lead | COE Lead |
Thời hạn từ cấp 2 trở lên: **nghe máy trong 15'; quyết định qua điện thoại trong 30'; có mặt tại trung tâm trong 60'** khi cần làm hoặc duyệt. SDM hotline nghe máy trong 15' và huy động team trong 30'; COE Lead trong 1 giờ. Kết hợp với thang SLA: 70% là Shift Leader/Sub-Lead trong 15'; 85% là Lead (on-call ngoài giờ) trong 30'; 95% là COE Lead, báo RHQ trong 1 giờ.
**Ví dụ:** 23:10 thứ Ba, ticket Merch Medium chạm 85%. Ngoài giờ làm việc nên Shift Leader gọi Merch Lead on-call, Lead phải nghe máy trước 23:25 và quyết trước 23:40 (tiếp quản, workaround, hoặc update requester). Shift Leader ghi cuộc gọi lên ticket dạng "[SLA 85%] Remaining … Status … Action … Next check …".
> Giờ QA còn chờ quyết. CM-08 §1.4 tạm theo deck v08Oct (ca sớm 04:00–12:00, ca chiều 11:00–19:00); đề xuất v9.4 là 08:00–16:00 và 16:00–24:00. Dùng bảng CM-08 tới khi CEO quyết.

### 3. Khi nào phải escalate, và kênh nào
| Tín hiệu | Escalate tới | Trong |
|---|---|---|
| SLA 70%, 85%, 95% | Shift Leader/Sub-Lead, Lead, COE Lead | 15', 30', 1 giờ |
| Ticket Merch ở ON HOLD COE chạm 50% hoặc 70% | Shift Leader chase Tech Lead (ngoài giờ: Tech on-call) | Theo chu kỳ cảnh báo |
| Change P0/P1 chờ duyệt PC ticket | Tech Lead hoặc on-call nhắn approver trên Mattermost | Ngay sau khi gửi PC ticket |
| Chạm ngưỡng E4 (≥10,000 USD, >5 market, price file ≥500 SKU) | Merch Lead hoặc Deputy | Trước khi build |
| Nghi incident (giá sai live, lỗi checkout) | Shift Leader, rồi Incident Manager | Phân loại trong 15' (trong giờ) / 30' (ngoài giờ) |
| Yêu cầu ngoài scope | Shift Leader, rồi Lead; COE Lead quyết cùng RHQ | Trước khi trả lời requester |
| Samsung L2/L3 im lặng quá chu kỳ follow-up | Tech Lead; COE Lead nếu cần RHQ | Trong ngày |
| Nghi sự cố an ninh | Shift Leader, DevSecOps Engineer, SDM | Trong 1 giờ |
**Kênh.** Jira comment là kênh chính thức và hiện là kênh duy nhất với subsidiary. Với RHQ là Mattermost. Gọi điện (không bao giờ voice call Mattermost) cho incident P0 hoặc High, cảnh báo 95%, go-live mà requester không trả lời câu hỏi bắt buộc, hoặc sau 2–3 vòng hiểu nhầm. Sau mỗi cuộc gọi viết call summary lên ticket trong 15'. Chỉ nhắn Oliver Leung trên Mattermost cho PC ticket P0 hoặc P1.

### 4. Chuỗi bị chặn: khi cấp kế không trả lời
Quy tắc giống nhau ở mọi cấp: gọi hai lần trong 10'; không ai nghe thì sang cấp kế để **có người trả lời trong 15'**. On-call không trả lời là vi phạm process và ghi vào on-call log.
**Ví dụ Tech P0 02:00, layer 1 im lặng:** phút 0 Merch Shift Leader gọi layer 1 Tech on-call; phút 10 không nghe sau hai lần → gọi layer 2; phút 15 → gọi Tech Lead (nếu Tech Lead chính là layer 1 thì gọi Deputy Sub-Lead); phút 20 → SDM hotline. Trong lúc chờ không làm thay việc Tech: Shift Leader chỉ là người có mặt tại trung tâm, ticket COEC vẫn là việc của Tech Team. Comment lên ticket đã gọi ai và lúc nào.
Nếu chính SDM hotline không nghe, CM-08 nêu một BiPlus delivery manager trong lịch on-call là người thay SDM khi nghỉ phép; số điện thoại ở trang CoE trên Samsung Confluence. Không bao giờ dùng kênh cá nhân hay chat riêng với subsidiary để vòng qua chuỗi im lặng.
Chuỗi bị chặn cũng có thể là **approval** bị chặn: PC ticket gấp mà approver chưa duyệt khi impact tăng. Tech Lead gọi Incident Manager và COE Lead (SDM thay) để COE Lead nói chuyện với RHQ. Không ai chạy change khi chưa duyệt.
> Số hotline, điện thoại trực, on-call đăng trên trang CoE trên Samsung Confluence; CM-08 §1.6 nói Project Assistant cập nhật trước Checkpoint 1 (31/10). Tới đó facilitator đưa danh sách hiện hành.

### 5. Giữ rule dưới áp lực: escalate quyết định
Một số requester ép CoE bỏ qua kiểm soát. Bạn không bao giờ tự quyết ngoại lệ: giữ rule, nói requester điều sẽ xảy ra, và escalate quyết định.
| Tình huống | Rule | Escalate tới |
|---|---|---|
| Subsidiary xin publish giá/promotion không có Knox | Cần Knox theo đường duyệt trong brief, kể cả last-minute; không có thì không publish phần đó | Shift Leader trực và Merch Lead, ngay lập tức |
| EPP site mới hoặc kích hoạt lại, go-live hôm nay, không có email duyệt của RHQ | PC approver chỉ duyệt khi đính email duyệt | Template 19; ticket tạm sang ON HOLD SUBS giao subsidiary; Shift Leader, rồi Lead |
| Yêu cầu ngoài catalogue ("chỉ 5 phút") | CoE chỉ làm service catalogue trong quyền của mình | Shift Leader hoặc Lead; Template 6 sau khi Lead xác nhận; COE Lead đưa RHQ |
**Viết escalation message** theo 6 phần của comment tốt: lời chào, context, status, bước kế + giờ, yêu cầu đánh số, kết. Ví dụ gửi Merch Lead on-call (mô phỏng):
```
Hi [Lead], this is [name], Shift Leader N. DEMO-1209 (NZ, promotion, go-live 03:00 NZT).
Status: setup done and internal check done; Knox approval sent 01:40 ICT along the brief's path, not yet approved.
The subsidiary asks us to publish without Knox.
Need: your decision by 02:30 ICT. I will not publish the promotion until approved.
```
> Việc làm gì khi 23:59 tới mà Knox vẫn thiếu là đề xuất của BiPlus chờ CEO xác nhận (MR-03 §2.6): không publish phần thiếu Knox và báo Shift Leader trực + Merch Lead ngay. Ticket bị trả vì thiếu duyệt EPP đi INVALID hay ON HOLD SUBS cũng còn mở (CM-13 ch.13); tạm dùng ON HOLD SUBS.

## Quiz (đáp án)
1 21:30 thứ Bảy, ticket Merch Low chạm 85% → **B: Merch Lead on-call, nghe máy trước 21:45 và quyết trước 22:00** (escalation Merch chạy 24/7). 2 Chủ nhật 02:00 Tech P0, Shift Leader gọi layer 1 lúc 02:00 và 02:05 không ai nghe; 02:10 → **B: gọi layer 2 on-call** (D sai: Shift Leader không làm thay ticket Tech). 3 Team Member Merch cần 1.5 triệu coupon code, vượt giới hạn 1 triệu/lần ở Backoffice nên Tech phải load bằng ImpEx → **B: functional — tạo COEC liên kết, ticket Merch sang ON HOLD COE, tiếp tục chase Tech** (không chuyển ticket Merch sang COEC; chỉ Tech Level 2 liên hệ Samsung L2/L3). 4 22:40 subsidiary: "Go-live 00:00, Knox sẽ đến sau, publish ngay đi" → **C: không publish phần chưa duyệt; báo Shift Leader trực và Merch Lead ngay, trả lời trên ticket** (template last-minute chỉ thay QA, không thay Knox). 5 Kích hoạt lại EPP site hôm nay, subsidiary nói RHQ "đồng ý qua điện thoại" nhưng không có email → **C: Template 19, xin email duyệt, tạm sang ON HOLD SUBS giao subsidiary, báo Shift Leader** (ON HOLD RHQ chỉ dẫn tới bị từ chối). 6 Gọi subsidiary xác nhận end date thiếu, sau cuộc gọi → **B: viết call summary lên ticket trong 15'** (Mattermost không phải kênh với subsidiary). 7 Escalation message đầy đủ → **C: "Hi [Lead], DEMO-1209 (NZ, promotion, go-live 03:00 NZT). Setup and internal check done; Knox sent 01:40 ICT, not approved. Subsidiary asks to publish without Knox. Need your decision by 02:30 ICT. I will not publish until approved."**

## Practice
**PR-GP3.2-1. Bốn drill escalation** (20', role-play theo cặp, facilitator đóng vai người bị gọi; dùng ma trận CM-08 §1.2 và 1.3; ticket mô phỏng): với mỗi drill nói ai bạn liên hệ, kênh nào, trước mấy giờ, và viết message tiếng Anh 3–5 dòng. (1) 23:10 thứ Ba, ticket Merch Medium chạm 85%. (2) 02:00 Chủ nhật, Tech P0; layer 1 on-call không nghe hai cuộc. (3) 22:40, subsidiary xin publish promotion trước khi Knox duyệt. (4) 10:00, EPP site cần kích hoạt lại cho go-live hôm nay; không có email duyệt của RHQ. **Pass:** 4/4 đúng người, kênh, giờ. (1) Merch Lead on-call qua điện thoại; nghe máy trước 23:25, quyết trước 23:40; SLA comment lên ticket. (2) Layer 2 lúc 02:10, Tech Lead lúc 02:15 (Deputy Sub-Lead nếu Tech Lead là layer 1), SDM hotline lúc 02:20; comment ai được gọi và lúc nào; Shift Leader không làm ticket COEC. (3) Không publish; báo Shift Leader trực và Merch Lead ngay; comment ticket nêu rule. (4) Template 19 trên ticket, ticket sang ON HOLD SUBS giao subsidiary, báo Shift Leader; không kích hoạt lại trước khi đính email. Mỗi message có context, status, yêu cầu và giờ. Không cần truy cập hệ thống.
