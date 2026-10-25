# Tài liệu chung CM – Ops CoE (Samsung SEAO) – bản tóm tắt

Tóm tắt từ trang Confluence "Tài liệu chung (CM)" (https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2478375074) và 13 trang con. Mỗi trang con = một file. Tất cả nguồn là **bản nháp** (v0.3; TC-01…05 và CM-12 v0.2, cập nhật 22/10/2026; nguồn nay song ngữ Anh–Việt; CM-13 v1.0 là trang mới và thắng mọi tài liệu khác về quy tắc RHQ), ví dụ dùng dữ liệu giả lập. Các file tóm tắt giữ lại số liệu, quy tắc, mẫu và điểm "chờ RHQ/CEO chốt"; muốn đọc chi tiết từng câu hỏi/bài tập hãy xem trang gốc.

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
| CM-13 | [CM-13-quy-tac-rhq.md](CM-13-quy-tac-rhq.md) | Quy tắc RHQ tập trung (v1.0): SLA, ticket, Merch–Tech, QA, kiểm tra nội bộ, yêu cầu gấp, PC ticket, Knox approval, quyền truy cập, dữ liệu/PII, EPP, 3PD, BVT, strike, 23 điểm chờ RHQ, 10 quy tắc | Toàn đội |

## Tech Team (TC) – 5 trang con
Tóm tắt từ trang Confluence "Tech Team (TC)" (https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2478081979), bản nháp v0.1 (21/10/2026), mỗi trang con = một file. Đọc cùng nhóm CM (TC chỉ chi tiết hóa phần riêng của Tech).

| Mã | File | Nội dung chính | Người đọc |
|---|---|---|---|
| TC-01 | [TC-01-tech-operating-manual.md](TC-01-tech-operating-manual.md) | Phạm vi Tech (62 service/21 nhóm, COEC), 3 tầng L1/L2/Samsung L2-L3, tổ chức & chứng nhận, ca/vòng xoay/on-call, priority P0–P4 & SLA/cảnh báo, kiểm soát thay đổi (PC), phối hợp Merch/QA/BVT, KPI, case book | Toàn bộ Tech, Technical Advisor |
| TC-02 | [TC-02-level-1-shift-playbook.md](TC-02-level-1-shift-playbook.md) | Cẩm nang ca L1: ca sớm 04:00, bàn giao 11:00–12:00, ca chiều & bàn giao 19:00, healthcheck HC-01…08, ranh giới L1/L2 & PC, dashboard/filter COE-F, checklist, mẫu bàn giao A–D, mẫu comment tiếng Anh | Tech Level 1 |
| TC-03 | [TC-03-quy-trinh-coec-samsung-l2-l3.md](TC-03-quy-trinh-coec-samsung-l2-l3.md) | Workflow COEC (thẻ từng trạng thái), nguồn ticket & ticket liên kết/nhầm team, tiếp nhận–phân công, tự QA & PC, trạng thái chờ, Maintenance Request/evidence pack/follow-up SDS India, kết thúc ticket, 4 ví dụ đầu cuối | Tech L1/L2, Sub-Lead |
| TC-04 | [TC-04-on-call-handbook.md](TC-04-on-call-handbook.md) | On-call 2 lớp & call tree, chuẩn 15'/30'/60', không remote, đánh giá qua điện thoại, thông báo RHQ (T1–T6), thay đổi khẩn bằng PC, 3 playbook P0, on-call log, bàn giao 04:00, nghỉ sau đêm trực | On-call lớp 1/2, Shift Leader Merch |
| TC-05 | [TC-05-runbook-pc-ticket-change-rules.md](TC-05-runbook-pc-ticket-change-rules.md) | Danh mục runbook Tech & bảng quyết định PC, chuẩn runbook/script/dòng bắt buộc, PC ticket & strike, kiểm soát nội bộ 3 lớp, chuyển đổi tháng 11 & quyền production, freeze, chỉ mục Confluence | Tech L2, Tech Lead |

## Merchandising Team (MR) – 7 trang con
Tóm tắt từ trang Confluence "Merchandising Team (MR)" (https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2477263980), bản nháp v0.3 (22/10/2026), mỗi trang con = một file. Đọc cùng nhóm CM (MR chỉ chi tiết hóa phần riêng của Merchandising); MR-04 là "anh em sinh đôi" của TC-03 (workflow Shop Merchandising vs COEC).

| Mã | File | Nội dung chính | Người đọc |
|---|---|---|---|
| MR-01 | [MR-01-merchandising-operating-manual.md](MR-01-merchandising-operating-manual.md) | Sứ mệnh, 17 nhóm việc/43 sub-task RFP, tổ chức 29 ghế, 3 ca & quân số, Market PIC/Tech counterpart 8 thị trường, một ngày từng vai trò, priority & SLA (High 4h/Medium 16h/Low 24h), phối hợp QA–Tech–BVT, KPI, leo thang, case book C01–C13 | Toàn bộ Merch |
| MR-02 | [MR-02-shift-leader-playbook.md](MR-02-shift-leader-playbook.md) | 3 vai Shift Leader, checklist đầu ca, kiểm soát SLA 5/15/30', cảnh báo 50/70/85/95, duyệt R1/R2/R3/E4, 23:59, yêu cầu gấp, thay mặt Tech/QA ngoài giờ, IM tạm thời, đòn bẩy vắng người, bàn giao, coaching, ca đêm/cuối tuần | Shift Leader, Sub-Lead |
| MR-03 | [MR-03-market-owner-playbook.md](MR-03-market-owner-playbook.md) | Market PIC sở hữu queue, sắp xếp queue theo SLA & go-live, weekly sync/CSAT/khiếu nại, market rules page (17 mục), lịch thị trường & lễ 2027, giao tiếp & 9 mẫu tiếng Anh, morning pickup/bàn giao, vắng mặt, introduction call | Market Owner |
| MR-04 | [MR-04-quy-trinh-merchandising-chi-tiet.md](MR-04-quy-trinh-merchandising-chi-tiet.md) | Luồng Shop Merchandising M1–M8, 16 trạng thái Jira & đồng hồ SLA, ON HOLD SUBS/COE/RHQ, nhiều KM/thị trường & tách ticket, ngoài giờ, enhancement/BVT/Shop App, COEC liên kết, 3 ví dụ đầu cuối | Toàn bộ Merch, QA |
| MR-05 | [MR-05-danh-muc-service-chuan-runbook.md](MR-05-danh-muc-service-chuan-runbook.md) | Catalogue 58 service Merch, chuẩn runbook 16 mục, SRL0–5 & lộ trình sprint, mẫu + runbook RB-MER-PRM-01, chỉ mục Confluence | Lead, Sub-Lead, người viết runbook |
| MR-06 | [MR-06-kiem-soat-chat-luong-rui-ro-thiet-lap.md](MR-06-kiem-soat-chat-luong-rui-ro-thiet-lap.md) | 4 loại lỗi gây thiệt hại, 14 price sanity rules, kiểm tra nội bộ (thay read-back) + Knox approval, E4 & duyệt hai cấp, kiểm sau go-live 30'/monitor 2h, FPY & 16 root cause code, lỗi theo nhóm service, checklist Doer/Checker | Doer, QA, Shift Leader |
| MR-07 | [MR-07-peak-launch-campaign-playbook.md](MR-07-peak-launch-campaign-playbook.md) | Lịch peak 11/2026–2/2027, flagship & VN Clean Room, T-14→T+1, freeze, roster tăng cường, go-live nhiều thị trường cùng tối (cut-off 17:00), QA hai lớp, Tech standby & PC, BVT, war room, post-peak review | Lead, Shift Leader, MO |

## SAP / Hybris
[SAP-hybris-nghiep-vu-samsung-seao.md](SAP-hybris-nghiep-vu-samsung-seao.md): giáo trình nền tảng SAP Commerce/Hybris cho Samsung SEAO (kênh, thành phần hệ thống, SKU/giá/tồn kho, promotion và coupon, đơn hàng và RDD, EPP/SMB/O2O/3PD, HAC và FlexibleSearch, đặc thù 8 nước), từ trang https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2480047339.

## Tổng hợp câu hỏi và đáp án
[QA-tong-hop-cau-hoi-dap-an.md](QA-tong-hop-cau-hoi-dap-an.md) gom toàn bộ câu hỏi kiểm tra, bài tập và tình huống của 25 bài và tài liệu SAP (CM-01…CM-13, TC-01…TC-05, MR-01…MR-07, SAP), chia theo từng bài, mỗi câu kèm đáp án và giải thích ngắn (quét lại nguồn Confluence ngày 25/10/2026).

## Một số điểm xuyên suốt
- **Đồng hồ SLA chỉ chạy khi ticket ở trạng thái thuộc CoE**; chuyển trạng thái (không phải comment) mới là xác nhận đã nhận.
- **Mọi thay đổi production của Tech cần PC ticket do Oliver Leung (RHQ) duyệt**, ImpEx/Groovy phải có dòng số PC ticket + COEC gốc.
- **Dữ liệu Samsung chỉ nằm trên hệ thống Samsung**; bằng chứng QA tạo trên máy trạm CoE, đính thẳng Jira, xóa bản trên máy; không đưa dữ liệu vào AI.
- **QA Team chỉ QA công việc Merchandising**; không làm BVT, không QA cho Tech.
- Nhiều chi tiết còn ghi "chờ RHQ/CEO chốt" (giờ ca QA, kênh với subsidiary, người duyệt PC khi Oliver vắng 23/10–9/11, …) — được giữ nguyên trong từng file.
