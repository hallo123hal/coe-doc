# QA-3.4 Role track exit: QA final assessment

> Nguồn: page 2483192747 · 80 phút (Study 5' · Demo 5' · Quiz 25' · Practice 45') · Bài test cá nhân gồm trắc nghiệm và một case thực hành trên Backoffice staging, chấm theo rubric; facilitator: QA Lead (chấm) + QA Sub-Lead 2 (chuẩn bị môi trường) · Cần xong QA-1 → QA-3.3; ôn phụ lục câu hỏi của QA-01, QA-02, QA-03 trước khi thi. Cần Backoffice staging + simulator; không có (hoặc simulator không chạy trên S2) thì assessor phát ảnh in của rule và kết quả simulator, làm Part 2 trên giấy theo cùng rubric. Assessor chuẩn bị riêng cho mỗi người rule `TRAINING_FINAL_<số>`, ticket mô phỏng và phiếu chấm có danh sách lỗi cài sẵn (phiếu này không bao giờ đăng lên trang).

## Cấu trúc & điều kiện đạt
- 5 phút đầu đọc hướng dẫn và nhận ticket mô phỏng; **Part 1:** 20 câu trắc nghiệm / 25', 1 điểm/câu; **Part 2:** case thực hành / 45', 10 điểm theo rubric; 5 phút cuối nhận xét nhanh.
- **Đạt:** ≥80% mỗi phần (Part 1 ≥16/20, Part 2 ≥8/10) **và** không có critical error. 80% cùng ngưỡng T3 trong CM-11 §3.2 (24/30).
- **Đây là role track exit cho QA**, không phải L1 certification và không cấp production access. Theo CM-11 §1.3 certification theo từng service: L0 qua T3, L1 qua T4 (replay thực hành) và T5 (exam), L2 qua T6; T7 (phỏng vấn RHQ) áp dụng cho QA Lead và Sub-Lead trước production access.

| Phần bài này | Test Academy gần nhất (CM-11) | Còn cần sau bài này |
|---|---|---|
| Part 1: 20 câu, đạt 80%, 5 câu must-pass | Ngân hàng T3 QA (câu 36–45) và luật RHQ (54–68); T3 là 30 câu / 45', đạt 24 | Thi chính T3 (Day 5) |
| Part 2: một promotion với 5 lỗi cài sẵn | T4 replay task Q-01: 3 lỗi cài sẵn, bỏ sót là critical error | T4: 20 replay check mỗi service, ≥95% chính xác, không critical error |
| Không bao gồm | T5 exam: một check kiểu live (60–90'), runbook walkthrough, tình huống ngoại lệ | T5 theo service; Sub-Lead chấm, Lead duyệt |

## Must-pass và critical error
- **5 câu must-pass ở Part 1:** câu 1 (override), 4 (R3 chờ QA), 9 (hành động sau PASS), 13 (evidence), 18 (scope QA). Sai một câu = Part 1 không đạt.
- **Critical error (rớt ngay):** PASS hoặc "conditional PASS" khi còn lỗi blocking; tự sửa setup; publish live; evidence chứa dữ liệu cá nhân, access code, danh sách coupon code hoặc video; bất kỳ hành động nào trên production.
- Không đạt: ôn lại các session liên quan câu sai, thi lại với bộ câu hỏi và case khác sau ít nhất một buổi ôn. Chưa đạt thì chưa xong QA role track. Đạt cũng không tự cấp level hay production access — đó là T3, T4, T5 theo service.

## Part 2 — môi trường và rubric
Rule `TRAINING_FINAL_<số>` trên Backoffice staging cụm SMS, site `sg` hoặc tương đương, chưa publish live. Ticket mô phỏng có brief đã duyệt, internal check đủ 6 giá trị, comment "Go-live schedule" hai time zone và self-check của Doer. Rule có **5 lỗi cài sẵn**; như T4 task Q-01, bỏ sót lỗi liên quan tiền hoặc thời gian là critical error. 45 phút để đo độ chính xác chứ không đo tốc độ; simulator chậm thì assessor đưa bộ ảnh chuẩn bị sẵn để dựng evidence.

| Tiêu chí Part 2 | Điểm |
|---|---|
| Tìm đúng lỗi cài sẵn (1 điểm/lỗi, tối đa 5) | 5 |
| Đúng defect category + RC code cho các lỗi tìm được | 1 |
| Kết luận và thao tác Jira đúng: FAIL, label `QA_Returned`, STG SETUP, Assignee về Doer, một comment duy nhất, re-check scope | 1 |
| Evidence: cấu trúc template F, Input/Expected/Actual, thấy store + ngày giả lập, tên file chuẩn, <15 MB, không video | 2 |
| Comment tiếng Anh theo template A.4 | 1 |

## Quiz — 20 câu Part 1 và đáp án
1 Merch Lead muốn bỏ qua QA FAIL, ai override → **C: COE Lead, có báo RHQ** (must-pass). 2 Promotion chưa live, QA được làm gì → **A: đọc field và chạy simulator**. 3 QA due time → **D: sớm nhất của OLA, luật 25%, go-live − 1h**. 4 R3 sắp breach SLA, chưa có PASS, không phải last-minute → **B: vẫn chờ QA PASS, leo thang ở 70/85/95%** (must-pass). 5 Price file 45 SKU không E4 → n = **A: 30 + mandatory set**. 6 N'=150, n=30 → k = **C: 5**. 7 Ticket thiếu comment "Go-live schedule" (QCL-00 dòng 0.3) → **B: không kiểm, trả STG SETUP `RC-EVD`**. 8 Brief "10% off accessories" nhưng file SKU có 2 tablet → **D: QUESTION, Doer hỏi subsidiary** (A.5, brief không rõ không tính FAIL của Doer). 9 Sau PASS ticket ở đâu, ai chuyển → **B: ở QA REVIEW; Shift Leader duyệt và chuyển PRD SETUP** (must-pass). 10 Coupon 25 USD × 500 → **C: R3 ở E4, exposure 12,500 USD**. 11 Promotion hết 07-Dec 23:59 SGT, negative test thời gian → **A: 08-Dec 00:00 SGT**. 12 Cross-check N/A → **D: kiểm filter site/date và ký hiệu `$` trước**. 13 Lưu/gửi evidence → **D: PowerPoint dựng trên CoE PC, đính Jira, rồi xóa** (must-pass). 14 Khách EPP không thấy payment mode của Base Store → **B: multistore có danh sách payment mode riêng**. 15 Promotion chỉ cho nhóm "VIP_TEST" → **A: thử account trong và ngoài nhóm**. 16 Doer có 2 QA FAIL tính trong tháng → **C: QA Sub-Lead báo Shift Leader cùng ngày**. 17 Wave 2/3 QA again pass → **C: "Go-live batch 2/3 QA re-check", ticket ở PENDING LAUNCH**. 18 Việc thuộc scope QA sau 21/10/2026 → **A: QA REVIEW ticket Merch, QA again mỗi go-live** (must-pass). 19 Go-live 00:00 ngày mai, đã PASS + Shift Leader duyệt, ở REVIEW SETUP, 23:59 subsidiary chưa duyệt → **C: publish đúng giờ như đã hẹn, comment, QA again lúc go-live**. 20 Setup còn trong tester group, Merch nhờ QA gỡ restriction → **B: không gỡ; subsidiary phải xác nhận trước**.

## Practice
**PR-QA3.4-1** (45'; Backoffice staging, Confluence nháp, CoE workstation): ticket mô phỏng `DEMO-QA-FIN` (SG, R3, Medium). Brief v2 đã duyệt: giảm 15% cho 4 SKU `DEMO-SKU-101…104` (gồm 2 biến thể màu), 01-Dec-2026 00:00 → 07-Dec-2026 23:59 SGT, chỉ SG B2C, không stacking với promotion khác, giới hạn 1 lần/khách; internal check của Doer khớp brief. Việc: (1) chấm nhanh QCL-00; (2) BO-1, BO-2, BO-3 trên rule `TRAINING_FINAL_<số>`; (3) chạy ít nhất T1–T7 và test giới hạn per-customer; (4) viết **một** comment FAIL tiếng Anh theo A.4 liệt kê mọi lỗi với category, RC code và re-check scope; (5) dựng evidence template F (slide 1 liệt kê mọi lỗi, rồi mỗi lỗi một slide Expected/Actual) tên `DEMO-QA-FIN_QA_check1_FAIL.pptx`, <15 MB, rồi xóa bản local; (6) viết các thao tác Jira sẽ làm. **Pass:** ≥8/10 theo rubric, kết luận FAIL, không critical error, và tìm đủ mọi lỗi liên quan tiền/thời gian trên phiếu chấm. Không có access: assessor phát ảnh 3 tab của rule + kết quả 8 test run; vẫn viết comment và dựng evidence từ ảnh.
