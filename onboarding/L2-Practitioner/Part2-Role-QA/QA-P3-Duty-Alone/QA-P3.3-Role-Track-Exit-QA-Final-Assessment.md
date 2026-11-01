# QA-P3.3 Role track exit: QA final assessment

> Nguồn: page 2484077014 · 120' (Study 30' · Demo 20' · Quiz 10' · Practice 60') · Facilitator: QA Lead · Capability C4 · Cần xong QA-3.4 (L1) và mọi session QA-P trước (checklist và sampling QA-P1/P2.2, return và RC code QA-P2.1, dispatch và due time QA-P3.1, cao điểm và ranh giới QA-P3.2); phải đã qua T3 (quiz nền tảng 80%) cho track Q. Session này là **role track exit** của lộ trình L2 QA: 20 check rút từ các service QA-P1, không từ một service. Certification riêng: T4 và T5 **theo từng service** sau khoá học, T6 tuần giám sát QA sau chương trình. Access: Backoffice staging el3-s2, promotion simulator, storefront staging, Jira SCOE, Confluence (read), workstation CoE ở khu làm việc an toàn để làm bằng chứng; QA không có HAC (cần query thì trainer đưa output). Không có access staging thì không thi được: QA Lead lên lịch sau khi cấp access; trong lúc đó làm lại case book QA-01 Phụ lục A trên giấy.

## Mục tiêu
Giải thích format, điểm đạt và lỗi nghiêm trọng của 20 check exit, và T4, T5, T6 theo từng service nối tiếp sau khoá học; tính một kết quả có đạt không: 19/20 check đúng và không lỗi nghiêm trọng; nói điều gì xảy ra sau fail lần một, lần hai, và được làm gì sau khi đạt; qua 20 check exit ≥95% không miss nghiêm trọng.

## Thuật ngữ
**Certification per service** (level giữ theo service trong catalogue, không theo người: có thể L2 special price và L1 promotion cùng lúc); **L0, L1, L2, L3** (Trained (qua T3, chỉ tập); Certified (qua T4 và T5, ticket live với 100% output được kiểm); Independent (qua T6); Coach (4 tuần live đạt target)); **Role track exit** (session cuối lộ trình L2 QA: 20 check qua các service QA-P1 trên staging, độ chính xác ≥95%, không lỗi nghiêm trọng; đóng khoá học, không cert service nào); **T4 practical replay** (ticket đã đóng hoặc chuẩn bị làm lại trên staging; với QA là 20 check có lỗi cài sẵn); **T5 certification exam** (bài thi lên L1 cho một service: thực hành, duyệt runbook, tình huống ngoại lệ); **Critical error** (lỗi tự nó làm fail bài, VD miss lỗi cài sẵn hay ghi PASS không bằng chứng); **Skill matrix** (hồ sơ Confluence về level mỗi người theo service, RHQ xem được; kết quả T5 ghi ở đây); **Retake** (lần thi thứ hai sau fail: T4 trong 2 ngày làm việc sau thêm replay; T5 sau coaching).

## Nội dung
### 1. Role track exit nằm ở đâu
Role track exit đóng khoá học. Certification chạy theo service trên thang Academy: sau khoá học bạn thi T4 và T5 cho mỗi service sẽ làm (L1 Certified), rồi một tuần QA giám sát (T6) trên queue live cho L2 Independent. QA Lead đặt lịch T4 và T5 theo service trong lịch Academy; không thuộc session này.
Thang Academy có tám bài T1-T8 và bốn level mỗi service. QA Team Member thi T1-T6; QA Sub-Lead thi thêm T7 (phỏng vấn RHQ).
| Level | Được làm gì | Đạt bằng |
|---|---|---|
| L0 Trained | Chỉ tập trên staging và replay; không ticket live | T3 |
| L1 Certified | Ticket live; 100% output được kiểm trước production; PASS của QA L1 được L2, L3 hay Sub-Lead review | T4 và T5, theo service, sau khoá học |
| L2 Independent | Làm service một mình trong các gate bình thường | T6 tuần QA giám sát, sau chương trình |
| L3 Coach | Đào tạo và chấm người khác | 4 tuần live đạt target; Lead quyết |
**Không cert nghĩa là không truy cập production.** Access cấp theo đợt sau cert (29/10, 6/11, 13/11, 20/11). Người dưới điểm đạt không bao giờ làm service một mình. Làm service chưa cert gây incident là một trong ba hành động luôn bị RHQ strike. Lịch 3 tuần chuẩn: T4 ngày 7-10, T5 ngày 11-12. Cohort 0 nén: W1 thi T5 ngày 31/10, W2 ngày 7/11, và service promotion, price chỉ giao cho người đã qua T5 đúng service đó.
> QA-01 §2.5 gọi 20 check là "track Q final test" và CM-11 xếp replay kiểu này dưới T4. Trong khoá học này 20 check trộn nhiều service, làm role track exit; không thay T4 của service nào. CM-11 cũng ghi dashboard v1.4 gọi L1 "Supervised" và L2 "Certified"; quyền mỗi level như nhau. CEO quyết một bộ tên.

### 2. Bài exit: 20 check
**Cách chạy.** Sub-Lead chuẩn bị ticket các service QA-P1 trên staging Samsung (product, stock, price, promotion, coupon, content), ít nhất một check mỗi nhóm service, ưu tiên bẫy phổ biến: thiếu thông tin, múi giờ, giá bất thường, nhiều market. Trainer cài lỗi vào setup. Mỗi ticket bạn làm như ca thật: kiểm data đủ chưa, chọn mẫu SKU, test (positive, negative, exploratory), trả PASS, FAIL hay QUESTION kèm QA record và bằng chứng.
**Điểm đạt.** 20 check với **độ chính xác ≥95%**: tối đa một check sai, và **không lỗi nghiêm trọng**.
**Lỗi nghiêm trọng của QA** (một lỗi fail cả bài): miss lỗi cài sẵn (CM-11 task mẫu Q-01: "miss bất kỳ một lỗi nào là lỗi nghiêm trọng"); ghi PASS khi chưa check hay không bằng chứng; tự sửa setup; bỏ QA trên việc có gate mà không có quyết định Shift Leader theo luật yêu cầu gấp; chụp màn hình bằng điện thoại hay gửi bằng chứng qua kênh khác; hỏi trực tiếp subsidiary thay vì qua Doer; thao tác production hay chuyển data ra ngoài hệ thống Samsung; tự chạy query HAC hay nhờ Tech query ngoài COEC liên kết; test biên promotion trong simulator mà không đổi giờ market sang GMT+8.
**Check mẫu Q-01 (CM-11, mô phỏng).** Brief TH: mua 1 `DEMO-P1` tặng `DEMO-C1`; 20/11 00:00 tới 22/11 23:59 giờ Bangkok; chỉ B2C; loại `DEMO-P9`; 1 quà mỗi order. Lỗi cài: end time theo giờ Singapore (kết thúc sớm 1 giờ); `DEMO-P9` không bị loại; bao cả nhóm EPP. Kết quả đúng: một FAIL ba dòng, mỗi dòng có bằng chứng; giới hạn quà ghi là pass; simulator cho thấy quà được thêm và gỡ cùng `DEMO-P1`.
**Người chấm nhìn gì trong mỗi check:** quyết định data đủ; mẫu (N, n, k, s và mandatory set); mọi lỗi cài đã tìm ra; category và mã RC đúng; một return gộp; status và Assignee đúng (status sau PASS chưa chấm tới khi quyết D5); bằng chứng làm trên workstation CoE, đính kèm, xoá bản local.
> CM-11 không định nghĩa "95% accuracy" đếm thế nào (theo check hay theo mục checklist). Khoá học đọc là số check đúng trên 20, nên 19/20 đạt và 18/20 fail. Xác nhận với QA Lead trước khi thi.

### 3. Sau khoá học: T4 và T5 theo service
T4 là practical replay ticket đã đóng hay chuẩn bị của một service. T5 là bài thi cert của service đó. Qua cả hai là L1 Certified chỉ trên service đó. T5 thi **theo service**; Sub-Lead chấm, Lead duyệt, kết quả vào skill matrix trên Confluence Samsung, nơi RHQ xem được.
| Phần | Nội dung | Thời lượng (đề xuất) | Chấm |
|---|---|---|---|
| A. Thực hành | Một ticket của service trên staging theo runbook, có bằng chứng | 60-90' | Từng bước; bước critical 100% |
| B. Duyệt runbook | Giải thích từng bước, điểm kiểm soát, lý do; trả lời "what if…" | 20-30' | Mọi bước đúng |
| C. Tình huống ngoại lệ | 4 câu: thiếu thông tin; phối hợp hay duyệt; ticket ở cảnh báo 70%; dấu hiệu incident | 20' | Đúng hành động, người, status Jira, giờ |
| D. Giao tiếp | Hand-back hay câu hỏi bằng tiếng Anh | 10' | Rubric T2 (liệt kê cho Merch và Market Owner) |
**Với QA, phần C nghĩa là ví dụ:** ticket ở QA REVIEW không có comment internal check (trả `RC-EVD` và gặp Doer); ticket coupon có code do Tech tạo dưới COEC liên kết (QA chỉ check setup Merch, không check ImpEx); ticket ở QA REVIEW chạm 70% (báo Shift Leader trong 15 phút); thấy giá sai trên site live lúc QA again (báo Shift Leader ngay; không sửa; incident nếu liên quan tiền). **Hàng chấm critical:** phân loại và mức rủi ro; internal check (R3); phối hợp và duyệt; dấu hiệu incident. Kết luận **Pass chỉ khi mọi bước đúng và bước critical 100%**.
> CM-11 xếp T4 ở ngày 7-10 và T5 ngày 11-12, và riêng T5 mất 100-140 phút mỗi service. Đó là lý do T4, T5 chạy theo service trong lịch Academy chứ không trong session này. QA có thi phần D không chưa nêu.

### 4. Đạt, fail và thi lại
| Bài | Ai chấm | Fail lần 1 | Fail lần 2 |
|---|---|---|---|
| T4 (theo service) | Sub-Lead | Thêm replay; thi lại trong 2 ngày làm việc | Giao service rủi ro thấp hơn; bench hoặc ứng viên thứ hai thay |
| T5 | Sub-Lead chấm, Lead duyệt | Thi lại sau coaching | Như T4 |
| T6 | Lead và SDM | Thêm một tuần giám sát | Rời queue; bench thay; tier L2 của people-risk ladder |
Điểm đạt do BiPlus đề xuất để thống nhất với RHQ.
**Sau khi đạt (L1):** nhận ticket live của service đó; mọi PASS bạn đưa được L2, L3 hay Sub-Lead review trước khi trả, kèm tên người review trong QA record. Trong re-check 5% hằng tuần của QA Lead, người cert dưới 4 tuần được lấy mẫu trước.
**Lên L2 (T6), sau chương trình:** khi đã L1 trên service, một tuần giám sát trên queue QA live với first-pass yield ≥90% tháng 11 và 95% từ tháng 12, không lỗi nghiêm trọng, đạt target phản hồi, handoff note đầy đủ, không tin nhắn bị chặn vì sai thông tin. Lead và SDM ký.
**Giữ level:** khi runbook đổi, người đã cert được recertify. QA miss lặp lại dẫn tới coaching và recertify.

### 5. Chuẩn bị: câu hỏi đằng sau mỗi check
Trước mỗi check tự hỏi cùng câu người chấm hỏi: 1) **Data đủ chưa?** Brief, file SKU (diff file >100 dòng), giờ go-live ở cả hai múi giờ, internal check của Doer viết trước khi build. Không đủ: một return A.2 với `RC-EVD`. 2) **Mẫu đúng chưa?** Tất cả SKU tới 30; còn lại n cộng mandatory set; ghi N, n, k, s. 3) **Đã test đủ ba loại?** Positive, negative (ngay dưới ngưỡng, SKU ngoài list, sai store hay group, ngày ngoài kỳ hạn), exploratory (stacking, múi giờ của ngày end, banner). 4) **Return đã gộp?** Một comment, mọi defect kèm category, mã RC, giá trị kỳ vọng và thực tế, và re-check scope. 5) **Bằng chứng an toàn?** PowerPoint screenshot trên workstation CoE, đính Jira, xoá bản local; không điện thoại, không video, không kênh khác. 6) **Trong ranh giới?** Không sửa, không publish, không order thật, không BVT, không ImpEx Tech.
Handover liên quan: Working Session P1 (23/10: QA REVIEW, REVIEW SETUP, PENDING LAUNCH, ma trận QA review; xem lại trước bài exit).

## Quiz (đáp án)
1 Trong 20 check bạn đúng 19; ở check sai bạn miss một trong ba lỗi cài sẵn; đạt không → **B: Không: miss lỗi cài sẵn là lỗi nghiêm trọng**. 2 Hôm qua qua T5 special price; hôm nay ticket coupon trong queue và không ai rảnh; được check không → **C: Không: cert theo service; check service chưa cert gây incident bị strike**. 3 Thấy end time promotion lệch một giờ; để tiết kiệm thời gian cho Doer bạn sửa trong Back Office và ghi PASS; ảnh hưởng tới bài → **C: lỗi nghiêm trọng: QA không bao giờ sửa setup**. 4 Fail T5 promotion lần đầu vào thứ Sáu → **B: thi lại sau coaching** ("trong 2 ngày làm việc" là luật T4). 5 Ticket 45 SKU; bạn check 30 SKU ngẫu nhiên nhưng quên SKU giá thấp nhất, kết quả cuối đúng → **B: lỗi quy trình: mandatory set gồm giá cao nhất và thấp nhất**. 6 T5 phần C: ticket ở QA REVIEW chạm cảnh báo SLA 70%; câu trả lời ăn điểm → **C: báo Shift Leader trong 15 phút kèm giờ dự kiến có kết quả**. 7 Sau khi qua T4 và T5 (L1), PASS của bạn khác gì → **B: L2, L3 hay Sub-Lead review mỗi PASS trước khi trả, ghi tên người review trong QA record**. 8 Ngày thi bạn không có access staging → **C: lên lịch sau khi cấp access; trong lúc đó tập trên giấy**.

## Practice
**PR-QA-P3.3-1. Role track exit: QA final assessment** (60' trong session; staging el3-s2 (Backoffice, promotion simulator, storefront; không HAC), Jira SCOE, workstation CoE; nếu 20 check không vừa, QA Lead chạy phần còn lại trong lần ngồi thứ hai cùng tuần; người chấm: QA Sub-Lead; duyệt: QA Lead). 20 check qua các service QA-P1 với lỗi cài sẵn: mỗi cái quyết data đủ, ghi mẫu, test, trả PASS, FAIL hay QUESTION kèm QA record và bằng chứng. T5 không thuộc session này. **Pass:** ≥19/20 check đúng; mọi lỗi cài sẵn được tìm (không miss); không lỗi nghiêm trọng trong danh sách mục 2; mỗi FAIL là một comment gộp có category, mã RC, giá trị kỳ vọng và thực tế; bằng chứng đính ticket và xoá bản local. Kết quả ghi là "L2 QA role track exit passed" kèm ngày; không cấp level service nào. Tiếp theo: T4 và T5 theo service trong lịch Academy, rồi T6 tuần QA giám sát sau chương trình, QA Lead và SDM ký. Không access: lên lịch sau khi cấp access staging; trong lúc đó làm case book QA-01 case 1, 2, 7, 8 trên giấy và so với Phụ lục B (đạt: 8/10 điểm mỗi case và không lỗi nghiêm trọng).
> Material gap: bộ 20 check có lỗi cài sẵn chưa được viết. Tới khi có, QA Lead có thể dựng từ ticket lab đã dùng ở QA-P1 và QA-P2 (VD TRN-024, TRN-034) bằng cách cài lỗi vào object staging chỉ có tiền tố `TRAINING_`; đây là gợi ý của tác giả khoá học, không phải luật nguồn.
