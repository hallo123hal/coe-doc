# MER-2.3 Promotion rule, coupon, naming convention, Knox promotion

> Nguồn: page 2483061268 · 130 phút (Study 35' · Demo 15' · Quiz 10' · Practice 70') · Facilitator demo Promotion Rules, simulator, Coupon Management trên staging; learner làm một mình rồi đổi vai Doer/QA; facilitator: Sub-Lead certified PRM/CPN + QA Sub-Lead.
> Cần xong G3.4, MER-1.2 (A.10), MER-1.3 (RB-MER-PRM-01). Quyền: staging s2 với Marketing (Promotion Rules, Coupon Management) + quyền *Preview-promotion-module* để chạy simulator — vị trí menu simulator trên s2 và quyền Preview cho learner **chưa xác nhận** (Lead xác nhận trước cohort). Facilitator đưa 2 SKU training cùng nhóm (A, B) + 1 SKU ngoài list (C) để test cart không đạt.

## Mục tiêu
Build promotion rule đúng code, tên theo convention, website, rule group, priority, condition, action, dates; test bằng simulator với cart đạt/không đạt và ghi kết quả đối chiếu expected; tạo coupon đúng Coupon Guidelines và gắn vào rule bằng condition *Carts with voucher codes*; điền đúng phần Approval, phân loại thay đổi nào cần Knox lại; nhận và từ chối request promotion bị cấm.

## Thuật ngữ
**Promotion Templates** (Marketing › Promotion Templates; rule tạo từ template đã có sẵn condition/action); **Clone Promotion Rule** (copy giữ mọi setting, cần code mới, luôn Unpublished); **preview-promotion-module** (chỉ cho simulator, publish vào đây không cần Knox); **`<cc>-promotions-module`** (module live của nước; publish discount rule vào đây gửi Knox, chỉ live sau khi Knox duyệt); **Approval Title / Description / Business PIC** (3 field phần Approval của rule — điền đủ trước khi publish discount rule); **Campaign (validity)** (cho một rule nhiều khung giờ start/end trong một kỳ); **QAS-PRM-01** (checklist QA cho promotion, dùng dựng evidence PowerPoint 6 slide); **Undeploy**; **Exclusive vs normal group** (`exclusivePackagePromotionGroup` chỉ áp rule priority cao nhất; `productPromotionRuleGroup`, `orderpromotiongroup` cộng dồn, priority cao chạy trước); **KNOXPENDINGAPPROVAL / KNOXAPPROVED / KNOXREJECTED**; **RNPL** (loại promotion trong danh sách naming và là trường hợp duy nhất còn dùng voucher; ý nghĩa đầy đủ chờ xác nhận RHQ — CM-13 §14.4; xem 06 RNPL (SR+)).

## Nội dung
### 1. Tạo rule và đặt tên
Cả 3 cách tạo cho ra rule ở trạng thái **Unpublished**: New (Marketing › Promotion Rules › "+", nhập Code & Name, Finish); Clone (chọn rule › Clone Promotion Rule › code mới › Save); From template (Marketing › Promotion Templates › chọn template › nhập Code › OK). **Code là duy nhất, không đổi được sau khi tạo.** Name theo naming convention (G3.4) — tên sai là lỗi RHQ ghi nhận breach nhiều nhất.

| Phần tên | Giá trị hợp lệ (06 Naming Convention) |
|---|---|
| Country | SG, MY, ID, TH, VN, PH, NZ, AU |
| Site | B2C, EPP, SMB, O2O, EA |
| Platform | WEB (web & app), APP, CRP, ePromoter, LS |
| Category | SP TB WR MXAPS MO TV AV VC MW RF AC DW WM CA MS MX CE ALL VD DA HA; nhiều category nối bằng `-` |
| PromotionType | BOGO PWP BMSM EV PROMOTEXT REWARDS DISCOUNT PAYMENT SHIPPING SIM TRADE-IN RNPL (CRP thêm PPX, ESG, NRM) |
| Priority VN | Package, FOC 600 (exclusive group); Ecobundle 400–500; coupon cấp sản phẩm 200–300; coupon cấp giỏ 50–100; payment promotion 0–30 |
| Priority SG | First purchase 303 (EPP 203); % off RRP & fixed price 304–500; amount off 100–299; distributed 10–99; halt & always-on từ 1000 |

Lỗi hay gặp: Site trước Country; ngày không dạng ddMMMyy; dùng `_` trong free text (phải `-`).

### 2. Điền rule: properties, conditions, actions
Thứ tự: **Rule Properties** (Name, Website = promotion group của nước VD `vnPromotionGroup`, Rule group, Priority theo convention nước, Start/End) → tab **Conditions & Actions** (condition: container X chứa Qualifying products; action trỏ tới container) → Save (vẫn Unpublished tới khi publish).
Action thường dùng: Percentage discount on products (có biến thể tính trên RRP); Fixed discount; Target Fixed Price; Distributed discount (chia đều mức giảm cho các SKU); Partner product discount (mua X giảm Y); Free gift. **Free gift theo stock**: gift nhập trước có ưu tiên, hết hàng thì dùng gift kế. Stock Check Type: CHECK_PROMO_STOCK đọc `promoStockAvailable`; CHECK_STOCK_AVAILABILITY đọc tồn thật; DISABLED không check, chỉ dùng gift đầu — kiểm field này với brief trước khi Save. Condition Category Price Threshold tính trên tổng cả giỏ.

### 3. Publish preview và test simulator
Preview-promotion-module cho simulator, không cần duyệt. Country module (VD `vn-promotions-module`) là live — publish discount rule vào đó gửi Knox, chỉ live sau khi Knox duyệt ("Knox before publish live" ở G3.4 và "publishing starts Knox" ở đây là cùng một bước). Trên ticket thật chỉ làm sau QA PASS và Shift Leader duyệt; **khi training chỉ publish preview**.
Thiết kế test: luôn có cart đạt và không đạt, cart ngay dưới/trên ngưỡng (299 và 300 với ngưỡng 300), SKU ngoài list, ngày ngoài hiệu lực. Evidence QA = PowerPoint 6 slide (Summary, Setup, Simulator eligible, Simulator ineligible, Price, Conclusion), không video.

| Cart test tối thiểu cho "10% off SKU A, B" | Kết quả mong đợi |
|---|---|
| 1 × SKU A | SKU A giảm 10% |
| SKU A + SKU B | cả hai giảm 10% |
| 1 × SKU C (ngoài list) | không giảm |
| SKU A, ngày ngoài hiệu lực (nếu simulator cho chọn) | không giảm |

### 4. Coupon
Marketing › Coupon Management › Coupons. **Single**: một mã chung, đặt Maximum Total Redemptions & Maximum Redemptions per Customer. **Multi**: prefix đúng 4 chữ/số, part count 3, part length 4, rồi generate. Gắn vào rule bằng condition *Carts with voucher codes*. **Luôn đặt đủ 3 giá trị: mức giảm, tổng lượt dùng, lượt/khách** — trống = không giới hạn = luôn là sanity hold (PS-08). Số mã lớn cần ImpEx → tạo linked COEC (CPN-01, MER-1.2).

### 5. Knox cho promotion
Mọi promotion cần Knox trước khi live (kể cả free-gift/non-discount; CM-13 ch.10, CM-07 §2.2); path từ cột approval path của brief, CoE không chọn. Các bước dưới là flow Hybris cho **discount rule**; free-gift/non-discount Hybris không hiện popup Knox (hành vi hệ thống, không phải luật) → hỏi Shift Leader cách gửi Knox evidence.
Các bước (KB Promotion Rule Knox Approval): điền Approval Title, Description, Business PIC ở phần Approval rồi Save (thiếu một thì nút OK bị disable) → bấm publish → popup *Request for Discount Promotion Approval* → chọn Approval Process đúng path trong brief (danh sách nhóm theo MX, VD, DA), OK; brief không có path thì **không đoán**, hỏi trong câu hỏi gộp → rule sang KNOXPENDINGAPPROVAL → `knoxPromotionStatusJob` (45') → KNOXAPPROVED → cronjob publish (45') → PUBLISHED; bị từ chối là KNOXREJECTED, sửa rule KNOXREJECTED sẽ tạo version mới UNPUBLISHED. Mẫu nội dung: trang "1. Knox Discount Promotional Approval Template".
Lưu ý: ngày đặt theo campaign thì Period không hiện trong approval; rule dùng qualifying category thì mọi SKU của category hiện trong approval; publish nhiều rule một lúc thì path theo rule giảm nhiều nhất, mọi Business PIC phải duyệt, một người từ chối thì cả batch bị từ chối; **không publish chung discount và non-discount** (hệ thống cảnh báo "Discount Promotion and Non-Discount Promotion are mixed").
Campaign (SOP): chỉ dùng khi một rule có nhiều khung start/end trong một kỳ; muốn đổi/gia hạn → **xóa campaign cũ, tạo campaign mới, gửi Knox mới; không sửa dates của campaign đang dùng**. Bulk upload rule: Export Promotion Source Rule từ rule mẫu, giữ cột 2, thêm rule từ cột 3, import; kết quả cronjob SUCCESS / UNKNOWN (lỗi một phần) / FAILED.

### 6. Control R3 và request phải từ chối
- Control R3 cho promotion: ghi internal check trước khi build; chạy sanity PS-05 (giảm ≥30% khi category chưa có range), PS-06 (stacking không có trong brief), PS-07 (quà có landed cost ≥100 USD), PS-08 (coupon), PS-10 (ngày, time zone, >90 ngày). Ngưỡng là đề xuất tới khi Merch Lead & QA Lead xác nhận (MER-3.1). Rollback: unpublish rule hoặc đặt end date = hiện tại.
- Ngoài 2 lệnh cấm ở G3.4: **Rewards boosting chỉ dùng discount type PERCENTAGE (FIXED_PRICE bị cấm)**; **RNPL bị cấm cho model flagship N mới nhất (S26 series, Buds4, Buds4 Pro, Z Fold, Z Flip)**, mọi RNPL setup cần RHQ review; **Samsung Members EPP chỉ được 5% sitewide trên giá B2C**, không promotion nào khác ngoại trừ HR và RNPL.

### Điểm đáng nhớ từ KT
Promotion brief là template phức tạp nhất (mỗi loại một sheet; subsidiary điền một phần, CoE điền một phần); các field gồm site (EPP phân cách bằng dấu phẩy), main SKU, stacking, dates, loại & prefix coupon, discount type, cart message, remarks, FOC consignment, xử lý khi hết quà — trống/mâu thuẫn thì hỏi một lần, không đoán số tiền. Không biết thuật ngữ promotion thì hỏi team CoE; RHQ không giải thích mọi khái niệm. Mục 06 RHQ COE Guidelines gom luật mới từ Suwon & RHQ và ghi đè KB cũ (CM-13 §14.4). Dùng coupon, không dùng voucher (trừ RNPL). EPP có guideline GNB mới; long-term financing (1 site SG) và Samsung Members có luật riêng.

## Quiz (đáp án)
1 Tên BOGO S25 B2C VN web+app 01–28/02/2025 đúng → `VN_B2C_WEB_SP_01FEB25_28FEB25_BOGO_S25-Series`. 2 Clone rule PUBLISHED → **Unpublished, code mới bạn nhập**. 3 Publish vào preview-promotion-module → **không cần Knox**. 4 Publish chung 8% và 25% → **path theo rule giảm nhiều nhất (25%)**. 5 Sửa condition rule KNOXREJECTED → **tạo version mới UNPUBLISHED**. 6 Multi-code đúng Guidelines → **prefix `VNCP`, 3 phần × 4**. 7 Gia hạn promotion đặt ngày theo campaign → **xóa campaign cũ, thêm mới, gửi Knox mới**. 8 RRP 25.000.000, A 8% (450), B coupon 1.000.000 (250), C 300.000 khi dùng thẻ bank X (20), normal group → **21.700.000** (A → 23.000.000, B → 22.000.000, C → 21.700.000).

## Practice
- **PR-MER-2.3-1 Naming** (giấy, 10'): (a) viết tên cho 5 brief (MY EPP TV 10% 01–15/12/2026; SG B2C BMSM tủ lạnh+máy giặt 05–20/12; AU B2C trade-in boost smartphone 01–31/12; PH B2C free shipping tủ lạnh 10–12/12; VN B2C payment bank X smartphone 01–07/12) → ví dụ `MY_EPP_WEB_TV_01DEC26_15DEC26_DISCOUNT_…`, `SG_B2C_WEB_RF-WM_05DEC26_20DEC26_BMSM_…`, `AU_B2C_WEB_SP_01DEC26_31DEC26_TRADE-IN_…`, `PH_B2C_WEB_RF_10DEC26_12DEC26_SHIPPING_…`, `VN_B2C_WEB_SP_01DEC26_07DEC26_PAYMENT_…` (free text chỉ dùng `-`); (b) tìm lỗi 5 tên sai — free text chứa `_`; Site trước Country; ngày không phải ddMMMyy; SALE không có trong PromotionType; REF không phải mã category (tủ lạnh là RF).
- **PR-MER-2.3-2 Build & test** (staging, 25'): brief website `vn`, giảm 10% SKU A, B khi giỏ có ≥1 trong 2, từ 00:00 hôm nay đến 23:59 ngày kia ICT, normal group. Viết internal check bằng template C.2 (MR-06 App. C) đủ 6 giá trị, kết thúc "Matches approved brief v1". Build: code `TRAINING_<NAME>_PROMO01`, Name `VN_B2C_WEB_SP_<ddMMMyy>_<ddMMMyy>_DISCOUNT_Training-<NAME>`; Website `vnPromotionGroup`, Rule group `productPromotionRuleGroup`, Priority 350 (VN chưa có band cho product discount thường; 350 nằm giữa coupon cấp sản phẩm 200–300 và Ecobundle 400–500 nên discount chạy trước coupon; trên ticket thật lấy priority từ brief hoặc hỏi Sub-Lead); container X = SKU A, B; action Percentage discount 10%. Save, kiểm Unpublished; publish vào preview-promotion-module (**không** `vn-promotions-module`); chạy 4 cart ở bảng trên, chụp từng kết quả. Pass: internal check đủ 6 giá trị; tên đúng convention; 4 screenshot khớp expected; rule không nằm ở `vn-promotions-module`. Không có Preview right: tạo rule Unpublished, điền cột "expected" rồi so với kết quả facilitator chạy simulator.
- **PR-MER-2.3-3 Coupon gắn rule** (staging, 20'): tạo single coupon `TRAINING<NAME>CPN`, Max Total 100, Max/Customer 1, dates như PROMO01; clone PROMO01 thành `TRAINING_<NAME>_PROMO02`, thêm condition Carts with voucher codes với mã mới; undeploy PROMO01 khỏi preview, publish PROMO02 vào preview; simulator 2 cart (SKU A không mã / có mã); cấu hình multi-code (prefix 4 ký tự, 3 phần × 4; sinh tối đa 10 mã nếu facilitator cho phép). Pass: không mã → không giảm, có mã → giảm 10%; coupon đủ 3 giá trị; mã dạng `XXXX-XXXX-XXXX-XXXX`; biết khi nào số mã phải chuyển Tech qua COEC.
- **PR-MER-2.3-4 Approval & Knox** (staging không submit + giấy, 10'): điền Approval Title/Description/Business PIC theo trang "1. Knox Discount Promotional Approval Template", Save, không publish vào `vn-promotions-module`; phân loại 6 thay đổi trên promotion đã publish — đổi Funding Type, đổi Cost Centre, thêm campaign, đổi Quota, thêm 1 SKU vào container, sửa dates của campaign đang dùng → **Knox lại**: thêm campaign, thêm SKU (đổi Conditions); **không Knox**: Funding Type, Cost Centre, Quota; **sửa dates campaign đang dùng: không được phép**. Viết A.13 cho DEMO-6301 (path từ brief + giờ gửi); status không đổi.
- **PR-MER-2.3-5 Từ chối** (giấy, 5'): 5 request — discount thêm chỉ khi mua trên Shop App (cấm promotion theo platform); overtrade TH bằng promo rule (phải dùng overtrade feature); rewards boost kiểu FIXED_PRICE (chỉ PERCENTAGE); RNPL cho Z Fold mới nhất (cấm, RHQ review); promotion riêng cho Samsung Members EPP ngoài 5% sitewide. Viết reply tiếng Anh ngắn + bước tiếp (dùng đúng feature, hoặc chuyển RHQ kèm lý do). **Dọn cuối buổi:** undeploy và xóa PROMO01/02; xóa coupon training hoặc đặt Active = false và ghi vào trang bài tập; chụp danh sách rule lọc `TRAINING_<NAME>` sau dọn.
