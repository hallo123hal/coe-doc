# MER-P3.1 AEM pages, banners, Shop App content

> Nguồn: page 2484044205 · 90 phút (Study 20' · Demo 15' · Quiz 10' · Practice 45') · Facilitator: Shift Leader/Sub-Lead · Capabilities C2, C4 · Cần xong MER-2.5 (L1); phải biết status path Shop Merchandising, tier R1–R3, cách ticket tới REVIEW SETUP. Mang bốn practice ticket SCOE-36 (TRN-030), SCOE-38 (TRN-032), SCOE-42 (TRN-036), SCOE-39 (TRN-033) cùng attachment. Truy cập staging Backoffice SMS el3-s2 (không HAC), Jira SCOE; phần content cần tài khoản EPP 2.0 CMS staging do trainer cấp và QA Auth cho AEM QA web `p6-qaweb-sa.samsung.com` (QA Auth mất ~24h trên wds.samsung.com nên xin từ hôm trước). Shop App CMS staging cần IP CoE whitelisted và account có role EPP EDIT. AU (TRN-033) chạy SMA cluster el5, chưa mở cho lab. EPP 2.0 CMS live vào qua WMC bằng SingleID, do RHQ cấp quyền. Không có access: triage và viết kế hoạch setup trên giấy (site × slot × field × value × asset × giờ); ghi "CMS staging not available – graded on the plan".

## Mục tiêu
Quyết định content nằm ở hệ thống nào (AEM author, EPP 2.0 CMS, Hybris Backoffice, Shop App CMS) và service ID nào; kiểm brief banner/text theo giới hạn field (HD01 30/78 ký tự, flag 18 ký tự, merch text SAVINA 300 byte) và viết một câu hỏi gộp cho các dòng sai; dựng banner matrix và internal check line với giờ go-live/kết thúc theo giờ market và ICT; làm cập nhật cosmetic trên staging (hoặc kế hoạch), lấy evidence before/after, verify trên preview và storefront; nêu đường duyệt và publish của từng công cụ, khi nào áp rule 23:59 và removal sub-task.

## Thuật ngữ
**Banner matrix** (bảng lập kế hoạch của MER-AEM-04: mỗi banner một dòng (slot, vị trí, asset, CTA, link, start, end), mỗi nhóm site một cột, điền trước khi sửa); **EPP 2.0 CMS** (công cụ cho trang store EPP ở `PIM > EPP v.2 > CMS > Page Mgmt`, flow Save > QA > Live, vào qua WMC bằng SingleID; tách biệt với Hybris và AEM author (WMS); AEM author chỉ cho trang multistore giữ trong AEM Sites; trang B2C samsung.com thuộc AEM team địa phương của subsidiary); **HD01_Home KV Carousel** (component hero homepage EPP 2.0: 1–7 slide, headline ≤30 ký tự, mô tả ≤78, ảnh desktop 1440×810, mobile 720×1280); **Merchandising flag (badge)** (tag ngắn trên tile sản phẩm, lưu như record AdditionalInfoV2 loại MERCHANDISING_FLAG: ≤18 ký tự, không số, không dấu phẩy, không HTML); **Old Hybris / New Hybris** (flag Hybris chỉ hỗ trợ market Old Hybris (AU, NZ, SG, MY, TH, VN); New Hybris (ID, PH) thì quản lý flag trong AEM); **Shop App operation policy** (bảng luật ASC nói ai sửa được khu nào; VD COE và subsidiary không sửa B2C Home (chỉ PTK từ 01/01/2026)); **ASC → Suwon approval** (duyệt hai cấp (ASC rồi Suwon Office) cho đổi KV image và category filter trên trang B2C Offer của Shop App); **Removal sub-task** (sub-task Jira tạo lúc go-live để banner bị gỡ vào end date; thiếu sẽ gây known error "expired banner live").

## Nội dung
### 1. Runbook MER-AEM-04 trên TRN-030
MER-AEM-04 (campaign page và banner) là pack chính. Low (24h, initial response 2h), standard change, R1, không PC ticket, không Knox (banner không chứa thay đổi giá). Checker là QA Team theo luật sampling, hoặc peer/Shift Leader cho thay đổi chỉ-copy và việc gỡ. Shift Leader duyệt trước PRD SETUP.
**TRN-030 (MY, SCOE-36):** requester xin thay slide 1 của carousel HD01 trên hai site EPP `epp_smetesting` và `my_dennis_test`, và gỡ slide 3 (banner "Back To School" đã hết hạn) trên `epp_smetesting`. Live D0 10:00 MYT, gỡ D+38 23:59 MYT; theo ICT là 09:00 D0 (MYT − 1 giờ). Triage thấy bẫy cài sẵn: headline dòng 2 "Year-End Tech Deals for Your Business" 37 ký tự, HD01 cho 30. Hỏi một lần, làm dòng 1 và 3 trong lúc đó, giữ STG SETUP vì còn việc làm. Dòng 1: headline `Year-End Tech Deals` (19/30), CTA `Shop now`, link tương đối `/offers/`; EPP 2.0 thêm prefix `https://www.samsung.com/<cc>/multistore/<store>` nên link về trang offers của chính site.
| Bước | Doer | Checker |
|---|---|---|
| 1 | APPROVED-ES → STG SETUP; viết internal check line và banner matrix | Matrix đủ so với brief và nhóm site; có internal check line |
| 2 | Chụp trạng thái trước của từng homepage (danh sách slide, thứ tự, ngày) | Có version hoặc ảnh before |
| 3 | Sửa slide 1, gỡ slide 3, giữ thứ tự slide khác | Đúng asset mỗi site và thiết bị; slot và vị trí như brief |
| 4 | Preview desktop và mobile, bấm mọi CTA | Nhãn và link CTA mỗi site; trang đích là path của site |
| 5 | Self-check, rồi QA REVIEW (sampling) hoặc peer check; Shift Leader duyệt; PRD SETUP | Lịch và giờ kết thúc đúng; không đụng component BC |
| 6 | Publish lúc go-live, live check một site mỗi nhóm, REVIEW SETUP, removal sub-task | Live sau publish trên site mẫu; banner gỡ đã mất, thứ tự đúng |
> Pack liệt kê bước màn hình và số hình nhưng AEM, EPP 2.0 CMS, Shop App CMS chưa có ảnh, và vài tên nút "chờ xác nhận ở KT". Màn hình staging khác runbook thì ghi "check on staging" trong evidence; không đoán.

### 2. Content nằm ở đâu
eStore chạy trên ba hệ thống: Hybris (sản phẩm, giá, stock, promotion, coupon, multistore), AEM (nội dung trang: home, campaign, offer có T&C, GNB) và Shop App CMS. Trước khi mở trang nào, quyết định công cụ theo loại site và loại content.
| Content | Công cụ và đường | Service | Đường publish |
|---|---|---|---|
| Trang B2C samsung.com (homepage, buy page, text/banner PD) | Không phải việc CoE: AEM team địa phương của subsidiary sở hữu | Không; trả dòng đó lại requester kèm lý do | – |
| Trang multistore trong AEM Sites (`/content/samsung/<cc>/multistore/...`) | AEM author (WMS) | MER-AEM-01, MER-AEM-04 (trang BC: MER-BCF-04) | Samsung Direct Workflow (System Admin publish ~1 phút) |
| Homepage, offer, PF, GNB của store EPP | EPP 2.0 CMS qua WMC (SingleID), `PIM > EPP v.2 > CMS > Page Mgmt` | MER-AEM-01 (trang cố định), MER-AEM-04 (banner) | Save > QA > Live |
| Merchandising flag và merch text | Hybris Backoffice, `Product Cockpit > Bulk Upload` (MERCHANDISING_FLAG, MARKETING/DELIVERY_MERCHANDISING_TEXT) trên master catalog | MER-TXT-03 (≤10 SKU), MER-TXT-01 (≥11) | Sync master > child Staged > Online |
| Shop App home, offer, shop, account | Shop App CMS, STG `opstools-s1-<cc>.seasam.org`, PROD `opstools-<cc>.seasam.org` | MER-SAC-01 | Request approval (role REQUEST-APPROVAL) > Publish (role PUBLISH) |
Hai luật tránh phần lớn lỗi: (1) Ops COE chỉ sửa site có AEM bật và RHQ Platform không tự chạy (EA OE, Samsung Members, SESP financing EPP); flag AEM (`isAemEnableSite`) ở bản ghi Website trong Backoffice (WCMS › Website); cả store thì nhờ Tech output query qua COEC liên kết, hoặc dùng danh sách site market trong KB. (2) Không đụng trang BC dưới việc banner; đó là MER-BCF-04, và B2C BC authoring không được làm trong giờ HQ.
TRN-030: tìm Backoffice chỉ chứng minh hai multistore tồn tại; homepage và component HD01 nằm ở EPP 2.0 CMS, không ở Hybris. TRN-033 cho phía Shop App: site AU `samsung_education_au` (EDU) và `government_au` (CORP) sửa trong Shop App CMS, ngoài Hybris.
> TRN-030 tiêu đề "#EPP Site Cosmetic Update" khớp MER-AEM-01 V2 (multi-site cosmetic pack) nhưng lab ánh xạ sang MER-AEM-04 V1 vì thay hero KV. MER-AEM-01 nói ranh giới cho campaign hero "xác nhận ở KT". Tới đó: đổi hero KV là MER-AEM-04, section cố định là MER-AEM-01.

### 3. Giới hạn text, badge, merch text
Lỗi content "không ai thấy" tới khi requester phàn nàn thường là vượt giới hạn field. Đếm ký tự bằng `=LEN` trong file brief trước khi nhận việc; dấu cách tính.
| Field | Giới hạn | Nguồn |
|---|---|---|
| HD01 headline / description | 30 / 78 ký tự | KB Homepage Components, qua MER-AEM-04 |
| Merchandising flag (badge) | 18 ký tự; không số, không dấu phẩy, không HTML; một flag mỗi SKU; flag Hybris thắng flag AEM | RHQ Merchandizing Flags (03/2026), MER-TXT-03 |
| Benefit flag (Benefits V4.0) | 26 ký tự (object khác; đừng nhầm) | TRN-032 |
| Merch text SAVINA (VN) | 400 ký tự gồm dấu cách và 300 byte; chỉ HTML màu, đậm, nghiêng, xuống dòng | KB merch text VN, TRN-036 |
**TRN-032 (ID, SCOE-38):** requester xin "Hybris badge" cho 8 SKU (VD `SM-S948BLBCXID`, `SM-X210NZAAXID`) trên `id_test1`. Hai bẫy: ID là New Hybris nên theo RHQ badge thuộc AEM và phải hỏi; và 4 dòng phá luật: dòng 4 "Exclusive EPP Price Drop" (24 ký tự), dòng 5 "Save 20% Today" (số), dòng 6 "Hot, Limited" (dấu phẩy), dòng 8 `<b>Hot</b>` (HTML). Dòng 1, 2, 3, 7 đi tiếp. Ngày: D0 00:00 WIB = D−1 17:00 GMT trong template.
**TRN-036 (VN, SCOE-42):** dòng 3 có 242 ký tự nhưng 315 byte vì chữ có dấu tiếng Việt chiếm 2–3 byte. Dòng 4 dùng `text-align`, EPP không hiển thị. Dòng 6 có `fpt` ở cả excludedSites và includedSites; excluded thắng. Với thay đổi V2 hai ngày sau, upload với **cùng tên**: tên mới tạo record thứ hai và text cũ vẫn live.
> MER-TXT-03 không có bản Confluence trong pack cache; luật flag 18 ký tự lấy từ vault pack và TRN-032. RHQ cũng nói màu chữ flag luôn xanh và không đổi được trong khi template upload có cột màu: mở tới KT; không đổi màu. Validation 18 ký tự HGE-10919 có bật trên el3-s2 chưa chưa verify; trainer đưa giá trị config dạng output query Tech chạy, bạn không chạy. AEM Additional Info Type: chỉ e-voucher (NZ, AU) còn dùng. disableCTA, PDP_NOT_AVAILABLE và delivery message không còn dùng (nay làm trong AEM hoặc GCDM). Không đặt.

### 4. Content Shop App (MER-SAC-01)
Low, R1, không có QA Team gate: peer kiểm trên AOS và iOS và Shift Leader kiểm evidence. Trước khi sửa, áp operation policy và luật copy.
| Khu | COE/subsidiary được làm | Duyệt |
|---|---|---|
| B2C Home | Không (chỉ PTK từ 01/01/2026); route cho ASC (campaign địa phương qua MKV4) | – |
| B2C Offer | Được | RTB không cần; đổi KV image và category filter cần ASC rồi Suwon Office |
| B2C Shop | Được | ASC duyệt |
| EPP Home / Offer / Shop / Account | Được | – |
Luật copy: không giá trị số trong head copy (09/2026); không CTA "Buy now" trên bất kỳ KV nào kể cả Offer KV (04/2026). ASC hoặc HQ không trả lời trong 24h sau khi post Jira thì comment ticket và go-live.
**TRN-033 (AU, SCOE-39):** sáu asset tuần 46. A01–A03 (entry point offer EDU và CORP, 720×1070) làm ngay. A04 (EDU Home Main KV) chờ copy mới vì head copy "Save up to $500" có số và CTA "Buy now". A05 (B2C Offer KV) chuẩn bị bản nháp và chỉ publish khi thấy duyệt ASC trên approval ticket. A06 (B2C Home Main KV) không làm: thuộc ASC. Go-live D0 00:00 AEDT = 20:00 ICT D−1 (AEDT − 4 giờ); kết thúc D+6 23:59 AEDT kèm revert plan.
> TRN-033 là ticket AU. AU chạy SMA el5, ngày 25/10/2026 account lab không login được el5 nên slot site còn placeholder. Làm TRN-033 như triage giấy và kế hoạch sản xuất tới khi trainer gắn dữ liệu staging.

### 5. Duyệt, publish, đóng ticket content
Mọi service content ở session này là R1: không Knox, không PC ticket, nhưng Shift Leader duyệt trước PRD SETUP. Checker phụ thuộc service, không phụ thuộc thay đổi trông nhỏ thế nào.
| Service | Checker | QA Team |
|---|---|---|
| MER-AEM-04 banner | QA Team, peer hoặc Shift Leader | Sampling: 20% ticket/tuần/cluster, tối thiểu 3; trong ticket được lấy mẫu một site mỗi nhóm cộng 10% phần còn lại (tối thiểu 2); 100% cho set gắn cờ launch và campaign page |
| MER-AEM-01 trang cố định | Operator thứ hai | QA Team (QAS-AEM-01) cho pack >10 site |
| MER-TXT-03 flag và text | Peer trước sync, Shift Leader duyệt | Khi yêu cầu hoặc mẫu |
| MER-SAC-01 Shop App | Peer trên AOS và iOS | Không (Shift Leader kiểm evidence) |
Sau PASS: Shift Leader duyệt, PRD SETUP, publish tay lúc go-live (không có lịch publish/unpublish), live check bởi người thứ hai trên một site mỗi nhóm, REVIEW SETUP kèm evidence PowerPoint. Requester không trả lời tới 23:59 thì publish đúng giờ và comment "Published as aligned for go-live at [date time]. No feedback received at the time of publishing." Tạo removal sub-task cho end date. Chỉ RHQ đóng ticket.
Last-minute request (VD raise 18:00 cho go-live nửa đêm) nhận comment "Last minute request, please QA on your own when it goes live. If any issue, please contact us." Tính vào báo cáo tuần. Mốc 17:00 VN và label `LastMinRequest` đến từ bản nháp cũ; xác nhận với Shift Leader trước khi dùng.
> Nguồn không thống nhất R1 content có qua QA Team không: QA-01 và QA-03 theo catalogue (sampling MER-AEM-04); QA-02 và CM-07 nói R1 không có QA gate; handover 23/10 nói thay đổi AEM CMS và Shop App CMS "cần QA verify"; CM-13 §7.2 nói "R1 do Shift Leader kiểm". Theo CM-13 làm mức tối thiểu và áp sampling catalogue khi dispatcher chọn ticket (open item DL-01 C1). Runbook sửa đổi (01/11) nay gửi mọi ticket AEM CMS và Shop App CMS sang QA REVIEW. (D9 under review.)

## Quiz (đáp án)
1 VN xin đổi hero KV trên 6 site EPP nội bộ; mở công cụ nào → **B: EPP 2.0 CMS `PIM > EPP v.2 > CMS > Page Mgmt`** (AEM author chỉ cho multistore trong AEM Sites; B2C là của AEM team subsidiary). 2 Brief banner có headline 37 ký tự cho carousel HD01, các dòng khác ổn → **C: làm dòng hợp lệ; hỏi requester một lần headline ngắn hơn** (ON HOLD SUBS chỉ khi hết việc để làm). 3 Requester ID xin "Hybris badge" cho 8 tile EPP; điểm đầu tiên cần nêu → **B: ID là New Hybris; theo RHQ flag quản lý trong AEM**. 4 Dòng merch text SAVINA có 242 ký tự → **B: chỉ sau khi kiểm byte; giới hạn SAVINA là 300 byte**. 5 D+2 requester VN đổi giá trị voucher trong merch text có sẵn; upload thế nào → **B: cùng tên với lần upload đầu** (tên mới tạo record thứ hai, text cũ vẫn live). 6 Yêu cầu Shop App AU có KV mới trên B2C Home → **C: không làm; B2C Home chỉ ASC/PTK; route cho ASC**. 7 Set banner ở REVIEW SETUP kèm evidence, go-live 00:00 giờ market, 23:59 requester vẫn chưa trả lời → **B: publish đúng giờ và đăng comment chuẩn "Published as aligned…"**.

## Practice
- **PR-MER-P3.1-1. Cập nhật banner EPP trên TRN-030** (30'; staging el3-s2 + tài khoản EPP 2.0 CMS staging của trainer, Jira SCOE-36): triage TRN-030, viết internal check line và banner matrix. Thay slide 1 HD01 trên `epp_smetesting` bằng asset TRAINING, gỡ slide 3 cùng site, preview desktop và mobile. Làm `my_dennis_test` chỉ sau khi trainer đóng requester gửi headline ≤30 ký tự. Dọn dẹp cuối (khôi phục trạng thái trước). **Pass:** headline 37 ký tự được phát hiện ở triage và hỏi trong một comment (không tự sửa); go-live ghi D0 10:00 MYT (09:00 ICT) và gỡ D+38 23:59 MYT; slide 1 có headline `Year-End Tech Deals`, CTA `Shop now`, link `/offers/`, ảnh 1440×810 và 720×1280; slide 3 đã gỡ và các slide khác giữ thứ tự; ảnh before/after mỗi site; CTA mở `/multistore/<store>/offers/` của chính site; ticket giữ STG SETUP khi chờ (không ON HOLD SUBS). Không có access: viết matrix, kế hoạch setup và câu hỏi gộp; trainer demo các bước author.
- **PR-MER-P3.1-2. Triage badge trên TRN-032** (20'; staging el3-s2 Backoffice, Jira SCOE-38): kiểm 8 SKU trong Backoffice (Advanced Search trên Product ở catalog ID, export kết quả) và đọc giá trị config HGE-10919 từ output query trainer đưa (Tech chạy). Đếm mọi text flag bằng `=LEN`. Viết một comment cho requester. Nếu trainer cho phần Hybris, upload 4 dòng hợp lệ với tên `TRAINING_<NAME>_TRN032_id_EPP_<SKU>_MERCH_FLAG` và `includedSites` = `id_test1`, rồi dọn. **Pass:** comment nêu điểm New Hybris/AEM và liệt kê dòng 4 (24 ký tự), 5 (số), 6 (dấu phẩy), 8 (HTML) kèm lý do; dòng 1, 2, 3, 7 đi tiếp; ngày bắt đầu D0 00:00 WIB ghi D−1 17:00 GMT; không record cho dòng 4, 5, 6, 8; dòng 7 không có site EPP Fokus; evidence gồm kết quả validation 18 ký tự hoặc ghi chú "validation not enabled on el3-s2". Không có access: đếm ký tự và viết comment trên giấy từ `flag-request.xlsx`.
> Khoảng trống: bước AEM, Shop App CMS, BO 2.0 chưa có ảnh (chưa có quyền công cụ); TRN-033 là ticket AU chưa gắn dữ liệu staging nên chỉ dùng triage giấy (kỳ vọng: A01–A03 làm, A04 chờ copy, A05 chờ duyệt ASC, A06 route ASC; go-live 20:00 ICT D−1). TRN-036 (SCOE-42) là luyện thêm tùy chọn cho merch text.
