# TEC-2.2 HAC, FlexibleSearch, ImpEx, Groovy

> Nguồn: page 2482897558 · 120 phút (Study 30' · Demo 15' · Quiz 10' · Practice 65') · Facilitator giải thích từng khái niệm trên HAC staging rồi lab cá nhân có coach; facilitator: Tech Sub-Lead có L2 · Cần xong G5.2, G3.3, TEC-2.1. Cần Backoffice staging + HAC staging đúng cluster (SMS cho VN, TH, ID, MY, SG, PH, NZ; SMA chỉ AU; mọi lab chạy SMS staging, URL do facilitator đưa). Facilitator tạo (hoặc cho learner tạo) delivery mode `TRAINING_<name>_dm` trên Backoffice staging, chọn 1 SKU và 1 site. Không mượn account người khác.

## Mục tiêu
Giải thích type, item, attribute và vì sao 1 SKU trả nhiều dòng khi không lọc catalog version; viết FlexibleSearch có JOIN + lọc catalog version/`originalVersion` cho 4 câu hỏi nghiệp vụ; phân biệt INSERT / UPDATE / INSERT_UPDATE / REMOVE; chạy ImpEx trên staging với ITGC header và ImpEx rollback tương ứng; viết Groovy với `DRY_RUN = true`, chạy ở rollback mode và in số record trong scope.

## Thuật ngữ
**Type system** (mỗi type như một class Java gắn bảng dữ liệu: `Order`, `TokoVariantProduct`); **Item / attribute** (item = một record có pk; attribute = một field); **Enumeration type** (type có danh sách giá trị cố định, VD `OrderStatus`); **ImpEx header line** (dòng lệnh của một block: mode, type, cột — khác "ITGC header line" ở đầu file); **Modifier** (phần trong `[ ]` sau tên cột: `[unique=true]`, `[mode=append]`); **ITGC header line** (dòng 1 bắt buộc của mọi ImpEx/Groovy chạy production: `#NOTE ITGC_JIRA:PC-1234(COEC-5678)`); **PC-TBC** (số PC tạm dùng trên staging); **Scripting console** (menu HAC chạy Groovy trực tiếp; có Commit mode và Rollback mode); **DRY_RUN**; **Script library** (`IMP-TEC-xx`, `GRV-TEC-xx`, `QRY-TEC-xx`); **Spring bean** (service có sẵn: `flexibleSearchService`, `modelService`).

## Nội dung
### 1. HAC và type system
Menu HAC cho Tech: Console › FlexibleSearch, ImpEx Import, Scripting Languages, Platform › Configuration; không bao giờ bấm Platform › Initialization/Update. Trước khi gõ gì kiểm URL phải chứa `samsungel3-s2`, không thì đóng tab.
Hybris không cho làm việc trực tiếp với bảng DB mà qua **type**: `Order` là type, mỗi order là một item có pk; attribute có 2 loại — giá trị (`code`, `date`) và tham chiếu tới item khác (chỉ lưu pk) nên `{o.status}` trả số, phải JOIN `OrderStatus` mới đọc được "ORDER_SPLIT". Type kế thừa: `{Product}` gồm cả subtype, `{Product!}` chỉ đúng type Product. Quên tên attribute: Backoffice › System › Types › gõ tên › Search by type, mở type xem attribute (VD màn hình ghi "Available amount" nhưng attribute là `available`).

### 2. Catalog version và FlexibleSearch
Sản phẩm thuộc một catalog version (cặp catalog + version, G3.3); cùng SKU nằm ở Master Staged, child Staged, child Online → query không lọc ra 3 dòng. Luôn JOIN `CatalogVersion`, `Catalog` và lọc (VD `{c.id} = 'phEstoreProductCatalog' AND {cv.version} = 'Online'`). Order không có catalog version nhưng có bản cũ → `{o.originalVersion} IS NULL`.

| Điểm | FlexibleSearch | SQL thường |
|---|---|---|
| Bảng | Tên type trong ngoặc nhọn `{Order AS o}` | Tên bảng thật |
| Cột | Tên attribute `{o.code}` | Tên cột thật (có thể khác attribute) |
| Tham chiếu | Lưu pk, JOIN theo pk `{os.pk} = {o.status}` | Foreign key |
| Field đa ngôn ngữ | `{p.name[en]}` | Bảng riêng |
| Subtype | `{Product}` gồm subtype, `{Product!}` chỉ type đó | Không có khái niệm này |
| Subquery | trong `{{ ... }}` | trong `( ... )` |
| Tham số | `?catalogName` | tùy tool |

Hybris dịch FlexibleSearch sang SQL của DB thật (tab SQL trong HAC cho thấy). Query chỉ đọc trên production không cần PC nhưng phải ghi lý do và chỉ chọn cột cần (TEC-2.1).

### 3. ImpEx: header, cột unique, bốn mode
ImpEx là file text nạp/đổi data hàng loạt; mỗi block có một header line và các dòng data bắt đầu bằng `;`. VD tạo phí giao cho delivery mode training:
```impex
$currency = NZD
INSERT_UPDATE ZoneDeliveryModeValue;deliveryMode(code)[unique=true];zone(code)[unique=true];currency(isocode)[unique=true];minimum[unique=true];value
;TRAINING_an_dm;nz-north;$currency;0;49
```
Các cột `[unique=true]` cùng nhau xác định "dòng nào"; `deliveryMode(code)` nghĩa là tìm delivery mode theo code, không cần pk. Bốn mode: **INSERT** tạo mới (đã tồn tại cùng unique → lỗi); **UPDATE** chỉ sửa dòng có sẵn, dòng chưa có không được tạo (bài F4); **INSERT_UPDATE** có thì sửa, chưa có thì tạo — dùng cho đa số việc; **REMOVE** xóa item khớp unique — thường làm rollback cho dòng vừa tạo. Cột dạng list (VD user group của account): `groups(uid)[mode=append]` thêm, `[mode=remove]` bớt, không mode thì **thay cả list** — nguyên nhân lỗi "0 errors nhưng mất hết group" ở TEC-2.1.

### 4. ITGC header line và quy trình TBC
ImpEx dùng `#NOTE ITGC_JIRA:PC-xxxx(COEC-yyyy)`, Groovy dùng `//NOTE ITGC_JIRA:PC-xxxx(COEC-yyyy)`, luôn ở dòng 1. Thiếu hoặc số PC không khớp PC đã duyệt là strike cho người chạy (CM-13 §9.3); kiểm dòng 1 với PC trước mỗi lần chạy. **Quy trình TBC:** (1) chạy staging với `PC-TBC`; (2) tạo PC lấy số; (3) thay TBC bằng số thật; (4) checker so hai bản — chỉ dòng này được khác; (5) đính bản cuối vào PC; file chạy production phải y hệt file đính kèm.

### 5. Groovy trong Scripting console
Script chạy trực tiếp trên hệ thống và gọi được service có sẵn: `flexibleSearchService` (query trong script); `modelService` (`save`/`remove` item); `businessProcessService.restartProcess(process, "cancelOrder")` (restart process từ đúng bước — VD KB Script to cancel order). **Console mặc định ở rollback mode: chạy xong mọi thay đổi bị hoàn tác;** chỉ commit mode mới lưu thật. Script có ghi data phải bắt đầu bằng `def DRY_RUN = true` — lần chạy đầu chỉ in "sẽ đổi gì". Trên production, dry run cũng là một lần chạy Groovy nên PC phải ghi "dry run, then execute".

### 6. Luật script, repeat-use, ai được chạy gì
10 luật script (TC-05 §2.3) gom lại: file nằm trong script library kèm version, ngày, người sửa, số COEC; một script một mục đích, tham số ở đầu file; scope là danh sách code khớp PC; in số record trong scope và số record đã đổi; không password/token/PII trong file, không đưa script chứa data Samsung vào AI; không sửa file sau khi đã duyệt; query chỉ chọn cột cần.
**Repeat-use:** mọi file bắt đầu là "new" kể cả file nhận khi KT; chỉ Tech Lead đánh dấu repeat-use (đề xuất sau ≥3 lần chạy production thành công không đổi nội dung). Repeat-use **chỉ cho bỏ kết quả staging** — vẫn cần PC, header line, checklist trước khi chạy, và second check khi đụng price/order/payment/access.
**Ai chạy gì:** trên staging Tech tập thoải mái; trên production ImpEx/Groovy chỉ do **Tech Team Level 2** chạy, có PC duyệt và header đúng số; Level 1 không chạy, kể cả file repeat-use.

### Điểm đáng nhớ từ KT
Script mới phải chạy staging trước và đính kết quả vào PC; script dùng nhiều lần có thể bỏ — nhưng hiện chỉ Tech Lead mới được đánh dấu repeat-use và chỉ bỏ phần staging (CM-13 §9.2, TC-05 §1.6). Mọi ImpEx/Groovy phải mang dòng PC + ticket gốc; thiếu thì bị email giải trình và strike. Mọi PC đến Oliver, duyệt rồi mới chạy; Oliver là approver duy nhất, không backup, không duyệt sau kể cả khi incident (CM-13 §9.4–9.5). Thư viện 08 Impex/Scripting chưa đủ script và chưa có version control → mỗi script mới thêm vào Tech library kèm version, ngày, người sửa, số COEC; script nhận lúc KT bắt đầu là "new". Giữ nguyên cách làm hiện tại, cải tiến qua Tech Lead chứ không sửa thẳng script production.

## Quiz (đáp án)
1 Dòng đầu Groovy chạy production cho PC-12345 / COEC-5678 → `//NOTE ITGC_JIRA:PC-12345(COEC-5678)`. 2 Query một SKU ra 3 dòng cùng code → **SKU nằm ở nhiều catalog version**. 3 `UPDATE ZoneDeliveryModeValue` cho zone `nz-north` chưa có dòng → **không tạo dòng mới; cần INSERT_UPDATE**. 4 Chạy Groovy có `modelService.save(...)` mà không đổi mode → **script chạy nhưng thay đổi bị hoàn tác (rollback mặc định)**. 5 File ImpEx đã được Tech Lead đánh dấu repeat-use → **bỏ được kết quả staging**. 6 Thêm `th-storeagentgroup` cho 50 account mà không mất group cũ → `groups(uid)[mode=append]`. 7 ImpEx production hỏng ở dòng 40/100 → **dừng, ghi các dòng đã vào, báo Tech Lead trước**. 8 Checker so ImpEx chạy staging với bản đính PC → **chỉ khác ở dòng header (TBC thay bằng số PC)**.

## Practice
- **PR-TEC-2.2-1** (Backoffice + HAC staging, 12'): Backoffice › System › Types → `TokoVariantProduct` → Search by type, ghi parent type và 3 attribute (`approvalStatus`, `salesStatus`, `catalogVersion`); HAC chạy `SELECT {p.code}, {c.id}, {cv.version} FROM {TokoVariantProduct AS p JOIN CatalogVersion AS cv ON {cv.pk} = {p.catalogVersion} JOIN Catalog AS c ON {c.pk} = {cv.catalog}} WHERE {p.code} = '<SKU>'` → nhiều dòng (mỗi cặp catalog–version một dòng); thêm `AND {c.id} = '<B2C child catalog>' AND {cv.version} = 'Online'` chỉ còn 1 dòng; mở tab SQL ghi tên bảng thật của `TokoVariantProduct`. Pass: giải thích đúng vì sao nhiều dòng; query đã lọc trả đúng 1 dòng.
- **PR-TEC-2.2-2** (HAC, 15'): viết và chạy 4 query — (a) approval & sales status của SKU ở B2C child, Online (Query 1 textbook + filter lab 1); (b) 20 order SUSPENDED mới nhất của một site (JOIN `BaseSite AS s ON {s.pk} = {o.site}`, lọc `{s.uid}`, `{o.originalVersion} IS NULL`, `ORDER BY {o.date} DESC`, giới hạn 20 bằng ô max-rows); (c) cronjob có "stock" trong tên với result FAILURE/ERROR (sửa Query 5, thêm `{r.code} IN ('FAILURE','ERROR')`); (d) bài D7: order của một site ở SUSPENDED, CREATED >1h, hoặc WAIT_FRAUD_MANUAL_CHECK, chỉ bản hiện hành, chia 2 nhóm "có thể chạy lại sau duyệt" / "cần subsidiary xác nhận". Pass: ≥3/4 chạy; (a) lọc catalog version; (b) và (d) lọc `originalVersion`; 0 dòng trên staging vẫn ổn nếu query đúng.
- **PR-TEC-2.2-3** (20'): với `TRAINING_<name>_dm`, zone & currency facilitator đưa (VD `nz-north`, `NZD`), dòng 1 mọi file là `#NOTE ITGC_JIRA:PC-TBC(COEC-TRAIN-<name>)`: (a) INSERT_UPDATE tạo phí 49 → Backoffice thấy 1 dòng 49; (b) chạy lại cùng dòng bằng INSERT → lỗi vì đã tồn tại; (c) UPDATE đổi phí `nz-north` thành 59, rồi UPDATE thêm một zone chưa có dòng → `nz-north` thành 59, dòng zone mới không được tạo; (d) REMOVE đúng 4 cột unique → dòng phí biến mất, Backoffice về như trước (a). Ghi bảng 3 cột (lệnh / kỳ vọng / thực tế). Pass: cả 4 file có header ở dòng 1; có screenshot Backoffice trước/sau; giải thích đúng vì sao INSERT lỗi và UPDATE không tạo dòng; chỉ đụng delivery mode TRAINING của mình.
- **PR-TEC-2.2-4** (Scripting console, giữ rollback mode, 18'): (a) script chỉ đọc in code + status 5 order mới nhất của một site (FlexibleSearchQuery với `{o.originalVersion} IS NULL`, `{bs.uid} = 'vn'`, `ORDER BY {o.date} DESC`, `q.setCount(5)`), dòng 1 là `//NOTE ITGC_JIRA:PC-TBC(COEC-TRAIN-<name>)`; (b) khung script ghi data theo GRV-TEC-01: dòng 1 header, `def ORDER_CODES = [...]` lấy từ kết quả (a), `def DRY_RUN = true`, in "orders in scope: 2", mỗi order in "would re-push" hoặc "skip, already has NERP number", mọi lệnh ghi nằm trong `if (!DRY_RUN) { ... }` (để trống trong lab); (c) trả lời: script có lệnh save chạy ở rollback mode thì sao; production cần gì; khi nào được đổi `DRY_RUN` thành `false`. Pass: (a) chạy và không ghi gì; (b) in đúng số order và data không đổi; (c) nêu đủ — PC duyệt ghi "dry run, then execute", Tech Team Level 2 chạy, file giống bản đính kèm, header đúng số PC & COEC.
