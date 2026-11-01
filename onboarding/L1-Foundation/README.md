# CoE Onboarding Program – Foundation L1

> Nguồn: Confluence `SamsungCoETech` – page 2482896912. Tổng hợp từ trang gốc (cập nhật 01/11/2026).

## Mục đích
Chương trình onboarding cho mọi thành viên mới của **Ops CoE** (Merchandising, Tech, QA). Gồm 3 cluster: **C1 + C2 = General foundation** (ai cũng học), **C3 = role path** của team mình. Mỗi trang session có cùng 8 phần: *Before you start, New terms, Learning objectives, Lesson, Study materials, Quiz, Completion checklist, Practice*.

Quy tắc vận hành lấy từ các tài liệu **CM-01 → CM-13** (CoE Overview). Khi trang L1 và CM mâu thuẫn → **CM đúng**, và **CM-13 (RHQ Rules) thắng** các CM khác; báo CoE Office.

## Cấu trúc

| Cluster | Module | Số session | Thời lượng | Nguồn CM chính |
|---|---|---|---|---|
| [C1 Overview & Service Management](C1-Overview-and-Service-Management/README.md) | G1 Orientation, G2 Service Management | 11 | 615 phút (~10.3h) | CM-01,02,03,04,06,07,08,09,10,13 |
| [C2 Knowledge Base](C2-Knowledge-Base/README.md) | G3, G4, G5, G6 | 12 | 645 phút (~10.8h) | SEAO textbook, CM-09,10,11,12,13 |
| [C3 CoE operations by role](C3-CoE-Operations-by-Role/README.md) | Merchandising (13 session, 925 phút), Tech (12, 870 phút), QA (11, 845 phút) | 11–13 | 14–15.5h | Mer: CM-05,07,12,13 + MR-xx; Tech: CM-06,08,12,13 + TC-xx; QA: CM-04,05,06,13 + QA-xx |

Tổng: ~21h cho C1+C2, + 14–15.5h role path (giờ lớp, chưa tính đọc CM ngoài giờ và chờ cấp quyền hệ thống).

## Lộ trình học
1. **G1 Orientation** – Samsung SEAO, CoE, RHQ rules, bảo mật. **Phải qua lesson T1 (G1.3) và ký cam kết bảo mật trước khi có quyền hệ thống.**
2. **G2 Service Management** – loại công việc, workflow Jira, SLA, ca trực, incident, change control, escalation, tools. Dùng 1 ticket mô phỏng **DEMO-8101** xuyên suốt.
3. **G3–G5** – sản phẩm, giá, tồn kho, promotion, order, kênh bán, 8 thị trường; thực hành Backoffice và HAC (staging).
4. **G6** – Knowledge, BVT, bài **Final General test** (25 câu, đạt ≥ 20) trước khi bắt đầu C3.
5. **C3** – role path (Merchandising / Tech / QA), kết thúc bằng *role track exit*.

Module đánh số theo thứ tự học; session chỉ dựa vào session trước nó.

## Đánh giá & chứng nhận

| Bước | Ở đâu | Chứng minh |
|---|---|---|
| Session quiz | Mọi session | Tự kiểm tra; mỗi đáp án có giải thích + mục CM cần đọc lại |
| Lesson T1 | G1.3 | Quy tắc an toàn thông tin (CM-10); bắt buộc trước khi có quyền hệ thống |
| Final General test | G6.3 | Được vào role path; 25 câu, đạt 20 |
| Role track exit | MER-3.4, TEC-4.2, QA-3.4 | Hoàn thành role path; Tech có thêm incident drill chấm điểm |
| L1 certification per service | CM-11 (T4 replay, T5 practical) – ngoài L1 Foundation | Được làm service đó cùng checker; production cần thêm T7 (phỏng vấn RHQ) |

Role track exit **không phải** L1 certification; chỉ người đã certified service mới được xử lý ticket thật (CM-11 §1.3).

## Cách dùng
- **Learner:** theo lộ trình, không bỏ quiz/practice (bài test cuối dùng lại).
- **Lead/buddy:** kiểm tra completion checklist + kết quả T1, G6.3, role track exit trước khi học viên đi tiếp.
- **Facilitator:** chuẩn bị data/account staging ở mục *Before you start*; đáp án/agenda để trên trang session.

## Open points cần chốt trước cohort sau
| Vấn đề | Ai quyết | Session |
|---|---|---|
| Mọi promotion đều cần Knox (kể cả free-gift, non-discount); một số KB nói khác | RHQ | G2.6, G3.4, G6.2, MER-1.3, MER-2.3, Glossary |
| CM-13 §4.6 (quét COEC ngoài giờ), §11.1 (email domain) mâu thuẫn CM khác; CM-13 §8.2 vs CM-07 §3.6 về kiểm soát last-minute | CM owner (CoE Office) | G1.3, G2.4, TEC-1.4, MER-3.2 |
| Ai được báo khi ticket bị QA trả lại lần 2 (CM-03/05/07 nêu người khác nhau) | CoE Office | MER-3.1, QA-1.2 |
| NZ system cluster, vị trí simulator trên staging, quyền staging cho sync/preview, giới hạn multi-coupon, ngưỡng fraud score | Merchandising & Tech Leads | G3.2, G3.4, G4.3, MER-2.x |
| Giờ ca QA (deck v08Oct hay proposal v9.4) | CEO | QA-3.2 |
| Một số hình còn theo flow cũ (MER-3.4, TEC-4.1, TEC-4.2, QA-1.2, QA-3.4) | Course owner | như liệt kê |
| G6.3 mới cần bài retake tương ứng | Academy | G6.3 |

## Change log (01/11/2026)
Review toàn bộ trang L1 so với CM-01..13; đánh số lại module G1–G6 theo thứ tự học (Service Management là G2); thay transcript/screenshot KT bằng bảng "What the Samsung KT session said"; thêm MER-1.4 Intake duty, QA-3.2 QA on shift, incident drill trong TEC-4.2; đổi tên role final test thành role track exit; sửa link textbook SEAO.
