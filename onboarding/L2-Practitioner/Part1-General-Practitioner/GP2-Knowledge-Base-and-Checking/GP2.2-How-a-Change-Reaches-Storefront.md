# GP2.2 How a change reaches the storefront

> Nguồn: page 2484502579 · 60 phút (Study 15' · Demo/thảo luận 10' · Quiz 5' · Practice 30') · Thực hành theo case; facilitator: Shift Leader hoặc Sub-Lead · Capability C2 · Cần xong G3.2 (Hybris, AEM, Shop App, NERP, Knox) và G6.2 (capstone); mang ghi chú GP2.1 về Staged/Online/CTA và tờ 4 cột (layer, first check, owner, next step). Chỉ cần Confluence (đọc); Jira SCOE (đọc) để xem TRN-041, TRN-042. Không có access: facilitator in bảng runbook và 5 case thực hành.

## Mục tiêu
Giải thích đường đi của thay đổi product status, price, promotion, content từ màn hình setup tới storefront; nói phải chờ bao lâu và kiểm gì trước khi test storefront; với case "đã làm nhưng không thấy", nêu layer khả dĩ nhất, phép kiểm đầu tiên và ai sở hữu việc sửa; giải thích vì sao Hybris đúng mà trang vẫn sai.

## Thuật ngữ
**Master và child catalog** (master giữ sản phẩm; child catalog như `vnEstoreProductCatalog` cho D2C giữ status theo kênh và phục vụ site); **Synchronise to Online** (Catalog › Products › chọn › Synchronize copy Staged sang Online; chỉ Online khách thấy); **Super Sync** ("Products Sync Selector" trong Product Cockpit kéo DOTCOM (nội dung AEM), PRICE, STOCK, IMAGE từ hệ thống nguồn vào master); **Preview vs live promotion module** (rule publish vào `<cc>-preview-promotions-module` chỉ chạy trên simulator; khách chỉ nhận từ `<cc>-promotions-module`); **Knox jobs** (`knoxPromotionStatusJob` đặt KNOXAPPROVED; `knoxPromotionPublishingJob` publish; `knoxPriceApplyingJob` ghi giá đã duyệt vào Staged; production chạy ~mỗi 45', có thể trễ khi tải khu vực; staging el3-s2 trigger mỗi giờ ở phút 02, 12, 45); **Nav sync job** (cronjob mỗi market copy header/footer AEM sang trang Hybris, VD `vn-DotComCmsFooterNavSyncJob` cho footer cart); **Layer** (nguồn của kết quả storefront: dữ liệu Hybris, promotion engine, cronjob, nội dung AEM, Shop App CMS, code storefront, cache).

## Nội dung
### 1. Product status: Staged, sync, Online
Việc product làm trong Backoffice production, ở bản **Staged** của từng child catalog, chỉ hiện sau khi **sync sang Online**. SKU mới đi master Staged → child Staged → Online; đổi status đặt ở từng child Staged phục vụ site. Status đặt ở catalog dùng chung áp dụng cho mọi site của nó; loại trừ riêng một site là service khác (MER-MST-02).
| Bước | Ở đâu | Khách thấy |
|---|---|---|
| Super Sync (DOTCOM, PRICE, STOCK, IMAGE) | Product Cockpit › Products › master catalog › "Products Sync Selector" | Chưa gì; dữ liệu vào master |
| Đặt approval và sales status | Catalog › Products › child catalog, version Staged | Chưa gì |
| Sync Staged → Online | Catalog › Products › chọn › Synchronize | Status mới, sau indexing và cache |
| Test storefront | PDP và add to cart trên một site mỗi loại catalog | CTA theo rule KB |
Super Sync lỗi cho biết nguồn nào thiếu: DOTCOM lỗi khi model chưa publish trên AEM (KE-MER-PRD-01-01); PRICE lỗi khi NERP có vấn đề; STOCK lỗi → hỏi có cần Stock Import Override không. Stock import theo lịch `<cc>-tokoStockImportUpdateJob` cũng chạy ~mỗi 30' (TH 3 lần/giờ).
**Ví dụ TRN-007:** HW-S800B/XV đặt unapproved + PURCHASABLE trong `vnEstoreProductCatalog` Staged. Tới khi sync catalog D2C, `vn` vẫn hiện "Mua ngay". Ticket nói: sync mọi catalog đã đổi, ghi giờ ICT, chờ indexing và cache rồi test storefront.
> Lab ticket TRN-007 gọi thao tác sync là "Push to Target → Online"; runbook MER-PRD-01 gọi nút toolbar "Synchronize" và runbook sửa đổi (01/11/2026) mô tả dialog: chọn target — child Staged khi sync từ master, Online khi sync từ child Staged. Dùng tên trong runbook.

### 2. Giá và promotion: Knox nằm trên đường đi
Giá và promotion đi qua **Knox approval** và các job theo lịch trước khi tới storefront. Chờ Knox không có Jira status: SLA clock vẫn chạy (D1 under review).
**Giá (MER-PRC-01):** upload file (Product Cockpit › Bulk Upload) → PriceInfoChange VALID → Check A bởi QA → Shift Leader duyệt → submit Knox trong 4 giờ làm việc từ khi intake đủ → `knoxPromotionStatusJob` đặt KNOXAPPROVED → `knoxPriceApplyingJob` đặt COMPLETED và ghi price row vào Staged → release lên Online cho SKU của ticket, chỉ khi Knox approved, mọi record COMPLETED và Check A đạt → Check B lúc go-live bởi người thứ hai.
**Promotion (MER-PRM-01):** lưu rule (UNPUBLISHED) → publish vào module **preview** (không Knox) → simulate → QA REVIEW → Shift Leader duyệt → publish vào module **live**, phát sinh yêu cầu Knox (KNOXPENDINGAPPROVAL) → KNOXAPPROVED → PUBLISHED bởi publishing job → kiểm go-live trong 30' (E4: 15').
| Đổi promotion đã publish | Knox lại? |
|---|---|
| Actions, conditions, website, dates | Có, ở lần publish kế |
| Name, status | Không |
Không để hai version của một rule cùng KNOXAPPROVED; không publish rule discount và non-discount cùng lúc.
KT Samsung (21/10/2026): *Knox áp dụng cho thay đổi giá và promotion. Promotion đã publish: actions, conditions, website, dates cần duyệt lại ở lần publish kế; name và status thì không. Cột approval trong campaign brief cho biết dùng đường nào.*
> KB Samsung "Promotion Rule Knox Approval" publish sau Knox rồi QA, còn MER-PRM-01 v0.2 yêu cầu QA ở preview module trước, Knox sau QA PASS. MER-PRM-01 sửa đổi (01/11/2026) giữ QA ở preview trước. Trên production cho phép tới ~90' sau duyệt trước khi coi rule/giá là kẹt. Trên staging el3-s2 Knox tắt cho cả chín store nên publish luyện tập không hiện popup Knox và không phản ánh production.
> **Under review (D1, D5):** runbook sửa đổi giữ ticket ở ON HOLD SUBS với Doer là Assignee khi chờ Knox. Promotion thêm green light của subsidiary ở REVIEW SETUP trước live publish và Knox; giá thì Knox trước, rồi sync, front-end QA, REVIEW SETUP. Hai đường trên giữ nguyên tới khi D1, D5 chốt.

### 3. Indexing và cache: khi nào test storefront
Sau sync hoặc publish, storefront cần thời gian. Test quá sớm → báo lỗi giả; chờ vô tận cũng không.
| Nội dung | Chờ trước khi test (nguồn) |
|---|---|
| Add-on page | ~30' (MER-PRD-01, KB Add-on Category Filter) |
| Gift page | 15–20' (MER-PRD-01, KB Add-on Page) |
| Add-on flag và giá gạch ngang (Auto MBO) | ~30' sau go-live; API cache 1 giờ (MER-PRM-04) |
| Benefit | Tối đa 1 giờ (cache); go-live gấp nhờ Tech purge CDN cache (MER-TXT-02) |
| Giá sau khi release Online | PDP và cart trong vài giây; trang listing (product filter) hiện giá gạch ngang muộn hơn (MER-PRC-01) |
| PDP sau đổi status | Độ trễ chung chờ xác nhận ở KT |
| Trang AEM sau publish | Front end có thể trễ 5–10'; thay đổi có thể mất tới 1 giờ; gấp thì nhờ requester xin content team purge CDN (MER-AEM-01) |
| Stock từ NERP | Import theo lịch ~mỗi 30' (TH 3 lần/giờ) |
Test trong cửa sổ ẩn danh, desktop và mobile, một site mỗi loại catalog hoặc nhóm site. Dữ liệu đúng mà giá trị cũ vẫn còn **sau** thời gian sync và cache thì nghi nguyên nhân kỹ thuật: tạo COEC liên kết cho Tech (flush cache, sync job), giữ ticket Merch ở ON HOLD COE và tiếp tục containment nếu liên quan tiền. Header/footer trùng lặp chập chờn do DevOps xử lý (xóa cache CDN hoặc dispatcher, ON HOLD ES).
> Nguồn không nêu thời gian Solr indexing cho PDP và search, cũng không có quy trình purge cache cho Hybris (purge cluster từ HAC là việc Tech dưới PC ticket, TEC-TSP-05). Tới đó, ghi giờ sync và giờ từng lần test theo ICT để Lead thấy bạn chờ đủ chưa.

### 4. Nội dung ngoài Hybris: AEM, Shop App, code storefront
Không phải mọi thứ trên trang đều từ Hybris. Thay đổi Hybris có thể đúng mà trang vẫn sai vì phần đó ở nơi khác.
| Phần trang | Hệ thống và đường publish | Owner |
|---|---|---|
| Homepage EPP, offer, PF, FAQ, nội dung footer, banner. Trang B2C samsung.com/<cc>/ thuộc AEM team của subsidiary, không phải CoE | AEM author: Create Workflow › Samsung Direct Workflow (System Admin publish ~1 phút); EPP 2.0 CMS qua WMC với SingleID: Save › QA › Live | Merchandising (MER-AEM-01 → 04) |
| Header và footer ở cart, checkout | Copy từ AEM bởi nav sync job của market; chạy lại là đổi production, cần PC ticket | Tech (TEC-TSP-05; job lỗi TEC-TSP-06) |
| CMS component trong Backoffice (đoạn T&C) | Tech đổi ở Staged dưới PC ticket | Tech (TEC-TSP-05 V6) |
| Message key trong code storefront (properties) | Chỉ qua release của Samsung: Maintenance Request bởi Tech L2 gửi SDS India; COEC ở SYSTEM SUPPORT | Samsung, Tech theo dõi |
| Offer và banner Shop App | Shop App CMS: Request approval › Publish (role -REQUEST-APPROVAL, -PUBLISH; -APPROVE chỉ RHQ) | Merchandising (MER-SAC-01) |
**Ví dụ TRN-042 (VN, một COEC bốn item):** (1) footer cart khác home → lớp nav sync; `vn-DotComCmsFooterNavSyncJob` kết thúc ERROR trên el3-s2 (MY, TH cũng ERROR) nên cần COEC liên kết cho TEC-TSP-06 và là ứng viên Problem; (2) câu T&C checkout → CMS component, Tech đổi với PC ticket; (3) message validate số điện thoại → code properties, Samsung release; (4) hero banner `/promotion-nov` → nội dung AEM, ticket Shop Merchandising riêng (MER-AEM-04). Priority P3: lỗi hiển thị có workaround.

### 5. "Done but not visible": kẹt ở đâu
Kiểm từ dữ liệu đi ra: dữ liệu đúng chưa, đã ở Online hoặc live module chưa, job đã chạy chưa, cache hết hạn chưa, phần trang đó có nằm trong Hybris không?
| Triệu chứng | Layer khả dĩ nhất | Kiểm đầu tiên | Owner sửa |
|---|---|---|---|
| SKU activate nhưng không mua được | Data hoặc sync | KE-MER-PRD-01-04 theo thứ tự: chưa sync, index pending, hết stock, bị loại trừ, thiếu delivery mode | Merchandising (route MER-STK-01, MER-MST-02, MER-DLV-01) |
| Sau hide vẫn hiện | Data, sót một catalog | Mọi catalog phục vụ site (KE-MER-PRD-01-05) | Merchandising |
| Rule PUBLISHED, cart vẫn giá đầy đủ | Setup promotion | Website của rule vs promotion group mặc định của site; rule ở live module chứ không chỉ preview | Merchandising |
| Rule KNOXAPPROVED hàng giờ | Knox publish job | Inactive promotion report và job log; hai version approved (KE-TEC-TSP-01-01) | Tech; Samsung L2/L3 nếu lỗi nền tảng |
| Đổi ở AEM author nhưng chưa lên live | AEM publish hoặc cache | Đã publish, purge, kiểm lại cửa sổ ẩn danh (KE-MER-AEM-01-01) | Merchandising; TEC-TSP-01 nếu kéo dài |
| Footer khác nhau giữa home và cart | Nav sync job | Trạng thái và kết quả job gần nhất trong Backoffice › System › Background Processes › CronJobs | Tech (TEC-TSP-05, TEC-TSP-06) |
**Ví dụ TRN-041 (TH, site `test_smb_th`): hai rule, hai nguyên nhân khác nhau.** PR01 (10% off SM-S938BZKBTHL) PUBLISHED nhưng website là `thPromotionGroup` trong khi site dùng `test_smb_thPromotionGroup`; engine không bao giờ áp dụng. Đây là setup Merch: quay lại ticket Merch (vẫn ở ON HOLD COE) và đổi website cần Knox lại. PR02 (8% off SM-S921BLGCTHL) KNOXAPPROVED 49 giờ sau duyệt dù dates và website đúng, không có engine rule, job báo SUCCESS, và job log cho thấy hai version KNOXAPPROVED của cùng rule: lỗi publish của nền tảng (KE-TEC-TSP-01-01). Tech L2 dựng evidence pack 7 phần và tạo Maintenance Request; COEC sang SYSTEM SUPPORT. Không ai bảo subsidiary submit lại Knox vì sẽ tạo thêm version.

## Quiz (đáp án)
1 Đặt SKU approved + PURCHASABLE ở `vnEstoreProductCatalog` Staged 10' trước, `vn` vẫn không CTA → **B: catalog D2C đã sync sang Online chưa**. 2 Rule mới publish vào `th-preview-promotions-module`, qua simulator, khách không được giảm → **A: preview chỉ nuôi simulator; chưa publish vào live module (kèm Knox)**. 3 Promotion đã publish cần đổi end date → **B: Knox lại ở lần publish kế vì dates đổi**. 4 Footer cart VN khác home, AEM đã đúng → **B: nav sync job `vn-DotComCmsFooterNavSyncJob`; Tech, chạy lại cần PC ticket**. 5 Đổi message validate số điện thoại ở form địa chỉ → **C: message key trong code storefront; Tech L2 tạo Maintenance Request cho Samsung release**. 6 Giá đã đúng, đã sync, quá thời gian cache mà PDP vẫn giá cũ → **B: COEC liên kết cho Tech (flush cache), ticket Merch ở ON HOLD COE, tiếp tục containment nếu liên quan tiền**. 7 Rule KNOXAPPROVED 49 giờ, dates và website đúng, job SUCCESS, subsidiary đề nghị submit lại Knox → **B: không; submit lại tạo version mới; Tech điều tra publish job (KE-TEC-TSP-01-01) và escalate kèm evidence pack nếu lỗi nền tảng**.

## Practice
**PR-GP2.2-1. Năm case, năm phép kiểm đầu tiên** (20', giấy; facilitator đọc 5 case ngắn): (1) TH: rule PR01 (10% off SM-S938BZKBTHL) PUBLISHED trên `test_smb_th` nhưng cart test hiện giá đầy đủ (TRN-041); (2) TH: PR02 KNOXAPPROVED 49 giờ sau duyệt, dates và website đúng; (3) VN: trang cart hiện footer cũ, home hiện footer mới (TRN-042); (4) VN: QA85LS03BAKXXV đã unhide (approved + PURCHASABLE) và sync nhưng không add to cart được trên `vn` (TRN-007); (5) MY: banner homepage đổi ở AEM author 1 giờ trước, site live vẫn hiện banner cũ. Với mỗi case viết layer khả dĩ nhất, phép kiểm đầu tiên, owner sửa. **Pass:** 4/5 đúng kèm owner đúng. Đáp án: (1) setup promotion; website của rule vs promotion group mặc định (`thPromotionGroup` vs `test_smb_thPromotionGroup`); Merchandising, Knox lại sau khi đổi website. (2) Knox publish job; inactive report và job log, hai version approved (KE-TEC-TSP-01-01); Tech L2, Maintenance Request cho Samsung L2/L3 nếu lỗi nền tảng, không submit lại. (3) Nav sync job; trạng thái `vn-DotComCmsFooterNavSyncJob`; Tech (TEC-TSP-05, job lỗi TEC-TSP-06), chạy lại dưới PC ticket. (4) Stock; stock = 0 trong pool nên CTA mong đợi là stock alert chứ không phải Buy now (thứ tự KE-MER-PRD-01-04: sync, index, stock); Merchandising, route MER-STK-01 nếu cần stock. (5) AEM publish hoặc cache; đã publish, purge, cửa sổ ẩn danh (KE-MER-AEM-01-01); Merchandising, TEC-TSP-01 hoặc RHQ Platform nếu kéo dài. Không cần truy cập hệ thống.
