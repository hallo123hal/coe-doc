# TEC-1.1 Tech Operating Manual

> Nguồn: page 2483224663 · 60 phút (Study 25' · Demo 10' · Quiz 10' · Practice 15') · Tự học rồi thảo luận nhóm; facilitator: Tech Lead/Sub-Lead · Tài liệu chính: TC-01. Cần xong General foundation (nhất là G2.1–G2.3); chỉ cần đọc Confluence BiPlus. Hỏi Sub-Lead mình thuộc Team A hay B và seat ID (chưa xếp thì làm như Team A).

## Mục tiêu
Liệt kê 10 nhóm việc Tech hằng ngày và việc không phải của Tech (kèm nơi chuyển); phân biệt các nghĩa của chữ "L"; vẽ sơ đồ Tech Team (9 seat, Team A/B, PIC 3PD, Technical Advisor); nêu điều kiện cần trước khi có production access (CM-11).

## Thuật ngữ
**Billable seat** (vị trí tính phí trong hợp đồng với RHQ; Tech có 9 seat TEC-01…TEC-09); **Bench** (người dự phòng BiPlus trả lương, ngoài 9 seat); **Team A / Team B** (chia theo market: A = VN, TH, ID, NZ; B = SG, MY, PH, AU); **PIC 3PD** (một Team Member làm 100% 3PD — luồng data giữa Hybris và middleware marketplace); **Technical Advisor** (chuyên gia hỗ trợ cả team, không nhận ticket, không on-call); **Double-hatting** (làm dự án khác song song — không được phép); **Tech service code** `TEC-XXX-NN` (VD `TEC-ORD-02` hủy order; runbook `RB-TEC-ORD-02`); **Takeover 30/11/2026** và **Hypercare** (theo dõi sát tới 31/12).

## Nội dung
### 1. TC-01 là bản đồ của Tech
Mỗi chương tóm tắt rồi trỏ tới tài liệu chi tiết: TC-02 ca Level 1 (TEC-1.3); TC-03 xử lý COEC và làm việc với SDS India (TEC-1.2); TC-04 on-call (TEC-1.4); TC-05 runbook, PC ticket, ImpEx, Groovy (TEC-2). Mỗi trang TC song ngữ (English ở trên); mâu thuẫn → CM-13 thắng. **Phạm vi:** RFP giao Tech 19 mục việc; CoE chia thành **62 service trong 21 nhóm** (trên tổng 143 service); đề xuất giả định ~700 ticket Tech/tháng, khoảng 2/3 đã có runbook.

### 2. 10 nhóm việc hằng ngày và việc không phải của Tech
10 nhóm: order remediation, stuck order, order healthcheck, invoice, cancel & return, EPP access, report, configuration, defect, payment. VD "thêm domain `@bankx.com.sg` vào EPP SG" là EPP access, làm trên COEC.
**Tech không làm (và chuyển đi đâu):** setup product/price/promotion/coupon/AEM/Shop App CMS → Merch; QA cho Merch → QA Team (QA không QA việc Tech); sửa code & deploy → SDS India hoặc Spoke; tạo user, reset password Back Office → team khác (COEC chờ ở ON HOLD ES); whitelist IP → RHQ (COEC chờ ở ON HOLD HQ); vận hành các marketplace 3PD (Tech chỉ lo luồng data với Hybris); tự duyệt change production của mình (chỉ Oliver Leung duyệt — G2.6). Lỗi hay gặp: "làm nhanh cho xong" việc ngoài scope như reset password BO — hãy chuyển đúng team và đặt đúng waiting status.

### 3. Ba tầng hỗ trợ và các nghĩa của "L"
Luôn viết đầy đủ "Tech Team Level 2" hoặc "SDS India (Samsung L2/L3)", không bao giờ chỉ viết "L2". **Chỉ Tech Team Level 2 (kể cả người on-call) được liên hệ SDS India; Level 1 chỉ thu thập evidence.**

| Thuật ngữ | Nghĩa | Cách viết đúng |
|---|---|---|
| Tech Team Level 1 / Level 2 | Vai trực. L1: 2 người trong khung 04:00–19:00. L2: 08:00–18:00, nhận việc ngoài runbook | "Handed over to Tech Team Level 2 (Team A)" |
| Certification L0–L3 | Cấp certify theo service (CM-11) | "Checker holds L2 for TEC-ORD-02" |
| Samsung L2/L3 | SDS India, nhận việc qua Maintenance Request | "Waiting for SDS India (Samsung L2/L3)" |
| On-call layer 1 / layer 2 | Hai vai on-call ngoài giờ Tech (TEC-1.4). Layer 1 là lead; layer 2 là TM trong tuần Level 2 | "Called on-call layer 1 at 23:05" |
| LB error level L1–L4 | KB 3PD nhóm lỗi Logicbroker theo người sửa (TEC-3.2) | "LB error level L4, needs RHQ" |

### 4. Tổ chức Tech Team
Tech Lead (TEC-01), Sub-Lead A (TEC-02, Team A), Sub-Lead B (TEC-03, Team B); 6 Team Member (TEC-04…09, mỗi team 3 người; một seat là PIC 3PD); 1 bench và Technical Advisor ở ngoài 9 seat; không double-hatting. VD 01:30 Chủ nhật không ai nghe on-call: không gọi Technical Advisor (không on-call) — tiếp tục call tree (TEC-1.4).

### 5. Certification, production access, KPI nội bộ
Certification theo service như G2.1; riêng Tech: **người L1 không thể là checker cho ai, kể cả người L1 khác — checker phải L2 hoặc L3 cho đúng service đó.** Không certification = không production access; sau T4 + T5 và Tech còn phải qua phỏng vấn RHQ (T7); Lead xin mọi access qua approval ticket (CM-11 §1.3–1.4).
KPI nội bộ Tech: không COEC nào không owner >1h (áp cho ticket đã ở status CoE; ticket ở NEW thì đo thời gian tới ASSIGNED theo target initial response: P0 15', P1 30', còn lại 78'); không production change nào thiếu PC; 100% file ImpEx/Groovy có header line, 0 strike; on-call trả lời trong 15' (100%); RCA Critical trong 48h (tối đa 72h); theo dõi thêm số PC ticket, thời gian chờ ở ON HOLD HQ, số ticket SYSTEM SUPPORT quá hạn follow-up.

### Điểm đáng nhớ từ KT
Nhiều việc Tech cần duyệt trước khi chạy (PC kèm attachment) → mọi Tech change production cần PC do Oliver Leung duyệt, **không có duyệt sau** (CM-13 §9). Subsidiary hay nhờ đổi thành viên Knox approval path khi nhân sự vào/ra → xử lý như COEC request, chỉ đổi đúng điều request nêu; CoE không bao giờ chọn Knox path giá/promotion. Daily order monitoring = healthcheck Level 1, mỗi phát hiện mở COEC riêng (TEC-1.3). KB chỉ là tài liệu tham khảo; mâu thuẫn CM thì CM thắng, CM-13 thắng các CM khác.

## Quiz (đáp án)
1 Staff bank X không vào được EPP vì domain chưa có trong list → **việc Tech, COEC theo runbook**. 2 Subsidiary nhờ reset mật khẩu Back Office → **chuyển team sở hữu, COEC sang ON HOLD ES**. 3 Comment "Ticket passed to L2" gây nhầm vì → **người đọc không phân biệt Tech Level 2 với SDS India**. 4 Team B → **SG, MY, PH, AU**. 5 01:30 CN P1, on-call không ai nghe, muốn gọi Technical Advisor → **sai: không on-call, theo call tree**. 6 Dự án BiPlus khác xin Tech part-time → **không (no double-hatting)**. 7 P2 mất owner từ 05:05 đến 06:10 → **vi phạm KPI nội bộ "không COEC không owner >1h"**.

## Practice
- **PR-TEC-1.1-1** (giấy, 8'): vẽ sơ đồ một trang: 3 tầng hỗ trợ, Team A/B và market, PIC 3PD, Technical Advisor, các bên Samsung (RHQ, Oliver Leung, HQ Suwon, SDS India, Spoke, SDSAP) kèm kênh liên hệ; đánh dấu vị trí của bạn; thể hiện rõ chỉ Level 2 liên hệ SDS India và Oliver là approver PC duy nhất.
- **PR-TEC-1.1-2** (7'): 8 request → ai làm và COEC ở status nào: (1) thêm domain vào EPP SG → Tech; (2) đổi giá SKU TH → Merch; (3) reset password BO → team khác, ON HOLD ES; (4) whitelist IP store O2O PH → RHQ, ON HOLD HQ; (5) order MY kẹt ORDER_SPLIT → Tech; (6) checkout lỗi ngay sau code release → P0 incident, Tech Lead/on-call layer 1 là IM, RHQ nhận thông báo đầu trong 30'; cause là code release thì Level 2 mở Maintenance Request, COEC sang SYSTEM SUPPORT, update RHQ mỗi 30'; (7) báo cáo bán hàng hằng tháng → Tech sau khi có PUMI (TEC-3.3); (8) khách Lazada MY đổi địa chỉ → subsidiary nhờ CS agent đổi trên Hybris, CoE không vận hành marketplace (Lead xác nhận).
