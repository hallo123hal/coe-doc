# TEC-P3.3 3PD middleware and Rewards points

> Nguồn: page 2484437127 · 75' (Study 20' · Demo 10' · Quiz 10' · Practice 35') · Facilitator: Shift Leader/Sub-Lead · Capabilities C2, C4 · Cần xong TEC-3.2 (luồng order, stock, product giữa Hybris, middleware và marketplace; interface GCRM). Mang pack TEC-TSP-02 và TEC-REW-02 và hai case giấy do facilitator phát. Access tuỳ chọn: staging Backoffice/HAC el3-s2 (Order › Orders, Business Processes, CronJobs). Bài thực hành hoàn toàn trên giấy, không cần access.

## Mục tiêu
Dựng order table của case 3PD và nêu hop lỗi kèm bằng chứng; quyết định owner của lỗi 3PD (CoE fix, TEC-MON-02, data Merch, team middleware, development partner, subsidiary) và nhịp escalate; phân loại ticket Rewards vào V1–V5 và liệt kê ba kiểm tra read-only đầu; chuẩn bị điều chỉnh điểm để duyệt: kiểm journal, peer check input, conversion factor, PC, duyệt của programme owner khi cần.

## Thuật ngữ
**Hop** (một chặng của luồng tích hợp: marketplace → middleware, middleware → Hybris, Hybris → NERP; bạn xác định hop nơi order dừng); **Logicbroker (Bifrost)** (middleware đưa order marketplace 3PD vào Hybris qua API SamsungBifrost; pack v0.2 gọi middleware 3PD là "MSA"); **PIC 3PD** (thành viên Tech Team chuyên 100% ticket 3PD, có backup certified; quyết định CEO 21/10/2026); **Order table (template TSP-02)** (mỗi order một dòng: Hybris order, PO ID marketplace, store ID, status thấy, hành động cần; mỗi dòng kết thúc "not in Hybris" hoặc "stuck at [step]"); **Re-push với SO mới** (gửi lại order sang NERP để có sales order mới; chỉ sau khi subsidiary xác nhận trong ticket là chưa ship gì); **Rewards journal** (record `TokoRewardsTransactionJournal` mỗi request điểm: requestType U (dùng) hay C (cancel/refund), result, returnCode); **Conversion factor** (điểm trên đơn vị tiền mà refund script dùng, VD SG = 500; Checker tính lại từ log redemption Kibana); **Programme owner** (owner Rewards của subsidiary xác nhận điểm bằng văn bản và quyết định lỗi số dư, refund không có order); **RWD2N3008 / RWD2N3004** (mã trả về: "not enough cancelable points" = đã refund; "not enough point to cancel" = số dư thấp hơn refund).

## Nội dung
### 1. Runbook TEC-TSP-02
Phủ lỗi giữa Hybris, middleware và marketplace 3PD (Shopee, Lazada, TikTok Shop…), cộng service MSA cho order D2C (fraud, notification, GCRM). 231 ticket 2026, ~26/tháng. Doer: engineer Level 2 (3PD và middleware). Checker: Tech Sub-Lead. Approver: Tech Lead và PC approver. Priority thường: P2 cho order marketplace kẹt, P3 cho một sync, FI hay chỉnh GCRM đơn lẻ. Desk xác nhận priority trong 30 phút. Cả luồng sập một market, lộ dữ liệu hay thiệt hại >500 USD là P0, mở COE-INC-01.
| Variant | Dùng khi | Tỷ lệ |
|---|---|---|
| V1 Order marketplace không chảy | Order mất, "not found" (404), hay kẹt | Phổ biến nhất: "Stuck Order TIKTOK" ~11%, "Orders not found in MSA" ~6% |
| V2 Status, cancel, FI, GCRM | Order huỷ không có FI posting; order completed cần đẩy GCRM | ~3%; batch hằng tháng TH, VN |
| V3 Order data mapping | Số tiền, seller discount, freebie, delivery mode khác | Ít gặp |
| V4 Stock, price, product feed | Stock listing hay sản phẩm không cập nhật | ~6% ("Dummy stock") |
| V5 Fraud service | Order chờ kết quả fraud quá lâu | Ít gặp (AU, SG) |
| V6 Đổi rule MSA | Rule/setting mới | Normal change cần RHQ duyệt |
| V7 Document Failed trong portal middleware (thêm 01/11) | Order Failed trong portal Logicbroker (hoặc Intrepid) kèm lỗi: stock, SKU inactive, delivery mode, địa chỉ, token | Vận hành bình thường hằng ngày theo SDSAP |
| Bước | Doer | Checker |
|---|---|---|
| Tiếp nhận | Luồng và kênh; impact; kiểm master incident; release trong 72h; template A "không re-push hay cancel trong lúc này" | Priority khớp impact; đã kiểm master incident |
| Order table | Backoffice › Order › Orders; Business Processes cho bước lỗi; field SO, DO, FI | Order table đủ với trạng thái before |
| Nguyên nhân | Trace theo PO ID và giờ trong log; ghi nguyên nhân trước mọi push | Root cause nêu và chứng minh |
| Fix | Order chưa vào Hybris: một Retry trong portal middleware sau khi sửa nguyên nhân và kiểm số tiền (V7). Mọi thay đổi Hybris production: subsidiary xác nhận và PC, kể cả một order; batch qua TEC-ORD-05 hay TEC-TSP-03 | Có xác nhận; tôn trọng ngưỡng |
| Verify | Mọi order ở status mong đợi có SO; kết quả FI và GCRM | Không dữ liệu cá nhân |
> Pack v0.2 gọi middleware 3PD là "MSA". TEC-TSP-02 sửa đổi (01/11) đặt tên theo handover 3PD 27/10: đa số market (PH, VN, ID, TH…) dùng Logicbroker, gọi API SamsungBifrost; SG SESP dùng Intrepid; AU bán trên eBay với product/stock qua API trực tiếp. CoE làm việc với bốn công cụ middleware; MSA phục vụ fraud và trade-in. Ghi tên middleware lên mọi ticket trước khi điều tra.

### 2. 3PD từng hop: marketplace, middleware, Hybris
CoE quản lý middleware, không quản lý marketplace. Ticket 3PD vào COEC và tới PIC 3PD (backup khi vắng); không bao giờ tới Merch, và không tới Samsung L2/L3 trước khi qua kiểm TC-03 §6.1. Tech Lead xin quyền middleware qua approval ticket.
| Hop | Xem gì (read-only) | Bằng chứng gãy | Owner |
|---|---|---|---|
| Marketplace → middleware | Status marketplace của requester; portal middleware | Order chưa bao giờ tới middleware | Chủ 3PD của subsidiary (marketplace từ chối update) |
| Middleware → Hybris | Log theo PO ID và giờ; Backoffice › Order › Orders | "Not in Hybris"; lời gọi create thiếu hay bị từ chối (SKU không có ở 3PD store, không giá hay stock, sai site) | Middleware không gọi: vendor middleware (CoE tạo support ticket Logicbroker/Intrepid), báo RHQ. Hybris từ chối: sửa data (Merch data services) |
| Thông báo ngược | Order dưới store hay PO khác | 404 "order not found" (KE-TEC-TSP-02-02) | CoE tìm hay tạo lại sau khi sửa nguyên nhân |
| Trong Hybris | Business Processes: Code, Definition, Process State, Result (VD splitOrder, sendConsignmentToExternalERP) | Bước lỗi xác định; không lỗi tích hợp | Runbook TEC-MON-02 (V7) |
| Hybris → NERP, FI, GCRM | HAC: gerpSalesOrderNumbers, gerpFIStatus; `waitingForSendToGCRMForInstantEarn` | Không SO; FI thiếu hoặc bằng 0 (KE-05) | Số tiền 0: lỗi mapping, development partner; không gửi lại |
**Ví dụ (PH TikTok Shop).** PH gửi danh sách order TikTok Shop một ngày kẹt trước shipping request. V1, P2. Xác nhận priority trong 30 phút, đăng template A, tìm từng order trong Backoffice và đánh dấu từng dòng. Một nguyên nhân 3PD đã biết là thiếu entry trong `delivery_mode_mapping`. Ghi nguyên nhân trước mọi push, lấy xác nhận của subsidiary là chưa ship gì, và PC duyệt kể cả một order; nhiều order cùng nguyên nhân đi TEC-ORD-05 hay TEC-TSP-03. Cùng nguyên nhân 3 lần/tháng mở COE-PRB-01. Rủi ro lớn nhất: push trước khi biết nguyên nhân gây ship đôi hoặc FI thiếu/bằng 0; order đã push không kéo lại khỏi NERP được.
**Document Failed trong Logicbroker (V7).** SDSAP xử lý hằng ngày. Mở document trong portal, đọc lỗi và khớp cấp (KB "2) Logicbroker Common Issue"):
- Cấp 1, data subsidiary (hết stock, SKU inactive, delivery mode, giá, địa chỉ hay region code chưa map): báo subsidiary bên nào sai; data Hybris sửa qua MER-PRD-01, MER-DLV-01 hay MER-STK-01; rồi re-push.
- Cấp 2, data document (tên quá dài, dấu backslash trong địa chỉ, thiếu first name, cancellation bị rút): CoE sửa document trong portal trước re-push.
- Cấp 3, lỗi API/vendor (401, 500, 503, 504, connection closed): retry một lần; vẫn Failed thì tạo ticket vendor middleware, báo RHQ và theo dõi tới đóng. Cấp 4 (Bifrost, delivery mode chưa bật cho marketplace, thiếu site locale): RHQ.
- Mất kết nối ("Lazada API: Failed to refresh token", Shopee "Partner and shop has no linked"): kết nối lại account ở Settings › Connections, rồi retry các document Failed (KE-TEC-TSP-02-12).
- Không hành động: lỗi TikTok post 11001002 và 11031002 xảy ra sau khi SO và DO đã có trong Hybris (KE-TEC-TSP-02-13).
**Chỉ một Retry.** Bấm Retry một lần, chỉ sau khi sửa nguyên nhân và kiểm số tiền. Số tiền bị cộng lại mỗi lần bấm; SDSAP từng thấy order vượt một tỷ (KE-TEC-TSP-02-09; handover 27/10). Re-push order chưa vào Hybris qua portal là vận hành bình thường CoE làm. Tech common rules còn để mở câu hỏi PC cho portal re-push, nên ghi sự đồng ý của Sub-Lead lên ticket. Mọi thay đổi Hybris production cần PC duyệt. Checker mục 13: portal status không còn Failed, một retry, số tiền bằng marketplace.

### 3. Escalate case 3PD
| Tình huống | Escalate tới | Follow-up |
|---|---|---|
| Middleware không gọi Hybris, hay chức năng middleware hỏng | Vendor middleware (CoE tạo support ticket Logicbroker/Intrepid), báo RHQ; lỗi Bifrost, API Hybris và MSA: RHQ Platform | Mỗi 2 ngày làm việc; bridge nếu P0 |
| Defect code Hybris (split, mapping, số tiền FI) | Development partner qua TEC-OWN-01 | 2 ngày làm việc (P0–P2), 4 (P3) |
| Marketplace từ chối update hay hiện sai status | Chủ 3PD của subsidiary | Mỗi 4 ngày làm việc |
| FI posting bị từ chối | FI của subsidiary, rồi development partner | Mỗi 2 ngày làm việc |
| Cả market hay thiệt hại >500 USD | Tech Lead, COE-INC-01 | Mỗi 30 phút trên bridge |
Known error khớp trước: KE-01 order kẹt ở order split; KE-02 404 "order not found"; KE-03 order chờ kết quả fraud (cập nhật case không tới service); KE-05 không FI posting hay số tiền 0 trên order huỷ; KE-06 freebie thiếu trong NERP khi sản phẩm chính đã ship (SO riêng chỉ sau khi logistics xác nhận).
> Clock Tech dừng ở SYSTEM SUPPORT khi vendor middleware, team MSA hay partner làm việc. Nhịp follow-up vẫn chạy.

### 4. Điều tra Rewards: phân loại và kiểm
TEC-REW-02 xử lý vấn đề điểm Samsung Rewards trên order: 226 ticket 2026, ~25/tháng, một market mỗi ticket. Mặc định P3 (40h, nội bộ 26h). P2 chỉ khi credit/refund hỏng cả market hay site, có bằng chứng; batch hằng ngày có ngày vẫn P3. Doer: Level 2 (Level 1 chuẩn bị). Checker: engineer certified thứ hai, bắt buộc. Approver: RHQ qua PC; programme owner xác nhận điểm bằng văn bản.
| Variant | Dùng khi | Kiểm đầu (read-only) |
|---|---|---|
| V1 Chưa cộng điểm sau hoàn tất (~42%) | Order completed, không điểm | Order và consignment COMPLETED; Rewards Enrollment true; ngày hoàn tất; lần chạy cuối `<cc>MktCPIOrderOutboundSyncCronJob` sau hoàn tất |
| V2 Chưa hoàn điểm sau huỷ/return | Điểm chưa về | Mọi consignment CANCELLED; hàng journal của refund trước đó |
| V3 Bị trừ điểm không có order | Payment lỗi hay bỏ checkout | Không có order; `<cc>-tokoAbandondCartRewardRefundJob` đã chạy từ lúc bỏ |
| V4 Re-interface | Phía Rewards thiếu transaction/status | Journal: không hoặc một hàng requestType U có returnCode S |
| V5 Số điểm, tier, giới hạn bị tranh chấp | Khách nghi ngờ số điểm | Luật earn, cap, booster, `toko.rewards.*`, PointsInfo |
Route ra: ước tính cart 0 ở checkout → TEC-TSP-05; setting earn → TEC-REW-01; booster → MER-PRM-10; huỷ chưa xong → TEC-ORD-02. Định danh account chỉ ở protected field, không trong comment.
**Ví dụ (MY, V1).** MY gửi order completed chưa cộng điểm. Mỗi order: status COMPLETED, consignment COMPLETED, Rewards Enrollment true. Trong HAC đọc `orderCompletedDate` và `orderOrGerpCompletedDate`; trên staging 41/348 order COMPLETED từ 2026-10-01 thiếu `orderOrGerpCompletedDate` (KE-TEC-REW-02-01). Thiếu ngày: lấy từ bằng chứng NERP của requester, Checker xác nhận, Level 2 đặt sau khi RHQ duyệt PC. Đã interface nhưng không cộng không phải lỗi ngày: sang SYSTEM SUPPORT.
> Trường ngày hoàn tất nào job earn cần và trường nào được sửa còn mở (KT-1). Tới khi KT trả lời, ghi cả hai trường vào bảng before và để Tech Lead quyết.

### 5. Điều chỉnh điểm có duyệt
BiPlus không hoàn tác được refund điểm: điểm refund nhầm chỉ programme owner đảo được. Nên mọi điều chỉnh là Normal change có PC duyệt, peer check input và kết quả, và không chạy trước duyệt.
| Bước | Doer | Checker |
|---|---|---|
| Huỷ hoàn tất | Mọi consignment CANCELLED; nếu kẹt, link TEC-ORD-02 và không bao giờ refund song song | Huỷ đã xong |
| Lịch sử refund | Journal (VQ-9): requestType C, result SUCCESS, returnCode S nghĩa là đã refund | Không refund trước đó |
| Input | Định danh account, transaction ID, approval ID, điểm đối chiếu screenshot record Rewards | Input = record Rewards |
| Conversion factor | Từ log redemption Kibana (PointBalance / ExchangedAmount); không dùng factor market khác | Factor tính lại |
| PC và chạy | PC duyệt; script thư viện có số PC và COEC dòng đầu; dry run nếu version có | PC duyệt, header script |
| Kết quả | Một dòng kết quả mỗi dòng input; phân loại lỗi theo return code | Kết quả khớp |
V3 (không có order) thêm bước: lấy duyệt bằng văn bản của programme owner vì không có order làm mỏ neo cho refund.
Return code: RWD2N3008 "not enough cancelable points" = đã refund: đưa lịch sử và đóng. RWD2N3004 "not enough point to cancel" = số dư thấp hơn refund: ON HOLD SUBSIDIARY, programme owner quyết. Mã khác (RWD2N3002, RWD2N3003, RWD0N3002, RWD0N1001, RWD3N0002) chưa có nghĩa tài liệu hoá: không tự giải quyết. Dòng log "token not available or expired" là bình thường; đọc dòng cuối.
Escalate: đã interface nhưng chưa cộng → team nền tảng Rewards qua programme owner (SYSTEM SUPPORT nếu cần SDS India), mỗi 4 ngày làm việc; job earn/refund không chạy cho cả market → RHQ Platform và SDS India, mỗi 2 ngày làm việc.
> TEC-REW-02 nói refund script cần Level 2; Level 1 certified có được chạy không còn mở (KT). Quyền BiPlus vào back office Rewards cũng mở (KT-10): tới đó làm việc từ screenshot của requester.
Handover liên quan: Day 3 3PD Ticket Handling and Middleware (27/10: document Failed, cảnh báo Retry, middleware từng market; bundle split và dòng giveaway); SC+ MX and CE on 3PD Platform (28/10: Tech kiểm luồng order và XML payload sang NERP; item category SG YSNA); Order Remediation (27/10: bước order process, tab Administration › Order Process, chạy lại một bước); Kibana Log (trace PO ID cho order 3PD); Rewards Enable Rewards for Site (30/10: bật Rewards cho site ở cả HQ Rewards System và TokoConfigProperty; không có điểm để test trên staging/production); All SEAO Cronjob (job GCRM và cấp điểm, không rerun khi chưa duyệt).

## Quiz (đáp án)
1 PH gửi 18 order TikTok Shop kẹt trước shipping request; subsidiary bảo "re-push hết ngay" → **B: đăng template A ("không re-push hay cancel trong lúc này"), dựng order table, ghi nguyên nhân trước mọi push**. 2 Order ở trong Hybris, business process cho thấy bước lỗi `splitOrder`, log không lỗi tích hợp → **C: xử lý theo runbook TEC-MON-02 (V7) và link, hoặc re-route nếu không còn câu hỏi tích hợp**. 3 Order huỷ TH có FI posting số tiền 0 → **B: không gửi lại; nêu lỗi mapping, báo FI subsidiary, gửi lại từng order chỉ sau fix, FI xác nhận**. 4 Thông báo middleware trả 404 "order not found", kiểm gì đầu tiên → **A: order nằm dưới store/PO khác, hoặc lời gọi create lỗi trước đó**. 5 MY: order COMPLETED, mọi consignment COMPLETED, Enrollment true, ngày hoàn tất đủ, job order SUCCESS sau hoàn tất, vẫn không cộng điểm → **C: đã interface nhưng chưa cộng: đưa order, ngày, lần chạy job cho team nền tảng Rewards qua programme owner (SYSTEM SUPPORT nếu cần SDS India)**. 6 Trước khi refund điểm order SG đã huỷ, journal có requestType C result SUCCESS returnCode S → **B: đã refund: đưa lịch sử và đóng; không bao giờ refund lần hai**. 7 Cart AU bị trừ điểm, payment lỗi, không có order → **B: kiểm job refund abandoned-cart, lấy duyệt bằng văn bản của programme owner, rồi refund theo V2 bước 4–8**. 8 Refund script dòng SG lỗi RWD2N3004 → **C: số dư thấp hơn refund; ON HOLD SUBSIDIARY, programme owner quyết** (A là RWD2N3008). 9 Order Lazada PH Failed trong Logicbroker "inactive SKU", Merch đã kích hoạt SKU, Retry đầu như không làm gì → **B: dừng, kiểm số tiền document và order trong Hybris trước; không Retry lần hai** (số tiền cộng lại mỗi lần bấm, KE-TEC-TSP-02-09).

## Practice
**PR-TEC-P3.3-1. Case tích hợp: order 3PD kẹt** (20'; giấy; case mô phỏng dựa trên ví dụ TSP-02: danh sách 8 order TikTok Shop PH một ngày, kèm screenshot Backoffice từng order, kết quả business process và đoạn log theo PO ID; không dữ liệu khách). Làm: (1) đặt priority kèm lý do; (2) dựng order table và đánh dấu từng dòng; (3) nêu hop lỗi và bằng chứng; (4) nêu owner và hành động kế, gồm cần gì trước mọi push; (5) viết dòng escalate với nhịp follow-up nếu cần. **Pass:** hop lỗi và owner đúng mọi order theo đáp án facilitator; P2 với lý do "order kẹt trước shipment"; không plan push trước khi có nguyên nhân văn bản, xác nhận chưa ship của subsidiary và PC duyệt; lỗi xử lý order nội bộ route sang TEC-MON-02; nhịp follow-up khớp TEC-TSP-02 §2.10.
**PR-TEC-P3.3-2. Case tích hợp: refund Rewards** (20'; giấy; batch SG V2 mô phỏng 4 dòng: status order, status consignment, hàng journal (requestType, result, returnCode), giá trị screenshot back office Rewards, một dòng log redemption Kibana). Với mỗi dòng quyết định: refund, đóng (đã refund), chờ TEC-ORD-02 hay programme owner. Với dòng cần refund, điền bảng input (transaction ID, approval ID, điểm), tính lại conversion factor, liệt kê PC phải chứa gì. **Pass:** mỗi dòng đúng quyết định theo đáp án; không dòng nào có journal C/S bị refund; dòng consignment chưa CANCELLED link TEC-ORD-02 và không refund song song; conversion factor suy ra từ log (SG = 500); nội dung PC nêu script thư viện, số PC và COEC dòng đầu, dry run nếu có, và nói rõ BiPlus không đảo được refund.
> Material gap: chưa có lab ticket cho 3PD và Rewards; hai lab ticket sẽ được viết. Tới đó facilitator dựng hai case giấy từ ví dụ TEC-TSP-02 và TEC-REW-02 với dữ liệu mô phỏng và đáp án.
