# MER-2.2 Price and Knox price approval

> Nguồn: page 2483257480 · 60 phút (Study 20' · Demo 8' · Quiz 7' · Practice 25') · Facilitator demo price row và PriceInfoChange trên staging; learner làm một mình; facilitator: Sub-Lead certified PRC-01…03.
> Cần xong G3.3, G2.6, MER-1.2 (A.13), MER-1.3 (before value). Quyền: Backoffice staging s2, sửa price row ở `vn` B2C child (Staged), Product Cockpit; BO right cho Knox price là *Business PIC* và *PriceInfoChange* (trang Merchandising BO Access) — trên staging chỉ xem, không submit.

## Mục tiêu
Tạo SPECIAL price row ở Staged child, sync, kiểm staging PDP, dọn data; kiểm file giá của subsidiary theo 5 điểm, đổi validity sang GMT, viết một câu hỏi gộp thay vì tự sửa; lấy Knox price path từ cột approval path của brief, đối chiếu bảng 06 Knox Approvals, báo Sub-Lead khi lệch, điền đúng field PriceInfoChange; áp đủ control R3 cho giá.

## Thuật ngữ
**Price row**; **Discount row** (dòng discount gắn SKU, PRC-03; sửa cũng tạo PriceInfoChange); **PriceInfoChange** (bản ghi Hybris tạo khi giá đổi, dùng để gửi Knox; giá chỉ áp dụng sau khi Knox duyệt); **validityFrom/validityTo** (cột ngày trong template, text theo GMT); **Site Matrix** (bảng cmsSite thuộc catalog nào: Estore, EPP, SME, 3PD, Financing; VD `vnshopee` thuộc VN 3PD catalog); **PS-01…04, PS-13** (price sanity rule; đủ 14 rule ở MER-3.1); **Diff file** (so giá cũ/mới: SKU, old, new, % đổi, flag vi phạm; bắt buộc >100 dòng); **Dry run**; **Division** (MX, VD (EB), VD (TV), HA, AC — quyết định Knox path); **NOTIFIER** (người chỉ nhận thông báo trong approval line; CoE chỉ thêm/bớt NOTIFIER dưới path HOD).

## Nội dung
### 1. Tạo special price thủ công
Special price = price row loại SPECIAL, hiện là giá chính trên website. Administration Cockpit › Catalog › Products → chọn SKU, **bản Staged của child catalog** → tab Price › "Create a new price row" (Unit = pieces, Price, Currency) → trên dòng mới: ba chấm › Edit Details, kiểm catalog version là Staged và price type SPECIAL → Save → sync Staged lên Online. Trên website giá đặc biệt là giá chính, giỏ hiện tổng tiết kiệm. **Ghi giá cũ lên ticket (before value) trước khi đổi**; rollback giá = trả về before value.

### 2. Template giá, GMT, Site Matrix
Template special price: modelCode; price *hoặc* discountPercent (không bao giờ cả hai); currency; unit = pieces; cmsSite chữ thường, cách nhau dấu phẩy không dấu cách; minqtd; validityFrom/validityTo dạng text `YYYY-MM-DD HH:MM:SS` theo **GMT**. MY, SG, PH = GMT+8 → 00:00 local = 16:00 GMT hôm trước; ID, TH, VN = GMT+7 → 00:00 local = 17:00 GMT hôm trước; AU/NZ phụ thuộc DST. Bulk: Product Cockpit › Special Price › tải template (chỉ tải được template của nước mình) → chọn đúng child catalog → điền → Import → chờ trạng thái xanh "in sync" → sync SKU lên Online → kiểm website. Site Matrix VN: `vn,ea,vn_ea_oe` thuộc Estore; `vnlazada,vnshopee,vntiki,vntiktok` thuộc 3PD catalog. cmsSite sai = sai market hoặc sai kênh.

### 3. Kiểm file giá của subsidiary — 5 điểm, sanity, bulk, E4
**Không sửa file của subsidiary.** Trước khi upload kiểm 5 điểm: mọi field bắt buộc đã điền; currency đúng; không dấu cách trong SKU/cmsSite; cmsSite khớp Site Matrix; thời gian theo GMT. Sai → trả file kèm một câu hỏi gộp.
Price sanity chạy trước build (ngưỡng mặc định là đề xuất, Lead xác nhận): **PS-01** giá dưới floor (không có floor thì <50% RRP); **PS-02** giảm ≥20% so với giá bán hiện tại cần xác nhận văn bản; **PS-03** giá mới/giá cũ <0.5 hoặc >2, hoặc khác số chữ số (VD file ghi 25.990 thay vì 25.990.000); **PS-04** giá bán > RRP, giá gạch ngang < giá bán, giá 0/trống; **PS-13** file >100 dòng phải có diff file.
Bulk & E4: >100 dòng cần diff file + dry run, kiểm 5 điểm (số dòng, SKU trùng, ô trống/0, currency & dấu thập phân, dòng bị flag); screenshot before/after ≥5 SKU (giá cao nhất, thấp nhất, giảm sâu nhất, SKU launch, 1 SKU ngẫu nhiên); **sai 1 SKU là cả file FAIL**; diff file không rời hệ thống Samsung. **File ≥500 SKU là E4**: Merch Lead/Deputy duyệt cấp 2; không tách file để né E4.

### 4. PriceInfoChange và gửi Knox
Bulk price upload, sửa price row, sửa discount row, hoặc bật "multistore discount off" đều tạo PriceInfoChange ở Price Settings › Prices › PriceInfoChange. Sau khi Knox duyệt → KNOXAPPROVED → COMPLETED; cronjob `knoxPriceApplyingJob` áp giá đã duyệt vào phút 45 mỗi giờ. Merch cần 2 BO right: Business PIC và PriceInfoChange.
Gửi Knox giá (SOP Knox Approval submission): (1) Business PIC = người tạo ticket (CoE tạo hộ thì là người yêu cầu; thiếu Business PIC thì nhờ subsidiary tạo COEC ticket để thêm); (2) Approval Title & Comment = "Ticket Number & Ticket Title"; (3) Approval Process lấy từ cột approval path của brief, **CoE không tự chọn** (CM-13 §10.2); path trong brief không hợp division SKU/bảng 06 thì hỏi Sub-Lead trước khi submit; chỉ submit **một** path; RRP của F-code/Z-code/Packcode hỏi ticket creator; RRP của SC+ MX luôn đi path MX; (4) đã raise thì không sửa tay approval line/nội dung — muốn đổi phải cancel và submit mới; (5) ghi giờ gửi & path lên ticket (A.13), theo dõi trong handoff note.

### 5. Knox price path (06 Knox Approvals) và lỗi hay gặp

| Division | Discount | Knox approver |
|---|---|---|
| CE (VD, DA) | <25% | eStore Sales Head |
| CE (VD, DA) | 25% đến <30% | thêm HOD |
| CE (VD, DA) | 30% đến <40% | eStore Head, HOD, CFO subsidiary |
| CE (VD, DA) | ≥40% | thêm President subsidiary |
| MX | mọi mức | eStore Head, HOD, CFO, President |

Đổi approver là thủ tục chính thức: subsidiary tạo COEC ticket kèm email xác nhận từ Suwon D2C RPM PIC, Ops COE giao cho RHQ D2C Platform Head duyệt trước khi ai làm gì. Lỗi hay gặp: dùng giờ local thay vì GMT; cmsSite viết hoa/có dấu cách; quên **Block price import** nên NERP ghi đè giá; quên sync; sửa tay approval line đã raise.

### Điểm đáng nhớ từ KT
RHQ có bộ template request đã duyệt (new product, SC+, merchandising tags, price, special price, promotion brief, delivery mode, new/EPP site): chỉ dùng bản mới nhất; muốn đổi template phải đề xuất RHQ — CoE không tự sửa. Subsidiary đôi khi dán bảng vào ticket thay vì dùng template → không dựng lại/sửa data, thiếu/mơ hồ thì trả lại với một câu hỏi gộp (CM-05 §3.4). File bị mã hóa → nhờ người upload mở khóa.

## Quiz (đáp án)
1 Special price MY bắt đầu 00:00 01/12/2026 local → validityFrom **2026-11-30 16:00:00**. 2 Một dòng có cả price và discountPercent → **trả file kèm một câu hỏi gộp**. 3 Giảm 35% TV (VD) → **eStore Head, HOD, CFO subsidiary**. 4 Approval đã raise nhưng chọn sai line → **cancel và submit mới**. 5 File 650 SKU → **diff file, dry run, và Lead cấp 2 duyệt (E4)**; không tách đôi để né E4. 6 Đặt giá khác RRP cho SKU Normal, sáng hôm sau quay về RRP → **chưa bật Block price import**. 7 Đã tạo SPECIAL ở Staged và Save mà PDP vẫn giá cũ → **chưa sync Staged lên Online**.

## Practice
- **PR-MER-2.2-1** (staging, 12'): ghi before value (RRP, trạng thái Block price import, các price row sẵn có); tạo price row Unit pieces, Price = RRP −10% (làm tròn), VND; kiểm Staged + SPECIAL, đặt validity hôm nay → +2 ngày; Save; sync (hoặc nhờ facilitator); ghi giá bán và giá gạch ngang trên staging PDP; **dọn**: xóa price row ở Staged, sync lại, PDP về RRP. Pass: screenshot PDP trước/sau; special price là giá chính, RRP gạch ngang; data về before value; giải thích được chuyện gì xảy ra với giá nhập tay nếu không bật Block price import. Nếu staging tạo PriceInfoChange chờ Knox và giá không áp: dừng, chụp bản ghi, báo facilitator, **không submit Knox** — vẫn tính đạt (Lead xác nhận hành vi staging trước cohort).
- **PR-MER-2.2-2** (giấy, 8'): (a) điền 2 dòng special price MY (B2C `my` và 1 EPP MY tra Site Matrix), validity 01/12/2026 00:00 → 07/12/2026 23:59 giờ MY → validityFrom `2026-11-30 16:00:00`, validityTo `2026-12-07 15:59:00` (giây :00/:59: Lead xác nhận); (b) kiểm file 6 dòng giả → tìm đủ 5 lỗi: dòng 2 có dấu cách trong SKU; dòng 3 có cả price và discountPercent; dòng 4 dùng giờ local; dòng 5 <50% RRP (PS-01, cả PS-03); dòng 6 cmsSite viết hoa. Viết một câu hỏi gộp tiếng Anh bằng template C.10 (MR-06 Appendix C), không tự sửa file.
- **PR-MER-2.2-3** (staging view + giấy, 5'): mở Price Settings › Prices › PriceInfoChange ghi tên field & status (không submit). Ba brief: (1) VD TV 27% "eStore Sales Head, HOD"; (2) HA 42% "eStore Head, HOD, CFO"; (3) MX 10% "MX: eStore Head, HOD, CFO, President". Đối chiếu bảng 06: (1) và (3) khớp → dùng nguyên path brief; (2) **lệch** (42% cần thêm President) → không tự đổi path, hỏi Sub-Lead trước khi submit. Viết A.13 cho DEMO-6201 (case 1): Approval Title dạng "Ticket Number & Ticket Title", ghi path + giờ gửi, status không đổi.
