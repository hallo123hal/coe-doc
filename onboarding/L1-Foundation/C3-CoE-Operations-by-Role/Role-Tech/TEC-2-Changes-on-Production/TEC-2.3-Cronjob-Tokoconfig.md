# TEC-2.3 Cronjob, Tokoconfig, configuration

> Nguồn: page 2483191911 · 60 phút (Study 20' · Demo 10' · Quiz 10' · Practice 20') · Lecture + lab Backoffice & HAC staging; facilitator: Tech Sub-Lead · Cần xong TEC-2.2, G4.1. Không có access thì xem demo và đọc kết quả từ screenshot facilitator.

## Mục tiêu
Tra một cronjob trên Backoffice và HAC staging, đọc đúng Status, Result, end time; gọi tên cronjob đưa order qua từng status chính; tra TokoConfigProperty và giải thích scope từ suffix; chọn đúng loại duyệt cho: xem, chạy lại, tạo mới, đổi tham số cronjob, đổi Tokoconfig.

## Thuật ngữ
**Job** (code làm một việc, VD chuyển consignment tới kho); **CronJob** (record chạy job: tham số, site áp dụng, status, result, log mỗi lần chạy); **Trigger** (lịch chạy dạng cron expression, `*/5 * * * *` = mỗi 5'); **Status / Result** (Status: RUNNING, FINISHED; Result: SUCCESS, FAILURE, ERROR); **TokoConfigProperty** (type lưu setting key = value của platform Toko, đổi không cần deploy); **Suffix `.xx`** (cuối key là mã store/site, VD `.vn`; key không suffix là setting cấp cluster); **HAC property** (setting hiện ở Platform › Configuration, VD `backoffice.forgot.accessSeconds`); **`COEC_logs_extract`** (label Jira xin Kibana log cũ hơn cửa sổ lưu ~3 tuần).

## Nội dung
### 1. Job, cronjob, trigger và cách đọc cronjob
Job là code; cronjob là record cấu hình chạy code đó; trigger là lịch. VD `tokoPaymentEventQueueExecuterCronJob` có lịch `*/5 * * * *` (mỗi 5'). Một job có thể có nhiều cronjob, mỗi site một cái nên tên thường bắt đầu bằng mã site `xx-`. Đọc cronjob: xem Status, Result, End time của lần chạy cuối, nếu lỗi thì đọc log (Status FINISHED + Result FAILURE = chạy xong nhưng thất bại). Tra ở: Backoffice › System › Types › `CronJob` › Search by type, lọc theo code; hoặc FlexibleSearch Query 5 textbook ch.07 (`CronJob` LEFT JOIN `CronJobStatus`, `CronJobResult`, ORDER BY `{cj.endTime}` DESC).

### 2. Cronjob đưa order đi qua các status
Order kẹt ở một status >1 giờ → kiểm consignment và cronjob tương ứng, đọc lỗi của step trong process. Hai status tài chính dễ nhầm: WAITING_FOR_SEND_FINANCIAL = chờ gửi FI đầu tiên sang N-ERP (trước split); WAITING_FOR_FINANCIAL = N-ERP đã gửi billing number, chờ hoàn tất tài chính. ORDER_SPLIT là status của order, `splitOrder` là step của process.

| Chuyển status order | Cronjob |
|---|---|
| WAITING_FOR_CAPTURE_RESULT → WAITING_FOR_SEND_FINANCIAL | `tokoPaymentEventQueueExecuterCronJob` |
| WAITING_FOR_SEND_FINANCIAL → ORDER_SPLIT | `xx-tokoFinancialInitialUpdateJob` |
| ORDER_SPLIT → SHIPPING_REQUESTED | `xx-tokoTransferConsignmentToWarehouseJob` (consignment chờ ở WAITING_FOR_TRANSFER tới khi gửi; N-ERP trả SO) |
| SHIPPING_REQUESTED → SHIPPING_PREPARATION → SHIPPED | `xx-bulkFetchConsignmentUpdateJob` (nhận DO, rồi 1st GI từ NERP) |
| WAITING_FOR_FINANCIAL → COMPLETED | `xx-tokoFinancialCompletionJob` (cần billing number từ NERP) |
| Return → COMPLETED | `xx-tokoReturnsProcessCheckStatusJob` |

Cronjob dọn dẹp cấp cluster: `SMS-ProductReferenceRemovalCronJob` / `SMA-ProductReferenceRemovalCronJob` xóa product reference EXPIRED/INACTIVE (SMS bật cho NZ và TH; SMA cho AU); `toko-sms-RemoveExpiredDiscountRowsScriptCronJob` xóa discount row hết hạn >60 ngày (SG, MY, ID, PH, NZ, TH, VN). Cronjob tích hợp hay gặp: sync stock lên 3PD (từ khóa `marketplacestocksync`); trade-in PH Bolttech (`ph-boltechTradeInImportData`, `ph-boltech-product-price-imports`); menu & footer EPP (`xx-DotComCmsEppNavSyncJob`, `xx-tokoDotComCmsEPPFooterNavSyncCronJob`); e-invoice MY (`tokoB2BITaxInvoiceRevalidationDailyBaseCronjob`); giá AU (`knoxPriceValidityCheckJob`, `knoxPriceApplyingJob`); report (VD `toko-sg-tokoSalesNonPIIReportJob`). **Log:** Kibana giữ ~3 tuần (thực tế 25–26 ngày); log cũ hơn thì Tech Level 2 tạo ticket cho Samsung L2 (SDS India) với label `COEC_logs_extract`.

### 3. Duyệt cho việc liên quan cronjob
- Xem cronjob, đọc log: chỉ đọc, không PC.
- Chạy lại cronjob / sync tay trên production: **PC; không hoàn tác**; job đụng order, giá, payment cần second check (TSP-06); chỉ Tech chạy; Merch/QA không bao giờ; không ai chạy Initialization/Update (CM-13 §9.1).
- **Tạo cronjob mới:** RHQ D2C Platform Head rồi HQ GMO; mô tả mục đích & field, đính ImpEx, kèm test staging; cronjob có PII cần thêm HQ PUMI; Tech không tự tạo.
- Report cronjob mới hoặc đổi người nhận: PUMI trước rồi PC; thêm/bớt field không-PII: không PUMI nhưng vẫn PC; thêm field PII: quy trình PII (TEC-3.3).
- **Đổi tham số cronjob** nằm trong danh sách Backoffice Config Change: RHQ duyệt + test staging + PC.

### 4. Tokoconfig và HAC property
**Tokoconfig:** TokoConfigProperty là cặp key = value lưu như data, bật/tắt tính năng theo store/site. Tech đổi bằng ImpEx hoặc Backoffice, luôn với PC (service CFG-03); ImpEx/Groovy production bắt đầu bằng ITGC header `#NOTE ITGC_JIRA:PC-1234(COEC-5678)` (Groovy `//NOTE …`), file mới chạy staging trước; Merch/QA không có HAC → nhờ Tech qua linked COEC.
- VD tách quà FOC thành consignment riêng khi delivery mode khác máy chính: cần **cả 3 key TRUE** — `toko.autoAssign.deliverymode.on.foc.disabled.xx`, `toko.enable.splitby.deliverymode.xx`, `new.foc.flow.enabled.xx`.
- `payment.info.external.system.enabled.xx` bật Samsung Vault; `external.system.vault.delete.enable.xx` cho khách xóa thẻ đã lưu.
- `toko.overselling.backorder.count.enabled` là setting cấp cluster (không suffix); KB nói rõ **không được đổi thành FALSE**.
Tokoconfig ≠ HAC property. Property hiện ở Platform › Configuration (chỉ đọc): `toko.backoffice.forgot.enable=true` bật "forgot password" Backoffice; `backoffice.forgot.accessSeconds=1800` làm link hết hạn sau 1.800 giây. Đổi property cũng là Backoffice Config Change.

### 5. Ba cấp cấu hình
Với delivery mode & payment mode: Multistore thắng trước, rồi Website (CMSSite), rồi Base Store; base store bắt buộc ở mọi nước; PH, ID, TH dùng Site Payment Config thay cho cấp website cho payment mode. Thêm payment mode vào multistore thì base store phải có sẵn; gỡ khỏi multistore thì cũng kiểm base store và website.

### Điểm đáng nhớ từ KT
Không tạo cronjob trên production khi chưa duyệt; duyệt cần PUMI do người xin data raise. Gần như mọi thay đổi cấu hình Backoffice có quy trình duyệt riêng → dùng danh sách Backoffice Config Change + test staging + PC. Có một database do HQ quản hoàn toàn, team không bao giờ sửa. EPP site mới/kích hoạt lại: có email duyệt thì để ticket chờ RHQ (ON HOLD HQ ở COEC, ON HOLD RHQ ở Shop Merch); không có email thì không build (kể cả staging), trả subsidiary kèm link template RHQ bằng ON HOLD SUBS — **không "reject"** (CM-13 ch.13).

## Quiz (đáp án)
1 Order kẹt ORDER_SPLIT >1h → kiểm trước `xx-tokoTransferConsignmentToWarehouseJob` (và đọc lỗi step `splitOrder`; ca phổ biến nhất là không có tồn ở kho nào dùng được — "missing values for [warehouse]"). 2 Subsidiary báo sai tồn, đòi chạy lại stock cronjob gấp → **PC duyệt, và chỉ Tech chạy**. 3 Thêm 1 người nhận vào report cronjob đang chạy → **PUMI duyệt, rồi PC, rồi làm**. 4 Tách quà FOC thành consignment riêng → **đặt cả 3 key FOC TRUE**. 5 Key cấp cluster không được đặt FALSE → `toko.overselling.backorder.count.enabled`. 6 MY e-invoice chạy 2 lần/ngày thay vì 1 → **Backoffice Config Change kèm PC** (Lead xác nhận lịch có tính là tham số không; tới lúc đó câu này không tính điểm). 7 Cronjob Status FINISHED, Result FAILURE → **chạy xong nhưng thất bại; đọc log, mở COEC** (chạy lại cần PC).

## Practice
- **PR-TEC-2.3-1** (HAC + Backoffice staging, 12'): sửa Query 5 thành `... WHERE ({cj.code} LIKE '%Financial%' OR {cj.code} LIKE '%Consignment%') ORDER BY {cj.endTime} DESC` → danh sách cronjob có tiền tố site, status, result, endTime; thêm `AND {r.code} IN ('FAILURE','ERROR')` chỉ giữ lần chạy lỗi (0 dòng trên staging vẫn hợp lệ); chọn một cronjob, mở ở Backoffice (System › Types › CronJob › Search by type), so Status/Result/End time với kết quả query, xem trigger nếu màn hình có; viết nháp comment COEC tiếng Anh cho một cronjob FAILURE mô phỏng nêu bước kế và nói rõ chạy lại cần PC. Pass: query chạy và khớp Backoffice; comment không đề xuất chạy lại trước khi có PC.
- **PR-TEC-2.3-2** (8'): Backoffice › System › Types › `TokoConfigProperty` › Search by type, lọc key kết thúc bằng mã store của team (VD `.vn`); chọn 3 key có trong bảng KB Tokoconfig, ghi giá trị, cấp (Store/Site) và ý nghĩa; HAC › Platform › Configuration tìm `toko.backoffice.forgot.enable` ghi giá trị. Pass: giải thích đúng 3 key so với KB; nêu đúng loại duyệt để đổi (Backoffice Config Change + PC).
