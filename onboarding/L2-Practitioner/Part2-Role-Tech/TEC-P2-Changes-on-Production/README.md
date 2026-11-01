# TEC-P2. Changes on production

> Nguồn: page 2484306466 · 270' (~4.5h). Thuộc Part 2 Role Tech.

Thay đổi production theo cách Practitioner: test trên staging, có PC ticket, có rollback và có người check thứ hai.

| Session | Thời lượng | Mục tiêu chính | Capabilities |
|---|---|---|---|
| [TEC-P2.1 HAC, FlexibleSearch, ImpEx and Groovy with a PC ticket](TEC-P2.1-HAC-FlexibleSearch-ImpEx-Groovy-PC-Ticket.md) | 120' | Viết query cho 5 câu hỏi điều tra | C2, C4, C5 |
| [TEC-P2.2 EPP whitelist, delisting, access codes, retiree list](TEC-P2.2-EPP-Whitelist-Delisting-Access-Codes-Retiree.md) | 90' | Quản lý whitelist, access code và dự đoán ai đăng nhập được | C2, C4 |
| [TEC-P2.3 Enhancement support and handoff](TEC-P2.3-Enhancement-Support-Handoff.md) | 60' | Chuẩn bị enhancement handoff để build team hành động được | C2, C4 |
| **Tổng** | **270'** | | |

Học theo thứ tự. Runbook (sửa đổi 01/11/2026): TEC-EPP-01 (domain và email whitelist), TEC-EPP-03 (access code), TEC-ADH-02 (enhancement support Tech); quy tắc chung A.II.2 Tech Services. Mọi script bắt đầu bằng dòng cố định `#NOTE ITGC_JIRA:PC-xxxxx (COEC-xxxxx)` (ImpEx) hoặc `//NOTE ITGC_JIRA:PC-xxxxx (COEC-xxxxx)` (Groovy); thiếu dòng là vi phạm nghiêm trọng.
