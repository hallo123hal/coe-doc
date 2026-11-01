# TEC-P2.1 HAC, FlexibleSearch, ImpEx and Groovy with a PC ticket

> Nguồn: page 2484535429 · 120' (Study 30' · Demo 20' · Quiz 10' · Practice 60') · Facilitator: Shift Leader/Sub-Lead · Capabilities C2, C4, C5 · Cần xong TEC-2.1, TEC-2.2, TEC-2.3 (mở HAC, chạy SELECT, đọc header ImpEx, giải thích vì sao cần PC). Mang TRN-038 (SCOE-44) với `scope-list.csv`, `precheck-queries.sql`, `archive_TRN038.impex`, `rollback_TRN038.impex`, `pc-ticket-draft.md`. Access: staging Backoffice + HAC el3-s2, Jira SCOE. Chỉ Tech chạy ImpEx trong lab, sau khi trainer/Tech Lead duyệt; chỉ chạm 3 SKU pool (`QA65Q60RAKXXM`, `SM-R177NZKAXME`, `SM-R770NZSAXME`) và chỉ version **Staged** của `mysmeProductCatalog`, `myb2bProductCatalog`; không sync Online, không cronjob. Không có access: trainer chạy import, bạn làm các bước khác trên giấy.

## Mục tiêu
Viết query read-only cho 5 câu hỏi điều tra và ghi lý do lên ticket; chuẩn bị ImpEx với mandatory line, đúng catalog version, scope khớp danh sách code, rollback từ giá trị BEFORE đã export; biết khi nào dùng Groovy và review DRY_RUN, scope, output, commit mode; hoàn tất 3 lớp kiểm soát nội bộ và PC ticket để RHQ duyệt ngay lần đầu, rồi chạy pre-run checklist.

## Thuật ngữ
**Read-only investigation query** (SELECT để tìm nguyên nhân 1 ticket; không PC nhưng ghi lý do/COEC lên ticket); **Mandatory line** (dòng đầu mọi ImpEx/Groovy chứa số PC duyệt và COEC gốc; thiếu là strike); **Catalog version macro** (`$catalogVersion` trỏ Staged hay Online; default sai ghi thẳng Online hoặc không đổi gì); **Rollback file** (ImpEx đảo ngược từ BEFORE export, thử trên staging trước khi gửi PC; chạy production cũng cần PC); **DRY_RUN flag** (Groovy mặc định `true`, lần chạy đầu chỉ in; PC ghi "dry run, then execute"); **Commit mode** (cài đặt HAC Groovy console để ghi thật; không có thì không đổi gì, KE-TEC-MON-02-04); **Script library entry** (IMP-TEC, GRV-TEC, QRY-TEC; chỉ Tech Lead duyệt version mới/đánh dấu repeat-use); **Repeat-use** (Tech Lead đánh dấu dùng nhiều lần không đổi nội dung; chỉ bỏ kết quả staging, không bỏ PC, mandatory line hay second check); **Strike** (vi phạm RHQ ghi theo người; 3 trong 1 năm = loại vĩnh viễn khỏi team).

## Nội dung
### 1. Query read-only an toàn
Bốn luật: ghi lý do (COEC) lên ticket trước khi query; chỉ lấy cột cần; kết quả ở lại công cụ Samsung, không export về máy; không query production "chỉ để xem". Thói quen: join enum qua type (OrderStatus, ConsignmentStatus, ProcessState) và đọc `{x.code}` không PK; trên Order thêm `{o.originalVersion} IS NULL` (nếu không có thể đọc bản snapshot); lọc theo list code hoặc store + khoảng ngày, ngày cao điểm chia theo store/ngày và tránh ProcessTaskLog (KE-TEC-MON-01-07: query ProcessTaskLog bị abort 3 lần trên el3-s2); đổi giờ sang giờ market trước khi đánh giá tuổi (KE-TEC-MON-01-04). Log nằm ở Kibana ~3 tuần; cũ hơn cần ticket L2 label `COEC_logs_extract`.
| Câu hỏi | Pattern (pack, verified el3-s2 24/10/2026) |
|---|---|
| Order store `vn` kẹt status trung gian? | MON01-Q1: Order join OrderStatus + BaseStore, status IN (...), modifiedtime cũ hơn cut time |
| Order đã tới NERP chưa? | Consignment `{gerpSalesOrderNr}` (MON01-Q3); `{externalSalesOrderNr}` rỗng trên el3 |
| Refund được chấp nhận chưa? | PaymentTransactionEntry join PaymentTransactionType, lọc order code: type, transactionStatus, amount |
| NERP export job khoẻ? | MON01-Q4: CronJob join CronJobStatus + CronJobResult cho `<cc>-tokoTransferConsignmentToWarehouseJob` và FI jobs |
| Status SKU theo catalog version? | TokoVariantProduct join CatalogVersion, Catalog, enum salesStatus/approvalStatus, `{p.code} IN (...)` (TRN-038 Q1) |
Groovy read-only có thể chạy rollback mode, nhưng mọi Groovy trên production tính là chạy Groovy; dry run trên production cũng cần PC duyệt.
> Quyền xem HAC production của Level 1 còn là câu hỏi KT mở. Đến khi RHQ cấp, L1 điều tra production bằng màn Backoffice trong quyền được cấp và tập HAC trên staging.

### 2. ImpEx có header và rollback
ImpEx cho thay đổi dữ liệu hàng loạt kiểu UPDATE/INSERT đơn giản. Mười luật script: một mục đích, tham số ở đầu, scope là danh sách code cụ thể khớp PC từng dòng, không password/dữ liệu cá nhân thật trong library, không sửa sau khi PC duyệt.
**Ví dụ TRN-038 (MY):** subsidiary xin archive 312 SKU hết vòng đời trên 3 catalog (936 dòng). Merch PIC tạo **COEC liên kết**, đặt ticket Merch ON HOLD COE (SLA vẫn chạy); Tech dùng ImpEx theo TEC-TSP-03 (bulk data fix: Level 2, PC có, second eyes + Tech Lead review bắt buộc). Lab tập với 3 SKU pool trên 2 catalog Staged, scope = 6.
```
#NOTE ITGC_JIRA:PC-TBC (SCOE-44)
# Library: IMP-TRN-038 v0.1 | Purpose: archive 3 SKU pool (staging rehearsal)
$catalogSme = mysmeProductCatalog
$cvSme = catalogversion(catalog(id[default = $catalogSme]), version[default = 'Staged'])[unique = true, default = $catalogSme:Staged]
UPDATE TokoVariantProduct; code[unique = true]; $cvSme; salesStatus(code); approvalStatus(code)
; QA65Q60RAKXXM  ; ; ARCHIVED ; check
```
Checker đọc từng dòng: macro default là `Staged` (default `Online` ghi vào catalog live); enum viết thường `check`, không `CHECK`; archive = salesStatus ARCHIVED + approvalStatus check (hoặc unapproved) ở child catalog, rồi sync **chỉ các SKU này** lên Online (sync cả catalog đẩy thay đổi của người khác); rollback dùng BEFORE của từng catalog (BEFORE ở `myb2bProductCatalog` có thể khác, VD PDP_NOT_AVAILABLE thay vì PURCHASABLE); "0 errors" không nghĩa là đúng: chạy lại query AFTER (Q3) và so sánh. Ví dụ TC-05: `groups(uid)[mode=replace]` thay vì `mode=remove` cho 0 lỗi nhưng xoá hết group khác của 5 account test. ImpEx chạy từng dòng và có thể dừng giữa chừng: lỗi thì dừng, ghi các dòng đã vào bằng query read-only, báo Tech Lead, hoàn tất hoặc rollback chỉ trong scope PC.
> Dòng bắt buộc cố định (A.II.2): `#NOTE ITGC_JIRA:PC-xxxxx (COEC-xxxxx)` dòng đầu ImpEx, `//NOTE ITGC_JIRA:PC-xxxxx (COEC-xxxxx)` dòng đầu Groovy. Ngoặc chứa ticket gốc: COEC trên production, ticket SCOE trong lab. Thiếu = vi phạm nghiêm trọng (CM-13 §9.3: strike). Định dạng cũ của TC-05 §2.4 và TC-01 §6.4 không còn dùng.
> Số PC chỉ có sau khi tạo PC. Test staging với `PC-TBC`, tạo PC lấy số, thay `TBC`, Checker xác nhận hai bản chỉ khác dòng đó. File chạy phải giống file đính kèm.

### 3. Groovy: khi nào được và review thế nào
Chỉ dùng Groovy khi ImpEx không làm được (VD restart order process từ action lỗi, hoặc kiểm logic từng record trước khi đổi). Update field đơn giản dùng ImpEx; TRN-038 nói rõ không dùng Groovy cho archive.
| Luật | Lý do |
|---|---|
| Groovy ghi có `DRY_RUN = true` mặc định; lần đầu chỉ in | Checker so list in ra với scope PC |
| Scope là list code ở đầu (`ALLOWED_ORDERS`), không bao giờ "mọi order ERROR" | PC duyệt list, không duyệt điều kiện |
| In record trong scope, record đã đổi, từng code; tóm tắt lên COEC | Bằng chứng post-check |
| Bỏ qua record đã xử lý/không khớp | Chạy lại an toàn (idempotent) |
| Production chỉ Tech Level 2 (Tech Lead, Sub-Lead, Team Member tuần Level 2) hoặc on-call chạy | TC-05 §2.7 |
| Giữa dry run và execute chỉ `DRY_RUN` được đổi | Sửa khác phải update và duyệt lại PC |
| Chạy commit mode khi ghi | Không thì không đổi gì (KE-TEC-MON-02-04) |
| Không dữ liệu Samsung vào công cụ AI; code AI hỗ trợ review từng dòng | TC-05 rule 8 |
**Ví dụ TRN-037:** `remediate_TRN037.groovy` bắt đầu `//NOTE ITGC_JIRA:PC-TBC (SCOE-43)`, `DRY_RUN = true`, `ALLOWED_ORDERS` chỉ order test của học viên, restart process đúng action lỗi trong task log (`processExternalServicesAction`). Checker trả NOT OK nếu có order BVT trong `ALLOWED_ORDERS`. Restart process không hoàn tác được nên PC ghi "IRREVERSIBLE".
KT 21/10: "Script mới phải chạy staging trước, kết quả đính PC. Script dùng nhiều lần có thể bỏ bước này. Mọi script phải có dòng PC + ticket gốc theo format Suwon. Chạy production không có = yêu cầu giải trình bằng email và strike."

### 4. Kiểm soát nội bộ trước PC
RHQ PC approver (hiện Oliver Leung) duyệt việc có được làm không, không test script của bạn. BiPlus có 3 lớp, luôn theo thứ tự, **trước** khi gửi PC:
| Lớp | Ai | Bắt buộc khi | Comment trên COEC |
|---|---|---|---|
| 1 Self-QA trên staging | Doer | Mọi thay đổi | "Self-QA" + ảnh staging: đúng job, đúng scope, chạy lại an toàn, rollback chạy được, không hỏng gì khác |
| 2 Another set of eyes | Tech khác có cert L2/L3 đúng service đó | ImpEx/Groovy mới; chạm giá, order, payment, permission; mọi PC từ người cert L1 | "Second check": đã kiểm gì, giờ |
| 3 Tech Lead review | Tech Lead (ngoài giờ: lớp 1 on-call) | Rủi ro cao: payment mode, base store, NERP, FI, access rule, External SSO, bulk data fix, remediate order bằng script; mọi fix P0, P1 | "Tech Lead review": cách làm, rollback đã test, cửa sổ chạy, ai được báo |
Checker đọc mọi dòng (header, INSERT/UPDATE/REMOVE, `mode=append|remove|replace`, giá trị, format ngày/múi giờ), so scope với chẩn đoán và PC nháp, mandatory line, kết quả staging, rollback, lịch freeze. Không có Checker certified thì không gửi PC. TRN-038 áp cả 3 lớp (bulk data fix) và rollback phải thử staging (Q4 = BEFORE) trước PC.
> CM-13 §9.3 cần second checker cho script mới hoặc thay đổi giá/order/payment/permission, các trường hợp khác cho phép hỏi thêm khi chưa chắc. TC-05 đọc chặt hơn: ImpEx repeat-use chạm order vẫn cần another set of eyes. Theo TC-05; không mâu thuẫn CM-13.

### 5. PC ticket: scope, bằng chứng, approver, chạy
| Bước | Doer làm | Checker kiểm |
|---|---|---|
| 1-4 | Chẩn đoán read-only; phân loại; chuẩn bị script + rollback; staging + self-QA | Kết quả staging là của cùng file |
| 5 | Comment kiểm soát nội bộ trên COEC | Có comment second check và Tech Lead kèm giờ |
| 6 | Tạo PC: summary `[PC] [Market] [Short change] (COEC [number])`, issue link, scope là list code, ảnh before, kết quả staging, file có mandatory line, rollback hoặc "irreversible", cửa sổ chạy theo ICT và SGT, người chạy, post-check | Không dữ liệu cá nhân trong description; số trong file khớp |
| 7 | COEC sang ON HOLD HQ "PC ticket pending: [number]"; chỉ P0/P1 mới liên hệ đầu mối duyệt chỉ định (tên trong on-call sheet của Tech Lead) | Clock chỉ dừng sau khi PC thật sự gửi |
| 8 | RHQ PC approver duyệt. Kiểm ticket gốc về IN PROGRESS (RHQ thường chuyển); không thì tự chuyển và comment key PC | Duyệt đọc được trên PC |
| 9-10 | Pre-run checklist; chạy (pilot trước nếu bulk); post-check số lượng; comment cả hai ticket; LAUNCH VERIFICATION | Record đã đổi = record trong scope |
Dự kiến ~3 giờ chờ duyệt. Ticket Merch liên kết ở ON HOLD COE vẫn đếm SLA: báo Merch PIC khi PC gửi và duyệt. **Ba hành động luôn bị strike:** chạy ImpEx/Groovy production không mandatory line; đổi production không PC duyệt; làm service chưa cert gây incident. Chạy ngoài scope PC (thêm record, đổi file sau duyệt) coi như không PC. Nếu xảy ra: báo Tech Lead trong ca, không sửa log hay chạy lại để che.
Không phải script KB nào cũng an toàn: SDSAP gọi KB script [VN] Modify Promotion Action là "not recommended" (ImpEx trên rule action rồi Groovy republish rule; handover All Scripting 28/10). Đổi action trên promotion đã publish cần Knox duyệt lại trước publish tiếp theo nơi có Knox, mà Groovy republish có thể bỏ qua bước đó. Nếu ticket xin: PC duyệt, Knox re-approval trước mọi republish, Tech Lead review.
> RHQ chưa đưa template PC chính thức, field Jira bắt buộc của project PC, hay luật gộp nhiều COEC vào 1 PC. Dùng template TC-05 §3.4, một PC mỗi COEC (một PC có thể nhiều record cùng một thay đổi). PC gốc có duyệt luôn rollback không còn mở: ghi rollback vào PC gốc và xin duyệt cả hai.

## Quiz (đáp án)
1 Query read-only production để biết vì sao 1 order MY kẹt → **C: lý do (COEC) ghi trên ticket, chỉ cột cần** (B PUMI dành cho report/dữ liệu lịch sử). 2 ImpEx archive báo "0 errors" trên staging, bước tiếp → **B: chạy lại BEFORE query như AFTER và so từng dòng**. 3 `UPDATE Customer;uid[unique=true];groups(uid)[mode=replace]` để bỏ 1 group khỏi 120 account → **B: sai mode, replace xoá hết group khác; dùng `mode=remove` và chạy lại staging**. 4 Test staging với `PC-TBC`, giờ có PC-1234; file đính kèm được khác gì → **A: chỉ mandatory line**. 5 Groovy restart process chạy production dưới PC duyệt nhưng không đổi gì → **B: chạy không commit mode; chạy lại commit mode dưới cùng PC**. 6 Ticket Merch ở ON HOLD COE khi PC pending → **B: clock COEC dừng ở ON HOLD HQ, SLA Merch vẫn chạy; báo PIC khi PC gửi và duyệt**. 7 Sau run thấy ImpEx production không có mandatory line → **C: báo Tech Lead trong ca; không sửa log, không chạy lại; Tech Lead báo RHQ**. 8 Thay đổi nào bỏ được kết quả staging → **B: ImpEx library Tech Lead đánh dấu repeat-use, dùng lại với tham số mới** (A script mới nhận từ KT vẫn là "mới"; D remediate order P1 là rủi ro cao).

## Practice
**PR-TEC-P2.1-1. Bulk archive bằng ImpEx có rollback và PC (TRN-038)** (55'; el3-s2 HAC; 3 SKU pool trên 2 catalog Staged; `myEstoreProductCatalog:Online` chỉ đọc; trainer/Tech Lead duyệt trước import và đóng PC approver). Chạy Q0 (catalog version tồn tại), Q1 BEFORE, Q2 (scope count), điền cột BEFORE của `scope-list.csv`. Hoàn tất `archive_TRN038.impex` (dòng đầu `#NOTE ITGC_JIRA:PC-TBC (SCOE-44)`, macro Staged, 6 dòng) và `rollback_TRN038.impex` từ BEFORE. Viết comment self-QA, nhận second check và Tech Lead review. Sau duyệt: import, Q3 AFTER, chạy rollback, Q4. Điền `pc-ticket-draft.md` (scope 936 dòng production, kết quả staging, rollback đã thử, cửa sổ chạy ICT và SGT, người chạy, post-check với pilot 1 SKU và sync chỉ SKU), thay `TBC` bằng số PC, đưa COEC sang ON HOLD HQ "PC ticket pending". **Pass:** Q2 = 6 (hoặc ít hơn kèm ghi "out of scope (not in catalog)"); approvalStatus viết thường `check`; không dòng Online hay `myEstoreProductCatalog` đổi modifiedtime; Q3 ARCHIVED/check trên 6 dòng Staged; Q4 = BEFORE (no-op chấp nhận nếu BEFORE đã ARCHIVED/check, rollback rỗng); rollback dùng giá trị export theo catalog; có 3 comment kiểm soát trước PC; PC nháp đủ field template TC-05 và file đính kèm chỉ khác file đã test ở mandatory line; mandatory line khớp format từng ký tự (thiếu/khác là fail). Không có access: trainer chạy import; bạn viết file, comment và PC nháp từ output Q1 in sẵn.
**PR-TEC-P2.1-2. Năm query điều tra** (15'; el3-s2 HAC read-only hoặc giấy). Viết và chạy: (1) order kẹt theo status store `vn`; (2) consignment của `ID261022-26950388` có `gerpSalesOrderNr` không; (3) payment entry (type, transactionStatus, amount) của `SG261022-26972065`; (4) cờ active, status, result, end time của 4 cronjob NERP `vn-`; (5) salesStatus và approvalStatus theo catalog version của 3 SKU pool TRN-038. Viết lý do 1 dòng cho mỗi query. **Pass:** mỗi query dùng enum join và trả code, lọc theo list code hoặc store + ngày, thêm `{o.originalVersion} IS NULL` trên Order, không chọn cột khách hàng; kết quả mong đợi (lab 24-25/10): (2) SO 1355797013; (3) AUTHORIZATION, CAPTURE, REFUND_FOLLOW_ON ACCEPTED cùng số tiền; (4) 4 job active, FINISHED, SUCCESS.
