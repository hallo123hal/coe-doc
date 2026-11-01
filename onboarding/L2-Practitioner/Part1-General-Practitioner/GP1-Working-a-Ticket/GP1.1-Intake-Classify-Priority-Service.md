# GP1.1 Intake: classify, reassess priority, pick the service

> Nguồn: page 2484437083 · 60 phút (Study 15' · Demo/thảo luận 10' · Quiz 5' · Practice 30') · Thực hành theo case trên staging và practice ticket; facilitator: Shift Leader hoặc Sub-Lead · Capabilities C1, C4 · Cần xong G2.1 (4 process, 3 câu hỏi kiểm tra, R1–R3) và G2.2 (status Shop Merchandising/COEC, COEC liên kết); mang bảng priority RFP của G2.3 (Merch High 4h/Medium 16h/Low 24h; Tech P0 4h … P4 120h) và spreadsheet trên CoE workstation. Chỉ cần Confluence (đọc); Jira SCOE (đọc) giúp mở practice ticket. Không có Confluence: facilitator in CM-05 §3.1–3.6 và CM-02 §2.7, đưa ticket dạng text.

## Mục tiêu
Phân loại request giống thật vào Service Request, Incident, Change hoặc Problem và nêu bước tiếp (đích 18/20); đánh giá lại priority theo bảng RFP và ghi lý do một dòng; map request sang service ID và mở đúng mục runbook; tách ticket hỗn hợp thành action line (SKU + catalog + action) và route từng line.

## Thuật ngữ
**Reassessment** (đối chiếu priority requester chọn với bảng RFP trước khi giao); **Default priority** (VD MER-PRD-01 Low 24h, TEC-MON-02 P2 16h); **Route check** (câu triage đầu tiên trên COEC: request này có thuộc service khác không); **Action line** (một dòng mỗi SKU, catalog, action); **Service ID** (mã catalogue mang theo priority, risk tier, QA gate, runbook); **Problem trigger**; **Move vs link** (chuyển nguyên ticket khi 100% việc thuộc team kia; giữ ticket và tạo COEC liên kết khi chỉ một phần cần Tech); **label `no-runbook`** (service chưa có runbook, runbook viết trong 3 ngày làm việc).

## Nội dung
### 1. Bốn process trên request thật
Phân loại làm ở bước B2, cùng với đổi status ghi nhận; sai thì SLA, Checker, Approver đều sai. Trước khi coi là Service Request thường, hỏi 3 câu: production có sai ảnh hưởng khách/doanh thu không; có dấu hiệu lộ dữ liệu không; hệ thống có không truy cập được không? Bất kỳ câu nào "có" → báo Shift Leader, người quyết định mở incident process.

| Title thật | Bẫy | Loại đúng |
|---|---|---|
| "[TH] Promotion PR01 published but not applied" (TRN-041) | Giống yêu cầu setup | Incident trên COEC (TEC-TSP-01 V1); rule PR01 nằm sai promotion group nên fix quay lại Merchandising |
| "[ID] [Order remediation] 5 orders stuck" (TRN-037) | "Cứ push đi" | Incident cho lần này; stuck order lặp lại trong một market là Problem trigger |
| Bulk ImpEx archive SKU cho MY (TRN-038) | Coi là setup Merch thường | Change Tech: COEC + PC ticket |
| QA thấy SKU sai trong promotion mới chỉ publish lên simulator | Gọi là incident | Không phải incident: QA FAIL vì chưa live |

**Problem trigger:** cùng triệu chứng 3 lần/tháng; cùng loại ticket reopen 2 lần; ticket chờ Samsung L2/L3 >10 ngày làm việc; stuck order lặp lại trong một market. Lỗi hay gặp: chỉ đọc title; tạo ticket mới để "bắt đầu lại" clock; chuyển cả ticket Merch sang COEC khi chỉ một phần cần Tech.

### 2. Bảy quyết định lúc intake (CM-05 §3.1)
Ở L2 bạn tự quyết, Shift Leader (Merch) hoặc Sub-Lead (Tech, QA) xác nhận.
| # | Quyết định | Cách làm | Lỗi hay gặp |
|---|---|---|---|
| 1 | Loại và team | Mục 1; việc Merch hay Tech | Làm tiếp ticket sai team |
| 2 | Service | Tra catalogue theo nội dung | Chọn service "generic" để khỏi tìm |
| 3 | Market và channel | 1 trong 8 market; B2C, EPP, SMB, O2O, 3PD | Bỏ sót market thứ hai |
| 4 | Priority | Default của service, chỉnh theo impact thật | Hạ xuống cho "nhẹ đầu" |
| 5 | Risk tier, E4 | R1/R2/R3 theo service; E4 từ 10,000 USD, >5 market, hoặc price file ≥500 SKU | Không đếm SKU trong file |
| 6 | QA gate | Bắt buộc, sampling hoặc không (Merch); self-QA trên staging (Tech) | Bỏ QA vì việc "nhỏ" |
| 7 | Due date | Sớm hơn của SLA deadline và go-live − thời gian kiểm | Quên giờ go-live |
Ghi thêm: giờ go-live từng promotion (giờ market + giờ VN), số wave, ngôn ngữ nội dung. Time zone: VN, TH, ID UTC+7; SG, MY, PH UTC+8; AU (Sydney) UTC+11 giờ mùa hè (từ 04/10/2026), UTC+10 (AEST) ngoài mùa hè; NZ UTC+13 mùa hè, UTC+12 (NZST) ngoài mùa hè.
**Ví dụ TRN-007** (VN, "SAVINA Hide and Unhide SKU VD 12 Nov"): Shop Merchandising; service MER-PRD-01 và MER-STK-01; VN, catalog D2C + EPP + SME; Low (24h) vì là việc product/stock; R2; QA sampling; ticket không có giờ go-live nên due = SLA deadline. Initial response: APPROVED-ES → STG SETUP trong 2 giờ (nội bộ 78').

### 3. Đánh giá lại priority trước khi giao
Reporter hầu như luôn raise High; có subsidiary chọn P0/P1 trên COEC vì tưởng nhanh hơn. Quy tắc: (1) bắt đầu từ default của service (project quyết bảng: Shop Merchandising dùng High/Medium/Low, COEC dùng P0–P4); (2) kiểm impact thật — an ninh dữ liệu, hệ thống không truy cập được, hoặc thiệt hại vượt ngưỡng (Merch 10,000 USD; Tech 500 USD cho P0, 100–500 USD cho P1) thì nâng và có thể là incident; (3) đếm promotion: một promotion là Medium (16h); >2 là Low (24h); đúng 2 promotion chưa chốt → hỏi Shift Leader, ghi lý do; (4) priority khác default thì ghi lý do lên ticket; Shift Leader/Sub-Lead sửa priority sai trong 30' và báo requester; (5) không bao giờ hạ priority để tránh breach, không đổi vì queue bận; "URGENT" trong title làm due date sớm hơn chứ không đổi priority.
> **Under review (D13):** các runbook không thống nhất bao nhiêu promotion thì là Medium. Tạm thời ticket có đúng 2 promotion chuyển Shift Leader quyết và ghi lại.

| Ticket | Raised | Sau reassess | Lý do một dòng |
|---|---|---|---|
| TRN-041 (TH COEC) | Medium | P2 | "Launch promotion blocked on test_smb_th, no live loss" |
| TRN-037 (ID COEC) | P2 | P2, Tech Sub-Lead xác nhận | "Stuck orders, paid, no global failure" |
| TRN-042 (VN COEC) | Medium | P3 | "Display defect with workaround; checkout not blocked" |
| TRN-001 (VN Shop Merch) | Medium | Low (RFP) | "Product status and stock lines, no promotion" |
Handover P1 (23/10/2026): *sub-lead phải reassess priority trước khi giao vì ảnh hưởng tính SLA và báo cáo; subsidiary có thể đổi priority lại trong lúc làm, khi đó phải sửa tay.* Vendor hiện tại review priority hằng tuần trước báo cáo. Lưu ý: TRN-001 bảo trainee "đừng tự đổi priority, hãy ghi lại", CM-05 §3.6 bảo Shift Leader/Sub-Lead sửa trong 30' — cả hai nhất quán: bạn đề xuất và ghi lý do, Shift Leader/Sub-Lead là người đổi. RHQ chưa có hướng dẫn viết cho evidence; người trình bày handover hứa bổ sung định nghĩa P0–P4 đã thống nhất vào deck (open point).

### 4. Từ request tới service và runbook
Chọn service cũng là chọn priority, risk tier, QA gate, runbook. Mỗi runbook trong *A.II* bắt đầu bằng phần 1 "Recognise the ticket": title điển hình, default priority, các variant (V1, V2…); variant quyết định bước runbook nào theo. Trang gốc có 4 bước: team theo project + issue type; service theo nội dung; tách line; chọn variant.
| Title điển hình | Service | Default |
|---|---|---|
| "SAVINA-MX Active/Archive SKUs [date]", "[TSE][L2] To set product_[date]" | MER-PRD-01 | Low |
| "[TV] SKU Activate & Sync Warehouse Stock" | MER-STK-01 | Low |
| "[W17] AC Price Upload" | MER-PRC-01 | Low |
| "[TSE] Promotion D2C Aug 26 V4" | MER-PRM-09 | Low |
| "Stuck order on Hybris [date]", "Repush new SO - [date]" | TEC-MON-02 | P2 |
| "[SAVINA] Request cancel & refund" | TEC-ORD-02 | P3 |
| "[EPP] Request for Domain Whitelisting - [date]" | TEC-EPP-01 | Medium khi ở market project; P3 sau khi chuyển COEC |
| "PRODUCT - SMS - VN: Mismatched GNB/Footer link/text…" | TEC-TSP-05 | P2–P4 theo impact |
Khi bắt đầu: mở runbook theo mã, kiểm readiness level và mình có certified cho service đó, dán link runbook vào comment đầu. Không có runbook: label `no-runbook` + báo Shift Leader; không có service phù hợp: chọn gần nhất, ghi lý do, báo Shift Leader/Sub-Lead.
> Lưu ý: TEC-EPP-01 ghi "Requests Medium: 16h" còn CM-02 Appendix A (scenario 13) đặt P3 sau khi chuyển COEC — cả hai đúng: ticket theo bảng của project nó đang ở, SLA Tech tính từ lúc chuyển.
> **Under review (D4):** root runbook sửa đổi nói ticket EPP whitelist/access-code làm trong country project, không chuyển COEC; TEC-EPP-01 và CM-13 §5.2 nói ticket toàn Tech thì chuyển. Tạm thời làm theo 16h. Quiz Q5 và practice item 8 không chấm.

### 5. Tách ticket hỗn hợp thành action line
Không chọn một service cho cả ticket. **Một line mỗi SKU, catalog, action.** Line pre-order → MER-STK-03; virtual stock hoặc block/unblock → MER-STK-02/01; delivery text → MER-DLV-02; giá → service giá của nó; trong cùng ticket hoặc ticket liên kết. Ticket nhiều thay đổi lấy **risk tier cao nhất** cho cả ticket.
**TRN-007** → 
| Item | SKU | Catalog | Action | Service |
|---|---|---|---|---|
| 1 | QA50LS03BAKXXV, QA50LS03DAKXXV, QA65LS03FAKXXV | D2C, EPP, SME (3PD chờ xác nhận) | Hide: kiểm approval + ARCHIVED | MER-PRD-01 V3 |
| 2 | HW-T420/XV, HW-Q600C/XV | `vnMasterProductCatalog` | Unblock stock import | MER-STK-01 V2 |
| 3 | QA85LS03BAKXXV | D2C, EPP, SME | Unhide: approved + PURCHASABLE | MER-PRD-01 V2 |
| 4 | HW-S800B/XV | chỉ `vnEstoreProductCatalog` | "Mua ở đâu": unapproved, giữ PURCHASABLE | MER-PRD-01 V4 (chỉ approval) |
Item 1 và 3 trên 3 catalog (3 SKU × 3 + 1 × 3) cộng 2 và 1 line cho item 2 và 4 = **15 line**, mỗi line cần một kết quả. Trên COEC cùng ý tưởng là route check theo item: TRN-042 có 4 item ở 4 lớp (nav sync job, CMS component, code properties, AEM banner), banner AEM (MER-AEM-04) được trả về Merchandising thành ticket riêng.

## Quiz (đáp án)
1 COEC TH "Promotion PR01 published but not applied", requester chọn Medium, không mất tiền live nhưng launch promotion bị chặn → **B: P2, lý do "launch promotion blocked, no live loss"** (P0 cần an ninh dữ liệu, site không truy cập hoặc thiệt hại >500 USD). 2 Ticket Merch VN "Hide 3 TV; Unblock stock 2 soundbar" → **C: tách action line, hide thuộc MER-PRD-01, unblock thuộc MER-STK-01, cùng ticket**. 3 MY báo order không sang NERP sau sync đêm, lần thứ 3 trong tháng → **B: Incident cho lần này + Problem record**. 4 ID đánh banner ticket "URGENT, go-live 3 giờ nữa", banner không T&C → **C: Low; urgency làm due date sớm hơn chứ không đổi priority**. 5 (không chấm tới khi D4 chốt) Ticket Merch xin thêm email domain vào EPP access list, toàn việc Tech → **B: chuyển chính ticket sang COEC kèm comment; SLA Tech tính từ lúc chuyển**. 6 Subsidiary đổi priority Medium về High giữa chừng, không có impact mới → **C: đề xuất sửa kèm lý do; Shift Leader sửa lại Medium và báo requester**. 7 Không tìm thấy service trong catalogue → **A: chọn service gần nhất, ghi lý do, báo Shift Leader/Sub-Lead**.

## Practice
**PR-GP1.1-1. Intake 20 request** (25', giấy/spreadsheet): facilitator phát 20 title kèm context một dòng. Với mỗi title ghi: process (SRM/IM/CM/PM), priority sau reassess (kèm lý do nếu khác), service ID, bước đầu (đổi status + bước kế). Pass: 18/20 process đúng; mọi reassess High hoặc P0/P1 có lý do một dòng; service ID đúng theo phần "Recognise the ticket". Đáp án service/priority: 1 MER-PRD-01 + stock line, Low; 2 MER-PRD-01 + MER-STK-01, Low; 3 TEC-MON-02, P2; 4 TEC-TSP-01, P2; 5 TEC-TSP-05, P3; 6 MER-PRC-01, Low; 7 MER-PRM-09, Low; 8 TEC-EPP-01 (routing chưa chấm tới khi D4 chốt); 9 TEC-MON-02, P2; 10 TEC-ORD-02, P3; 11 TEC-ORD-05, P3; 12 TEC-REW-02, P3; 13 MER-STK-02, Low; 14 MER-STK-01, Low; 15 MER-STK-03, Low; 16 MER-AEM-04, Low (banner "urgent" không T&C); 17 MER-CPN-01, Low; 18 MER-INC-01, High (promotion MY cho 50% thay vì 5%, đang live, thiệt hại >10,000 USD); 19 TEC-ORD-07, P3; 20 MER-PRF-04, Medium. Bước đầu mọi ticket Shop Merchandising là APPROVED-ES → STG SETUP; COEC là NEW → ASSIGNED. Không cần truy cập hệ thống.
