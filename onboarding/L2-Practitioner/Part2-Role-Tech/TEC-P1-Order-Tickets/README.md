# TEC-P1. Order tickets

> Nguồn: page 2484469842.

Order monitoring và order operations trên dữ liệu staging: stuck order, cancel, return, invoice.

| Session | Thời lượng | Mục tiêu chính | Capabilities |
|---|---|---|---|
| [TEC-P1.1 Daily order-to-NERP check and stuck orders](TEC-P1.1-Daily-Order-NERP-Check-Stuck-Orders.md) | 120' | Chạy daily check và tạo COEC đúng | C2, C3, C4 |
| [TEC-P1.2 Cancel, return, remediation, refund check](TEC-P1.2-Cancel-Return-Remediation-Refund.md) | 120' | Cancel và return order đúng và chứng minh refund | C2, C4 |
| [TEC-P1.3 Invoice and e-invoice](TEC-P1.3-Invoice-and-E-Invoice.md) | 75' | Chuẩn bị batch invoice correction tuân thủ | C2, C4, C5 |
| **Tổng** | **315' (~5.2h)** | | |

Runbook module (sửa đổi 01/11/2026): TEC-MON-01, TEC-MON-02, TEC-ORD-02, TEC-ORD-03, TEC-ORD-05, TEC-ORD-07; quy tắc chung: A.II.2 Tech Services. Trước TEC-P1.1 phải có Kibana login chạy được (xem "Before you start" của TEC-P1.1).
