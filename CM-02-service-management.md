# CM-02 Service Management cho người mới

> Tóm tắt trang Confluence CM-02 (v0.2, bản nháp 21/10/2026). Dạy **khái niệm** Service Management/ITIL ở mức người mới, gắn với ví dụ CoE. Người đọc: toàn đội Ops CoE, bench và người mới Academy. Quy trình chi tiết nằm ở CM-03 (SLA), CM-04 (ca), CM-05 (Service Request), CM-06 (Incident), CM-07 (Change/Problem/knowledge), CM-08 (leo thang), CM-09 (công cụ). Proposal v9.4 (D.1.4) cam kết RHQ quản lý incident, request, change, problem, knowledge theo ITIL ngay trên Jira/Confluence Samsung. Chuẩn tham chiếu "ITIL v5" nhưng tài liệu chỉ dạy 7 guiding principles và khái niệm nền; phần "điểm mới v5" CEO bổ sung sau.

## 1. Dịch vụ, khách hàng, giá trị, 7 nguyên tắc ITIL
- RHQ không đánh giá bằng số thao tác trên Backoffice mà bằng việc dịch vụ có giao **đúng, đúng hạn, an toàn, có bằng chứng**, mọi giờ, 8 thị trường.
- **Output** (làm ra gì) ≠ **Outcome** (khách đạt gì) ≠ **Value** (lợi ích sau khi trừ chi phí & rủi ro). Ví dụ: promotion đúng mức giảm nhưng sai múi giờ → output có, outcome sai, value âm.
- Chất lượng = **Utility** (làm đúng cái cần) + **Warranty** (đúng lúc, an toàn, ổn định). Hạn thật của ticket = mốc đến trước giữa **hạn SLA** và **giờ go-live** (vd banner TH xong 10:30 khi campaign bắt đầu 09:00 = thất bại).
- **Khách hàng**: RHQ = customer/sponsor (đặt yêu cầu, đo SLA, khấu trừ); 8 subsidiary + EPP/SMB/O2O/3PD = user/requester; người mua = người hưởng cuối (CoE không liên hệ trực tiếp); HQ Suwon = bên ban hành quy định (ON HOLD HQ); Samsung L2/L3 (SDS India) = sửa code/deploy/hạ tầng; SDSAP = đơn vị vận hành hiện tại (kết thúc 30/11/2026); BiPlus Ops CoE = service provider.
- Requester đưa đầu vào và xác nhận kết quả, không làm/kiểm thay CoE. Ngoại lệ RHQ cho phép: last-minute request không đủ thời gian QA → subsidiary tự QA khi go-live.
- **Value co-creation**: outcome + cost + risk. Hỏi subsidiary **một** comment gộp, kèm đề xuất cụ thể (vd "đề xuất kết thúc 23:59 SGT 12/12, chỉ B2C, xin xác nhận").

### 7 guiding principles
| # | Nguyên tắc | Ở CoE |
|---|---|---|
| 1 | Focus on value | Đọc brief để hiểu outcome; phản hồi đầu có owner/bước tiếp/thời điểm; go-live sớm hơn SLA thì theo go-live (vd Low 24h nhưng campaign sau 6h → xếp lên trước) |
| 2 | Start where you are | Dùng Jira/Confluence/trạng thái hiện có; không tự đổi tên trạng thái; ghi gap log |
| 3 | Progress iteratively | 4 sprint nhận dần việc; phân tích thứ Bảy; runbook có phiên bản |
| 4 | Collaborate & visibility | Mọi việc trên ticket, handoff note, báo sớm |
| 5 | Think holistically | Promotion chạm Merch/QA/Tech; kiểm storefront, không chỉ Backoffice |
| 6 | Keep it simple | Một câu hỏi gộp; không bỏ cổng kiểm soát bắt buộc (QA gate, duyệt Shift Leader, read-back, kiểm sau R3, PC ticket) |
| 7 | Optimize & automate | Chuẩn hóa trước rồi mới automate; AI chỉ công cụ được duyệt |

## 2. Bốn loại việc
| Loại | Nhận biết | Quy trình |
|---|---|---|
| **Service Request** | Xin việc chuẩn đã có trong catalogue (143 service); có mẫu, runbook, SLA | CM-05 |
| **Incident** | Dịch vụ đang chạy bị gián đoạn/sai ngoài kế hoạch | CM-06 |
| **Change** | Thêm/sửa/xóa gì đó chạm production | CM-07 |
| **Problem** | Nguyên nhân gốc / lỗi lặp lại | CM-07 |

- Phân loại ngay khi tiếp nhận cùng service, priority, risk tier. Không chắc → hỏi Shift Leader (Merch) / Sub-Lead (Tech, QA).
- Service Request Merchandising thường tạo thay đổi production → làm theo quy tắc Change (risk tier, QA gate, duyệt) **trong cùng ticket Shop Merchandising**, không tạo ticket Change riêng. Tech: COEC là ticket làm việc + **PC ticket** do Oliver Leung duyệt cho mọi thay đổi production.
- **Incident**: ưu tiên **khôi phục trước, tìm nguyên nhân sau**; Tech P0 và Merch/QA High = major incident, khôi phục trong 4h kể cả ngoài giờ; sai giá/khuyến mại: phút 0–30 tắt/rollback promotion, báo RHQ & subsidiary trong 30 phút; Incident Manager = Lead trụ (ngoài giờ on-call; Shift Leader tạm thời). Chín bước I1–I9 ở CM-06. Phải đọc nội dung, không chỉ tiêu đề ("Please update price" có thể là giá sai đang bán).
- **Change**: gồm Backoffice, AEM, Shop App CMS, cấu hình/dữ liệu Tech (payment, base store, NERP, FI, access rule, EPP, ImpEx, Groovy), deploy code/hạ tầng (L2/L3). Merchandising: R1 (text, banner, CMS), R2 (product setup, delivery, stock), R3 (giá, discount, promotion, voucher, payment, quyền) + ngưỡng E4; QA kiểm R3 và R2 có gate, Shift Leader duyệt. Tech: staging → tự QA → another set of eyes → PC ticket.
- **Problem**: known error, workaround. Mở problem record khi: cùng dấu hiệu 3 lần/tháng; cùng loại ticket reopen 2 lần; chờ L2/L3 > 10 ngày làm việc; stuck order lặp lại ở một thị trường (+ sau training 21/10: ticket tồn lâu ở trạng thái chờ, last-minute request lặp lại).
- Ví dụ chuỗi: MY promotion giảm sai → incident → tắt trong 30' → emergency change (Merch Lead duyệt, ghi trong 2h) → RCA → problem (CAPA 3 ngày làm việc) → service request mới đi đủ cổng R3.
- **Lỗi phân loại hay gặp**: chỉ đọc tiêu đề; coi lỗi QA phát hiện trước khi live là incident (đó là FAIL của cổng QA); tạo ticket mới để "reset đồng hồ"; chuyển nguyên ticket Merch sang COEC khi chỉ cần Tech một phần; xử lý incident như change thường (khống chế trước).

## 3. Ticket và vòng đời
- Ticket = bản ghi duy nhất (SLA, audit, bằng chứng đều từ ticket). Mọi yêu cầu vào Jira trong 5 phút; không làm ngoài ticket; không ticket nào không owner (lọc 30'); không chép nội dung ticket ra ngoài.
- **Issue type/project**: Shop Merchandising (subsidiary tạo; Merch + QA xử lý; 1 workflow chung 8 nước), COEC (Merch/QA/HQ/subsidiary tạo; chỉ Tech), Maintenance (Tech tạo; SDS India), Enhancement (đội phát triển; PIC BVT test), PC ticket (Tech tạo; Oliver duyệt).
- **Khi tiếp nhận**: chuyển trạng thái xác nhận nhận; kiểm service; loại việc; priority; (Merch) risk tier/E4/QA gate; due date; thị trường/kênh; assignee là người CoE. Trùng/thử → INVALID kèm lý do.
- **5 nhóm trạng thái & đồng hồ SLA**: (1) trước CoE – PLANNING/PLANNING REVIEW: chưa tính; (2) vào hàng đợi – APPROVED-ES / NEW: bắt đầu đo initial response; (3) CoE đang làm – STG SETUP, QA REVIEW, PRD SETUP, **ON HOLD COE** / ASSIGNED, IN REVIEW, IN PROGRESS, QA REVIEW, WAITING QA: **tính**; (4) chờ ngoài CoE – ON HOLD SUBS, ON HOLD RHQ, REVIEW SETUP / ON HOLD SUBSIDIARY, SYSTEM SUPPORT, ON HOLD HQ, ON HOLD ES: **dừng**; (5) xong – PENDING LAUNCH, LAUNCH VERIFICATION, CLOSED, INVALID: không tính. CoE tạm lập kế hoạch theo giờ lịch 24/7 đến khi RHQ xác nhận cách tính.
- **Workflow Shop Merchandising**: PLANNING → PLANNING REVIEW → APPROVED-ES → STG SETUP → (QA REVIEW) → PRD SETUP → REVIEW SETUP → PENDING LAUNCH → (go-live, QA lại trên production) → LAUNCH VERIFICATION → CLOSED. Bốn điểm: (1) qua QA REVIEW hay không do risk tier (R3, R2 có gate phải qua; R1/R2 không gate đi thẳng, Shift Leader vẫn duyệt); (2) STG SETUP ≠ môi trường staging; (3) REVIEW SETUP: bằng chứng QA (PowerPoint) đính Jira; nếu go-live ngày mai mà 23:59 chưa duyệt → vẫn publish và comment "đã publish như đã thống nhất, chưa nhận phản hồi"; (4) go-live nhiều đợt: mỗi đợt QA lại trên production, giữa các đợt ở PENDING LAUNCH. *L.V. APPROVAL* chưa rõ, không dạy như bước bắt buộc.
- **Workflow COEC**: NEW → ASSIGNED (Tech Lead) → IN REVIEW/IN PROGRESS → QA REVIEW/WAITING QA (Tech tự QA trên staging) → LAUNCH VERIFICATION (giao người tạo) → CLOSED. ON HOLD HQ gồm chờ duyệt PC ticket (comment "PC ticket pending"; Oliver duyệt xong chuyển ticket gốc về IN PROGRESS); ON HOLD ES: quyền Hybris/tài khoản/reset mật khẩu Back Office; SYSTEM SUPPORT: SDS India. SEAO không có Accenture: CoE tự chạy production sau khi PC duyệt.
- **Owner**: team ownership (CoE giữ đến khi đóng) + personal ownership (đúng 1 người có tên). Ngoại lệ Assignee: ON HOLD SUBS (subsidiary), LAUNCH VERIFICATION COEC (người tạo). Merch: Market Owner ca ngày, Team Member ca tối/đêm; Shift Leader xác nhận. Không ticket nào không owner quá 1 giờ; không rời ca mà không có owner mới trong handoff.
- **Trạng thái chờ ≠ nút dừng đồng hồ**: ON HOLD SUBS = comment + chuyển trạng thái + giao Assignee cho subsidiary; có trả lời → về STG SETUP ngay; ON HOLD COE vẫn tính SLA; mọi trạng thái chờ có owner CoE + next action + thời điểm nhắc. Theo dõi ticket ở L2/L3: High 2 ngày làm việc/lần, Medium 4 ngày, Low hằng tuần (mỗi lần 1 comment). Dashboard cần xem: APPROVED-ES chưa nhận, ON HOLD SUBS mà Assignee là người CoE, COEC ở NEW.
- **Merchandising cần Tech** (vd 500.000 voucher cần ImpEx): tạo ticket COEC mới + issue link, ticket Merch sang ON HOLD COE; hai SLA chạy song song (Tech chậm → Merch trễ). Việc hoàn toàn thuộc team kia → **move** chính ticket (SLA theo team mới); quy tắc move chờ RHQ xác nhận văn bản.
- **Kết thúc/mở lại/hủy**: mở lại xử lý trên chính ticket, giữ priority, **đồng hồ cộng tiếp, không reset**; INVALID đóng hẳn, làm lại thì clone. Cấm: ON HOLD SUBS giả, INVALID rồi clone, tách ticket, tạo ticket mới thay vì move, đổi priority để dừng/reset đồng hồ.
- Câu hỏi còn mở (SDM hỏi RHQ): L.V. APPROVAL, nghĩa "ES", Shift Leader Merch có được chuyển COEC NEW→ASSIGNED ngoài giờ Tech không, ai đóng ticket tồn ở REVIEW SETUP/LAUNCH VERIFICATION.

## 4. Priority (bảng RFP 3.3)
- Impact, urgency giúp đọc bảng; **priority do bảng RFP quyết**, không đặt theo cảm giác. Sai priority → Shift Leader/Sub-Lead sửa trong 30 phút và ghi lý do.
- **Merchandising & QA** (SLA ticket Merch, gồm cả bước QA; RHQ không đo QA riêng): **High 4h** (ảnh hưởng bảo mật dữ liệu; mất doanh thu > 10.000 USD); **Medium 16h** (1 promotion đơn lẻ; multistore EPP/SMB/O2O/3PD, EPP site/access management, GNB EPP2.0, merge EPP stores, O2O new store/IP whitelisting, referral, fixed price/percentage/total cart discount, BOGO, cross-sell, overtrade, SC+, redemption eVoucher…); **Low 24h** (> 2 promotion, product setup, buying page, special price, discount row, text, flag, benefits, delivery mode, stock, product reference, shipping message, PINMAP, payment config, add-ons, voucher creation, campaign page/banner, CMS, user account/password reset, Samsung Rewards, CS support). Đúng 2 promotion là Medium hay Low: chưa rõ, tạm hỏi Shift Leader.
- **Tech**: P0 (bảo mật dữ liệu, không truy cập được; mất > 500 USD) 4h; P1 (100–500 USD) 8h; P2 (khẩn, lỗi đơn do cấu hình, báo cáo quản trị gấp) 16h; P3 (vận hành hằng ngày, báo cáo, sửa dữ liệu hàng loạt) 40h; P4 (câu hỏi, nghiên cứu) 120h. Ticket nằm ở project nào dùng thang đó.
- **Initial response**: RFP 2h, ≥ 97%; nội bộ P0/High 15', P1 30', khác 78'. Merch đo APPROVED-ES→STG SETUP; Tech NEW→ASSIGNED. Ngoài cửa sổ Tech (04:00–19:00 T2–T7): Shift Leader Merch kiểm COEC NEW; P0/P1 gọi Tech on-call.
- **Due date** = mốc sớm hơn giữa hạn SLA và (go-live − thời gian QA/duyệt). RHQ: promotion nên gửi trước go-live 2–3 ngày làm việc (chờ xác nhận); gửi muộn = **last-minute request** (gắn nhãn, đếm cho họp tuần). Severity (Critical/High/Medium/Low) dùng cho incident report, khác priority.
- Checklist tiếp nhận: chuyển trạng thái trong mục tiêu; đọc toàn bộ mô tả; kiểm ảnh hưởng dữ liệu/doanh thu; chọn bảng + đếm promotion; tính due date; P0/High → báo Shift Leader mở incident.

## 5. SLA, OLA, KPI
- **SLA** (BiPlus–RHQ, có khấu trừ), **OLA** (giữa các team nội bộ để giữ SLA), **KPI** (đo để cải tiến), **UC** (hợp đồng với nhà cung cấp ngoài; L2/L3 là đội Samsung nên chỉ theo dõi chủ động, không "đòi" theo hợp đồng).
- **Composite** = Resolution×75% + Response×15% + Pass Rate×6% + Report Completion×3% + User Acceptance×1%; quý < 97% khấu trừ 1–5%; nội bộ 98,5%. BVT KPI do PIC Merch/Tech.
- **OLA cho QA** (minh họa, nội bộ): dispatch trong 15'; kiểm High 30', 1–2 mục 2h làm việc, một lô 8h; PASS kèm bằng chứng hoặc FAIL kèm danh sách lỗi + root cause code; QA + duyệt Shift Leader dùng tối đa **25% thời gian SLA còn lại**; go-live cùng tối gửi QA trước 17:00 (ngưỡng nội bộ); quá tải → phân lại 15', gọi bench QA, báo QA Lead. Còn: duyệt trước production High 15'/khác 30'; L1→L2 kèm handover; Shift Leader gọi Tech on-call P0/P1 ngoài giờ.
- **KPI**: Composite 97%/98,5%; First-pass yield 90% (T11), 95% (từ T12); escaped defect ≤ 1/1000 mục QA; CSAT 4,3 từ quý 2 (phản hồi ≥ 20%); ticket không owner = 0; runbook coverage 60% sau T1, 90% sau T3. Không biến mục tiêu nội bộ thành cam kết với RHQ; chỉ COE Lead và CEO được cam kết với RHQ.

## 6. Doer – Checker – Approver
| | Merchandising | Tech |
|---|---|---|
| Doer | Market Owner/Team Member (setup, bằng chứng, rollback R3) | Tech TM (làm staging trước, chuẩn bị ImpEx/Groovy) |
| Checker | QA Team (R3, R2 có gate); Shift Leader với R1 | Tự QA trên staging; thêm another set of eyes khi chưa chắc/rủi ro cao |
| Approver | Shift Leader trực (+ Merch Lead/Deputy khi E4) | Oliver Leung qua PC ticket (duyệt duy nhất, HOD cụm SEAO gồm SMB) |
- Ba vai trò trong **cùng một ticket** (Merch). Doer không bao giờ tự duyệt, kể cả Shift Leader/Lead (cần deputy Shift Leader đã chứng nhận hoặc Lead; chưa có thì chưa lên production). Với Tech, kiểm soát nội bộ phải xong **trước** khi gửi PC ticket; Oliver không có backup — chỉ nhắn Mattermost khi P0/P1 gấp.
- Ví dụ DEMO-6010 (MY, 40 SKU 5%): read-back → setup + publish simulator → QA thấy 50% → FAIL → sửa → PASS → Shift Leader duyệt. DEMO-6020 (xóa user group 300 tài khoản SG): ImpEx mới → staging → tự QA → another set of eyes → PC ticket (ON HOLD HQ) → Oliver duyệt → chạy production → LAUNCH VERIFICATION.
- **QA độc lập**: chỉ QA việc Merch, không QA Tech, không BVT; báo cáo QA Lead (không phải Merch Lead); **quyền trả về** — chỉ COE Lead được vượt (và báo RHQ); QA Lead kiểm lại 5% PASS mỗi tuần; 2 lần bị QA trả trong tháng của cùng TM = mức L1 people-risk ladder (kèm cặp, giảm WIP nửa, chứng nhận lại 5 ngày làm việc).
- **Checker kiểm**: giá trị, phạm vi (SKU/market/store/kênh), thời gian & múi giờ, tương tác (cộng dồn), hiển thị storefront/giỏ hàng/mobile, bằng chứng. Checker không tự sửa. Bằng chứng QA = PowerPoint chụp từng bước, tạo trên máy trạm, đính Jira, xóa bản trên máy (CM-10).
- **Approver Merch** kiểm: risk tier đúng, cổng trước đủ (QA PASS, read-back R3), go-live trong ca đang trực thị trường (R3), có rollback (R3); High duyệt 15', khác 30'.

## 7. Service catalogue, runbook, knowledge base
- **143 service / 53 nhóm**: Tech 21 nhóm/62 service; Merchandising 19/58 (SKU, buying page, price upload/special price/discount row, text/flag/benefits, multistore, stock, 8 loại promotion, coupon, trade-in, AEM CMS, Shop App CMS…); QA 7/11; liên trụ 6/12 (governance, Composite, major incident, RCA, BVT engagement, launch, đào tạo, problem mgmt). Service QA liên quan BVT/Tech sẽ được gán lại khi rà với RHQ.
- Mỗi service: request template + trường bắt buộc, priority mặc định, runbook, risk tier, QA gate. **Class A** (~30) đạt SRL3 trước CP1 (31/10); **Class B** SRL3 trước CP3 (26/11); **Class C** có tài liệu trước CP3. SRL0 (liệt kê) → SRL5 (tối ưu).
- **Runbook** tối thiểu: điều kiện trước; bước đánh số có checkpoint; guardrail; bằng chứng; rollback (bắt buộc R3); khi nào dừng & leo thang. Chỉ làm service đã chứng nhận (L0 Trained – staging; L1 Certified – ticket live có kiểm; L2 độc lập; L3 Coach). Ticket chưa có runbook phải gắn cờ; viết runbook trong 3 ngày làm việc.
- **Knowledge base** trên Confluence Samsung: runbook, QA checklist/test case, known error/workaround, market rules & glossary, handoff note, configuration record, trang RHQ (guide add-on, flagship/freeze plan), trang CoE (auxiliary). Không chép ra máy cá nhân/BiPlus.

## 8. Đo lường & cải tiến liên tục
- Đo từ Jira Samsung, cùng công thức với RHQ; không dashboard riêng/không export. Các tầng: ticket (cảnh báo 50/70/85/95%) → ca (Shift Leader/Tech L1) → ngày (stand-up) → tuần (Weekly Service Review, họp RHQ) → tháng (Composite vs 97%/98,5%) → quý (QBR, rà catalogue/skill matrix).
- < 98,5%: SDM lập kế hoạch khắc phục nội bộ trong 5 ngày làm việc. < 97%: COE Lead + CEO gửi RHQ kế hoạch khắc phục trong 5 ngày làm việc (nguyên nhân, hành động, owner, ngày).
- **PDCA** (ví dụ lỗi múi giờ AU/NZ giờ mùa hè → thêm dòng "múi giờ & DST" vào read-back/checklist → 0 FAIL sau 2 tuần → cập nhật runbook, đào tạo lại). Nhịp: hằng tuần phân tích ticket trễ/reopen + weekly problem review; thứ Bảy retro/sprint planning; hằng tháng 3 cải tiến trình RHQ với số liệu trước/sau + monthly knowledge review; hằng quý đề xuất cải tiến phía Samsung (mẫu yêu cầu, quy tắc priority, automation Jira).
- Bạn góp: ghi nguyên nhân đúng (không "lỗi người" chung chung — nêu chỗ sửa hệ thống), báo sớm lỗi lặp lại (3 lần/tháng), cập nhật runbook, đề xuất; chuyển trạng thái đúng lúc vì số liệu đọc từ lịch sử trạng thái.

## 9. Bài tập và kiểm tra (dùng cho T3)
- 20 tình huống phân loại (loại việc / priority / lý do), ví dụ đáp án: 1 promotion → Service Request R3, Medium; checkout lỗi toàn site → Incident major P0 (Shift Leader gọi Tech on-call, thay đổi khẩn vẫn cần PC ticket); 5 promotion → Low, QA lại mỗi đợt; text/flag → R1 Low; voucher dùng vượt giới hạn gây thiệt hại > 10.000 USD → Incident High; đơn không sang NERP lần 3 → Incident + mở Problem (P2); QA FAIL trước live → không phải incident; 500.000 voucher → ticket Merch (Low) + COEC liên kết, ON HOLD COE, ImpEx cần PC; ticket đúng là việc Tech (EPP access code) → move sang COEC; duyệt 17:50 cho go-live 00:00 → last-minute request; gửi cảnh BVT trên Mattermost → handoff + nhắn Merch/Tech Lead chỉ định PIC; brief sai nhưng thiệt hại > 10.000 USD → vẫn xử lý incident High.
- 20 câu kiểm tra (đáp án chính): outcome vs output; RHQ = customer & sponsor; 1 promotion = Medium 16h; P1 = 100–500 USD 8h; RFP phản hồi 2h vs nội bộ 15'; OLA nội bộ; chỉ COE Lead vượt QA; reopen không reset đồng hồ; lọc không owner 30'; ON HOLD COE vẫn tính SLA; initial response = APPROVED-ES→STG SETUP; QA chỉ Merch; thay đổi Tech cần PC ticket kể cả 5 giây; L2/L3: Maintenance Request + SYSTEM SUPPORT, CoE giữ ownership, theo dõi 2 ngày làm việc/lần; Composite 96,8% → kế hoạch khắc phục gửi RHQ trong 5 ngày làm việc.
