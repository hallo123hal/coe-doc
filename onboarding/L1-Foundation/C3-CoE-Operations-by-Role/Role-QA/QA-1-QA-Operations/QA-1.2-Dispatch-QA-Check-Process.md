# QA-1.2 Dispatch and the QA check process

> Nguồn: page 2483192609 · 90 phút (Study 35' · Demo/thảo luận 15' · Quiz 10' · Practice 30') · Lecture + demo màn hình Jira chỉ đọc + bài tính QA due time theo cặp; facilitator: QA Sub-Lead 2 (dispatcher chính) · Cần xong QA-1.1; ôn G2.3 (SLA clock, alert 50/70/85/95%) và G2.6 (last-minute, label `LastMinRequest`). Chưa có Jira thì làm trên giấy hoặc Excel.

## Mục tiêu
Thực hiện 4 bước QA check (nhận, dispatch, test, trả kết quả); tính QA due time và sắp queue; phân biệt thao tác Jira cho PASS, FAIL, QUESTION, thiếu data; chọn defect category + RC code và viết FAIL comment bằng template A.4.

## Thuật ngữ
**Dispatch** (giao ticket ở QA REVIEW cho một Checker kèm depth và QA due time); **QA due time** (hạn có kết quả = sớm nhất của 3 mốc); **Internal check comment** (comment Doer viết trước khi build, ghi 6 giá trị cần setup); **QUESTION** (kết quả thứ ba: brief không rõ, QA chưa kết luận được); **Defect category** (Price, Promotion logic, Coupon, Content, Partner service, Journey); **RC code** (root cause, VD `RC-TZN`); **Re-check**; **Templates A.1–A.7** (QA-02 Appendix A); **QA on-call** (chỉ nhận ticket High cần QA gate ngoài giờ); **REVIEW SETUP** (hand-back, owner đính kèm evidence QA và xin subsidiary review/duyệt, clock tạm dừng); **PENDING LAUNCH** (chờ go-live từng wave, không tính SLA); **ICT** (UTC+7, mọi giờ trên ticket ghi kèm time zone).

## Nội dung
### 1. Bốn bước của QA check
Dispatcher làm bước 1–2, Checker làm bước 3–4.
- **Bước 1, nhận:** kiểm nhanh 4 mục bắt buộc: brief đã duyệt; file SKU (>100 dòng cần diff file); go-live theo giờ market **và** giờ Việt Nam; bằng chứng setup (R3: internal check comment viết trước khi build + kết quả tự test của Doer). **Data không có trên Samsung Jira ticket thì coi như không tồn tại**, dù Doer nói đã gửi qua chat.
- **Thiếu data = không kiểm.** Một comment liệt kê mọi thứ thiếu (template A.2), ghi `RC-EVD`, chuyển về STG SETUP, Assignee = Doer, đến bàn Doer giải thích trong 10'. Hết ca Doer thì Shift Leader giao người khác.
- **Bước 2, dispatch trong 15':** Checker không phải Doer và không phải người viết internal check; có certificate service đó; Checker L1 cần L2/L3/Sub-Lead review trước khi trả PASS; tối đa 2 ticket đang làm/người; không giao một người hai ticket cùng giờ go-live. Viết comment A.1, VD: `QA dispatch: checker Chi, depth normal, SKU coverage 30 of 45 + 5 must-check SKUs. QA due 11:02 ICT. Go-live 01-Dec-2026 00:00 PHT (30-Nov 23:00 ICT).`
- **Bước 3, test:** thực tế test trên production khi setup chưa live bằng promotion simulator (G3.4, luyện ở QA-2.1). Mỗi ticket có positive, negative, exploratory. **5 điều không bao giờ làm:** đổi setup; publish live hay đổi lịch activation; đặt order thật; dùng account người khác; export data. Thấy promotion đã live sớm hơn giờ → dừng, báo Shift Leader ngay (có thể là incident).
- **Bước 4, trả kết quả:**
  - **PASS:** comment A.3 + file PowerPoint evidence. Ticket **ở lại QA REVIEW**, Assignee = Shift Leader trực để duyệt; Shift Leader duyệt và chuyển PRD SETUP (CM-05 §5.5–5.6). QA không tự chuyển tiếp.
  - **FAIL:** một comment A.4 liệt kê mọi lỗi, mỗi lỗi có category + RC code; label `QA_Returned`; chuyển STG SETUP.
  - **QUESTION:** comment A.5, chuyển STG SETUP. Doer gom câu hỏi gửi subsidiary và chuyển ON HOLD SUBS. Brief thật sự không rõ thì không tính FAIL của Doer.

### Đường đi sau PASS (CM-03 §2.7.1, CM-05 §5.5, 6.2, 6.4)
| Status | Ai chuyển tới | SLA clock | Việc |
|---|---|---|---|
| QA REVIEW | Doer | Chạy | QA kiểm; PASS → A.3 + evidence, giao Shift Leader; FAIL/thiếu data → STG SETUP |
| PRD SETUP | Shift Leader sau duyệt | Chạy | Duyệt trong 15' (High) / 30' (khác); Knox theo đường duyệt trong brief |
| REVIEW SETUP | Owner | **Tạm dừng** | Owner đính kèm evidence QA, xin subsidiary review/duyệt. Không duyệt trước 23:59 ngày trước go-live: CoE vẫn publish đúng giờ và comment (CM-13 §3.6) |
| PENDING LAUNCH | Owner sau khi subsidiary duyệt | Không tính | Mỗi wave: shift publish live, QA kiểm lại trên production (A.6); còn wave thì ở lại PENDING LAUNCH |
| LAUNCH VERIFICATION | Owner/Shift Leader sau wave cuối | Không tính | RHQ đóng hàng loạt, CoE không tự CLOSED |
QA không tự chuyển sang REVIEW SETUP. Chi tiết wave ở QA-3.2.

### 2. QA due time và thứ tự queue
QA due = **sớm nhất** của: (a) **OLA**: giờ vào QA REVIEW + 30' (High), 2 giờ làm việc (Medium/Low 1–2 item), 8 giờ làm việc (batch); (b) **luật 25%**: giờ vào + 25% SLA còn lại − thời gian Shift Leader duyệt (15' High, 30' khác); (c) **go-live (giờ VN) − 1 giờ**.

| Ví dụ (vào QA REVIEW 14:00) | SLA còn | (a) | (b) | (c) | QA due |
|---|---|---|---|---|---|
| DEMO-3301 NZ Medium | 7h | 16:00 | 14:00+1h45−30' = 15:15 | go-live 18:00 → 17:00 | **15:15** |
| DEMO-3302 SG High | 3h | 14:30 | 14:00+45'−15' = 14:30 | 23:00 → 22:00 | **14:30** |
| DEMO-3303 VN Low | 20h | 16:00 | 14:00+5h−30' = 18:30 | 3 ngày nữa | **16:00** |

Sắp queue theo QA due sớm nhất, xuyên mọi market, không theo thứ tự đến. Hai ticket chênh <15' thì ưu tiên: High/incident fix → go-live trong 4h tới → QA again cho R3 live ngoài giờ → re-check sau FAIL. Label `Urgent_Request` của requester **không đổi priority hay QA due**.

### 3. Ticket trễ, R3 và escalation
- **Sau 17:00 ICT** (ngưỡng nội bộ): ticket muộn mà vẫn kiểm xong trước go-live − 1h thì kiểm, Shift Leader báo rủi ro bằng A.7; không đủ thời gian thì báo Shift Leader trong 15'. Last-minute request do Merch owner comment câu RHQ (G2.6). **QA không bao giờ viết "QA PASS" khi chưa kiểm.** Ticket do CoE làm trễ không phải last-minute.
- **R3 luôn chờ QA:** không QA PASS thì không PRD SETUP, không publish, kể cả sắp breach SLA (ngoại lệ duy nhất: last-minute request). Ticket ở QA REVIEW chạm 70% SLA thì Sub-Lead và Shift Leader thêm người trong 15'.
- **Leo thang:** FAIL lần 2 cùng ticket → báo QA Lead ngay, Shift Leader tìm root cause ghi lên ticket (CM-03 §7.3). Doer có 2 FAIL tính trong tháng → QA Sub-Lead báo Shift Leader cùng ngày. Backlog: dispatcher phân lại trong 15' và nhờ QA Lead gọi QA bench. **Không bao giờ** hạ depth, PASS khi chưa đủ mẫu, hay để Doer tự QA.

### 4. Defect category, RC code, re-check
Chọn RC theo thứ tự: category trước; Doer làm đúng brief mà brief sai → `RC-BRF`; làm đúng runbook mà runbook sai → `RC-RUL`; còn lại chọn theo loại lỗi. VD brief ghi hết hạn 23:59 SGT, Doer nhập 23:59 ICT → Promotion logic, `RC-TZN`.

| Code | Dùng khi | Tính vào return của Doer |
|---|---|---|
| `RC-ENT` | Gõ sai, thừa/thiếu số 0, chọn sai giá trị | Có |
| `RC-RUN` | Không theo runbook, bỏ bước, bỏ sanity | Có |
| `RC-TZN` | Sai ngày, giờ, time zone | Có |
| `RC-SCP` | Sai scope: store, market, customer group, category, thiếu SKU | Có |
| `RC-STK` | Sai stacking, promotion conflict | Có |
| `RC-LIM` | Sai usage limit, số lượng, quota | Có |
| `RC-FIL` | Lỗi file bulk: template, cột, định dạng số, thiếu diff file | Có |
| `RC-EVD` | Thiếu evidence, internal check, rollback, data cho QA | Có |
| `RC-KNW`, `RC-COM` | Không hiểu cơ chế; hiểu nhầm do dịch/diễn đạt | Có, kèm coaching |
| `RC-BRF`, `RC-CHG`, `RC-TOL`, `RC-DEP`, `RC-RUL`, `RC-CAP` | Brief sai; subsidiary đổi yêu cầu; lỗi nền tảng; chờ bên khác; runbook sai; vội do quá tải (chỉ là mã phụ) | Không |

Re-check sau FAIL: lỗi field → kiểm các field liên quan và chạy lại test chính trên simulator; lỗi SKU → kiểm mọi SKU sai và lấy mẫu gấp đôi; Doer đổi nhiều hơn danh sách lỗi hoặc ticket trả vì `RC-EVD` → kiểm lại toàn bộ.

## Điểm đáng nhớ từ KT
- QA không có SLA riêng, dùng SLA Merch; QA trễ làm trượt go-live thì team chịu trách nhiệm với subsidiary (BiPlus có OLA nội bộ).
- Evidence là PowerPoint ảnh chụp từng bước, không video lên Jira (giới hạn 15 MB); tạo trên CoE workstation, đính kèm Jira, xóa bản local (CM-13 §6.3, CM-10).
- Slide vendor nói QA chuyển ticket sang Review Setup; **quy tắc CoE**: Shift Leader duyệt → PRD SETUP, rồi owner hand-back ở REVIEW SETUP.
- Không duyệt trước 23:59 hôm trước: CoE publish đúng giờ và comment không nhận phản hồi (CM-13 §3.6). "L.V. Approval" không dạy; gặp thì hỏi Shift Leader.
- Có filter hằng ngày bắt ticket bỏ qua QA: R3 và R2 có gate không qua PRD SETUP nếu thiếu QA PASS; QA Lead re-check 5% PASS mỗi tuần.

## Quiz (đáp án)
1 Vào QA REVIEW 09:00, dispatch muộn nhất → **09:15**. 2 Ai chuyển PRD SETUP sau PASS → **D: Shift Leader sau khi duyệt**. 3 Medium còn 8h SLA, tổng QA + duyệt tối đa → **A: 2 giờ** (25%). 4 High vào 09:40, đã dùng 1h10 của SLA 4h, go-live 15:00 VN → **C: 10:07** (còn 2h50, 25% = 42.5', 09:40 + 42.5' − 15' ≈ 10:07, sớm hơn OLA 10:10 và go-live 14:00). 5 21:00 thứ Ba, Medium cần QA gate (ca tạm Q4/Q11) → **B: chờ ca sớm 04:00, clock chạy** (on-call chỉ nhận High; không dùng ON HOLD SUBS dừng clock). 6 R3 thiếu internal check comment → **C: trả STG SETUP một lần, `RC-EVD`, gặp Doer**. 7 Brief 23:59 SGT, Doer nhập 23:59 ICT → **A: Promotion logic, `RC-TZN`**. 8 Subsidiary gắn `Urgent_Request` cho ticket Low → **D: không đổi priority hay QA due**.

## Practice
- **PR-QA1.2-1** (15', giấy/Excel): 4 ticket vào QA REVIEW 13:20 ICT: (1) MY High, đã dùng 1h/SLA 4h, go-live 23:00; (2) AU Medium còn 10h, go-live 20:00; (3) VN Low batch 3 promotion còn 22h, go-live 3 ngày nữa; (4) PH Medium re-check sau FAIL (OLA re-check 1h), còn 4h, go-live 23:00. Checker: An (L2, rảnh), Binh (L2, viết internal check ticket 2), Chi (L1 promotion), Dung (L2, đang kiểm 2 ticket). Pass: QA due (sai số ≤2'): **(1) 13:50; (2) 15:20; (3) 18:20; (4) 13:50**; thứ tự (1), (4), (2), (3) (High trước khi bằng giờ); không giao ticket 2 cho Binh, không thêm việc cho Dung, nếu giao Chi thì nêu người review; comment A.1 có tên Checker, depth, SKU coverage, QA due, go-live hai time zone.
- **PR-QA1.2-2** (10'): viết **một** comment A.4 cho DEMO-QA-120 (SG, 15% off, 1 lần/khách) với 3 lỗi: end 23:59 ICT thay vì SGT (Promotion logic `RC-TZN`); trống per-customer limit (`RC-LIM`); thiếu 2 SKU biến thể màu (`RC-SCP`). Pass: đủ 3 lỗi với category + code, câu "Re-check scope", giờ đã nói với Doer (ICT), và thao tác Jira: label `QA_Returned`, STG SETUP, Assignee về Doer.
- **PR-QA1.2-3** (5'): comment A.2 cho DEMO-QA-121 (VN, special price 160 SKU) thiếu diff file (>100 dòng) và go-live "01/12 00:00" không time zone. Pass: một comment nêu cả hai thiếu sót, `RC-EVD`, nhờ Doer chuyển lại QA REVIEW sau khi bổ sung.
