# QA-2.4 Negative testing, evidence and QA return

> Nguồn: page 2483389134 · 70 phút (Study 15' · Demo/thảo luận 5' · Quiz 10' · Practice 40') · Facilitator cho xem file evidence mẫu, học viên tự dựng rồi review chéo theo cặp; facilitator: QA Lead · Cần xong PR-QA2.1-2 (giữ ảnh chụp trong thư mục tạm trên CoE workstation, không có thì dùng bộ ảnh dự phòng), G1.3 (information security), QA-1.2 (A.3, A.4, RC code); cần PowerPoint + template evidence QA-03; chỉ đính lên Jira khi Lead chỉ định ticket training, còn lại dựng xong xóa sau buổi.

## Mục tiêu
Thiết kế bộ test positive/negative/exploratory cho promotion chưa gặp; dựng evidence pack đúng CM-13 và QA-03 (đúng template, đúng tên, ≤15 MB, không video, xóa bản local); viết comment PASS (A.3) và FAIL (A.4) kèm evidence; phân biệt QA_Returned (lỗi Doer) với QA Defect và escaped defect (lỗi QA/CoE).

## Thuật ngữ
**Evidence pack** (file PowerPoint chứng minh từng bước QA đã làm, đính vào Jira comment); **Templates P, F, G** (P cho promotion 8 slide, F cho FAIL, G cho QA again khi go-live; còn R, V, A, D, C, S); **Input / Expected / Actual** (3 dòng chú thích mỗi ảnh); **QA record** (comment kết quả QA + file evidence); **QA Defect** (lỗi của QA: báo lỗi khi setup đúng, hoặc bỏ sót lỗi khi setup sai); **"One return, all errors"** (mỗi lần trả liệt kê hết lỗi).

## Nội dung
### 1. Ba loại test và "một lần trả, mọi lỗi"
Mỗi promotion cần: **Positive** (cart đủ điều kiện, gồm cả sát giới hạn); **Negative** (dưới ngưỡng, SKU ngoài danh sách, store/customer group không quyền, ngoài khung giờ); **Exploratory** (stacking với promotion đang chạy, time zone, banner khớp cơ chế, mobile view). Lỗi người mới hay gặp: chỉ test cart đủ điều kiện; chọn sai store; chỉ so brief mà quên internal check; kiểm những SKU đầu file thay vì mẫu chọn theo luật. FAIL dùng A.4, mỗi lỗi một category + một RC chính. Mỗi vòng trả tốn ~1–3 giờ SLA, trả thiếu lỗi làm ticket chậm gấp đôi.

### 2. Lỗi của Doer và lỗi của QA
`QA_Returned` = lỗi Doer mà QA bắt được. **QA Defect** = lỗi QA (báo sai hoặc bỏ sót). Lỗi lọt lên production sau QA PASS = **escaped defect** (G2.1); sau mỗi escaped defect, checklist phải có thêm dòng blocking trong 3 ngày làm việc sau RCA.

### 3. Luật evidence của RHQ (CM-13 ch.6)
File PowerPoint có ảnh chụp từng bước, đính vào Jira comment; Jira tối đa 15 MB/file, **không video**; chỉ dựng trên CoE workstation trong khu vực bảo mật; **không ảnh chụp bằng điện thoại**; không gửi qua Mattermost, email, chat; không lưu trên hệ thống BiPlus; không đưa vào công cụ AI. Không bao giờ để lộ trong ảnh: dữ liệu cá nhân khách chưa che, mật khẩu, access code, danh sách coupon code, cửa sổ ứng dụng khác. Chỉ được thêm khung, mũi tên, che; không chỉnh sửa làm đổi nội dung.

### 4. Dựng file: template P và tên file
Slide 1 là kết luận (ticket, market, cơ chế, giờ hai time zone, số lần check, kết quả, Checker, checklist + version); mỗi slide chứng minh một ý và tiêu đề là câu kết luận; mỗi ảnh có Input/Expected/Actual, khung đỏ quanh field chính, thấy site/store/ngày giả lập; tiếng Anh, 6–12 slide. Template F cho FAIL: slide 1 liệt kê mọi lỗi, rồi mỗi lỗi một slide Expected/Actual.
**Tên file:** `{ticket}_QA_check{n}_{PASS|FAIL}.pptx` (VD `DEMO-2701_QA_check2_PASS.pptx`); QA again lúc go-live: `{ticket}_GL_batch{n}.pptx`.

| Slide (template P) | Tiêu đề mẫu | Ảnh cần |
|---|---|---|
| 1 Summary | DEMO-2701 VN 10% off 2 SKUs: PASS, check 1 | Bảng thông tin ticket |
| 2 Configuration | Rule values match the internal check | Properties, Conditions, Actions có khung đỏ |
| 3 Not live yet | Rule is not published live | Publish status của rule |
| 4 Eligible case | 1 × SKU-A gets 10% off | Simulator T1, T2 |
| 5 Not eligible cases | No discount outside SKU list, store or period | Simulator T3–T6 |
| 6 Interaction | Stacking with SKU-D promotion follows the brief | Simulator T7 |
| 7 Price proof | Final price equals calculation | Bảng giá tự tính so simulator |
| 8 Conclusion | All checklist items passed | Checklist, version, số dòng N/A, SKU coverage |

### 5. Lưu, xóa và viết comment
7 bước: (1) mở template; (2) chụp bằng tool được duyệt, lưu thư mục tạm; (3) dựng slide; (4) đính file vào QA record comment; (5) mở lại file từ Jira để kiểm; (6) xóa file và ảnh tạm, cả trong recycle bin; (7) hoàn tất comment.
Comment A.3 mẫu: `QA result: PASS (check 1). Checker: Chi. Reviewed by: An. Depth normal: 2 of 2 SKUs. Checked on staging, not live, with the promotion simulator: positive, negative and exploratory tests passed. Setup matches the approved brief and the internal check. Evidence: TRAINING-QA-01_QA_check1_PASS.pptx. Checklist: QCL-PRM-01 v1.0, 18 items checked, 2 N/A with reasons. Ready for Shift Leader approval.` Thực tế "staging" thành "production, not live".

## Quiz (đáp án)
1 Evidence batch promotion >15 MB → **D: nén, tách file <15 MB, đính Jira** (không video, không kênh khác). 2 3 lỗi trong check 1 → **A: một comment FAIL với cả 3 lỗi, category + RC**. 3 Slide đạt chuẩn → **C: tiêu đề kết luận, khung đỏ, Input/Expected/Actual**. 4 QA PASS nhưng bỏ sót lỗi, lên production sai → **B: QA Defect và escaped defect**. 5 Tên file check 2 PASS của DEMO-2701 → **D: `DEMO-2701_QA_check2_PASS.pptx`**. 6 Tiered tối đa 10%, cart trên tier cao nhất → **A: chỉ 10%**. 7 Brief duyệt sai giá, Doer build đúng brief, internal check khớp brief → **C: `RC-BRF`** (không tính là Doer return). 8 Run exploratory cho 10% off Galaxy Watch → **C: Watch đang có bundle promotion khác** (A là positive; B, D là negative).

## Practice
- **PR-QA2.4-1** (25'): dùng ảnh PR-QA2.1-2 dựng file template P 8 slide, đặt tên `TRAINING-QA-<tên>_QA_check1_<PASS|FAIL>.pptx`, viết comment A.3 hoặc A.4 theo mẫu; có ticket training thì đính vào comment và mở lại từ Jira; cuối cùng xóa file + ảnh tạm kể cả recycle bin. Bạn cùng cặp chấm bằng 5 ô "Before attaching the evidence file" của QA-03. Pass: slide 1 đủ thông tin kết luận; mỗi ảnh có Input/Expected/Actual + khung đỏ, thấy store và ngày giả lập; không có dữ liệu cá nhân, mật khẩu, access code, danh sách code; file <15 MB, tiếng Anh; không còn bản nào trên máy.
- **PR-QA2.4-2** (15', giấy): promotion "BMSM MY: mua 2 giảm 5%, mua ≥3 giảm 10%, tối đa 4 unit, cho Galaxy Buds và Watch, 15–20/12/2026 giờ MY, B2C". Viết ≥12 test run (input + expected): negative/giới hạn — dưới ngưỡng, đúng mỗi tier, trên tier cao nhất, vượt số lượng tối đa, cart lẫn SKU không đủ điều kiện, EPP store, 1 phút trước start, 1 phút sau end; positive — 2 Galaxy Buds; 1 Buds + 2 Watch; exploratory — cùng cart với Watch đang có promotion khác (stacking), cart và banner trên mobile view. Pass: đủ 12 run, 2 run exploratory đối chiếu internal check; expected đúng (1 món không giảm; trên tier cao nhất vẫn 10%; unit thứ 5 không giảm; EPP không áp); giờ ghi cả giờ MY và ICT (giờ MY − 1).
