# QA-1.3 Checklists, sampling plan and sanity test

> Nguồn: page 2483192629 · 90 phút (Study 35' · Demo/thảo luận 10' · Quiz 10' · Practice 35') · Tự đọc, facilitator giải một ví dụ tính toán, rồi bài cá nhân và review nhóm; facilitator: QA Sub-Lead 2 · Cần xong QA-1.1, QA-1.2; chỉ cần Confluence + giấy/Excel, không cần Backoffice.

## Mục tiêu
Dùng QCL-00 quyết định ticket đủ data cho QA hay phải trả `RC-EVD`; tìm mã checklist cho các service Merch phổ biến; tính SKU coverage và chọn dòng mẫu bằng systematic sampling (ghi N, n, k, s); viết lại dòng checklist mơ hồ thành dòng kiểm được.

## Thuật ngữ
**Two-column checklist** (cột Doer tự kiểm + cột QA kiểm độc lập); **[Blocking] item** (sai là FAIL ngay, không có "conditional PASS"); **QCL code** (`QCL-00` lõi chung, `QCL-PRM-01` product/cart discount…); **Standard operations BO / SIM / SF** (kiểm trên Backoffice / simulator / storefront); **Test run** (một lần chạy cart trên simulator, ghi 5 input + 3 output); **Ticket sampling** (với service "sampling" chỉ kiểm 20% ticket); **SKU coverage** (số SKU kiểm trong một ticket = mandatory set + n random); **Mandatory set** (SKU luôn kiểm: flagship, giá cao nhất, thấp nhất…); **Systematic sampling** (lấy dòng s, s+k, s+2k… thay vì chọn tự do); **Market cluster** (5 nhóm: VN; TH+ID; MY+SG; PH và EPP/SMB/O2O/3PD; AU+NZ); **Monthly sanity test**; **BLOCKED** (không chạy được bước kiểm, không bao giờ ghi PASS).

## Nội dung
### 1. Checklist hoạt động thế nào
- **Hai cột:** Doer điền cột tự kiểm trước khi chuyển QA; Checker kiểm lại trên hệ thống, không copy kết quả Doer. Mỗi dòng chỉ một kết quả: Pass, Defect, hoặc N/A kèm lý do. Ghi mã và phiên bản trong QA record (VD `QCL-PRM-02 v1.0`).
- **Mã cần biết trước:** `QCL-PRM-01` (product/cart discount), `QCL-PRM-02/03/04` (BOGO, COMBO, cross-sell), `QCL-PRC-01` (price, special price, discount row), `QCL-CPN-01` (coupon), `QCL-PRD-01/02` (SKU, Z-Code, F-Code), `QCL-MST-01` (multistore), `QCL-GL-01` (QA again mỗi wave go-live). Danh sách đủ ở QA-03 §1.2.
- **11 standard operations trên 5 tool:** Backoffice — BO-1 đọc field đối chiếu brief và internal check; BO-2 xác nhận chưa live; BO-3 tìm promotion/giá khác chạy cùng SKU. Simulator — SIM-1 positive, SIM-2 negative, SIM-3 stacking. Storefront — SF-1 desktop incognito, SF-2 test account tới trước bước thanh toán, SF-3 mobile view trong browser. Thêm AEM-1, APP-1 cho content.
- **Một test run ghi 5 input + 3 output.** Input: store, customer group, SKU và số lượng, ngày giờ giả lập, coupon. Output: promotion áp dụng, số tiền giảm, tổng cart. VD: "store `vn`, regular customer, 1 × SKU-A, 02-Dec 10:00 ICT, no coupon; result: PROMO01 applied, discount 800,000, total 7,200,000".

### 2. QCL-00 — lõi chung
Kiểm QCL-00 trước mọi checklist khác. Các dòng [Blocking]: 0.1 ticket vào QA REVIEW bằng transition; 0.3 go-live có hai time zone; 0.4 brief đủ thông tin; 0.5 với R3, internal check viết **trước khi build**, đủ 6 giá trị (SKU, giá/discount, thời gian + time zone, site/store, stacking, usage limit) và kết thúc bằng "Matches approved brief v[n]" — chỉ ghi "OK" là không đủ. Thiếu một dòng blocking thì **không kiểm, trả `RC-EVD`**. Dòng 0.13 (Knox) luôn N/A với QA vì Shift Leader kiểm Knox. Dòng 0.11 chỉ xác nhận COEC liên kết đã xong; QA không kiểm phần Tech.

### 3. Ticket sampling và SKU coverage
- **Ticket sampling:** service gate "sampling" kiểm 20% ticket/tuần/cluster, tối thiểu 3, lấy mỗi ticket thứ 5. Luôn thêm: 5 ticket đầu của Doer L1 mới, mọi ticket của Doer trong people-risk ladder, bulk file >100 dòng. Một ticket mẫu FAIL → kiểm toàn bộ ticket service đó trong cluster tuần đó.
- **SKU coverage:** mandatory set gồm SKU launch/flagship, SKU giảm ≥20%, giá cao nhất và thấp nhất, ≥1 SKU mỗi category, SKU có sanity flag hoặc nêu trong brief. Cộng n SKU random theo bảng. Sai một SKU = FAIL cả ticket, re-check gấp đôi n.

| N (số SKU trong file) | n random (ngoài mandatory set) | Ví dụ |
|---|---|---|
| ≤30 | Kiểm tất cả | 18 SKU → 18 |
| 31–300 | 30 | 45 SKU → 30 + mandatory |
| 301–499 | 10% làm tròn lên | 420 → 42 + mandatory |
| 500–999 | 10% (luôn E4, so toàn bộ diff file) | 620 → 62 + mandatory |
| ≥1,000 | 10% | 1,200 → 120 + mandatory |

### 4. Systematic sampling và siết mẫu
N' = số dòng ngoài mandatory set; k = phần nguyên của N'/n; chọn s từ 1 đến k; lấy dòng s, s+k, s+2k… VD DEMO-3402: 240 SKU, mandatory 14, n=30, N'=226, k=7, s=4 → dòng 4, 11, 18…; tổng 44 SKU. Ghi: `SKU coverage: N=240, mandatory set=14, random n=30, k=7, s=4`.
**Siết mẫu khi có dấu hiệu rủi ro:** 1 SKU sai → gấp đôi mẫu; tháng đầu BiPlus chạy một service → tăng một level; hypercare 12/2026 → QA Lead re-check 10% PASS thay vì 5%; lỗi escaped lặp lại → service lên 100%. **Không bao giờ giảm mẫu vì áp lực thời gian**; giảm mẫu cần QA Lead đồng ý bằng comment.

### 5. Viết dòng checklist, phiên bản, monthly sanity test
- **Dòng kiểm được:** một dòng một hành động; nêu đối tượng, giá trị so sánh và nơi kiểm; không dùng từ mơ hồ ("OK", "carefully"); viết tiếng Anh. VD "Dates OK" → "Start and end date/time in BO-1 equal the internal check, in market time (SGT)".
- **Phiên bản:** checklist đổi giữa lúc đang kiểm → tiếp tục bản cũ nhưng áp dụng ngay dòng blocking mới, ghi cả hai phiên bản. Checklist thật nằm trên Samsung Confluence; QA-03 chỉ là mô hình mô phỏng.
- **Monthly sanity test** (RHQ chưa quyết QA có làm không): 14 flow SAN-01…SAN-14 trên production sau release tháng, 8 market. Flow không chạy được → ghi BLOCKED kèm lý do, không PASS. Flow quan trọng hỏng → báo Tech Level 1, xử lý như incident (G2.5).

## Quiz (đáp án)
1 Price upload 240 SKU, không E4, mandatory 14 → **A: 44** (14 + 30). 2 226 dòng ngoài mandatory, n=30 → k = **B: 7**. 3 Dòng 0.5 QCL-00 R3 chỉ ghi "Internal check: OK" → **C: thiếu data, về STG SETUP, `RC-EVD`**. 4 Special price 80 SKU không E4 → n = **D: 30 + mandatory set**. 5 SAN-09 ở TH không chạy được vì thiếu payment test → **A: BLOCKED + lý do**. 6 Đang kiểm bằng `QCL-CPN-01 v1.0` thì ra v1.1 có thêm dòng blocking → **B: giữ v1.0, áp dụng dòng blocking mới ngay, ghi cả hai**. 7 Một ticket mẫu của cluster MY+SG FAIL trong tuần → **C: kiểm mọi ticket service đó trong cluster tuần này**. 8 Dòng viết đúng → **D: "Start/end time in BO-1 equals internal check, market time"**.

## Practice
- **PR-QA1.3-1** (15'): tính n và tổng SKU cho file 18, 45, 240 (mandatory 14), 620 (mandatory 18), 1,200; với file 240 tính k, chọn s (gợi ý lấy từ số phút hiện tại, vượt k thì lấy phần dư, dư 0 thì s=k), liệt kê 5 dòng đầu, viết dòng `SKU coverage`. Pass: 18→18; 45→30+mandatory; 240→44; 620→62+18=80 SKU và so toàn bộ diff file; 1,200→120+mandatory; dòng cách đều với k=7.
- **PR-QA1.3-2** (12'): chấm QCL-00 cho DEMO-QA-110 (SG, 12% off 6 SKU Galaxy Buds, R3, Medium; vào QA REVIEW bằng transition 10:05 ICT; brief v1 đủ; go-live "05-Dec 00:00" không time zone; build 09:30, internal check viết 09:50 chỉ "OK"; không có rollback; có self-check `QCL-PRM-01 v1.0`; không freeze; không COEC). Pass: 0.1 và 0.4 Pass; 0.3 Defect (không time zone); 0.5 Defect (viết sau build, chỉ "OK"); 0.8 Defect (R3 không rollback); 0.9, 0.11 N/A; 0.13 N/A (Shift Leader kiểm Knox). Quyết định: không kiểm, trả STG SETUP `RC-EVD`, một comment A.2 liệt kê 3 thiếu sót.
- **PR-QA1.3-3** (8'): viết lại dòng "Dates OK" và "Coupon fine" theo 10 quy tắc §3.2, rồi viết test case `TC-PRM01-04` (negative, thời gian) có ID, bước, data, một expected result. Pass: dòng kiểm được, tiếng Anh, nêu mã BO/SIM và giá trị so sánh; test case dùng thời điểm 1 phút sau end time theo giờ market với kết quả "promotion not applied".
