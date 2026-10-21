# CM-01 Welcome pack: Samsung SEAO và Ops CoE

> Tóm tắt trang Confluence CM-01 (v0.2, bản nháp 21/10/2026). Chủ sở hữu/rà soát: Service Delivery Manager (SDM); ký duyệt: CEO; biên soạn: CoE Office. Người đọc: toàn đội Ops CoE. Là **tài liệu đầu tiên** người mới đọc; bức tranh chung trước khi đọc CM-02…CM-11 rồi 4–7 tài liệu của team (MR/TC/QA). Ví dụ trong tài liệu là dữ liệu giả lập.

## 1. Samsung SEAO, RHQ, 8 subsidiary
- **SEAO** = South East Asia & Oceania. **RHQ** (Singapore) là *product owner* của CoE: quyết định ưu tiên, duyệt mốc chuyển đổi, nhận báo cáo SLA, chủ trì governance. **Subsidiary** = công ty con từng thị trường, nơi phát sinh yêu cầu; người gửi = **requester**.
- 8 thị trường: VN, TH, ID (UTC+7 – bằng Hà Nội), MY, SG, PH (+1h), AU (Sydney +4h), NZ (Auckland +6h, tháng 10–3 do DST). Tech team: A (VN, TH, ID, NZ), B (MY, SG, PH, AU). Merchandising backup PIC: Sub-Lead 1 (VN), 2 (TH, ID), 3 (MY, SG), 4 (PH + EPP/SMB/O2O/3PD), 5 (AU, NZ).
- Vì 03:00 Hà Nội = 09:00 Auckland nên Merchandising trực 24/7.
- Các kênh bán: B2C, **EPP** (nhân viên đối tác), **SMB**, **O2O**, **3PD**, **Shop App**, **EA App**.

## 2. Nền tảng
- **eStore** chạy trên: **SAP Commerce (Hybris)** – Merchandising dùng Backoffice (Back Office 2.0, có *promotion simulator*), Tech thêm **HAC**, ImpEx, Groovy; **AEM** (nội dung trang); **Shop App CMS**. Đơn hàng → **NERP** (ERP Samsung).
- Mọi yêu cầu/bằng chứng nằm trên **Jira/Confluence của Samsung**; cấm dùng hệ thống BiPlus chứa dữ liệu Samsung.
- Hai môi trường: **Production** và **Staging** (thử, enhancement, BVT, đào tạo, Tech chạy thử ImpEx/script). Merchandising thiết lập hằng ngày **trên production** (promotion: setup → publish sang simulator → test → publish live).
- ⚠ Trạng thái Jira **STG SETUP** chỉ nghĩa "CoE đã nhận và đang thiết lập" – vẫn làm trên production. **PRD SETUP** tương tự.

## 3. Ops CoE là gì
- **CoE** = Center of Excellence: gom việc vận hành eStore vào một đội, một quy trình, một bộ chỉ số. Samsung công bố RFP; BiPlus nộp proposal v9.4, deck v08Oct, đã trúng thầu.
- **6 thách thức RFP** → câu trả lời của CoE: nhân sự ổn định (Academy, bench 6); liên tục khi vắng (backup có tên mỗi ghế/giờ); SLA ổn định (đồng hồ, cảnh báo 50/70/85/95%, Shift Leader); chất lượng (R1/R2/R3, QA độc lập, Doer–Checker–Approver, PC ticket); kỷ luật BVT; governance/compliance.
- **3 trụ**: **Merchandising** (Hybris/AEM/Shop App CMS; 17 nhóm việc, 43 sub-task; tiếng Anh + Bahasa + Việt + Thái), **Tech** (project Jira COEC; L1/L2; sự cố, ImpEx, query, script; làm việc với Samsung L2/L3), **QA** (kiểm độc lập việc Merchandising; không BVT, không QA cho Tech).
- **Service catalogue 143 service** (Class A ~30 chiếm đa số khối lượng, B, C); mỗi service có runbook, cổng QA, người được chứng nhận; mức sẵn sàng **SRL0–SRL5**. Chưa có runbook → hỏi Sub-Lead/Lead, không tự nghĩ cách.
- **3 lớp**: Execution (COE Lead + 3 team, 48 ghế tính phí), CoE Operations Office, Commitments. **5 nguyên tắc**: Workforce is a system; mỗi ghế/giờ có backup; Doer ≠ Checker ≠ Approver; đo cái Samsung đo; skin in the game.

## 4. Các bên liên quan
| Bên | Vai trò / kênh |
|---|---|
| RHQ (Singapore) | Product owner; COE Lead là đầu mối; họp tuần/tháng/quý + 3 checkpoint; **Mattermost 100%**; duyệt ticket ON HOLD RHQ; **Oliver Leung** (HOD cụm SEAO) duyệt PC ticket |
| HQ (Suwon) | Ban hành quy định ImpEx/Groovy/add-on page; ON HOLD HQ |
| Subsidiary | Tạo/duyệt ticket Shop Merchandising, trả lời ON HOLD SUBS, xem bằng chứng QA ở REVIEW SETUP; Market Owner = Market PIC; **chỉ qua comment Jira** (kênh chat chờ RHQ; Knox Messenger nếu được cấp) |
| Samsung L2/L3 (SDS India) | Nhận **Maintenance Request** + evidence pack khi Tech không tự sửa; ticket COEC sang SYSTEM SUPPORT; **CoE vẫn là owner**, theo dõi High 2 ngày/Medium 4 ngày/Low hằng tuần |
| Đội phát triển enhancement | CoE (PIC BVT) test, bằng chứng trên Confluence |
| SDSAP (đơn vị vận hành hiện tại) | KT qua MS Teams, bàn giao; dịch vụ kết thúc **30/11/2026**; không so sánh cách làm cũ/mới trên kênh chung; câu hỏi bàn giao ghi gap log |

Kickoff 20/10/2026: RHQ không đào tạo nghiệp vụ; SDSAP trình bày KT; BiPlus tự xây năng lực qua Academy.

### Jira – ai làm trên đâu
| Loại | Ai tạo | Ai xử lý |
|---|---|---|
| Shop Merchandising (1 workflow chung 8 nước) | Subsidiary | Merchandising, QA |
| COEC (COE Centralization SEAO) | Merchandising, QA, HQ, subsidiary | Chỉ Tech |
| Maintenance Request | Tech | SDS India |
| Enhancement | Đội phát triển | Đội phát triển; PIC BVT của CoE test |
| PC ticket | Tech | Oliver Leung duyệt |

### Đồng hồ SLA – chỉ chạy khi việc ở phía CoE
| | Shop Merchandising | COEC (Tech) |
|---|---|---|
| Bắt đầu đo initial response | APPROVED-ES | NEW |
| **Tính** | STG SETUP, QA REVIEW, PRD SETUP, ON HOLD COE | ASSIGNED, IN REVIEW, IN PROGRESS, QA REVIEW, WAITING QA |
| **Dừng** | ON HOLD SUBS, ON HOLD RHQ, REVIEW SETUP | ON HOLD SUBSIDIARY, SYSTEM SUPPORT, ON HOLD HQ, ON HOLD ES |
| Không tính | PLANNING(+REVIEW), PENDING LAUNCH, LAUNCH VERIFICATION, CLOSED, INVALID | LAUNCH VERIFICATION, CLOSED, INVALID |

Quy tắc: **chuyển trạng thái = xác nhận nhận** (APPROVED-ES→STG SETUP; NEW→ASSIGNED), comment không đủ. Hỏi subsidiary: comment + ON HOLD SUBS + **giao Assignee cho subsidiary**; không dùng chỉ để dừng đồng hồ; khi subsidiary trả lời (thường chỉ comment) → chuyển ngay về STG SETUP. ON HOLD COE vẫn tính SLA. INVALID đóng hẳn (muốn làm lại thì clone).

### QA / BVT / PC ticket
- Merchandising: QA Team kiểm (R3; R2 có gate), Shift Leader duyệt, subsidiary xem bằng chứng ở REVIEW SETUP; QA time nằm trong SLA ticket (BiPlus đặt OLA nội bộ). Ngoại lệ **last-minute request**: comment "Last minute request, please QA on your own when it goes live…", đứng chờ hỗ trợ, đếm báo họp tuần RHQ.
- Tech: tự QA trên staging, Tech khác kiểm khi rủi ro cao, Oliver Leung duyệt PC ticket. Không có QA Team trong luồng Tech.
- **BVT**: RHQ báo cửa sổ trước tối đa 1 tuần, ngày cố định; **100% test case pass** mới go-live (99% là không). PIC dự kickoff, test từ ngày đầu, cập nhật Confluence hằng ngày.
- **PC ticket**: không có thì **không đổi gì trên production, kể cả việc 5 giây**. ImpEx/Groovy phải có dòng ghi số PC ticket + ticket COEC gốc, thiếu = **strike**. Chờ duyệt: COEC → ON HOLD HQ ("PC ticket pending"). P0/P1 gấp thì nhắn Oliver qua Mattermost.
- Chưa rõ: PC viết tắt gì/ở project nào/mẫu; ai duyệt khi Oliver vắng 23/10–9/11. Vai trò BVT Coordinator (proposal gán QA Sub-Lead 1) mâu thuẫn với việc QA không tham gia BVT → tạm: Merchandising/Tech Lead chỉ định PIC; đề xuất một Tech Sub-Lead giữ lịch BVT; CEO chốt.
- **Merchandising cần Tech** (vd 500.000 voucher cần ImpEx): không chuyển ticket; tạo ticket COEC mới, issue link, chuyển ticket gốc ON HOLD COE (đồng hồ vẫn chạy → phải đôn đốc Tech). Ticket nhầm team: *move* ticket (chờ RHQ xác nhận).

## 5. Tổ chức BiPlus CoE (56 người)
48 ghế tính phí (COE Lead 1, Merchandising 29, Tech 9, QA 9) + CSM + SDM + bench 6 (4 Merch, 1 Tech, 1 QA) + CoE Operations Office.
- **COE Lead**: tại RHQ Singapore từ 1/12/2026 (SDM làm thay), đầu mối duy nhất với RHQ. **CSM** (Singapore): quan hệ RHQ/subsidiary, CSAT. **SDM** (Hà Nội, hotline 24/7): Transition Manager, Scrum Master 4 sprint.
- Merchandising: Lead (Hybris, duyệt E4, on-call ngoài 08–17), 5 Sub-Lead = Shift Leader (1 là Deputy Lead), 8 Market Owner, 15 Team Member (1 Thái, 1 Bahasa). Tech: Lead (nhận COEC, phân priority, rà thay đổi rủi ro cao, chỉ định PIC BVT), 2 Sub-Lead (Team A/B, L2, on-call 1/3 tuần), 6 Team Member. QA: Lead (có quyền trả ticket, đặt OLA), Sub-Lead 1 (Deputy, ca chiều), Sub-Lead 2 (dispatcher, sampling, test library, ca sớm), 6 Team Member. Bench: dự phòng đã đào tạo.
- **Operations Office**: Executive Sponsor David Bui (CEO), Workforce Lead Thảo (COO), SDM Quốc (CDO); CEO kiêm Process & Knowledge Lead/Atlassian Platform Eng/DevSecOps; Project Assistant, English Coach (2h/tuần, bài T2), HR.
- **Đợt vào làm**: W0 (15 lãnh đạo, 21/10), W1 (29, 23/10), W2 (12 gồm bench, 26/10). Quyền production theo đợt **sau chứng nhận**: 29/10, 6/11, 13/11, 20/11.

## 6. Lộ trình chuyển đổi (baseline RHQ từ 20/10/2026)
| Mốc | Nội dung |
|---|---|
| 20–21/10 | Kickoff; 21/10 RHQ training hệ thống đầu tiên (Oliver Leung) |
| 22–25/10 | Setup (tài khoản, thiết bị, khu bảo mật), **không làm live**; Day 0 Academy/T1; cần tài khoản Mattermost; quyền Confluence mất 2–3 ngày |
| 23–30/10 | KT từ SDSAP (MS Teams, ghi hình); 26–30/10 ~10 người thăm MY COE |
| 31/10 (T7) | **Checkpoint 1** – cho phép làm live |
| 2–8/11 Sprint 1 | Việc không ảnh hưởng doanh thu: Merch 20% / Tech 10% / QA 0% (shadow) |
| 9–15/11 Sprint 2 (CP2 14/11) | 40% / 30% / 60%; 11.11 vẫn do SDSAP |
| 16–22/11 Sprint 3 | 70% / 60% / 100%; tuần 24/7 đầu tiên |
| 23–29/11 Sprint 4 (CP3 26/11) | 90% / 90% / 100%; diễn tập takeover; Black Friday 27/11 hai lớp QA; CP3 = go/no-go |
| **30/11/2026** | **Takeover** 100% (Cyber Monday), SDSAP kết thúc; hypercare đến 31/12, 12.12 peak đầu, gate G4 |
| 28/02/2027 | Ngày 90, gate G5 |
Nhịp sprint: thứ Hai steering RHQ, stand-up đầu ca, scoreboard gửi RHQ mỗi sáng, thứ Bảy phân tích + retro. Khấu trừ Composite SLA từ 1/2027, nhưng SLA đo từ ngày đầu live.

## 7. Cam kết BiPlus
- **Resolution (RFP 3.3), đạt ≥ 97%/tháng**: Tech P0 4h (kể cả ngoài giờ), P1 8h, P2 16h, P3 40h, P4 120h; Merchandising & QA High 4h, Medium 16h, Low 24h (gồm cả bước QA; RHQ không đo SLA riêng cho QA).
- **Initial response**: 2h mọi priority (≥ 97%).
- **Composite SLA** = Resolution 75% + Response 15% + BVT pass 6% + Report completion 3% + User acceptance 1%; trung bình quý, 8 thị trường; < 97% bị khấu trừ 1–5% phí.
- **Mục tiêu nội bộ**: phản hồi 78 phút (P0/High 15', P1 30'); đạt 98,5%; ticket vào Jira trong 5 phút; lọc ticket không owner mỗi 30'; cảnh báo 50/70/85/95% thời gian SLA (assignee → Shift Leader/Sub-Lead → Lead → COE Lead báo RHQ).
- **Chất lượng**: R1 (text, banner, CMS), R2 (product setup, delivery, stock), R3 (giá, discount, promotion, voucher, payment, quyền); **E4** khi ≥ 10.000 USD, > 5 thị trường hoặc file giá ≥ 500 SKU.
- **An ninh**: dữ liệu chỉ trên hệ thống Samsung, bằng chứng QA tạo trên máy trạm → đính Jira, AI theo RFP 3.12, audit báo trước 3 ngày làm việc (xem CM-10).
- **Ngôn ngữ**: tiếng Anh; 4 tuần đầu mọi tin gửi subsidiary/RHQ được duyệt đến khi đạt 4 tuần + 50 tin đạt (T8).
- **Nhân sự**: báo vị trí trống trong 48h làm việc; thay trong 60 ngày (Lead/Sub-Lead) hoặc 45 ngày; không kiêm nhiệm; nghỉ > 3 ngày làm việc phải có backup.

## 8. Một ngày ở CoE
- **Merchandising 24/7, 3 ca** (giờ ICT): Đêm 00–08, Ngày 08–16, Tối 16–24; bàn giao 00:00/08:00/16:00, chồng ca 15', **handoff note viết**. Quân số T2–T6: Đêm SL+1, Ngày SL+14 (8 Market Owner + 6 TM), Tối SL+4; T7: SL+1 / +5 / +2; CN & lễ: SL+1 mỗi ca.
- **Tech L1**: ca sớm 04–12 và chiều 11–19 (T2–T7), mỗi ca 2 người (1 Team A + 1 Team B); **L2** 08–18 (5 người ngày thường, 2 người T7); on-call 19:00–04:00 và CN.
- **QA** (chỉ việc Merchandising): ca sớm + ca chiều T2–T6; CN chỉ on-call. Giờ QA tạm theo deck v08Oct/dashboard v1.4 (proposal v9.4 ghi khác); ngưỡng 17:00 cho yêu cầu gấp, hạn gửi promotion (2 hay 3 ngày), người kiểm queue CN 09:00/17:00 – **chờ RHQ/CEO chốt**.
- **On-call**: trả lời trong **15 phút**, có mặt tại trung tâm Hà Nội trong **60 phút**, không xử lý từ nhà.
- Mẫu ngày Team Member Merchandising: 07:45 có mặt + đọc handoff → 08:00 stand-up → nhận ticket (APPROVED-ES→STG SETUP), làm theo runbook, ghi evidence → 15:30 cập nhật mọi ticket + handoff → 16:00 chồng ca.
- **Handoff note tối thiểu**: ticket đang làm + next action, ticket sắp chạm cảnh báo, ticket đang chờ (ON HOLD SUBS/COE, SYSTEM SUPPORT, PC pending), COEC ở NEW chưa nhận, go-live ca tới, BVT notification, sự cố mở, người vắng.
- **Công cụ**: Jira (mọi ticket, trao đổi subsidiary), Confluence (runbook, handoff, báo cáo, BVT), Mattermost (100% RHQ), email Samsung, MS Teams (chỉ KT), Hybris/HAC/AEM/Shop App CMS (chỉ service đã chứng nhận, không dùng tài khoản chung).
- **Khu làm việc bảo mật** (làm hằng ngày, 24/7) ≠ **Clean Room** (phòng UAT flagship của RHQ, 40 chỗ chia 2 được, ~4 phòng họp cho 8 subsidiary, 20–25 chỗ cho đội lõi; dùng vào các ngày "VN Clean Room"; cách vận hành RHQ sẽ hướng dẫn sau).

## 9. Mười quy tắc vàng
1. Không làm remote (kể cả on-call).
2. Dữ liệu Samsung chỉ trên hệ thống Samsung; không chụp bằng điện thoại; bằng chứng QA tạo trên máy trạm → đính Jira.
3. Không đưa dữ liệu Samsung vào AI; chỉ dùng công cụ được duyệt.
4. Mọi yêu cầu vào Jira trong 5 phút; không làm ngoài ticket.
5. Không ticket nào không owner; lọc mỗi 30 phút.
6. Doer, Checker, Approver là 3 người khác nhau.
7. Chỉ làm service đã được chứng nhận (L0–L3), đúng runbook.
8. Thấy rủi ro vỡ SLA/sự cố thì báo ngay; báo sớm không bị phạt, giấu mới bị phạt.
9. Bàn giao ca bằng handoff note viết.
10. Không backup, không nghỉ; vắng đột xuất báo Shift Leader/Sub-Lead trước giờ ca.

Ví dụ nổi bật: RHQ nhắn Mattermost nhờ kiểm banner → tạo ticket COEC trong 5 phút rồi mới làm; promotion go-live ngày mai mà 23:59 subsidiary chưa duyệt REVIEW SETUP → vẫn publish như thỏa thuận và comment "đã publish như đã thống nhất, chưa nhận phản hồi"; giá giỏ hàng thấp bất thường sau go-live → báo Shift Leader (Incident Manager tạm thời tắt promotion trong 30 phút đầu).

## 10. Hỏi ai, kênh nào
- Hỏi người gần nhất trước, việc khẩn báo ngay Shift Leader/Sub-Lead. Leo thang: Merchandising: Shift Leader → Merchandising Lead (on-call ngoài 08–17) → SDM hotline 24/7 → COE Lead; Tech/QA: on-call lớp 1 → Lead → SDM hotline.
- Danh bạ theo vai trò (roster công bố trước 4 tuần, cập nhật mỗi thứ Sáu trên trang CoE Confluence Samsung). **Còn phải điền**: số SDM hotline, số on-call, tên kênh Mattermost nội bộ, email nhóm CoE, cách báo vắng (SDM & Atlassian Platform Engineer điền trước 31/10).
- Kênh: comment Jira (mọi thứ về ticket + toàn bộ trao đổi subsidiary); Mattermost RHQ; Mattermost nội bộ; email Samsung; hotline/on-call cho việc khẩn. Chưa mở kênh chat riêng với subsidiary khi RHQ chưa cho phép.
- Trang auxiliary trên Confluence: danh sách Lead, nghỉ phép/lễ VN, roster, danh sách team, trang workflow ticket.
- FAQ: Mattermost nhờ làm gì → phải có ticket; ON HOLD SUBS (đã giao subsidiary) dừng đồng hồ, ON HOLD COE thì không; QA không kiểm Tech, không BVT; chưa có runbook → hỏi + gap log; tự làm khi đạt L2 sau tuần có giám sát (T6).

## Phụ lục
- **A. Checklist tuần đầu**: Day 0 nhận quyền khu bảo mật/máy trạm/buddy, onboarding bảo mật + T1 (20 câu, ≥ 90%, mọi câu trọng yếu đúng) + ký cam kết, kiểm tài khoản Mattermost/Confluence; Day 1 học SEAO/CoE/SLA/workflow; Day 2–4 CM-02…CM-09; Day 5 bài T2 và T3 (30 câu, ≥ 80%).
- **B/C. Câu hỏi kiểm tra** (13 trắc nghiệm + 6 tình huống) và đáp án: RHQ ở Singapore là product owner; 03:00 Hà Nội = 09:00 Auckland (tháng 11); STG SETUP = CoE đã nhận, làm trên production; High = 4h; mục tiêu phản hồi 78 phút; takeover 30/11/2026; Shift Leader duyệt (thêm Merchandising Lead với E4); lọc không owner 30'; ON HOLD SUBS dừng đồng hồ; Oliver Leung duyệt PC ticket; QA chỉ QA Merchandising.
