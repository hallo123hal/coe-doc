# Tài liệu chung CM – Ops CoE (Samsung SEAO) – bản tóm tắt

Tóm tắt từ trang Confluence "Tài liệu chung (CM)" (https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2478375074) và 12 trang con. Mỗi trang con = một file. Tất cả nguồn là **bản nháp** (v0.2; CM-12 v0.1, 21/10/2026), ví dụ dùng dữ liệu giả lập. Các file tóm tắt giữ lại số liệu, quy tắc, mẫu và điểm "chờ RHQ/CEO chốt"; muốn đọc chi tiết từng câu hỏi/bài tập hãy xem trang gốc.

| Mã | File | Nội dung chính | Người đọc |
|---|---|---|---|
| CM-01 | [CM-01-welcome-pack.md](CM-01-welcome-pack.md) | Samsung SEAO/RHQ/8 subsidiary, nền tảng Hybris–AEM–Shop App, 3 trụ, tổ chức 56 người, lộ trình đến takeover 30/11/2026, cam kết SLA, một ngày ở CoE, 10 quy tắc vàng | Toàn đội |
| CM-02 | [CM-02-service-management.md](CM-02-service-management.md) | Khái niệm ITIL, 4 loại việc, vòng đời ticket & trạng thái, priority, SLA/OLA/KPI, Doer–Checker–Approver, catalogue 143 service, cải tiến liên tục | Toàn đội, bench, người mới Academy |
| CM-03 | [CM-03-sla-handbook.md](CM-03-sla-handbook.md) | SLA RFP 3.3, Composite & khấu trừ, đồng hồ SLA theo trạng thái, phản hồi đầu, ngân sách thời gian, cảnh báo 50/70/85/95%, filter/dashboard, báo cáo | Toàn đội |
| CM-04 | [CM-04-shift-handbook.md](CM-04-shift-handbook.md) | Ca 24/7 (N/D/E, Tech L1/L2, QA), quân số, vai trò trong ca, stand-up, handoff note, vắng mặt, ca đêm, peak/lễ | Toàn đội |
| CM-05 | [CM-05-service-request.md](CM-05-service-request.md) | Luồng Service Request 9 bước (B1–B9), tiếp nhận, phân loại, hỏi subsidiary, QA/duyệt/PC ticket, hand-back, ánh xạ trạng thái Jira | Toàn đội |
| CM-06 | [CM-06-incident-oncall.md](CM-06-incident-oncall.md) | Severity matrix, 9 bước I1–I9, Incident Manager, on-call, bridge, mẫu thông báo RHQ, playbook sai giá/khách không đặt hàng, known error, diễn tập | Toàn đội |
| CM-07 | [CM-07-change-problem-cai-tien.md](CM-07-change-problem-cai-tien.md) | R1/R2/R3 + E4, cổng kiểm soát, PC ticket, price sanity/read-back, rollback, freeze/peak, Problem, RCA/CAPA, knowledge base & SRL, cải tiến | Toàn đội, Shift Leader, Lead, CoE Office |
| CM-08 | [CM-08-leo-thang-giao-tiep.md](CM-08-leo-thang-giao-tiep.md) | Ma trận leo thang, contact card, kênh giao tiếp, 18 mẫu tiếng Anh, tiếng Thái/Bahasa, duyệt tin người mới, họp RHQ | Toàn đội |
| CM-09 | [CM-09-cong-cu-samsung.md](CM-09-cong-cu-samsung.md) | Tài khoản/MFA, Jira (project, trường, workflow, dashboard, JQL filter), Confluence, Mattermost, email/Teams, Hybris/AEM, điều cấm | Toàn đội |
| CM-10 | [CM-10-an-toan-thong-tin.md](CM-10-an-toan-thong-tin.md) | 10 quy tắc ATTT, tình huống đúng/sai, báo sự cố trong 1 giờ, bài T1 & bản cam kết | Toàn đội |
| CM-11 | [CM-11-academy.md](CM-11-academy.md) | Academy 3 tuần, chứng nhận L0–L3, 8 bài test T1–T8, phiếu chấm, skill matrix, glossary, 6 thẻ tra cứu nhanh | Toàn đội; Lead/Sub-Lead |
| CM-12 | [CM-12-bvt-handbook.md](CM-12-bvt-handbook.md) | BVT enhancement: quy tắc RHQ, 3 KPI, vai trò PIC, dòng thời gian, trang Confluence, case thị trường, defect/retest, năng lực, notification ngoài giờ | Merch, Tech, Lead, Shift Leader |

## Tech Team (TC) – 5 trang con
Tóm tắt từ trang Confluence "Tech Team (TC)" (https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2478081979), bản nháp v0.1 (21/10/2026), mỗi trang con = một file. Đọc cùng nhóm CM (TC chỉ chi tiết hóa phần riêng của Tech).

| Mã | File | Nội dung chính | Người đọc |
|---|---|---|---|
| TC-01 | [TC-01-tech-operating-manual.md](TC-01-tech-operating-manual.md) | Phạm vi Tech (62 service/21 nhóm, COEC), 3 tầng L1/L2/Samsung L2-L3, tổ chức & chứng nhận, ca/vòng xoay/on-call, priority P0–P4 & SLA/cảnh báo, kiểm soát thay đổi (PC), phối hợp Merch/QA/BVT, KPI, case book | Toàn bộ Tech, Technical Advisor |
| TC-02 | [TC-02-level-1-shift-playbook.md](TC-02-level-1-shift-playbook.md) | Cẩm nang ca L1: ca sớm 04:00, bàn giao 11:00–12:00, ca chiều & bàn giao 19:00, healthcheck HC-01…08, ranh giới L1/L2 & PC, dashboard/filter COE-F, checklist, mẫu bàn giao A–D, mẫu comment tiếng Anh | Tech Level 1 |
| TC-03 | [TC-03-quy-trinh-coec-samsung-l2-l3.md](TC-03-quy-trinh-coec-samsung-l2-l3.md) | Workflow COEC (thẻ từng trạng thái), nguồn ticket & ticket liên kết/nhầm team, tiếp nhận–phân công, tự QA & PC, trạng thái chờ, Maintenance Request/evidence pack/follow-up SDS India, kết thúc ticket, 4 ví dụ đầu cuối | Tech L1/L2, Sub-Lead |
| TC-04 | [TC-04-on-call-handbook.md](TC-04-on-call-handbook.md) | On-call 2 lớp & call tree, chuẩn 15'/30'/60', không remote, đánh giá qua điện thoại, thông báo RHQ (T1–T6), thay đổi khẩn bằng PC, 3 playbook P0, on-call log, bàn giao 04:00, nghỉ sau đêm trực | On-call lớp 1/2, Shift Leader Merch |
| TC-05 | [TC-05-runbook-pc-ticket-change-rules.md](TC-05-runbook-pc-ticket-change-rules.md) | Danh mục runbook Tech & bảng quyết định PC, chuẩn runbook/script/dòng bắt buộc, PC ticket & strike, kiểm soát nội bộ 3 lớp, chuyển đổi tháng 11 & quyền production, freeze, chỉ mục Confluence | Tech L2, Tech Lead |

## Một số điểm xuyên suốt
- **Đồng hồ SLA chỉ chạy khi ticket ở trạng thái thuộc CoE**; chuyển trạng thái (không phải comment) mới là xác nhận đã nhận.
- **Mọi thay đổi production của Tech cần PC ticket do Oliver Leung (RHQ) duyệt**, ImpEx/Groovy phải có dòng số PC ticket + COEC gốc.
- **Dữ liệu Samsung chỉ nằm trên hệ thống Samsung**; bằng chứng QA tạo trên máy trạm CoE, đính thẳng Jira, xóa bản trên máy; không đưa dữ liệu vào AI.
- **QA Team chỉ QA công việc Merchandising**; không làm BVT, không QA cho Tech.
- Nhiều chi tiết còn ghi "chờ RHQ/CEO chốt" (giờ ca QA, kênh với subsidiary, người duyệt PC khi Oliver vắng 23/10–9/11, …) — được giữ nguyên trong từng file.
