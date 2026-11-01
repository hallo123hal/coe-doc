# GP2.1 From KB page to verified result

> Nguồn: page 2484208024 · 60 phút (Study 15' · Demo/thảo luận 10' · Quiz 5' · Practice 30') · Thực hành theo case trên staging và practice ticket; facilitator: Shift Leader hoặc Sub-Lead · Capability C2 · Cần xong G6.1, G5.1, G5.2 (Part A; Part B chỉ Tech); đọc trước hai trang KB "0. KB - Product Status (CTA)" và "0. KB - Product Active/Archive" (link ở MER-PRD-01 mục 7); mang check plan trống 5 dòng (precondition, expected, check, result, evidence). Truy cập: staging Backoffice SMS el3-s2 (Advanced Search + Export); Tech thêm HAC el3-s2 đọc-chỉ FlexibleSearch; Jira SCOE cho TRN-007; storefront staging `vn` và `test1`. Không có access: facilitator in sẵn export và ảnh storefront cho 5 SKU.

## Mục tiêu
Biến một trang KB thành check plan 5 bước (precondition, expected, bằng chứng); chọn phép kiểm rẻ nhất mà vẫn chứng minh được (màn hình Backoffice, export Backoffice, hoặc storefront; Tech thêm FlexibleSearch đọc-chỉ) và nói vì sao; chạy plan trên staging, ghi mỗi kết quả kèm giờ ICT; nhận ra trang KB lỗi thời hoặc thiếu và báo gap đúng cách.

## Thuật ngữ
**Check plan** (5 dòng từ một trang KB: precondition, expected, check, actual, evidence; mỗi SKU và catalog một plan); **CTA** (nút trên storefront, do sales status, approval, stock, pre-order quyết định; unapproved + PURCHASABLE ở VN hiện "Mua ở đâu"); **Cheapest sufficient check** (phép kiểm rẻ nhất vẫn chứng minh: một màn Backoffice cho một SKU, export Advanced Search theo catalog version cho nhiều SKU/catalog (Tech: FlexibleSearch chỉ đọc), storefront cho cái khách thấy); **Read-only FlexibleSearch** (SELECT trong HAC, chỉ Tech chạy; staging chạy trong lab, production cần lý do + PC ticket; Merch/QA lấy cùng dữ liệu từ Backoffice); **Staged vs staging** (Staged catalog là bản nháp trên production; staging environment el3-s2 là hệ thống test riêng); **KB gap** (chênh giữa trang KB và màn hình thật hoặc runbook, VD nhãn sai, thiếu case); **Page PIC** (một người duy trì trang kiến thức trên RHQ Confluence; gap báo qua comment trang và Sub-Lead).

## Nội dung
### 1. Đọc trang KB như một procedure
Trang KB của Samsung viết cho người đã biết hệ thống. Đọc như procedure, điền ba cột: **preconditions**, **steps/rules**, **expected result**; rồi ghi **trang không nói gì**.
Ví dụ "0. KB - Product Status (CTA)":
| Sales status | Approval | Điều kiện thêm | CTA trên eStore |
|---|---|---|---|
| PURCHASABLE | approved | còn hàng | Buy now (VN "Mua ngay") |
| PURCHASABLE | approved | đặt pre-order period | Pre-order now |
| PURCHASABLE | approved | hết hàng | Notify stock / get stock alert |
| PURCHASABLE | unapproved | – | Where to buy (VN "Mua ở đâu") |
| ARCHIVED | unapproved (hoặc check) | – | Không CTA; EPP: không tìm thấy sản phẩm trong multistore |
| (trong AEM, không phải Hybris) | – | – | Coming Soon (VN "Sắp ra mắt") |
| Sản phẩm add-on page | approved | – | Continue |
"0. KB - Product Active/Archive" thêm cặp theo loại SKU: SKU thường active = PURCHASABLE + approved, archived = ARCHIVED + check hoặc unapproved ("both are applicable"); quà Z-code active = PURCHASABLE_NOT_VISIBLE + approved; SKU trade-in T-code thì các trang KB khác nhau: bảng Active/Archive ghi ARCHIVED + check/unapproved ngay cả khi active, còn trang Product Normalization và trang trade-in MY, TH ghi approved + PDP_NOT_AVAILABLE. Theo runbook của nước; không chốt được thì hỏi Lead. Đây là ví dụ KB gap thứ hai.
Trang CTA **không** nói: đặt giá trị ở catalog nào (mỗi child catalog của site, Staged, rồi sync); chờ bao lâu storefront mới hiện; CTA text của EPP BC page cấu hình riêng; check khác unapproved thế nào với SKU archived. Một dòng ghi "Product Status: Approval" nhưng ý là Purchasable. Đây là các gap bạn đối chiếu với runbook.
> Hai trang KB không có heading nên không link theo section được; mở từ bảng KB của MER-PRD-01. MER-PRD-01 ghi trang Active/Archive liệt kê trạng thái khác cho SKU embargo (PURCHASABLE_NOT_VISIBLE, approved, theo thỏa thuận) so với runbook (ARCHIVED tới go-live); MER-PRD-01 sửa đổi (01/11/2026) chốt: giữ check hoặc unapproved với ARCHIVED tới go-live; approved + PURCHASABLE_NOT_VISIBLE trước launch chỉ khi subsidiary đồng ý bằng văn bản, để QA test promotion.

### 2. Biến trang thành check plan 5 bước
Viết **trước** khi đổi gì, để Checker theo được mà không cần bạn: (1) **Precondition** — SKU tồn tại ở mỗi catalog trong scope, có price row và stock nếu cần; (2) **Expected** — cặp giá trị từ KB và CTA dự đoán; (3) **Check A, data** — approval và sales status theo catalog version ở Online; (4) **Check B, customer view** — trang storefront theo loại catalog, sau indexing và cache; (5) **Record** — output query, ảnh, giờ ICT, một kết quả mỗi dòng.
**Ví dụ TRN-007 item 4, HW-S800B/XV trên D2C:**
| Dòng | Nội dung |
|---|---|
| Precondition | HW-S800B/XV trong `vnEstoreProductCatalog`, PURCHASABLE + approved, stock 200 (pool, đọc trên el3-s2 24/10/2026) |
| Expected | Unapproved + PURCHASABLE ở `vnEstoreProductCatalog` Online → CTA "Mua ở đâu" trên `vn`; EPP catalog không đổi |
| Check A | Backoffice Advanced Search theo SKU, export theo catalog version (approval, sales status) cho catalog `vn`, version Online. Tech có thể chạy cùng phép kiểm bằng FlexibleSearch chỉ đọc trên `TokoVariantProduct` ở HAC staging |
| Check B | Storefront `vn`: PDP hiện "Mua ở đâu"; storefront `test1` (EPP): không đổi |
| Record | Export và ảnh trong PowerPoint trên CoE workstation kèm giờ, VD "D0 14:25 ICT" |

### 3. Chọn phép kiểm
Chọn phép rẻ nhất mà **chứng minh** được kết quả. Màn hình có thể đọc nhầm không phải bằng chứng; storefront còn cache cũng không.
| Phép kiểm | Hợp cho | Giới hạn |
|---|---|---|
| Backoffice: Catalog › Products › SKU (Approval ở mục Essential; Sales Status ở tab Administration), hoặc Advanced Search + Export | Một SKU, hoặc export Checker theo catalog | Chậm khi nhiều SKU × catalog |
| Chỉ Tech: FlexibleSearch chỉ đọc trong HAC (mẫu query V-PRD01-01: status một SKU ở mọi catalog version) | Nhiều SKU và catalog cùng lúc; Staged vs Online | Chỉ SELECT. Trên production chỉ Tech chạy, cần lý do và PC ticket. Merch/QA không có HAC: dùng Backoffice Advanced Search + Export, hoặc nhờ Tech đưa output query trên COEC liên kết |
| Storefront: PDP và add to cart, một site mỗi loại catalog | Cái khách thấy | Cần sync, indexing, cache; add-to-cart trả resultCode 0000 khi active còn hàng, 0001 "Sorry, there is no stock for this product." khi archived |
Phân biệt ba nghĩa: **staging environment** el3-s2 là hệ thống test riêng cho training, BVT, Tech test trước PC ticket; **Staged catalog** là bản nháp trên production — đổi chỉ ở Staged vẫn là đổi production; **STG SETUP** của Jira chỉ là một bước workflow.
Luật lab el3-s2: đang dùng cho BVT ENH-92 RC1; chỉ đổi SKU trainer giao, ghi giá trị trước và khôi phục; HAC chỉ Tech và chỉ đọc; không ai chạy cronjob, Initialization hay Update.

### 4. Chạy plan và đọc kết quả
Chạy Check A (data) trước, rồi Check B (customer view). Khi kết quả khác dự đoán, dùng known error của service trước khi đoán.
**Runbook MER-PRD-01 (verify thay đổi status):** (1) Doer export status theo catalog version cho mỗi SKU (Tech có thể chạy V-PRD01-01) / Checker: Online bằng Staged cho mỗi catalog yêu cầu; (2) so với cặp mong đợi từ KB / Checker: từng dòng, không catalog nào ngoài yêu cầu bị đổi; (3) chờ indexing và cache rồi test PDP và add to cart trên một site mỗi loại catalog / Checker: mẫu storefront mỗi loại; (4) ghi giờ ICT và đính evidence / Checker: evidence đủ; internal check line khớp.
| Known error | Triệu chứng | Kiểm theo thứ tự |
|---|---|---|
| KE-MER-PRD-01-04 | Đã activate nhưng không mua được | Chưa sync, index pending, hết stock, bị loại trừ, thiếu delivery mode; route sang MER-STK-01, MER-MST-02, MER-DLV-01 |
| KE-MER-PRD-01-05 | Sau hide vẫn hiện trên D2C | Chỉ đổi ở một catalog; áp dụng cho mọi catalog phục vụ site |
| KE-MER-PRD-01-09 | Bulk edit bỏ sót SKU | Khoảng trắng trong mã; trim, chạy lại, so số dòng |
**Ví dụ MER-PRD-01 §5 (PH):** monitor activate (approved + PURCHASABLE), soundbar deactivate (check + ARCHIVED) trong `phEstoreProductCatalog` và `phEppProductCatalog`. Storefront: monitor add to cart được ở một eStore và một EPP site; soundbar "no longer available". Chỗ hay trượt: quên EPP catalog (KE-05), hoặc đặt "deactivate" là unapproved thay vì check + ARCHIVED.

### 5. Nhận ra trang lỗi thời và báo
RHQ Confluence là single source of truth. Một số trang lỗi thời vì vendor trước không cập nhật; BiPlus có thể cập nhật, và khi nghi ngờ thì hỏi RHQ trước khi theo. Bảng KB của MER-PRD-01 cho thấy lần cập nhật cuối của từng trang: trang từ 2025 trở về trước (VD "PH - Fundamental SKU setup for MX", 2025-04) có thể lỗi thời, đối chiếu với bước và ảnh runbook.
**Báo gap:** (1) dừng, không đoán; nếu chặn ticket live thì báo Shift Leader, ticket chờ trong SLA trong khi người certified L3 hoặc Sub-Lead kiểm; (2) comment lên trang: trang nói gì, bạn thấy gì (màn hình, kết quả query, ngày giờ ICT, môi trường), nguồn bạn theo; (3) báo Sub-Lead. Không tự sửa runbook đã phát hành trừ khi được giao; page PIC cập nhật và ghi change history.
VD comment cho gap trang CTA: "The OOS row says 'Product Status: Approval'. On el3-s2 (D0 14:30 ICT) an approved, PURCHASABLE SKU with stock 0 shows the stock alert CTA. Please confirm the row means Purchasable. Source: MER-PRD-01 V2 step 6."
> Kênh chính xác để báo gap trên trang KB Samsung (comment trang, Sub-Lead hay page PIC của RHQ) mô tả cho runbook ở MR-05 §5.4 và cho trang kiến thức ở CM-13 §18.1, nhưng chưa có procedure chung cho KB space đã copy. Comment lên trang và báo Sub-Lead cho tới khi Process and Knowledge Lead đặt kênh.

## Quiz (đáp án)
1 Sau "unhide", QA85LS03BAKXXV approved + PURCHASABLE ở D2C Online với stock 0, CTA trên `vn` → **B: Notify stock / get stock alert** (C là CTA của unapproved + PURCHASABLE — bẫy của item 4). 2 Xác nhận status 7 SKU trong 3 catalog VN, Staged và Online, trên staging → **B: một Backoffice Advanced Search với export theo catalog version liệt kê SKU, catalog, version, sales status, approval status** (C không chứng minh Staged vs Online và phụ thuộc cache). 3 SKU đã hide vẫn hiện trên D2C, data `vnEstoreProductCatalog` Online ARCHIVED + check → **A: kiểm catalog khác phục vụ site còn active không (KE-MER-PRD-01-05)**. 4 Đồng nghiệp: "chỉ đổi ở Staged nên không phải đổi production" → **B: sai; Staged catalog là bản nháp trên production nên vẫn theo runbook, QA gate và duyệt**. 5 KB nói đặt SKU embargo PURCHASABLE_NOT_VISIBLE + approved còn runbook MER-PRD-01 nói ARCHIVED tới go-live → **B: theo runbook, ghi khác biệt lên ticket; dùng trạng thái của KB chỉ khi subsidiary đồng ý bằng văn bản**. 6 Thấy dòng KB sai → **C: comment lên trang với trang nói gì, bạn thấy gì, giờ ICT, nguồn đã theo, và báo Sub-Lead**. 7 Query nào chạy được trên production mà không cần duyệt → **B: query chỉ đọc có lý do ghi lại; report và dữ liệu lịch sử cần PUMI được duyệt trước** (UPDATE cần PC ticket).

## Practice
**PR-GP2.1-1. Check plan cho product status và CTA** (30'; staging el3-s2, site `vn` và `test1`, ticket TRN-007 sau khi setup item 1, 3, 4 xong bởi trainer hoặc ở GP1.3; không đổi gì). Dùng "0. KB - Product Status (CTA)" viết check plan 5 bước và dự đoán CTA trên `vn` cho QA50LS03BAKXXV, QA50LS03DAKXXV, QA65LS03FAKXXV, QA85LS03BAKXXV, HW-S800B/XV. Kiểm từng dự đoán bằng một Backoffice Advanced Search + export theo catalog version (SKU, catalog, version, sales status, approval status trong catalog `vn`, Online) và storefront. Tech có thể dùng một FlexibleSearch chỉ đọc ở HAC staging thay export. Ghi mọi kết quả kèm giờ ICT. Ghi một gap của trang KB. **Pass:** 5/5 dự đoán giải thích được bằng rule KB — ba TV ARCHIVED + check → không CTA trên `vn` và không search được trên EPP; QA85LS03BAKXXV approved + PURCHASABLE stock 0 → CTA stock alert; HW-S800B/XV unapproved + PURCHASABLE trên D2C → "Mua ở đâu", EPP không đổi. Không đổi gì; query Tech chỉ SELECT. Mỗi kết quả có giờ ICT và evidence làm trên CoE workstation. Một KB gap nêu rõ trang nói gì, bạn thấy gì. Không có access: dùng export và ảnh storefront in sẵn.
