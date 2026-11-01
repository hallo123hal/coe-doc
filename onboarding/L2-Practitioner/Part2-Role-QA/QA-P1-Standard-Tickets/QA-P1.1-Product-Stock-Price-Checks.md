# QA-P1.1 Product, stock and price checks

> Nguồn: page 2484076994 · 90' (Study 20' · Demo 15' · Quiz 10' · Practice 45') · Facilitator: QA Lead/QA Dispatcher · Capabilities C2, C4 · Cần xong QA-2.2 (kiểm product, price, stock trong Backoffice và frontend) và QA-1.3 (checklist, sampling plan, sanity test); phải biết 4 bước QA (receive, dispatch, test, return), kết quả PASS/FAIL/QUESTION và bảng mã RC. Mang ticket thực hành SCOE-7 (TRN-001), SCOE-13 (TRN-007), SCOE-50 (TRN-044), SCOE-33 (TRN-027) sau khi Merch trainee (hoặc trainer) đã setup với lỗi cài sẵn. Access: Backoffice staging el3-s2 (Advanced Search và Export theo catalog version, tab Product Administration, tab Prices, Price Settings › PriceInfoChange), storefront staging `vn`, `test1`, `my`, `my_dennis_test`, Jira SCOE. **QA không có HAC** (staging lẫn production; HAC chỉ Tech): khi check cần nhiều dòng hơn Backoffice hiển thị, Checker xin Tech output query qua COEC liên kết; trong khoá học trainer đưa output, bạn không chạy query. QA không bao giờ đổi setup, publish, hay export danh sách giá/SKU khỏi máy; bằng chứng là PowerPoint làm trên workstation CoE. Không access: bản giấy với export before/after in sẵn.

## Mục tiêu
Chọn checklist, độ sâu check và mẫu SKU cho ticket product/stock/price, ghi N, n, k, s trong QA record; kiểm product status theo từng child catalog so với bảng status-CTA trong Back Office lẫn storefront, gồm một negative case; kiểm RRP hay stock sync qua các catalog trong scope và xác nhận dòng bị giữ không bị sync; kiểm file special price với PriceInfoChange trước Knox gồm overlap và price sanity; viết một comment FAIL liệt kê mọi defect kèm category và mã RC.

## Thuật ngữ
**QCL (QA checklist)** (checklist hai cột theo nhóm việc trong QA-03, VD QCL-PRD-01 (SKU setup), QCL-STK-01 (stock), QCL-PRC-01 (giá, special price, discount row); luôn dùng với QCL-00); **Blocking item** (mục đánh dấu [Blocking]; một defect là FAIL, không có "conditional PASS"); **QA gate** (bước trong status path của runbook đưa ticket sang QA REVIEW; runbook sửa đổi đặt theo service và thường theo variant); **Ticket sampling** (Level 1 của sampling plan: 20% ticket của service sampling mỗi tuần mỗi cluster, tối thiểu 3; cluster 1 là VN); **Mandatory set** (SKU luôn kiểm trong mẫu: SKU launch/flagship, giảm ≥20%, giá cao nhất và thấp nhất, một SKU mỗi category, SKU bị sanity gắn cờ); **Systematic sampling (N, n, k, s)** (chọn phần ngẫu nhiên mỗi dòng thứ k từ điểm bắt đầu s, k = N' ÷ n; QA record phải ghi N, n, k, s); **Check A / B / C** (special price: A = QA kiểm file và PriceInfoChange trước Knox; B = người thứ hai lúc bắt đầu window; C = sau khi kết thúc); **Giá ba lớp** (Back Office = giá đã lưu, simulator = giá cuối có promotion, storefront ở đợt go-live: PDP, category, cart, checkout).

## Nội dung
### 1. Từ ticket tới checklist và độ sâu check
Lúc dispatch (trong 15 phút) dispatcher chọn Checker, độ sâu check và giờ QA đến hạn. Runbook của service, thường cả variant, quyết định ticket có đi QA REVIEW không và checklist nào. Mức rủi ro quyết độ sâu: K1 chuẩn; K2 cho E4 hoặc re-check sau SKU FAIL.
Bảng dưới thay danh sách gate "catalogue v0" cũ, lấy từ Jira status path của 19 runbook Merch sửa đổi (A.II.1 Merch Services). Dòng gắn D9 chưa chấm điểm tới khi quyết định D9.
| Service (runbook sửa đổi 01/11/2026) | QA gate trong status path | Ghi chú | Checklist |
|---|---|---|---|
| MER-PRD-01 SKU setup | V1 upload template và V6 đổi attribute: QA REVIEW mọi ticket. SKU flagship: QA | **Under review: D9.** V2-V4 dòng chỉ-status: Merch tự check kèm bằng chứng, cộng mẫu 20% hằng tuần của BiPlus (tối thiểu 3) | QCL-PRD-01 |
| MER-STK-02 Virtual stock | QA kiểm 100% trước khi bán | – | QCL-STK-01 |
| MER-STK-03 Pre-order stock | QA kiểm trước khi mở window và sau mỗi lần đổi số lượng/ngày | – | QCL-STK-01 |
| MER-STK-01 Super Sync | V3 (RRP): QA lấy mẫu storefront theo loại catalog | **Under review: D9.** V1, V2 stock: QA chỉ khi được yêu cầu; không thì check nội bộ | QCL-STK-01 |
| MER-DLV-01 Delivery mode | V4 (fee promotion): QA mọi ticket. V1, V2, V3, V5: sampling theo ma trận QA | – | QCL-DLV-01 |
| MER-PRC-02 Special price | Check A mọi ticket: file, overlap, stacking. Không Knox trước PASS | Check B lúc bắt đầu và Check C lúc kết thúc bởi người thứ hai | QCL-PRC-01 |
| MER-PRC-01 Price upload | Check A mọi ticket: file, overlap, sanity. Không Knox trước PASS | Check B lúc go-live bởi người thứ hai | QCL-PRC-01 |
| MER-PRM-06 Trade-in | QA mọi ticket, trước PRD SETUP và lúc go-live: cart test trade-in và negative | – | Runbook 4.1 |
| MER-CPN-01 Coupon | QA mọi ticket: test theo VOU-01 và VOU-02 | – | QCL-CPN-01 |
| MER-PRM-01 Product discount | QA mọi ticket: simulator trên catalog Staged | – | QCL-PRM-01 |
| MER-PRM-04 COMBO | QA mọi ticket: test cặp, tỷ lệ, special price, package trong simulator | – | Runbook 4.1 |
| MER-PRM-02 Cart discount | QA mọi ticket: cart dưới, bằng, trên mỗi ngưỡng; chỉ tier tốt nhất; payment khác; SKU bị loại | – | QCL-PRM-01 |
| MER-PRM-09 Batch (>2 promotion) | QA mọi dòng và basket stacking | – | QCL-PRM-09 |
| MER-PRF-04 Freebie | QA mọi ticket: simulator trước go-live, rồi live trên storefront mỗi đợt go-live | – | QCL-PRF-01 |
| MER-TXT-02 Benefits | Tuỳ chọn: launch, multi-group EPP, mẫu (QAS-MER-01) | Peer check file trước upload | QCL-TXT-01 |
| MER-AEM-04 Campaign page và banner | Runbook: QA mọi ticket. Trong ticket: một site mỗi group cộng 10% còn lại (tối thiểu 2) | **Under review: D9.** QA-01 và CM-07 giữ là sampling | QCL-AEM-01 |
| MER-AEM-01 AEM page | Runbook: peer check rồi QA mọi ticket | **Under review: D9.** QA-01, CM-07 nói R1 không qua QA | QCL-AEM-01 |
| MER-SAC-01 Shop App | Runbook: peer check rồi QA mọi thay đổi Shop App CMS | **Under review: D9.** QA-01, CM-07 nói R1 không qua QA | QCL-SAC-01 |
| MER-INC-01 Live error | Second checker trong 30 phút, rồi QA team/QA on-call trên storefront live trước khi gỡ containment | – | Runbook 4.1 |
Mọi check bắt đầu bằng QCL-00, lõi "đủ dữ liệu cho QA chưa?". Blocking item gồm: ticket tới QA REVIEW bằng đổi status; go-live theo giờ market và ICT; brief đầy đủ; với R3, comment check nội bộ của Doer có timestamp trước khi build. Thiếu blocking item thì không test: trả về STG SETUP với `RC-EVD`, về bàn Doer. Ticket nhiều service lấy mức cao nhất và gate chặt nhất. TRN-044 có dòng stock (MER-STK-01) và RRP (MER-STK-01 V3); chỉ dòng RRP đi QA Team, theo mẫu.
> Under review: quyết định D9 của L2 gap review. Runbook theo handover 23/10 (dòng status PRD-01 và stock STK-01 là Merch tự check; thay đổi AEM và Shop App CMS luôn qua QA). QA-01, QA-03, CM-07 §3.3 giữ mẫu ticket 20% và nói R1 không qua QA. Merch Lead và QA Lead quyết.

### 2. Sampling: bao nhiêu SKU và SKU nào
Sampling plan có hai level. Level 1 chọn ticket của service sampling (20% mỗi tuần mỗi cluster, tối thiểu 3; một FAIL nghĩa là mọi ticket cluster đó trong tuần đều bị kiểm). Level 2 đặt độ phủ SKU trong ticket đã đi QA.
| SKU trong ticket (N) | Phần ngẫu nhiên n | Cộng | Sau FAIL |
|---|---|---|---|
| 1-30 | Tất cả N | – | Tất cả N |
| 31-300 | 30 | Mandatory set | n gấp đôi (60) |
| 301-499 | 10% làm tròn lên | Mandatory set | n gấp đôi |
| ≥500 | 10% | Mandatory set; file giá ≥500 SKU là E4 | n gấp đôi |
**Ví dụ (QA-01 Case 2, mô phỏng).** Special price 48 SKU (20 TV, 18 monitor, 10 soundbar). 10% của 48 ≈ 5 <30 nên n = 30. Mẫu phải có SKU launch, SKU giảm sâu nhất 35%, giá cao nhất (5,000 AUD), thấp nhất (120 AUD) và một SKU mỗi category. Một SKU hiện 899 AUD trong khi file ghi 989 AUD: cả ticket FAIL (Price, `RC-ENT`). Hoàn tất cả mẫu rồi mới trả. Check 2 gấp đôi thành 60 >48 nên kiểm cả 48.
Chọn phần ngẫu nhiên trên file diff trong hệ thống Samsung, không export: đánh dấu mandatory set, k = N' ÷ n (số nguyên), s từ 1 tới k, lấy dòng s, s+k, s+2k… Ghi `SKU coverage: N=…, mandatory set=…, random n=…, k=…, s=…`. Ticket lab: TRN-001 có 9 SKU, TRN-007 có 7 SKU, nên khi bị lấy mẫu bạn kiểm tất cả.
> Sheet lab TRN-001 nói "ít nhất 1 SKU mỗi item, cả hai kênh" cho mẫu QA. QA-03 bảng 2.3 nói tới 30 SKU thì kiểm hết. Theo QA-03: kiểm cả 9 SKU khi ticket nằm trong mẫu. Giảm độ phủ cần QA Lead đồng ý bằng văn bản trên ticket.

### 3. Kiểm product status (MER-PRD-01)
Kênh là **child catalog**; trạng thái bán là cặp approvalStatus + salesStatus trên version Staged của mỗi child catalog, rồi sync sang Online.
| salesStatus | approvalStatus | CTA trên storefront (VN) |
|---|---|---|
| PURCHASABLE | approved | Buy now (hết hàng: stock alert) |
| PURCHASABLE | unapproved | "Where to buy" (không mua online được) |
| ARCHIVED | check / unapproved | Không CTA; không tìm thấy trên EPP |
| Bước | Doer | Checker |
|---|---|---|
| 1 | Tách dòng theo SKU và catalog; export trạng thái before | Mỗi dòng có một kết quả; có export before |
| 2 | Kiểm phụ thuộc trước khi ẩn (F-code, gift, tham chiếu add-on, promotion trong promotion group của site) | Phụ thuộc đã báo requester |
| 3 | Đặt status trong từng child Staged catalog được yêu cầu | Status theo catalog trong export after, từng dòng |
| 4 | Sync Staged → Online; chờ index và cache | Online = Staged; không SKU/catalog ngoài yêu cầu bị đổi |
| 5 | Test PDP và add to cart theo loại catalog | Mẫu storefront theo loại catalog; API add-to-cart 0000 khi active, 0001 khi archived |
**TRN-001 (VN, SCOE-7).** D2C = `vnEstoreProductCatalog`, EPP = `vnProductCatalog` (catalog mặc định của `test1`). Ẩn `SM-S928BLBQXXV`, `SM-S928BLBWXXV` trên D2C và EPP, và `EP-T1510NBEGWW` chỉ D2C. Bỏ ẩn `SM-W620NZKAXXV`, `QA85LS03BAKXXV`, `SM-R800NZSAXXV` trên cả hai. Kỳ vọng trên `vn`: `SM-R800NZSAXXV` hiện Buy now; `SM-W620NZKAXXV` và `QA85LS03BAKXXV` hiện stock alert vì stock pool bằng 0 — không phải lỗi setup nhưng phải ghi trong comment. Negative: `EP-T1510NBEGWW` vẫn PURCHASABLE trên catalog EPP.
**TRN-007 (VN, SCOE-13).** `HW-S800B/XV` phải thành "Where to buy" chỉ trên D2C: unapproved + PURCHASABLE. Thấy ARCHIVED là FAIL, `RC-ENT`. Ba TV ARCHIVED trên mọi catalog trong scope (D2C, EPP, SME), không 3PD.

### 4. Kiểm stock và RRP (MER-STK-01)
Super Sync đẩy dữ liệu NERP vào Hybris từ Product Cockpit (data type STOCK, PRICE, DOTCOM, IMAGE). Checker xác nhận nguồn đã sẵn sàng, scope đủ, không gì ngoài ticket bị đổi. Hai luật cứng: không chạy Super Sync STOCK trên SKU đang pre-order (gỡ pre-order trước theo MER-STK-03), và chạy price sanity trước khi sync RRP (PS-03: mới ÷ cũ <0.5 hoặc >2; PS-04: giá bán >RRP).
**TRN-044 (MY, SCOE-50).** Bốn dòng. Dòng 2: RRP `EF-XF966SBEGWW` từ 349 lên 379 MYR (tỷ lệ 1.09, sanity ổn), sync từ 18/11 00:00 MYT. Dòng 3: `EP-DA705BWEGWW` còn pre-order 18/20 trên `SETOnline` → không được sync. Dòng 4: `SM-R420NZKAXME` 499 → 4,990 tỷ lệ 10 → PS-03 giữ, không sync.
QA Team kiểm dòng 2 theo mẫu: Backoffice › Product Cockpit › Products, tìm theo từng catalog version, tab Prices, price type RRP: 379 trong `myProductCatalog`, `myEstoreProductCatalog` Staged và Online, và `myb2bProductCatalog`. Export dòng làm bằng chứng. Runbook nêu export Q4 diff cho mục này; query đó là của Tech nên trong lab trainer đưa output. PDP trên `my` và `my_dennis_test`: giá đúng; giá bán không vượt RRP. Negative: dòng 3 pre-order vẫn 18; dòng 4 RRP vẫn 499; không SKU ngoài ticket bị đổi. Lỗi cài sẵn của lab: "vẫn RRP 349 trong myEstoreProductCatalog Online; master 379" — child sync Staged → Online chưa chạy.
> MER-STK-01 V3 đề xuất mẫu storefront 10% SKU, tối thiểu 3 mỗi loại catalog ("confirm ở KT"); QA-03 bảng 2.3 kiểm hết tới 30 SKU. Với một SKU ở dòng 2 cả hai cho cùng check: một site mỗi loại catalog.

### 5. Kiểm giá trước Knox (QCL-PRC-01, MER-PRC-02)
Giá là R3 có gate bắt buộc. QA kiểm giá ba lớp: Back Office, simulator, storefront ở đợt go-live. Với special price, thứ tự cố định: Check A (QA) → Shift Leader duyệt (PRD SETUP) → Doer nộp Knox. Trước Knox so file với **PriceInfoChange** (status VALID), không so với price row Staged: row chỉ xuất hiện ở Staged sau Knox duyệt và job áp giá. Mở Backoffice › Price Settings › Prices › PriceInfoChange, chuyển advanced search (User = Doer, Timestamp = khung upload) và export record.
QA không nộp Knox và không đánh giá đường duyệt; Doer và Shift Leader sở hữu. QA kiểm ba thứ: tham chiếu Knox, giờ và đường duyệt có trong comment ticket; file DiscountContent của request không thiếu/thừa SKU (MER-PRC-02 mục 15); sau duyệt record là COMPLETED và đã sync trước khi bắt đầu (mục 8).
Blocking của QCL-PRC-01: đúng template, market, currency, dấu thập phân; số dòng = SKU trong brief, không trùng/trống/giá trị 0; diff file khi >100 dòng; price sanity PS-01 đến PS-04 từng dòng; giá Back Office của mẫu = giá mới; ngày hiệu lực và hết hạn theo giờ market; không có hiệu lực trước giờ đã duyệt.
**TRN-027 (AU, SCOE-33).** Price match 30%, 35%, 52% dưới RRP trên ba TV, làm tròn xuống, hiệu lực D+2 00:00 tới D+6 23:59:59 AEDT, tức `2026-11-17 13:00:00` tới `2026-11-22 12:59:59` GMT với D0 = 16/11/2026. Special price Always-On (không ngày) phải giữ không ngày, nên sau window giá về Always-On, không về RRP. Dòng 52% phạm PS-01 (giá cuối <50% RRP) và requester muốn được báo khi >50%: chưa nộp tới khi requester xác nhận bằng văn bản.
> TRN-027 là ticket AU trên SMA el5, chưa gắn data staging. Dùng phương án NZ (`QA55Q7FAMSXNZ`, `QA98QN90DASXNZ`, `UA55DU7000SXNZ` trên `nzProductCatalog`, NZD, NZDT) hoặc làm giấy. Handover Price Row 29/10 chốt câu Always-On: sau window giá rơi về giá nằm dưới. Row mới trong window của row cũ tự tách row cũ: hệ thống kết thúc nó trước window mới và bắt đầu lại sau. Kiểm row đã tách ở Staged sau COMPLETED vì tách đã từng lỗi sau một số deployment (MER-PRC-02 §2.1).

### 6. Viết kết quả QA
| Kết quả | Khi | Trên Jira |
|---|---|---|
| PASS | Mọi mục pass, độ phủ đủ, có bằng chứng | QA record + PowerPoint; ticket ở QA REVIEW; Assignee về Doer cho Shift Leader duyệt |
| FAIL | Ít nhất một defect | Một comment liệt kê mọi defect, mỗi cái kèm category và mã RC; label `QA_Returned`; về STG SETUP |
| QUESTION | Brief thiếu, mâu thuẫn hay mơ hồ | Về STG SETUP; Doer hỏi subsidiary một câu gộp |
(Under review: D5 của L2 gap review. Dòng PASS chưa chấm điểm tới khi quyết D5; cái được chấm là QA record và bằng chứng.) Category defect: Price, Promotion logic, Coupon, Content, Partner service, Journey. Mã thường dùng: `RC-ENT` (nhập data), `RC-RUN` (bỏ bước runbook, VD không sync), `RC-SCP` (sai store, catalog, kênh), `RC-EVD` (thiếu data/bằng chứng). Re-check sau SKU FAIL phủ mọi SKU sai cộng mẫu gấp đôi.
Ví dụ TRN-001: `QA result: FAIL (check 1). Checklist QCL-PRD-01 v1.0. All defects listed: 1. RC-RUN: SM-R800NZSAXXV EPP Online still ARCHIVED – Staged updated but not synced. 2. RC-SCP: EP-T1510NBEGWW hidden on the EPP catalog; ticket asks D2C only. SKU coverage: N=9, all SKUs checked. Evidence: TRN-001_QA_check1_FAIL.pptx. Please fix and return to QA.`
> Sáu category defect không có tên cho product status hay stock; ví dụ lab chỉ cho mã RC. Tới khi QA Lead quyết (bảng mã còn là đề xuất, DL-01 C1), hỏi QA Lead ghi category nào cho lỗi status/stock.
Handover liên quan: Working Session P1 (23/10: phương pháp QA, ma trận QA review (ticket nào bỏ QA), báo cáo special price, status SLA); Day 2 Product Setup and Sync (26/10: Super Sync trong master catalog, đọc kết quả, RRP chỉ từ NERP); Day 5 Price Row (29/10: kiểm file special price, đổi GMT, lỗi catalog, tự tách row); Day 3 Knox Approval (27/10: flow PriceInfoChange, status và job Knox, file DiscountContent); [QA Team] SKU Fundamental Setup, Z-code, F-code, SuperSync (26/10).

## Quiz (đáp án)
1 Ticket special price 240 SKU trong 4 category, mandatory set 14 SKU, bạn kiểm bao nhiêu → **C: 44 (30 ngẫu nhiên + 14 mandatory)** (N=240 thuộc dải 31-300: n=30 vì 10%=24 <30). 2 TRN-001 `QA85LS03BAKXXV` được bỏ ẩn hiện stock alert thay vì Buy now; stock pool 0, status approved + PURCHASABLE ở Online → **B: Pass; ghi thiếu stock trong comment**. 3 TRN-007 thấy `HW-S800B/XV` ARCHIVED trên D2C, ticket xin "Where to buy" → **B: RC-ENT: phải là unapproved + PURCHASABLE**. 4 TRN-044 dòng 2: master `myProductCatalog` RRP 379 nhưng `myEstoreProductCatalog` Online 349 → **B: FAIL, Price: child sync Staged → Online chưa chạy** (QA không tự sửa). 5 TRN-044 dòng 4 xin Super Sync RRP 4,990 cho SKU 499, QA kỳ vọng thấy → **B: 499 không đổi; dòng bị giữ theo PS-03** (4,990 ÷ 499 = 10 >2). 6 File special price ở QA REVIEW, Knox chưa nộp, so với → **C: record PriceInfoChange status VALID**. 7 Một SKU sai trong mẫu 30, 29 đúng → **A: FAIL cả ticket; check 2 dùng mẫu gấp đôi cộng SKU sai**.

## Practice
**PR-QA-P1.1-1. QA trên bốn ticket product, stock, price** (50'; staging el3-s2, Jira SCOE; trainer đã chạy setup TRN-001, TRN-007, TRN-044 với lỗi cài sẵn, và đưa TRN-027 dạng file giấy hoặc phương án NZ). Với mỗi ticket: kiểm QCL-00, chọn checklist và độ phủ, kiểm setup trong Backoffice bằng Advanced Search và Export theo catalog version (ticket liệt kê query thì dùng output trainer đưa), kiểm mẫu storefront, viết QA record (PASS hoặc một comment FAIL kèm category và mã RC) có dòng coverage. Không sửa gì. **Pass:** tìm ra mọi lỗi cài sẵn. Tối thiểu: TRN-001 — `SM-R800NZSAXXV` EPP Online vẫn ARCHIVED (RC-RUN) và `EP-T1510NBEGWW` bị ẩn trên EPP (RC-SCP), coverage N=9 kiểm hết, SKU stock-alert không báo là defect. TRN-007 — `HW-S800B/XV` ARCHIVED thay vì unapproved + PURCHASABLE (RC-ENT). TRN-044 — RRP 349 vẫn trong `myEstoreProductCatalog` Online (child sync chưa chạy); negative cho thấy pre-order 18 ở dòng 3 và RRP 499 ở dòng 4. TRN-027 — so với PriceInfoChange, không phải row Staged; 30%/35%/52% làm tròn xuống; dòng 52% giữ theo PS-01 tới khi có xác nhận văn bản; row Always-On không có validityTo. Mỗi FAIL là một comment, label `QA_Returned`, về STG SETUP. Không access: làm từ export before/after và screenshot in sẵn.
**PR-QA-P1.1-2. Lấy mẫu file 48 SKU** (10'; giấy). Dùng QA-01 Case 2 (48 SKU: 20 TV, 18 monitor, 10 soundbar; launch `DEMO-TV-NEW1`; giảm sâu nhất `DEMO-MON-07` 35%; cao nhất `DEMO-TV-98`; thấp nhất `DEMO-SB-02`). Quyết E4 và diff file, tính mẫu, viết dòng coverage và coverage của check 2. **Pass:** không E4 (một market, <500 SKU, exposure 6,000 USD); không diff file (<100 dòng) nhưng price sanity vẫn bắt buộc; n = 30 gồm 4 SKU nêu tên và ít nhất một SKU mỗi category; một SKU sai làm FAIL ticket (Price, RC-ENT); check 2 phủ cả 48.
