# TEC-1.3 Level 1 shift and healthcheck

> Nguồn: page 2483224683 · 60 phút (Study 25' · Demo 10' · Quiz 5' · Practice 20') · Lecture + mô phỏng một ca trên giấy, demo healthcheck trên HAC staging; facilitator: Tech Sub-Lead Team A · Tài liệu chính: TC-02. Cần xong TEC-1.2, G2.4, G5.2; HAC staging cho bài healthcheck (không có thì dùng screenshot facilitator); Confluence để dựng trang handover (không có thì giấy).

## Mục tiêu
Theo các mốc giờ ca sáng/chiều; quét overnight queue đúng 6 thứ tự ưu tiên; chạy một vòng healthcheck chỉ đọc và mở COEC cho mỗi phát hiện; quyết định đúng thời điểm bàn giao cho Level 2 và viết comment 4 phần.

## Thuật ngữ
**T4, T11** (T4 = ca sớm 04:00–12:00; T11 = ca chiều 11:00–19:00); **Overnight queue** (ticket dồn từ 19:00 hôm trước tới 04:00); **Healthcheck HC-01…HC-08** (vòng check chỉ đọc tìm stuck order, cronjob lỗi, trang hỏng trước khi khách báo); **Healthcheck log** (trang `HC-yyyy-mm-dd-TEC`, không ghi order number); **Max self-handling** (thời gian tối đa Level 1 tự xử lý từ ASSIGNED trước khi giao Level 2); **Duty phone**; **Part A/B/C/D** (4 phần biên bản bàn giao Tech: A 04:00, B 08:00, C 11:00, D 19:00); **COE Watch: Tech** (dashboard Jira Tech với filter `COE-F..`, VD COE-F01T = COEC ở NEW).

## Nội dung
### 1. Nhịp một ngày Level 1
Level 1: 2 người/ca (1 Team A, 1 Team B), Thứ Hai–Thứ Bảy. Ca sớm bắt đầu 04:00 để mở cửa sổ cho NZ (09:00 NZ = 03:00 Hà Nội mùa hè) và AU (09:00 AU = 05:00 Hà Nội).

| Giờ | Ca | Việc |
|---|---|---|
| 03:45 | Sớm | Vào secure area; đọc on-call log, section 9 handoff Merch, part D hôm trước |
| 04:00–04:15 | Sớm | Nhận bàn giao từ on-call layer 1 và Shift Leader đêm; gọi thử duty phone; ký part A |
| 04:15–05:15 | Sớm | Quét COEC NEW và overnight queue theo 6 bước |
| 05:15–06:00 | Sớm | Healthcheck sáng đủ 8 mục, NZ và AU trước |
| 06:00 | Sớm | Điểm kiểm: không còn ticket NEW tạo trước 04:00 |
| 08:00–08:15 | Sớm | Bàn giao cho Level 2 ở stand-up (part B), ≤30s/ticket |
| 10:45 | Chiều | Đến |
| 11:00–12:00 | Cả hai | Bàn giao trực tiếp (part C) |
| 13:30–14:00 | Chiều | Healthcheck giữa ngày: HC-01, 02, 05, 06 |
| 15:00–15:30 | Chiều | Cập nhật BVT nếu được giao; hạn 15:30 ICT (16:30 SGT) |
| 18:00 | Chiều | Level 2 về; ca chiều là người Tech duy nhất |
| 18:15–18:40 | Chiều | Healthcheck tối như giữa ngày; từ 18:30 rà ticket mở, cập nhật status & deadline (CM-04 §6.4) |
| 18:45 | Chiều | COEC NEW tạo trước giờ này phải ASSIGNED trước 19:00 |
| 18:45–18:55 | Chiều | Viết part D (8 mục của handoff note CM-04 template 6.5.2); gửi on-call layer 1, cc Merch Shift Leader, rồi gọi layer 1 đọc |
| 19:00 | Chiều | Chuyển duty phone, gọi thử; on-call ghi "Received by" |

### 2. Quét overnight queue — không đổi thứ tự
1) P0/P1 còn ở NEW → gọi Sub-Lead và lead đang giữ on-call layer 1 ngay. 2) PC ticket duyệt qua đêm → ticket đã về IN PROGRESS, clock đang chạy. 3) P2–P4 theo priority cao trước; cùng priority thì cũ trước. 4) Ticket có SLA chạy qua đêm: chạm 70% thì báo Sub-Lead. 5) ON HOLD SUBSIDIARY mà Assignee vẫn là người CoE (filter COE-F02). 6) COEC chặn Merch ticket đang ở ON HOLD COE.
Mục tiêu: mọi ticket tạo trước 04:00 có Assignee trước 06:00; >5 ticket còn NEW sau 05:15 thì báo Sub-Lead. 19:00–04:00 on-call layer 1 sở hữu COEC NEW và quét mỗi 5' (TEC-1.4) nên khi bạn đến phần lớn đã ASSIGNED; việc không gấp được giao qua on-call log.

### 3. Bàn giao trực tiếp lúc 11:00
Thứ tự theo rủi ro: P0–P2 và incident; ticket ≥70% SLA; PC ticket đang chờ/đã duyệt chưa chạy; COEC chặn Merch; ticket có follow-up chiều nay; phát hiện healthcheck; BVT; việc runbook còn lại. Biên bản trên Confluence Samsung: `HO-yyyy-mm-dd-EARLY-TEC` (A, B, C) và `HO-yyyy-mm-dd-LATE-TEC` (D); dùng Jira Issues macro; không gõ tay order number, tên khách, email, access code. **Trách nhiệm chỉ chuyển khi người nhận ghi "Received by".**

### 4. Healthcheck: chỉ đọc, mỗi phát hiện một COEC
Healthcheck chỉ đọc nên không cần PC. Mỗi phát hiện mở COEC riêng (service TEC-MON-02, mặc định P2); danh sách order chỉ nằm trong Jira. 3 vòng/ngày: sáng đủ 8 mục (45'); giữa ngày & tối HC-01, 02, 05, 06; ngày peak (27/11, 30/11, 12.12, launch flagship) mỗi 2 giờ. Team A: VN, TH, ID, NZ; Team B: SG, MY, PH, AU. VD log: "Round 1 / AU / HC-02 / 7 orders stuck at ORDER_SPLIT over 2h / COEC-xxxx / A2" — không ghi order number.

| Mã | Kiểm gì | Ngưỡng cảnh báo (đề xuất) |
|---|---|---|
| HC-01 | Order đã thanh toán nhưng chưa gửi NERP / bị NERP từ chối | đã trả >2h |
| HC-02 | Order kẹt cùng status trung gian | >2h |
| HC-03 | Lệch payment–order | mọi ca |
| HC-04 | Cancel/return chưa gửi NERP hoặc chưa refund | >24h |
| HC-05 | Cronjob tích hợp lỗi | một export order lỗi là đủ |
| HC-06 | Smoke check storefront (mở site, cart, checkout) | mọi lỗi: cân nhắc P0 |
| HC-07 | Cảnh báo hệ thống từ Samsung | mọi ca |
| HC-08 | Invoice chưa phát hành | >24h |

**Khi nào thành incident:** HC-06 thấy checkout/payment/login lỗi với đa số khách → P0; order hàng loạt không tới NERP hoặc khách bị trừ tiền không có order → P1; HC-02 thấy ≥10 order ở một market hoặc 2 market cùng dấu hiệu → báo Sub-Lead cân nhắc incident; nghi lộ data → P0 bảo mật thông tin, báo Sub-Lead, Tech Lead, DevSecOps ngay (ngoài giờ: hotline SDM), không copy data (CM-10 §3; TEC-3.3).

### 5. Luật Level 1 và bàn giao cho Level 2
Sáu luật: chỉ làm service đã certified theo runbook (không có runbook thì đừng tự tìm lâu); không change production nếu không có PC do Oliver duyệt; **không chạy ImpEx/Groovy trên production, kể cả file dùng lại**; không liên hệ SDS India, không tạo Maintenance Request, không đụng middleware 3PD; quyết định giao Level 2 trước 50% SLA, muộn nhất 70%; sau khi giao vẫn theo dõi và nhắc.
**Max self-handling (từ ASSIGNED):** P0 không tự xử lý; P1 60'; P2 4h; P3 & P4 8h (VD P2 ASSIGNED 09:00, 13:00 chưa có hướng rõ thì giao). Cách giao: đổi Assignee, **giữ status (clock không dừng)**; comment 4 phần: Checked, Reason, Request, SLA left (kèm giờ chạm 70%); chuẩn bị phần 1–3 evidence pack; post kênh `coe-tech`; P0/P1 hoặc ngoài giờ Level 2 thì phải gọi điện; bên nhận xác nhận trong 15'.
3 lỗi Level 1 hay làm hỏng clock: chờ PC mà quên chuyển ON HOLD HQ; để ticket ở ON HOLD SUBSIDIARY sau khi subsidiary đã trả lời; chuyển ON HOLD SUBSIDIARY chỉ để dừng clock. Nhịp dashboard COE Watch: Tech: COE-F01T (COEC NEW), COE-F04T (P0/P1 mở) mỗi 5'; filter SLA 70/85/95% (COE-F06T/F07T/F08T) mỗi 15'; COE-F02, F03 (không owner CoE) mỗi 30'; COE-F12 (PC pending) mỗi 2h; COE-F11 (SYSTEM SUPPORT đến hạn follow-up) hằng ngày 08:00.

## Quiz (đáp án)
1 Lúc 04:20 có P3 tạo 21:00, P1 còn NEW, PC duyệt lúc 02:00, P2 tạo 23:30 → **P1 NEW, PC đã duyệt, P2, P3**. 2 Vòng healthcheck sáng có cần PC? → **không, chỉ đọc; mỗi phát hiện mở COEC**. 3 P2 ASSIGNED 09:00, chưa có hướng → giao Level 2 muộn nhất **13:00**. 4 Giao ticket cho Level 2 thì status → **giữ nguyên, đổi Assignee, comment 4 phần**. 5 18:20 thấy P3 COEC mới ở NEW → **ca chiều chuyển ASSIGNED trước 19:00**. 6 05:30 HC-06 thấy checkout AU lỗi với đa số khách → **P0, xử lý như incident**.

## Practice
- **PR-TEC-1.3-1** (HAC staging, 12'): mở HAC staging, **kiểm URL chứa `samsungel3-s2`** (nếu không thì đóng tab; môi trường ở trang Hybris Login Instructions); Console › FlexibleSearch; chạy query dưới đây (thay `vn` bằng base store của market team bạn; AU ở cluster SMA nên Team B chọn SG, MY hoặc PH); kỳ vọng bảng 3 cột (order code, status, order date) cũ nhất trước — staging có thể trả 0 dòng (vẫn hợp lệ, ghi "0"); đếm order có order date >2h trước, viết một dòng log (Round / Market / HC / Result / Ticket / Run by, không order number) và nháp comment A4. Pass: query chạy (hoặc đọc đúng screenshot); log không có order number hay data khách; nêu mặc định P2 và khi nào thành incident.
```sql
SELECT {o.code}, {os.code}, {o.date}
FROM {Order AS o
  JOIN OrderStatus AS os ON {os.pk} = {o.status}
  JOIN BaseStore AS bs ON {bs.pk} = {o.store}}
WHERE {o.originalVersion} IS NULL
  AND {bs.uid} = 'vn'
  AND {os.code} IN ('CREATED', 'WAITING_FOR_SEND_FINANCIAL', 'ORDER_SPLIT')
ORDER BY {o.date} ASC
```
- **PR-TEC-1.3-2** (8'): dựng trang `HO-yyyy-mm-dd-EARLY-TEC` đủ part A, B, C theo TC-02 §7.4–7.6, điền 4 ticket DEMO mô phỏng theo đúng thứ tự rủi ro: P2 ở 72% SLA, PC đã duyệt chưa chạy, COEC chặn Merch ticket, phát hiện healthcheck. Pass: đủ 3 phần, đúng thứ tự, có "Received by", không order number/tên khách.
