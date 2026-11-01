# TEC-P4.3 BVT PIC for Tech and role track exit

> Nguồn: page 2484240841 · 120' (Study 30' · Demo 20' · Quiz 10' · Practice 60') · Facilitator: Shift Leader/Sub-Lead · Capabilities C3, C4 · Cần xong TEC-4.1 (Enhancement, release, BVT cho Tech) và TEC-4.2 (Role track exit: Tech final assessment), cùng các session TEC-P cho service sẽ thi. Mang danh sách service đã tập trong TEC-P1…P4 (VD TEC-MON-01, TEC-TSP-01, TEC-TSP-05), runbook từng cái, phiếu T4 replay và T5 trống từ facilitator. Access: staging Backoffice + HAC el3-s2, storefront staging với cookie từ getcookie.html, Jira SCOE; đánh giá chỉ chạy staging, không chạm production. Không access: học Lesson và làm Quiz trước, lên lịch BVT smoke, T4 replay, T5 khi có access.

## Mục tiêu
Quyết định Tech có phải BVT PIC của một enhancement không và viết comment bắt đầu; chạy BVT smoke check trên staging: pre-check, chạy case, theo dõi order qua các job, ghi Pass/Fail/Blocked kèm bằng chứng đạt chuẩn; xử lý case fail qua defect, retest và sign-off, tính chi phí KPI BVT trong Composite SLA; qua Tech role track exit, và biết các bước T4, T5, T6 theo từng service sau chương trình.

## Thuật ngữ
**Enhancement** (thay đổi trên eStore, Shop App hoặc AEM do development team phía Samsung làm, VD bước checkout mới; BVT test trước go-live); **BVT PIC** (người CoE phụ trách một vòng BVT; Tech khi enhancement chạm checkout, payment, order, invoice, EPP access, report, integration hay cấu hình Back Office kỹ thuật); **BVT window** (ngày test cố định RHQ công bố tối đa 1 tuần trước, VD 2-5/11; không thương lượng); **Pre-check trước khi đặt order** (smoke check trước case dựa trên order: SKU trong NERP có MAP và giá, map warehouse đúng, stock trong warehouse đó); **Test case status** (Not run, Pass, Fail, Blocked; mỗi lần chạy lại là run mới, giữ kết quả cũ); **Evidence caption** (`Case ID | Run | dd-Mon hh:mm SGT | Environment | Market store | Result`, một screenshot mỗi case và run); **T4 practical replay** (ticket đã đóng làm lại trên staging; đạt khi first-pass yield ≥90% và không lỗi nghiêm trọng); **T5 certification exam** (một ticket của service làm trên staging (A), duyệt runbook (B), tình huống ngoại lệ (C); mọi bước đúng và bước critical 100%); **First-pass yield (FPY)** (tỷ lệ replay đúng ngay lần đầu, VD 9/10 = 90%); **Certification L1** ("Certified": được nhận ticket live của service đó, 100% output được kiểm trước production).

## Nội dung
### 1. BVT và Tech PIC
Trước khi enhancement go-live RHQ mở vòng BVT. CoE dùng tính năng mới như user nghiệp vụ ở 8 market, so với kết quả mong đợi, ghi bằng chứng mọi case, ghi defect cho development team, và chỉ đề xuất sign-off khi 100% case pass. CoE làm hai việc: hỗ trợ subsidiary kiểm backend và cấu hình, và tự chạy test end-to-end, thêm case market. Regression của team global ngoài phạm vi CoE.
| Enhancement chạm | PIC |
|---|---|
| Promotion, coupon, giá, set-up sản phẩm, buying page, AEM, Shop App CMS, text và flag | Merchandising |
| Checkout, payment, order, invoice, cancel/return, EPP access, report, integration, middleware 3PD, cấu hình Back Office kỹ thuật | Tech |
| Cả hai | Hai PIC, một lead PIC theo phần lớn hơn; một trang BVT và một file Excel chung |
Tám luật RHQ tóm tắt: window công bố tối đa 1 tuần trước, không thương lượng; theo dõi trên ticket enhancement của development team, không project riêng; PIC là Merch hoặc Tech, **QA Team không tham gia**; kickoff là ngày 1, PIC comment "received, understood, starting" và tạo trang Confluence; CoE thêm case market; **go-live chỉ khi 100% pass, 99% = không go-live**; RHQ kiểm bằng chứng; không sign-off đúng hạn = không go-live. Ticket SEAO dùng chung được test ở cả 8 nước trong cùng window.
BVT không có SLA clock nhưng ba KPI nằm trong Composite SLA: Test Case Pass Rate 6%, Test Report Completion 3%, User Acceptance 1%. Ở Tech, Tech Lead thường giao Team Member tuần Level 2 kèm backup; P0, P1 vẫn đi trước BVT. Runbook TEC-ADH-02 (V3) đặt timing: BVT kết thúc ít nhất 2 ngày làm việc trước go/no-go, test data sẵn sàng 2 ngày làm việc trước BVT. Sub-task hỗ trợ trên enhancement có workflow riêng, không phải workflow COEC.
> Vai BVT Coordinator vẫn chờ quyết. TC-01 và TC-02 nói hiện tại Tech Sub-Lead giữ lịch BVT chung và Tech Lead giao người Tech; CEO quyết (DL-01).

### 2. Chạy vòng: bước, smoke check, bằng chứng
| Mốc | Target |
|---|---|
| Kickoff = ngày 1 | Comment bắt đầu ngay sau kickoff; tạo trang BVT; case rủi ro cao và case market trước; ≥50% case chạy ngày 1; mọi defect có defect row ngay hôm đó |
| Ngày 2 | 100% case chạy ít nhất một lần (window 4 ngày); mọi window: lượt chạy đầy đủ đầu tiên trong nửa đầu |
| Hằng ngày | File Excel và trang BVT cập nhật trước 16:30 SGT (15:30 giờ Việt Nam), hoặc giờ họp nếu RHQ đặt sớm hơn |
| Ngày cuối | Retest cuối, test report trong 4 giờ làm việc sau khi case cuối pass, User Acceptance, comment đóng |
| Bước (TEC-BVT-01, V1 Enhancement BVT) | Doer | Checker |
|---|---|---|
| Trước khi bắt đầu | Đọc "[READ ME] BEFORE DOING BVT" và "Pre-check Before Place Order"; thông báo có scope, môi trường, test case, hạn hoàn tất; không nằm trong cửa sổ deploy lịch STGx | Thông báo đầy đủ |
| Snapshot | Ghi key tokoconfig và setting trang ticket nêu (không secret) | Giá trị khớp trang |
| Smoke check | Lấy cookie (getcookie.html), mở storefront; pre-check SKU: trong NERP có MAP và giá, map warehouse đúng, stock trong warehouse | Data sẵn sàng trước case order |
| Thực hiện | Chạy từng case đúng như viết; screenshot mỗi bước, số order | Mỗi case chạy có kết quả và bằng chứng |
| Theo dõi order | Backoffice › Order › Orders; order kẹt >1 giờ chỉ tới job của nó (Waiting for Financial Send: `tokoFinancialInitialUpdateJob`; Order Split: `tokoTransferConsignmentToWarehouseJob`; shipping: `bulkFetchConsignmentUpdateJob`; Wait for Financial: `tokoFinancialCompletionJob`) | Lỗi được phân tích: defect, data hay môi trường |
| Report | Trang BVT và Excel master; Sub-Lead review trước hạn hằng ngày | Defect log đủ; pass rate = pass / đã chạy; nộp đúng hạn |
Trên el3-s2 `my-tokoFinancialInitialUpdateJob` đang inactive nên order MY không rời Waiting for Financial Send ở đó: kiểm trước case MY. Staging el3-s2 còn dùng cho release BVT của người khác: không đổi object không tạo cho case của bạn.
**Chuẩn bằng chứng.** Một screenshot mỗi case và run, caption `Case ID | Run | dd-Mon hh:mm SGT | Environment | Market store | Result`; chụp trên workstation CoE và upload thẳng lên trang BVT rồi xoá khỏi máy; chỉ dùng test account; không dùng lại từ case/run/ngày khác; không đưa vào công cụ AI. Chỉ dùng Blocked khi case thật sự không chạy được, không bao giờ để che Fail.
> TEC-BVT-01 service pack (vault, draft v0.1/runbook v0.2) không có bản Confluence nên không link được; các bước trên lấy từ đó. Target nội bộ "chạy xong ở 65% window" chặt hơn mốc CM-12 (lượt đầy đủ đầu trong nửa đầu); theo CM-12 và coi 65% là điểm muộn nhất. Nơi ghi defect (Jira EMBT cho Hub, SAM cho Spoke theo pack; sheet Defect của Excel theo CM-12) cần xác nhận ở KT; mọi trường hợp đều ghi defect vào file Excel.

### 3. Defect, retest, sign-off và chi phí KPI
**Case fail:** chạy lại đúng các bước và kiểm data, account, môi trường; ghi Fail kèm bằng chứng; thêm defect row (`DEF-nn`, tiêu đề `[enhancement code] [market] actual result`, bước, expected/actual, bằng chứng, severity đề xuất) trong 1 giờ làm việc; ghi mã defect vào dòng case và comment defect trên ticket enhancement; upload Excel; báo blocker ngay trên kênh; theo dõi hằng ngày với BA phía Spoke (fix hiện mất 2-3 ngày).
**Retest** chỉ khi fix đã ở môi trường test, trong cùng ngày, và chạy lại cả case liên quan. Ghi mỗi lần là run mới; không sửa kết quả cũ.
**Sign-off:** PIC đề xuất và Lead xác nhận khi 100% case chạy pass, không Blocked hay Not run, defect log đóng, test report đủ và User Acceptance được ghi (ai, khi nào, ở đâu). RHQ sign-off cuối và quyết go-live.
**Ví dụ CM-12 (mô phỏng).** Một tháng có 2 vòng BVT. Lần chạy cuối 76/80 case pass; một test report trễ; một vòng thiếu User Acceptance.
| KPI | Kết quả | Điểm Composite mất |
|---|---|---|
| Pass Rate (6%) | 95.0% | 5.0 × 0.06 = 0.30 |
| Report Completion (3%) | 50.0% | 50.0 × 0.03 = 1.50 |
| User Acceptance (1%) | 50.0% | 50.0 × 0.01 = 0.50 |
| Tổng | | 2.30 |
Một ticket vi phạm Resolution tốn ~0.034 điểm nên report trễ một mình bằng ~44 ticket vi phạm. Với Resolution và Response 98%, tháng xuống 95.9%, dưới 97%.
Vi phạm BVT là vi phạm quy trình (RFP 3.4): ghi PASS cho case chưa chạy; dùng lại screenshot; đổi expected result không có xác nhận bằng văn bản; bỏ một ngày cập nhật; giấu blocker; report trễ do CoE. "Nếu không chạy kịp, ghi Not run và báo."
> RFP không nói Pass Rate tính trên lần chạy cuối hay mọi lần chạy, hay case fail do defect của development có tính vào CoE không. Chưa áp dụng phương pháp nào tới khi RHQ đồng ý (CM-12 §1.4); ghi mọi run kể cả run fail. BVT vi phạm có tính strike không cũng chờ quyết.

### 4. Role track exit, rồi certification theo service
Session này là Tech **role track exit**. Nó kết thúc chương trình; **không cấp certification cho service nào**. Certification tính **theo service**, không theo người. Không certification, không truy cập production; truy cập cấp theo đợt sau certification (29/10, 6/11, 13/11, 20/11).
| Level | Được làm gì | Đạt bằng |
|---|---|---|
| L0 Trained | Chỉ tập trên staging và replay | T3 |
| L1 Certified | Ticket live, 100% output kiểm trước production | T4 và T5 |
| L2 Independent | Làm một mình trong các gate; làm another set of eyes cho đúng service đó | T6 (tuần giám sát) |
| L3 Coach | Đào tạo và chấm người khác | Lead quyết |
Sau chương trình, Sub-Lead lên lịch certification theo service, ngoài lớp: T4 replay rồi T5 exam cho L1 Certified; sau đó T6, một tuần làm việc có giám sát, cho L2 Independent (FPY 90% tháng 11, 95% từ tháng 12; CM-11 §3.1). Người L1 không bao giờ là another set of eyes cho ai.
**T4 practical replay.** Sub-Lead chọn ticket đã đóng của service có bẫy phổ biến. Đọc mỗi cái như ticket mới: phân loại priority và rủi ro, kiểm đầy đủ, soạn câu hỏi cho subsidiary (không gửi), viết các đổi status Jira (Tech: NEW → ASSIGNED, ON HOLD HQ khi chờ PC), làm lại việc trên staging theo runbook kèm bằng chứng, viết hand-back tiếng Anh. Mỗi replay được review theo 8 điểm. Đạt: FPY ≥90% (VD 9/10) và không lỗi nghiêm trọng. Tech: replay runbook theo team và một incident drill. TC-01 Phụ lục A là case book Tech (VD A.1, replay cancel order trên staging, 45 phút).
**Lỗi nghiêm trọng của Tech** (một lỗi là fail): lên kế hoạch đổi production không có PC duyệt; ImpEx hoặc Groovy không có dòng đầu cố định `#NOTE ITGC_JIRA:PC-xxxxx (COEC-xxxxx)` (Groovy: `//NOTE ITGC_JIRA:PC-xxxxx (COEC-xxxxx)`) hay dòng khác; đổi trước khi PC duyệt; re-trigger trước khi đọc status payment gateway; chạm order BVT; TEC-ORD-05 đẩy sang Cancelled thiếu refund position cho mọi line; rerun cronjob không duyệt; làm service chưa cert; thao tác production; chuyển dữ liệu ra ngoài hệ thống Samsung; sai market/site/store; lỗi múi giờ làm lệch giờ hiệu lực.
**T5 certification exam (theo service):**
| Phần | Nội dung | Thời gian | Chấm |
|---|---|---|---|
| A. Thực hành | Một ticket làm trên staging theo runbook, có bằng chứng | 60-90 phút | Từng bước; bước critical 100% |
| B. Duyệt runbook | Giải thích từng bước, điểm kiểm soát và lý do; câu hỏi "what if…" | 20-30 phút | Mọi bước đúng |
| C. Tình huống ngoại lệ | Thiếu thông tin; second checker, PC, ON HOLD HQ; cảnh báo 70%; dấu hiệu incident | 20 phút | Đúng hành động, người, status, giờ |
Đạt khi mọi bước đúng và bước critical 100%. Sub-Lead chấm, Lead duyệt; kết quả vào skill matrix trên Samsung Confluence, nơi RHQ xem được.
> CM-11 và proposal v9.4 gọi L1 "Certified" và L2 "Independent"; dashboard v1.4 gọi L1 "Supervised" và L2 "Certified". Quyền của từng level giống nhau, chỉ tên khác. CEO quyết tên. TC-01 Phụ lục A đề xuất điểm đạt cho case book (mọi key point và 80% tổng điểm); luật T4 chính thức là CM-11 (FPY 90%, không lỗi nghiêm trọng): theo CM-11.

### 5. Chấm điểm, luật thi lại, và tiếp theo
| Bài | Ai chấm | Fail lần 1 | Fail lần 2 |
|---|---|---|---|
| T4 replay | Sub-Lead | Thêm replay, thi lại trong 2 ngày làm việc | Giao service rủi ro thấp hơn; bench hoặc ứng viên thứ hai thay |
| T5 exam | Sub-Lead chấm, Lead duyệt | Thi lại sau coaching | Như T4 |
| T6 tuần giám sát (bước lên L2) | Lead và SDM | Thêm một tuần giám sát | Rời queue; bench thay |
- Điểm đạt do BiPlus đề xuất để thống nhất với RHQ. Người dưới điểm đạt không bao giờ làm service một mình; bench hoặc ứng viên thứ hai thế chỗ.
- Mỗi service thi riêng; đạt T5 TEC-MON-01 không cert TEC-TSP-01.
- Khi runbook đổi, người đã cert được recertify.
- Sau L1: T6 là tuần làm việc giám sát với 100% output được kiểm; đạt khi FPY 90% tháng 11 (95% từ tháng 12), không lỗi nghiêm trọng, đạt target phản hồi.

## Quiz (đáp án)
1 Enhancement đổi cách hiển thị phí giao hàng ở bước payment; PIC CoE và QA Team có test không → **B: Tech PIC; QA Team không tham gia BVT**. 2 Ngày 3 của window 4 ngày, case không chạy được vì sandbox payment staging sập; đồng đội gợi ý ghi Pass với screenshot hôm qua của case tương tự → **B: Blocked, kèm lý do, giờ báo và người được báo; báo blocker trên kênh**. 3 Cuối window 79/80 case pass, một defect chờ fix, subsidiary nói tính năng ổn → **B: không sign-off: go-live chỉ khi 100% pass; tiếp tục retest khi fix tới và báo trạng thái**. 4 Tháng có Resolution và Response đều 98%, BVT mất 2.3 điểm vì report trễ và thiếu User Acceptance → **B: Composite tháng xuống ~95.9%, dưới 97%**. 5 T5 phần C: trong lúc thực hành thấy job export order staging lỗi ở 3 market cùng lúc → **B: coi là dấu hiệu incident: báo ngay Shift Leader hoặc Sub-Lead, không lặng lẽ sửa**. 6 T5 phần C: ticket replay cần đổi data production mà runbook phủ → **B: staging, self-QA, second checker L2/L3 đúng service, PC, COEC sang ON HOLD HQ "PC ticket pending", chỉ chạy sau khi Oliver duyệt**. 7 Đạt 9/10 replay T4 ngay lần đầu, nhưng một replay lên kế hoạch ImpEx thiếu dòng số PC và COEC → **B: Fail: một lỗi nghiêm trọng làm fail T4 bất kể FPY**. 8 Fail T4 lần đầu trên TEC-TSP-01 → **B: thêm replay, thi lại trong 2 ngày làm việc**.

## Practice
**PR-TEC-P4.3-1. BVT smoke check** (30'; staging el3-s2 storefront + Backoffice; facilitator đưa bộ mini BVT 4 case cho một enhancement Tech mô phỏng (một case order B2C SG, một case order MY, một case có lỗ hổng data cài sẵn, một case bị chặn bởi môi trường), trang BVT trong space sandbox và file Excel theo dõi; chỉ test account). Viết comment bắt đầu. Với mỗi case: pre-check SKU (NERP, MAP, warehouse, stock), chạy, theo dõi order trong Backoffice › Order › Orders, ghi status và bằng chứng với caption CM-12. Với Fail, viết defect row. Cuối cùng cập nhật trang và Excel và nói có đề xuất sign-off không. **Pass:** comment bắt đầu đủ năm mục (received, understood, starting; PIC và backup; số case; link trang BVT; update kế); mỗi case có status trung thực và screenshot caption riêng; case MY ghi `my-tokoFinancialInitialUpdateJob` inactive trên el3-s2 (môi trường, không phải lỗi sản phẩm); phát hiện lỗ hổng data ở pre-check; case bị chặn là Blocked, không Pass; không đề xuất sign-off khi còn case Fail, Blocked hay Not run; không đổi object không tạo cho case. Không access: lên lịch sau khi có access.
**PR-TEC-P4.3-2. Role track exit: tập T4 và T5** (90'; staging; Sub-Lead chọn ticket COEC đã đóng cho mỗi service bạn đã tập và chuẩn bị phiếu T4 replay, phiếu chấm T5; Lead duyệt kết quả). Đây là buổi tập theo format T4 và T5, không phải certification. T4: replay các ticket đã chọn (phân loại, kiểm đầy đủ và câu hỏi, status Jira gồm ON HOLD HQ cho mọi PC, làm trên staging theo runbook kèm bằng chứng, hand-back tiếng Anh). T5 cho một service: phần A thực hành (60'), phần B duyệt runbook, phần C bốn tình huống ngoại lệ. Dùng case book TC-01 (VD A.1) nếu không đủ ticket đã đóng. **Pass:** điểm như bài thật: T4 FPY ≥90% và không lỗi nghiêm trọng; T5 mọi bước đúng và bước critical 100%. Đạt được ghi là role track exit, không phải L1. Sau đó Sub-Lead đặt lịch T4 và T5 cho từng service sau chương trình, và T6 sau L1; chỉ các kết quả đó vào skill matrix là L1 và L2. Fail lần đầu: thêm replay trước khi đặt T4 thật. Không access: lên lịch sau khi có access.
> Material gap: chưa thu thập ticket COEC đã đóng để replay. Tới khi Sub-Lead thu thập, dùng case book TC-01 Phụ lục A (mô phỏng) và ticket lab SCOE-45, SCOE-47, SCOE-48 làm tài liệu replay, và ghi trong skill matrix đã dùng tài liệu nào.
