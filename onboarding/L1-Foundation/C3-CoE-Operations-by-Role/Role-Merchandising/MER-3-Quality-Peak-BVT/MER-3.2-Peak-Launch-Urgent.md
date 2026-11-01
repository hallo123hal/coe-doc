# MER-3.2 Peak, launch, campaign; urgent requests

> Nguồn: page 2483192130 · 65 phút (Study 25' · Demo 10' · Quiz 10' · Practice 20') · Lecture + tabletop một đêm peak; facilitator: Merch Lead (Peak Lead) · Tài liệu chính: MR-07. Không cần hệ thống; dùng các trang QBH8 đã có trong RESOURCES (trang flagship RHQ hạn chế quyền, xin qua Lead mất 2–3 ngày). Cần xong G3.3, G2.6, MER-1.1, MER-3.1.

## Mục tiêu
Lập lịch go-live theo giờ VN và phân checker cho đêm peak nhiều market, gồm deadline cùng ngày; phân loại thay đổi trong freeze 48h và freeze flagship: được / cần ngoại lệ / cấm; xử lý QA FAIL sau giờ go-live và request khẩn đêm peak; mô tả vai trò, kênh, nhịp update của war room và việc sau peak.

## Thuật ngữ
**Peak** (campaign 11.11, Black Friday, Cyber Monday, 12.12; ra mắt flagship; mùa lễ); **T-14…T+1** (lịch chuẩn bị tính lùi từ ngày D); **QA cut-off 17:00** (hạn nội bộ: setup go-live tối nay phải tới QA trước 17:00 ICT; RHQ chưa xác nhận); **QA layer 2** (check lại giá trị liên quan tiền do QA Lead/Sub-Lead khác người layer 1); **War room** (khu ngồi chung ở trung tâm Hà Nội đêm peak — không có war room ảo); **Peak Lead** (Merch Lead/Deputy chỉ huy đêm peak: quyết go/no-go từng market, duyệt E4 cấp 2); **Go-live coordinator**; **Restricted SKU** (SKU flagship chưa công bố, quyền xem/setup hạn chế); **Knox Approval Post Sign-Off**; **Daily scoreboard** (báo cáo gửi RHQ sáng sau đêm peak).

## Nội dung
### 1. Các loại peak và mùa peak đầu tiên
3 loại: campaign (go-live 00:00 local nhiều market cùng đêm); ra mắt flagship (~2 lần/năm, embargo, nhiều lớp freeze, UAT ở Clean Room); mùa lễ (Tết, Giáng sinh, Năm mới; nhân sự tối thiểu theo RFP 3.5). Mùa đầu trùng giai đoạn chuyển giao: **11.11 (T4) ở Sprint 2** — SDSAP còn làm, BiPlus quan sát và ghi bài học cho checkpoint 14/11; **Black Friday 27/11 (T6) ở Sprint 4** — 2 lớp QA, thêm bench; **Cyber Monday 30/11 = ngày takeover**, go-live NZ/AU rơi tối Chủ nhật 29/11 khi ca chỉ có Shift Leader + 1 người; **12.12 (T7)** — peak đầu tiên BiPlus chạy 100%, Merch Lead có mặt tại chỗ; wave 1 flagship dự kiến cuối 01/2027; roster Tết thống nhất với RHQ trước 15/12/2026.

### 2. Chuẩn bị T-14 → T+1
T-14: gom lịch campaign 8 market & kênh, dự báo tải so với 80% capacity, rà lịch release (BVT), nháp roster, báo hạn brief. T-10: phân loại ticket, ghi Knox path. T-7: brief đủ, roster chốt, danh sách war room. T-5: internal check rồi build. T-3: QA layer 1. T-2: bắt đầu freeze, PC duyệt, Knox gửi. T-1: QA layer 2, duyệt, diễn tập rollback cho E4. D: war room. T+1: kiểm end time, trạng thái order, backlog.
Hai lớp QA chỉ áp dụng cho việc Merch: layer 1 là QA Team Member (checklist, SKU scope, simulator); layer 2 là QA Lead hoặc Sub-Lead khác, re-check giá trị liên quan tiền sau layer 1 PASS và trước khi duyệt. Ca QA 04:00 re-check các thay đổi R3 đã live qua đêm.

### 3. Đêm peak: theo thứ tự giờ go-live, QA cut-off 17:00
Đêm peak ở Hà Nội kéo dài 18:00–02:00: NZ 18:00, AU 20:00, SG/MY/PH 23:00 (ca E), VN/TH/ID 00:00 (ca N, đúng giờ bàn giao). Mỗi go-live có go-live check, post-change check và 2h theo dõi; 23:00–01:00 chạy song song hai cửa sổ theo dõi. Shift Leader ca E viết handoff 23:30 và theo dõi SG/MY/PH tới 01:00 hoặc giao bench. **Ưu tiên theo giờ go-live, không theo market; go/no-go từng market; không market nào chờ market khác; không có "bật trước, check sau".**

| Hạn trong ngày go-live (giờ VN) | Phải xong |
|---|---|
| Trước 12:00 | Build xong, có internal check |
| Trước 14:00 | Setup E4 đã tới QA |
| Trước 17:00 | Mọi setup đã tới QA; E4 có duyệt cấp 2 |
| 1 giờ trước go-live | QA PASS, Shift Leader duyệt, Knox đã gửi, ghi tên người check & người monitor |

### 4. Freeze: 48 giờ campaign và freeze flagship
- **Freeze 48h trước 11.11, 12.12, Black Friday** (flagship theo freeze plan riêng): chỉ thay đổi đã được RHQ duyệt + thay đổi khẩn trong incident; ngoại lệ ghi bằng chứng duyệt (ai duyệt, ngày, phạm vi, link) trong thân ticket; **stock luôn được cập nhật**; thay đổi phụ thuộc enhancement chưa BVT sign-off không go-live.
- **Flagship freeze (VD QBH8) — Hybris Soft Freeze:** chỉ đổi promotion/giá của rule hoặc SKU đang có, kèm PUMI ghi rule ID và giá trước/sau; không promotion mới, không PUMI "blanket" (ở đây PUMI là phê duyệt đổi giá/promotion của freeze plan QBH8; CM-07 và glossary dùng PUMI cho form data request — quan hệ giữa hai nghĩa còn mở với RHQ, CM-13 §20.2).
- **Hard Freeze:** chỉ cho phép các cập nhật tay trong Hybris: stock; EPP domain filter, retiree, access code, employee ID (4 việc này của Tech → move COEC); Approval & Sales Status; Block Stock & Block Price Import; CSM; Stock Override; pre-order dates; overselling weeks; AEM Super Sync. **Không đổi gì ở AEM EPP 2.0 và Shop App**, kể cả trang CMS EPP 2.0 (QBH8 2; MER-2.5 áp dụng cùng luật).

### 5. Flagship: bảo mật và Knox sau sign-off
Ký cam kết; không chụp, ghi hình, chia sẻ; ai vi phạm bị loại khỏi team ngay; không dùng AI với sản phẩm embargo. Sau sign-off chạy **Knox Approval Post Sign-Off** cho promo rule, special price, discount row có restricted SKU (lùi start time 1 giây để kích hoạt Knox). Publish chung batch với promo không có SKU flagship thì **không được bỏ Knox**.

### 6. Request khẩn, war room, sau peak
- **QA FAIL sau giờ go-live: không go-live** (không phải urgent). Ticket last-minute thật vẫn đi QA nếu QA kịp; chỉ khi QA không kịp mới áp control tối thiểu: internal check + sanity (R3), Shift Leader duyệt, người thứ hai check lúc go-live + order monitor, comment + label last-minute, Knox cho giá & promotion (CM-07 §3.6, quyết định 22/10/2026; CM-13 §8.2 còn ghi chờ CEO — đã yêu cầu sửa). Ngay cả control tối thiểu cũng không kịp → báo subsidiary bằng văn bản và đề xuất giờ mới. Mỗi tuần đếm ticket `LastMinRequest` gửi Lead.
- **War room:** vai trò Peak Lead, Shift Leader, Go-live coordinator, monitor, QA, Tech standby, người nói Thái & Bahasa. Kênh: Jira là nguồn sự thật; Mattermost với RHQ; Jira comment với subsidiary; bridge cho incident; cấm Zalo và kênh cá nhân. Nhịp: đăng peak plan trước 17:30; 3 dòng cho mỗi go-live; báo RHQ incident trong 30' (Critical) / 2h (High); gửi daily scoreboard sáng hôm sau.
- **Sau peak:** T+1 kiểm end time 23:59 local (NZ 17:59, AU 19:59, SG/MY/PH 22:59, VN/TH/ID 23:59 giờ VN); nhân viên ca đêm nghỉ 48h; post-peak review trong 3 ngày làm việc, 60 phút, không đổ lỗi; mỗi CAPA có owner & deadline; bài học vào checklist/runbook trong 3 ngày làm việc.

### Điểm đáng nhớ từ KT
Mỗi launch có RHQ Online Content Playbook (đọc trước khi setup). Add-on page: HQ đặt tab & SKU, thêm được nhưng không được bỏ. Trang flagship chỉ người làm flagship xem được; freeze plan đổi theo từng flagship. Hard freeze EPP 2.0 CMS: bản KT nói cho sửa homepage/offer/detail nhưng không publish nội dung flagship — **kế hoạch bằng văn bản thắng**: QBH8 hard freeze không cập nhật gì ở AEM EPP 2.0/Shop App. Hybris soft freeze: PUMI một thay đổi một lần. "Hot freeze" 2–3 ngày sau Unpacked chính là Hybris hard freeze (CM-13 §19.2); stock luôn cập nhật được. Subsidiary không mở được trang freeze plan → CoE đưa approval path và nội dung cần điền; bằng chứng duyệt ghi trong thân ticket.

## Quiz (đáp án)
1 Go-live 00:00 giờ AU (AEDT) 27/11/2026 → **20:00 ngày 26/11 giờ VN** (AEDT = UTC+11). 2 Ticket PH QA FAIL 22:30, go-live 23:00, chưa PASS → **không go-live; đề xuất giờ mới**. 3 Peak Lead muốn ở nhà theo dõi qua điện thoại → **không: phải có mặt tại trung tâm trong 60'**. 4 Hard Freeze flagship, việc được phép → **đổi pre-order dates**. 5 Soft Freeze, subsidiary xin đổi giá 2 SKU trong promotion có sẵn → **PUMI có rule ID, giá trước/sau**. 6 Hạn cuối mọi setup trong ngày go-live tới QA → **17:00 giờ VN**. 7 Sau sign-off publish batch có cả promo SKU restricted và promo SKU thường → **không bỏ được Knox**.

## Practice
- **PR-MER-3.2-1** (giấy, 8'): bảng giờ go-live VN, ca phụ trách, checker, monitor cho Cyber Monday 30/11/2026 ở 8 market — NZ 18:00 và AU 20:00 ngày 29/11; SG/MY/PH 23:00 ngày 29/11 (ca E); VN/TH/ID 00:00 ngày 30/11 (ca N); giải thích 29/11 là Chủ nhật chỉ có Shift Leader + 1 người, 30/11 là ngày takeover nên Merch Lead phải xác nhận thêm người.
- **PR-MER-3.2-2** (6'): phân loại 6 request trong Hard Freeze — cập nhật stock (được); đổi special price có sẵn (cần ngoại lệ: bằng chứng duyệt trong thân ticket + Knox lại); tạo promotion mới (không); thêm retiree vào EPP (được trong freeze nhưng là việc Tech → move COEC, A.11); sửa banner Shop App (không); đổi pre-order dates (được).
- **PR-MER-3.2-3** (6'): 22:30 đêm Black Friday ticket PH giảm giá 3 SKU go-live 23:00 bị QA layer 2 FAIL vì sai end time: viết comment tiếng Anh cho requester (giờ local + VN, đề xuất giờ mới), nêu ai cần báo, và dòng handoff note lúc 23:30. Pass: không go-live, không gắn `LastMinRequest`; requester được báo bằng văn bản và Peak Lead được báo; giờ mới đề xuất sau khi sửa và có QA PASS mới; handoff ghi ticket, việc đang chờ, ai tiếp tục và khi nào.
