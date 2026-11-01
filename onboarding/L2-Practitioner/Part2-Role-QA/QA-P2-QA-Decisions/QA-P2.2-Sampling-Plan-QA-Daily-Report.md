# QA-P2.2 Sampling plan and the QA daily report

> Nguồn: page 2483698715 · 60' (Study 15' · Demo 10' · Quiz 5' · Practice 30') · Facilitator: QA Lead · Capabilities C3, C4 · Cần xong QA-1.3 (checklist, sampling plan, sanity test); biết ma trận QA theo mức rủi ro (R3, R2 có gate, R2 sampling, R1) và luật phủ SKU cơ bản (≤30 SKU kiểm hết). Mang máy tính hoặc spreadsheet trên workstation CoE (không chép data ticket ra spreadsheet cá nhân). Không cần Backoffice staging.

## Mục tiêu
Quyết với từng ticket QA kiểm 100% hay lấy mẫu và tính mẫu SKU kèm mandatory set; chọn mẫu ticket hằng tuần cho một cluster và biết điều gì xảy ra khi một mẫu FAIL; tính K1, K2 và số return cho một ca từ shift log; viết daily QA report từ shift log, giữ mọi số liệu trên hệ thống Samsung và không tên người.

## Thuật ngữ
**Ticket sampling (level 1)** (ticket nào của service "sampling" đi QA REVIEW: 20% mỗi tuần mỗi cluster, tối thiểu 3); **SKU coverage (level 2)** (số SKU của một ticket được kiểm: tất cả tới 30; trên 30 thì 10% làm tròn lên hoặc 30, lấy số lớn hơn, cộng mandatory set); **Mandatory set** (SKU luôn kiểm: SKU launch/flagship, giảm ≥20%, giá cao nhất và thấp nhất, một SKU mỗi category, SKU bị sanity gắn cờ hay nêu trong brief); **Systematic sampling (N, n, k, s)** (chọn phần ngẫu nhiên trên diff file theo bước k = N' ÷ n từ điểm s; cả năm giá trị vào QA record; VD N'=226, n=30, k=7, s=4 → dòng 4, 11, 18…); **Cluster** (nhóm market để đếm mẫu: 1 VN; 2 TH, ID; 3 MY, SG; 4 PH và EPP, SMB, O2O, 3PD; 5 AU, NZ); **Sampling log** (trang Confluence tuần `QA-Sampling log 2026-W46`, ticket, lựa chọn và kết quả theo cluster qua Jira macro); **Tightened inspection** (kiểm chặt hơn sau tín hiệu rủi ro, VD mẫu gấp đôi sau SKU FAIL, hay 100% cluster tới hết tuần sau một mẫu fail); **K1–K13** (13 KPI QA Team: tốc độ K1–K5, chất lượng K6–K9, go-live và tuân thủ K10–K12, yêu cầu gấp K13); **Daily stand-up report** (năm mục QA Lead báo mỗi sáng: queue đầu ca, tuổi ticket cũ nhất, deadline QA trễ hôm qua và vì sao, có gọi bench không, dự báo hôm nay).

## Nội dung
### 1. Kiểm 100% hay lấy mẫu
Hai level: **Level 1** hỏi ticket có đi QA REVIEW không. **Level 2** hỏi bao nhiêu SKU (hay postal code, coupon code, dòng tab add-on) trong ticket được kiểm. QA Sub-Lead 2 sở hữu sampling plan, dispatcher áp dụng, QA Lead kiểm hằng tuần.
| Kịch bản | Level 1: ticket | Level 2: SKU | Ai kiểm |
|---|---|---|---|
| R3 (giá, special price, discount, mọi promotion, coupon, giá trade-in) | 100% | Bảng mục 2 | QA Team |
| R3 đạt E4 (≥10,000 USD, >5 market, hay file giá ≥500 SKU) | 100% | Cột E4; Merch Lead thêm một duyệt | QA Team |
| Gate QA "mandatory" (R2, và R1 như MER-AEM-02, 03) | 100% | Bảng | QA Team |
| Gate QA "sampling" (R2 khác; MER-TXT-01, MER-AEM-04) | 20% mỗi tuần mỗi cluster, tối thiểu 3 | Bảng, nếu được chọn | QA Team; không chọn: Shift Leader |
| "Shift Leader check" (R1 khác) | Không qua QA | – | Shift Leader |
| MER-INC-01 (sửa lỗi live) | 100% sau fix | Mọi SKU bị ảnh hưởng | QA Team |
| Check sau FAIL | 100% | Mẫu gấp đôi | QA Team, ưu tiên Checker đầu |
Thiếu thời gian không bao giờ là lý do kiểm ít SKU hơn bảng. Check nhỏ hơn cần QA Lead đồng ý trong comment ticket kèm lý do.
> CM-07 và MR-06 nói R1 không qua QA Team; catalogue MR-05 và QA-01 cho bốn service R1 một QA gate (MER-AEM-02, 03 mandatory; MER-TXT-01, MER-AEM-04 sampling). QA-01, QA-03 tạm theo catalogue. Runbook sửa đổi đặt gate theo service và variant (bảng ở QA-P1.1 mục 1): chỉ sample MER-PRD-01 V2-V4, MER-DLV-01 V1-V3 và V5, MER-TXT-02, và gửi mọi ticket MER-AEM-04, MER-AEM-01, MER-SAC-01 sang QA. Under review: D9 của L2 gap review.

### 2. Cỡ mẫu SKU và systematic sampling
**Mandatory set** luôn kiểm: SKU launch/flagship; SKU giảm ≥20% từ giá bán hiện tại; giá mới cao nhất và thấp nhất; ít nhất một SKU mỗi category; SKU bị sanity gắn cờ trong diff file hay nêu trong brief/internal check.
**Phần ngẫu nhiên n:** N ≤30 kiểm hết. Trên 30, n = 10% N làm tròn lên hoặc 30, lấy số lớn hơn, chọn ngoài mandatory set. Tổng kiểm = n + mandatory set, tối đa N.
| N | Phần ngẫu nhiên n | Tại E4 | Sau FAIL |
|---|---|---|---|
| 1-30 | Tất cả | Tất cả | Tất cả |
| 31-300 | 30 | Cộng cross-check cả diff file (đề xuất) | 60 |
| 301-499 | 10% làm tròn lên | Như vậy | n gấp đôi |
| 500-999 | 10% | Luôn E4 cho file giá; cross-check cả diff file | n gấp đôi |
**Chọn phần ngẫu nhiên không export data:** đánh dấu dòng mandatory; N' = số dòng còn lại; k = N' ÷ n (phần nguyên); chọn s từ 1 tới k (VD phút hiện tại mod k, cộng 1); kiểm dòng s, s+k, s+2k… tới đủ n; ghi N, n, k, s và các dòng vào QA record.
**Ví dụ (QA-03 `DEMO-3402`, mô phỏng).** Upload giá 240 SKU AU, 4 category. Mandatory set 14 (2 launch, 9 giảm ≥20%, cao nhất, thấp nhất, 1 cho category thiếu). n = 30 vì 10% là 24. N' = 226, k = 7, s = 4. Tổng kiểm 44. Check 1 fail ở một SKU: check 2 dùng n = 60, cộng 14, cộng SKU fail = 75.
> QA-02 §1.4.2 liệt kê mandatory set là "SKU giảm sâu nhất"; QA-03 §2.3 (chủ sampling plan) nói mọi SKU giảm ≥20%. Theo QA-03, đã gồm SKU giảm sâu nhất.

### 3. Sampling ticket hằng tuần và siết chặt
Service sampling không có gate bắt buộc: ticket không được chọn đi từ STG SETUP sang PRD SETUP sau khi Shift Leader duyệt. Nên mẫu được chọn **trước khi Doer xin duyệt**.
1. Người intake thêm label service; dispatcher chạy filter ứng viên sampling đầu mỗi ca QA và mỗi 2 giờ.
2. Trên sampling log tuần, đếm theo cluster: cứ ticket thứ 5 vào mẫu (20%).
3. Chọn thêm ngoài 20%: 5 ticket đầu của Doer mới cert L1 trên service đó; mọi ticket của Doer ở L1 của people-risk ladder; bulk >100 dòng (MER-TXT-01, MER-DLV-03).
4. Comment `Selected for QA sample. Please move to QA REVIEW after self-check.` và gắn label sample.
5. Ticket làm ngoài giờ QA được sample ở ca QA kế và kiểm live trên production.
6. Trước **12:00 thứ Sáu**, bù cluster nào dưới 3 mẫu.
7. **Một mẫu FAIL:** kiểm mọi ticket service sampling của cluster đó trong tuần (ticket live trong 1 ngày làm việc) và đưa ticket mới qua QA REVIEW 100% tới hết tuần.
Tín hiệu siết khác: tháng đầu của service (lên một mức, chờ quyết), hypercare tháng 12/2026 (QA Lead re-check 10% PASS thay 5%, chờ quyết), cao điểm (hai lớp QA), và defect lọt lặp lại (service 100% tới khi xong CAPA). Cluster về bình thường sau 4 tuần không có mẫu fail (đề xuất).
> Cluster, label sample (đề xuất `qa-sample`), phạm vi "cả tuần" sau mẫu fail và luật nới lỏng chờ QA Lead quyết trước 09/11/2026.

### 4. Bộ KPI QA, K1 tới K13
KPI đo hệ thống, không đo người. Mọi số liệu lấy từ Jira và Confluence Samsung.
| # | KPI | Target | Đo bởi |
|---|---|---|---|
| K1 | Dispatch trong 15 phút (trong giờ QA) | 100%; dưới 95% trong tuần thì review roster | Sub-Lead 2 |
| K2 | Kết quả High trong 30 phút | 100% | QA Lead |
| K3 | Một hoặc hai item trong 2 giờ làm việc; batch trong 8 | ≥95% | QA Lead |
| K4 | QA cộng duyệt trong 25% ngân sách còn lại | ≥95% | QA Lead, Merch Lead |
| K5 | SLA vi phạm mà thời gian QA REVIEW là nguyên nhân chính | 0 | QA Lead |
| K6 | FPY: thay đổi pass ở check đầu | ≥95% | QA đo, Merch sở hữu |
| K7 | Rejection rate, kèm tỷ lệ `RC-EVD` | Giảm dần theo tháng | Sub-Lead 2 |
| K8 | Defect lọt trên 1,000 item pass | Tối đa 1 | QA Lead |
| K9 | QA miss trong re-check 5% PASS | 0 | QA Lead |
| K10 | Đợt go-live có comment QA-again | 100% | Sub-Lead |
| K11 | PASS có bằng chứng đủ; file còn trên máy | 100%; 0 | Sub-Lead |
| K12 | Tuần có mẫu đủ mỗi service | 100% | Sub-Lead 2 |
| K13 | Yêu cầu phút chót có QA gate: tổng, đúng giờ, không kịp | Theo dõi, báo hằng tuần | Merch Lead đếm, QA Lead thêm |
Đo hằng tuần; **K1 còn xem hằng ngày**, K8 còn tổng hợp hằng tháng.
> Target K1, K3, K4 (95%) và cách đo K5, K11 là đề xuất CoE Office; QA Lead quyết cùng OLA trước Sprint 2.

### 5. Daily QA report
Nhịp báo cáo bốn lớp: **mỗi ca** handoff note của dispatcher; **hằng ngày** báo cáo của QA Lead tại stand-up với các Lead; **hằng tuần** báo cáo QA 7 phần; **hằng tháng** xu hướng, defect lọt và CAPA.
Báo cáo ngày dựng từ handoff note ca và filter Jira (COE-F14 queue QA, COE-F16, COE-F17). Tại stand-up QA Lead (hoặc Sub-Lead 1) báo: 1) ticket ở QA REVIEW đầu ca; 2) tuổi ticket cũ nhất; 3) ticket trễ deadline QA hôm qua và vì sao; 4) đã gọi bench chưa; 5) dự báo hôm nay (go-live lớn, tải dự kiến). Thêm K1 trong ngày, và từ handoff note: ticket High, return kèm mã RC, đợt QA-again đã làm (K10), yêu cầu phút chót.
**Quy tắc an toàn:** lưu báo cáo trên Confluence Samsung với Jira macro; không export ticket ra Excel, không screenshot dashboard sang kênh khác, không đưa data ticket vào công cụ AI; dùng dòng ẩn danh khi bàn lỗi cá nhân.
> Nguồn không định nghĩa template "QA daily report" riêng. QA-01 §8.2 liệt kê lớp hằng ngày là báo cáo stand-up của QA Lead, QA-02 §5.4 cho năm mục. Cấu trúc trên kết hợp chúng với handoff note và K1 hằng ngày; QA Lead nên xác nhận là chuẩn.
Handover liên quan: Working Session P1 (23/10: quy trình QA review và ma trận ticket bỏ QA; dashboard và filter chính thức gồm dashboard QA (ticket ở QA REVIEW và PENDING LAUNCH theo thành viên QA)).

## Quiz (đáp án)
1 Ticket promotion SG 24 SKU, độ sâu thường → **B: 24** (10% chỉ áp trên 30 SKU). 2 File giá 420 SKU, mandatory set 12; phần ngẫu nhiên n → **B: 42** (10% làm tròn lên; 12 mandatory cộng thêm, không nằm trong n). 3 Cluster 3 (MY, SG): một ticket service sampling fail hôm Thứ Tư → **B: kiểm tất cả: ticket live trên production trong 1 ngày làm việc, ticket mới qua QA REVIEW 100% tới hết tuần**. 4 Thứ Sáu 11:30, cluster 5 (AU, NZ) có 2 mẫu → **C: chọn thêm trong ticket của cluster tuần đó trước 12:00 và kiểm trên production nếu đã live** (chọn ticket "dễ" là lỗi sampling). 5 Ca bận, Checker file giá E4 600 SKU muốn kiểm 30 SKU → **B: không được: n = 60 cộng mandatory set, cross-check cả diff file; check nhỏ hơn cần QA Lead đồng ý bằng văn bản trên ticket**. 6 Ca có 8 ticket vào QA REVIEW, 7 dispatch trong 15 phút, một ticket High ra kết quả sau 42 phút → **A: K1 87.5%, K2 trượt**. 7 QA Lead giữ số liệu hằng ngày ở đâu → **B: trên Confluence Samsung với Jira macro, ẩn danh với lỗi cá nhân**.

## Practice
**PR-QA-P2.2-1. Daily report từ shift log** (30'; giấy). Ca sớm mô phỏng Thứ Ba 04:00-12:00 ICT (Sub-Lead 2 và 2 Team Member). Shift log: 04:00 queue đầu ca `DEMO-7001` (vào QA REVIEW Thứ Hai 18:40), `DEMO-7002` (20:15), `DEMO-7003` (22:05); 04:10 cả ba dispatch; 04:30, 05:10 QA again trên production `DEMO-6990` đợt 1/2 và `DEMO-6991` đợt cuối, đều OK, đã đăng comment A.6; 05:00 `DEMO-7004` High vào, dispatch 05:06, PASS 05:28; 05:40, 06:20 `DEMO-7001` PASS, `DEMO-7002` PASS; 06:30 `DEMO-7005` Medium vào, dispatch 06:52; 07:00 `DEMO-7003` FAIL `RC-SCP`; 07:15 `DEMO-7006` Medium vào, dispatch 07:24, PASS 08:40; 08:00 `DEMO-7007` batch Low vào, dispatch 08:12, còn đang kiểm lúc 12:00; 08:10 `DEMO-7005` FAIL `RC-TZN`; 09:30 `DEMO-7008` Medium vào, dispatch 09:41, trả 09:50 `RC-EVD`; 09:45 `DEMO-7005` quay lại QA REVIEW, dispatch 09:55, PASS check 2 lúc 10:30; 10:20 `DEMO-7009` High vào, dispatch 10:24, PASS 11:05. Khác: Thứ Hai `DEMO-6985` trễ deadline QA 40 phút (queue lúc 17:00); không gọi bench; không yêu cầu phút chót; dự báo 6 go-live tối cùng ngày (SG, MY); sampling cluster 3: 2/3 tuần này. Viết daily QA report cho stand-up. K1 đếm mỗi lần vào QA REVIEW trong giờ QA (gồm re-check); ba ticket qua đêm không tính K1 nhưng phải dispatch trong 15 phút đầu ca. **Pass:** queue đầu ca 3; ticket cũ nhất 9 giờ 20 phút (`DEMO-7001`); trễ hôm qua: `DEMO-6985`, 40 phút, queue lúc 17:00; không gọi bench; dự báo 6 go-live tối. K1 = 6/7 = 85.7% (`DEMO-7005` dispatch sau 22 phút), dưới target. K2 = 1/2 (`DEMO-7009` mất 45 phút), trượt. Return 3: 2 FAIL (`RC-SCP`, `RC-TZN`) và 1 `RC-EVD` (1/3). PASS 6, gồm 1 ở check 2. K10: 2/2 đợt có comment. Mở lúc bàn giao: `DEMO-7007` (chưa xong), `DEMO-7008` (chờ Doer). Sampling: cluster 3 cần thêm 1 trước thứ Sáu 12:00. Không tên, không giá, chỉ link ticket. Số liệu do tác giả khoá học tính; QA Lead xác nhận quy ước đếm K1. Không cần access.
