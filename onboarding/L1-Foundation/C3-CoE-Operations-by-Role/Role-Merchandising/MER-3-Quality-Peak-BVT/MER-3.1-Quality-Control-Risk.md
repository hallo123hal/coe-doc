# MER-3.1 Setup quality control and risk (R1/R2/R3, E4, price sanity)

> Nguồn: page 2483388645 · 65 phút (Study 28' · Demo 7' · Quiz 10' · Practice 20') · Lecture + case theo cặp, role play desk check; facilitator: Merch Lead + QA Lead · Tài liệu chính: MR-06. Không cần hệ thống; mở sẵn MR-06 Appendix C (C.1 "Sanity hold", C.2 internal check). Cần xong G2.1, G2.6, MER-1.2, MER-2.2.

## Mục tiêu
Chạy 14 price sanity rule trên bảng giá và viết "Sanity hold"; tính exposure và quyết E4; viết internal check đủ giá trị và desk check theo cặp; nêu 3 lớp kiểm sau go-live, ngưỡng báo động, deadline contain; biết RC code nào tính cho Doer và khi nào vào L1 của people-risk ladder.

## Thuật ngữ
**Gross exposure** = (giá được duyệt − giá thực thu) × số lượng; quà tính theo landed cost. **Net loss** = gross − phần thu hồi được. **Sanity hold** (dừng ticket vì vi phạm sanity rule, hỏi subsidiary một câu gộp bằng C.1). **Desk check** (Doer đọc giá trị từ màn hình, Shift Leader đối chiếu từng dòng với internal check và nói "check"/"stop" — pilot). **Order anomaly monitor** (theo dõi order 8 lần, phút 15, 30… đến 120 sau go-live R3). **RC code** (root cause code lỗi QA trả, VD RC-TZN time zone, RC-BRF sai brief). **People-risk ladder L1** (bắt buộc coaching khi 1 người có 2 QA FAIL tính cho Doer trong tháng hoặc 1 strike).

## Nội dung
### 1. Bốn lỗi gây thiệt hại & chuỗi control R3
Sai giá, sai promotion, sai market, sai thời điểm — bẫy phổ biến nhất là **time zone** (27/11/2026 00:00 NZ = 18:00 hôm trước giờ VN; AU = 20:00). Luôn ghi time zone cạnh mọi giờ và viết ngày không thể đọc nhầm (`27-Nov-2026 00:00 AEDT`). Sanity chạy 2 lần, internal check trước build, kiểm tiếp sau mỗi wave. Lỗi hay gặp: tự sửa giá hộ subsidiary; gửi nhiều câu hỏi rời rạc; ghi giờ không kèm time zone; để Doer tự làm post-change check.

### 2. 14 price sanity rule

| Code | Quy tắc | Ngưỡng mặc định (đề xuất) |
|---|---|---|
| PS-01 | Giá cuối dưới floor | Theo market rules page; không có thì <50% RRP |
| PS-02 | Giảm mạnh so với giá bán hiện tại | ≥20% cần xác nhận văn bản |
| PS-03 | Sai bậc độ lớn (thiếu số 0, currency, dấu thập phân) | giá mới/giá cũ <0.5 hoặc >2; khác số chữ số |
| PS-04 | Hiển thị phi lý | giá bán > RRP; giá gạch < giá bán; giá 0/trống |
| PS-05 | Discount ngoài khoảng của category | chưa có khoảng thì ≥30% là hold |
| PS-06 | Stacking, xung đột promotion | stacking không có trong brief là hold |
| PS-07 | Quà giá trị cao | landed cost ≥100 USD: xác nhận và tính exposure |
| PS-08 | Coupon | vượt cap; không giới hạn tổng lượt; thiếu giới hạn/khách khi brief yêu cầu |
| PS-09 | Trade-in, overtrade | cao hơn bảng giá partner đã xác nhận |
| PS-10 | Ngày, giờ, time zone | ngày đã qua; >90 ngày; thiếu/sai time zone |
| PS-11 | Freeze, BVT | thay đổi trong freeze không có bằng chứng duyệt; phụ thuộc enhancement chưa BVT sign-off |
| PS-12 | Store scope, số market | khớp brief; >5 market là E4 |
| PS-13 | Bulk file | >100 dòng cần diff file; không SKU trùng, không ô trống |
| PS-14 | Virtual stock, pre-order | ≥500 đơn vị hoặc vượt cam kết subsidiary |

Sanity chạy 2 lần: Doer trên brief/file trước build; QA trên kết quả build trước PASS. Vi phạm rule → dừng, comment "Sanity hold" (C.1) gộp mọi câu hỏi; ON HOLD SUBS, assign subsidiary; go-live trong 8 giờ tới thì báo Shift Leader; chỉ nhận trả lời bằng văn bản trên Jira; không tự đổi giá trị.

### 3. Internal check & desk check
Viết internal check tiếng Anh trong 30' sau lần sanity đầu; tối thiểu 6 giá trị: SKU, giá/discount, thời gian kèm time zone, site/store, stacking, usage limit; dòng cuối "Matches approved brief v[n]". **Không internal check = không build R3.** Desk check (pilot): Doer đọc từng giá trị từ màn Backoffice, Shift Leader so với internal check và nói "check"/"stop".

### 4. Exposure và E4 hai cấp
Gross exposure = (giá duyệt − giá thực thu) × số lượng; quà theo landed cost; cộng phần trade-in/coupon vượt giới hạn. Ví dụ MR-06 A: giá 1.200 USD nhập thành 120 USD (thiếu số 0): phát hiện lúc 20:15 thiệt hại 2.160 USD; bỏ qua post-change check thì 9.720 USD gross, 6.480 USD net. **Không tính được exposure → đề xuất E4 và hỏi Shift Leader; Shift Leader quyết và ghi lý do** (CM-07 §2.3). E4 duyệt 2 cấp: cấp 1 Shift Leader; cấp 2 Merch Lead/Deputy (người khác Doer, Checker, Shift Leader). Hạn nội bộ: 15' cho High, 30' cho ticket khác. Ngoài 08:00–17:00 T2–T6 Lead on-call đến trung tâm Hà Nội trong 60', **không duyệt từ nhà** → đưa ticket E4 lên trước 17:00. Lead không duyệt kịp trước go-live thì **không publish**, báo subsidiary dời giờ.

### 5. Kiểm sau go-live và contain
3 lớp: go-live check; post-change check bởi người thứ hai (không phải Doer) trong 30' (15' với E4) — 12 mục storefront (ẩn danh, desktop & mobile, tới checkout) + 1 test order; order anomaly monitor 8 lần (phút 15, 30…120). **Ngưỡng báo động:** số order gấp 3 dự kiến; discount lớn hơn internal check; giá dưới floor/<50% RRP; coupon dùng hết 80% giới hạn trong 2h; order ngoài scope; ngày peak không có order nào trong 60'.
Có bất thường → contain trước, tìm nguyên nhân sau: phút 0 báo Shift Leader; trong 15' Shift Leader xác nhận tác động; trong 30' dùng kill switch (60' nếu không có) và báo RHQ + subsidiary bằng template CM-06; danh sách order ảnh hưởng trong 24h; RCA & CAPA trong 48h (tối đa 72h); cập nhật checklist trong 3 ngày làm việc; người liên quan được certify lại.

### 6. Kết quả QA, RC code, people-risk ladder
QA trả PASS, FAIL (một lần trả liệt kê mọi lỗi) hoặc QUESTION; thiếu data → về STG SETUP mã RC-EVD. Phạm vi SKU: ≤30 SKU check hết; >30 check max(10%, 30) + SKU launch, SKU giảm sâu nhất, giá cao nhất/thấp nhất, ≥1 SKU/category. QA-1.3 và QA-03 dùng bộ bắt buộc khác nhau (QA-03: mọi SKU giảm ≥20%, mọi SKU có sanity flag) — tới khi QA Lead chọn một, self-QA check cả hai. **FPY** = số PASS ở lần check đầu / tổng lần check đầu của ticket có QA gate.
RC code **tính cho Doer**: ENT, RUN, TZN, SCP, STK, LIM, FIL, EVD, KNW, COM; **không tính**: BRF (sai brief khi internal check khớp brief đã duyệt), CHG, TOL, DEP, RUL, CAP. Mỗi lỗi 1 mã chính, tối đa 1 mã phụ. **L1:** 2 QA FAIL/tháng với mã tính cho Doer, hoặc 1 RHQ strike → coaching, giảm nửa khối lượng, peer check mọi ticket, certify lại trong 5 ngày làm việc.

## Quiz (đáp án)
1 R3 là E4 khi → **đủ ít nhất 1 trong 3 điều kiện**. 2 Subsidiary không đưa số lượng nên không tính được exposure → **đề xuất E4, Shift Leader quyết**. 3 Sanity chạy mấy lần → **2 lần: Doer rồi QA**. 4 Brief sai giá, Doer build đúng brief, internal check khớp → **RC-BRF, không tính cho Doer**. 5 Post-change check E4 → **không phải Doer, trong 15'**. 6 20:10 thấy sai giá trên production, không có kill switch → **báo Shift Leader, contain trong 60'**. 7 Coupon dùng 85% giới hạn trong 2h đầu → **ngưỡng báo động; báo Shift Leader**.

## Practice
- **PR-MER-3.1-1** (giấy, 8'): brief AU B2C 8 dòng → gán PS code, viết một "Sanity hold" C.1 gộp câu hỏi, ghi status & Assignee. Đáp án: dòng 1 (1.200→120 AUD) PS-03 (và PS-01); dòng 2 (1.299→1.499, RRP 1.399) PS-04; dòng 3 (35% off, chưa có range) PS-05; dòng 4 (01/12/2026–30/03/2027) và dòng 5 (thiếu time zone) PS-10; dòng 6 (coupon AUXMAS không đặt tổng lượt) PS-08; dòng 7, 8 không vi phạm. Một câu hỏi gộp, ON HOLD SUBS, assign subsidiary, không tự sửa giá.
- **PR-MER-3.1-2** (6'): E4 cho 6 case — (a) coupon 50 USD × 300 lượt = 15.000 → E4; (b) 40 USD × 200 = 8.000 → không; (c) promotion 6 market → E4; (d) price file 520 SKU → E4; (e) quà landed cost 120 × 50 = 6.000 → không E4 nhưng vẫn cần xác nhận theo PS-07; (f) không có số lượng → đề xuất E4, Shift Leader quyết.
- **PR-MER-3.1-3** (cặp, 6'): viết internal check C.2 cho BOGO `DEMO-BUDS-3` tặng `DEMO-CASE-3`, TH B2C, 11–13/12/2026 ICT, không cộng dồn với cart-level coupon, 1 lần/khách; đổi vai desk check với cấu hình mô phỏng có 1 lỗi gài (end time 23:59 ngày 12/12) → Shift Leader nói "stop"; sửa xong kết thúc "Desk check verified".
