# MER-1.1 Merchandising Operating Manual: roles, shifts, flow of work

> Nguồn: page 2482995563 · 65 phút (Study 30' · Demo 5' · Quiz 10' · Practice 20') · Facilitator: Merch Lead (hoặc Deputy) · Tài liệu chính: MR-01, MR-02, MR-03 · Cần xong G1.1, G2.4, G2.7; PR-MER-1.1-1/2 trên giấy; PR-MER-1.1-3 cần Backoffice staging view-only (hoặc screenshot Base Store của facilitator). Facilitator giao mỗi learner 1 market cho market card.

## Mục tiêu
Phân biệt việc hằng ngày của Team Member, Market Owner, Shift Leader, Merch Lead; nêu Shift Leader tự quyết gì, khi nào phải gọi Merch Lead, và 7 điều Market Owner không làm; tra backup PIC, Tech team, ca VN phụ trách go-live của từng market; sắp thứ tự queue một market theo 9 luật MR-03; dựng khung market card.

## Thuật ngữ
**Span** (nhóm market mà một Sub-Lead là backup PIC; VD Sub-Lead 3 giữ MY & SG); **Leadership on duty** (vai Shift Leader trực hotline COE, trả lời RHQ/market trong 15'); **SLA Controller** (giữ status Jira khớp công việc thật để clock chạy đúng); **Queue** (danh sách ticket mở của một market, Market Owner quyết thứ tự); **Internal due date** (= sớm hơn giữa SLA deadline và go-live − thời gian cần check; VD SLA 22:00, go-live 20:00, QA cần 3h → 17:00); **Morning pickup** (Market Owner nhận ticket mở trong 07:45–08:30, mọi ticket có owner mới trước 08:30); **Weekly sync** (họp 15' hằng tuần Market Owner–subsidiary, ghi chú tiếng Anh trên Confluence Samsung); **Market rules page** (trang luật của một market/kênh trên Confluence Samsung; 12 trang, template 17 section).

## Nội dung
### 1. Team, 3 thước đo, ai làm gì
- **3 thước đo:** *Correct* (QA FPY, escaped defect), *On time* (SLA initial response & resolution), *Safe* (loss register, incident, self-audit). VD promotion đúng giá nhưng live trễ 1h → đạt Correct, trượt On time.
- Team 29 chỗ: 1 Merch Lead, 5 Sub-Lead kiêm Shift Leader (một người là Deputy Lead), 8 Market Owner, 15 Team Member, + 4 bench. **Sprint 1 chỉ nhận R1/R2; R3 (price, promotion, coupon) bắt đầu Sprint 2 (09/11).**
- **Team Member**: làm ticket Shift Leader giao, ca N/D/E; mỗi ca Shift Leader chỉ định 1 TM trực intake (xem APPROVED-ES, phân loại ticket mới — CM-04 §3.3; học ở MER-1.4). **Market Owner**: giữ queue 1 market, ca D 08–16 T2–T6, ~90% thời gian là ticket. **Shift Leader**: điều phối ca và duyệt mọi Merch change. **Merch Lead**: có mặt 08–17 T2–T6, duyệt E4; ngoài giờ on-call 3/4 tuần (tuần 4 là Deputy).

### 2. Shift Leader: 3 vai và giới hạn quyền
- 3 vai: **Leadership on duty**, **SLA Controller**, **Approver** (duyệt mọi Merch change trước production; *không* duyệt thay đổi Tech).
- **Tự quyết:** giao lại ticket, chuyển người giữa các market, kéo dài ca, gọi bench, gọi Tech/QA on-call, duyệt R1–R3 dưới ngưỡng E4, publish theo luật 23:59 khi Knox đã duyệt.
- **Phải gọi Merch Lead khi:** ticket chạm 85% SLA; có ca E4; có Merch incident; quyết định vượt quyền ca; ticket R3/E4 khẩn không kịp control tối thiểu; Knox chưa duyệt sát giờ publish. Gọi điện chứ không chỉ nhắn; 2 cuộc/10' không ai nghe → gọi người kế tiếp.

### 3. Market Owner: sở hữu gì, không làm gì
- Sở hữu: queue market, ticket chờ subsidiary, backlog lúc 08:00, weekly sync, CSAT, market rules page, market calendar.
- **7 điều MO không làm:** (1) duyệt change (MO là Doer); (2) tự chọn Knox approval path; (3) tự đổi priority (hỏi Shift Leader); (4) làm đầu mối ngoài giờ; (5) trả lời khiếu nại chính thức (việc COE Lead); (6) hứa hơn SLA hay bàn bồi thường; (7) nhận request qua kênh cá nhân (VD subsidiary nhắn riêng xin sửa giá gấp → yêu cầu tạo ticket).
- Market rules pages: 8 market + EPP, SMB, O2O, 3PD (3PD do 3PD PIC ở Tech giữ); chỉ nằm trên Confluence Samsung, không chứa password/PII. Trang mâu thuẫn runbook → theo runbook, sửa trang trong 3 ngày làm việc.

### 4. Market PIC, backup, giờ go-live

| Market | Backup PIC (span) | Tech team | Go-live 00:00 local → giờ VN (tháng 10–3) | Ca VN |
|---|---|---|---|---|
| VN | Sub-Lead 1 | Team A | 00:00 | N |
| TH, ID | Sub-Lead 2 | Team A | 00:00 | N |
| MY, SG | Sub-Lead 3 | Team B | 23:00 hôm trước | E |
| PH, nhóm kênh EPP/SMB/O2O | Sub-Lead 4 (backup nhóm kênh: Merch Lead) | Team B | 23:00 hôm trước | E |
| AU | Sub-Lead 5 | Team B | 20:00 hôm trước | E |
| NZ | Sub-Lead 5 | Team A | 18:00 hôm trước | E |

Go-live 00:00 local ở NZ, AU, SG, MY, PH rơi vào ca chiều (E) giờ VN; ở VN, TH, ID rơi đúng giờ bàn giao 00:00 và thuộc ca N.

### 5. Sắp queue — 9 luật MR-03
1) Incident và High. 2) Ticket subsidiary vừa trả lời → đưa về STG SETUP ngay. 3) Ticket gần/quá 70%, kể cả ON HOLD COE chờ Tech. 4) Ticket cần hỏi subsidiary → hỏi đầu ca, một câu gộp, xin luôn asset. 5) Ticket go-live hôm nay cần QA → theo giờ go-live. 6) Còn lại → theo internal due date. 7) Cùng due date → R3 trước R2 trước R1. 8) Việc R1 <15' → làm khi chờ việc khác. 9) Thấy không kịp → báo Shift Leader trước khi ticket chạm 50%. *Vì sao hỏi trước:* gửi câu hỏi mất vài phút nhưng subsidiary cần hàng giờ để trả lời — trong ví dụ queue VN (MR-03 §2.4) ticket cần hỏi (5107, 5105) làm trước ticket có deadline sớm hơn (5101).

### 6. Ranh giới với Tech & weekly sync
Việc của Tech (COEC), không phải Merch: EPP access list, whitelist O2O store/agent, Samsung Rewards, Referral, ImpEx, lỗi order, payment mode, delivery mode cấp site, NERP/FI config. 3PD do 3PD PIC (Tech) xử lý; QA chỉ check việc Merch. Weekly sync 15': 2' mở đầu; 5' ticket mở, ON HOLD SUBS, REVIEW SETUP; 4' lịch tuần sau; 2' feedback/CSAT/số urgent; 2' action. **Đừng hứa "2–3 ngày làm việc" như deadline cố định — chỉ là khuyến nghị.**

### Điểm đáng nhớ từ KT
Merch gánh ~60–70% workload, là tuyến đầu với subsidiary. Review requirement trước khi làm, không giả định (nước, SKU, loại change, cơ chế, approval, phụ thuộc). Jira là single source of truth; chat/điện thoại/WhatsApp không tính. ON HOLD chỉ khi hợp lệ (có câu hỏi thật và assign subsidiary). PENDING LAUNCH ngoài SLA, luôn comment lý do, và QA lại production mỗi wave. Mỗi subsidiary nhiều PIC với style khác nhau → ghi lại trên market rules page.

## Quiz (đáp án)
1 Promotion SG live 00:00 giờ SG → **23:00 hôm trước giờ VN, ca E**. 2 MO không được tự làm → **chọn Knox approval path khi brief im lặng**. 3 Promotion 6 market ~4.000 USD → **phải gọi Merch Lead: >5 market là E4**. 4 Ba ticket A (Low R3, 18:00), B (Medium R3 thiếu time zone, 00:20), C (Low R1, 22:00) → **B, A, C** (gửi câu hỏi cho B trước). 5 Tech on-call xin Shift Leader Merch duyệt fix Back Office cho P0 → **từ chối; Tech cần PC duyệt**. 6 Ticket VNME chỉ xin thêm email domain vào EPP access list → **move cả ticket sang COEC** (toàn bộ là việc Tech).

## Practice
- **PR-MER-1.1-1** (giấy, 5'): bảng giờ go-live 00:00 local ngày 27/11/2026 quy ra giờ VN cho 8 market + ca VN + Tech team + span Sub-Lead; làm lại cho 15/06/2027 khi AU/NZ không dùng DST (AU 21:00, NZ 19:00 hôm trước; Sydney UTC+10, NZ UTC+12).
- **PR-MER-1.1-2** (giấy, 7'): xếp thứ tự 9 ticket DEMO-5101…5109 của MR-03 §2.4 (che lời giải): ghi internal due date, thứ tự, luật áp dụng; với ticket cần hỏi, viết pickup comment "Picked up by [VN Market Owner] at 08:10 ICT. Next action…". Pass: khớp lời giải (5107, 5105 hỏi trước 5101), mỗi dòng có số luật.
- **PR-MER-1.1-3** (giấy + Backoffice view-only, 8'): market card 8 section (Identity; Payment; Services; Warehouse & delivery; Channels; Other; 3 lỗi cấu hình thường gặp; KB pages) — điền 3 section: Identity (site code, subsidiary, cluster SMS/SMA — AU là SMA duy nhất —, lệch giờ, backup PIC, Tech team), Payment (3 payment mode + 2 delivery mode thật từ Base Store, không Save; PH/ID/TH còn Site Payment Config, EPP/SMB multistore có list riêng), KB pages (≥2 link). Pass: đủ 8 section; 3 section đầu đúng; tên mode lấy từ staging chứ không từ textbook; ghi chênh lệch giữa textbook và hệ thống nếu có.
