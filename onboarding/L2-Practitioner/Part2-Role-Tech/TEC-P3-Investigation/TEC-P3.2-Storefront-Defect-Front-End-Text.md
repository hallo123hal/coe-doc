# TEC-P3.2 Storefront defect and front-end text

> Nguồn: page 2484371908 · 60' (Study 15' · Demo 10' · Quiz 5' · Practice 30') · Facilitator: Shift Leader/Sub-Lead · Capabilities C2, C4 · Cần xong G3.2 (thành phần hệ thống: phần trang nào AEM phục vụ, phần nào Hybris). Mang pack TEC-TSP-05 và attachment TRN-042 (brief, `text-change-sheet.csv`, `diagnosis-queries.sql`, `pc-ticket-draft.md`). Access: staging Backoffice + HAC el3-s2, storefront `https://stg2.shop.samsung.com/vn/` (cookie qua getcookie.html), Jira SCOE-48. Không access: facilitator đưa screenshot màn CronJobs và tab Properties của component, làm giấy.

## Mục tiêu
Phân loại yêu cầu storefront vào variant (V1–V8) và layer bằng reproduce + kiểm read-only; route từng yêu cầu trong ticket nhiều yêu cầu đến đúng owner (Tech fix, Samsung release, service Tech khác, Merch); quyết định hành động Tech nào cần PC và viết PC cho thay đổi text có ngày kèm rollback; viết update cho requester giải thích route từng mục bằng ngôn ngữ đơn giản.

## Thuật ngữ
**Layer** (nguồn của triệu chứng storefront: data, configuration, AEM content, code storefront Hybris, email template, cache; VD thông báo lỗi số điện thoại nằm trong code); **Nav sync job** (cronjob sao chép AEM GNB/footer sang trang Hybris như cart, checkout, VD `vn-DotComCmsFooterNavSyncJob`); **CMS component** (item Backoffice chứa text storefront, Vvd CMSParagraphComponent, TermsConditionComponent; Tech sửa được dưới PC); **Message key** (text trong properties file của code storefront, VD `address.phone.invalid`; chỉ release của Samsung mới đổi được); **Samsung-executed change** (thay đổi SDS India làm qua pull request, QA server review và Ops release; CoE xin qua Maintenance Request); **Text change sheet** (danh sách requester: key, ngôn ngữ, text cũ, text mới, người duyệt; BiPlus không dịch khi chưa có duyệt bằng văn bản); **Before value** (text/setting đã lưu trước khi sửa để rollback khôi phục); **Sibling tickets** (cùng defect mở theo từng market, VD "Mismatched GNB/Footer" ở VN, MY, TH, SG; link dưới một parent).

## Nội dung
### 1. Runbook TEC-TSP-05
Phủ defect trên trang Hybris và AEM phục vụ (cart, checkout, PDP, PLP, buying và add-on, My Page, GNB và footer, email giao dịch) và thay đổi text front-end nhỏ, trên site B2C, EPP, SMB, EA. 355 ticket 2026, ~39/tháng. Doer: engineer Level 1 hoặc 2. Checker: engineer thứ hai; Tech Lead review khi rủi ro cao. Approver: RHQ qua PC, và RHQ cho code release.
Priority theo impact: P2 (16h) khi cart/checkout bị chặn cho nhóm SKU hoặc phân khúc site; P3 (40h) cho lỗi hiển thị có workaround, email hoặc lỗi text; P4 (120h) cho cosmetic và đổi text không có ngày. Checkout chặn cả site là P1 hoặc P0 kèm COE-INC-01.
| Variant | Dùng khi | Tỷ lệ |
|---|---|---|
| V1 Cart và checkout | Không add được vào cart, chặn gift/FOC, form địa chỉ | ~30%, nhóm lớn nhất |
| V2 GNB, header, footer | GNB trên cart/checkout khác trang AEM | ~15%, title lặp phổ biến nhất |
| V3 PDP, PLP, buying, add-on | Flag, benefit, giá hay khối add-on sai | ~19% |
| V4 Email giao dịch | Không nhận, sai nội dung, đổi template | ~6% |
| V5 My Page, account | Địa chỉ, voucher, màn order lỗi | ~6% |
| V6 Text front-end và localisation | Text cuối theo từng ngôn ngữ từ requester | ~9% |
| V7 Thông báo khách SMS/Viber (thêm 01/11) | SMS order VN hay Viber/SMS PH không nhận, hoặc cần bật/tắt. Kiểm đầu: Approval Status của trang SMS VN (Staged và Online) hay tokoconfig Viber PH. Mọi thay đổi dưới PC | Hiếm; chỉ VN, PH |
| V8 Hành trình store EPP: Open EPP và bulk order portal (thêm 01/11) | Open EPP hiện trang login hay chặn guest checkout; bulk portal không vào được hay upload bị từ chối dòng. Kiểm đầu: cờ Open EPP và cờ bulk-store; sửa cờ thuộc TEC-CFG-05 | Hiếm; Open EPP ở PH, bulk order ở NZ và AU |
| Bước | Doer | Checker |
|---|---|---|
| Route check và priority | So với "Not this service"; re-route nội dung Merch ngay khi tiếp nhận | Đúng service, không phải content Merch; priority khớp impact |
| Reproduce | Site và staging cùng cluster, cùng loại user và thiết bị; giờ market | Đã reproduce trên site và staging |
| Xác định layer | Data, config, AEM, code, email template, cache; read-only | Layer và nguyên nhân có chứng cứ |
| Chuẩn bị thay đổi | Text đã duyệt theo ngôn ngữ; before value; rollback; PC | Text đã duyệt; giữ before value; PC duyệt trước khi đổi |
| Verify | Mọi site bị ảnh hưởng, desktop và mobile, guest và registered | Defect pack đầy đủ khi escalate |

### 2. Layer: front-end, content hay Hybris
Xác định layer trước khi gọi owner. Reproduce trên site báo lỗi với test account cùng loại user và thiết bị, rồi trên staging cùng cluster. AU chạy trên SMA (el5/STG4), không kiểm từ el3 được.
| Triệu chứng | Layer | Kiểm (read-only) | Ai hành động |
|---|---|---|---|
| Footer cart khác trang chủ | Nav sync job | Backoffice › System › Background Processes › CronJobs, tìm `DotComCmsNavSyncJob`: Current status, Last result | Tech rerun dưới PC; job lỗi sang TEC-TSP-06 (KE-TEC-TSP-05-01) |
| SKU không add được vào cart | Product data | salesStatus, approval, price row, stock, delivery service | Merch owner sửa data (KE-03) |
| Câu T&C trên checkout | CMS component | Component trong Backoffice, tab Properties, Staged | Tech dưới PC |
| Thông báo validate hay label | Message key trong code | Staging không có type "localisation value"; chỉ LocalizedString và SiteMessage | SDS India release qua Maintenance Request |
| Email hiện placeholder | Email template | EmailPageTemplate, RendererTemplate | L3 fix (KE-06) |
| Header trùng, ngắt quãng | Cache hoặc component | Giờ, URL | DevOps clear cache (ON HOLD ES); lỗi component sang SYSTEM SUPPORT |
**TRN-042, mục 1.** Linh (VN eStore Ops) báo footer cart `vn` khác trang chủ. So sánh `/vn/` và `/vn/cart` trên `vn` và `test1`, guest, desktop và mobile, lập bảng khác biệt kèm giờ GMT+7. Trên el3-s2 `vn-DotComCmsFooterNavSyncJob` FINISHED/ERROR (chạy cuối 2026-10-24 14:24), còn `vnDotComCmsNavSyncJob` và `vn-DotComCmsEppNavSyncJob` SUCCESS. Job footer cũng lỗi ở MY, TH. Kết luận: footer chưa đồng bộ; job lỗi sang TEC-TSP-06 trong COEC liên kết; defect lặp ở 3 market là ứng viên COE-PRB-01. Không rerun job: rerun đổi trạng thái hệ thống và cần PC. Trạng thái job đổi theo ngày, dùng kết quả bạn thấy hôm đó.
> Message key nằm trong properties file của code (TECHNICAL DESIGN IDME-1610) nên là Samsung-executed (TEC-TSP-05 §2.7 bước 3). Trong Backoffice chỉ sửa được CMS component. KE-TEC-TSP-05-08 ("release hoặc CMS edit (PC)") nghĩa là một trong hai tuỳ text nằm đâu. GNB/footer AEM tới trang Hybris qua sync job chạy mỗi ngày một lần (SMB GNB hằng tuần), nên thay đổi AEM mới hơn một lượt chạy chưa phải defect. Site mới không có GNB trên cart thường thiếu trong `TokoDotComCmsSyncCronJob.siteIdList` (KE-TEC-TSP-05-11; thêm vào là thay đổi PC).

### 3. Route: gửi từng yêu cầu đúng owner
Re-route lúc tiếp nhận, trước khi làm.
| Yêu cầu | Owner |
|---|---|
| Landing, campaign, offer; hero banner | MER-AEM-01, MER-AEM-02, MER-AEM-04 |
| Mục GNB cần soạn | MER-AEM-03 |
| Text, flag, benefit Merch | MER-TXT-03, MER-TXT-02 |
| Logic promotion/giá, giảm sai | TEC-TSP-01 |
| Bước payment; tên payment mode | TEC-TSP-04; TEC-CFG-02 |
| Giá trị tokoconfig; job lỗi là vấn đề chính | TEC-CFG-03; TEC-TSP-06 |
| Tính năng mới | TEC-ADH-02 |
Cách route tuỳ phần việc của người khác trong ticket (TC-03 §2.4):
- **Toàn bộ là việc Merch** (VD banner, giá): Tech Sub-Lead quyết, bạn comment lý do, chuyển chính ticket sang project Shop Merchandising của market và báo Merch Shift Leader. Không tạo ticket mới; SLA theo dõi trên từng ticket.
- **Merch còn phần sau Tech:** giữ COEC; yêu cầu subsidiary tạo ticket Shop Merch cho phần set-up, link hai ticket.
- **Yêu cầu không liên quan trong một ticket:** yêu cầu requester tách khi tiếp nhận; yêu cầu liên quan cùng mục tiêu giữ chung.
**Bảng route TRN-042.** Mục 1 footer: TEC-TSP-05 V2, kiểm job, COEC liên kết cho TEC-TSP-06. Mục 2 text T&C: V6, PC và Checker, sửa ở Staged. Mục 3 thông báo lỗi số điện thoại: V6, Maintenance Request tới SDS India (chỉ Tech Level 2), COEC sang SYSTEM SUPPORT. Mục 4 hero banner `/promotion-nov`: nội dung AEM, MER-AEM-04; Tech không làm, yêu cầu requester tạo ticket Shop Merch. Priority P3: lỗi hiển thị có workaround, checkout không bị chặn.
> TC-03 §2.6 nói yêu cầu không liên quan nên tách khi tiếp nhận. TRN-042 giữ mục 1-3 trên một COEC (cùng storefront, cùng requester) và chỉ route mục 4 ra. Nếu các mục khác owner và timeline thì theo TC-03 và hỏi Sub-Lead có tách không; ghi quyết định trong comment.

### 4. Đổi text dưới PC, rollback có ngày
Sửa text Backoffice của Tech là Normal change. TEC-TSP-05 không có Standard production change, và RHQ xác nhận không có ngoại lệ PC cho thao tác runbook. Bảng quyết định TC-05: xem và query read-only không cần PC; sửa record hay cấu hình, rerun cronjob hay sync tay, và mọi rollback trên production đều cần.
Các bước V6: 1) xác nhận là text front-end, không phải MER-TXT-03, MER-AEM-01 hay tên payment mode; 2) lấy text cuối theo từng ngôn ngữ kèm người duyệt có tên (BiPlus không dịch khi chưa duyệt bằng văn bản); 3) định vị component, lưu before value (screenshot tab Properties); 4) viết PC, comment của Checker trước, COEC sang ON HOLD HQ khi chờ; 5) sau duyệt, sửa ở catalog version KB nêu (T&C bảo hành PH: KB sửa component ở Online-catalog trực tiếp, không sync; item Staged như trang SMS VN thì sync lên Online, TEC-TSP-05 §2.7); kiểm mọi ngôn ngữ trên desktop và mobile; trong lab chỉ tới Staged; 6) thay đổi có ngày: lên lịch đúng giờ go-live theo giờ market; text cũ khôi phục vào ngày kết thúc dưới PC vì rollback cũng là thay đổi production.
**TRN-042, mục 2.** Text lên D+3 08:00, hoàn nguyên D+10 23:59 (GMT+7). PC summary dạng `[PC] [Market] [Short change] (COEC [number])`. Scope: một component, `TRAINING_<TEN>_TRN042_TNC` trong `vnContentCatalog:Staged`. Nội dung: text mới đúng như sheet, người duyệt, screenshot before, cửa sổ, executor, post-check trên `vn` và `test1` desktop/mobile, rollback gồm khôi phục D+10. Loại trừ mục 3 và 4. Trên staging dừng ở Staged, không sync. Không bao giờ sửa `TermsAndConditionFooter` hay component không có tiền tố `TRAINING_`.
> TEC-TSP-05 §2.7 bước 5 nói text cũ khôi phục "bằng PC thứ hai"; TRN-042 cho phép "một PC (hoặc cùng PC)" gồm cả khôi phục. RHQ chưa công bố template PC. Dù cách nào, việc khôi phục phải ghi trong PC trước cửa sổ; hỏi Tech Lead hình thức RHQ chấp nhận.

### 5. Escalate phần code và đóng vòng
Mục 3 (`address.phone.invalid`): text nằm trong code nên SDS India đổi. Tech Level 2 tạo Maintenance Request với evidence pack 8 phần; Level 1 chuẩn bị phần 1-3 (bước, loại user và thiết bị, expected/actual). Nội dung: key, text cũ và mới tiếng Việt, site, screenshot, ngày muốn D+3. COEC sang SYSTEM SUPPORT: clock dừng, CoE giữ ownership và follow-up mỗi 4 ngày làm việc cho P3.
Update requester giải thích mỗi mục một dòng, VD "3. Thông báo số điện thoại: lưu trong code storefront nên Samsung phải release. Maintenance Request <key> đã tạo; ticket của chúng tôi ở SYSTEM SUPPORT." và "4. Hero banner: vui lòng tạo ticket Shop Merch cho team Merch; chúng tôi không đổi nội dung AEM ở đây."
Cuối cùng: LAUNCH VERIFICATION, giao requester. RHQ đóng COEC, không tự đóng. Bằng chứng là screenshot trong PowerPoint trên workstation CoE, không video, tối đa 15 MB mỗi file.
Handover liên quan: Kibana Log (28/10: trace cart theo cart id); All SEAO Cronjob (30/10: nhóm job gồm AEM navigation, product sync; đọc log job; không rerun khi chưa duyệt); VN SMS OTP and Notifications (28/10: năm trang SMS order VN, Approval Status, Staged rồi Online, PC trước, V7); PH SMS Viber (28/10: Infobip Viber với SMS failover, tokoconfig PH); Open EPP and AEM (29/10: cờ Open EPP, V8); Bulk Order Site Config (29/10: hành trình bulk portal, cờ, delivery mode); Auto MBO Flag and Price (27/10: cờ và giá trang add-on, V3); Samsung Vault Saved Card (30/10: ba setting Vault, chỉ SG và NZ, V5). TEC-TSP-06 (job failure, Service Packs v0.2) không thuộc 13 runbook nên báo Tech Lead.

## Quiz (đáp án)
1 Ticket COEC xin thay hero banner trang campaign VN, không gì khác → **B: theo quyết định Sub-Lead, comment lý do, chuyển chính ticket sang project Shop Merch VN và báo Merch Shift Leader** (D chỉ khi Merch còn phần sau Tech; C phá theo dõi SLA). 2 Footer cart `vn` khác trang chủ, footer AEM đã publish, CronJobs `vn-DotComCmsFooterNavSyncJob` FINISHED/ERROR → **C: ghi trạng thái job; mở COEC liên kết cho TEC-TSP-06; mọi rerun cần PC duyệt**. 3 Requester muốn đổi thông báo validate số điện thoại trên form địa chỉ; staging không có type localisation → **B: Tech Level 2 tạo Maintenance Request tới SDS India; COEC sang SYSTEM SUPPORT**. 4 T&C lên D+3 08:00, hoàn nguyên D+10 23:59 (GMT+7), nội dung PC đúng → **B: scope một component, text duyệt theo ngôn ngữ, before value, cửa sổ, executor, post-check, và khôi phục D+10 nằm trong rollback**. 5 TRN-042 P3, mục 3 ở SYSTEM SUPPORT, follow-up theo RFP → **B: mỗi 4 ngày làm việc** (P0–P2 mỗi 2, P4 hàng tuần). 6 Requester gửi text tiếng Việt đã dịch không nêu người duyệt → **C: hỏi một lần (template B) text cuối theo ngôn ngữ và người duyệt**. 7 Hành động không cần PC → **C: FlexibleSearch read-only trên trạng thái CronJob, ghi lý do lên ticket** (rollback trên production cần PC).

## Practice
**PR-TEC-P3.2-1. Ticket footer và text (TRN-042)** (30'; staging el3-s2 + SCOE-48; chỉ sửa `TRAINING_<TEN>_TRN042_TNC` và chỉ sau khi facilitator "duyệt" PC; không cronjob, không sync). Làm: (1) comment đầu với priority P3 và lý do; (2) bảng route check cho 4 mục (layer, service, hành động); (3) đọc trạng thái job footer, nav và EPP nav của VN trong CronJobs và ghi lại; (4) soạn PC cho mục 2 kèm khôi phục D+10 23:59; (5) soạn nội dung Maintenance Request cho mục 3; (6) viết update requester, một dòng mỗi mục. **Pass:** route đúng 4 yêu cầu: mục 1 V2 kèm COEC liên kết cho TEC-TSP-06 (job ERROR), không rerun; mục 2 V6 dưới PC, scope một component, rollback có ngày D+10 23:59 GMT+7; mục 3 V6 tới SDS India qua Maintenance Request, COEC SYSTEM SUPPORT, follow-up mỗi 4 ngày làm việc; mục 4 MER-AEM-04, Tech không làm. Không sửa ngoài component `TRAINING_`; text khớp sheet từng ký tự; không bằng chứng video. Không access: làm giấy với screenshot facilitator, cùng tiêu chí pass.
