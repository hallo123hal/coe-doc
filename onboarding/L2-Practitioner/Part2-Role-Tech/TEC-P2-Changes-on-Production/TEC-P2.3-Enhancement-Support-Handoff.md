# TEC-P2.3 Enhancement support and handoff

> Nguồn: page 2484338926 · 60' (Study 15' · Demo 10' · Quiz 5' · Practice 30') · Facilitator: Shift Leader/Sub-Lead · Capabilities C2, C4 · Cần xong TEC-4.1 (Enhancement, release và BVT cho Tech; CoE không build code). Chưa có practice ticket cho service này: facilitator đưa brief mô phỏng. Access: Confluence (read); tuỳ chọn HAC staging el3-s2 cho export cấu hình read-only. Có thể làm hoàn toàn trên giấy.

## Mục tiêu
Phân loại một support item enhancement vào V1–V7 và nói CoE làm gì, cái gì giao build team, SDS India hay service cấu hình sở hữu; viết impact note build team hành động được (giá trị hiện tại theo market, gap, câu hỏi đánh số, acceptance criteria đề xuất); lên kế hoạch test data và BVT lùi từ go-live, định tuyến defect sau launch theo ngày hết warranty; chuẩn bị handoff đầy đủ để Sub-Lead duyệt không phải sửa nhiều.

## Thuật ngữ
**Enhancement Request (parent)** (ticket tính năng mới của development team; build team chuyển status, CoE không bao giờ làm); **Support Sub-task** (item con nơi CoE làm việc: "Requirement Analysis…", "Technical Analysis", "Test Case Execution", "Pre & Post Launch Support"); **Build team (Spoke)** (đối tác dev thiết kế, code, deploy; BA là đầu mối khi BVT); **Impact note** (ghi chú CoE theo market trước requirement sign-off: object chạm tới kèm giá trị hiện tại, gap, câu hỏi đánh số, acceptance criteria đề xuất, service bị ảnh hưởng); **Dormancy key** (key Tokoconfig theo store mà enhancement ship ở trạng thái tắt, VD key `toko.smc.%`: 15 cờ SC+ theo store trên staging); **Readiness checklist** (trang sẵn sàng production lập cùng build team: release, bước bật, owner, giờ theo market, verify, đường tắt); **Warranty period** (2 tuần Launch Verification của parent; defect trong đó đi build team, sau đó TEC-TSP-01); **Enhancement tracker** (sổ CoE mỗi enhancement: key, market, kênh, build team, release, go-live, cửa sổ BVT, hết warranty, COE owner).

## Nội dung
### 1. TEC-ADH-02 trong một trang
Hỗ trợ vận hành cho enhancement do đối tác dev hoặc RHQ Platform team xây. 2026: 367 ticket, ~38/tháng, cả 8 market. SC+ chiếm ~1/3 enhancement (~57/157 parent), phương thức thanh toán ~46.
| Mục | Luật |
|---|---|
| Doer | Enhancement desk Tech Level 2; mỗi enhancement một COE owner có tên; Level 1 giữ tracker và nhắc |
| Checker | Tech Sub-Lead review mọi impact note, plan, enablement checklist **trước khi gửi** |
| Approver | Không có cho support; RHQ PC approver (hiện Oliver Leung) duyệt enablement trên production |
| Priority | P3 (40h, nội bộ 26h) mỗi support item; P2 (16h) khi câu hỏi chặn BVT/release trong 2 ngày làm việc; plan item đến hạn 2 ngày làm việc trước mốc nó phục vụ. Jira hiện P4 trên hầu hết ticket 2026 (359/367); SLA theo P4 hay P3 là câu hỏi mở cho RHQ PIC |
| Change class | Không có trong service này. Không bao giờ chạy setting production từ ticket này |
| Rủi ro lớn nhất | Tính năng deploy nhưng không bật, hoặc bật khác nhau theo market, và BVT bắt đầu không có test data |
| Variant | Dùng khi |
|---|---|
| V1 Requirement review và impact note | Phân tích requirement, user story, acceptance criteria, trước sign-off |
| V2 Build team question | Build team hỏi hiện tại hoạt động thế nào |
| V3 Test data và BVT plan | Release có cửa sổ BVT |
| V4 Production enablement và post-launch support | Bật tính năng đã deploy, hỗ trợ launch, bàn giao kiến thức |
| V5 Multi-market rollout tracking | Một enhancement clone theo market |
| V6 Incident → enhancement request | Fix incident cần build >~5 ngày |
| V7 Handover enhancement đã giao | (thêm 01/11) build team bàn giao tính năng cho vận hành |
Clock theo workflow của Sub-task (tên status: xác nhận ở KT) và chỉ dừng khi item ở requester hoặc team khác, sau một lần làm rõ đầy đủ. "Waiting for Customer", "Escalated", "Scheduled / Pending Go-live" không phải status CM-13: đừng dựa vào.
> Vòng đời parent viết khác nhau ở hai nguồn: TEC-ADH-02 (New/In Evaluation, Local Review, Pre-Check, Assigned, Requirement sign-off, In Progress, QA Server Review (BVT), Approved for Launch, Launch Verification, Closed) và CM-12 §4.1 (NEW, IN EVALUATION, APPROVED-ES, REQUIREMENTS SIGN-OFF, IN PROGRESS, QA SERVER REVIEW, APPROVED FOR LAUNCH, LAUNCH VERIFICATION, CLOSED). Cả hai đồng ý CoE không bao giờ chuyển parent; tên chính xác để KT.

### 2. Ai làm gì
BiPlus trả lời, review, lập kế hoạch, verify. Không đổi code, thiết kế hay setting production trong service này.
| Việc | Ai | CoE bàn giao thế nào |
|---|---|---|
| Thiết kế, code, deploy; sub-task "Technical Implementation" | Build team (development team, Spoke) | Trả lời câu hỏi trên Sub-task (V2); defect BVT gửi bug ticket cho build team, fix ~2-3 ngày |
| Impact note, trả lời, BVT plan, readiness checklist, verify, KB | CoE Tech Level 2 (ADH-02) | Post trên Sub-task sau Sub-Lead check |
| Test data trên staging | TEC-BVT-02 (kỹ thuật), MER-BVT-02 (sản phẩm, giá) | Data ticket có due date, link tới parent |
| Chạy và quản lý BVT | TEC-BVT-01, MER-BVT-01, COE-BVT-01; QA Team **không** tham gia | Plan giao COE-BVT-01 |
| Enablement production (Tokoconfig, payment mode, delivery) | Service sở hữu (VD TEC-CFG-03, TEC-SIT-05) với PC duyệt | Bước readiness checklist có owner, ngày, đường tắt |
| Incident live; defect sau warranty | TEC-TSP-01; bug code/platform đi SDS India (Samsung L2/L3) qua Maintenance Request | Evidence pack; COEC ở SYSTEM SUPPORT, CoE giữ ownership |
| Defect trong 2 tuần warranty | Build team, qua parent enhancement | Comment và link trên parent |
Escalate sang SDS India chỉ Tech Level 2 (kể cả on-call) làm, với evidence pack 8 phần: số COEC, market, bước lỗi, lỗi nguyên văn, giờ bắt đầu, thay đổi gần nhất, đã thử gì, ước tính ảnh hưởng.
> Outline session ghi "what goes to SDSAP". Trong nguồn Confluence SDSAP là operator hiện tại bàn giao cho BiPlus, dịch vụ hết 30/11/2026 (TC-01 §2.4); enhancement đi "development team, Spoke", bug platform đi SDS India. Công ty nào build enhancement sau khi tiếp quản và Spoke có thuộc SDSAP không: không nêu, xác nhận ở KT. Bàn giao cho "build team ghi trên parent ticket".

### 3. Impact note: handoff mà build team hành động được
Impact note (V1) là handoff chính, đến hạn **trước requirement sign-off**, Sub-Lead check, post trên Sub-task và thành review comment trên requirement document.
| Bước | Doer | Checker (Sub-Lead) |
|---|---|---|
| 1 | Đăng ký enhancement vào tracker; đọc parent (vấn đề, version requirement doc, acceptance criteria); báo requester một lần các mục governance còn thiếu | Phủ mọi market và kênh trong scope |
| 2 | Export cấu hình hiện tại theo market, read-only và có ngày: payment mode, delivery mode, Base Store, key Tokoconfig (không bao giờ `secureValue`), template, field NERP và FI | Giá trị đúng môi trường, có ngày |
| 3 | Map từng acceptance criterion tới object, bước Backoffice, report, catalogue service | Mọi criterion được map |
| 4 | Liệt kê gap: thiếu mã theo market, bản dịch, template, xung đột, effort sau go-live, không có option tắt; hỏi cấu hình đơn thuần có đáp ứng không | Đã cân nhắc phương án chỉ-cấu-hình |
| 5 | Viết note: scope, market, object kèm giá trị hiện tại, rủi ro, câu hỏi đánh số, acceptance criteria đề xuất, service bị ảnh hưởng | Câu hỏi đánh số và có owner; không dữ liệu khách |
**Ví dụ mô phỏng (VN, SC+ hằng tháng có tháng miễn phí).** Export read-only staging el3-s2 (24/10/2026): V-ADH-02-1 trả 20 payment mode `vn-` kèm cờ active; V-ADH-02-2 trả 15 delivery mode `vn`; query `toko.smc.%` trả 15 key SC+ theo store (id, my, nz, ph, sg, vn); multistore test `sg_test1`, `id_test1`, `phtest1`, `test1`, `test_smb_th`, `epp_smetesting` tồn tại và active. Note liệt kê object có giá trị kèm ngày, đặt câu hỏi đánh số (payment mode nào được mang tháng miễn phí; tên dormancy key theo store; đường tắt), đề xuất acceptance criteria theo market, nêu service bị ảnh hưởng (SC+ set-up MER-PRD-03, payment mode TEC-SIT-05).
> KB chưa có template impact note, và export cấu hình nào được phép trên production cần xác nhận ở KT. Dùng 5 khối trên và lấy giá trị từ staging khi production chưa cho export, ghi nhãn môi trường và ngày.

### 4. Test data và BVT plan, tính lùi từ go-live
Lập lùi từ các ngày build team và RHQ đưa: go-live, build freeze, go/no-go, cửa sổ BVT, môi trường.
- BVT kết thúc ít nhất **2 ngày làm việc trước go/no-go** để fix và retest.
- Test data sẵn sàng **2 ngày làm việc trước khi BVT bắt đầu**.
- RHQ chốt cửa sổ BVT ~1 tuần trước và ngày không thương lượng.
- Liệt kê data: kỹ thuật (site, store, payment/delivery mode, user group, test user, EPP access, order ở status cho trước) cho TEC-BVT-02; sản phẩm, giá, promotion, SC+, stock cho MER-BVT-02. Nêu tên SKU test theo market và kiểm tồn tại.
- Giao plan cho COE-BVT-01: một BVT PIC mỗi team và market. Chọn PIC theo scope: checkout, payment, order, invoice, EPP access, integration, cấu hình Backoffice kỹ thuật → Tech PIC.
- Ghi snapshot cấu hình staging lúc BVT bắt đầu (KE-TEC-ADH-02-04: setting staging dùng chung bị team khác đổi gây pass/fail giả).
Go-live cần 100% test case pass kèm bằng chứng; 99% = không go-live.
**Ví dụ (ngày mô phỏng).** Go/no-go thứ Sáu 20/11. BVT phải kết thúc thứ Tư 18/11; cửa sổ 4 ngày thì bắt đầu muộn nhất thứ Sáu 13/11, test data sẵn sàng thứ Tư 11/11. Data ticket cho TEC-BVT-02 và MER-BVT-02 tạo ngay với các due date đó.
KT 21/10: "Kickoff do development team chạy cùng CoE và subsidiary: demo tính năng, test case, test data, ngày bắt đầu/kết thúc. … Bug: tạo bug ticket cho development team; fix ~2–3 ngày. BA của Spoke theo dõi. … Sign-off: test case pass 100% có bằng chứng trên Confluence; 99% thì không go live."

### 5. Enablement, định tuyến warranty, incident → enhancement
**Enablement (V4).** Lập readiness checklist cùng build team: release đã deploy, từng bước bật (setting, toggle, data), owner, ngày và giờ theo market, bước verify, đường tắt. Enhancement ship ở trạng thái tắt sau key Tokoconfig theo store nên "deployed" không phải "live" (KE-TEC-ADH-02-05). Mỗi bước route cho service sở hữu; chỉ chạy sau PC duyệt, do CoE Tech: không có Accenture cho SEAO và không phụ thuộc development team cho thay đổi cấu hình hay data. Verify trên production bằng test account, record Backoffice và output interface nếu thấy được. Theo dõi trong thời gian thoả thuận (thường 3 ngày làm việc).
**Định tuyến warranty.** Ghi ngày hết warranty vào tracker. Trong 2 tuần warranty: defect đi build team qua parent. Sau đó: TEC-TSP-01. Defect gây thiệt hại: tắt tính năng qua service sở hữu, COE-INC-01 nếu P0.
**Incident → enhancement (V6).** Khi TEC-TSP-01 cho thấy fix cần >~5 ngày build, hoặc requester xin hành vi mới, soạn request cho requester: problem statement, hành vi hiện tại kèm bằng chứng, market, ảnh hưởng kinh doanh, acceptance criteria đề xuất, incident liên kết. Thống nhất kết quả incident (workaround tại chỗ, incident resolved kèm link) và theo dõi request mới tới khi được chấp nhận/từ chối.
**Bàn giao enhancement đã giao (V7, thêm 01/11).** Khi build team bàn giao tính năng đã deploy cho vận hành, thường cuối giai đoạn giám sát (~14 ngày), kiểm pack có 3 phần: hướng dẫn setup và vận hành, danh sách lỗi có thể xảy ra, cấu hình local theo market (luật SDSAP, handover SC+ MX và CE 28/10). Đòi build team phần thiếu trước khi hết warranty (KE-TEC-ADH-02-10). Ghi enablement key theo market kèm giá trị production, ticket tham chiếu, ngày hết warranty, rồi publish trang KB dưới "Handover of enhancements to Operation COE" (TEC-KNB-01).
**Một handoff tốt gồm (checklist Sub-Lead):** mọi market và kênh trong scope; giá trị hiện tại đúng môi trường, có ngày; từng acceptance criterion được map; câu hỏi đánh số có owner; đã cân nhắc phương án chỉ-cấu-hình; ngày plan khớp lịch release; data ticket có due date; readiness checklist có owner, giờ, đường tắt; ngày hết warranty; quyết định từ call/chat tóm tắt vào Jira trong 1 ngày làm việc; không dữ liệu khách.
Handover liên quan: SC+ MX và CE (28/10: handover phải có gì; ~14 ngày giám sát rồi maintenance và L2); Working Session P1 (23/10: BVT document, staging access, trang test data); Auto MBO Flag and Price (27/10: bốn key enablement theo site, nay chuẩn cho flagship); PH SMS Viber OTP (28/10: dự án một lần với một cờ enable, vai trò CoE sau go-live).

## Quiz (đáp án)
1 Build team xin "bật luôn" key Tokoconfig SC+ trên production từ Sub-task vì tính năng đã deploy → **B: route bước cho service sở hữu (TEC-CFG-03) với PC, theo readiness checklist** (CoE không bao giờ chạy setting production từ ticket ADH-02; không chuyển parent). 2 Requirement sign-off thứ Năm; impact note đến hạn khi nào và ai check → **B: trước thứ Năm; Tech Sub-Lead check trước khi gửi**. 3 Go/no-go thứ Sáu 20/11; BVT bắt đầu thứ Sáu 13/11 → **B: BVT kết thúc 18/11; data sẵn sàng 11/11** (2 ngày làm việc mỗi mốc). 4 Defect xuất hiện 3 tuần sau launch, warranty 2 tuần → **B: TEC-TSP-01 (và SDS India qua Maintenance Request nếu bug platform)**. 5 Fix incident cần ~8 ngày build → **C: V6: soạn enhancement request (vấn đề, bằng chứng, market, ảnh hưởng, acceptance criteria đề xuất, incident liên kết) và thống nhất kết quả incident**. 6 Quyết định scope thống nhất qua chat với build team → **B: tóm tắt vào Jira trong 1 ngày làm việc và xin xác nhận**. 7 Requester nói tính năng "live" nhưng khách không thấy → **B: deployed nhưng chưa enabled (dormancy key còn tắt); kiểm readiness checklist và verify trên production** (KE-TEC-ADH-02-05).

## Practice
**PR-TEC-P2.3-1. Handoff cho enhancement mô phỏng** (30'; giấy hoặc workstation CoE; facilitator đưa brief mô phỏng dựa trên ví dụ TEC-ADH-02: VN, "SC+ monthly with free months", requirement sign-off sau 5 ngày làm việc, go/no-go vào một thứ Sáu cho trước, cửa sổ BVT 4 ngày; kết quả staging read-only 24/10/2026 in sẵn: 20 payment mode `vn-`, 15 delivery mode `vn`, 15 key `toko.smc.%`, 6 multistore test active). Làm: (1) điền dòng tracker; (2) viết impact note: scope, market và kênh, object kèm giá trị hiện tại (nhãn "staging el3-s2, 24/10/2026"), gap, ≥5 câu hỏi đánh số có owner, acceptance criteria đề xuất, service bị ảnh hưởng; (3) lập BVT plan lùi: ngày kết thúc BVT, ngày test data sẵn sàng, data ticket cho TEC-BVT-02 và MER-BVT-02, Tech PIC; (4) soạn các dòng readiness checklist cho enablement (bước, service sở hữu, có cần PC, owner, giờ VN, verify, đường tắt); (5) viết dòng định tuyến warranty. **Pass:** note phủ mọi market trong scope, mọi giá trị có ngày và môi trường; câu hỏi đánh số có owner; đã cân nhắc phương án chỉ-cấu-hình; BVT kết thúc 2 ngày làm việc trước go/no-go và data sẵn sàng 2 ngày làm việc trước BVT; enablement Tokoconfig đi TEC-CFG-03 kèm PC, không bao giờ từ ticket ADH-02; có đường tắt; ghi ngày hết warranty và luật định tuyến (build team trong warranty, TEC-TSP-01 sau); không dữ liệu khách. Sub-Lead (hoặc facilitator) chấp nhận không phải sửa nhiều. Không cần access hệ thống.
> Material gap: chưa có practice-lab ticket cho TEC-ADH-02, bài này dùng brief mô phỏng. Thay bằng replay các Sub-task enhancement đã đóng (VD VNME-29364 và AUME-19457, read-only) khi thu thập xong.
