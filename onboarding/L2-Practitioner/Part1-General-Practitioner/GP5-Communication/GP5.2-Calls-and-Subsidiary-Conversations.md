# GP5.2 Calls and subsidiary conversations in English

> Nguồn: page 2483730257 · 60 phút (Study 15' · Demo/thảo luận 10' · Quiz 5' · Practice 30') · Thực hành theo case; facilitator: Shift Leader hoặc Sub-Lead · Capability C6 · Cần xong G2.7 (L1) và GP5.1 (status update, rubric T2); mang tai nghe, giấy, mẫu call summary CM-08 và Template 6 (từ chối lịch sự). Chỉ cần Confluence (đọc); facilitator phát bản ghi Handover Working Session P1 (23/10). Không có Confluence: facilitator phát bản ghi và in các mục cần đọc.

## Mục tiêu
Nghe bản ghi 10 phút và liệt kê decision và action item kèm owner, ngày; dùng cấu trúc cuộc gọi 5 bước và câu xác nhận trong cuộc gọi với subsidiary; viết call summary lên ticket trong 15' theo format CM-08; xử lý câu hỏi scope, đổi priority và pushback mà không phá SLA hay luật priority, và đưa hướng đi tiếp.

## Thuật ngữ
**Call summary** (bản ghi cuộc gọi lên ticket trong 15': giờ ICT, gọi với ai, Agreed, Open (owner, hạn), Next update); **Confirmation sentence** (nhắc lại điều đã thống nhất trước khi kết thúc, VD "So, to confirm: the end date is 31 December, 23:59 local time."); **Decision** (điều cuộc họp đã thống nhất mà chưa ai phải làm gì, VD "SLA đếm 5 status cho Shop Merchandising"); **Action item** (việc có một owner và một ngày, ghi trong minutes trên Confluence Samsung); **Priority reassessment** (Sub-Lead kiểm priority trước khi giao vì reporter hầu như luôn raise High); **Saying no with a path forward** (từ chối kèm lý do và phương án thay: ai làm được, kênh nào, CoE làm được gì thay); **Commitment authority** (ai được hứa cam kết mới; không có thẩm quyền thì nói "I will confirm with our COE Lead and come back to you by [date]").

## Nội dung
### 1. Nghe và xác nhận
Phần lớn việc là viết, nhưng bạn phải nói khi có incident, khi ticket sắp lỡ deadline, trong họp governance, và khi hai ba vòng viết vẫn còn hiểu nhầm. Trước khi gọi, mở ticket và chuẩn bị 3 ý: cái gì, cần gì, đến khi nào. Lấy số điện thoại subsidiary chỉ từ trang CoE trên Confluence Samsung.
| Bước | Nói gì | Câu mẫu |
|---|---|---|
| 1. Chào, giới thiệu | Tên, team, lý do | "Hi [Name], this is [Your name] from the Samsung Ops CoE. I am calling about ticket DEMO-1234." |
| 2. Sự kiện | Status trong 1–2 câu | "The promotion for MY is set up, but the end date is missing." |
| 3. Yêu cầu | Cần gì, đến khi nào | "Could you confirm the end date before 16:00 SGT?" |
| 4. Xác nhận | Nhắc lại điều đã thống nhất | "So, to confirm: the end date is 31 December, 23:59 local time." |
| 5. Kết | Bước kế, cảm ơn | "I will update the ticket now. Thank you for your time." |
Khi nghe không rõ: "Sorry, could you repeat that, please?"; "Just to make sure I understand, you mean...?"; "Could you please put that in the ticket as well?". Câu cuối quan trọng nhất: thỏa thuận không nằm trên ticket thì không tồn tại với RHQ.
**Nghe bản ghi KT/handover:** người trình bày nói nhanh và transcript nhiễu. Nghe ba loại câu: rule ("cái này đã thống nhất với RHQ"), decision hoặc lời hứa ("tôi sẽ bổ sung thông tin sau") và câu hỏi còn mở. Ghi timestamp cạnh mỗi câu.

### 2. Tóm tắt cuộc gọi hoặc bản ghi
Mỗi cuộc gọi có call summary trên ticket trong 15':
```
Call summary ([time] ICT, [caller] with [role at subsidiary or RHQ]):
- Agreed: [decision].
- Open: [item still open], owner [name], by [time].
- Next update: [time] ICT ([time] local).
```
Trong họp với RHQ nói ngắn: kết quả, nguyên nhân, hành động, người, ngày. Lấy số liệu từ Samsung Jira, không ước lượng. Mọi action item ghi vào minutes trên Confluence Samsung.
**Ví dụ: Handover P1, phút 34:20–44:36.** Tóm tắt tốt đoạn này:
- **Decision (34:20):** với Shop Merchandising, 5 status tính vào SLA: APPROVED-ES, STG SETUP, PRD SETUP, QA REVIEW, ON HOLD COE. Các status khác bị loại. Đã thống nhất với RHQ; thay đổi bàn với RHQ PIC.
- **Action (36:00):** người trình bày sẽ thêm tên country project vào slide Shop Merchandising. Owner: người trình bày (vendor hiện tại). Ngày: không nêu, nên là open point.
- **Rule (36:55):** ticket COEC phải là issue type Maintenance Request vì filter chỉ lấy loại này; priority P0–P4. Component và sub-category thường sai và đội sửa để báo cáo.
- **Rule (39:30):** vấn đề lặp lại thì link ticket trước; subsidiary không link thì đội tìm trong lịch sử Confluence hay Jira.
- **Decision (40:30):** status COEC: SUBSIDIARY khi cần thông tin, SYSTEM SUPPORT cho L2/L3 (đổi code, hotfix, RCA), ON HOLD ES khi project khác phải cấp quyền (VD AUTEU), ON HOLD RHQ cho duyệt RHQ. NEW, ASSIGNED, IN REVIEW, IN PROGRESS, QA REVIEW tính vào SLA.
Lưu ý bản tóm tắt không chứa: từ đệm của người trình bày, và bất cứ thứ gì bạn đoán. Câu nào không rõ thì viết thành open question kèm timestamp.
> Slide Handover P1 tính APPROVED-ES (Shop Merchandising) và NEW (COEC) vào SLA. CM-13 chỉ tính Resolution từ STG SETUP và ASSIGNED; APPROVED-ES và NEW đo initial response. Khi tóm tắt, ghi điều người trình bày nói và thêm "CM-13 differs" như open point; khi làm ticket, theo CM-13.

### 3. Câu hỏi scope và từ chối kèm hướng đi
CoE chỉ làm service trong catalogue và trong quyền có. Bạn không tự quyết scope: Shift Leader hoặc Lead xác nhận trước, scope do COE Lead quyết cùng RHQ. Rồi dùng Template 6 và luôn đưa phương án thay:
```
Hello [Name],
Thank you for your request. Unfortunately, [request] is outside the scope
of the Ops CoE service, so we are not able to do it.
This is usually handled by [team]. We suggest raising it with [team / channel].
If you believe it should be in scope, please let us know and we will ask
RHQ to confirm.
```
**Ca thường (CM-08 Scenario 5):** requester nhờ CoE sửa layout trang checkout vì "chỉ 5 phút". Không làm, dù về kỹ thuật làm được. Báo Shift Leader, dùng Template 6 sau khi Lead xác nhận. Trong cuộc gọi: "I would like to help, but this change is outside what the CoE is authorised to do on the platform. I have raised it with our COE Lead, who will confirm with RHQ by [date]." Với Tech, kể cả việc trong scope trên production vẫn cần PC ticket đã duyệt, dù chỉ 5 giây.
KT Samsung (21/10/2026): *"Keep current practices during the transition. Agree any process change with RHQ first. Do not delete or overwrite working content without confirmation."*

### 4. Đổi priority và pushback
Reporter hầu như luôn raise High. Sub-Lead đánh giá lại priority trước khi giao vì nó điều khiển SLA và báo cáo; subsidiary có thể đổi lại sau, khi đó sửa tay. Market Owner không đổi priority đã phân loại: nhờ Shift Leader sửa và ghi lý do lên ticket. Không bao giờ hạ priority để tránh breach.
Luật Merch (RFP 3.3): High chỉ khi ảnh hưởng an ninh dữ liệu hoặc mất doanh thu >10,000 USD (4 giờ, bất kể giờ làm việc); Medium cho một promotion và request phức tạp (16 giờ); Low cho >2 promotion, product setup, giá, CMS tương tự (24 giờ).
**Ví dụ: ticket Low "trong 2 giờ".** Subsidiary gọi: "This product setup is urgent, please finish it in 2 hours." Đây là Low (24 giờ). Hướng đi: (1) ghi nhận impact, không tranh cãi; hỏi lý do: có giờ go-live không? (2) Không tự đổi priority và không hứa 2 giờ — MR-03: không hứa gì vượt SLA và process; (3) có giờ go-live thật thì nó đặt due date nội bộ: sớm hơn của SLA deadline và go-live − thời gian kiểm; báo Shift Leader, người có thể sắp lại queue; (4) go-live quá gần cho QA thì áp rule urgent request (comment last-minute, kiểm soát tối thiểu, label LastMinRequest); (5) xác nhận điều đã thống nhất và viết call summary.
Câu mẫu: "I understand this is urgent for your launch. The ticket stays Low, but we plan it against your go-live at [time] local. I will confirm the expected completion with our Shift Leader and update this ticket by [time] ICT ([time] local)."
> Deck Handover P1 hiển thị SLA Merch theo ngày làm việc (High 1, Medium 2, Low 3). CM-13 trích RFP 3.3 là 4, 16 và 24 giờ. Theo CM-13 trong mọi trao đổi với subsidiary. **Under review (D6):** cơ sở SLA (giờ RFP hay guideline ngày làm việc của RHQ) chưa chốt; tạm theo giờ RFP (mục tiêu ngắn hơn).
Ghi chú từ Handover Day 5 (29/10, Ngavt "Tip manage ticket on the Jira"): với yêu cầu bạn không chắc làm được: xin ticket tham chiếu, kiểm setup cũ, hỏi senior, không bao giờ trả lời "cannot" trước. Jira là bản ghi duy nhất: green light qua điện thoại hay chat chỉ tính khi đã nằm trên ticket (Handover P1 48:55–52:50).

## Quiz (đáp án)
1 Trong cuộc gọi requester AU nói promotion nên kết thúc "on the 31st at midnight"; trước khi đóng bạn nói → **B: "So, to confirm: the promotion ends on 31 December at 23:59 Sydney time. Could you please put that in the ticket as well?"** 2 Kết thúc cuộc gọi với requester SG lúc 10:20 ICT; call summary viết khi nào, ở đâu → **C: trên ticket, trước 10:35 ICT, với Agreed, Open (owner, hạn) và Next update**. 3 Trong bản ghi Handover P1 người trình bày nói "I will add the country project names to the slide"; ghi vào summary thế nào → **A: action item: owner là người trình bày, ngày không nêu nên là open point**. 4 Subsidiary khăng khăng CoE sửa layout trang checkout "trong 5 phút"; bạn làm gì đầu tiên → **C: báo Shift Leader hoặc Lead; sau khi Lead xác nhận ngoài scope mới gửi Template 6 kèm team/kênh thay thế**. 5 Ticket product setup là Low, subsidiary nói gấp muốn xong trong 2 giờ, không có giờ go-live và không mất doanh thu → **B: giữ Low; không hứa 2 giờ; hỏi có giờ go-live không và xác nhận kế hoạch với Shift Leader; update ticket**. 6 Họp sync tuần, RHQ hỏi Market Owner CoE có nhận loại request mới từ tuần sau không; Market Owner không có thẩm quyền cam kết → **C: "I will confirm with our COE Lead and come back to you by [date]."** 7 Requester đổi priority ticket 3 promotion về High; Market Owner làm gì → **B: nhờ Shift Leader sửa priority và ghi lý do lên ticket**.

## Practice
- **PR-GP5.2-1. Tóm tắt Handover P1 phút 34–44** (15', giấy; facilitator phát bản ghi 34:20–44:36): viết tóm tắt ba mục — Decisions, Action items (owner, ngày), Open questions (kèm timestamp). Không chép transcript. **Pass:** có ít nhất: 5 status Shop Merchandising tính SLA và luật thay đổi bàn với RHQ PIC; COEC issue type Maintenance Request và priority P0–P4; nghĩa của SUBSIDIARY, SYSTEM SUPPORT, ON HOLD ES, ON HOLD RHQ; action của người trình bày thêm tên country project (không nêu ngày). Ghi chú việc đếm APPROVED-ES và NEW khác CM-13. Không bịa gì. Không có access: facilitator phát bản ghi; dùng mục 2.12–3.4 in sẵn của notes Handover P1.
- **PR-GP5.2-2. Role-play: ticket Low "trong 2 giờ"** (20': 5' chuẩn bị, 5' gọi, 5' summary, 5' feedback; theo cặp, trainer đóng subsidiary): subsidiary gọi về ticket Low product setup và muốn xong trong 2 giờ. Sau đó họ ép: "Then make it High." Chạy cuộc gọi 5 bước, giữ rule, thống nhất kế hoạch và viết call summary. **Pass:** priority vẫn Low và học viên không tự đổi; không hứa 2 giờ; học viên hỏi giờ go-live, nêu Shift Leader là người xác nhận kế hoạch, và kết thúc bằng câu xác nhận; call summary trên giấy trong 15' với Agreed, Open (owner, hạn) và Next update theo ICT và giờ địa phương; rubric T2 ≥2 mỗi tiêu chí cho summary. Không cần truy cập hệ thống.
