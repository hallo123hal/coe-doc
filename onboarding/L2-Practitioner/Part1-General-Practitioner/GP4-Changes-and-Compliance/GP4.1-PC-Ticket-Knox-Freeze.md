# GP4.1 PC ticket, Knox approval and freeze

> Nguồn: page 2484502599 · 60 phút (Study 15' · Demo/thảo luận 10' · Quiz 5' · Practice 30') · Thực hành theo case; facilitator: Shift Leader hoặc Sub-Lead · Capabilities C1, C5 · Cần xong G2.6 (R1/R2/R3, E4, luật PC ticket, Knox) và G1.2 (luật RHQ, ba hành động luôn bị strike); đọc trước hai ticket luyện tập SCOE-44 (TRN-038: archive 312 SKU bằng ImpEx) và SCOE-35 (TRN-029: gia hạn PWP trong freeze). Chỉ cần Confluence (đọc CM-13, TC-05, CM-07); bài kiểm trên giấy. Không có access: facilitator in CM-13 ch.9–10, TC-05 §1.4, 3.4, 6.2 và text hai ticket.

## Mục tiêu
Chọn đúng approval route cho một change (Knox, PC ticket, PUMI, access approval ticket, RHQ approval email); kiểm change đủ compliance trước khi thực thi và liệt kê mọi approval/evidence còn thiếu; chuẩn bị PC ticket đầy đủ cho bulk change (summary line, scope dạng mã, before snapshot, kết quả staging, mandatory line, internal control, rollback, run window); quyết định khi nào promotion đã publish cần Knox lại và ghi gì trong lúc chờ; quyết định việc gì được phép trong freeze 48 giờ hoặc freeze flagship và cách xin exception.

## Thuật ngữ
**Approval route** (một cơ chế duyệt cho mỗi change: workflow Shop Merchandising + Knox cho giá và promotion; PC ticket cho change production của Tech; PUMI cho dữ liệu/report; approval ticket cho access; RHQ approval email cho EPP site); **Mandatory line** (dòng đầu mọi lần chạy ImpEx/Groovy trên production, kèm số PC ticket đã duyệt và số COEC gốc; thiếu thì người chạy bị strike); **Before snapshot** (ảnh/export dữ liệu trước khi đổi, đã che dữ liệu cá nhân; bắt buộc trong PC ticket); **Run window** (giờ chạy production dự kiến theo ICT và SGT, người chạy, post-check, VD "today 16:00 SGT by Tech Level 2, post-check after 30 min"); **Re-approval trigger** (đổi action, condition, website hoặc date của promotion đã publish → lần publish sau cần Knox lại; đổi tên thì không); **48-hour freeze** (trước 11.11, Black Friday, 12.12 chỉ change đã được RHQ duyệt; với Tech PC ticket phải ghi "During the 48-hour freeze for [event]"); **Exception approval** (duyệt bằng văn bản cho change trong freeze; CoE ghi vai trò approver, ngày, scope, link trang vào thân ticket trước khi làm); **Compliance page** (trang RHQ lưu duyệt exception freeze; subsidiary có thể không có quyền xem nên CoE tra evidence).

## Nội dung
### 1. Chọn approval route
Trước khi chạm vào gì, gọi tên route. Phần lớn lỗi compliance bắt đầu từ sai route (VD setup Merch gửi như PC ticket, hoặc ImpEx Tech làm "dưới Knox").
| Change | Route | Approver | Evidence giữ |
|---|---|---|---|
| Setup Merch giá, promotion, product, CMS | Workflow Shop Merchandising (cổng R1/R2/R3/E4) + Knox cho giá và promotion | Shift Leader (+ Merch Lead khi E4); Knox theo đường duyệt trong brief | Internal check, QA evidence, giờ và đường gửi Knox |
| Mọi change Tech trên production: data, cấu hình Back Office, ImpEx, Groovy, nút hành động order, chạy lại cronjob, rollback | PC ticket trong Jira project PC | RHQ PC approver (một approver chỉ định; P0/P1 gấp thì đầu mối duyệt chỉ định) | Kết quả staging, before snapshot, rollback, mandatory line |
| Report, dữ liệu lịch sử, report cronjob, người nhận | PUMI trước, rồi PC ticket | Subsidiary tạo PUMI; RHQ | PUMI đã duyệt đính Jira |
| Quyền truy cập và account | Approval ticket theo template RHQ, do Lead tạo | RHQ | Approval ticket |
| EPP site mới hoặc kích hoạt lại | Email duyệt của RHQ đính kèm; ticket sang ON HOLD RHQ (Merch) hoặc ON HOLD HQ (COEC) | RHQ | Email duyệt trên ticket |
Không cần PC ticket cho việc trên staging, xem/query chỉ đọc (kèm lý do trên ticket), hay yêu cầu sang team khác (ON HOLD ES) và SDS India (SYSTEM SUPPORT).
**Ví dụ TRN-038:** subsidiary MY xin archive 312 SKU MX trong ba catalog (936 dòng). Làm tay trên Backoffice không an toàn trong SLA, nên Merch PIC **không** chuyển ticket: tạo COEC liên kết và đặt ticket Merch ở ON HOLD COE (SLA vẫn chạy). Route: phần Merch là R2 (Shift Leader duyệt; không E4 vì 312 < ngưỡng 500 SKU và chỉ một market). Phần Tech là ImpEx trên production nên cần PC ticket. Archive không đổi giá hay promotion nên Knox không thuộc change này.
> RHQ xác nhận access xin qua ticket trong Jira project AUTEU, do Lead tạo cho thành viên, theo template RHQ (KT 21/10), gồm cả middleware 3PD và offboarding vào ngày làm việc cuối. Runbook dùng cùng route (TEC-MON-02 "access per AUTEU grant"; MER-SAC-01 "IP whitelist via AUTEU"). Không xin access qua kênh nào khác.

### 2. PC ticket đầy đủ cho bulk change
Luồng PC ticket có 10 bước. Clock tính khi việc còn ở phía CoE và chỉ dừng ở ON HOLD HQ.
| Bước | Ai | Việc | Status COEC |
|---|---|---|---|
| 1–2 | Người được giao | Chẩn đoán chỉ đọc; phân loại change | IN REVIEW, IN PROGRESS |
| 3–4 | Doer | Script/steps và file rollback; chạy trên staging; self-QA | IN PROGRESS, QA REVIEW |
| 5 | Checker; Tech Lead | Internal control, comment trên COEC | QA REVIEW (WAITING QA) |
| 6 | Doer | Tạo PC ticket, đặt số vào mandatory line, link COEC | IN PROGRESS |
| 7 | Doer | ON HOLD HQ, comment "PC ticket pending: [number]"; nhắn thẳng PC approver chỉ cho P0, P1 | ON HOLD HQ (dừng) |
| 8 | RHQ PC approver | Duyệt và chuyển COEC về IN PROGRESS | IN PROGRESS |
| 9–10 | Doer (ImpEx, Groovy: Tech Level 2) | Pre-run checklist; chạy đúng như đã duyệt; post-check; kết quả trên COEC và PC | IN PROGRESS, rồi LAUNCH VERIFICATION |
**Quy tắc nội dung (TC-05 template đề xuất):** summary `[PC] [Market] [Short change] (COEC [number])`. Scope là danh sách mã cụ thể + số lượng, không bao giờ "all SKUs with status X"; dữ liệu cá nhân chỉ dạng file đính kèm. Đủ evidence ngay lần đầu: ảnh before (đã che), kết quả staging (bắt buộc với ImpEx/script mới), file có mandatory line, internal control, rollback hoặc "irreversible" kèm lý do. Run window theo ICT và SGT, người chạy và post-check.
**Áp dụng TRN-038:** summary `[PC] [MY] Archive 312 MX SKUs (COEC [number])`. Scope: danh sách 312 mã × 3 catalog. Before values export theo từng catalog (có thể khác giữa `mysmeProductCatalog` và `myb2bProductCatalog`) để rollback khôi phục từng catalog. Kết quả staging trên các catalog version Staged. Mandatory line trong ImpEx. Second checker và Tech Lead review comment. Run window trước go-live D+1 10:00 MYT (09:00 ICT); deadline SLA Merch D+1 12:00 ICT. Chỉ có một PC approver và PC ticket chờ ~3 giờ nên gửi sớm.
**Pre-run checklist:** PC đã duyệt và số khớp script; có mandatory line; có kết quả staging; self-QA xong và với script mới thì người thứ hai đã kiểm; rollback plan đã viết; môi trường và scope đã duyệt. Không bao giờ sửa file sau khi duyệt.
> RHQ chưa đưa template PC ticket chính thức hay các field Jira bắt buộc (TC-05 §3.4); dùng template đề xuất. Mandatory line cố định, là dòng đầu script: `#NOTE ITGC_JIRA:PC-xxxxx (COEC-xxxxx)` trong ImpEx và `//NOTE ITGC_JIRA:PC-xxxxx (COEC-xxxxx)` trong Groovy (A.II.2 quy tắc chung; TEC-MON-02 bước 9; CM-13 §9.3). Dạng "PC ticket: … | COEC ticket: …" của đề xuất TC-05 bị bỏ. Thiếu dòng là vi phạm nghiêm trọng.

### 3. Knox cho giá và promotion
Giá và promotion phải được Knox duyệt trước khi publish live. Knox là cổng riêng cạnh QA và Shift Leader duyệt; không thay thế cái nào.
- **Khi nào cần Knox lại:** nếu **action, condition, website hoặc date** của promotion đã publish đổi, lần publish kế phải duyệt lại. Đổi cấu hình khác (VD tên promotion) không cần.
- **Đường duyệt:** khác nhau theo subsidiary và ngành hàng (MX là mobile, CE là consumer electronics). Campaign brief có cột approval path do subsidiary điền; CoE theo đúng và không bao giờ tự chọn đường.
- **Request gấp:** vẫn setup rồi gửi Knox như thường. Last-minute chỉ bỏ QA của CoE, không bao giờ bỏ Knox.
- **Evidence giữ:** trên ticket ghi giờ gửi Knox và đường nào. Shift Leader theo dõi ticket chờ Knox ở mục 7 handoff note.
- **File giá Knox:** mọi cột đúng, không khoảng trắng đầu/cuối, đúng site và currency. Không bao giờ sửa file của subsidiary: trả lại kèm các ô cần sửa. Không bao giờ thêm/bớt/đổi approver trong approval line; việc đó cần ticket chính thức (MER-PRC-02; Handover P1 23:15–27:20). Một lần submit Knox giá tối đa 10,000 dòng.
**Áp dụng TRN-029:** subsidiary PH xin gia hạn hai rule PWP đã hết hạn (B2C và O2O, hai promotion group) từ D-1 23:59 đến 31/12/2026, và viết "no need QA preview, extend and raise knox approval, QA on live frontend". Gia hạn end date là thay đổi **date** nên mỗi rule cần Knox lại theo đường MX trước lần publish kế. "No QA preview" không được chấp nhận: ngoại lệ duy nhất cho QA gate là last-minute request do Shift Leader quyết. Hai promotion là Medium, không phải High như requester chọn (D13 under review).
> RHQ chưa nói ticket ở status nào khi chờ Knox (CM-13 §10.2). Tạm thời ghi giờ gửi và đường trên ticket, không chuyển ON HOLD SUBS chỉ để dừng clock. Cách gửi từng loại Knox học từ đội CoE hiện tại trong KT.
> **Under review (D1):** runbook giá/promotion sửa đổi giữ ticket ở ON HOLD SUBS với Doer là Assignee khi Knox pending, comment mỗi 2–3 ngày làm việc. Mục chờ Knox không chấm tới khi D1 chốt. **(D13):** runbook không thống nhất 2 promotion có phải Medium; hỏi Shift Leader và ghi lại lựa chọn.

### 4. Change freeze và exception
Freeze là giai đoạn quanh sự kiện lớn khi chỉ change được phép mới tới production.
| Freeze | Khi nào | Được phép gì |
|---|---|---|
| 48-hour freeze | 48 giờ trước 11.11, Black Friday, 12.12 (COE Lead công bố lịch hằng tháng) | Chỉ change đã được RHQ duyệt; với Tech PC ticket đã duyệt ghi "During the 48-hour freeze for [event]" |
| Soft freeze (flagship) | Ngày trên trang flagship của RHQ | Change hạn chế; exception cần duyệt |
| Hard freeze (flagship) | Ngày trên trang flagship | Hầu như không gì ngoài mục được liệt kê; subsidiary luôn cập nhật được stock |
| Hybris hard freeze | Thường 2–3 ngày sau Galaxy Unpacked | Coi mọi ImpEx, Groovy, cấu hình Back Office là không được phép trừ khi plan cho phép hoặc có exception approval |
| Shop App freeze | Ngày riêng | Kiểm Tech fix trên dữ liệu Shop App dùng |
> **Under review (D14):** RHQ (KT 21–22/10) mô tả ba giai đoạn: EPP 2.0 CMS hard freeze (cho sửa homepage, offer, detail; không publish nội dung flagship), Hybris soft freeze (chỉ đổi giá và promotion, duyệt qua PUMI theo approval path) và hot freeze 2–3 ngày sau Unpacked (chỉ cập nhật stock và dừng bán). Runbook sửa đổi theo mô hình đó. Bảng trên giữ tới khi D14 chốt. Quiz Q5 không chấm.
**Xin exception.** Exception (đổi sản phẩm, đổi giá last-minute) luôn cần duyệt và subsidiary phải tuân thủ. CoE tra approval trên compliance page và ghi vai trò approver, ngày, scope, link vào **thân ticket** trước khi làm. **Không approval, không làm.** Với Tech dưới flagship plan coi là hai approval: exception approval và PC ticket đã duyệt ghi "During [freeze type]; exception approval: [link]". Change sự kiện chuẩn bị từ T-14 và PC ticket duyệt trước T-2. Change khẩn trong incident vẫn theo CM-06 và vẫn cần PC ticket.
**Áp dụng TRN-029:** ticket tạo D0 14:00 PHT, trong Ops CoE stop cho setup MX/CE (D-3 → D+3) và bốn giờ trước flagship soft freeze. SKU không phải flagship và ticket không có exception approval. Hành động đúng: không đổi rule. Chuyển STG SETUP (initial response), rồi ON HOLD RHQ với một comment gộp: setup stop và freeze; rule đã hết hạn D-1 nên khoảng trống không backfill được; đổi date cần Knox mới; QA bắt buộc; đề xuất gia hạn ngay sau freeze, hoặc subsidiary tạo exception request với RHQ. Báo Merch Lead trong ca.
> Open points: PC ticket do PC approver duyệt có đồng thời là exception approval flagship không, và hành động vận hành (re-push stuck order, cancel order, sửa invoice) có được phép trong Hybris hard freeze không — chưa quyết (TC-05 §6.3); tới đó nếu plan không rõ thì Tech Lead hỏi RHQ trên Mattermost và không hành động khi chưa có trả lời trừ khi là incident. TRN-029 mô tả freeze exception như chuỗi PUMI nhiều cấp do subsidiary khởi xướng; CM-13 mô tả PUMI chỉ cho data và report. Theo CM-13: CoE không bao giờ tự duyệt exception và ghi evidence duyệt vào thân ticket.

### 5. Kiểm compliance trước khi thực thi
Chạy trên mọi change trước hành động production đầu tiên. Mỗi "không" là thứ còn thiếu; chưa sửa thì chưa bắt đầu.
| # | Câu hỏi | TRN-038 (bulk archive) | TRN-029 (gia hạn PWP) |
|---|---|---|---|
| 1 | Route đúng? | COEC liên kết + PC ticket; ticket Merch ON HOLD COE | Workflow Shop Merchandising + Knox |
| 2 | Scope xác nhận bằng văn bản? | Hỏi: catalog eStore (B2C) có trong scope không; SKU nào phải giữ active ở đâu? | Hai rule, hai promotion group (B2C, O2O) |
| 3 | Kiểm freeze? | Không ở hard freeze; ImpEx sẽ không được phép nếu có | Trong setup stop và soft freeze: bị chặn |
| 4 | Approval | Shift Leader (R2); PC ticket do RHQ PC approver duyệt | Exception approval; Knox lại theo đường MX |
| 5 | Evidence | Before values mỗi catalog, kết quả staging, mandatory line, comment của checker và Tech Lead, rollback | QA preview, internal check, giờ + đường gửi Knox |
| 6 | Status đúng khi chờ? | COEC ON HOLD HQ "PC ticket pending" | ON HOLD RHQ cho freeze; không ON HOLD SUBS để dừng clock |

## Quiz (đáp án)
1 Tech Team Member phải xóa một user group khỏi 1,200 customer account bằng ImpEx mới → **B: PC ticket: kết quả staging (ImpEx mới), before data, rollback, mandatory line, second checker; COEC sang ON HOLD HQ** (PUMI chỉ cho report và trích xuất dữ liệu, không để đổi dữ liệu). 2 Promotion đã publish đổi tên "Nov" → "Dec"; promotion đã publish khác dời end date 3 ngày → **C: chỉ đổi end date cần Knox lại**. 3 Cột approval path trong brief trống, subsidiary nói "dùng đường CE như mọi khi", sản phẩm là điện thoại → **C: xin subsidiary điền approval path trong brief; không tự chọn đường**. 4 TRN-038: ImpEx sẵn sàng, đã test staging, PC đã duyệt, nhưng header file vẫn mang số PC của lần chạy tuần trước → **B: dừng; mandatory line phải mang số PC đã duyệt và số COEC; checker đối chiếu trước khi chạy; chạy sai dòng = strike**. 5 (không chấm tới khi D14 chốt) Hai ngày sau Galaxy Unpacked, MY xin thêm instalment payment mode, nói "đã duyệt" nhưng không gửi evidence → **B: kiểm compliance page; có exception approval thì ghi vào thân ticket và tiếp tục staging, review, PC ticket ghi freeze và link; không có thì không làm và báo Tech Lead**. 6 10/11 20:00 bulk coupon ImpEx cho 11.11 chưa gửi PC ticket → **B: PC ticket sự kiện phải duyệt trước T-2, trước freeze; giờ chỉ change đã được RHQ duyệt mới chạy, nên escalate Tech Lead và thống nhất plan với requester**. 7 TRN-029 đến trong setup stop với label `Urgent_Request` → **B: urgent không vượt freeze hay Knox; không đổi rule, chuyển ON HOLD RHQ với một comment gộp và đề xuất đường nhanh nhất tuân thủ**.

## Practice
**PR-GP4.1-1. Compliance check cho hai change** (30', giấy, theo cặp; SCOE-44 TRN-038 và SCOE-35 TRN-029; với TRN-029 facilitator phát thông báo freeze: Ops CoE stop setup MX/CE từ D-3 đến D+3, soft freeze từ D0 18:00 KST, hard freeze D+2 đến D+3; ticket tạo D0 14:00 PHT). Với mỗi ticket chạy kiểm compliance 6 câu, liệt kê mọi thứ còn thiếu trước khi thực thi, route đúng và Jira status đúng. TRN-038: nháp thêm summary line PC ticket và các heading phần description. TRN-029: viết comment duy nhất gửi requester. **Pass:** TRN-038 — COEC liên kết đã tạo và ticket Merch ở ON HOLD COE (không chuyển); R2, không E4 (312 SKU < 500, một market); thiếu trước khi thực thi: xác nhận scope bằng văn bản (catalog eStore, SKU giữ active), before values mỗi catalog, kết quả staging, rollback mỗi catalog, mandatory line, self-QA, second checker và Tech Lead review, PC ticket đã duyệt; COEC ở ON HOLD HQ "PC ticket pending"; không cần Knox; PC summary dạng `[PC] [MY] … (COEC …)` với scope là mã và run window trước 09:00 ICT D+1. TRN-029 — chưa setup gì; thiếu: freeze exception approval, Knox lại cho cả hai rule (đổi date, đường MX), QA preview; priority Medium kèm lý do; initial response sang STG SETUP rồi ON HOLD RHQ; một comment nêu freeze, khoảng hết hạn, nhu cầu Knox và QA, và phương án nhanh nhất tuân thủ. Không bước nào làm trước approval của nó ở cả hai ticket. Không cần truy cập hệ thống.
