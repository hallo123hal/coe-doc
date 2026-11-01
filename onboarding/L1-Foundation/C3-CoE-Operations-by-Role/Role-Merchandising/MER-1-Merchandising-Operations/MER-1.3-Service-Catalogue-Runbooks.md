# MER-1.3 Merchandising service catalogue and runbooks

> Nguồn: page 2482930151 · 50 phút (Study 24' · Demo 6' · Quiz 10' · Practice 10') · Talk + bài tra cứu theo cặp; facilitator: Sub-Lead phụ trách runbook (hoặc Process & Knowledge Lead) · Tài liệu chính: MR-05; thực hành trên giấy, chỉ cần bảng catalogue MR-05 §1.3. Cần xong G2.1 và G6.1.

## Mục tiêu
Tra Service ID, priority mặc định, risk tier, QA gate của một request; nhận service cần linked COEC, email duyệt hoặc Knox; biết cảnh báo/rollback/safe stop nằm ở đâu trong runbook; giải thích ai viết–duyệt–certify runbook và vì sao service phải đạt SRL3 trước khi BiPlus làm live.

## Thuật ngữ
**Service ID** (`MER-PRM-01`; runbook tương ứng `RB-MER-PRM-01`); **QA gate** (Mandatory = QA check hết / Sampling = theo sampling plan / Shift Leader checks = không qua QA Team); **Linked COEC** (service luôn cần ticket COEC liên kết, VD tạo bulk coupon code bằng ImpEx); **Warning** (hộp cảnh báo đặt ngay trước bước rủi ro); **Before value** (giá trị cũ Doer ghi lên ticket để rollback); **SRL0–SRL5** (Service Readiness Level); **Safe stop** (dừng an toàn: để mọi thứ ở trạng thái chưa publish, ghi bước đã làm/chưa làm vào handoff note).

## Nội dung
### 1. Đọc catalogue
Merch có **58 service trong 19 nhóm** (17 nhóm RFP + Issue Resolution + Housekeeping), mỗi service có 1 kết quả, 1 priority mặc định, 1 runbook, 1 team làm, 1 risk tier, 1 QA gate; catalogue version v0, sẽ thống nhất với RHQ sau bàn giao. Đọc một dòng: `MER-PRM-01 Product discount (M/R3/Mandatory)` = Medium, R3, QA check hết. **Shift Leader luôn duyệt trước khi publish live, kể cả service "Shift Leader checks".** Ticket nhiều phần lấy priority & tier của phần chặt hơn (VD DEMO-3307 "giảm 12% 4 SKU + gắn flag Hot Deal" = MER-PRM-01 + MER-TXT-03 → Medium, R3). Không bao giờ hạ tier để nhanh; thấy tier sai thì nâng lên và ghi lý do (CM-07 §2.4).

| Nhóm | Service tiêu biểu (Priority / Risk / QA gate) |
|---|---|
| Product Setup | PRD-01 Samsung SKU (L/R2/Sampling); PRD-04 Z-Code, quà (L/R2/Mandatory); PRD-05 F-Code bundle (L/R3/Mandatory) |
| Price | PRC-01 Price upload, PRC-02 Special price, PRC-03 Discount row (L/R3/Mandatory) |
| Promotion | PRM-01…08, PRM-10 (M/R3/Mandatory); PRM-09 >2 promotion (L/R3/Mandatory) |
| Coupon | CPN-01 tạo coupon, bulk code cần COEC; CPN-02 coupon rule & link (L/R3/Mandatory) |
| Multistore | MST-01 EPP/SMB/O2O/3PD mới (M/R2/Mandatory); MST-02 Excluded products (M/R2/Sampling) |
| Product Reference | PRF-01 Accessories (L/R2/Sampling); PRF-05 PWP bundle (L/R3/Mandatory) |
| Text, Flag, Benefit | TXT-01 bulk text & flag (L/R1/Shift Leader checks; >100 dòng cần diff file); TXT-02, TXT-03 (L/R1/Shift Leader checks) |
| AEM, Shop App | AEM-01 page (L/R1/SL checks); AEM-02 offer page có T&C (L/R2 tạm/Mandatory); SAC-01 Shop App (L/R1/SL checks) |

### 2. Service cần linked COEC, email duyệt hoặc Knox
Luôn cần linked COEC: **MST-01** (store config), **DLV-01** (delivery mode mới), **PRM-08** (bulk eVoucher code), **CPN-01** (bulk coupon code qua ImpEx), và mọi việc vượt khả năng giao diện. EPP site mới/kích hoạt lại (MST-01) cần thêm email duyệt của RHQ (MER-2.4). **Knox áp dụng cho mọi thay đổi giá và mọi promotion, kể cả free-gift/non-discount** (CM-13 ch.10, CM-07 §2.2). Hybris chỉ bật popup Knox cho discount rule — đó là hành vi hệ thống, không phải luật: rule free-gift thì hỏi Shift Leader cách gửi Knox evidence; path luôn lấy từ brief (MER-2.2, MER-2.3).

### 3. Runbook: 16 section và warning
Runbook là điều kiện để làm việc thật: không runbook → không certification → không production access. Runbook chỉ nằm trên Confluence Samsung — **không copy sang hệ thống BiPlus, không in, không lưu máy**. 16 section: (1–5) Purpose & scope, When to use, Who can do it, Preconditions, Internal check & sanity; (6–10) Steps, Self-check (2 cột), Warnings, Evidence, QA evidence required; (11–16) Post-change & go-live check, Rollback & safe stop, When Tech is needed, Escalation, Market notes & templates, Change history. Không áp dụng thì ghi "Not applicable" kèm lý do, không xóa.
**Warning đặt ngay trước bước rủi ro.** 12 warning chuẩn: Time zone, Store scope, Stacking, Staged vs Online catalog, Publish live, Add-on page, Freeze, Bulk >100 dòng, E4 threshold, Quantity limit, Knox re-approval, EPP site.

### 4. Rollback & safe stop
Mọi runbook R3 có rollback viết sẵn; Doer ghi before value trước khi đổi; Shift Leader quyết định rollback. Promotion/coupon: unpublish rule hoặc đặt end date = hiện tại. Price: trả về before value. Stock: reset số lượng và bật lại feed NERP. Reference: xóa cấu hình mới. AEM/Shop App: unpublish hoặc khôi phục bản trước.

### 5. Ví dụ RB-MER-PRM-01
SG, giảm 15% 3 SKU, 01–07/12 SGT: ghi before value + internal check; kiểm trùng rule ở Marketing › Promotion Rules; tạo rule từ template "percentage discount on products" (website, condition 3 SKU, value 15, ngày theo SGT, stackability); Save, **không publish live**; publish simulator, test SKU trong/ngoài list và ngày trong/ngoài hiệu lực; QA REVIEW (checklist QAS-PRM-01), Shift Leader duyệt, Knox, REVIEW SETUP; publish live 01/12 00:00 SGT (23:00 30/11 giờ VN), go-live check.

### 6. SRL và ai sở hữu runbook
SRL0 Listed; SRL1 Defined (RHQ duyệt); SRL2 Documented (runbook 16 section, QA checklist, KB); **SRL3 Ready** (thử trên Jira, mỗi ca có người certified); SRL4 Proven (4 tuần live đạt target); SRL5 Optimised. Service chuyển cho BiPlus ở sprint N phải đạt SRL3 trước sprint đó, không thì BiPlus không làm live. Doer (hoặc người Lead chỉ định) viết → Sub-Lead review kỹ thuật và release → **Merch Lead certify khi 2 người làm theo thành công**. Làm ticket live cần L1 trở lên (G2.1).

### Điểm đáng nhớ từ KT
Template request chuẩn xây cùng subsidiary nhiều năm: chỉ dùng bản RHQ duyệt mới nhất, đổi template phải đề xuất RHQ, không tự sửa (CM-13 §14.1); file template có macro/bị mã hóa → nhờ người upload mở khóa. Hay dùng nhất: XC+ (có change log), Benefit, Promotion, Multistore new site (cần thông tin đầy đủ; EPP mới cần email RHQ). Cần buổi riêng giải thích template — promotion brief dạy ở MER-2.3.

## Quiz (đáp án)
1 Ticket 3 promotion cùng lúc → **MER-PRM-09, Low, R3, QA Mandatory**. 2 Luôn cần linked COEC → **MER-CPN-01 bulk coupon code qua ImpEx**. 3 Time zone warning đặt ở đâu → **ngay trước bước nhập ngày**. 4 Ai certify runbook → **Merch Lead, sau khi 2 người làm thành công**. 5 "Giảm 12% 4 SKU + flag Hot Deal" → **Medium, R3 (phần chặt hơn)**. 6 Đổi giá 20 SKU, bắt buộc để rollback được → **ghi before value của 20 SKU lên ticket**.

## Practice
**PR-MER-1.3-1** (giấy, 10'): 6 request mô phỏng → Service ID, priority, risk, QA gate, cần linked COEC/email RHQ/Knox hay không. (1) 12% off 4 SKU + flag "Hot Deal" → PRM-01 + TXT-03, Medium R3; (2) tạo 300.000 coupon code → CPN-01, R3, linked COEC; (3) thêm SKU vào add-on page flagship → BYP-01, R2; (4) EPP site mới cho bank X → MST-01, R2, QA Mandatory, cần email RHQ + linked COEC; (5) cập nhật banner AEM → AEM-04, R1, SL checks (R2 nếu banner có T&C); (6) 4 promotion BOGO Black Friday → PRM-09, Low, R3. Knox: (1) và (6) cần (BOGO kiểu free-gift vẫn cần); (2) sinh code không cần Knox nhưng promotion rule mà coupon kích hoạt thì cần; (3)(4)(5) không cần Knox ((4) cần email RHQ thay thế).
