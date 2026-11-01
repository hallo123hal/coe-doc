# CoE Onboarding Program – Practitioner L2

> Nguồn: Confluence `SamsungCoETech` – page 2483602704 (draft v0.1, cập nhật 26/10/2026).

## Mục đích
Dành cho thành viên Ops CoE (Merchandising, Tech, QA) **đã hoàn thành L1**. L1 dạy "cái gì & ở đâu"; **L2 đào tạo làm việc một mình trong các case thường** (cột Level 2 Practitioner của năng lực CoE C1–C6). Thực hành dùng **CoE Service Pack của 32 dịch vụ ưu tiên** và ticket thực hành trong Jira project **SCOE**, chạy trên dữ liệu thật ở **staging el3-s2**.

> Draft v0.1, chờ Leads và SDM review. Nhiều tài liệu nguồn còn draft/"to be confirmed" (đánh dấu Note box); đáp án "tính bởi tác giả" cần Lead xác nhận.

## Bắt đầu khi nào
- Đã qua mọi quiz L1, Final General test G6.3 và final assessment role.
- Có quyền **Backoffice + HAC staging (el3-s2)** và mở được ticket SCOE.
- Buddy giờ là **Checker**; bạn là **Doer** trong mọi practice ticket. L2 chạy song song với công việc có giám sát; chỉ làm service thật khi đã certified (CM-11).

## Cấu trúc

| Part | Module | Session | Thời lượng |
|---|---|---|---|
| [Part 1 General Practitioner](Part1-General-Practitioner/README.md) | GP1–GP6 | 16 | 990 phút (~16.5h) |
| [Part 2 Merchandising](Part2-Role-Merchandising/README.md) | MER-P1–P4 | 12 | 1065 phút (~17.8h) |
| [Part 2 Tech](Part2-Role-Tech/README.md) | TEC-P1–P4 | 12 | 1065 phút (~17.8h) |
| [Part 2 QA](Part2-Role-QA/README.md) | QA-P1–P3 | 8 | 660 phút (~11h) |

Mỗi learner: Merchandising/Tech ≈ 34h, QA ≈ 27.5h, trong 2–3 tuần.

- **Part 1** (bắt buộc cho cả 3 role) theo một ngày làm việc: nhận ticket → áp dụng KB → chạy ca → change & compliance → giao tiếp → chứng minh qua ca có giám sát.
- **Part 2**: mỗi service session đi qua runbook trong service pack → practice ticket làm một mình trên staging → peer check có evidence → status & SLA clock → rollback.

## Cách học một session
Layout giống L1. Tỷ lệ thời gian: **25% học, 15% demo, 10% quiz, 50% practice**.
- Bắt đầu từ một case (ticket/tình huống/request); đọc link "Read:" để giải case, không đọc trước.
- Là Doer: ghi **before values** trước, để checker so với **after export**, rồi **rollback** cuối bài. Staging el3-s2 dùng chung với BVT và learner khác → chỉ đổi object được giao.
- Quiz đạt **80%**; tiêu chí practice nằm trên trang session.

## Tiêu chí hoàn thành

| Part | Tiêu chí |
|---|---|
| Part 1 | Qua mọi quiz (≥80%); GP6.1 ca giám sát được Shift Leader/Sub-Lead ký; qua GP6.2 (≥80%, đúng hết critical case) |
| Part 2 | Qua mọi quiz + practice của role; qua final role assessment |
| Per service | T4 replay FPY ≥ 90%, không lỗi critical, và qua T5 → certification L1; tuần giám sát (T6) → service L2 (CM-11) |
| Sau chương trình | Lead cập nhật skill matrix |

## Ma trận năng lực (Level 2)

| Năng lực | Phát biểu Level 2 | Dạy ở | Đánh giá ở |
|---|---|---|---|
| C1 Overview & Service Mgmt | Áp dụng SLA clock, priority, các bước quy trình; phân biệt SRM/IM/CM/PM | GP1.1–1.3, GP3.3, GP4.1, TEC-P4.2 | GP6.1, GP6.2 |
| C2 Knowledge Base | Đọc & áp dụng KB cho case chuẩn của stream mình; kiểm tra kết quả | GP2.1–2.2; MER-P1–P3; TEC-P1–P3; QA-P1 | Final role assessment (MER-P4.4, TEC-P4.3, QA-P3.3) |
| C3 CoE ops by role | Chạy ca/duty một mình: handoff, queue scan, dispatch, call tree, on-call, daily report | GP3.1–3.3; MER-P4.1–4.3; TEC-P4.1–4.3; QA-P2.2, P3.1, P3.2 | GP6.1; TEC-P4.2 drill; QA-P3.3 |
| C4 Ticket handling | Xử lý ticket chuẩn với Doer/Checker, evidence, status & SLA đúng | GP1.1–1.3 + mọi service session Part 2 | T4 replay, T5 exam, T6 |
| C5 Compliance | Áp dụng luật trong case thực: xuất data, deadline vs rule, PC ticket & Knox | GP4.1–4.3; MER-P1.3, P2.3, P4.2; TEC-P1.3, P2.1; QA-P3.2 | GP6.2 |
| C6 Individual skills | Viết update/RCA đúng tone; họp tiếng Anh; xử lý hội thoại subsidiary | GP1.4, GP3.2, GP3.3, GP5.1, GP5.2; TEC-P3.1, QA-P2.1 | GP5.2 role-play; GP6.2 writing; T8 |

Exam CT01–CT06 (sheet "4. Capabilities"): GP6.2 phủ CT01, CT05, CT06; final role assessment phủ CT02–CT04 (biến thể M, T, Q).

## Quy tắc khi học & thực hành
- Backoffice/HAC chỉ trên **staging**. HAC chỉ chạy **FlexibleSearch read-only**; ImpEx và Groovy chỉ **Tech**, trên staging, ở session ghi rõ.
- Chỉ đổi object được giao; ghi before; rollback cuối. Object mới đặt tên `TRAINING_<NAME>_<TICKET>_…`.
- Không đưa dữ liệu Samsung ra khỏi hệ thống Samsung; **không đưa vào AI tools**; mask dữ liệu khách hàng trong evidence.
- Hai tài liệu mâu thuẫn → theo **CM-13 RHQ rules** và báo Lead.

## Tài liệu còn thiếu
- Ticket đã đóng cho **T4 replay** (~10/service, từ Samsung Jira, mask PII) – cho MER-P4.4, TEC-P2.3, TEC-P4.3.
- Screenshot AEM, Shop App CMS, BO 2.0 (promotion simulator, Multistore) – cho MER-P3.1, QA-P1.2, QA-P1.3.
- AU staging (el5): ticket TRN-008, 023, 026, 027, 033 chưa gắn data.
- Practice ticket chưa viết: bộ 20 QA check có lỗi gài (QA-P3.3), ticket 3PD và Rewards (TEC-P3.3).
- Tài liệu: BiPlus Security Framework v3; các bậc cao của people-risk ladder (CO-05).
- Quyết định: format thi L2 (đề xuất scenario + staging lab) và tên các level certification (Certified hay Supervised).
