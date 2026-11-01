# QA-3.3 QA in peak and launch, and the boundaries between QA, BVT and Tech

> Nguồn: page 2483192727 · 50 phút (Study 12' · Demo/thảo luận 8' · Quiz 10' · Practice 20') · Lecture ngắn rồi thảo luận một đêm peak mô phỏng; facilitator: QA Lead cùng Merchandising Lead (Peak Lead) · Cần xong G4.3 (time zone 8 market), G2.6 (freeze, PC ticket, Knox), G6.1 (BVT), QA-3.2; chỉ cần Confluence + giấy.

## Mục tiêu
Quy đổi go-live 00:00 của 8 market sang giờ VN và tìm ai QA again cho từng wave; áp dụng các mốc trong ngày go-live (12:00, 14:00, 17:00, go-live − 1h) và luật hai lớp QA; phân biệt việc QA với BVT, bước QA của Tech, và kiểm Knox; xử lý đúng khi QA again trên production thấy lỗi.

## Thuật ngữ
**Peak** (giai đoạn tải cao: campaign 11.11/Black Friday/12.12, flagship launch, ngày lễ); **Peak Lead** (điều phối đêm peak, thường là Merchandising Lead); **Cut-off** (giờ trong ngày setup phải tới QA để go-live tối cùng ngày, VD 17:00 ICT); **Two QA layers** (K3: người thứ hai, không phải layer 1, kiểm lại độc lập các giá trị tiền); **War room** (phòng điều phối đêm peak tại trung tâm Hà Nội, không có war room ảo); **Post-change check** (kiểm storefront ngay sau go-live bởi người khác Doer, ≤30', E4 15'); **Order anomaly monitor** (theo dõi order mỗi 15' trong 2 giờ sau go-live); **T-14 … T+1** (đếm ngày quanh ngày sự kiện D).

## Nội dung
### 1. Ba loại peak và lịch 2026
Campaign (11.11, Black Friday 27/11, Cyber Monday 30/11, 12.12, cuối năm — nhiều market go-live 00:00 giờ địa phương cùng một đêm); flagship launch (có embargo, nhiều lớp freeze); ngày lễ (Tết, Christmas, New Year). Chồng lên lịch tiếp quản 2026: 11.11 rơi vào Sprint 2 — SDSAP vẫn xử lý thay đổi campaign, QA BiPlus làm 60% ticket thường ngày (CM-04 §2.5, §9.1); Black Friday ở Sprint 4 — BiPlus làm 100% với hai lớp QA; **Cyber Monday trùng ngày tiếp quản 30/11**, go-live NZ/AU rơi vào tối Chủ nhật 29/11 giờ VN khi ca chỉ có Shift Leader + 1 người; 12.12 là thứ Bảy, peak đầu tiên BiPlus tự chạy toàn bộ.

### 2. Đêm peak và các mốc ngày go-live
Đêm peak ở Hà Nội chạy ~18:00–02:00 giờ VN. Luôn ghi time zone cạnh mỗi giờ; sắp việc theo giờ go-live chứ không theo market; quyết định go/no-go theo từng market; **không có "bật trước, kiểm sau"**.

| Market | Go-live 00:00 địa phương 30/11/2026 | Giờ VN (ICT) | Ai QA again (ca Q4/Q11 tạm, CM-04 §2.1) |
|---|---|---|---|
| NZ (UTC+13, giờ mùa hè) | 30/11 00:00 | 29/11 18:00, Chủ nhật | Người Merch thứ hai kiểm; QA again đầu ca sớm 04:00 |
| AU (UTC+11, giờ mùa hè) | 30/11 00:00 | 29/11 20:00, Chủ nhật | Như trên; ticket High cần QA gate thì gọi QA on-call |
| SG, MY, PH (UTC+8) | 30/11 00:00 | 29/11 23:00 | Như trên |
| VN, TH, ID (UTC+7) | 30/11 00:00 | 30/11 00:00 | Như trên; ca sớm 04:00 kiểm lại R3 đã go-live |

Mốc đếm ngược trong ngày go-live (ngưỡng nội bộ): trước 12:00 mọi setup cho tối đó build xong, chưa live, có internal check; trước 14:00 setup E4 đã tới QA kịp duyệt cấp hai; trước 17:00 mọi setup đã vào QA; go-live − 1h: QA PASS, Shift Leader duyệt, Knox đã gửi. Nếu QA FAIL và giờ go-live đã qua thì setup không go-live; owner báo requester bằng văn bản và đề xuất giờ mới.

### 3. Hai lớp QA, check sau go-live, freeze, war room
- **Hai lớp QA (K3), chỉ cho việc Merch.** Layer 1: QA TM làm đủ checklist, SKU coverage và simulator. Layer 2: QA Lead hoặc Sub-Lead (không phải người layer 1) kiểm lại độc lập các giá trị tiền, sau layer 1 PASS và trước khi duyệt. Lịch mẫu: T-3 QA layer 1; T-1 QA layer 2 + duyệt; ngày D war room; T+1 kiểm end time và trạng thái order.
- **Sau R3 go-live:** người thứ hai (không phải Doer) kiểm storefront trong 30' (E4: 15') trên desktop + mobile, incognito, tới bước checkout; rồi theo dõi order mỗi 15' trong 2 giờ. Dấu hiệu bất thường: order gấp 3 dự kiến; discount lớn hơn internal check; giá dưới sàn; coupon chạm 80% giới hạn trong 2 giờ; không có order nào sau 60' vào ngày peak.
- **Freeze:** 48 giờ trước sự kiện chỉ cho thay đổi được RHQ duyệt; ngoại lệ luôn cần duyệt + evidence trong thân ticket (QCL-00 dòng 0.9). **Cập nhật stock luôn được phép.** Setup phụ thuộc enhancement chưa BVT sign-off thì không go-live.
- **War room** nằm trong khu làm việc secure tại Hà Nội; người on-call được gọi phải có mặt trong 60'. QA là một vai trong war room cùng Peak Lead, Shift Leader, go-live coordinator, order watcher và Tech trực. Jira là nguồn chính thức duy nhất; dùng Mattermost với RHQ, chỉ Jira comment với subsidiary.

### 4. Ranh giới QA, BVT, Tech, Knox
- **QA và BVT** (CM-13 ch.16, CM-12): BVT kiểm enhancement của dev team, PIC là Merch hoặc Tech. **QA Team không làm BVT**; không ai được "mượn QA" cho BVT, Shift Leader không gọi QA on-call cho BVT. QA chỉ cần biết BVT phải pass 100% trước go-live.
- **QA và Tech:** QA REVIEW trong COEC là Tech tự kiểm trên staging; WAITING QA là kiểm bởi người Tech thứ hai. Ticket Merch cần Tech (VD 500,000 coupon code cần ImpEx) thì Merch tạo COEC liên kết và chuyển ticket Merch sang ON HOLD COE. QA chỉ kiểm phần Merch và một mẫu kết quả mà Merch PIC đã kiểm.
- **QA và Knox:** giá và promotion cần Knox approval; Doer gửi sau khi Shift Leader duyệt và trước khi publish. QA không gửi cũng không kiểm Knox; Shift Leader kiểm (tạm thời, chờ CEO).

### 5. Nhắc lại: lỗi khi QA again trên production
Các bước như QA-3.2: báo Shift Leader ngay và ghi giờ; không sửa hay tắt gì; Shift Leader xác nhận impact trong 15' và mở incident theo CM-06 nếu có rủi ro tiền; ghi là escaped defect. Đêm peak khác ở tải: nhiều market go-live trong vài giờ nên war room giữ một danh sách go-live duy nhất và ai kiểm mỗi cái.

## Quiz (đáp án)
1 Go-live 00:00 AU (mùa hè, UTC+11) 27/11/2026 là mấy giờ VN → **C: 26/11 20:00**. 2 PH QA FAIL lúc 22:30 ICT, go-live 23:00, chưa có PASS → **A: không go-live; báo requester, đề xuất giờ mới** (không phải last-minute request). 3 Ai làm layer 2 → **D: QA Lead hoặc Sub-Lead, không phải người layer 1**. 4 RHQ thông báo BVT tuần Black Friday, Tech Lead muốn "mượn" 2 QA → **B: không mượn QA; BVT PIC là Merch hoặc Tech**. 5 Ticket COEC ở QA REVIEW, ai kiểm → **A: Tech tự kiểm trên staging**. 6 Hard freeze flagship, subsidiary xin cập nhật stock 3 SKU khác → **D: xử lý như thường theo risk level** (stock luôn được phép). 7 00:20 ICT, QA again thấy giá PDP thấp hơn internal check → **C: báo Shift Leader ngay, ghi giờ**. 8 QA có kiểm đường Knox trước PASS không → **B: không; Shift Leader kiểm đường duyệt và giờ** (QCL-00 dòng 0.13 là N/A với QA).

## Practice
- **PR-QA3.3-1** (10', giấy): lập bảng go-live 00:00 địa phương 30/11/2026 cho 8 market: giờ VN, thứ, ca QA đang trực (Q4/Q11 tạm), ai QA again (QA TM, QA on-call hay người Merch thứ hai), hạn post-change check (30' hoặc 15' với E4) và cửa sổ theo dõi 2 giờ; giải thích vì sao đêm này là điểm nóng. Pass: giờ VN đúng cả 8 market (NZ 18:00 và AU 20:00 ngày 29/11; SG, MY, PH 23:00 ngày 29/11; VN, TH, ID 00:00 ngày 30/11); nêu 29/11 là Chủ nhật, mỗi ca chỉ có Shift Leader + 1 người, QA chỉ có on-call, 30/11 là ngày tiếp quản; chỉ ra hai cửa sổ theo dõi chạy song song từ 23:00 đến 01:00.
- **PR-QA3.3-2** (10', cặp): tuần Black Friday, ai kiểm/quyết và QA làm gì: (a) RHQ gửi thông báo BVT cho enhancement checkout; (b) ticket Merch cần 500,000 coupon code bằng ImpEx, có COEC liên kết; (c) Shift Leader hỏi đường Knox của một promotion đúng chưa; (d) layer 2 cho price file E4 650 SKU; (e) subsidiary xin cập nhật stock trong freeze 48 giờ. Đáp án: (a) BVT PIC từ Merch hoặc Tech, không bao giờ là QA; (b) Tech tự kiểm ImpEx, có second Tech checker và PC ticket; QA chỉ kiểm phần Merch và mẫu kết quả Merch PIC đã kiểm; (c) Doer gửi Knox theo đường trong brief, Shift Leader kiểm; QA không; (d) QA Lead hoặc Sub-Lead không làm layer 1; (e) được phép, xử lý theo risk level như thường.
