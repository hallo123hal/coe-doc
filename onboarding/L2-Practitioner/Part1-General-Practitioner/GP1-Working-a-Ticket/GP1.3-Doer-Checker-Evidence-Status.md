# GP1.3 Doer, Checker, evidence and the right status

> Nguồn: page 2484175202 · 60 phút (Study 15' · Demo/thảo luận 10' · Quiz 5' · Practice 30') · Thực hành theo case trên staging và practice ticket; facilitator: Shift Leader hoặc Sub-Lead · Capabilities C1, C4 · Cần xong G2.6, MER-3.1 (internal check, desk check, RC code), QA-2.4; mang checklist Checker MER-PRD-01 (§4.1) và bảng kết quả trống (SKU, catalog, action, before, after, result). Truy cập: staging Backoffice SMS el3-s2 (đọc + pool SKU được giao), Jira SCOE, Confluence; không dùng HAC; evidence chỉ làm trên CoE workstation. Không có staging: dùng ảnh trong runbook MER-PRD-01 và file before/after in sẵn, kiểm trên giấy.

## Mục tiêu
Chọn risk tier, Checker, Approver từ bảng CM-07 và nói lý do; lấy before export, đổi, lấy after export và so từng dòng sao cho before export dùng làm rollback; viết internal check line và dựng evidence pack theo CM-13; chuyển ticket Shop Merch qua STG SETUP, QA REVIEW, PRD SETUP, REVIEW SETUP đúng lúc và biết ai chuyển.

## Thuật ngữ
**First matching row** (đọc bảng tier CM-07 từ trên xuống, dừng ở dòng đầu khớp; "product setup, stock" dừng ở dòng 6, R2); **Highest tier wins** (TRN-007 có hide (R1/R2) và stock (R2) nên R2); **Before export** (export giá trị theo catalog trước khi đổi — cũng là file rollback); **After export**; **Internal check line** (comment Doer viết trước khi build: SKU, catalog, action, go-live kèm time zone, kết thúc "Matches approved brief"); **Line result** (mỗi action line kết thúc với đúng một kết quả: done, routed, blocked); **Sampling service** (service không có QA gate bắt buộc; cứ ticket thứ 5 mỗi cluster = 20%, tối thiểu 3/tuần vào QA REVIEW); **Another set of eyes** (trên COEC: second checker có Academy L2/L3 đúng service đó; bắt buộc với script mới hoặc thay đổi chạm giá, order, payment, access).

## Nội dung
### 1. Risk tier quyết định ai kiểm, ai duyệt
Tier đặt lúc intake: Team Member trực intake đề xuất, Shift Leader xác nhận. Đọc từ trên xuống, dừng ở dòng khớp đầu tiên. Không bao giờ hạ tier để nhanh.
| Dòng | Điều kiện | Tier | Checker | Approver |
|---|---|---|---|---|
| 4 | R3 chạm E4 (≥10,000 USD, >5 market, price file ≥500 SKU) | R3 + E4 | QA 100% | Shift Leader + Merch Lead/Deputy; Knox |
| 5 | Giá, special price, discount, promotion, coupon, trade-in; payment trên ticket Shop Merch | R3 | QA 100% sau price sanity + internal check | Shift Leader; Knox |
| 6 | Product setup, delivery mode, stock, pre-order, multistore, product reference | R2 | QA nếu service có gate, không thì sampling | Shift Leader |
| 7 | Text, flag, benefits text, banner/CMS không T&C, nội dung Shop App, hide/show | R1 | Shift Leader | Shift Leader |
| 3 | Change Tech: data, cấu hình Back Office, ImpEx, Groovy | Tech | Self-QA trên staging; another set of eyes khi bắt buộc | PC ticket: RHQ PC approver chỉ định |
Doer không bao giờ duyệt việc của chính mình. Với Merch R2 có QA gate và R3, Doer/Checker/Approver là ba người khác nhau. Trong MER-PRD-01 Checker là operator certified thứ hai, QA Team nhận flagship và mẫu tuần, Shift Leader duyệt.
**Ví dụ TRN-007:** item 1, 3, 4 là MER-PRD-01 (hide, unhide, đổi CTA); item 2 là MER-STK-01 (unblock stock). Stock ở dòng 6 nên cả ticket là R2: Doer là Market Owner VN hoặc TM; Checker là operator certified thứ hai (QA theo mẫu); Approver là Shift Leader; không cần Knox (không giá, không promotion).
> CM-07 xếp "hide or show" vào R1 còn pack MER-PRD-01 và review TRN-007 (sửa từ R1 lên R2) coi hide/unhide là R2; CM-13 không chốt. Áp "highest tier wins" và "never downgrade": coi hide/unhide của MER-PRD-01 là R2 tới khi Merch Lead hoàn thiện catalogue.

### 2. Before/after: export là bằng chứng và là rollback
Làm việc trong bản **Staged** của từng child catalog rồi sync sang Online. Status Jira STG SETUP không có nghĩa là môi trường staging: Merch setup trên Backoffice production. Trong lab dùng staging el3-s2 chỉ như bản copy luyện tập.
**Runbook MER-PRD-01 (V2 activate, V3 hide) tóm tắt:**
| Bước | Doer làm | Checker kiểm |
|---|---|---|
| 1 | Tách ticket thành line (SKU, catalog, action), xác nhận nghĩa từng từ ("hide" = approval check + ARCHIVED) | Mọi line yêu cầu xuất hiện đúng một lần trong bảng kết quả |
| 2 | Chỉ V3: kiểm dependency (F-code, gift/add-on reference, promotion, lọc theo promotion group của site) | Dependency đã báo requester trước khi làm |
| 3 | Export before: Catalog › Products › search › Export (approval và sales status mỗi catalog version) | File before đã đính, mỗi catalog một file |
| 4 | Đặt giá trị trong từng child Staged catalog được yêu cầu | After export khớp yêu cầu từng dòng; số dòng bằng nhau; không đổi gì ngoài yêu cầu |
| 5 | Sync Staged → Online; chờ indexing và cache | Online export bằng Staged export |
| 6 | Test một site mỗi loại catalog: PDP và add to cart (archived trả "Sorry, there is no stock for this product.") | Mẫu storefront mỗi loại catalog |
**Rollback:** before export chính là rollback. Đổi ở Staged chưa sync: re-import before export. Đã live có lỗi, phát hiện trước Checker: re-import ngay và báo requester. SKU sai đang live và bán: đặt approval về check; MER-INC-01 nếu thiệt hại >10,000 USD.
**Ví dụ TRN-007 item 4:** before — HW-S800B/XV ở `vnEstoreProductCatalog` là PURCHASABLE và approved (pool, 24/10/2026). Yêu cầu "hiện Mua ở đâu chỉ D2C". After: unapproved, vẫn PURCHASABLE, chỉ ở `vnEstoreProductCatalog`; EPP không đổi. Lỗi hay gặp là ARCHIVED, làm mất CTA (QA FAIL, `RC-ENT`).
> Runbook MER-PRD-01 sync lên Online (V2 bước 4) trước after export cho Checker, còn QA-03 QCL-PRD-01 mục 6 nói "sync only after approval", và TRN-007 cũng sync sau khi Shift Leader duyệt. Theo thứ tự chặt hơn (kiểm, duyệt, rồi sync) tới khi Merch Lead đồng bộ pack (open point).

### 3. Internal check line và evidence pack
Trước khi build Doer viết internal check line lên ticket. Việc product status: SKU, catalog, action, go-live kèm time zone; R3: sáu giá trị CM-13 (SKU, giá/discount, thời gian + time zone, site/store, stacking, usage limit). Kết thúc "Matches approved brief". Không internal check line thì không build R3. Chỉ hỏi subsidiary khi brief thiếu hoặc tự mâu thuẫn.
```
Internal check: hide QA50LS03BAKXXV, QA50LS03DAKXXV, QA65LS03FAKXXV
(approval check + ARCHIVED) on D2C, EPP, SME catalogs, 3PD excluded per requester;
HW-S800B/XV unapproved + PURCHASABLE on vnEstoreProductCatalog only.
Go-live: on sync, D0 [hh:mm] ICT. Matches approved brief.
```
Self-check trước khi giao Checker: mỗi line một kết quả; after export khớp từng dòng theo catalog; không đổi thêm gì; internal check line đã có.
**Luật evidence (CM-13):** PowerPoint ảnh chụp từng bước, đính vào Jira comment cho subsidiary xem ở REVIEW SETUP; chỉ làm ảnh và PowerPoint trên CoE workstation trong khu secure, đính Jira rồi xóa bản local; không ảnh điện thoại, không kênh khác, không video trên Jira (RHQ nêu giới hạn 15 MB/ticket); export đính cùng comment dưới dạng file.

### 4. Chuyển status: khi nào, ai chuyển
| Chuyển | Khi nào | Ai |
|---|---|---|
| APPROVED-ES → STG SETUP | Nhận ticket, trong 2h (nội bộ 78', High 15') | Người trực intake |
| STG SETUP → QA REVIEW | Sau self-check, nếu service có QA gate hoặc ticket nằm trong mẫu | Doer |
| QA REVIEW → STG SETUP | QA FAIL (một lần trả liệt kê mọi lỗi) hoặc thiếu data (`RC-EVD`) | QA |
| QA REVIEW hoặc STG SETUP → PRD SETUP | Sau comment của Checker và export; cả hai đường đều được | Shift Leader duyệt |
| PRD SETUP → REVIEW SETUP | Đã sync, đã đính evidence; clock dừng | Doer (owner) |
| REVIEW SETUP → PENDING LAUNCH / LAUNCH VERIFICATION | Subsidiary duyệt; go-live tương lai chờ ở PENDING LAUNCH | Subsidiary, CoE |
Với service **sampling**, mẫu được chọn trước khi Doer xin duyệt: dispatcher gắn label cho mỗi ticket thứ 5 mỗi cluster và comment "Selected for QA sample. Please move to QA REVIEW after self-check." Ticket không được chọn đi STG SETUP → PRD SETUP sau khi Shift Leader duyệt. 5 ticket đầu của Doer mới certified luôn bị lấy mẫu.
**COEC** khác: ASSIGNED → IN REVIEW → IN PROGRESS → QA REVIEW (self-QA staging) → WAITING QA (another set of eyes) → ON HOLD HQ (PC) → IN PROGRESS → LAUNCH VERIFICATION, giao người tạo.
> **Under review (D7):** workflow COEC 2026 ở handover không có WAITING QA và dùng ON HOLD RHQ thay ON HOLD HQ. Dùng nhãn Jira hiển thị.
Handover Samsung (23/10/2026): *"QA attaches evidence and moves the ticket to Review Setup. The reporter reviews the evidence and may request more scenarios. The reporter must comment a green light on the ticket before CoE publishes the promotion and submits approval."*
> Slide 11 handover xếp "product activation" và "warehouse and stock setup" là "No QA review (Merch self-checks and attaches evidence)" trong khi QA-03 và MER-PRD-01 đặt SKU setup ở sampling (20%, tối thiểu 3/tuần). Slide chỉ là tham khảo "có thể đổi"; theo QA-03 sampling. CM-13 §3.6 cũng nói không có duyệt trước 23:59 hôm trước go-live thì CoE vẫn publish đúng giờ, nên luật "green light" chỉ áp dụng tới mốc đó.
> **Under review (D5, D9):** runbook sửa đổi dùng thứ tự khác cho promotion (QA REVIEW, rồi subsidiary green light ở REVIEW SETUP, rồi PRD SETUP và submit Knox) và cho giá (Knox trước, rồi sync, front-end QA, REVIEW SETUP). MER-PRD-01 nay cho status-only line (V2, V3, V4) tự kiểm kèm evidence còn V1 upload và V6 đổi attribute vào QA REVIEW. Bảng trên giữ nguyên tới khi D5, D9 chốt.

## Quiz (đáp án)
1 Ticket VN: update text/flag 15 SKU + set virtual stock 2 SKU → tier **B: R2, tier cao nhất trong ticket (stock)** (một tier mỗi ticket, không phải mỗi line). 2 Bạn là Shift Leader nhưng phải tự build R2 vì ca thiếu người, ai duyệt → **C: người khác có thẩm quyền duyệt (deputy Shift Leader certified hoặc Lead); chưa có thì chưa lên production**. 3 Đã đổi 9 line ở Staged, chưa sync, Checker thấy một SKU ARCHIVED thay vì unapproved → rollback **A: re-import before export cho line đó rồi làm lại đúng**. 4 Internal check line đúng cho TRN-007 item 4 → **C: "HW-S800B/XV unapproved + PURCHASABLE on vnEstoreProductCatalog only; EPP unchanged. Go-live on sync, D0 14:10 ICT. Matches approved brief."** 5 Ticket MER-PRD-01 không nằm trong mẫu QA, Checker đã comment và đính after export → **B: PRD SETUP, sau khi Shift Leader duyệt**. 6 QA mở ticket QA REVIEW thấy không có before export và internal check line → **B: trả STG SETUP `RC-EVD` và đến bàn Doer lấy data thiếu** (data thiếu ở phía CoE, không phải subsidiary). 7 Làm ảnh evidence ở đâu → **B: trên CoE workstation trong khu secure; đính Jira rồi xóa bản local**.

## Practice
**PR-GP1.3-1. Làm và kiểm một ticket lab** (30', theo cặp; staging SMS el3-s2 + Jira SCOE TRN-007): bạn A là Doer cho item 1, bạn B cho item 4; sau đó đổi vai và kiểm chéo. Chỉ đổi pool SKU trainer giao; không HAC; không cronjob, Initialization hay Update. Trainer trả lời câu hỏi 3PD: "all sites" không gồm marketplace. Việc Doer: viết internal check line, export before theo catalog, đổi trong Staged, export after, self-check, giao partner. Việc Checker: so before/after từng dòng bằng checklist MER-PRD-01 (mục 1–4, 9, 13), viết comment kết quả (PASS hoặc FAIL kèm RC); sau đó rollback từ before export và export status theo catalog version lần nữa. **Pass:** item 1 — QA50LS03BAKXXV, QA50LS03DAKXXV, QA65LS03FAKXXV là approval check + ARCHIVED ở mọi catalog trong scope (D2C, EPP, SME) và không đổi ở 3PD; item 4 — HW-S800B/XV unapproved + PURCHASABLE chỉ ở `vnEstoreProductCatalog`, EPP không đổi; mỗi action line một kết quả; số dòng before/after bằng nhau; internal check line có trên ticket; có comment Checker; chuỗi status luyện tập STG SETUP → QA REVIEW → PRD SETUP → REVIEW SETUP (chưa chấm tới khi D5, D9 chốt); sau rollback 4 SKU về PURCHASABLE và approved như before export. Không có access: dùng ảnh runbook và export in sẵn, kiểm trên giấy rồi viết comment Checker.
