# TEC-2. Changes on production

> Nguồn: page 2482897253 (cập nhật 24/10/2026).

Hai kỹ năng liên quan: (1) chuẩn bị change production theo luật RHQ — internal control, PC ticket, rollback; (2) dùng công cụ SAP Commerce (Hybris) để thực hiện change — FlexibleSearch, ImpEx, Groovy, cronjob, Tokoconfig. Mọi lab chạy trên **HAC staging**; không ai đăng nhập production trong khóa học.

| Session | Thời lượng | Mục tiêu chính |
|---|---|---|
| [TEC-2.1 Runbook catalogue, PC ticket, change rules](TEC-2.1-Runbook-PC-Change-Rules.md) | 75' | Đọc một dòng catalogue runbook và nói change có cần PC, second check, Tech Lead review không |
| [TEC-2.2 HAC, FlexibleSearch, ImpEx, Groovy](TEC-2.2-HAC-FlexibleSearch-ImpEx-Groovy.md) | 120' | Giải thích type, item, attribute và vì sao một SKU ra nhiều dòng khi không lọc catalog version |
| [TEC-2.3 Cronjob, Tokoconfig, configuration](TEC-2.3-Cronjob-Tokoconfig.md) | 60' | Tra một cronjob trên Backoffice và HAC staging, đọc đúng Status, Result, end time |
| **Tổng** | **255 phút (~4.2h)** | |
