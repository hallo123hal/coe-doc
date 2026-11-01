# GP4.3 When a deadline meets a rule

> Nguồn: page 2484208045 · 45 phút (Study 10' · Demo/thảo luận 5' · Quiz 5' · Practice 25') · Thực hành theo case; facilitator: Shift Leader hoặc Sub-Lead · Capabilities C5, C6 · Cần xong G1.2 (luật RHQ, strike), G1.3 (10 Golden Rules, T1), G2.6 (PC ticket, Knox, quy trình duyệt, strike); nên xong GP4.1 và GP4.2 trước vì bài dùng các approval route và bảng do/refuse/route. Chỉ cần Confluence (đọc CM-13, CM-10, CM-07, MR-06). Không có access: facilitator in CM-13 ch.8, 17, CM-10 §2.2 và mười case ngắn.

## Mục tiêu
Phán đoán một case ngắn là được phép, không được phép hay phải báo và nêu rule; nhận ra ba hành động luôn bị strike và chuyện xảy ra sau strike; áp dụng quy tắc nơi làm việc và AI, gồm ngày Clean Room và giai đoạn chuẩn bị flagship; viết reply giữ rule và đưa đường hợp lệ nhanh nhất bằng văn bản kèm giờ; escalate case áp lực lên đúng người thay vì tự quyết ngoại lệ.

## Thuật ngữ
**Pressure case** (yêu cầu mà deadline hoặc một người ép bạn bỏ kiểm soát, VD "publish ngay, Knox sẽ đến sau"); **Fastest legal path** (phương án nhanh nhất giữ mọi kiểm soát, đưa bằng văn bản kèm giờ, VD "Knox sent at 21:10 ICT; we publish within 15 minutes of approval"); **Secure work area** (khu kiểm soát ra vào ở tầng 6 nơi làm mọi việc CoE trên CoE workstation, không làm từ xa kể cả on-call); **Clean Room** (phòng UAT flagship của RHQ tại văn phòng BiPlus, 40 chỗ; khác secure work area; khách ở đó có người đi kèm); **Embargo** (thông tin chưa công bố như flagship sắp ra; cấm AI kể cả tool được duyệt); **RCA for a strike** (RCA trung thực của Lead gửi RHQ; RHQ quyết strike từ đó, nguyên nhân hệ thống (VD đổi code) thì không strike); **People-risk ladder L1** (tầng hỗ trợ mở trong 1 ngày làm việc sau 2 QA FAIL tính cho Doer trong tháng, hoặc 1 strike: coaching, WIP giảm nửa, peer check mọi ticket, certify lại trong 5 ngày làm việc); **"No approval, no work"** (luật freeze: exception cần evidence duyệt trong thân ticket trước khi bắt đầu).

## Nội dung
### 1. Case áp lực: cái gì không uốn
Ba case quay lại mỗi tuần. Ở mỗi case deadline là thật mà rule vẫn thắng. Việc của bạn: giữ kiểm soát và đi nhanh trong khuôn khổ đó.
| Case | Không uốn | Có thể làm |
|---|---|---|
| Request gấp, không kịp QA | Internal check, price sanity rule, Shift Leader duyệt, second checker trên production lúc go-live; Knox cho giá/promotion | Shift Leader quyết dùng đúng câu RHQ "Last minute request, please QA on your own when it goes live. If any issue, please contact us."; label `LastMinRequest`; trực lúc go-live |
| Subsidiary ép publish không Knox | Giá/promotion không publish live khi chưa có Knox theo đường duyệt trong brief | Gửi Knox ngay và ghi giờ + đường; publish phần đã duyệt; báo Shift Leader trực và Merch Lead |
| Go-live trong freeze | Exception luôn cần duyệt; evidence trong thân ticket trước khi làm; gấp không vượt freeze | Tra exception trên compliance page; không có thì không làm; đề xuất slot đầu tiên sau freeze hoặc đường exception |
| Yêu cầu ngoài scope ("chỉ 5 phút") | CoE chỉ làm service catalogue trong quyền; mọi change production Tech cần PC ticket đã duyệt | Báo Shift Leader hoặc Lead; Template 6 sau khi họ xác nhận; COE Lead đưa RHQ |
| Duyệt "qua điện thoại" | Duyệt phải là evidence viết trên ticket (email duyệt, bản ghi Knox, PC ticket đã duyệt) | Xin đính evidence; giữ ticket ở status chờ đúng |
Template last-minute chỉ gỡ QA gate của CoE. Không bao giờ gỡ Knox, freeze hay PC ticket. Subsidiary tự chịu trách nhiệm QA của họ, nhưng CoE phải giải thích nếu go-live trễ do nút thắt phía CoE.
> Làm gì khi 23:59 tới mà Knox vẫn thiếu là đề xuất BiPlus chờ CEO (MR-03 §2.6): không publish phần thiếu Knox và báo Shift Leader trực + Merch Lead ngay. Kiểm soát tối thiểu cho request R3 gấp cũng là đề xuất của CoE Office chờ CEO (CM-13 §8.1). Áp dụng cả hai tới khi quyết.

### 2. Nơi làm việc và AI
Các rule mà áp lực dễ khiến người ta phá là về nơi, thiết bị và công cụ.
- **Nơi:** mọi việc Samsung chỉ trong khu secure tầng 6, trên CoE workstation. Không làm từ xa, kể cả on-call. (SDSAP từng làm từ xa qua Samsung VPN với duyệt của quản lý lúc peak, theo handover 27/10. Rule BiPlus trong CM-10 giữ nguyên tới khi CEO và RHQ quyết khác.) Nhớ ra ticket chưa trả lời tối Chủ nhật khi ở nhà thì không mở Jira; gọi Shift Leader trực.
- **Thiết bị:** không ảnh điện thoại, ghi âm/ghi hình hay in dữ liệu Samsung. Hiện chưa thu điện thoại cá nhân nhưng cấm chụp/quay; khi chuẩn bị flagship, điện thoại để locker ở sảnh thang máy. Laptop ở lại tầng 6. USB bị chặn.
- **AI:** chỉ tool RHQ duyệt, và không bao giờ với dữ liệu Samsung: không brief, dữ liệu cá nhân, source code, mật khẩu. Không AI với sản phẩm embargo hay khi chuẩn bị flagship, kể cả tool được duyệt. Tới khi DevSecOps Engineer công bố danh sách duyệt, không dùng AI cho việc Samsung. Dán dữ liệu Samsung vào AI là security incident (báo trong 1 giờ).
- **Cửa và bàn:** vào bằng mặt của chính mình; không đi theo sau (tailgating); khách theo danh sách của SDM và có người đi kèm; bàn sạch.
- **Ngày Clean Room:** ngày "VN Clean Room" RHQ, HQ, đội Ấn Độ và subsidiary làm UAT flagship tại văn phòng BiPlus. Khách ở khu dành cho khách (Clean Room, phòng họp, khu core team), không bao giờ dùng CoE workstation hay account, và yêu cầu sửa của họ vẫn vào Jira.
Trước khi gửi, dán hoặc lưu gì, dừng 5 giây: Của Samsung hay của khách? Đích có phải hệ thống Samsung hay kênh được phép? Người nhận có cần không và địa chỉ đúng chưa? Tôi có dùng AI, điện thoại, USB, máy in hay kênh cá nhân không? Evidence đã đính Jira và xóa khỏi máy chưa? Ngày mai tôi giải thích được việc này trước audit của RHQ không?
> Bốn điều kiện laptop cho QA và Tech (chỉ dùng cho Samsung, image chuẩn, mạng có dây, không mang khỏi tầng 6 trừ khi SDM duyệt để duy trì dịch vụ) chờ CEO xác nhận, và danh sách AI được duyệt chưa công bố (CM-10 §1.3, CO-04). Tới đó: không AI, laptop ở lại tầng 6.

### 3. Strike và people-risk ladder
**Strike** là vi phạm RHQ ghi nhận cho một người khi RCA cho thấy người đó không theo process, hoặc không biết mà vẫn làm và gây incident. Lỗi hệ thống (VD đổi code sau deploy) không phải strike. RHQ quyết ai bị strike.
**Ba hành động luôn bị strike:** (1) chạy ImpEx/Groovy trên production không có mandatory line (số PC ticket + số COEC gốc); (2) đổi production không có PC ticket đã duyệt; (3) làm service mình chưa certified rồi gây incident.
Ba strike trong một năm dương lịch = rời team vĩnh viễn; đếm lại mỗi năm dương lịch. BiPlus chủ động thay người trước strike thứ ba. Vi phạm an ninh thông tin chưa tính strike nhưng xử lý theo CM-10, và event ladder CM-08 nói vi phạm process, an ninh hay AI lần hai thì BiPlus thay người.
**Sau đó:** RHQ báo Lead; Lead viết RCA trung thực (sự kiện, nguyên nhân hệ thống nếu có, không đổ lỗi, không giấu). Người đó vào **L1 của people-risk ladder** — cũng mở sau 2 QA FAIL tính cho Doer trong cùng tháng:
| Biện pháp L1 | Cách |
|---|---|
| Coaching | Ghép với senior hoặc L3 Coach cho service |
| Giảm nửa WIP | Số ticket đồng thời giảm một nửa |
| Peer check | Không ticket nào sang QA trước khi peer kiểm |
| Certify lại | Trong 5 ngày làm việc; đạt thì ra khỏi L1 |
Shift Leader mở L1 trong 1 ngày làm việc bằng trao đổi riêng và kế hoạch certify lại. L1 là hỗ trợ, không phải kỷ luật. Golden Rule 8 áp dụng suốt: báo sớm; giấu lỗi nghiêm trọng hơn chính lỗi.
> Các tầng cao hơn của ladder (CO-05) chưa có trên Confluence; bài chỉ dạy L1 (MR-06 §6.7). Cách đếm QA FAIL tính vào L1 (hai FAIL trên một ticket, kết quả QUESTION, QA Team Member) còn chờ Merch Lead và QA Lead quyết.

### 4. Đường hợp lệ nhanh nhất, bằng văn bản
Khi giữ một rule, đừng dừng ở "không". Viết một comment trên ticket làm bốn việc: nêu rule trong một câu; nói đã xong gì; đưa phương án tuân thủ nhanh nhất **kèm giờ** (ICT và địa phương); nói đã báo ai và update kế lúc nào. Từ ngữ đơn giản, không đổ lỗi, không hứa ngoài process.
**Ví dụ (mô phỏng, từ CM-13 ch.8, 10):** DEMO-7120 tạo 18:05 ICT, phải go-live 00:00 cùng ngày: giảm giá 2 SKU. 22:40 subsidiary viết "Go-live is at midnight. Knox will be approved tomorrow morning, please publish now." Shift Leader giữ rule và viết:
```
Hi [Name], thank you. Prices and promotions can only go live after Knox approval,
including urgent requests (RHQ rule).
Done: setup and internal check complete; Knox sent at 21:10 ICT along the approval path in the brief.
Fastest option: as soon as Knox is approved, we publish within 15 minutes and check the storefront.
If your approver can approve tonight, the promotion can still go live close to 00:00 local time.
Last minute request, please QA on your own when it goes live. If any issue, please contact us.
Our Merchandising Lead is informed. Next update by 23:30 ICT.
```
Hợp lệ vì: không có gì chưa duyệt được publish; câu RHQ dùng nguyên văn; giờ và đường gửi Knox có trên ticket; Lead đã biết; requester biết cái gì gỡ vướng. "15 phút" là cam kết Shift Leader đặt cho ca này, không phải SLA từ nguồn.
Rồi escalate quyết định, không phải công việc: Shift Leader trực và Merch Lead ngay; với freeze hay exception ngoài scope thì COE Lead đưa RHQ.
> Reply trên do tác giả khoá học viết từ CM-13 ch.8, 10 và CM-08 Template 16; giờ là mô phỏng.

## Quiz (đáp án)
1 21:30 ICT, subsidiary khăng khăng: "VP của chúng tôi duyệt qua điện thoại, publish giá ngay, Knox ngày mai" → **C: không publish giá chưa duyệt; gửi hoặc xác nhận Knox, ghi giờ + đường, reply đường hợp lệ nhanh nhất, báo Shift Leader và Merch Lead** (template last-minute chỉ gỡ QA gate). 2 (không chấm tới khi D14 chốt: trong mô hình freeze của RHQ không được đổi giá trong hot freeze) Hybris hard freeze, subsidiary xin đổi giá last-minute SKU flagship, compliance page có exception approval → **B: ghi evidence duyệt (vai trò approver, ngày, link) vào thân ticket, rồi làm qua mọi cổng R3**. 3 On-call Chủ nhật ở nhà, nhớ ra ticket cần một comment → **B: gọi Shift Leader trực; không mở Jira ở nhà**. 4 Brief tiếng Thái khó đọc, đồng nghiệp gợi ý AI tool "đã duyệt", brief là cho flagship sắp ra → **C: không được: không dữ liệu Samsung vào AI, không AI với sản phẩm embargo/flagship; nhờ Team Member nói tiếng Thái**. 5 Tech Team Member chạy ImpEx đã duyệt trên production nhưng dòng đầu mang số PC tuần trước, RHQ email 3 ngày sau → **B: Lead viết RCA trung thực; RHQ quyết strike; nếu tính thì người đó vào L1 (coaching, WIP giảm nửa, peer check, certify lại 5 ngày làm việc)**. 6 KHÔNG thuộc ba hành động luôn bị strike → **D: QA FAIL vì brief sai time zone** (QA FAIL chỉ tính vào L1 sau 2 lần/tháng, không phải hành động strike). 7 Ngày Clean Room, khách subsidiary xin dùng login Hybris của bạn → **B: từ chối lịch sự; ghi yêu cầu vào Jira; CoE sửa bằng account của mình theo runbook; báo Shift Leader**.

## Practice
**PR-GP4.3-1. Mười case và một reply** (20', giấy, làm một mình rồi so theo cặp; mọi case là mô phỏng). Phán đoán từng case: **allowed**, **not allowed** hay **report** (report = security incident/vi phạm báo trong 1 giờ) và nêu rule; rồi viết reply cho case 10. (1) Subsidiary xin publish promotion không Knox "vì approver đang nghỉ phép"; (2) request đến 18:05 ICT cho go-live cùng đêm; Shift Leader quyết dùng template last-minute và Knox đã gửi; (3) đồng nghiệp dán brief promotion vào AI translator miễn phí; (4) trong hard freeze, subsidiary cập nhật stock SKU flagship; (5) Tech Team Member định chạy fix Groovy "5 giây" trên production trước khi PC ticket được duyệt vì incident là P1; (6) bạn mang laptop CoE về nhà để on-call nhanh hơn; (7) nhân viên giao hàng đi theo sau bạn qua cửa tầng 6; (8) bạn làm QA evidence trên CoE workstation, đính Jira rồi xóa bản local; (9) Team Member chưa certified một service nhận ticket service đó "giúp queue"; (10) subsidiary khăng khăng go-live 00:00 không có Knox. **Pass:** các case trọng yếu đúng: (1) not allowed; (2) allowed (chỉ ngoại lệ QA gate, Knox vẫn gửi, giữ kiểm soát R3 tối thiểu); (3) report (dữ liệu Samsung vào AI); (4) allowed (stock luôn cập nhật được); (5) not allowed (PC ticket trước, nhắn PC approver cho P1, không chạy trước duyệt; chạy là bị strike); (6) not allowed; (7) report (tailgating, người lạ trong khu); (8) allowed; (9) not allowed (không certification, không làm production; gây incident là strike); (10) not allowed. Reply cho case 10 nêu rule Knox trong một câu, nói đã xong gì (setup, internal check, giờ + đường gửi Knox), đưa đường hợp lệ nhanh nhất kèm giờ, báo Shift Leader và Merch Lead, và cho giờ update kế. Không cần truy cập hệ thống.
> Khoảng trống tài liệu: BiPlus Security Framework v3 và các tầng cao của people-risk ladder (CO-05) chưa có trên Confluence; bài dùng CM-10, CM-13 và tầng L1 cho tới khi công bố.
