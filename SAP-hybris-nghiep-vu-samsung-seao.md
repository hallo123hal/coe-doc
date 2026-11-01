# SAP – SAP và nghiệp vụ Samsung SEAO (giáo trình nền tảng cho Ops CoE, phiên bản 2.0)

> Tóm tắt chi tiết trang Confluence "SAP và nghiệp vụ Samsung SEAO" (https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2480047339). Người lập: Quý Trần Đức. **Phiên bản 2.0, ngày 01/11/2026.** Đối tượng: Ops CoE Merchandising, QA, Tech. Nguồn: cây "10.1 Knowledge Base 2026", các trang RHQ, tài liệu vận hành CoE CM-01 đến CM-13. Trang song ngữ; bản tóm tắt này dựa trên phần tiếng Việt (chương N, 01–10).
> **Quy tắc nguồn:** khi các nguồn khác nhau về quy tắc quy trình thì theo **CM-13**; các chỗ khác nhau còn lại giáo trình ghi "(nguồn khác nói khác: …)".
> "SAP" ở đây là **SAP Commerce Cloud (Hybris)**, nền tảng eStore, không phải SAP ERP (ERP của Samsung là N-ERP/GERP). Cấu hình đổi theo chiến dịch, nên luôn kiểm tra lại Backoffice và trang KB trước khi làm. Tên, mã đơn và số tiền trong ví dụ (chị Lan…) là dữ liệu giả.

## Cách dùng giáo trình
- Đi cùng chương trình **L1 Foundation**: G3.1 → chương N và 01; G3.2 → 02; G3.3 → 03; G3.4 → 04; G4.1 → 05; G4.2 → 06; G4.3 → 08; G5.1 → N.12; G5.2 → 07. Đọc chương trước buổi học, làm bài sau buổi học, quay lại trang để tra cứu khi làm việc.
- Câu chuyện xuyên suốt: **chị Lan ở TP.HCM mua một điện thoại Galaxy và một tủ lạnh trên samsung.com/vn, trade-in máy cũ, nhập coupon, trả góp bằng thẻ tín dụng**. Mỗi chương nhìn câu chuyện từ một góc.
- Mỗi cụm chương có bài tập 5 bước: đọc/xem demo → ghi chép → bài nộp (BN1–BN4) → đọc lại/nghiên cứu → thực hành. Chương 09 có 18 câu tự kiểm tra và bài tập tổng hợp (BN5, BN6).

## Điểm thay đổi ở phiên bản 2.0 (so với bản cũ)
- **HAC chỉ dành cho Tech (CM-09).** Merch và QA đọc dữ liệu trên Backoffice, cần nhiều dòng thì nhờ Tech qua ticket COEC liên kết. Bài tập chương 07 tách thành phần làm trên giấy (mọi vai trò) và phần chạy trên HAC staging (chỉ Tech).
- **Merch setup trên production**, theo quy trình ticket, QA, Shift Leader duyệt và Knox. Staging dùng để học và thử. Phân biệt rõ **Staged** (phiên bản catalog), **staging** (môi trường) và **STG SETUP** (trạng thái Jira).
- **Promotion:** publish preview cho simulator, publish live thì mở luồng Knox từ Hybris, chuỗi trạng thái Knox, các thay đổi phải xin Knox lại, quy tắc campaign, naming convention, các yêu cầu RHQ cấm. Knox áp dụng cho **mọi giá và mọi promotion** (CM-13 chương 10).
- **Giá:** luồng Knox qua **PriceInfoChange**; quy tắc template giá (ngày giờ theo **GMT**).
- **Sản phẩm, tồn kho:** master/child catalog, SKU tạo từ AEM, 4 giá trị Product Type, trạng thái chuẩn theo loại SKU, T-Code là Approved + PDP Not Available, import tồn kho chỉ ghi đè `availableAmount`, ba cách chặn import.
- **Đơn hàng:** `ORDER_SPLIT` là trạng thái đơn (bước tên là `splitOrder`); order process ghi tên bước thật; bỏ các trạng thái không có trong KB; thêm các ca đơn kẹt; cách Hybris chọn kho và tính RDD.
- **Kênh bán:** EPP phải có RHQ duyệt trước (không có email phê duyệt thì ON HOLD SUBS), mã login type, quy tắc 3PD theo CM-13 chương 15, đơn RNPL từ marketplace.
- **Coupon thay voucher từ 1/5/2026**; voucher chỉ còn cho RNPL. ImpEx/Groovy trên production cần PC ticket và dòng header **`#NOTE ITGC_JIRA:PC-xxxx(COEC-yyyy)`**.
- **Các nước:** NZ thuộc cluster SMS; đối tác, marketplace, cổng thanh toán cập nhật theo các trang Market Rules.
- **Bài tập:** chỉ làm trên staging, đối tượng đặt tên `TRAINING_`, bằng chứng theo CM-10. Bảng thuật ngữ đầy đủ chuyển sang trang "Onboarding – Glossary for newcomers"; chương 10 chỉ giữ thuật ngữ chính và danh sách nguồn đầy đủ.

## Chương N. Kiến thức nền: thương mại điện tử từ con số 0

### N.1 Hành trình mua hàng
- Phần khách thấy (bước 1–5): xem trang sản phẩm, chọn màu/dung lượng, thêm vào giỏ, thêm trade-in và coupon, nhập địa chỉ, chọn cách giao và cách trả tiền, thanh toán. Phần chạy ngầm (bước 6–10): Hybris tạo đơn, cổng thanh toán giữ tiền, kiểm tra gian lận, thu tiền, gửi đơn sang N-ERP, kho lấy hàng và giao, đơn tách thành hai lần giao. Sau đó là các tình huống sau bán: hủy, trả hàng, giao trễ.
- Hệ thống theo từng phần: nội dung trang → **AEM**; giá, tồn kho, giỏ, promotion, coupon, đơn → **Hybris**; giá thu máy cũ → đối tác trade-in; giữ/thu tiền, trả góp → cổng thanh toán; đơn bán, lệnh giao, xuất kho, hóa đơn → **N-ERP**; lấy hàng, đóng gói, giao, mã vận đơn → kho/3PL.
- Trạng thái đơn đi theo đường: `PAYMENT_AUTHORIZED` → `PAYMENT_CAPTURED` → theo consignment (`SHIPPING_REQUESTED`, `SHIPPED`…).

### N.2 Sản phẩm
- **SKU** là mã một mặt hàng cụ thể; mỗi SKU có giá và tồn kho riêng (điện thoại `SM-S938BZGFATS`, máy giặt VN `WW80K5410WW/SV`). **Category** là nhóm để khách duyệt.
- **Catalog:** mỗi nước có một **master catalog** (chỉ có bản Staged) và nhiều **child catalog**, mỗi kênh một catalog (eStore B2C, EPP, SME/SMB, 3PD, một số nước có Refurbished). Nội dung dùng chung sửa ở master rồi sync xuống Staged của từng child; nội dung riêng kênh (giá, dịch vụ bán kèm, reference) sửa thẳng ở Staged của child.
- Mỗi child catalog có **Staged** (bản nháp) và **Online** (khách thấy); thay đổi chỉ đến khách sau khi **sync**. Vì vậy một SKU hiện thành nhiều dòng trong Backoffice.
- **RRP** là giá niêm yết; giá bán là giá sau special price/promotion. Hết tồn kho thì không đặt được, trừ khi bật **pre-order** hoặc **overselling** (bán vượt tồn kho thật trong một mức đã đặt).

### N.3 Tiền
- Cổng thanh toán là bên trung gian trừ tiền (OnePay, Cybersource ở VN; 2C2P, Adyen ở SG; iPay88 ở MY/PH; Midtrans ở ID; Adyen ở AU/NZ).
- Thẻ đi hai bước như cọc khách sạn: **authorize** (giữ tiền) → kiểm tra gian lận → **capture** (thu tiền). Đơn bị chặn hoặc hủy trước khi capture thì khoản giữ tự nhả, không cần hoàn tiền. Khoản giữ có hạn (khoảng **7 ngày** với Visa/Mastercard eCommerce), nên đơn chờ quá lâu mới capture có thể lỗi.
- Rule gian lận riêng từng nước, ví dụ VN: cùng một email mua cùng một SKU 6 lần trong 28 ngày thì đơn bị đưa vào diện xem xét.
- Hình thức khác: trả góp (Cybersource VN, 2C2P SG); **BNPL** (Atome SG/TH/ID/PH, Kredivo ID/VN, Home Credit ID/PH, Afterpay và Zip AU, Laybuy NZ); **COD** (VN, PH); **Samsung Rewards** (điểm làm phương thức thanh toán); refund.

### N.4 Hàng
- Một nước có thể có nhiều kho (kho trung tâm, kho điện máy, cửa hàng đại lý giao từ hàng của họ). **3PL** là bên thuê ngoài. Kho làm pick → pack → ship; mỗi kiện có tracking number.
- **Vì sao tách đơn:** điện thoại ở kho trung tâm giao xe máy, tủ lạnh ở kho điện máy cần xe tải và lắp đặt → 2 lần giao = 2 **consignment**. Hai lý do chính: khác kho và khác cách giao.
- **Lead time** tra trong bảng **LeadTime** theo kho, mã bưu chính, delivery mode. **Cut-off** cũng nằm trong bảng đó; đặt sau giờ chốt thì tính như đặt hôm sau.

### N.5 ERP
- **N-ERP** (còn viết NERP, tài liệu cũ gọi **GERP**). Đơn phải sang ERP mới xuất hàng, ghi doanh thu, xuất hóa đơn.
- Chứng từ và trạng thái Hybris tương ứng: **SO** (Sales Order) = `SHIPPING_REQUESTED`; **DO** (Delivery Order) = `SHIPPING_PREPARATION`; **GI** (Goods Issue đầu tiên, hàng rời kho) = `SHIPPED`; **Billing** = consignment hoàn tất, đơn sang `WAITING_FOR_FINANCIAL` rồi `COMPLETED` (ID và MY hiện "Billing done").
- Tồn kho nhập từ N-ERP bằng cronjob khoảng 30 phút một lần.

### N.6 Khuyến mại
- **Promotion** là rule hệ thống tự áp. **Coupon** là mã khách nhập: single (một mã dùng chung) hoặc multi (mỗi người một mã). Định dạng RHQ cho mã mới: tiền tố đúng 4 ký tự, chỉ chữ và số, 3 phần mỗi phần 4 ký tự, ví dụ `CEOD-5BM9-9GML-GCNK`.
- **Voucher** là cơ chế cũ. Từ 1/5/2026 chương trình mới dùng coupon; voucher chỉ còn cho **RNPL**. Trên Hybris và storefront coupon vẫn hay hiện chữ "voucher" (điều kiện "Carts with voucher codes", ô "My Voucher"), đừng nhầm với voucher RNPL.
- Mọi giá và mọi promotion phải qua **Knox approval** rồi mới lên live.

### N.7 Kênh bán
- B2C; B2B ở SEAO chủ yếu là **EPP** và **SMB**; **marketplace** (Shopee, Lazada, TikTok Shop…) nối qua **middleware**, CoE chỉ quản middleware, không thao tác trên sàn; **O2O** nối eStore với cửa hàng thật.

### N.8 Môi trường: staging và production
- **Production** là hệ thống thật. **Staging** là bản tách riêng để thử tính năng, BVT, đào tạo, và để Tech chạy thử ImpEx/script trước khi xin duyệt. Job nền như nhập tồn kho **không chạy trên staging**, nên dữ liệu ở đó có thể cũ.
- Khi làm thật, **Merch setup hằng ngày trên production** theo ticket, QA và phê duyệt. Promotion dựng trên production, thử bằng simulator (publish preview, không cần Knox), rồi publish live đúng giờ go-live sau khi Knox duyệt. Chỉ promotion quá phức tạp mới thử trên staging trước. **Khi đang học thì chỉ làm trên staging.**
- Ba từ dễ nhầm: **Staging** = môi trường thử; **Staged** = bản nháp của catalog (production cũng có; sửa "chỉ ở Staged" trên production vẫn là sửa production); **STG SETUP** = trạng thái Jira, CoE đã nhận yêu cầu và đang setup trên production.
- Deploy có thể làm hệ thống chập chờn vài phút.

### N.9 Cách CoE làm việc
- **CoE**: đội BiPlus vận hành eStore cho 8 nước SEAO. **RHQ** (Singapore) là product owner: đặt ưu tiên, đo SLA, duyệt PC ticket. **Subsidiary** là bên gửi yêu cầu (requester).
- **Ticket** Jira: Merch và QA làm trên issue type **Shop Merchandising** trong project từng nước; Tech làm trong project **COEC**.
- **PC ticket** (Prod Change, project PC): mọi thay đổi Tech làm trên production (dữ liệu, cấu hình Back Office, ImpEx, Groovy, cronjob báo cáo) cần PC ticket RHQ đã duyệt, kể cả việc 5 giây. Merch setup giá, promotion, sản phẩm, CMS **không dùng PC ticket** mà theo quy trình Shop Merchandising và Knox.
- **KB/Confluence:** Confluence của RHQ là nguồn chuẩn duy nhất; KB trong space này ("10.1 Knowledge Base 2026") là bản sao.
- **Merch** cấu hình sản phẩm, giá, promotion, nội dung trang. **QA** kiểm tra độc lập mọi setup của Merch và không tự sửa. **Tech** lo đơn kẹt, dữ liệu hàng loạt, cấu hình hệ thống, middleware 3PD. **Shift Leader** (Merchandising Sub-Lead) kiểm và duyệt việc của Merch trong ca.
- **Knox approval**: phê duyệt giá và promotion trên Knox theo approval path ghi trong campaign brief (MX và CE khác nhau). Không phải Knox Manage (dịch vụ quản lý thiết bị bán ở Úc).
- **PUMI**: mẫu phê duyệt yêu cầu dữ liệu (báo cáo, dữ liệu lịch sử, cronjob báo cáo, thêm bớt người nhận). Đi **trước** PC ticket. Không dùng để duyệt ngoại lệ freeze.
- **HAC**: chỉ Tech, với role RHQ cấp (CM-09). Merch và QA không có quyền HAC, cả staging lẫn production.
- **L2/L3** (SDS India): sửa lỗi CoE không tự sửa được, nhất là lỗi code. Tech gửi Maintenance Request và vẫn giữ ticket.

### N.10 Những thứ chạy ngầm
- **Cronjob**: ví dụ `vn-tokoStockImportUpdateJob` nhập tồn kho từ N-ERP 30 phút một lần; mỗi nước có danh sách riêng. **Sync/import**: sửa tay một số mà cronjob chép đè thì mất, nên các trường N-ERP không gửi (pre-order, overselling) mới upload tay. **Middleware** như Logicbroker giữa Hybris và sàn. **Log** là nhật ký để tìm lỗi.
- Không ai chạy, dừng hay đổi lịch cronjob khi không có ticket và phê duyệt. Khi học chỉ xem.

### N.11 Dữ liệu dạng bảng
- Mỗi dòng có mã định danh **pk**. Bảng trỏ sang bảng khác bằng pk (ví dụ đơn lưu status = 8796, tra sang bảng trạng thái mới biết là COMPLETED), giống VLOOKUP. Tra như vậy gọi là **JOIN**. Trong Backoffice thì bấm đúp vào ô trỏ sang đối tượng khác.

### N.12 Sử dụng Backoffice (Back Office 2.0)
- **Trước khi đăng nhập:** mỗi cluster có Backoffice riêng: 7 nước (VN, TH, ID, MY, SG, PH, NZ) ở **SMS (el3)**, AU ở **SMA (el5)**. Khi học dùng **SMS staging s2** (URL có `samsungel3-s2`). Tài khoản theo từng người, thường theo nước (`coe.vn.<tên>`), chỉ dùng tài khoản của mình. Backoffice chỉ mở được từ máy trạm CoE trong khu bảo mật (RHQ whitelist IP văn phòng). Không chép mật khẩu lên Confluence/chat.
- **Năm bước đầu:** đăng nhập staging → gõ tên màn hình vào ô tìm của cây điều hướng → lọc danh sách bằng mã → bấm một dòng, đọc các tab chi tiết → khi học chỉ xem; lỡ sửa thì đóng mà không Save.
- **Thực hành an toàn:** chỉ staging; chỉ sửa đối tượng của mình (tiền tố `TRAINING_<tên>_`, ví dụ `TRAINING_LAN_PROMO01`) hoặc đối tượng Lead giao, lỡ Save đối tượng người khác thì báo Lead ngay; không chạy cronjob, Initialization, Update; không sync cả catalog (người hướng dẫn sync); Merch/QA không có HAC; dữ liệu cá nhân đã che, không tìm cách xem; ảnh bằng chứng chỉ chụp trên máy trạm CoE, đính thẳng vào trang bài tập hoặc ticket đào tạo rồi xóa bản trên máy (**CM-10**), không chụp bằng điện thoại, không chép sang máy cá nhân, không dán vào công cụ AI.
- **Màn hình:** cây điều hướng bên trái, danh sách ở trên, khu chi tiết có tab ở dưới; bấm đúp ô trỏ sang đối tượng khác để mở, bấm x để quay lại.
- **Perspective:** Administration Cockpit (màn hình chính, xem/sửa mọi đối tượng); Product Cockpit (sản phẩm theo catalog, tải template, upload hàng loạt, duyệt sản phẩm, **Super Sync** DOTCOM/PRICE/STOCK/IMAGE, sync master → child và Staged → Online); Customer Support/CS Cockpit (tra khách và đơn; một số thao tác sau bán như SKU swap do CS agent làm); O2O Cockpit (nhân viên cửa hàng theo dõi đơn O2O).
- **Thao tác cơ bản:** tìm nâng cao bằng kính lúp (lọc site, trạng thái, catalog version); luôn để ý cột catalog/version; tab Administration xem lần sửa gần nhất và item type (`TokoVariantProduct`); hai lỗi hay gặp là quên sync và sửa Staged của master thay vì child; System › Types › gõ tên type (LeadTime, FraudConfig) › "Search by type" (một số type có nút upload riêng); Stock Level File Upload ở Base Commerce › Stock Level; System › Background Processes › CronJobs chỉ xem, không bấm chạy.
- **Bản đồ màn hình:** SKU → Catalog › Products; tồn kho → Base Commerce › Stock Level; promotion → Marketing › Promotion Rules; coupon → Marketing › Coupon Management › Coupons (Active, ngày, Maximum Redemptions per Customer, Maximum Total Redemptions); đơn → Orders (Order Details, Positions and Prices, Payment and Delivery, Consignments); cấu hình store → Base Store, WCMS › Website, Multistore; Delivery Modes/Delivery Costs; payment mode → Types › PaymentMode; lead time/cut-off → System › Types › LeadTime.
- **Cấp nào thắng:** delivery mode và payment mode đọc **multistore → website → base store**. Sau đó delivery mode khách chọn có thể làm ngắn danh sách thanh toán (chỉ cho các supported payment modes của nó).

## Chương 01. Samsung SEAO: ai bán, bán cho ai, qua kênh nào
- SEAO = Đông Nam Á và Châu Đại Dương. RHQ ở Singapore quản 8 công ty con, tất cả chạy chung Hybris. Nội dung web trên **AEM**, nội dung Shop App trên **Shop App CMS**, đơn đi từ Hybris sang N-ERP.

| Nước | Mã công ty con | Site | Chênh giờ so VN | Cluster |
|---|---|---|---|---|
| Việt Nam | SAVINA | vn | bằng | SMS (el3) |
| Thái Lan | TSE | th | bằng | SMS (el3) |
| Indonesia | SEIN | id | bằng (Jakarta) | SMS (el3) |
| Malaysia | SME | my | +1 | SMS (el3) |
| Singapore | SESP | sg | +1 | SMS (el3) |
| Philippines | SEPCO | ph | +1 | SMS (el3) |
| Úc | SEAU | au | +4 (Sydney, tháng 10–3), +3 (tháng 4–9) | **SMA (el5)** |
| New Zealand | SENZ | nz | +6 (Auckland, tháng 10–3), +5 (tháng 4–9) | SMS (el3) |

- 09:00 Auckland = 03:00 Hà Nội → ticket/promotion NZ, AU hay rơi ca đêm; Merch trực 24/7. Một tài khoản Backoffice dùng cho một cluster, thường tách theo nước (`coe.vn.<tên>`, `coe.au.<tên>`).
- **MX** (điện thoại, tablet, đồng hồ, tai nghe, phụ kiện) vs **CE** (TV, tủ lạnh, máy giặt, điều hòa, màn hình…): khác approval path Knox (theo cột approval path trong campaign brief), dịch vụ thu cũ (MX trade-in kèm overtrade; CE trade-up), dịch vụ bảo vệ (MX Samsung Care+; CE bảo hành, CE SC+, gói bảo dưỡng), giao hàng (CE cần xe tải và lắp đặt, delivery mode và phí riêng).
- Trang sản phẩm trên AEM: **BC** (Buying Configurator, flagship), **Split PD** (MX còn lại), **Standard PD** (mọi CE). Từ cũ của Hybris: PDP, PLP.
- **Kênh bán:**
  - eStore B2C: website chính, child catalog eStore.
  - **EPP**: nhân viên công ty đối tác, sinh viên, người về hưu, khách ngân hàng, nhà mạng. Mỗi EPP là một multistore dùng child catalog EPP; đăng nhập bằng access code, domain email, OTP email/SMS, SSO; có quota.
  - **SMB**: multistore dùng child catalog SME; tài khoản duyệt tay hoặc tự động bằng mã xác minh; giá và promotion riêng.
  - **O2O**: **Endless Aisle** (nhân viên đặt hộ trên site EA hoặc EA App, theo dõi trên O2O Cockpit), **BOPIS** (mua online, nhận tại cửa hàng), **BOSFS** (MY, đại lý giao từ hàng của họ).
  - **Shop App**: chung dữ liệu Hybris, nội dung trên Shop App CMS.
  - **3PD**: Lazada, Shopee, TikTok Shop; eBay và Woolworths ở Úc. Hybris đẩy sản phẩm/tồn kho qua middleware (Logicbroker và 3 middleware khác); đơn quay về Hybris rồi sang N-ERP. VN, TH, MY, ID, AU có child catalog 3PD riêng.
- **Quy định 3PD:** CoE không thao tác trên sàn, chỉ quản luồng middleware (đơn, tồn kho, dữ liệu sản phẩm). Một **PIC 3PD chuyên trách trong Tech Team** làm toàn thời gian, kèm một backup đã có chứng nhận (CM-13 §15.2). Mọi thay đổi dữ liệu 3PD trên production đi qua PC ticket.
- **Dịch vụ bán kèm:** Trade-in (MX); **Overtrade** (Samsung cộng thêm trên giá thu của đối tác, phải qua Knox); Trade-up (CE; không có ở VN và ID); **SC+** (bundle ở cả 8 nước, standalone, subscription ở VN/SG/ID/AU); Extended Warranty (CE, tài liệu cho Úc); CE Maintenance Pack; SIM plan và Knox Manage (Úc); **RNPL/SR+** (Reserve Now, Pay Later / Samsung Reservation+: mua voucher trị giá X trước khi ra mắt, mở bán được giảm hơn X; trường hợp duy nhất còn voucher; mọi setup phải qua RHQ review; **cấm với S26, Buds4, Z Fold, Z Flip**); Samsung Rewards.
- **Đối tác trade-in (bản mới):** VN **TCV** (không trade-up); PH **Bolttech**; TH **Remobie** (provider code `REMOBILE`, làm tay, không tích hợp); MY **CompAsia**; SG **TIPLUS** (CompAsia, CTDI, Laku6); ID **NBS** (Laku6, ENB; không trade-up); NZ **Assurant**; AU **Asurion**.
- **Các bên:** RHQ SEAO (product owner, duyệt PC ticket và yêu cầu ở ON HOLD RHQ, họp tuần); 8 công ty con (tạo ticket, duyệt ở PLANNING REVIEW, trả lời ở ON HOLD SUBS, xem kết quả ở REVIEW SETUP); HQ Suwon (header ImpEx bắt buộc, hướng dẫn add-on page, freeze plan flagship); L2/L3 SDS India; đội phát triển (BA phía Spoke, đội release toàn cầu: enhancement, kickoff BVT, sửa defect); middleware 3PD; đối tác ngoài; **SDSAP** (đơn vị vận hành hiện tại, bàn giao cho BiPlus, dịch vụ kết thúc **30/11/2026**).

## Chương 02. Thành phần hệ thống
- Hybris là trung tâm dữ liệu bán hàng; các kênh đọc dữ liệu từ Hybris và gửi đơn về Hybris; sau thanh toán đơn sang N-ERP.
- **Mỗi thành phần giữ gì:**
  - **Hybris**: sản phẩm, giá, tồn kho, promotion, coupon, store, khách, đơn.
  - **AEM**: trang chủ, ưu đãi, FAQ, GNB, Product Finder, BC page. Cronjob `xx-DotComCmsDeltaProductSyncJob` chép SKU mới tạo trên AEM sang Hybris (SKU "tự xuất hiện").
  - **WMC**: quản lý trang EPP 2.0 (store, trang chủ, GNB, SKU hiện trên EPP 2.0).
  - **N-ERP/GERP**: mã hàng gốc, RRP, tồn kho trung tâm, chứng từ bán hàng.
  - **GSCM**: tồn kho dự báo cho pre-order/backorder ở nước bật đồng bộ GSCM.
  - **OMS**: tồn kho kho đại lý và cửa hàng (MY; VN cho kho O2O).
  - Cổng thanh toán; middleware 3PD; Shop App CMS; **Kibana** (log, Tech dùng).
- Giá và promotion luôn ở Hybris, AEM chỉ hiển thị → giá BC page sai thì kiểm Hybris trước.
- **Bên trong Hybris:**
  - Administration Cockpit (gồm cả **PriceInfoChange**, thay đổi giá chờ Knox).
  - **Product Cockpit (PCM)**: upload hàng loạt sản phẩm, special price, product reference, trade-in, SIM plan; chạy Super Sync; mỗi người chỉ tải được template của nước mình.
  - Customer Support; promotion engine + simulator.
  - **Cronjob** (VN: `vn-tokoStockImportUpdateJob` 30 phút, `vn-tokoPriceImportUpdateJob` kéo giá N-ERP 2 giờ một lần, `vn-tokoTransferConsignmentToWarehouseJob` đẩy đơn sang N-ERP; các job khác đẩy sang 3PD, nhập SKU trade-in, gửi mã voucher RNPL, làm báo cáo).
  - **Toko config** (công tắc key-value của nền tảng Toko, ví dụ `knox.price.approval.disabled.<storeID>` = `false` thì giá phải chờ Knox; công tắc để thế nào thì quy định vẫn là mọi giá/promotion qua Knox).
  - **HAC**: chỉ Tech.
- **Hai cluster:** **SMS** (`el3`): VN, TH, ID, MY, SG, PH, NZ, cùng Đài Loan, Hồng Kông. **SMA** (`el5`): AU, cùng Nhật. NZ thuộc SMS (trang KB cronjob và danh sách Base Store SMS staging có `nz`; bảng ở trang Login Instructions thiếu NZ). KB tiêu đề `[SMS]` chỉ cho SMS, `[SMS|SMA]`/`[SMS/SMA]` cho cả hai. Mỗi cluster có Backoffice, HAC, cronjob riêng; thay đổi ở SMS không tự có ở AU. Ví dụ job xóa product reference hết hạn chỉ chạy cho NZ, TH (SMS) và AU (SMA). URL `samsungel3` = SMS, `samsungel5` = SMA; `s1`, `s2` là staging. Cả hai cluster nối N-ERP bằng cùng nhóm cronjob (gửi consignment, lấy cập nhật giao, gửi thanh toán/tài chính, nhập giá và tồn kho); job `MktCPI` đẩy khách, đơn, sản phẩm sang SAP Marketing Cloud.
- **Catalog:** master giữ dữ liệu dùng chung (sản phẩm, base product, category, dữ liệu từ AEM/N-ERP), chỉ có Staged, sync xuống Staged của child. Child giữ price row, Sales status, Approval, delivery mode, product reference, merchandising flag; có Staged và Online. Một SKU = 1 dòng master Staged + 1 Staged + 1 Online cho mỗi child. Child catalog theo nước: đa số có Estore, EPP, SME/SMB; VN, TH, MY, ID, AU có 3PD (AU thêm 3PD Clearance); VN có EaRetail và Refurbished; SG có Financing. Tra trang "SEAO Multistore Site Matrix". Ví dụ SKU SC+ bán trên sàn chỉ Approved + Purchasable ở catalog 3PD, Unapproved ở catalog khác.
- **Base store → Website → Multistore:** base store là quy định chung của nước (ví dụ "Toko MY Store": tiền tệ, kho, delivery mode, payment mode); website (CMSSite) là một site cụ thể (`my`, `my_ea_er1`) lấy từ base store và ghi đè một phần; multistore là cấu hình cho nhóm khách khép kín (site EPP/SMB có một bản ghi Website và một Multistore cùng mã). Hybris kiểm **multistore → website → base store**.
  - Ví dụ `my_ea_er1`: base store và website đều có Online banking, Samsung Rewards, Samsung Finance; multistore chỉ có Online banking, Samsung Finance → khách không thấy Rewards.
  - Vị trí cấu hình: Delivery mode ở Base store/Multistore › Administration › Delivery Modes, Website › `CMSSite.deliveryModes`. Giới hạn số lượng: Max Number of Cart Entries (base store, website), Product Quantity Max Limit (website), Cart restriction › Cart Quantity Limit (multistore). Ẩn sản phẩm: Multistore › Properties › Excluded Products (chọn SKU bản Online).
  - Delivery mode gán theo SKU ở mọi nước, riêng VN theo category.
- **BN1** (chương 01–02): gập tài liệu, vẽ sơ đồ kiến trúc (kênh ở trên, Hybris giữa, hệ thống phía sau ở dưới, mũi tên có nhãn dữ liệu) và bảng 3 cột (thành phần, giữ dữ liệu gì, CoE gặp khi nào). Đạt khi có đủ 6 kênh, middleware 3PD, N-ERP, OMS, cổng thanh toán, đối tác dịch vụ, kho; AEM vẽ là nguồn nội dung và SKU mới, không phải nguồn giá; bảng ≥ 6 thành phần. Thực hành: so payment mode ở 3 cấp của một site EPP (ví dụ `my_ea_er1`).

## Chương 03. Sản phẩm, giá, tồn kho

### Loại SKU
- Hai tầng: **base product** (`TokoProduct`, ví dụ "Galaxy S26": tên, mô tả, category; không giá, không tồn, không mua được) và **variant** (`TokoVariantProduct`, SKU bán thật). Category chỉ gắn vào base product.
- Trường **Product Type** (tab Administration): `NORMAL`, `GHOST`, `NON_SAMSUNG`, `EXTERNAL_SERVICE`. SKU tạo từ AEM mặc định NORMAL.
  - **Normal**: có mã N-ERP; RRP và tồn đồng bộ từ N-ERP.
  - **Z-Code**: không phải hàng tồn kho Samsung (lắp đặt, quà, hàng hãng khác, ví dụ `Z-INSTALL-REF-170`). Là GHOST (không vật lý/quà, không có trên N-ERP) hoặc NON_SAMSUNG (subs quyết định có đăng ký N-ERP). Không chạy Super Sync; subs cung cấp RRP và ảnh; delivery mode theo máy chính; tự tạo stock level.
  - **F-Code**: bundle nhiều sản phẩm dưới một mã. Purchasable nếu có trang mua AEM; thành phần không bán lẻ để PDP Not Available.
  - **T-Code**: mã máy cũ trade-in (EXTERNAL_SERVICE ở TH). Tạo bằng cronjob từ đối tác (MY CompAsia, PH Bolttech, VN TCV, NZ Assurant); TH upload tay (Remobie); AU T-code mới từ Asurion tự upload với Approved. Gắn vào máy mới qua product reference.
  - **SC+**: NORMAL hoặc EXTERNAL_SERVICE tùy loại; mã mới dạng `{SUBS}-{loại SC+}-{kiểu thanh toán}-...`, ví dụ `SMC-VN-BUNDLE-UPFRONT`.
  - **External service** (SIM plan, Knox Manage): `Is blocked for Price Import` và `Is blocked for Stock Import` = TRUE; gắn qua `AVAILABLE_SERVICE`.
- **Định dạng mã:** viết hoa, không chữ thường, dấu cách hay `+`; một số CE có `/` (`RF59C766FB1/SV`); mã dịch vụ dùng `-` hoặc `_`. `SC+ S25` sai hai chỗ.

### Trạng thái và CTA
- **Sales status**: `PURCHASABLE`, `PURCHASABLE_NOT_VISIBLE` (mua được, không hiện ở trang danh sách, không link sang trang mua), `PDP_NOT_AVAILABLE`, `ARCHIVED`. **Approval**: `APPROVED`, `UNAPPROVED`, `CHECK` (sản phẩm upload qua Product Cockpit lúc đầu chưa duyệt). Cả hai đặt riêng cho từng child catalog.
- **CTA**: Purchasable + Approved + còn hàng = **Buy now**; có add-on page = **Continue**; đang pre-order = **Pre-order now**; hết hàng = **Notify me** (khi có hàng, cronjob `xx-tokostocknotificationjob` gửi email); Purchasable + Unapproved = **Where to buy**; Archived + Unapproved/Check = không nút (EPP không tìm thấy trong multistore); chưa có trên Hybris nhưng có trang AEM = **Coming soon**; Purchasable Not Visible + Approved = mua được nhưng không hiện ở danh sách; PDP Not Available + Approved = chỉ bán qua sản phẩm khác (thành phần bundle, trade-in, SIM plan).
- QA kiểm nhãn tiếng địa phương trên BC page EPP: Coming soon = Sắp ra mắt / เร็วๆนี้ / Segera Hadir; Continue = Tiếp tục / ดำเนินการต่อ / Lanjutkan; Where to buy = Mua ở đâu / ฉันจะหาซื้อได้ที่ไหน / Lokasi pembelian.
- **Trạng thái chuẩn theo loại SKU (child catalog), ngừng bán thì mọi loại về Archived + Check/Unapproved:**

| SKU | Đang bán |
|---|---|
| Normal | Purchasable + Approved |
| Z-code quà tặng (FOC) | Purchasable Not Visible + Approved |
| F-code | Purchasable + Approved (PDP Not Available nếu không có trang mua AEM) |
| Thành phần F-code không bán lẻ / có bán lẻ | PDP Not Available + Approved / Purchasable + Approved |
| SC+ bundle | Archived + Approved |
| SC+ standalone | Purchasable Not Visible + Approved |
| SC+ standalone EXT | Archived + Approved |
| T-code | PDP Not Available + Approved |
| SKU không có trang AEM | Purchasable Not Visible + Approved |
| SKU embargo | Purchasable Not Visible + Approved, chỉ khi công ty con đồng ý |

- **T-code, nguồn không thống nhất:** bảng Product Active/Archive ghi Archived + Check/Unapproved kể cả khi đang dùng; Product Normalization và trang trade-in MY, TH ghi Approved + PDP Not Available (thiếu thì trade-in không vào giỏ ở MY). Làm theo runbook nước, chưa rõ thì hỏi Lead.
- **Embargo:** trước ngày ra mắt có thể để Purchasable Not Visible + tồn kho ảo để QA promotion; phải xin công ty con đồng ý và ghi trên ticket.

### 9 bước setup SKU mới (mỗi nước có trang "Fundamental SKU setup" và runbook)
1. **Nhận yêu cầu**: đối chiếu file với template RHQ (SKU, base code, category, giá, ngày bán). Lỗi: subs dán bảng thẳng vào ticket, thiếu cột.
2. **Tạo SKU**: thường đến từ AEM qua `xx-DotComCmsDeltaProductSyncJob` (email "Updated Products Report"); nếu chưa có thì upload Product Cockpit › Product bằng template `[mã nước]ProductCatalog` (modelCode, modelName = base code, category, unit = pieces). Lỗi: sai định dạng mã, sai base code, category không phải cấp thấp nhất.
3. **Super Sync và dữ liệu (master)**: Super Sync DOTCOM, PRICE, STOCK, IMAGE cho SKU Normal; kiểm category, Product Type, `Required Additional Info` (IMEI cho điện thoại), external service type. Lỗi: DOTCOM lỗi vì trang AEM chưa publish; sai Product Type cho quà/dịch vụ; chạy Super Sync cho Z-code.
4. **Duyệt và sync xuống child**: duyệt và kích hoạt base product trước, rồi variant; sync master xuống Staged các child.
5. **Giá, tồn kho**: kiểm RRP, thêm special price (qua Knox), kiểm Stock Level đúng kho; Z-code và dịch vụ tự tạo stock level. Lỗi: Super Sync PRICE lỗi mà không báo subs; nhập tồn ảo mà chưa chặn import.
6. **Giao hàng, reference**: gán delivery mode (theo SKU; VN theo category), thêm reference (phụ kiện, SC+, trade-in, quà, gợi ý) ở child catalog.
7. **Trạng thái**: Approval và Sales status từng child theo thời điểm (trước ra mắt để QA, đến giờ mở bán thì bán). Lỗi: bật Purchasable quá sớm.
8. **Sync** Staged → Online ở từng child.
9. **Kiểm tra** ngoài web (trang sản phẩm, giá, CTA, add-on page, giỏ), kiểm lại mỗi đợt go-live. Lỗi: chỉ kiểm trên Backoffice.

### Ra mắt sản phẩm và add-on page
- HQ ban hành **add-on page guide** (khoảng 5 tab bắt buộc và SKU bắt buộc từng tab). Subs được thêm, không được thiếu. Non-flagship (Watch, Buds) thường đơn giản.
- Mỗi tab add-on là một category mã bắt đầu `AEM_` trong master catalog (ví dụ `AEM_SENZ_RECOMMENDED`). Gắn phụ kiện bằng reference `ACCESSORIES`, rồi Administration Cockpit › Categories › tìm `AEM_` bản Master › tải Excel lưu lại › thêm SKU › Upload Products chọn **APPEND** (không chọn thì danh sách cũ bị xóa) › sync đến Online. Kiểm bằng nút **Continue** ngoài web. Z-code quà chỉ hiện trên add-on page khi bọc trong F-code.
- **Freeze plan** flagship (Galaxy S, Z Fold, Z Flip): soft freeze (ngoại lệ cần phê duyệt); hard freeze (chỉ việc liệt kê trong plan; subs luôn được cập nhật tồn kho); **Hybris hard freeze** thường 2–3 ngày sau Galaxy Unpacked; Shop App freeze. Đọc freeze plan trên trang của đúng flagship. Ngoại lệ: CoE lấy bằng chứng phê duyệt từ trang compliance ghi vào Description ticket; không có phê duyệt thì không làm. **Freeze không dừng đồng hồ SLA.**

### Product reference
- `ACCESSORIES` (phụ kiện, cũng là liên kết sang add-on page); `AVAILABLE_SERVICE` (SC+, T-Code, trade-up, SIM plan, Knox Manage); `AUTO_ADDED_SERVICE` (SC+ standalone tự thêm SKU EXT; SC+ luôn đi cùng máy); `MUST_PURCHASE_WITH` (hard bundle: dàn nóng/lạnh điều hòa, tủ lạnh kèm `Z-INSTALL-REF-170` ở MY); `CONSISTS_OF` (máy sấy kèm `Z-INSTALL-DV-200` ở MY, F-code kèm quà Z-code); `SELECTION_OF_BUNDLE` (benefit COMBO); `SELECTION_OF_GIFT` (chọn quà trên add-on page); `RECOMMENDED_PRODUCT`; `SELECTION_OF_RECOMMEND` ("Frequently Bought Together" trên BC page).
- Tạo một SKU: SKU child bản Staged › Category System › Product References › tạo mới (ngày hết hạn ở tab Administration) → sync. Hàng loạt: Product Cockpit › Bulk Upload › `PRODUCT_REFERENCES` (SourceCode, ReferenceType, Active, targetCode, excludedSites, startDate, endDate, commercial flag). `SELECTION_OF_RECOMMEND` và `RECOMMENDED_PRODUCT` cần thêm bản ghi `AEMAdditionalInfoTypeData` bật enabled.
- Giỏ bỏ qua reference Active = FALSE (MY: chọn được máy cũ trong pop-up nhưng trade-in không vào giỏ). NZ, TH, AU có cronjob dọn reference hết hạn/không active.

### Giá
- **RRP** từ N-ERP (VN cronjob 2 giờ một lần) hoặc Super Sync PRICE; PRICE lỗi thì subs làm với team N-ERP, gấp thì CoE upload RRP bằng file. Giữ RRP nhập tay phải bật **Is blocked for Price Import**; ở AU chặn import cần RHQ đồng ý.
- **Special price** = price row loại `SPECIAL` có ngày; hiện thành giá bán trên PDP, PLP, giỏ (giỏ hiện số tiền tiết kiệm); thường đặt ở child catalog. Một SKU: Products › SKU Staged › tab Prices › Create a new price row › Edit Details (catalog version Staged, price type SPECIAL). Hàng loạt: Product Cockpit › Special Price › tải template catalog mình › Import.
- **Quy tắc template giá:** mỗi dòng một SKU; chỉ điền `price` hoặc `discountPercent`; `cmsSite` viết thường, cách nhau dấu phẩy, không dấu cách (lấy từ Site Matrix); `minqtd` = 1; `validityFrom`/`validityTo` dạng text `YYYY-MM-DD HH:MM:SS` **theo GMT** (VN bắt đầu 00:00 ngày 1/12 giờ địa phương → nhập `2025-11-30 17:00:00`).
- **Knox cho giá ngay trong Hybris:** upload giá hoặc đổi price row, discount row, discount multistore → "Price Information Change Detected" → bản ghi **PriceInfoChange** trạng thái VALID → chọn dòng (tối đa **300 dòng** một lần) › Submit Price Change Info Approval › Title, Comment › đường duyệt (MX, VD, DA) › xuất Excel lưu › OK. Trạng thái: VALID → KNOXPENDINGAPPROVAL → KNOXAPPROVED (`knoxPromotionStatusJob`) → COMPLETED (`knoxPriceApplyingJob`). Chỉ khi COMPLETED price row mới vào Staged; sau đó sync và kiểm web. Giảm sâu thì đường duyệt dài; Hybris chọn đường theo mức giảm cao nhất trong lần gửi. Sửa lại giá trên Staged tạo PriceInfoChange mới, phải duyệt lại.
- **Was price** (giá gạch) lấy từ lịch sử giá, không từ trường "Was value"; sai thì Tech kiểm bảng price audit.
- **Rủi ro:** việc giá là mức **R3** (kiểm nội bộ với brief, price sanity, QA, Shift Leader duyệt). File giá **≥ 500 SKU là E4**, cần thêm Merchandising Lead hoặc Deputy duyệt. Bulk upload **> 100 dòng** cần file diff và chạy thử. Mọi giá/promotion qua Knox theo đường duyệt trong brief, kể cả yêu cầu gấp.

### Tồn kho (Base Commerce › Stock Level, theo SKU và kho)
- `availableAmount` (hàng thật; cronjob N-ERP hoặc Super Sync STOCK; bị ghi đè mỗi lần import nếu không chặn); `reserved` (Hybris giữ cho đơn chưa giao); `safetyStock`; `maxPreOrder` (Merch, không import từ N-ERP); `oversellingAmount`, `oversellingShippingDate` (Merch; Hybris không ghi đè; nước bật GSCM có thể lấy backorder từ GSCM); `promoStockAvailable` (chỉ cho mua theo bundle), `promoStockReserved`; `inStockStatus` (`NOTSPECIFIED`, `FORCEINSTOCK`, `FORCEOUTOFSTOCK`, trống; ví dụ Knox Manage để FORCEINSTOCK).
- **Số bán được** (không pre-order/overselling) = available − reserved − safety stock, ví dụ 40 − 12 − 5 = 23.
- **Chỉ `availableAmount` bị import ghi đè**; pre-order và overselling nhập thẳng được. Tự đặt `availableAmount` (SKU embargo, Z-code, SKU lỗi sync STOCK) thì chặn import trước bằng một trong ba cách: **Is blocked for Stock Import** trên sản phẩm (mọi kho thường); **Stock Import Override** (một SKU, một store, một kho; quản bằng ImpEx `TokoStockImportOverrideConfig`, trên production là việc Tech có PC ticket); ở VN **Is blocked for Stock Import for OMS** cùng Toko config `toko.oms.warehouses.vn` cho kho O2O lấy tồn từ OMS. Hỏi subs trước khi chặn.
- Upload hàng loạt: Stock Level › **Stock Level File Upload**, template KB, file `.xlsx` tên `XX-prod_StokLevel`, kiểm lại sau khi upload.

## Chương 04. Promotion, coupon và dịch vụ đi kèm

### Vòng đời promotion
- Merch dựng promotion **trên production**, theo ticket có QA và duyệt. Rule mới luôn **Unpublished**. Mỗi promotion publish **hai lần**:
  - **Publish preview** vào `preview-promotion-module`: chỉ phục vụ simulator, khách không thấy, không cần Knox.
  - **Publish live** vào module nước (`vn-promotions-module`, `nz-promotions-module`): khách thấy, mở luồng Knox.
- Đường đi: dựng rule theo brief (Unpublished) → publish preview → simulator, Doer internal check, QA kiểm, Shift Leader duyệt → đến giờ go-live publish live (rule giảm giá mở popup Knox) → KNOXPENDINGAPPROVAL → KNOXAPPROVED → **PUBLISHED** (chỉ PUBLISHED mới chạy) → kiểm storefront lúc go-live; ticket nhiều ngày bắt đầu thì mỗi đợt go-live QA lại trên production.
- Rule gồm **Rule properties** (mã duy nhất không sửa được, tên, website, rule group, priority, ngày, mục Approval), **Conditions**, **Actions**. Ba cách tạo: tạo mới (Marketing › Promotion Rules › "+"), clone (giữ nguyên tên, rule group, website, điều kiện, hành động, nên kiểm lại từng ô), từ template (Marketing › Promotion Templates). Mỗi lần lưu và publish lại tạo phiên bản mới, bản cũ ngừng. Gỡ khỏi module bằng **undeploy**.

### Knox approval cho promotion (CM-13 §10: mọi giá, mọi promotion)
- Approval path khác theo công ty con và MX/CE; dùng đúng cột approval path trong brief, không tự chọn; yêu cầu gấp cũng gửi Knox.
- Cách làm: điền Approval Title, Approval Description, Business PIC → publish vào module nước → popup **Request for Discount Promotion Approval** → chọn Approval Process (MX, VD, DA) → rule thành **KNOXPENDINGAPPROVAL** (theo dõi ở Knox Portal › Approval › Submission) → `knoxPromotionStatusJob` (**45 phút**) chuyển **KNOXAPPROVED** → cronjob publish (45 phút) chuyển **PUBLISHED**. Từ lúc người cuối duyệt tới lúc chạy có thể mất **~1,5 giờ**. Publish nhiều rule một lúc thì path theo rule giảm sâu nhất.
- Có thể sai: bị từ chối → KNOXREJECTED (sửa thì sinh phiên bản mới Unpublished, gửi lại); withdraw → về UNPUBLISHED; **hai phiên bản cùng KNOXAPPROVED khi cronjob chạy → cả hai INACTIVE, không bao giờ để xảy ra**; publish hàng loạt nhiều Business PIC → ai cũng phải duyệt, một người từ chối là cả lô bị từ chối; trộn rule giảm giá và không giảm giá trong một lô → Hybris chặn ("Discount Promotion and Non-Discount Promotion are mixed"); ngày đặt bằng campaign → Period không hiện trong approval; dùng qualifying categories → mọi SKU trong category hiện trong approval.
- Hybris chỉ mở popup cho **action giảm giá** (giỏ, sản phẩm, sản phẩm đi kèm, phí giao). Action không giảm giá (tặng quà, thông báo, halt, external voucher) không có popup, nhưng CM-13 vẫn đòi Knox → hỏi Shift Leader cách gửi (nguồn khác nói khác: hai trang KB Knox ghi promotion tặng quà/không giảm giá không cần duyệt; chờ RHQ xác nhận).
- Khi chờ Knox ghi rõ trên ticket thời điểm gửi và path; **không chuyển ON HOLD SUBS chỉ để dừng đồng hồ**.

### Thay đổi nào phải xin Knox lại (rule đã publish)
- **Có**: ngày giờ bắt đầu/kết thúc, website, điều kiện, hành động, thêm hoặc bỏ campaign.
- **Không**: tên, priority, description, message; approval title/description; cờ rewards boost, quota, funding type, cost centre.
- **Campaign** chỉ dùng khi một rule cần nhiều khung giờ trong một giai đoạn. Muốn đổi/gia hạn ngày: bỏ campaign cũ, tạo campaign mới, gửi Knox mới. **Sửa ngày campaign đang dùng để né Knox là vi phạm.**

### Promotion simulator
- Công cụ Back Office 2.0 (nằm trong Backoffice Extension, không có ở menu chính; không phải staging nào cũng có), đọc rule từ `preview-promotion-module`.
- Bước: chọn Country, Language, Catalog Version, Site, ngày giờ giả lập → thêm SKU, số lượng, coupon → Simulate, đọc promotion áp, tiền giảm từng dòng, giá cuối → chạy giỏ **không** đủ điều kiện (SKU ngoài danh sách, ngay dưới ngưỡng, ngay trước giờ bắt đầu và ngay sau giờ kết thúc, site/nhóm khách không đủ) → chạy giỏ có promotion khác để xem cộng dồn.
- Nhập giờ theo **múi giờ thị trường** (rule SG dựng theo giờ VN lệch 1 tiếng). Bằng chứng: chụp trên máy trạm, gom PowerPoint, đính ticket (CM-10). Không dùng được simulator thì thử bằng nhóm khách test trên storefront hoặc Special Price Report.

### Điều kiện hay dùng
- Container (nhóm điều kiện X, Y cho action trỏ tới); Qualifying products/categories; **Carts with voucher codes** (dùng cho coupon; giới hạn lượt dùng đặt trên coupon); Cart total, **Category Price Threshold** (đọc **tổng cả giỏ**, kể cả sản phẩm ngoài category); Target customer/customer group (Merch không tạo được: Tech tạo qua COEC, subs gửi danh sách bằng email có mật khẩu); Payment mode, Included BIN (thường 6 số đầu, upload hàng loạt chỉ chữ số); Qualifying sites (cho EPP); Qualifying service types/products/params/providers (ví dụ chỉ chạy khi giỏ có TRADE_IN, không chạy khi có trade-up).

### Website và rule group
- Ô **Website** ghi promotion group: B2C `vnPromotionGroup`, `nzPromotionGroup`, `sgPromotionGroup`; EPP/SMB `vneppChannelPromotionGroup`, `pheppChannelPromotionGroup`, `smbPromotionGroup`. Sai nhóm là chạy sai site hoặc không chạy.
- **Rule group**: nhóm loại trừ (`exclusivePackagePromotionGroup`) chỉ rule priority cao nhất áp; nhóm thường (`productPromotionRuleGroup`, `orderpromotiongroup`) cộng dồn, priority cao chạy trước. Quy ước từng nước ở trang Common Promotion Setup.

### Action hay dùng
- Percentage discount (biến thể RRP tính trên RRP); Fixed discount; Target fixed price (PH giới hạn 1 sản phẩm/category); Distributed discount; Partner product discount (%, % trên RRP, cố định); Cart discount (coupon, promotion thanh toán); **Free gift based on available stock and priority** (FOC, BOGO; **Stock Check Type**: CHECK_PROMO_STOCK đọc Promo Stock Available, CHECK_STOCK_AVAILABILITY đọc Available Amount, DISABLED luôn tặng món đầu tiên); Trigger rule message, Halt rule execution; Enable zero payment (NZ checkout 0 NZD).

### Naming convention và các yêu cầu RHQ cấm
- Tên: `{Country}_{Site}_{Platform}_{Category}_{StartDate}_{EndDate}_{PromotionType}_{free text}`. Country: SG, MY, ID, TH, VN, PH, NZ, AU. Site: B2C, EPP, SMB, O2O, EA. Platform: WEB (web và app), APP, CRP, ePromoter, LS. Ngày `ddMMMyy` (`01FEB25`). Free text dùng `-`, không `_`. Type: BOGO, PWP, BMSM, EV, PROMOTEXT, REWARDS, DISCOUNT, PAYMENT, SHIPPING, SIM, TRADE-IN, RNPL (CRP thêm PPX, ESG, NRM). Ví dụ `VN_B2C_WEB_SP_01FEB25_28FEB25_BOGO_S25Series`. Sai tên là lỗi RHQ bắt nhiều nhất.
- **Cấm:** promotion theo nền tảng (chỉ app hoặc chỉ web) từ 1/12/2025 (Hybris chặn điều kiện sales application, loại thiết bị, voucher chỉ cho mobile); overtrade bằng promotion rule (trừ SAVINA); RNPL trên S26, Buds4, Z Fold, Z Flip (và RHQ xem trước mọi setup RNPL).

### Priority và cộng dồn
- **VN** (cao → thấp): Package 600 và FOC 600 (`exclusivePackagePromotionGroup`, chỉ một áp); Ecobundle 400–500; coupon cấp sản phẩm 200–300; coupon cấp giỏ/lần mua sau 50–100; promotion thanh toán 0–30 (các nhóm sau dùng `productPromotionRuleGroup`). Thứ tự khách thấy: single price → package/FOC → giảm trực tiếp → welcome instant discount → coupon marketing → promotion thanh toán.
- **SG eStore**: mốc First purchase **303**; % trên RRP, target fixed price 304–500; % trên giá promo, giảm cố định 100–299; distributed 10–99; BOGO 100–500 tùy trường hợp; halt và always-on ≥ 1000. SG EPP mốc first purchase **203**, loại khác 204–500.
- **Ví dụ:** RRP 20.000.000; A giảm 10% (priority 400), B coupon −500.000 (priority 250), cùng nhóm thường → 18.000.000 → **17.500.000**. Nếu cùng nhóm loại trừ → chỉ A, còn 18.000.000, coupon vô tác dụng. QA so kết quả cộng dồn với brief.

### Coupon và voucher
- Từ 1/5/2026 mọi promotion có mã dùng **coupon** (Marketing › Coupon Management › Coupons). Single coupon: tổng số lần và số lần mỗi khách, có thể hiện ở My Voucher. Multi coupon: mỗi khách một mã, định dạng RHQ (`CEOD-5BM9-9GML-GCNK`), có thể nạp sang GCDM hoặc import dạng mã ngoài.
- **Luôn đặt đủ ba giá trị:** mức giảm, tổng số lần dùng, số lần mỗi khách. Để trống là vô hạn → sanity hold, dừng lại sửa.
- Số lượng: KB Coupon ghi Merch sinh được tới **1 triệu mã** trong Backoffice; không sinh được thì Tech dùng ImpEx: Merch giữ ticket, tạo COEC liên kết, chuyển ticket sang ON HOLD COE, phần Tech đi PC ticket (nguồn khác nói khác: ví dụ RHQ trong CM-13 lấy 500.000 mã là mức cần ImpEx; ngưỡng chưa thống nhất).
- **Voucher** (promotional, serial; Backoffice › Vouchers) chỉ còn cho **RNPL**, vì FI posting sang N-ERP chưa nhận coupon là voucher tiền mặt.

### Trade-in, overtrade, trade-up, clawback
- **Trade-in (MX):** máy cũ là SKU T-Code (`T_PHONE_SAMSUNG`, `T_PHONE_APPLE`), Approved + PDP_NOT_AVAILABLE (xem lưu ý mâu thuẫn ở chương 03), gắn vào máy mới bằng `AVAILABLE_SERVICE` Active = TRUE. T-Code vào hệ thống: MY cronjob API CompAsia, AU tự upload từ Asurion, TH Merch upload. Model mới: đối tác thêm bên họ rồi sync về Hybris. ID có lớp **EzTrade** nối nhiều đối tác.
- **Overtrade:** mọi subs trừ SAVINA dùng **tính năng overtrade**, không dùng promotion rule. Khai theo cặp SKU máy mới + T-Code ở Base Store › Administration › AddedService Configs › Discount Configuration, hoặc upload `TRADE_IN_DEVICE_PRICE` (kiểm lại ở Overtrade Discounts Bonus), cuối cùng chạy **Compute Up to Price**. Ví dụ Úc: giảm 540 = 390 Asurion + 150 Samsung. Knox cho overtrade đang "coming soon" trong hướng dẫn RHQ.
- **Trade-up (CE):** giảm số tiền cố định khi đổi đồ điện máy cũ; không có ở VN, ID. Setup: reference `AVAILABLE_SERVICE` tới `T-TRADEUP` + cấu hình trade-in của SKU trong Product Cockpit (category, hãng, số tiền, ngày, site). Cách revamp: External Service Type `TRADE_UP` trên SKU + promotion rule điều kiện Qualifying service types = Trade Up. Web có thể hiện số lớn hơn vì cộng thêm khoản giảm nền theo category.
- **Clawback** (thu hồi khoản giảm khi khách không gửi máy hoặc máy không đúng): chỉ SG, NZ, AU. Trạng thái NZ: NEW, WAIT, RECEIVED, CANCELED (thu hồi toàn bộ), TRADEIN_TIMEOUT (thu hồi toàn bộ), CLOSED, COMPLETED.

### Dịch vụ ngoài bắt buộc khai báo
- Một SKU chỉ hiện dịch vụ trên PDP và giỏ khi khai cả **External Service Type** (tab Administration của SKU) và **AddedService Configs** của base store. RHQ yêu cầu khai đủ: ACCESSORIES, BENEFIT, TRADE-IN (MX), TRADE-UP (CE khi có), INSURANCE (MX khi có), WARRANTY (CE khi có).

### BN2 (chương 03–04)
- Tình huống Thái Lan ra mắt điện thoại: QA được trước ngày ra mắt mà khách chưa thấy; special price 2 tuần; quà Z-Code cho 500 khách đầu; trade-in; sau 2 tuần thêm promotion theo phương thức thanh toán. Lập phiếu setup: SKU và loại, trạng thái trước/sau ra mắt, giá và cách nhập, tồn kho quà, reference, promotion (tên theo convention, điều kiện, hành động, rule group, priority tương đối), publish preview/live, bước cần duyệt, QA kiểm gì.
- Đạt khi: SKU quà đúng loại; trạng thái trước ra mắt cho QA mà khách không thấy; có sync; quà có cách kiểm tồn; trade-in đúng loại reference; tên đúng convention; có thứ tự priority; publish preview → simulator → publish live kèm Knox đúng thứ tự. Mọi promotion kể cả quà phải có Knox; giá qua Knox price approval.
- Thực hành: chỉ xem trên staging, không HAC, không publish vào module nước; chạy simulator với rule người hướng dẫn đã publish preview (một giỏ đủ điều kiện, một giỏ không).

## Chương 05. Đơn hàng và giao hàng

### Order và consignment
- Một **order** tách thành nhiều **consignment** khi khác kho hoặc khác delivery mode (một số nước tách thêm theo ngành hàng/division). Mỗi consignment có kho, delivery mode, trạng thái, tracking riêng; **N-ERP tạo một SO cho mỗi consignment**. Order entry giữ giá; consignment entry giữ số lượng cần giao.
- `PAYMENT_AUTHORIZED` và `PAYMENT_CAPTURED` chỉ thuộc order. Sau capture và tách, order theo consignment **chậm nhất**; chỉ hoàn tất khi consignment cuối xong và bút toán tài chính đóng.
- `ORDER_SPLIT` là trạng thái order lúc tạo consignment (bước tên `splitOrder`); `DELIVERED` là trạng thái consignment. Đơn 3PD theo quy trình dropship riêng; đơn voucher RNPL dùng delivery mode giao số.

### Order process (tên bước thật, Tech xem ở tab Administration)
1. `sendOrderAcknowledgementEmail` → `CREATED`.
2. `checkExternalEnabled`, `checkOrder`, `compensationApprovalCheck` → `CHECKED_VALID`/`CHECKED_INVALID`; `WAIT_FOR_CHECK_EXTERNAL` với payment mode cần cổng duyệt.
3. `fraudCheck`, `fraudCheckExternal` (FraudConfig, quota, mã dùng một lần, rồi fraud ngoài) → `FRAUD_CHECKED`, `WAITING_FOR_EXTERNAL_FRAUD_RESULT`, `EXTERNAL_FRAUD_RESULT_PROCESSED`, `WAIT_FRAUD_MANUAL_CHECK`.
4. Manual price check (khi thuộc diện; CS agent duyệt/từ chối) → `WAIT_FOR_MANUAL_PRICE_CHECK`, `APPROVED_/REJECTED_MANUAL_PRICE_CHECK`.
5. `reserveVirtualStock`, `shouldHaltPreOrderBeforeCapture` → `WAIT_PRE_ORDER_BEFORE_CAPTURE`.
6. `processExternalServicesOnConditionAction` (trade-in, SC+, SIM trước capture) → `WAIT_FOR_EXTERNAL_SERVICE_PROVIDER`.
7. `takePayment`, `checkAsyncCaptureResult`, `isCaptureSuccessfulAction` → `WAITING_FOR_CAPTURE_RESULT` → `PAYMENT_CAPTURED`.
8. `processExternalServicesAction` (kích hoạt dịch vụ sau capture) → `WAITING_FOR_EXTERNAL_SERVICE_PROCESS`.
9. `sendFinancialUpdate`, `isInitialFISuccess` (FI đầu sang N-ERP) → `WAITING_FOR_SEND_FINANCIAL`.
10. `splitOrder`, `waitForWarehouseSubprocessEnd` → `ORDER_SPLIT`.
11. Theo dõi consignment → `SHIPPING_REQUESTED`, `SHIPPING_PREPARATION`, `SHIPPED`.
12. `isFullyFulfilled`, `isSecondFIRequired` (FI lần hai khi đổi hàng, clawback, hủy một phần) → `WAITING_FOR_FINANCIAL`.
13. `completeFinancialUpdate`, `isOrderComplete`, `sendThankYouMessage` → `COMPLETED`.
- Short pick, hủy, hoàn tiền rẽ nhánh từ dòng chính.
- **Consignment process:** chờ khách bổ sung/món đi kèm → cập nhật tồn, gom đợt → gửi sang kho/3PL qua N-ERP (`WAITING_FOR_TRANSFER` đến lúc gửi; N-ERP trả SO = `SHIPPING_REQUESTED`) → ghi giá vốn, trừ kho, báo khách/cửa hàng → DO = `SHIPPING_PREPARATION`, GI đầu = `SHIPPED` → giao có lịch, chặng cuối, `READY_FOR_PICKUP`, nhắc nhận hoặc tự hủy khi quá hạn → thu tiền từng phần (lỗi `PARTIAL_CAPTURE_FAILED`), SMS/email → N-ERP gửi billing, consignment xong, order `WAITING_FOR_FINANCIAL` → `COMPLETED`.

### Trạng thái đơn hay gặp
- Khởi tạo `CREATED`; kiểm tra `CHECKED_VALID`, `CHECKED_INVALID`, `WAIT_FOR_CHECK_EXTERNAL`; thanh toán `PAYMENT_AUTHORIZED`, `PAYMENT_NOT_AUTHORIZED`, `WAITING_FOR_CAPTURE_RESULT`, `PAYMENT_CAPTURED`; gian lận (4 trạng thái ở bước 3); kiểm giá (3 trạng thái); pre-order/dịch vụ `WAIT_PRE_ORDER_BEFORE_CAPTURE`, `WAIT_FOR_EXTERNAL_SERVICE_PROVIDER` (SIM/broadband tới 24 giờ, SMC ~60 giây), `WAITING_FOR_EXTERNAL_SERVICE_PROCESS`; tài chính `WAITING_FOR_SEND_FINANCIAL`, `WAITING_FOR_FINANCIAL`; giao `ORDER_SPLIT`, `SHIPPING_REQUESTED`, `SHIPPING_PREPARATION`, `SHIPPED`, `READY_FOR_PICKUP`; từng phần `PARTIAL_SHIPPING_REQUESTED/PREPARATION`, `PARTIAL_SHIPPED`; kết thúc `COMPLETED`, `CANCELLED`, `REJECTED`; có vấn đề `SUSPENDED`, `PROCESSING_ERROR`, `FAILED_CHECK_EXTERNAL` (Tech xem); bỏ dở `TEMPORARY` (xóa sau "Temporary Order Removal Timeout Hours" của payment mode).
- Trả hàng: `RETURN_REQUESTED` → `RETURN_SHIPPING_REQUESTED` (RSO) → `RETURN_SHIPPING_PREPARATION` (RDO) → `RETURN_COMPLETED`, `RETURN_REFUNDED`; hoàn tiền lỗi `REFUND_FAILED`.
- My Account: `SHIPPING_REQUESTED` = Preparing order (SG) / Delivery requested (VN) / SO; `SHIPPING_PREPARATION` = Awaiting dispatch / Prepare for delivery / DO; `SHIPPED` = On the way / Delivering / GI đầu.

### Chỗ đơn hay kẹt
- `CREATED` quá lâu: node khởi động lại/deploy ("failed to respond") → chạy lại từ bước dừng (dừng trước `fraudCheck` thì chạy lại từ `fraudCheck`).
- `EXTERNAL_FRAUD_RESULT_PROCESSED`: ở `takePayment` cổng không trả mã giao dịch → hỏi subs đã authorize chưa; nếu rồi đặt transaction entry thành công rồi chạy lại. **Trước khi chạy lại `takePayment`, kiểm chưa có entry CAPTURE, nếu không khách bị trừ tiền hai lần.**
- `WAIT_FRAUD_MANUAL_CHECK`: trúng rule Review → subs/CS agent quyết, CoE không quyết.
- Lỗi ở `processExternalServicesAction` (đối tác trade-in không trả lời: "responseData is null", "Connection reset") → chạy lại từ bước đó.
- `PAYMENT_CAPTURED`, lỗi `incrementWtVolQtyDailyUsage`: SKU (thường SC+) không có delivery mode → thêm vào order entry, chạy lại.
- `WAITING_FOR_EXTERNAL_SERVICE_PROCESS`: đối tác không phản hồi hoặc SC+ trả "INVALID BILL DATA" (sai PID) → xác nhận PID mới, sửa, chạy lại.
- Bước tài chính (`completeFinancialUpdate`, `isInitialFISuccess`) → chạy lại.
- `ORDER_SPLIT` "missing values for [warehouse]": **ca hay gặp nhất**, không kho nào được phép còn hàng → kiểm tồn từng kho, subs đẩy tồn, chạy lại.
- `ORDER_SPLIT` "getRegion() is null": địa chỉ thiếu mã vùng → subs xác nhận, map vùng.
- `ORDER_SPLIT` "Please input Customer Number": cửa hàng O2O trống ship-to (`pointOfService.GerpShipTo`) → subs cấp mã ship-to đã đăng ký N-ERP.
- `ORDER_SPLIT` "Plant XXXX is not defined": mã ERP plant của kho không khớp.
- N-ERP từ chối khi tạo SO: sold-to không khớp, thiếu RRP, vật tư bị chặn/không thuộc sales area, sai `gerpSchedType`, thiếu mã bưu chính.
- `SHIPPED` quá lâu → chạy lại từ `isFullyFulfilled` hoặc `isProcessCompleted`; thiếu billing thì xin subs. `SUSPENDED` → runbook order remediation.
- **Ai làm gì:** Tech điều tra và sửa; mọi lần chạy lại/sửa dữ liệu đơn trên production cần **PC ticket do Oliver Leung (RHQ) approve**; Groovy/ImpEx phải có header ITGC dòng 1, file mới chạy staging trước (CM-13 §9). Merch và QA báo sớm trên ticket (mã đơn, trạng thái, nguyên văn lỗi), không đụng vào đơn. Subs/CS agent quyết đơn bị giữ và cung cấp dữ liệu nghiệp vụ còn thiếu.

### Chọn kho và tính RDD
- **Chọn kho:** kho gắn site xếp theo priority (TH, PH, SG, NZ): lấy kho priority cao nhất trên website, hết thì kho kế tiếp; site không có kho thì dùng kho base store. Kho theo vùng (VN): kho của base store có trên website, lọc theo vùng của địa chỉ, priority lớn thắng, lấy kho đầu còn hàng; SAVINA có `siteToWarehouseMap` đè lên (miền Bắc WV05-S520 trước WV10-S520, miền Nam ngược lại).
- RDD phụ thuộc kho + mã bưu chính + delivery mode (dùng ERP Delivery Mode, ERP Shipping Condition, ERP S Proc Ind).
- **RDD = ngày đặt + lead time + lead time vận hành kho (`whOpLeadTime`, mặc định 0) + 1 nếu quá cut-off (`cutOffSchedule`, thường 150000 = 15:00) + số ngày không giao + số ngày lễ** (lead time tính ngày lịch, rồi cộng mỗi ngày không giao/lễ rơi trong khoảng).
- Ví dụ mã bưu chính 1400, đặt thứ Tư 12/6/2024, lead time 5: chuẩn (không giao T7, CN) → **thứ Tư 19/6**; sau 15:00 → **thứ Năm 20/6** (5 + 1 + 2 = 8 ngày); 2 ngày lễ 13/6 và 17/6 → **thứ Sáu 21/6**; giao cả tuần → **thứ Hai 17/6**.
- **Dữ liệu:** file LeadTime master (ngày giao trong tuần, cut-off, lead time) và PostCode2XDock (map mã bưu chính → cross-dock), upload ở Types › LeadTime/PostCode2XDock › Search By Type › nút upload, ghi lại tên cronjob hiện ra. Tên file đúng định dạng (`TH Leadtime Master_FINAL_v1.xlsx`, `TH xDock Master_20240401.xlsx`); upload lại thì đổi version; dữ liệu trùng làm upload thất bại; lỗi quyền NASCA thì nhờ L2 qua maintenance ticket. Ngày lễ ở Base Store › Administration › **publicHolidays** (bị khóa trên lịch chọn ngày). Pre-order, overselling, backorder có thể đổi kết quả. Cần cờ TokoConfigProperty `split.order.by.preferred.warehouse.enabled.{country}`, `toko.oversell.leadtime.enabled`; trên delivery mode cần Enable RDD For Non-Calendar và `supportsRequestedDeliveryDates`; nạp lại config là script HAC (Tech, PC ticket trên production).
- Xem RDD trên đơn: Order › Positions and Prices › Order Entries › Requested Time; kho đã chọn (Preferred Warehouse) ở tab Administration của dòng hàng.

### Delivery mode
- Mã chứa mã nước (`sg-delivery-standard-AM`, `vn-o2o-pickup`). Tạo bằng **clone**: mang theo mọi thứ trừ mã và **phí giao** (`ZoneDeliveryModeValue`, tạo tay hoặc ImpEx; ImpEx production là việc Tech có PC ticket).
- Điền đủ **ERP delivery mode, shipping condition, special processing indicator** (subs cung cấp); thiếu một trong ba thì consignment không sang N-ERP và bảng lead time không khớp.
- Gán theo SKU (VN theo category) và bật ở Website/Multistore/Base Store theo ưu tiên; khách chỉ thấy delivery mode vừa gán cho mọi sản phẩm trong giỏ vừa bật ở cấp đang áp dụng.
- Postcode range list ở Delivery costs (trống = mọi mã). **Supported Payment Modes**: TV xe tải chỉ thẻ + điện thoại nhận thẻ/COD trong cùng giỏ → khách chỉ trả được bằng thẻ.
- Trường quan trọng: Identifier, Name; Is Active; Display Calendar; Calendar Group Id; Enable RDD For Non-Calendar; `deliveryTimeSlotSelectionEnabled` (BOPIS); Standalone, Skip Fulfilment, `ZoneDeliveryMode.exclusive` (standalone, giao số); `walkOut` (SAVINA, ví dụ `vn-o2o-Samsung68-walk-out`); `ZoneDeliveryMode.groups`; `toko.ce.delivery.modes.au` (SEAU: mỗi delivery mode mới phải thêm vào).
- Loại hay gặp: giao chuẩn, giao có lịch, kèm lắp đặt, xe tải CE (SENZ), BOPIS (gắn Point of Service), tủ nhận hàng Australia Post, giao số (SMC, voucher RNPL), delivery mode 3PD.

### Payment mode
- Đặt tên theo nước (`vn-pay-at-shop`, `my-iPay88OnlineBankingPaymentMode`), tìm ở Types › PaymentMode. Trường: Active, Identifier, tên, Icon, Supported Delivery Modes, Payment Info Type, payment/response strategy, Payment Provider Parameters (Tech cài), Temporary Order Removal Timeout Hours. Payment mode mới clone bằng Groovy (Tech, PC ticket). Trả góp có `PaymentModeConfig` theo ngân hàng, site, kỳ hạn, mỗi dòng có giá trị giỏ tối thiểu. Loại trừ sản phẩm ở Administration › Restrict Products.
- Bật ở: base store (bắt buộc mọi nước); website (MY, SG, VN, NZ, AU; **PH, ID, TH dùng Site Payment Config**); multistore (EPP/SMB ở MY, SG, VN, NZ, AU). Thêm vào multistore thì cũng phải có ở base store.
- **Khách không thấy phương thức:** (1) Active? (2) có ở cấp đang áp dụng và có trong base store? (3) giỏ đạt mức tối thiểu (trả góp theo ngân hàng/kỳ hạn)? (4) mọi delivery mode trong giỏ có hỗ trợ? (5) Restrict Products có loại trừ? (6) quy tắc riêng nước (VN `vn-pay-at-shop` chỉ hiện với cửa hàng Eligible store `CS_STORE`).

### BN3 (chương 05–06)
- Vẽ luồng đơn eStore từ checkout đến giao xong, tô các điểm hay kẹt kèm nguyên nhân, và tính 3 bài RDD (lead time vận hành kho = 0): (1) thứ Năm 10:00, lead 3, không giao T7/CN, cut-off 15:00 → **thứ Ba**; (2) đặt 16:30 → **thứ Tư**; (3) thứ Hai tuần sau là lễ → **thứ Tư**.
- Đạt khi luồng đúng thứ tự (authorize, gian lận, capture, FI đầu, `ORDER_SPLIT`, SO, DO, GI, billing, hoàn tất), có dịch vụ ngoài trước và sau capture, ≥ 4 điểm kẹt có nguyên nhân và người xử lý, RDD có cách tính từng dòng. Thực hành: xem đơn ≥ 2 consignment, RDD và kho ở dòng hàng, delivery mode, một multistore `sg_`.

## Chương 06. EPP, SMB, O2O, Shop App và 3PD
- Nhận diện kênh trên đơn: EPP (multistore, Site ID `xx_...`, login type, quota); SMB (multistore `isSme` = true); EA (multistore EA, cửa hàng không kho/delivery mode, nhân viên đặt từ user group cửa hàng); BOPIS (Point of Service có kho và delivery mode pickup); 3PD (site, catalog, delivery/payment mode 3PD, đơn đến từ middleware); Shop App (sales application **MOBILEAPP**).

### EPP
- **Site ID:** mã nước 2 chữ thường + `_` + ID subs (`sg_test_epp`, `id_vip_mall`); toàn chữ thường, chỉ chữ, số, `_`, `-`. `SG_bankx_epp` và `sg-bankx-epp` là sai.
- **Login type:** `SSO_DOMAIN` (email theo domain; bộ lọc trên multistore); `EMAIL_OTP`; `SSO_ACCESSCODE`; `SSO_ACCESSCODE_OTP` (access code + OTP SMS/email; SMS chỉ PH, VN); `SSO_HASHACCESSCODE` (link có chữ ký, hiệu lực vài giây); `SSO_GENID` (mã nhân viên); `SSO_VERIFICATIONCODE` (mã dùng chung; **không dùng cho site mới nếu không có lớp giới hạn thứ hai**); `SSO_SHEERID` (sinh viên); referral URL, external SSO; `SSO_PREMIUM_MULTILOGIN`. VN: store nhân viên SAVINA đăng nhập mã nhân viên; nhiều site SAVINA đang chuyển từ VERIFICATIONCODE sang ACCESSCODE_OTP.
- **Phê duyệt trước tiên (CM-13 §13):** mọi EPP mới và mọi lần kích hoạt lại cần RHQ duyệt. Có email phê duyệt của subs → chuyển ON HOLD RHQ (Shop Merchandising) / ON HOLD HQ (COEC) để Oliver Leung duyệt. Không có → **không dựng, kể cả staging**; đề nghị subs xin qua link template RHQ, chuyển **ON HOLD SUBS**, assign cho subs.
- **9 bước tạo:** kiểm phê duyệt → tạo multistore (Backoffice › Multistore › Create New Multistore; Site ID, catalog, channel **30** cho B2C/SMB, **31** cho B2B, site để clone như `samsung_external`) → login type (SSO_DOMAIN thì thêm domain) → cart restriction và quota (Cart Quantity Limit, Cart Purchase Limit, ngày, Recurrence MONTHLY/QUARTERLY/HALF_YEARLY/YEARLY, giới hạn theo user group, Category Purchase Limit, quota khuyến mãi theo category) → delivery mode và kho trên Website, payment mode trên Multistore (PH, ID dùng Site Payment Config) → ERP config (sold-to, partner number, sales org, distribution channel, division, company code) và ERP FI config clone từ site có sẵn (Tech, PC ticket) → nối AEM (4 cấu hình Website: `CMSSite.aemHomepageUrl` kết thúc `/`, Redirect to External PDP = TRUE, `CMSSite.isAemEnableSite` = TRUE, một dòng `CMSSite.urlRedirects` với 2 mẫu URL và `UrlRedirect.inclusive` = True) → tạo store trong WMC (Store Mgmt › Create New Store) và shop sync → kiểm bằng tài khoản test trên staging.

### SMB
- Multistore `isSme` = true; khách đăng ký bằng email công ty. Duyệt tay (subs trong cockpit CS agent › Business Approvals, hoặc CoE trong Backoffice) hoặc tự động bằng verification code riêng (tab Properties). **Không cần RHQ duyệt.** Giá có thể chia bậc bằng multistore pricing; promotion SMB thường giá cố định trước thuế.

### O2O
- **Endless Aisle**: nhân viên đặt hộ để nhận hoa hồng, hàng từ kho Samsung, cửa hàng không có kho/delivery mode. **BOPIS**: cửa hàng có kho và delivery mode pickup (`vn-o2o-pickup`, `sg-o2o-pickup-new`). Có thể kết hợp cả hai.
- Site EA xác thực 2 bước: nhân viên đăng nhập tài khoản O2O, khách xác nhận bằng Samsung Account (QR hoặc Shop App). MY, VN ghi thêm IP máy cửa hàng.
- **Mở cửa hàng cần:** IP tĩnh IPv4 (whitelist); địa chỉ, SĐT; mã MCS hoặc POS external ID; **sold-to và ship-to trên N-ERP** (ship-to phải đăng ký trước, trống thì kẹt `ORDER_SPLIT` "Please input Customer Number"; nước có FI posting cần ERP FI config); user group (group đối tác vào group admin, group cửa hàng vào group đối tác).
- **Quy ước tài khoản:** super admin `XX_pos_adm_o2o` (1 mỗi subs, ví dụ `id_pos_adm_o2o`); đối tác `XX_pos_adm_ZZZ` (`id_pos_adm_gtn`); cửa hàng `XX_store_usergroup_ZZZ_VVV_PPP` (`id_store_usergroup_gtn_jl_besar_ijen_c070121388`). ZZZ = mã đối tác 3–5 chữ do CoE đặt, VVV = tên cửa hàng viết thường, PPP = external ID. Một số group cũ không theo quy ước (`vn_adm_o2o`, `sg-o2o-pos-admingroup`).
- **MY O2O 2.0:** BOPIS 2.0 (~2 giờ, `my-o2o-pickup-express`) và BOSFS (giao trong ngày, `my-sfs-express`) từ hàng đại lý; mỗi cửa hàng có kho `SFS_...` và Point of Service riêng; **trường Delivery Mode của chính kho đó phải để trống**, nếu không đơn vào nhầm kho.

### 3PD
- **CoE quản gì (CM-13 §15.1):** luồng đơn (sàn → middleware → Hybris → N-ERP), luồng tồn kho (Hybris → middleware), dữ liệu sản phẩm, các luồng khác tùy middleware; không vận hành gian hàng. **4 middleware:** phần lớn Logicbroker, SG dùng **Intrepid**, eBay ở AU nối API trực tiếp (danh sách chính thức chờ RHQ). **Ai làm (§15.2):** PIC 3PD chuyên trách trong Tech Team (100%), kèm backup có chứng nhận; quyền vào middleware qua ticket phê duyệt; thay đổi dữ liệu 3PD production qua PC ticket.
- Luồng: đơn chạy quy trình dropship (staging phải tới `SHIPPING_REQUESTED`, production phải sang được N-ERP); tồn kho gửi sang middleware ~45 phút một lần; chỉ SEAU và SENZ tạo sản phẩm trên sàn từ Hybris; ngừng bán = Merch chuyển Unapproved (subs tự quản trạng thái/tồn trên sàn); sửa đơn/trả hàng 3PD do CS agent làm trên Hybris; **đơn RNPL từ sàn** dùng delivery mode tự hoàn tất (auto status COMPLETED, warehouse adapter AUTO_FULFILMENT) và sản phẩm GHOST, không có gì sang N-ERP.
- **Quy tắc RHQ cho site 3PD** (ngoại lệ cần RHQ duyệt trước): chỉ dùng delivery mode 3PD; mỗi nước chỉ một payment mode 3PD (ví dụ `sg-MarketplacePaymentMode`), riêng SAVINA hai; khách eStore không thấy. Merch tạo site 3PD (`thshopee`, `vnlazada`, `sgtiktok`) dùng catalog 3PD, bỏ cart restriction, không cài AEM; Tech cài ERP FI config, delivery mode, payment mode qua PC ticket; site production chỉ lên khi RHQ xác nhận staging đạt.

### Shop App
- Chung dữ liệu sản phẩm, giá, promotion; nội dung riêng (trang chủ, ưu đãi, dynamic page, in-store mode, menu category) trên Shop App CMS.
- GNB app dựng theo **category** (mã category PIM từ EPP 2.0 / Product IA), upload Pre-Prod rồi Prod; category không có SKU bán được thì không hiện.
- Promotion chỉ cho app dùng Qualifying Sales Application = `MOBILEAPP`.
- Voucher hiện ở My Voucher của app khi có mô tả, đơn vị tiền, thời hạn, **giới hạn site** và App configuration › Display = True; thiếu giới hạn site (và promotion không có qualifying sites) thì hiện cả ở nước khác.
- Test thanh toán riêng trên app: bản cập nhật app có thể làm hỏng luồng thanh toán dù web vẫn chạy.

## Chương 07. Sử dụng HAC và FlexibleSearch
- Backoffice = giao diện nghiệp vụ, từng đối tượng bằng form. HAC = console kỹ thuật (truy vấn nhiều dòng, ImpEx, Groovy). **Chỉ Tech dùng HAC** theo role RHQ cấp; Merch và QA không có quyền cả staging lẫn production (CM-09 §7.1, §7.3), nhưng ai cũng phải đọc hiểu được truy vấn và ImpEx vì chúng có trong ticket, runbook, PC ticket.
- HAC mở bằng `/hac/` trên cùng máy chủ Backoffice; tài khoản HAC cấp riêng. Khi học Tech chỉ dùng HAC staging (URL có `samsungel3-s2`); thấy URL production thì đóng tab và báo Lead. HAC che PII.
- **Menu:** Console › FlexibleSearch (tab SQL xem SQL thật; production chỉ đọc, ghi lý do lên ticket trước); Console › ImpEx Import (chỉ Tech, staging trước, production cần PC ticket và ITGC header); Console › Scripting Languages/Groovy (mặc định rollback; **mọi lần chạy Groovy trên production cần PC ticket, kể cả script chỉ đọc và dry run**); Platform › Configuration (chỉ xem); Platform › Logging; Monitoring; **Platform › Initialization, Update: không bao giờ dùng**.
- **Việc này làm ở đâu:** xem một đối tượng → Backoffice; xem nhiều dòng → FlexibleSearch (Tech; Merch/QA nhờ qua COEC; truy vấn chỉ đọc không cần PC ticket); sửa hàng loạt/cần logic → ImpEx, Groovy (chỉ Tech: COEC, staging trước, PC ticket + ITGC header); chạy lại cronjob production → chỉ Tech có PC ticket (TEC-2.3), Merch/QA không bao giờ; báo cáo, dữ liệu lịch sử, cronjob báo cáo mới → PUMI đã approve rồi PC ticket (CM-13 §12.1); **xuất email khách/PII → mặc định từ chối**, comment ticket và báo Shift Leader, PII không bao giờ rời Hybris qua email; Initialization/Update → không ai.
- **FlexibleSearch:** type (bảng), item (bản ghi), attribute (cột), pk; giống SQL (`SELECT`, `FROM`, `WHERE`, `ORDER BY`, `AS`, `JOIN … ON`, `LEFT JOIN`, `IN`, `LIKE`, `IS NULL`, `DESC`). Không JOIN thì `{o.status}` trả về số pk.
- **7 quy tắc:** (1) type và trường trong `{}`; (2) cả phần FROM gồm JOIN nằm trong một cặp `{}` lớn; (3) trường tham chiếu chỉ lưu pk → JOIN để lấy mã (`OrderStatus` → `{os.code}`); (4) trường đa ngôn ngữ `{p.name[en]}`; (5) lọc catalog và version với sản phẩm, thêm `{o.originalVersion} IS NULL` với đơn; (6) SKU bán được ở `TokoVariantProduct` (gốc `TokoProduct`); (7) tên trường truy vấn có thể khác nhãn/cột upload (`availableAmount` → `available`; `reserved` là số đang giữ). Lỗi người mới: quên `{}` lớn, dùng `TokoProduct`, không lọc version, mở nhầm HAC production.
- **5 câu mẫu** (nền cho TEC-2.2): (1) SKU: approval, sales status, catalog, version (`TokoVariantProduct` JOIN `ArticleApprovalStatus`, LEFT JOIN `SalesStatus`, JOIN `CatalogVersion`, `Catalog`; thêm `{cv.version} = 'Online'` và id catalog như `phEstoreProductCatalog` để lấy bản khách thấy; LEFT JOIN giữ SKU chưa có sales status); (2) tồn kho từng kho (`StockLevel` JOIN `Warehouse`; StockLevel gắn SKU bằng `productCode`, không bằng pk); (3) đơn, trạng thái, tổng tiền, thời điểm tạo (`Order` JOIN `OrderStatus`, `originalVersion IS NULL`); (4) consignment của đơn (`Consignment` JOIN `Order`, `ConsignmentStatus`, LEFT JOIN `Warehouse`); (5) cronjob tồn kho chạy lần cuối (`CronJob` LEFT JOIN `CronJobStatus`, `CronJobResult`, `LIKE '%stock%'`, `ORDER BY {cj.endTime} DESC`; kết quả SUCCESS, FAILURE, ERROR).
- **Đọc ImpEx** (ví dụ phí giao bulky SG): dòng 1 **ITGC header** `#NOTE ITGC_JIRA:PC-1234(COEC-5678)` (Groovy `//NOTE ITGC_JIRA:...`), thiếu hoặc số PC không khớp là **strike** (CM-13 §9.3); macro `$siteUid = sg`; **dòng ImpEx header** `INSERT_UPDATE ZoneDeliveryModeValue;...` (không phải ITGC header); mode `INSERT_UPDATE`/`INSERT`/`UPDATE`/`REMOVE`; `[unique=true]` nhận dòng; `deliveryMode(code)` tìm theo mã; dòng dữ liệu bắt đầu `;`. Khi đọc trả lời 4 câu: type nào, mode gì, bao nhiêu dòng, cột nào nhận dòng; rồi đối chiếu dòng 1 với PC ticket.
- Trên staging Tech chạy file với `PC-TBC` ở dòng 1, tạo PC ticket, thay TBC bằng số thật; file thử và file production chỉ được khác đúng dòng này (TEC-2.2). Định dạng `#NOTE ITGC_JIRA:...` là định dạng trang RHQ Impex/Scripting, KB, G5.2 và TEC-2.2 dùng (nguồn khác nói khác: TC-01, TC-05 đề xuất `# PC ticket: PC-XXXX | COEC ticket: COEC-YYYY`, chờ RHQ; Lead xác nhận khi RHQ ban hành).
- **Quy tắc dùng (staging khi học / production):** xem Backoffice: thoải mái / khi có lý do và chỉ với service đã có chứng nhận; sửa Backoffice: được để tập / theo runbook có QA và người duyệt, Tech sửa cấu hình cần PC ticket; FlexibleSearch: chỉ Tech / chỉ Tech, chỉ đọc, ghi lý do trước, chỉ chọn cột cần, báo cáo cần PUMI rồi PC ticket; xuất PII: không / mặc định từ chối; ImpEx, Groovy: Tech tập / **chỉ Tech Level 2**, PC ticket, kết quả staging, ITGC header; chạy cronjob: Merch/QA không / Merch/QA không bao giờ, Tech chỉ khi có PC ticket; Initialization, Update: không bao giờ.
- **BN4** (theo G5.2: phần A mọi role, phần B chỉ Tech): sổ tay thao tác 6 câu hỏi (CTA của SKU, tồn kho từng kho, promotion áp website nào/đã publish chưa, trạng thái và số consignment của đơn, payment mode khách EPP thấy, cronjob tồn kho lần cuối). Cả 6 câu có đường dẫn Backoffice; ≥ 3 câu có FlexibleSearch sửa từ 5 câu mẫu; câu 3 và 5 trả lời bằng Backoffice là đủ. Merch/QA viết truy vấn trên giấy; chỉ Tech chạy, trên staging (chỉ FlexibleSearch). Bài thêm cho Tech: lọc cronjob lỗi bằng `AND {r.code} IN ('FAILURE', 'ERROR')`.

## Chương 08. Tổng quan đặc thù từng nước (đọc thêm)
- Làm theo KB và trang Market Rules của chính nước đó, không lấy KB nước khác. AU là nước duy nhất trên SMA; AU, NZ có giờ mùa hè.

| Nước | Cluster | Trade-in | Marketplace (3PD) | Giao hàng đáng chú ý |
|---|---|---|---|---|
| VN | SMS | TCV | Shopee, Lazada, TikTok, Tiki | Kho ưu tiên theo miền, Same Day BOPIS, Express Delivery 4H, O2O walkout, lắp đặt |
| TH | SMS | Remobie (`REMOBILE`, làm tay) | Shopee, Makro Pro, KTC, K+ | Nhận tại cửa hàng đối tác, giao CE theo lịch từng vùng, lắp đặt |
| ID | SMS | NBS (Laku6, ENB) qua EzTrade | Lazada, Shopee, Tokopedia | Kho ưu tiên/dự phòng theo mã bưu chính và category, BOPIS, EA |
| MY | SMS | CompAsia | Lazada, TikTok Shop | BOPIS 2.0, BOSFS từ tồn kho đại lý |
| SG | SMS | TIPLUS (CompAsia, CTDI, Laku6) | Shopee, Lazada, TikTok, Qoo10 (qua Intrepid) | Pick & Collect, POPStation, hàng cồng kềnh |
| PH | SMS | Bolttech | Lazada, Shopee, TikTok (`phlazada`, `phshopee`, `phtiktok`) | BOPIS, EA, vùng phục vụ theo PINMAP |
| AU | SMA | Asurion | eBay, Woolworths, My Deals | Tủ nhận hàng Australia Post, nhãn trả hàng |
| NZ | SMS | Assurant | The Market | Phí giao theo đảo, xe tải riêng ở Auckland |

- **Khác:** clawback chỉ SG, NZ, AU; trade-up ở PH, TH, MY, SG, NZ, AU (không VN, ID); **multiple trade-in** bật ở mọi nước trừ SG; SC+ bundle cả 8 nước, subscription chỉ VN, SG, ID, AU; Logicbroker là một trong 4 middleware.
- **Cổng thanh toán** (cấu hình theo site; ID và PH dùng `sitepaymentconfig`; Samsung Rewards chỉ trả được một phần đơn):
  - VN: Cybersource (thẻ, trả góp, Samsung Pay), OnePay, NAPAS, VNPT (ATM, thẻ, VNPay QR, trả góp), FE Credit và tài chính khác, COD, chuyển khoản, trả tại cửa hàng; Payoo đã ngừng.
  - TH: KBank, 2C2P (trả đủ, trả góp, 123 bank direct, hoàn tiền tự động), SCB PayWise, Atome, GrabPay, QR, chuyển khoản, Samsung Pay, trả tại quầy và tại cửa hàng.
  - ID: Midtrans (thẻ, trả góp), bank transfer SNAP, GoPay SNAP, ShopeePay, Kredivo, Indodana, Home Credit, PayPal.
  - MY: iPay88 (thẻ, online banking, trả góp, Atome, Boost, GrabPay, Touch 'n Go, ShopeePay…), Razer Pay, Samsung Finance.
  - SG: Adyen (thẻ, Samsung Pay), 2C2P (PayNow QR, trả góp, GrabPay, Atome); Long Term Financing trên một site EPP.
  - PH: 2C2P (thẻ, GCash, GrabPay, trả góp), iPay88 (Atome, BillEase, Home Credit…), EastWest Bank, CreditLine, DragonPay, TendoPay, PayPal, COD có OTP.
  - AU: Adyen (thẻ, PayPal, Google Pay, Samsung Pay, Alipay, Zip, Afterpay), Samsung Finance by Glow, Latitude, TreviPay (doanh nghiệp), Marketplace Payment Mode cho 3PD.
  - NZ: Adyen (thẻ, Google Pay), PayPal, Worldpay, POLi, Laybuy, Flexicard, thẻ Farmlands; gần đây thêm Afterpay, Zip, Windcave.
- **Từng nước:**
  - **VN (SAVINA):** trả góp Cybersource (`vn-CybersourceCreditInstalmentPaymentMode`) theo ngân hàng/kỳ hạn 3–24 tháng; `vn-pay-at-shop` chỉ cửa hàng CS_STORE; nhiều kho, `siteToWarehouseMap` đè cấu hình (O2O: Bắc WV05 → WV10, Nam WV10 → WV05); delivery mode theo category (`vn-im-parcel-express` MX, `vn-ce-parcel-express` CE); Same Day BOPIS; Express 4H (chỉ trả trước, theo quận); trade-in TCV qua cronjob `vn-tcvTradeInImportDataV2`, `vn-tcv-product-price-imports`; đơn trade-in vẫn COD được; backorder và overselling shipping date; store nhân viên đăng nhập mã nhân viên; O2O quét IMEI trong giỏ.
  - **TH (TSE):** trade-in Remobie làm tay (subs gửi file chấm điểm hằng tháng, CoE upload T-SKU, giữ giá trên base store); có trade-up và multiple trade-in, không clawback; RDD theo kho, mã bưu chính; MX `th-delivery-standard-UPC-MX`, `th-delivery-standard-BKK-MX`, CE nhiều delivery mode theo lịch vùng; ~50 site EPP/B2B, ~190 site SMB; site EA qua app riêng; cấu hình OOW riêng.
  - **ID (SEIN):** trade-in qua EzTrade (cronjob `id-TokoEZTradeInImportData`, `id-eztrade-product-price-imports` mỗi ngày); kho MX WC27, WC28, CE WC31, WC33, WC51, marketplace WC26; **đổi thuế suất theo kế hoạch từng giờ** (dừng import giá → bảo trì → cập nhật thuế → chạy lại import → smoke test); RTF override; nhiều EPP ngân hàng.
  - **MY (SME):** iPay88, Razer Pay, Samsung Finance, Rewards; CompAsia (cronjob 8 giờ sáng, chỉ model có IMEI); BOPIS 2.0/BOSFS từ OMS đồng bộ 30 phút, chỉ Tây Malaysia; lắp đặt CE miễn phí = Z-Code + promotion 100%; SC+ 3PD dùng P-Code.
  - **SG (SESP):** SMB miễn GST đơn > 10.000 SGD khi đủ 3 điều kiện (website bật VAT reversal, prescribed goods, khách VAT enrolled); prescribed goods chỉ dùng Percentage Discount on Products, hàng khác Target Fixed Price; priority quanh First purchase; monetary e-voucher; TIPLUS, clawback; 3PD qua Intrepid; SC+ MX trên sàn bằng F-Code; EPP Long Term Financing mọi thay đổi cần RHQ duyệt.
  - **PH (SEPCO):** Bolttech (cronjob `ph-boltechTradeInImportData`, `ph-boltech-product-price-imports`); SC+ CE gói tháng và một lần; CE Maintenance Pack; target fixed price 1 SP/category; PINMAP; tài khoản cửa hàng và COD dùng OTP.
  - **AU (SEAU, SMA):** thẻ (lưu thẻ, 3DS, chặn BIN); Samsung Finance by Glow (12, 24 tháng từ 250 AUD; 36 tháng từ ~1.667 AUD); Latitude (ẩn dưới 300 AUD; mốc 600, 900, 1.200); Afterpay tới 4.000 AUD; PayPal; TreviPay cho EPP, SMB; Asurion có clawback, overtrade, trade-up, Extended Warranty, SIM plan, Knox Manage; parcel locker `au-parcel-locker-delivery` (chỉ MX, bật bằng `toko.parcel.locker.enabled.au`); lắp máy lạnh tính phí theo máy; EPP tầng T1 (nhân viên Samsung), T2 (ngân hàng, nhà mạng, chính phủ, giáo dục), T3.
  - **NZ (SENZ, SMS):** Assurant; overtrade trên base store theo danh sách Equipment ID; clawback; checkout 0 NZD (giỏ trước trade-in ≥ 1 NZD); phí giao tủ lạnh/máy giặt/máy lạnh **79 NZD đảo Nam** (`nz-parcel-home-delivery-Fee-SouthIsland`), **49 NZD đảo Bắc ngoài Auckland** (`...-NorthIsland-NonAKL`); EPP dùng `nz-parcel-home-delivery-2`; xe tải Auckland; đảo Nam CE lấy WC93 trước rồi WC83; màu sơn Resene cho Bespoke, thẻ Farmlands, kiểm địa chỉ NZ Post.
- Nếu giáo trình khác những gì thấy trên staging thì ghi lại và hỏi Market Owner.

## Chương 09. Tự kiểm tra (18 câu) và bài tập tổng hợp
- Sai từ 3 câu trở lên thì đọc lại chương ghi sau đáp án. Đáp án tóm tắt:
  1. Giá và promotion ở **Hybris**; AEM chỉ nội dung và hiển thị giá, tạo SKU mới; N-ERP giữ RRP.
  2. Sửa Staged của child thì khách chưa thấy, phải sync sang Online; dữ liệu chung sửa ở master rồi sync xuống; Staged ≠ staging.
  3. Purchasable + Unapproved = **Where to buy**.
  4. Khách EPP thấy danh sách của **multistore** (rồi website, rồi base store), sau đó bị delivery mode lọc thêm.
  5. Một hoặc nhiều consignment; sau capture order theo consignment chậm nhất; `COMPLETED` khi consignment cuối xong và FI đóng.
  6. T-Code là máy cũ trade-in, từ đối tác (cronjob MY, upload tự động AU, tay TH), chuẩn Approved + PDP Not Available, gắn `AVAILABLE_SERVICE` Active = TRUE (KB Active/Archive ghi khác → runbook nước, hỏi Lead).
  7. 200 suất pre-order → nhập `maxPreOrder` = 200, **không cần chặn import**; chỉ chặn khi tự gõ `availableAmount`.
  8. Preview module chỉ cho simulator, không Knox; module nước là publish live, đi Knox → PUBLISHED, khoảng 1,5 giờ sau lần duyệt cuối.
  9. Dời ngày kết thúc promotion đã publish → **phải xin Knox lại**; không sửa ngày campaign để né Knox.
  10. Voucher chỉ còn cho **RNPL/SR+**.
  11. `ORDER_SPLIT` "Please input Customer Number" = cửa hàng O2O trống ship-to; subs cấp mã, Tech điền và chạy lại (PC ticket); Merch/QA chỉ ghi lên ticket. Ca `ORDER_SPLIT` hay gặp nhất là thiếu tồn ở mọi kho.
  12. Trạng thái và tồn kho 200 SKU → FlexibleSearch trên HAC, **chỉ Tech chạy**, Merch/QA nhờ qua COEC; truy vấn chỉ đọc không cần PC ticket.
  13. JOIN `OrderStatus` vì status chỉ lưu pk; `originalVersion IS NULL` để lấy bản hiện tại.
  14. ImpEx trên HAC production: chỉ **Tech Level 2**, đã chạy staging với `PC-TBC`, PC ticket RHQ duyệt, dòng 1 ITGC header; áp cho mọi Groovy kể cả chỉ đọc/dry run.
  15. Authorize giữ tiền, capture lấy tiền sau kiểm tra gian lận và dịch vụ ngoài; khoản giữ ~7 ngày.
  16. RDD: đặt thứ Sáu 10:00, lead 2, không giao T7/CN → **thứ Ba**; đặt 16:00 → **thứ Tư**.
  17. EPP mới không có email phê duyệt → không dựng (kể cả staging), ON HOLD SUBS, assign subs; có email → ON HOLD RHQ/ON HOLD HQ. Kích hoạt lại cũng vậy.
  18. Production là hệ thống thật, Merch setup ở đó theo quy trình; staging để thử/BVT/đào tạo, không chạy job nền; STG SETUP = đang setup trên production; khi học chỉ làm trên `samsungel3-s2` với đối tượng `TRAINING_<tên>_`.
- **Bài tập tổng hợp** (chỉ staging, Merch/QA không HAC, chỉ dữ liệu giả, bằng chứng theo CM-10): (1) hoàn thiện BN1–BN4 kèm phần sửa; (2) **BN5**: gom ghi chép 4 bài vào một trang, thêm ≥ 3 câu hỏi gửi RHQ vào file câu hỏi chung, viết để RHQ trả lời được mà không cần gọi (thấy gì, KB nói gì, cần xác nhận gì); (3) **BN6** "Hybris SEAO bằng lời của tôi" (không chép câu nào): dữ liệu nằm đâu, promotion đi live thế nào (preview, simulator, publish live, Knox), đường đi đơn từ authorize đến `COMPLETED`; (4) thêm vào BN6 ba điểm khác nhau giữa các nước quan trọng nhất với team, mỗi điểm kèm KB/Market Rules làm căn cứ; (5) chọn một trang trong cây 10.1 KB chưa có trong bảng tài liệu gốc, ghi 3 ý chính (nói khác giáo trình thì ghi cả hai, hỏi Lead); (6) trả lời lại đúng hết 18 câu chương 09.

## Chương 10. Thuật ngữ và tài liệu gốc
- Bảng thuật ngữ đầy đủ ở trang **"Onboarding – Glossary for newcomers"**. Chương 10 chỉ giữ khoảng 46 thuật ngữ dùng nhiều nhất kèm chương giải thích: RHQ, subsidiary, Hybris/SAP Commerce/Toko, Backoffice, Product Cockpit, HAC, AEM, N-ERP/GERP, cluster SMS/SMA, staging/production, Staged/Online, master/child catalog, base store/website/multistore, SKU, Product Type, Z/F/T-Code, Sales status/Approval, RRP/special price, Stock Level, Super Sync, product reference, promotion rule, promotion module/publish, simulator, rule group, coupon/voucher, RNPL/SR+, trade-in/overtrade/trade-up/clawback, SC+, Knox approval/approval path, authorize/capture, consignment, ORDER_SPLIT, đơn kẹt, RDD/lead time/cut-off, delivery/payment mode, sold-to/ship-to, EPP/SMB, O2O EA/BOPIS/BOSFS, 3PD/middleware, PC ticket, ITGC header, FlexibleSearch/ImpEx/Groovy, type/pk, PUMI, freeze.
- Các chỗ nguồn còn khác nhau được ghi rõ: NZ thuộc SMS (trang login và trang thuật ngữ chưa xác nhận); Super Sync là chức năng Product Cockpit (trang thuật ngữ gọi là cronjob); ORDER_SPLIT là trạng thái (trang thuật ngữ và G4.1 gọi là bước).
- **Tài liệu gốc** theo chủ đề (đều trong space này: cây 10.1 KB, trang đồng bộ từ RHQ, Market Rules, tài liệu vận hành CoE): tổng quan/môi trường/cronjob; catalog và cấu hình store; sản phẩm, trạng thái, product reference; giá; tồn kho; promotion và Knox; coupon, voucher, RNPL; trade-in, overtrade, dịch vụ ngoài; đơn hàng và đơn kẹt; thanh toán và gian lận; giao hàng, kho, lead time; EPP và SMB; O2O và Shop App; 3PD (gồm biên bản Handover Day 3 3PD 27/10/2026); HAC, FlexibleSearch, ImpEx; 8 trang Market Rules; KB theo nước; CM-01, CM-09, CM-13. Khi tài liệu nói khác CM-13 về quy trình thì theo CM-13.
- Thấy giáo trình khác hệ thống thật thì ghi vào file câu hỏi chung để cập nhật giáo trình.

## Liên hệ với bộ tài liệu CM/TC/MR
- Quy tắc workflow, phê duyệt, tuân thủ (Knox cho mọi giá/promotion §10, PC ticket và ITGC header §9, EPP §13, PUMI và PII §12.1, 3PD §15, freeze §19, strike) nằm ở **CM-13**; quyền công cụ (HAC chỉ Tech) ở **CM-09**; bằng chứng/ảnh chụp ở **CM-10**; welcome pack ở **CM-01**; SLA và trạng thái ticket ở CM-03/CM-05; service chuẩn Merch ở MR-05; runbook/PC ticket Tech ở TC-01, TC-05 và các module TEC-2.x.
