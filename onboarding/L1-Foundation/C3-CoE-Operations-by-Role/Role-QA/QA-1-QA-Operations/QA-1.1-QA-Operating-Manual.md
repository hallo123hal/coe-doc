# QA-1.1 QA Operating Manual: role, scope, organisation and targets

> Nguồn: page 2483225546 · 60 phút (Study 29' · Demo/thảo luận 6' · Quiz 10' · Practice 15') · Tự đọc rồi thảo luận ca với facilitator (QA Lead) · Cần xong G1–G6; ôn G2.1 (Doer–Checker–Approver, R1/R2/R3, E4, SLA/OLA/KPI), G2.2 (QA REVIEW, STG SETUP), G2.6 (strike, last-minute request). Chỉ cần quyền đọc Confluence; mang bảng phân loại PR-G2.6-1 để so với QA matrix.

## Mục tiêu
Giải thích vì sao QA là Checker độc lập và được/không được làm gì với ticket; phân biệt việc của QA Team, BVT, Tech self-QA, Shift Leader; dùng QA matrix tìm service nào kiểm 100% hay lấy mẫu và độ sâu; liệt kê các QAS code và lý do QAS-CFG-01, QAS-BVT-01, QAS-ENH-01 bị bỏ; nhớ target nội bộ.

## Thuật ngữ
**QA gate** (điểm ticket cần QA PASS mới được duyệt); **QA matrix** (service nào kiểm 100%, service nào lấy mẫu, sâu bao nhiêu); **Check depth** K1 Standard, K2 Extended, K3 Two-layer, KM Sampling; **Override** (cho ticket đi tiếp sau QA FAIL, chỉ COE Lead); **QA miss** (bỏ sót lỗi mà checklist phải bắt được, target 0); **Re-check 5% PASS** (QA Lead mỗi tuần random 5% ticket PASS để kiểm lại); **QA again** (kiểm lại trên production ở mỗi wave go-live, học ở QA-3.2); **QA bench** (người dự phòng); **Dispatcher** (nhận ticket vào queue và giao Checker); **Track Q** (đường certification của QA, L0–L3); **No double-hatting** (một người không giữ hai vai, VD QA và Merch).

## Nội dung
### 1. QA là Checker độc lập
Mỗi setup Merch có 3 vai do 3 người khác nhau, kể cả ca đêm: **Doer** (Market Owner hoặc Merch TM đã certified), **Checker** (QA Team Member), **Approver** (Shift Leader trực, thêm Merch Lead/Deputy khi E4). QA báo cáo cho QA Lead, không phải Merch Lead. QA được trả ticket khi setup sai hoặc thiếu data để kiểm. **Chỉ COE Lead được override QA FAIL và phải báo RHQ**; Merch Lead, Shift Leader, Market Owner không có quyền này. **QA không bao giờ sửa setup thay Doer**, kể cả một field — vì người sửa thành Doer và không ai kiểm độc lập bản sửa.

### 2. Scope sau RHQ training 21/10/2026 (CM-13 ch.6)
QA chỉ kiểm việc Merch hằng ngày khi Shop Merchandising ticket ở QA REVIEW. **QA không làm BVT; không kiểm việc Tech** (QA REVIEW trong COEC là bước Tech tự kiểm trên staging). 3 việc thêm: QA again trên production ở mỗi wave go-live; kiểm lại setup Merch sau fix trong incident (CM-06); QA Lead re-check 5% PASS hằng tuần (hai việc đầu học ở QA-3.2). **Một SLA chung**: RHQ không đo riêng QA, thời gian ở QA REVIEW nằm trong SLA ticket Merch nên BiPlus đặt OLA riêng (QA-1.2). RHQ muốn Merch tự kiểm trước QA và return rate giảm dần theo tháng.

### 3. QA services (QAS)
| QAS | Kiểm gì | Trạng thái |
|---|---|---|
| QAS-PRM-01 | Promotion (discount, BOGO, combo, cross-sell, overtrade, SC+, eVoucher), coupon rules | Đang dùng |
| QAS-PRM-02 | Batch >2 promotion trong một ticket + interaction test | Đang dùng |
| QAS-PRC-01 | Price upload, special price, discount row, trade-in price | Đang dùng |
| QAS-MER-01 | SKU setup, Z-Code, F-Code, product reference, add-on page, multistore, delivery, stock, tạo coupon | Đang dùng |
| QAS-AEM-01 | Trang AEM, offer page, banner, GNB (R2, R3; R1 text change do Shift Leader, không qua QA) | Đang dùng |
| QAS-KNB-01 | Duy trì checklist và thư viện test case (QA Sub-Lead 2) | Đang dùng |
| QAS-VND-01, QAS-SAN-01 | Kiểm việc vendor khác; sanity test hằng tháng | Chờ RHQ |
| QAS-CFG-01 | Kiểm cấu hình Tech mới | **Bỏ**: QA không QA cho Tech |
| QAS-BVT-01, QAS-ENH-01 | BVT, enhancement | **Bỏ khỏi QA Team**: BVT do Merch/Tech PIC (CM-12) |

VD: MER-PRC-02 (special price) dùng QAS-PRC-01; MER-PRM-09 (batch 3 promotion) dùng QAS-PRM-02. Mapping nằm ở QA-03 §1.2.

### 4. QA matrix và check depth
| Risk | Service ví dụ | Cách kiểm | Depth |
|---|---|---|---|
| R1 | Text change, flag, banner không T&C | Shift Leader kiểm và duyệt, **không có QA gate** | — |
| R2 có gate | Z-Code, virtual stock, pre-order | 100% ticket | K1 |
| R2 sampling | SKU setup, PINMAP | 20% ticket/tuần/market cluster, tối thiểu 3 | KM |
| R3 | Price, special price, promotion, coupon, trade-in | 100% | K1, lên K2 khi có dấu hiệu rủi ro |
| R3 ở E4 | Exposure ≥10,000 USD, >5 market, hoặc price file ≥500 SKU | Bắt buộc | K2; K3 mùa cao điểm |

VD: special price 520 SKU cho TH là R3 và E4 → gate bắt buộc, K2 = lấy mẫu SKU gấp đôi, mẫu riêng cho từng market.

### 5. Tổ chức, certification, target, strike
- **Tổ chức:** 9 vị trí billable (RFP yêu cầu ≥8) + 1 QA bench. QA Lead là Hybris expert, sở hữu QA matrix, OLA, sampling plan. Sub-Lead 1 là Deputy, dẫn ca chiều. Sub-Lead 2 là dispatcher chính, dẫn ca sớm, giữ thư viện checklist. 6 người còn lại là QA Team Member. Không ai kiêm hai vai.
- **Certification theo service, không theo người** (CM-11 §1.3). Chưa có certificate service nào thì chưa có production access cho service đó. Role track QA chuẩn bị cho các bài test, không thay thế.

| Level | Được làm gì | Cách đạt |
|---|---|---|
| L0 Trained | Chỉ luyện trên staging và ticket replay | T3 quiz 30 câu, đạt 24 (80%) |
| L1 Certified | QA ticket thật cho service đó; L2/L3/Sub-Lead review mọi kết quả trước khi trả PASS | T4 replay thực hành (QA: 20 check, ≥95% chính xác, không lỗi critical) + T5 exam (mọi bước đúng, bước critical 100%) |
| L2 Independent | Kiểm một mình trong gate thường | T6 tuần có giám sát: FPY 90% tháng 11, 95% từ tháng 12, không lỗi critical |
| L3 Coach | Coach và chấm người khác | QA Lead quyết sau ≥4 tuần đạt target |

T7 (phỏng vấn RHQ) áp dụng cho QA Lead và Sub-Lead trước khi có production access (CM-11 §3.6).
- **Target nội bộ:** dispatch ≤15'; kết quả ticket High ≤30'; FPY ≥95%; ≤1 escaped defect/1,000 item PASS (≈1 lỗi/tháng toàn team); QA miss = 0. Nguyên tắc QA-01: *"Never buy speed by skipping a check step"*.
- **Strike (G2.6):** rủi ro trực tiếp nhất với QA là nhận kiểm service mình chưa certified rồi để lọt lỗi gây incident. VD chỉ có L1 promotion thì không nhận kiểm add-on page dù ca thiếu người.

## Điểm đáng nhớ từ KT (Samsung 21–23/10/2026)
- Setup fail QA gắn label `QA_Returned`; return rate đo hằng tuần theo team và PIC. Merch tự kiểm trước QA; FAIL lần 2 cùng ticket báo QA Lead (CM-13 §6.4, CM-05 §5.5).
- Phải có negative test bên cạnh positive; mỗi check có positive, negative và exploratory (QA-02 §1.5).
- Slide 11 của vendor nói stock/pre-order/multistore không cần QA review — **quy tắc CoE hiện hành**: scope lấy từ cột QA gate của MR-05 và QA matrix; stock, pre-order, multistore là R2 nên vẫn qua gate hoặc sampling.
- Simulator học ở QA-2.1; chỉ dùng tool trên CoE workstation (CM-10).

## Quiz (đáp án)
1 Merch Lead muốn promotion đi tiếp sau QA FAIL → **D: COE Lead, có báo RHQ**. 2 Việc KHÔNG thuộc QA Team (CM-13 ch.6) → **A: kiểm ở QA REVIEW của COEC** (đó là Tech self-check). 3 Doer nhập sai end date, sửa 10 giây → **B: ghi FAIL, liệt kê lỗi, trả Doer** (không có "conditional PASS"). 4 Special price 520 SKU TH → **C: bắt buộc kiểm K2 vì E4**. 5 Thời gian QA → **A: dùng chung SLA ticket Merch, BiPlus đặt OLA cho QA**. 6 Chỉ có L1 promotion nhưng được nhờ kiểm add-on page → **B: làm service chưa certified, incident là strike**. 7 Target escaped defect → **D: ≤1/1,000 item PASS**. 8 Tech nhờ QA kiểm cấu hình mới với QAS-CFG-01 → **C: từ chối, đã bỏ, Tech tự QA**.

## Practice
- **PR-QA1.1-1** (10', giấy): phân loại 6 yêu cầu theo risk, E4, cách kiểm, depth. Đáp án: (1) banner text không T&C VN → R1, Shift Leader duyệt, không gate; (2) BOGO TH B2C → R3, 100%, K1; (3) price file 650 SKU MY → R3 E4, K2; (4) virtual stock 300 pre-order SG → R2 có gate, 100%, K1; (5) coupon 50 USD × 300 lượt = 15,000 USD ở AU → R3 E4, K2; (6) 12 SKU mới PH → R2 sampling, KM. Pass ≥5/6.
- **PR-QA1.1-2** (5', cặp): ai làm? (a) Doer nhờ QA "giúp sửa" end time → Doer sửa, QA kiểm lại; (b) Merch Lead muốn bỏ QA FAIL → chỉ COE Lead override và báo RHQ; (c) Tech nhờ QA kiểm COEC ở QA REVIEW → Tech tự kiểm, không phải việc QA; (d) Shift Leader hỏi QA đã gửi Knox chưa → Doer gửi Knox, Shift Leader kiểm; QA không gửi cũng không kiểm Knox.
