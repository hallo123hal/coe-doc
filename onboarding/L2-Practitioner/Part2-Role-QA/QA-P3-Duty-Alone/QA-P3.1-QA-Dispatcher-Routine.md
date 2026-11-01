# QA-P3.1 QA dispatcher routine

> Nguồn: page 2483730337 · 60' (Study 15' · Demo 10' · Quiz 5' · Practice 30') · Facilitator: QA Lead · Capability C3 · Cần xong QA-1.2 (dispatch và quy trình QA check: 4 bước receive, dispatch, test, return và các status QA trên Jira); nên xong QA-P2.1, P2.2 trước (dispatcher dùng luật return và sampling plan). Mang máy tính và bảng múi giờ QA-02 §2.2. Access: Confluence (read); không cần Backoffice staging. Dispatch trên Jira thật cần dispatch certification (đề xuất: L2 trên service promotion và price, ≥2 tuần check live, qua QA-01 case 4 và 5).

## Mục tiêu
Tính QA due time của ticket từ giờ vào, priority, SLA đã dùng và giờ go-live ở bất kỳ market nào trong 8 market; sắp queue QA hỗn hợp theo QA due time và bảng rank, viết comment dispatch A.1; chọn Checker độc lập, có cert, không quá tải và độ sâu check phù hợp; nhận biết dấu hiệu backlog và chạy năm bước backlog theo thứ tự mà không hạ độ sâu check.

## Thuật ngữ
**Dispatcher** (người giao mọi ticket ở QA REVIEW cho một Checker kèm độ sâu check và QA due time trong 15 phút; ca sớm là Sub-Lead 2); **Dispatch certification** (điều kiện đề xuất để dispatch: L2 trên service promotion và price, ≥2 tuần check live, qua QA-01 case 4 và 5); **QA due time** (giờ phải có kết quả QA: sớm nhất của OLA, luật 25% và go-live trừ 1 giờ; VD QA due 11:02 ICT); **Luật 25%** (QA cộng Shift Leader duyệt dùng tối đa 25% thời gian SLA còn lại lúc ticket vào QA REVIEW); **Độ sâu K1, K2, K3, KM** (chuẩn; mở rộng (mẫu gấp đôi, dùng cho E4 và sau SKU FAIL); hai lớp (Black Friday và sự kiện chỉ định); sampling); **Queue rank** (bảng 7 rank dùng khi hai QA due time cách nhau <15 phút: High trước, sampling R2 hằng tuần cuối); **Dấu hiệu backlog S1-S5** (tín hiệu queue vượt năng lực, VD S1: ticket ở QA REVIEW >15 phút không ai check); **QA bench** (một người dự bị đã đào tạo có access, bắt đầu ngay trong ngày và chỉ làm service đã cert; QA Lead quyết gọi).

## Nội dung
### 1. Dispatcher và nhịp 15 phút
Mỗi ca QA có một dispatcher; roster chỉ được công bố khi mọi ca đều có.
| Ca (tạm thời, deck v08Oct) | Dispatcher |
|---|---|
| Sớm 04:00-12:00, T2-T6 | QA Sub-Lead 2 (dispatcher chính) |
| Chiều 11:00-19:00, T2, T3, T5, T6 | QA Sub-Lead 1 (Deputy QA Lead) |
| Chiều thứ Tư; sáng sớm thứ Bảy | QA Team Member 01, 03 hoặc 05 đã cert |
| Chiều thứ Bảy | QA Sub-Lead 1, một mình |
| Ngoài giờ QA, Chủ nhật | QA on-call nhận ticket được gọi |
**Hạn:** 15 phút từ lúc đổi status vào QA REVIEW tới khi Assignee là Checker và có comment A.1. Mở COE-F14 QA queue và refresh ít nhất mỗi 10 phút. Doer có ticket High hoặc go-live trong 4 giờ báo dispatcher trực tiếp.
**Nhịp ca (Phụ lục B.2):** đầu ca đọc handover và mở dashboard COE Watch: QA; lập danh sách QA-again từ COE-F17 và COE-F16; dispatch mọi ticket trong 15 phút kèm comment A.1; theo dõi dấu hiệu S1-S5; ticket ở QA REVIEW chạm 70% thì review với Shift Leader trong 15 phút; 17:00 nhìn trước các ticket sẽ không xong trước hết ca; cuối ca viết handoff note 12 mục.
```none
QA dispatch: checker {name}, depth {normal}, SKU coverage {30 of 45 + 5 must-check SKUs}.
QA due {11:02 ICT}. Go-live {01-Dec-2026 00:00 PHT (30-Nov 23:00 ICT)}.
```
> Thẻ dispatcher CM-11 nói "ưu tiên theo giờ go-live, rồi % SLA đã dùng". QA-02, chủ phương pháp dispatch, sắp theo **QA due time sớm nhất**, đã chứa mốc go-live. Theo QA-02.

### 2. Tính QA due time
Thời gian QA nằm trong SLA của ticket Merch: QA REVIEW tính vào SLA, RHQ không đo SLA QA riêng. Dispatcher ghi giờ **sớm nhất** trong ba điểm:
| Điểm | Cách tính |
|---|---|
| (a) OLA | Giờ vào + 30 phút (High), 2 giờ làm việc (một hai item), 8 giờ làm việc (batch >2 promotion hay file lớn); re-check sau FAIL: High 30 phút, còn lại 1 giờ làm việc (đề xuất CoE Office) |
| (b) Luật 25% | Giờ vào + 25% × SLA còn lại − thời gian duyệt (15 phút High, 30 phút khác) |
| (c) Go-live | Go-live theo giờ Việt Nam − 1 giờ |
Đổi go-live sang ICT trước: NZ +6 giờ (NZDT, khoảng cuối tháng 9 tới đầu tháng 4) hay +5; AU +4 (AEDT, khoảng đầu tháng 10 tới đầu tháng 4) hay +3; SG, MY, PH +1; VN, TH, ID 0. Nên 00:00 địa phương là 18:00 (NZ), 20:00 (AU), 23:00 (SG, MY, PH) tối hôm trước trong tháng 11.
**Ví dụ (QA-02, mô phỏng, tất cả vào lúc 14:00):**
| Ticket | Priority, SLA đã dùng | (a) | (b) | (c) | QA due |
|---|---|---|---|---|---|
| DEMO-3301 NZ | Medium, 9h (còn 7h) | 16:00 | 14:00 + 1h45 − 30 phút = 15:15 | 17:00 | 15:15 |
| DEMO-3302 SG | High, 1h (còn 3h) | 14:30 | 14:00 + 45 phút − 15 phút = 14:30 | 22:00 | 14:30 |
| DEMO-3303 VN | Low, 4h (còn 20h) | 16:00 | 18:30 | 3 ngày sau | 16:00 |
Thứ tự check: 3302, 3301, 3303. Sắp chỉ theo go-live sẽ đặt NZ trước và để ticket High SG vi phạm. Với batch Low, luật 25% gần như luôn chặt hơn OLA 8 giờ, nên luôn tính cả hai.

### 3. Sắp queue
1. Sắp theo **QA due time sớm nhất**, xuyên mọi market, không bao giờ theo từng market.
2. Due time cách nhau <15 phút: dùng bảng rank.
3. Ticket High dispatch và bắt đầu ngay; Checker bỏ việc sau nếu cần.
4. Không để một market lỡ go-live vì đang check ticket muộn hơn của market khác.
| Rank | Việc |
|---|---|
| 1 | High (an ninh dữ liệu, thiệt hại >10,000 USD); thay đổi khắc phục trong incident |
| 2 | Go-live trong 4 giờ tới, bất kỳ market |
| 3 | QA again trên R3 đã live ngoài giờ QA (đầu ca sớm) |
| 4 | Re-check sau khi Doer fix (check 2 trở đi) |
| 5 | Go-live tối nay hoặc trước 12:00 mai |
| 6 | Medium và Low khác; ít SLA còn lại trước |
| 7 | Sampling R2 hằng tuần; chỉ khi rank 1-6 trống |
Label `Urgent_Request` của requester không đổi priority hay QA due time. **17:00 ICT** là ngưỡng nội bộ cho go-live cùng tối: ticket đến muộn hơn nhưng vẫn xong trước go-live − 1 giờ thì check và Shift Leader cảnh báo requester (template A.7). Không thể thì báo Shift Leader trong 15 phút; chỉ là last-minute request nếu subsidiary gửi muộn, không phải nếu CoE chậm.
**Không đạt QA due time:** đưa lên đầu, giao người L2 rảnh nhất, báo Shift Leader trực tiếp, theo cảnh báo SLA (70%: QA Sub-Lead và Shift Leader trong 15 phút; 85%: QA Lead và Merch Lead trong 30 phút; 95%: COE Lead báo RHQ). R3 và R2 có gate **luôn chờ QA**.

### 4. Chọn Checker và độ sâu
**Luật Checker (QA-02 1.4.1):** 1) không phải Doer, không phải người làm internal check hay giúp ticket; 2) có cert QA service tương ứng (L1 trở lên) và quyền production (làm service chưa cert gây incident luôn bị RHQ strike); 3) PASS của Checker L1 được L2, L3 hay Sub-Lead review trước khi trả, ghi người review; 4) E4, SKU launch/flagship, ticket nhiều market: L2 trở lên (đề xuất); 5) re-check: ưu tiên Checker check 1 nếu đang ca; 6) tải: không giao thêm cho người đang giữ việc có due time sớm hơn; tối đa 2 ticket đang check cùng lúc (đề xuất); 7) không dồn mọi ticket cùng giờ go-live cho một người; 8) còn đủ thời gian ca, không thì giao ca sau và ghi handover.
**Độ sâu:** K1 chuẩn cho R3 và R2 có gate; K2 mở rộng (mẫu gấp đôi, mẫu riêng mỗi market) sau SKU FAIL, cho E4 và ticket nhiều market; K3 hai lớp cho Black Friday và sự kiện chỉ định; KM cho service sampling. Ticket nhiều service lấy độ sâu cao nhất.
> Luật 4, 6 và cross-check cả diff file ở E4 là đề xuất CoE Office. QA Lead quyết cùng OLA trước Sprint 2 (09/11).

### 5. Cân bằng tải và backlog
| Dấu hiệu | Nghĩa |
|---|---|
| S1 | Ticket ở QA REVIEW >15 phút không ai check |
| S2 | Tổng thời gian check ước tính > số checker × thời gian còn lại của ca |
| S3 | Ticket không đạt QA due time, nhất là go-live − 1 giờ |
| S4 | Ticket ở QA REVIEW chạm cảnh báo SLA 70% |
| S5 | Nhiều go-live cùng tối đến sau 17:00 |
**Năm bước, theo thứ tự, dừng khi queue về trong QA due time:** 1) dispatcher phân bổ lại trong 15 phút (chuyển việc cho người rảnh, sắp lại, tách batch theo promotion); 2) Sub-Lead cùng check; 3) báo QA Lead quyết có gọi QA bench không (QA Lead có mặt 08:00-17:00 T2-T6 và cũng check); 4) báo Shift Leader ticket nào rủi ro và khi nào có kết quả; 5) đòn bẩy ca: ca sau vào sớm hay tăng ca trong giới hạn, QA Lead quyết.
**Không bao giờ khi backlog:** hạ độ sâu R3 hay R2 có gate; PASS trước khi độ phủ SKU hay bằng chứng đủ; để Doer tự QA việc của mình; chuyển ticket ra khỏi QA REVIEW để thu nhỏ queue; đẩy queue sang ca sau không có handoff note cho từng ticket. Sampling R2 hằng tuần, cập nhật checklist và đào tạo được tạm dừng.
Handover liên quan: Working Session P1 (23/10: giám sát vấn đề Hybris hằng ngày và dashboard chính thức, gồm dashboard QA (ticket cũ hơn 1, 2, 3 ngày còn ở QA; QA REVIEW và PENDING LAUNCH theo thành viên QA)); Day 3 Ticket Management and SLA (27/10: dashboard, cao điểm cuối tháng, PENDING LAUNCH).

## Quiz (đáp án)
1 Ticket High vào QA REVIEW 09:40, SLA đã dùng 1h10, go-live 15:00 ICT; QA due → **B: 10:07** (còn 2h50, 25% ≈ 42 phút − 15 phút = 27 phút). 2 Ticket MY Medium vào 13:00, còn 12h SLA, go-live 00:00 MYT tối nay → **A: 15:00** (OLA 13:00+2h; 25%: 15:30; go-live 23:00 ICT − 1h = 22:00; sớm nhất là 15:00). 3 Hai ticket QA due 10:40 và 10:48: một re-check sau FAIL, một Medium go-live tối nay → **B: re-check (rank 4 trước rank 5)**. 4 Dispatch promotion SG; Team Member 03 sáng nay giúp Doer đọc brief và đang rảnh → **C: giao người đã cert khác: 03 không độc lập**. 5 09:00 ca sớm có 3 checker, còn ~4 giờ, queue ước tính 15 giờ check → **B: phân bổ lại trong 15 phút rồi báo QA Lead (dấu hiệu S2)**. 6 Ticket special price AU (Low, đã dùng 2h) vào QA REVIEW 16:30, go-live 00:00 AEDT tối nay → **A: (a) OLA, 18:30** (go-live 20:00 ICT − 1h = 19:00; luật 25%: 21:30). 7 Ticket ở QA REVIEW chắc chắn lỡ QA due time và sắp vi phạm SLA → **C: đưa lên đầu, giao người L2 rảnh nhất, báo Shift Leader; vẫn chờ QA**.

## Practice
**PR-QA-P3.1-1. Dispatch queue 12 item** (35'; giấy). Thứ Ba tháng 11 mô phỏng, 09:00 ICT. Người trong ca: Sub-Lead 2 (dispatcher, L2 mọi service); Team Member 02 (L2 price và special price, L1 promotion, chưa cert coupon; đã làm check 1 của `DEMO-8107`); Team Member 04 (L2 price, promotion, coupon; đã giúp Doer của `DEMO-8106` đọc brief); QA Lead có mặt từ 08:00. Ca chiều tới 11:00. Mọi giờ trong giờ QA nên giờ làm việc bằng giờ đồng hồ. OLA re-check: 1 giờ. Queue: DEMO-8101 SG promotion Medium vào 08:50, SLA đã dùng 6h, go-live 00:00 SGT tối nay; 8102 NZ special price 18 SKU Medium 08:55, 11h, 00:00 NZDT tối nay; 8103 TH coupon High 08:58, 1h, 12:00 ICT hôm nay; 8104 VN batch 5 promotion Low 08:30, 10h, 2 ngày nữa; 8105 AU special price 24 SKU (một item) Low 08:45, 4h, 00:00 AEDT tối nay; 8106 MY promotion Medium 09:00, 2h, 00:00 MYT tối nay; 8107 PH promotion re-check sau FAIL Medium 08:40, 9h, 00:00 PHT tối nay; 8108 ID special price 12 SKU Low 08:35, 21h, 00:00 WIB tối nay; 8109 SG file giá 620 SKU (E4) Low 09:00, 3h, 00:00 SGT tối nay; 8110 AU sửa giá sai đang live trong incident (MER-INC-01) High 08:59, 40 phút, đã live; 8111 MY coupon Medium 08:45, 1h, Thứ Năm 00:00 MYT; 8112 mẫu R2 hằng tuần, cập nhật stock TH đã live. Tính QA due time từng item, thứ tự dispatch, giao Checker đầu tiên, và nói escalate gì cho ai trước 09:15. **Pass:** QA due: 8108 08:50 (đã qua); 8103 09:28; 8110 09:29; 8107 09:40; 8102 09:40; 8105 10:45; 8111 10:45; 8101 10:50; 8106 11:00; 8104 11:30; 8109 13:45; 8112 không có (rank 7, cuối, có thể tạm dừng). Thứ tự như liệt kê: 8107 trước 8102 (rank 4 trước rank 5) và 8105 trước 8111 (go-live tối nay). Phân công tuân thủ: 8108 giao ngay người L2 và báo Shift Leader trực tiếp (QA due đã qua, ticket >85%); hai ticket High bắt đầu ngay; 8103 không giao Team Member 02 (chưa cert coupon); 8106 không giao Team Member 04 (không độc lập); 8107 giao Team Member 02 có L2 hoặc Sub-Lead review trước PASS; 8109 giao người L2, độ sâu K2, n = 62 cộng mandatory set; không ai giữ quá 2 ticket đang check. Trước 09:15 dispatcher báo QA Lead dấu hiệu S2 và S3, QA Lead cùng check hoặc gọi bench. Due time do tác giả khoá học tính; QA Lead xác nhận trước khi dùng. Không cần access.
