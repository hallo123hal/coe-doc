# Tổng hợp câu hỏi, đáp án và giải thích theo từng bài – Ops CoE Samsung SEAO

Tổng hợp từ phần **câu hỏi kiểm tra, bài tập và tình huống** của 3 nhóm tài liệu Confluence (space SamsungCoETech), quét lại ngày 25/10/2026 (v0.3):

- [Tài liệu chung (CM)](https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2478375074) – 13 trang con (CM-01…CM-13; CM-13 là trang mới)
- [Tech Team (TC)](https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2478081979) – 5 trang con (TC-01…TC-05)
- [Merchandising Team (MR)](https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2477263980) – 7 trang con (MR-01…MR-07)
- [SAP và nghiệp vụ Samsung SEAO](https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2480047339) – 1 trang (song ngữ, sửa 23/10/2026)

**Về nguồn:** cả 24 trang con cũ đã đổi ngày 22/10/2026 (v0.3; TC-01…05 và CM-12 v0.2), nay **song ngữ** (Anh trước, Việt sau); CM-13 là trang mới. Đáp án trong file này đã đồng bộ theo bản đó dựa trên so sánh theo câu, nên vẫn nên đối chiếu trang gốc khi cần chắc. Tài liệu gốc là **bản nháp**; mọi mã ticket (`DEMO-…`), số liệu, thị trường trong câu hỏi là **giả lập**. Một số đáp án còn ghi "chờ RHQ/CEO/anh David chốt" – giữ nguyên như trong nguồn.

**Cách đọc:**
- Mỗi bài có bảng *Câu hỏi – Đáp án – Giải thích ngắn*. Với trắc nghiệm, đáp án in đậm là lựa chọn đúng; chữ trong ngoặc là nội dung lựa chọn khi cần để hiểu câu hỏi.
- "(mẫu)" = câu tự luận/tình huống, cột giải thích là **đáp án mẫu** (diễn đạt khác vẫn đạt nếu đủ ý). Dấu ★ = câu/ý trọng yếu (sai là trượt).
- Số trong ngoặc ở cuối giải thích (vd "mục 6.3") là mục tương ứng trong trang gốc.
- Phần checklist theo vai trò, glossary, mẫu comment… không phải câu hỏi nên không đưa vào đây; xem file tóm tắt `CM-xx`, `TC-xx`, `MR-xx` cùng thư mục.

## Mục lục

| Nhóm | Bài | Nội dung câu hỏi | Quy mô |
|---|---|---|---|
| CM | CM-01 Welcome pack | Trắc nghiệm nền tảng + tình huống ngày đầu | 13 + 6 |
| CM | CM-02 Service Management | Phân loại 20 tình huống + câu hỏi kiểm tra | 20 + 20 |
| CM | CM-03 SLA handbook | Tính hạn chót, cảnh báo, Composite, tình huống + kiểm tra | 8 + 4 + 6 + 5 + 20 |
| CM | CM-04 Shift handbook | Trực ca, bàn giao, vắng mặt | 20 |
| CM | CM-05 Service Request | Trắc nghiệm + tình huống | 13 + 7 |
| CM | CM-06 Incident & on-call | Trắc nghiệm + tình huống | 14 + 6 |
| CM | CM-07 Change, Problem | Phân cấp 18 tình huống + kiểm tra | 18 + 20 |
| CM | CM-08 Leo thang & giao tiếp | 12 bài viết tiếng Anh + kiểm tra | 12 + 19 |
| CM | CM-09 Công cụ Samsung | Thực hành filter/comment + kiểm tra | 3 + 20 |
| CM | CM-10 An toàn thông tin (T1) | Đề T1 20 câu + 23 tình huống đúng/sai | 20 + 23 |
| CM | CM-11 Academy | Ngân hàng T3 53 câu + kiểm tra + 3 đề replay T4 | 53 + 16 + 3 |
| CM | CM-12 BVT handbook | Kiểm tra BVT | 15 |
| CM | CM-13 Quy tắc RHQ | Trắc nghiệm + tình huống + 10 quy tắc | 12 + 8 + 10 |
| TC | TC-01 Tech Operating Manual | Case book 10 case + kiểm tra | 10 + 16 |
| TC | TC-02 Level 1 Shift Playbook | Kiểm tra L1 | 20 |
| TC | TC-03 Quy trình COEC & Samsung L2/L3 | Trắc nghiệm + tình huống | 12 + 6 |
| TC | TC-04 On-call handbook | Trắc nghiệm + tình huống | 10 + 5 |
| TC | TC-05 Runbook, PC ticket, change rules | Trắc nghiệm + tình huống | 10 + 8 |
| MR | MR-01 Merchandising Operating Manual | Kiểm tra + 2 bài tập nhóm Shift Leader | 20 + 2 |
| MR | MR-02 Shift Leader Playbook | Kiểm tra chứng nhận Shift Leader | 20 |
| MR | MR-03 Market Owner Playbook | Kiểm tra Market Owner | 8 + 12 |
| MR | MR-04 Quy trình Merchandising chi tiết | Trắc nghiệm + tình huống | 14 + 6 |
| MR | MR-05 Danh mục service & runbook | Kiểm tra | 18 |
| MR | MR-06 Kiểm soát chất lượng & rủi ro | Trắc nghiệm + tình huống | 13 + 9 |
| MR | MR-07 Peak, launch, campaign | Trắc nghiệm + tình huống | 13 + 7 |
| SAP | SAP và nghiệp vụ Samsung SEAO | 15 câu tự kiểm tra + RDD + BN1–BN6 | 15 + 3 + 6 |

## Các quy tắc hay gặp nhất (đối chiếu nhanh)
- **Đồng hồ SLA:** dừng ở ON HOLD SUBS (đã giao Assignee cho subsidiary), ON HOLD RHQ/HQ, REVIEW SETUP, SYSTEM SUPPORT; **vẫn chạy** ở ON HOLD COE, QA REVIEW, STG SETUP. Subsidiary đã trả lời mà ticket còn ON HOLD SUBS → chuyển ngay về STG SETUP.
- **Initial response** = chuyển trạng thái (APPROVED-ES → STG SETUP; NEW → ASSIGNED), không phải comment. Nội bộ 78' (P0/High 15', P1 30'); RFP 2h.
- **STG SETUP không phải staging**: Merch thiết lập trên production chưa live, test bằng promotion simulator rồi publish đúng giờ.
- **Mọi thay đổi Tech trên production cần PC do Oliver Leung duyệt** (kể cả việc 5 giây); ImpEx/Groovy phải có dòng số PC + COEC gốc; chờ duyệt → ON HOLD HQ "PC ticket pending"; chỉ P0/P1 cần sửa ngay mới nhắn Oliver.
- **Cần Tech cho ticket Merch** (vd 500.000 mã coupon): không move; tạo COEC mới + issue link; Merch ON HOLD COE (SLA Merch vẫn chạy).
- **R1/R2/R3 + E4** (≥10.000 USD, >5 thị trường, file giá ≥500 SKU → Merch Lead/Deputy duyệt thêm); kiểm sau thay đổi 30' (E4 15'), monitor 15' trong 2h.
- **Yêu cầu gấp:** comment đúng câu "Last minute request, please QA on your own when it goes live. If any issue, please contact us.", gắn label, kiểm soát tối thiểu, đứng chờ hỗ trợ.
- **QA chỉ QA việc Merch** – không QA Tech, không BVT; chỉ COE Lead override QA FAIL (báo RHQ).
- **BVT:** PIC Merch hoặc Tech; 100% pass mới go-live; ngày không thương lượng.
- **An toàn thông tin:** dữ liệu Samsung chỉ trên hệ thống Samsung; không AI, không điện thoại chụp; bằng chứng QA tạo trên máy trạm CoE, đính thẳng Jira, xóa bản trên máy; sự cố báo văn bản trong 1 giờ.

---

# PHẦN I. TÀI LIỆU CHUNG (CM)

## CM-01 Welcome pack – Samsung SEAO và Ops CoE

**Trắc nghiệm** (đáp án đúng in đậm)

| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | RHQ của Samsung SEAO đặt ở đâu và có vai trò gì với CoE? (A Hà Nội – đơn vị vận hành; B Singapore – product owner; C Kuala Lumpur – đối tác 3PD; D Seoul – Samsung L2/L3) | **B** | RHQ ở Singapore là product owner. |
| 2 | Tám subsidiary của SEAO là: (A VN, TH, ID, MY, SG, PH, AU, NZ; B …KR; C …IN; D …LA) | **A** | VN, TH, ID, MY, SG, PH, AU, NZ. |
| 3 | 03:00 sáng tháng 11 ở Hà Nội thì ở Auckland là mấy giờ? (A 03:00; B 04:00; C 07:00; D 09:00) | **D** | Tháng 11 NZ dùng giờ mùa hè, sớm hơn Hà Nội 6 giờ. |
| 4 | STG SETUP của ticket Shop Merchandising nghĩa là gì? | **B** – CoE đã nhận ticket và đang thiết lập; việc thiết lập làm trên production | STG SETUP không phải môi trường staging. |
| 5 | Merchandising, QA priority High có resolution time? (A 2h; B 4h; C 16h; D 24h) | **B (4 giờ)** | SLA ticket Merchandising gồm cả bước QA. |
| 6 | Mục tiêu nội bộ BiPlus cho phản hồi đầu tiên (RFP 2 giờ)? (A 15'; B 30'; C 78'; D 120') | **C (78 phút)** | P0 và High 15 phút, P1 30 phút. |
| 7 | Ngày takeover (BiPlus sở hữu 100%, SDSAP kết thúc dịch vụ)? | **C – 30/11/2026** | Lộ trình chuyển đổi (chương 5). |
| 8 | Ai duyệt mọi thay đổi Merchandising trước production? | **C – Shift Leader trực (thêm Merch Lead với E4)** | Quy tắc vàng 6. |
| 9 | Ticket không owner được lọc bao lâu một lần? | **C – 30 phút** | Quy tắc vàng 5. |
| 10 | On-call phải xử lý một ticket thì làm gì? | **B** – trả lời trong 15 phút, có mặt tại trung tâm trong 60 phút | Quy tắc vàng 1; không làm remote. |
| 11 | Ở trạng thái nào đồng hồ SLA dừng? (A ON HOLD COE; B ON HOLD SUBS; C STG SETUP; D QA REVIEW) | **B – ON HOLD SUBS** | ON HOLD COE, STG SETUP, QA REVIEW đều tính SLA. |
| 12 | Ai duyệt PC ticket cho thay đổi Tech trên production (vd xóa user group qua Back Office)? | **C – Oliver Leung (RHQ, HOD cụm SEAO)** | Không PC được duyệt thì không thay đổi gì trên production, kể cả việc 5 giây. |
| 13 | Phát biểu nào đúng về QA Team? | **B** – chỉ QA công việc Merchandising; không BVT, không QA cho Tech | Thời gian QA nằm trong SLA ticket Merchandising. |

**Tình huống** (đáp án mẫu)

| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 14 | Người của subsidiary MY nhắn qua chat cá nhân nhờ đổi một dòng text "ngay, chỉ 1 phút". | Không trao đổi qua kênh cá nhân (quy tắc vàng 2); mọi trao đổi qua comment Jira. Đề nghị subsidiary tạo ticket Shop Merchandising; khi APPROVED-ES thì chuyển STG SETUP, làm theo runbook (R1, Shift Leader kiểm và duyệt). Không làm ngoài ticket (quy tắc vàng 4). |
| 15 | Ca tối quên ghi vào handoff note một go-live 02:00; ca đêm đã bắt đầu. | Báo ngay Shift Leader ca đêm, bổ sung handoff note bằng văn bản, xác nhận đã ghi nhận và giao người kiểm go-live (quy tắc vàng 8, 9). |
| 16 | Bạn đạt L2 price upload, chưa chứng nhận coupon; Shift Leader bận, ticket coupon sắp chạm cảnh báo 70%. | Không nhận ticket. Báo Shift Leader/Sub-Lead khác giao người đã chứng nhận; leo thang theo cảnh báo 70% nếu cần (quy tắc vàng 7). |
| 17 | Dùng công cụ AI dịch brief Thái sang Anh? | Không – brief là dữ liệu Samsung (quy tắc vàng 3). Nhờ Market Owner TH hoặc Team Member tiếng Thái dịch. |
| 18 | 06:00 biết không thể làm ca 08:00. | Báo Shift Leader/Sub-Lead ca ngày trước 08:00 theo kênh quy định để gọi backup; làm thủ tục nghỉ sau (quy tắc vàng 10). |
| 19 | Ticket `DEMO-2110` (TH) thiếu ngày kết thúc, cần hỏi subsidiary. | Ghi MỘT câu hỏi gộp, rõ, đầy đủ trong comment; chuyển ON HOLD SUBS và giao Assignee cho subsidiary (đồng hồ dừng). Không dùng ON HOLD SUBS chỉ để dừng đồng hồ. Subsidiary trả lời (thường chỉ bằng comment) → chuyển ngay về STG SETUP làm tiếp. |

**Quy tắc RHQ (CM-13)** – thêm ở v0.3

| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 20 | Việc nào **không** cần PC ticket? (A Tech chạy ImpEx gỡ user group; B Tech đổi cấu hình Back Office; C Market Owner setup giá theo workflow Shop Merchandising; D Tech tạo cronjob báo cáo trên production) | **C** | Setup Merchandising đi theo workflow Shop Merchandising và Knox approval; PC ticket chỉ cho thay đổi do **Tech** làm trên production (mục 3.2). |
| 21 | Promotion đã publish, thay đổi nào buộc lần publish tiếp theo phải duyệt Knox lại? (A đổi tên; B đổi ngày kết thúc; C đổi ghi chú nội bộ; D không thay đổi nào) | **B** | Đổi action, condition, website hoặc ngày thì phải duyệt lại; đổi tên thì không (mục 3.2). |
| 22 | Ba strike trong một năm dương lịch dẫn tới điều gì, ai quyết định ai bị strike? (A nhắc nhở – BiPlus; B bị loại khỏi đội vĩnh viễn – RHQ; C thi lại T3 – Lead; D chuyển bench – SDM) | **B** | Đủ ba strike trong năm dương lịch là bị loại vĩnh viễn; RHQ là bên quyết định, dựa trên RCA của Lead (mục 6.3). |
| 23 | Về 3PD, phát biểu nào đúng? (A Merch vận hành 3PD trên marketplace; B PIC 3PD chuyên trách ở Tech Team, có backup, CoE chỉ quản middleware; C QA phụ trách 3PD; D CoE thao tác trực tiếp trên marketplace) | **B** | PIC 3PD và backup nằm trong Tech Team; CoE không thao tác trên marketplace, chỉ quản middleware giữa Hybris và marketplace (mục 4.2). |


---

## CM-02 Service Management cho người mới

### A. Bài tập phân loại 20 tình huống (giả lập)
Với mỗi tình huống: loại việc – priority – lý do (dùng cho bài T3 Foundation quiz).

| # | Tình huống | Loại việc | Priority | Lý do ngắn |
|---|---|---|---|---|
| 1 | SG duyệt `DEMO-7001`: 1 promotion giảm 10% cho 30 SKU, go-live thứ Hai tuần sau | Service Request (Shop Merch), change R3 | Medium (16h) | 1 promotion = Medium; R3 phải qua QA REVIEW; initial response = chuyển APPROVED-ES → STG SETUP; Doer ghi **internal check** trên ticket trước khi build; **Knox approval** theo approval path trong brief |
| 2 | 20:40 T7, TH báo không checkout được toàn site từ 20 phút trước | Incident (major) trên COEC | Tech P0 (4h) | 20:40 T7 là ngoài khung Tech: Tech on-call lớp 1 nhận và chuyển ASSIGNED; Shift Leader có mặt tại trung tâm và gọi Tech on-call khi thấy P0 (CM-06); thay đổi khẩn vẫn cần PC, nhắn Oliver qua Mattermost; rollback một thay đổi vừa làm cũng cần PC |
| 3 | MY gửi `DEMO-7003` 5 promotion, ngày bắt đầu khác nhau | SR, change R3 | Low (24h) | >2 promotion = Low; QA lại production mỗi đợt, giữa các đợt ở PENDING LAUNCH |
| 4 | VN cập nhật text và flag 15 SKU | SR, change R1 | Low (24h) | Text/flag thuộc Low; R1 không qua QA, Shift Leader kiểm và duyệt |
| 5 | ID tạo COEC hỏi cách đọc trạng thái đơn trong Backoffice | SR (câu hỏi) trên COEC | Tech P4 (120h) | Câu hỏi/nghiên cứu = P4; không đổi production nên không cần PC |
| 6 | Coupon PH giới hạn 100 lượt, 2 giờ qua 400 đơn, thiệt hại >10.000 USD | Incident (major) | High (4h) | Mất doanh thu >10.000 USD; chặn coupon trong 30', báo RHQ và subsidiary trong 30' |
| 7 | AU yêu cầu tạo EPP site mới (multistore) cho kênh EPP, ticket chưa nói đã có phê duyệt hay chưa | SR, change R2 | Medium (16h) | Multistore EPP thuộc Medium; multistore là R2. **EPP site mới/kích hoạt lại**: hỏi ngay subsidiary đã có phê duyệt chưa; có email phê duyệt đính ticket → chuyển ON HOLD RHQ cho Oliver duyệt; chưa có → trả subsidiary theo template RHQ với comment "New EPP site creation requires RHQ approval. Please seek approval first using the approval template [link] and attach the approval email to this ticket." (tạm ON HOLD SUBS, giao subsidiary) |
| 8 | NZ upload special price 120 SKU | SR, change R3 | Low (24h) | Special price = Low; giá là R3 và phải qua Knox approval; file >100 dòng kèm file diff; xét E4 nếu exposure ≥10.000 USD |
| 9 | Lần thứ ba trong tháng, nhóm đơn MY không sang NERP sau đồng bộ đêm | Incident cho lần này, mở Problem | Tech P2 (16h) | Lỗi đơn do cấu hình, không toàn cục; stuck order lặp ở một thị trường = trigger mở problem |
| 10 | MY ticket Shop Merch `DEMO-7010` cần 500.000 mã coupon, Back Office không tạo được, cần ImpEx | SR Merch (coupon là promotion), R3, kèm COEC liên kết | Merch Low (24h; nhóm "voucher creation" trong bảng RFP, nay gọi là coupon); COEC thường P3 (40h) | Không chuyển ticket sang COEC: tạo COEC mới + issue link, ticket Merch sang ON HOLD COE (vẫn tính SLA); người tạo đôn đốc Tech; ImpEx cần PC |
| 11 | QA thấy promotion `DEMO-7011` (đã publish simulator, chưa live) sai store scope | Không phải incident; QA FAIL | Giữ priority ticket | Chưa live; QA REVIEW trả về STG SETUP, gặp trực tiếp người làm, ghi root cause code; cổng QA hoạt động đúng |
| 12 | SG banner trang offer AEM (không T&C) sai ảnh từ sáng, không ảnh hưởng giá | Incident nhỏ (ghi incident log), sửa bằng R1 | Low (24h) | Campaign page/banner/CMS = Low; không T&C nên R1 |
| 13 | VN ticket Shop Merch `DEMO-7013` xin cấp EPP access code cho domain email mới; toàn việc Tech | SR; move chính ticket sang COEC | Tech P3 (40h) | Toàn việc Tech nên move, không tạo mới; cấp access code và thêm domain email vào EPP access list là việc hoàn toàn của Tech, đổi dữ liệu production → cần PC; RHQ đã xác nhận CoE tự move được, không cần quyền admin; comment "Moved to COEC as this request is fully handled by the Tech team." |
| 14 | 17:50 T5, TH duyệt `DEMO-7014` promotion giảm 8%, live 00:00 cùng đêm | SR, R3; last-minute request | Medium (16h); due date 00:00 | Sau mốc nội bộ 17:00, QA có thể không kịp: comment mẫu "Last minute request, please QA on your own…", đứng chờ hỗ trợ (CoE không hỗ trợ 24/7/365 cho yêu cầu sát giờ); vẫn giữ kiểm soát tối thiểu R3 (internal check, price sanity, Shift Leader duyệt, người thứ hai kiểm production lúc go-live); promotion vẫn gửi **Knox approval**; gắn nhãn LastMinRequest để đếm |
| 15 | Ticket coupon ID reopen vì không áp dụng trên mobile; lần reopen thứ hai cùng loại trong tháng | SR (reopen), mở Problem | Low (24h), giữ nguyên | Xử lý tiếp trên chính ticket, đồng hồ cộng tiếp; 2 lần reopen cùng loại = trigger problem |
| 16 | Cổng thanh toán PH lỗi 40', ~6 đơn, ~300 USD | Incident | Tech P1 (8h) | Ảnh hưởng doanh thu 100–500 USD; cần điều tra nguyên nhân |
| 17 | RHQ tạo COEC đổi cấu hình base store kênh SMB ở MY | SR trên COEC, thay đổi Tech cần PC | Tech P3 (40h) | Làm trên staging, tự QA, người thứ hai kiểm (another set of eyes, giữ chứng nhận **L2 hoặc L3** của đúng service) vì chạm cấu hình cả kênh SMB; PC kèm kết quả staging và rollback; chờ duyệt ở ON HOLD HQ (đồng hồ dừng); Oliver duyệt rồi mới làm production |
| 18 | ID ticket "URGENT" đổi banner trang chủ, campaign bắt đầu sau 3 giờ | SR, R1 | Low (24h) | "URGENT" không đổi priority; urgency chỉ làm due date sớm hơn; Shift Leader kiểm và duyệt, làm ngay. CM-13 mới nói last-minute cho giá/promotion; banner R1 thì hỏi Lead trước khi gắn label LastMinRequest để đếm |
| 19 | 20:15 T6, RHQ nhắn Mattermost: cửa sổ BVT là T3–T6 tuần sau | BVT, theo dõi trên ticket enhancement | Không theo bảng; đo bằng 3 KPI BVT | Ngày BVT cố định, không thương lượng; Shift Leader ghi handoff, nhắn Merch Lead + Tech Lead chỉ định PIC; QA không tham gia; 100% test case pass mới go-live |
| 20 | Promotion VN cấu hình đúng brief đã duyệt và bản internal check trên ticket khớp brief, nhưng brief ghi sai mức giảm; đơn đang đặt, >10.000 USD | Incident (major) | High (4h) | Rollback ngay, báo RHQ trong 30'; nguồn sai ghi trong RCA, kết luận trách nhiệm theo điều tra chung với RHQ (RFP 3.10); CoE vẫn xử lý như incident bất kể ai sai |

### B. Câu hỏi kiểm tra (22 câu)

| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Điều nào là **outcome**, không phải output? | **b** – Người mua thấy đúng giá giảm từ giờ go-live và đơn chạy bình thường | Outcome là điều khách hàng đạt được; a, c, d là output/hoạt động |
| 2 | Theo ITIL, RHQ Singapore đóng vai trò gì với CoE? | **b** – Customer và sponsor | RHQ là product owner, đặt yêu cầu, đo SLA |
| 3 | Team Member chỉ comment "Noted", ticket vẫn ở APPROVED-ES. Vi phạm nguyên tắc nào? | **c** – Focus on value | Phản hồi phải có owner, bước tiếp theo, thời điểm; comment không thay cho chuyển STG SETUP |
| 4 | Ticket Merch có đúng 1 promotion: priority và resolution time? | **b** – Medium, 16h | Một promotion = Medium |
| 5 | Tech P1 là gì? | **b** – Ảnh hưởng doanh thu 100–500 USD, 8h | |
| 6 | Phản hồi đầu ticket High: cam kết RFP và mục tiêu nội bộ? | **a** – 2 giờ và 15 phút | RFP 2h cho mọi priority; nội bộ 15' với P0 và High |
| 7 | OLA là gì? | **b** – Thỏa thuận nội bộ giữa các team trong CoE để giữ SLA | RHQ không đo SLA riêng cho QA; BiPlus tự đặt OLA |
| 8 | Ai được vượt quyết định reject của QA? | **c** – COE Lead, kèm báo RHQ | Merch Lead không được vượt |
| 9 | Ticket bị mở lại (reopen) thì? | **b** – Giữ priority, đồng hồ cộng tiếp thời gian đã dùng | Không bao giờ đặt lại đồng hồ; không tạo lại ticket |
| 10 | Bộ lọc ticket không owner chạy bao lâu một lần? | **c** – 30 phút | Mọi ca; mục tiêu không ticket nào không owner quá 1 giờ |
| 11 | Trạng thái nào vẫn tính SLA? | **c** – ON HOLD COE | Chờ trong nội bộ CoE nên vẫn tính; chờ bên ngoài CoE thì dừng |
| 12 | Initial response ticket Merch đạt khi nào? | **b** – Khi CoE chuyển APPROVED-ES → STG SETUP | Comment thôi không đủ |
| 13 | QA Team QA cho việc nào? | **b** – Chỉ công việc hằng ngày của Merch | Không QA cho Tech, không BVT |
| 14 | Tech xóa user group (5 giây) – điều kiện bắt buộc? | **c** – PC ticket được Oliver Leung duyệt | Kể cả việc 5 giây; Oliver là người duyệt duy nhất |
| 15 | COEC P2 Tech không tự sửa được, phải chuyển Samsung L2/L3: làm gì, theo dõi thế nào, ai giữ ownership? | (mẫu) | Tạo Maintenance Request cho SDS India kèm evidence pack, chuyển COEC sang SYSTEM SUPPORT (đồng hồ dừng). CoE giữ ownership; theo dõi 2 ngày làm việc/lần (P2 thuộc nhóm High), mỗi lần một comment Jira + cập nhật requester; chờ >10 ngày làm việc thì mở problem record |
| 16 | Ca đêm có Shift Leader và bạn; bạn vừa đổi text banner (R1). Ai kiểm và duyệt? Nếu chính Shift Leader làm thì sao? | (mẫu) | R1: Shift Leader kiểm và duyệt trong một bước, bạn là doer. Nếu Shift Leader tự làm thì người duyệt là người khác có quyền (deputy SL đã chứng nhận hoặc Lead); chưa có thì chưa lên production |
| 17 | Ticket product setup có QA gate (Low, 24h) go-live sau 3 giờ: due date và làm gì? | (mẫu) | Due date = go-live trừ thời gian kiểm và duyệt, không phải hạn 24h. Báo Shift Leader, gắn nhãn last-minute, làm ngay, gửi QA sớm. QA không kịp thì comment last-minute theo mẫu, subsidiary tự QA khi go-live, CoE đứng chờ hỗ trợ (không hỗ trợ 24/7/365) và giữ kiểm soát tối thiểu: Shift Leader duyệt, người thứ hai kiểm production lúc go-live, với R3 thêm internal check + price sanity; giá/promotion vẫn gửi Knox approval |
| 18 | Cùng lỗi đồng bộ đơn hàng xảy ra lần thứ ba trong tháng ở một thị trường: ngoài xử lý lần này? | (mẫu) | Ghi nguyên nhân trên ticket, báo Lead; mở problem record; đưa vào weekly problem review |
| 19 | Composite SLA tháng là 96,8%: ai làm gì, trong bao lâu? | (mẫu) | Dưới 97% (RFP) và dưới 98,5% (nội bộ): COE Lead + CEO gửi RHQ kế hoạch khắc phục trong 5 ngày làm việc (nguyên nhân, hành động, owner, ngày); khấu trừ tính theo Composite quý |
| 20 | Dashboard hiện `DEMO-7120` ở ON HOLD SUBS, Assignee là bạn. Làm gì, vì sao? | (mẫu) | Đọc comment mới nhất. Subsidiary đã trả lời → chuyển ngay về STG SETUP (đồng hồ đang dừng sai thực tế). Chưa trả lời → giao Assignee cho subsidiary (lỗi quên giao), giữ câu hỏi trong comment, ghi thời điểm nhắc tiếp |
| 21 | Brief giảm giá R3 đã được subsidiary duyệt. Trước khi build, Doer làm gì và ghi gì lên ticket? Khi nào được hỏi subsidiary? | (mẫu) | Đối chiếu cấu hình với brief đã duyệt và ghi **internal check** lên ticket: SKU, giá hoặc mức giảm, thời gian kèm múi giờ, site hoặc store, quy tắc stack, giới hạn dùng; chạy price sanity rules; Checker theo cấp rủi ro (R3: QA, Shift Leader duyệt, thêm Lead khi E4). Chỉ hỏi subsidiary khi brief thiếu hoặc mâu thuẫn, hoặc price sanity cảnh báo: một câu hỏi gộp, ON HOLD SUBS, giao Assignee cho subsidiary |
| 22 | Promotion đã publish, subsidiary muốn đổi tên và đổi ngày kết thúc. Việc nào phải duyệt Knox lại, CoE lấy approval path ở đâu? | (mẫu) | Đổi ngày kết thúc (đổi NGÀY) thì lần publish tiếp theo phải duyệt Knox lại; đổi tên thì không. Approval path do subsidiary ghi ở cột approval path trong campaign brief, CoE làm đúng cột đó, không tự chọn; cách gửi Knox học từ đội CoE hiện tại và Market Owner ghi vào runbook |

---

## CM-03 SLA handbook – hiểu và giữ SLA

### A. Bài tập A – tính hạn chót có thời gian chờ
Lịch tham chiếu T2 07/12/2026 – CN 13/12/2026; giờ lịch trong trạng thái tính SLA; "bắt đầu" = giờ vào APPROVED-ES (Merch) hoặc NEW (COEC).

| # | Đề | Hạn ban đầu → cộng thêm → Hạn Resolution (ICT) | Điều cần để ý |
|---|---|---|---|
| 1 | Merch High, bắt đầu 22:40 T6 11/12; ON HOLD SUBS 30' | 02:40 T7 12/12 + 30' → **03:10 T7 12/12** | Ngày peak 12.12; chuyển STG SETUP trong 15' (22:55); quy trình sự cố chạy song song |
| 2 | Merch **Medium** (tạo EPP site mới, subsidiary đã đính email phê duyệt), bắt đầu 17:30 T6 11/12; ON HOLD RHQ 4h | 09:30 T7 + 4h → **13:30 T7 12/12** | Chỉ chuyển ON HOLD RHQ khi đã có email phê duyệt; RHQ duyệt xong ticket về STG SETUP, đồng hồ chạy lại; T7 nửa quân số, lại là 12.12 |
| 3 | COEC P3, bắt đầu 16:20 T6 11/12; ON HOLD HQ 3h (PC) | 08:20 CN + 3h → **11:20 CN 13/12** | CN Tech chỉ on-call: phải xong trước 19:00 T7; được duyệt lúc nào đồng hồ chạy lại lúc đó |
| 4 | COEC P1, bắt đầu 21:05 T3 08/12; 1h ở WAITING QA chờ người kiểm thứ hai kiểm lại ImpEx | 05:05 T4 09/12 + 0 → **05:05 T4 09/12** | Chờ kiểm nội bộ vẫn tính. Ngoài giờ Tech: on-call lớp 1 quét NEW mỗi 5' và chuyển ASSIGNED trong 30' (21:35); Shift Leader thấy P1 thì gọi on-call. Người kiểm thứ hai phải giữ chứng nhận Academy **L2 hoặc L3** của đúng service |
| 5 | Merch Medium, bắt đầu 06:15 CN 13/12; 2h ON HOLD SUBS + 1h ON HOLD COE | 22:15 CN + 2h (ON HOLD COE không cộng) → **00:15 T2 14/12** | CN Tech chỉ on-call: 1h chờ Tech ăn thẳng vào ngân sách; QA CN chỉ on-call (chờ chốt giờ QA) |
| 6 | COEC P4, bắt đầu 11:00 T5 10/12; ON HOLD SUBSIDIARY 6h + 18h | 11:00 T3 15/12 + 24h → **11:00 T4 16/12** | 120h = 5 ngày lịch gồm T7, CN; cộng tổng hai lần dừng |
| 7 | Merch Medium cần QA, bắt đầu 10:30 T7 12/12; 2h QA REVIEW (QA trả về) | 02:30 CN + 0 → **02:30 CN 13/12** | QA REVIEW vẫn tính; QA dùng chung SLA Merch; T7 QA chỉ ca sớm + Sub-Lead 1 ca chiều (tạm): xong trước 19:00 T7 |
| 8 | NZ duyệt ticket Low 10:00 T2 07/12 giờ NZDT; ON HOLD SUBS 1h30 | 04:00 T3 08/12 + 1h30 → **05:30 T3 08/12 ICT = 11:30 T3 08/12 giờ NZ** | 10:00 NZDT = 04:00 ICT; ca đêm Merch chuyển STG SETUP trước 05:18 |

### B. Bài tập B – cảnh báo
| # | Đề | Đáp án |
|---|---|---|
| 1 | Medium vào APPROVED-ES 13:00 T4, ON HOLD SUBS 15:00–17:00. Tính 50/70/85/95% và hạn | Dùng 2h trước khi dừng; 2h dừng không tính; 17:00 chạy tiếp. 50% (8h) = 23:00 T4; 65% = 01:24 T5; 70% = 02:12; 85% = 04:36; 95% = 06:12; hạn **07:00 T5**. 50% rơi ca tối; 65/70/85/95% và hạn rơi ca đêm. Handoff 16:00 và 00:00 phải nêu ticket; ở 85% (ngoài giờ) người nhận là Merch Lead on-call |
| 2 | High vào 09:00, ON HOLD SUBS 09:30–10:00; 13:18 chưa xong | Đã trôi 4h18 trừ 30' dừng = 3h48 → mức **95%**, còn **12 phút** (hạn 13:30). COE Lead (SDM làm thay) báo RHQ ngay kèm nguyên nhân + ETA; SDM được báo; Lead phải nhận ticket từ 85% (12:54); sự cố chạy song song |
| 3 | COEC P2 đã dùng 9h, chuyển SYSTEM SUPPORT 12:00 T4. 20:00 T5 đang ở mức nào? | Vẫn 9/16h (56%): đồng hồ dừng, không cảnh báo mới. CoE vẫn giữ ownership và follow-up theo RFP: P2 thuộc nhóm High, 2 ngày làm việc/lần → comment chậm nhất 12:00 T6; Tech L2 nhắc SDS India trên Maintenance Request. Ticket Merch liên kết ở ON HOLD COE vẫn chạy và qua đủ các mức |
| 4 | Ticket Low vỡ SLA, chỉ có 1 comment cảnh báo 50% | Không đạt cam kết "mọi ticket vỡ có ≥3 cảnh báo ghi lại". Ghi nguyên nhân vỡ trong 1 ngày làm việc; ghi nhận lỗi quy trình + phân tích vì sao 70/85/95% không được xử lý; đưa vào rà soát tuần; nếu do người thì mức L1 của people-risk ladder |

### C. Bài tập C – Composite và khấu trừ
| # | Đề | Đáp án |
|---|---|---|
| 1 | Resolution 97,50%, Response 98,00%, Pass Rate/Report/UA 100% | 97,50×0,75 + 98,00×0,15 + 10 = 73,125+14,700+10 = **97,8%** (>97% nhưng <98,5%: cần kế hoạch khắc phục nội bộ) |
| 2 | Quý: 97,2 – 96,4 – 97,1 | (97,2+96,4+97,1)/3 = **96,9%** → khấu trừ **1%** (rất gần 97% vẫn bị trừ) |
| 3 | Quý: 95,0 – 92,3 – 93,9 | 281,2/3 = **93,7%** → khấu trừ **3%** |
| 4 | T1 96,0%, T2 97,5%: T3 cần bao nhiêu để quý không bị trừ? | 3×97,0 − 96,0 − 97,5 = **97,5%** |
| 5 | Response 100%, BVT 100%: Resolution thấp nhất để tháng đạt 98,5%? | 0,75R + 15 + 10 = 98,5 → R = 73,5/0,75 = **98,0%** |
| 6 | 2.000 ticket; Resolution 50 vỡ; Response 30 trễ; 2 BVT đạt đủ | Resolution 97,50%, Response 98,50% → 73,125 + 14,775 + 10 = **97,9%** (dưới mốc nội bộ 98,5%) |

### D. Bài tập D – tình huống
| # | Đề | Đáp án |
|---|---|---|
| 1 | RHQ nhắn Mattermost 14:05 báo lỗi (đọc như P2); TM tạo COEC lúc 14:40 | Tạo sau 35' là vi phạm quy tắc 5 phút. Đồng hồ chính thức chạy từ NEW (14:40) nhưng CoE lập kế hoạch từ lần liên hệ đầu (14:05): ASSIGNED trước 15:23 (78'), muộn nhất 16:05 (2h); hạn Resolution theo kế hoạch 06:05 hôm sau (16h). Comment đầu ghi "First contact: 14:05 ICT via Mattermost" |
| 2 | Medium ở ON HOLD SUBS 6h; TM nói "đồng hồ đang dừng, không sao" — kiểm gì? | Chỉ đúng khi đủ 3 điều: câu hỏi đã ghi trong comment; ticket đã giao cho subsidiary (Assignee là người subsidiary); subsidiary chưa trả lời. Đọc comment cuối: nếu subsidiary đã trả lời → đồng hồ đang dừng sai thực tế → chuyển ngay về STG SETUP, giao lại người CoE, lập kế hoạch như thể thời gian đó đã tính SLA, kiểm ngày go-live. Nếu Assignee vẫn là người CoE mà dashboard không bắt được, báo Shift Leader. Chưa trả lời và go-live gần: nhắc qua comment Jira |
| 3 | Low trả từ REVIEW SETUP về STG SETUP; đã dùng 18h (10h ở ON HOLD SUBS). Ngân sách còn? Tạo ticket mới "cho sạch" đúng hay sai? | Còn **24 − 18 = 6 giờ** (10h ON HOLD SUBS và thời gian ở REVIEW SETUP không tính). Tạo ticket mới là **sai**: vi phạm quy tắc không tạo mới thay reopen, bị coi là làm đẹp số SLA |
| 4 | Merch Medium dùng 2h rồi sang ON HOLD COE; 5h sau COEC liên kết vẫn ON HOLD HQ chờ PC. TM nói "Tech dừng nên ticket mình cũng dừng" | **Sai.** ON HOLD COE vẫn chạy: đã dùng 2+5 = 7/16h (44%), còn 9h, sắp chạm 50%. Người tạo COEC đôn đốc Tech Lead ngay (PC đã gửi chưa, đủ kết quả staging chưa); nếu P0/P1 thì Tech nhắn Oliver qua Mattermost; Oliver là người duyệt duy nhất, không có người duyệt thay nên phải gửi PC sớm. 50%: Shift Leader ghi next action; 85%: Lead quyết định cập nhật subsidiary về ETA |
| 5 | T6 15:00 có 6 COEC P3 mới ở NEW, 2 cái cần PC. Hạn và kế hoạch? | Hạn ban đầu cả 6 là 07:00 CN (40h); mốc 65% là 17:00 T7. Hai ticket cần PC: hạn lùi đúng bằng thời gian ON HOLD HQ nhưng khi duyệt đồng hồ chạy lại ngay. CN Tech chỉ on-call nên thực tế phải xong trước 19:00 T7. Kế hoạch: ASSIGNED cả 6 ngay (trước 16:18); chia Level 1 ca chiều (đến 19:00) và Level 2 (đến 18:00) T6; 2 ticket PC: test staging, gửi PC, ON HOLD HQ "PC ticket pending" ngay chiều T6; phần còn lại cho ca sớm/chiều/L2 T7; ghi cả 6 vào bàn giao 19:00 T6 và sáng T7 |

### E. Câu hỏi kiểm tra (Phụ lục A, bài T3 phần SLA)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Resolution Tech P2? (8/16/24/40h) | **b – 16 giờ** | |
| 2 | Merch 4 promotion cùng lúc? | **b – Low, 24h** | >2 promotion = Low |
| 3 | Phản hồi đầu P3: RFP và mục tiêu nội bộ? | **a – 2 giờ và 78 phút** | |
| 4 | Trọng số Composite đúng? | **b** – Resolution 75%, Response 15%, Pass Rate 6%, Report Completion 3%, User Acceptance 1% | |
| 5 | Composite quý 96,9% khấu trừ? | **b – 1%** | |
| 6 | Composite quý 92,0% khấu trừ? | **b – 4%** | |
| 7 | COEC ở SYSTEM SUPPORT (chờ SDS India): đồng hồ Resolution? | **a – dừng** | CoE vẫn follow-up |
| 8 | Initial response Merch ghi nhận khi? | **b** – CoE chuyển APPROVED-ES → STG SETUP | |
| 9 | Merch ở ON HOLD COE: đồng hồ? | **b – chạy** | |
| 10 | Cần hỏi subsidiary thông tin thiếu? | **b** – comment câu hỏi, chuyển ON HOLD SUBS, giao ticket cho subsidiary | |
| 11 | Ở 95%, ai báo RHQ trước khi vỡ? | **c – COE Lead (SDM làm thay khi chưa bổ nhiệm)** | |
| 12 | Lọc ticket không owner? | **a – mỗi 30 phút, mọi ca** | |
| 13 | Low đã dùng 18h, bị trả từ REVIEW SETUP: ngân sách còn? | **b – 6 giờ** | |
| 14 | Mốc nội bộ Composite tháng và hành động? | **b** – 98,5%, kế hoạch khắc phục nội bộ do SDM trong 5 ngày làm việc | |
| 15 | Nhịp follow-up tối thiểu theo RFP cho COEC P3 ở SYSTEM SUPPORT? | **c – 4 ngày làm việc** | |

| # | Tình huống | Đáp án |
|---|---|---|
| 16 | COEC P0 tạo 01:30 CN, checkout một thị trường lỗi, cần ImpEx khẩn: ai phản hồi/xử lý, hạn, duyệt gì? | Ngoài giờ Tech: Tech on-call lớp 1 đang trực quét COEC NEW mỗi 5' và chuyển ASSIGNED (mục tiêu 15' với P0); Shift Leader Merch tại trung tâm thấy P0 thì gọi on-call ngay. On-call trả lời 15', có mặt tại trung tâm trong 60'; lớp 1 không nghe thì gọi lớp 2 → Tech Lead → SDM hotline. Hạn Resolution **05:30 CN** nếu không có dừng. ImpEx khẩn vẫn cần PC do Oliver duyệt: nhắn Oliver qua Mattermost (P0); trong lúc chờ COEC ở ON HOLD HQ "PC ticket pending" (đồng hồ dừng); ImpEx có dòng số PC + COEC gốc. Sự cố chạy song song: thông báo RHQ (Critical 30' nội bộ, RFP 2h), bridge, IM là on-call (CM-06, CM-07) |
| 17 | TM muốn hạ Medium → Low "để có thêm 8h". Bạn là Shift Leader | **Không được.** Priority chỉ sửa khi xếp sai theo bảng RFP, do Shift Leader/Sub-Lead, có lý do trên ticket. Ca bận thì dùng thang cảnh báo + đòn bẩy huy động: giao lại, chuyển người giữa thị trường, bench/on-call, ca sau đến sớm |
| 18 | Ticket vỡ SLA, không có comment cảnh báo nào | Lỗi quy trình: ghi nguyên nhân vỡ trong 1 ngày làm việc, phân tích nguyên nhân gốc vì sao không có cảnh báo, đưa vào rà soát tuần; ảnh hưởng cam kết "100% ticket vỡ có ≥3 cảnh báo ghi lại" |
| 19 | Viết cho RHQ về phản hồi đầu: (a) "The SLA for first response is 78 minutes." hay (b) "Our internal target is 78 minutes; the contractual SLA is 2 hours."? | **(b)**. 78' là mục tiêu nội bộ; cam kết hợp đồng (RFP) là 2h. Gọi mục tiêu nội bộ là "SLA" tạo cam kết mới không có trong hợp đồng |
| 20 | 21:00 dashboard có 3 ticket ON HOLD SUBS với Assignee là người CoE | Mở từng ticket, đọc comment cuối. Subsidiary đã trả lời → chuyển ngay về STG SETUP, giao người làm, tính lại hạn (coi thời gian từ lúc subsidiary trả lời là thời gian SLA), báo người nhận thời gian còn lại. Câu hỏi chưa được trả lời → đổi Assignee sang subsidiary (CoE quên giao). ON HOLD SUBS mà không có câu hỏi nào trong comment → chuyển về trạng thái đang làm (không dùng ON HOLD SUBS khi không thật sự chờ). Ghi giờ quét + kết quả vào nhật ký ca; nhắc lại quy tắc giao ticket ở stand-up ca sau |
| 21 | 18:10 T3, subsidiary VN tạo ticket giảm giá 2 SKU, cần live 00:00 cùng ngày. Bạn là Shift Leader ca tối, QA Team có thể không kịp. CoE vẫn phải làm gì? | Gắn label LastMinRequest + comment đúng câu RHQ ("Last minute request, please QA on your own when it goes live. If any issue, please contact us."). Giá là R3 nên vẫn bắt buộc: Doer đối chiếu brief và ghi tóm tắt giá trị chính lên ticket trước build (SKU, mức giảm, thời gian + múi giờ, site, stack, giới hạn dùng); chạy price sanity rules; Shift Leader duyệt; **gửi Knox approval theo approval path trong brief** (yêu cầu gấp không được bỏ bước này; không chuyển ON HOLD SUBS để chờ Knox); publish đúng giờ; sau 00:00 người thứ hai kiểm production và ghi handoff; đứng chờ hỗ trợ. Yêu cầu được đếm cho họp tuần RHQ |
| 22 | Tech TM cần xóa một user group qua Back Office trên production (5 giây); Merch TM cần đổi giá một SKU theo brief đã duyệt. Việc nào cần PC ticket? Ai duyệt, người duyệt vắng thì sao? | Việc của **Tech** cần PC ticket kể cả 5 giây: staging, tự QA, PC ghi thay đổi gì/vì sao/kết quả staging/rollback; COEC sang ON HOLD HQ; chỉ chạy sau khi duyệt. Đổi giá Merch **không** cần PC (đi workflow Shop Merchandising + Knox approval). **Oliver Leung duyệt duy nhất**, không người thay; Oliver vắng thì PC vẫn chờ, chậm ~3 giờ nên tạo sớm. Đổi production chưa có PC duyệt = chắc chắn bị RHQ tính strike |
| 23 | Subsidiary xin tạo EPP site mới nhưng chưa có phê duyệt; cùng ngày một ticket Shop Merch xin thêm domain email vào EPP access list. Xử lý từng ticket? | EPP site mới: hỏi đã có phê duyệt chưa; chưa có → trả subsidiary theo link template RHQ, tạm ON HOLD SUBS + giao subsidiary; có email đính ticket → ON HOLD RHQ cho Oliver (chỉ duyệt khi có email). Ticket thêm domain EPP là việc hoàn toàn của Tech → move chính ticket sang COEC, comment "Moved to COEC as this request is fully handled by the Tech team."; sau move theo SLA Tech |

---

## CM-04 Shift handbook – trực ca 24x7 và bàn giao ca

*(Bài T3 Foundation quiz – phần ca trực; checklist theo vai trò xem trực tiếp trong CM-04.)*

| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Ca đêm Merch chạy giờ nào, bao nhiêu người? (a 22:00–06:00 SL+2; b 00:00–08:00 SL+1; c 00:00–08:00 SL+4; d 16:00–24:00 SL+1) | **b** – 00:00–08:00, Shift Leader + 1, cả 7 ngày | Mục 2.4 |
| 2 | Ca ngày T2–T6 có SL + 14: 14 người gồm ai? | **b** – 8 Market Owner và 6 Team Member luân phiên | Mục 2.4 |
| 3 | Tech Level 1 bàn giao trực tiếp giữa hai ca vào khung nào? | **c** – 11:00–12:00, bàn giao trực tiếp, biên bản trên Confluence | Mục 6.3 |
| 4 | 21:00 T3 có COEC mới ở NEW, P0. Ai chịu trách nhiệm ticket và ai được gọi? (a không ai đến 04:00; b on-call Tech lớp 1 chịu trách nhiệm, Shift Leader thấy P0 thì gọi on-call; c QA on-call; d Market Owner) | **b** – Ticket COEC là việc của Tech Team: on-call Tech lớp 1 quét COEC NEW mỗi 5 phút, chuyển ASSIGNED và xử lý tại trung tâm; Shift Leader (có mặt tại trung tâm) thấy P0 thì gọi on-call lớp 1 ngay, **không nhận ticket Tech về mình** | Thay đổi production cần PC ticket được duyệt (mục 5.6) |
| 5 | On-call phải trả lời và có mặt tại trung tâm trong bao lâu? | **b** – 15 phút và 60 phút | Không làm remote (mục 3.6) |
| 6 | Bạn làm ca tối T4 (đến 24:00). Có được nhận ca ngày sáng T5 (08:00) để giúp bạn không? Vì sao? | **Không** | Chỉ nghỉ 8 giờ, dưới 16 giờ; ca tối không nối ca ngày (mục 2.8) |
| 7 | Ba thông tin bắt buộc cho mỗi ticket >70% trong handoff note? | Thời gian SLA còn lại; trạng thái (đang chờ gì); next action và owner mới | Mục 6.5 |
| 8 | 07:58, Shift Leader ca ngày chưa ký nhận handoff vì đang nghe điện thoại. Shift Leader ca đêm có được về lúc 08:00 không? | **Không** | Trách nhiệm chỉ chuyển khi ca vào ký nhận; ca ra ở lại đến khi có ký nhận và filter không owner rỗng (mục 6.2) |
| 9 | Ngày lễ VN có 5 thị trường BAU: Merch ca ngày, Tech, QA tối thiểu mấy người? | Merch ca ngày **10**; Tech **3**; QA **3**; ca đêm và ca tối Merch giữ SL+1 | Mục 2.6 |
| 10 | 05:00 bạn sốt cao, ca bắt đầu 08:00. Làm gì, theo thứ tự? | Gọi điện ngay cho Shift Leader đang trực (không chỉ nhắn tin); nói ca bị ảnh hưởng, thời gian vắng, ticket gấp; không cần nói chi tiết bệnh; làm thủ tục theo CO-02 | Mục 7.4.1 |
| 11 | Bạn là Shift Leader; 23:10 TM ca đêm báo không đi làm được. Ba việc đầu tiên? | Giao lại ticket gấp của người vắng; gọi backup, bench hoặc mời TM ca tối kéo dài (trong giới hạn làm thêm giờ) và báo Merch Lead on-call; cập nhật roster + handoff note | Ca đêm không để một người trong thời gian dài (mục 7.5) |
| 12 | 03:40 TM ca đêm gõ sai % giảm giá hai lần trên promotion R3. Nên làm gì? | Dừng thiết lập R3; báo Shift Leader; nghỉ ngắn, nhờ người còn lại kiểm thêm hoặc để Shift Leader giao lại | Mục 8.4 |
| 13 | Tuần on-call bắt đầu/kết thúc lúc nào? Ai giữ Tech lớp 2? | 08:00 T2 đến 08:00 T2 tuần sau; lớp 2 là TM tuần Level 2 cùng team với lớp 1 | Mục 2.7 |
| 14 | T7 10:00 có ticket nội dung Bahasa Indonesia. Ai trả lời, bằng ngôn ngữ gì? | TM trên ca trả lời bằng tiếng Anh; nội dung phải nhập bằng Bahasa chờ người bản ngữ; High thì Shift Leader gọi người bản ngữ | Mục 3.4 |
| 15 | Hai TM muốn đổi ca: năm điều kiện hợp lệ? | Người nhận đã chứng nhận (ca đêm cần L2); đúng quy tắc nghỉ; không quá 48h/tuần và một ngày cuối tuần; giữ người tiếng Thái, Bahasa; Lead duyệt trước và roster cập nhật trong ngày | Mục 7.3 |
| 16 | Sprint 1 (02/11–08/11): ca nào BiPlus chưa nhận? | Ca đêm Merch, Chủ nhật và on-call vẫn do SDSAP; QA chỉ shadow | Mục 2.5 |
| 17 | CN 17:00 kiểm queue thấy ticket Merch High cần QA gate hạn 23:00 CN. Bước tiếp? Điểm nào chờ chốt? | Ticket cần xử lý trước T2: người kiểm queue gọi QA on-call đến trung tâm (≤60'); thời gian ở QA REVIEW vẫn tính SLA Merch. Người kiểm queue CN đang chờ chốt, tạm là Shift Leader Merch đang trực | Mục 2.3, 9.4 |
| 18 | 20:30 T5, RHQ báo đợt BVT từ T2 tuần sau. Shift Leader ca tối làm gì? | **b** – Ghi handoff note và nhắn Merch Lead + Tech Lead để chỉ định PIC trong ngày làm việc kế tiếp | Không gọi QA on-call (QA không tham gia BVT); ngày BVT không thương lượng (mục 5.6) |
| 19 | ON HOLD SUBS có Assignee CoE; comment cuối là câu trả lời của subsidiary lúc 14:05. Làm gì, vì sao? | Chuyển ngay về STG SETUP và tiếp tục làm (hoặc giao owner làm) | Subsidiary trả lời bằng comment nhưng không chuyển trạng thái → đồng hồ dừng sai thực tế (mục 5.2) |
| 20 | Ticket Merch cần Tech chạy ImpEx: các bước trên Jira; ghi gì vào handoff khi hết ca trước khi Tech xong? | Không chuyển ticket Merch sang COEC. Tạo COEC mới ghi rõ cần Tech làm gì; liên kết hai ticket (issue link); chuyển ticket Merch sang ON HOLD COE + comment đang chờ Tech; đôn đốc Tech vì SLA Merch vẫn chạy. Phần ImpEx chạy production là việc của Tech: đi ticket COEC và PC ticket riêng, không đi theo ticket Merch. Hết ca: ghi vào handoff mục 4 ticket COEC liên kết, SLA còn lại, người đôn đốc mới và lần đôn đốc kế tiếp | Mục 5.1, 6.5 |

---

## CM-05 Quy trình yêu cầu dịch vụ (Service Request)

### A. Trắc nghiệm (bài tập 8.7, câu 1–13)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | RHQ nhắn yêu cầu Tech qua Mattermost lúc 14:00. Chậm nhất lúc nào phải có ticket COEC? (a 14:05; b 14:15; c 16:00; d khi bắt đầu làm) | **a – 14:05** | Mọi yêu cầu vào Jira trong 5 phút; việc Tech thì tạo ticket COEC (mục 2.1, 2.5) |
| 2 | Mục tiêu nội bộ initial response ticket Merch High? | **d – 15 phút** | P0/High 15', mức khác 78', RFP 2h (mục 2.7) |
| 3 | Initial response ticket Shop Merch dừng khi? | **b** – CoE chuyển APPROVED-ES → STG SETUP | Comment không đủ (mục 2.7) |
| 4 | Ticket một promotion BOGO cho VN có priority mặc định? | **b – Medium** | Một promotion đơn lẻ = Medium 16h (mục 4.1) |
| 5 | Due date của ticket là? | **c** – mốc sớm hơn giữa hạn SLA và giờ go-live trừ thời gian kiểm tra | Mục 3.1, 4.3 |
| 6 | Ai duyệt mọi thay đổi Merch trước production? | **c – Shift Leader đang trực** | Kể cả R1 (mục 5.6) |
| 7 | File giá 620 SKU cần thêm cấp duyệt nào? | **b** – Merch Lead hoặc Deputy vì E4 | File giá từ 500 SKU là E4 (mục 5.3) |
| 8 | Cần hỏi subsidiary trên ticket Merch, cách đúng? | **b** – comment, ON HOLD SUBS, giao ticket cho subsidiary | Với subsidiary chỉ dùng comment Jira (mục 3.5) |
| 9 | Merch ở ON HOLD COE chờ COEC liên kết; COEC ở SYSTEM SUPPORT. Đồng hồ? | **c** – COEC dừng, Merch vẫn chạy | SYSTEM SUPPORT dừng đồng hồ Tech; ON HOLD COE vẫn tính SLA Merch (mục 5.7, 5.8) |
| 10 | Tech xóa user group qua Back Office (5 giây): điều kiện bắt buộc? | **c** – PC ticket được Oliver Leung duyệt | Mọi thay đổi do Tech làm trên production (tạo/xóa/sửa dữ liệu; Back Office; ImpEx, Groovy; cronjob báo cáo, lấy dữ liệu sau PUMI) cần PC, kể cả việc 5 giây (mục 5.9) |
| 11 | Ticket Shop Merch đã INVALID nhưng subsidiary vẫn cần làm? | **b** – clone ticket và liên kết ticket cũ | INVALID không mở lại được (mục 6.7) |
| 12 | QA Team tham gia việc nào? | **c** – QA công việc hằng ngày của Merch | Không BVT, không QA Tech (mục 4.5) |
| 13 | Ai được ghi đè một lần từ chối của QA? | **c** – COE Lead, có báo RHQ | Mục 5.5 |

### B. Tình huống (đáp án mẫu, đánh số gốc 14–20)
| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 14 | 23:30 T7, COEC P1 mới ở NEW. Bạn là Shift Leader Merch | Ngoài cửa sổ Tech (19:00–04:00) ticket COEC là việc của Tech: on-call lớp 1 quét NEW mỗi 5' và chuyển ASSIGNED; Shift Leader có mặt tại trung tâm và gọi on-call khi thấy P0/P1. (1) Đọc ticket, kiểm thông tin cơ bản + dấu hiệu sự cố; (2) gọi on-call Tech lớp 1 ngay (CM-06), vì đây là P1: trả lời 15', có mặt tại trung tâm ≤60'; (3) on-call chuyển ASSIGNED và xử lý — ticket vẫn do Tech chịu trách nhiệm, bạn **không nhận ticket Tech về mình**; (4) ghi một dòng comment: đã gọi on-call lúc mấy giờ; (5) có dấu hiệu sự cố (mất doanh thu, không đặt được hàng) thì phân loại và mở quy trình sự cố theo CM-06 (IM tạm thời đến khi on-call có mặt); (6) ghi handoff note |
| 15 | Làm promotion R3; brief ghi giá sau giảm thấp hơn 60% giá niêm yết, requester đang họp, go-live còn 5h | Không đoán, không thiết lập theo giá đáng ngờ. (1) Comment nêu giá vi phạm price sanity rules, đề nghị requester xác nhận bằng văn bản; (2) ON HOLD SUBS, giao ticket cho requester, watch; (3) báo Market Owner/Shift Leader; (4) chuẩn bị phần không phụ thuộc giá nhưng không publish; (5) có trả lời thì về STG SETUP ngay; không kịp go-live vì chờ subsidiary thì comment rõ nguyên nhân; (6) quy tắc publish 23:59 không áp dụng cho giá chưa được xác nhận |
| 16 | Một ngày sau khi chuyển special price sang REVIEW SETUP, subsidiary comment thiếu 2 SKU | Đưa ticket từ REVIEW SETUP về STG SETUP. Giữ nguyên priority; đồng hồ chạy tiếp từ phần đã dùng, không đặt lại. Bổ sung 2 SKU theo runbook, cập nhật tóm tắt kiểm tra nội bộ cho phần đổi, qua lại QA REVIEW (special price là R3) và Shift Leader duyệt, đính bằng chứng mới, chuyển lại REVIEW SETUP. Không INVALID rồi clone. Ghi nguyên nhân thiếu SKU (lỗi CoE hay brief thiếu) để cải tiến intake kit/runbook |
| 17 | 15:45, bạn là TM ca ngày thiết lập dở ticket R2 go-live 20:00; ca hết 16:00 | Không bỏ dở không bàn giao, không vội chuyển QA REVIEW khi chưa self-check. (1) Cập nhật ticket: đã làm gì, còn gì, rủi ro, giờ go-live 20:00; (2) ghi vào handoff note với owner mới do Shift Leader ca tối chỉ định; (3) nói trực tiếp owner mới trong 15' chồng ca; (4) go-live 20:00 cần QA mà gần ngưỡng nội bộ 17:00 → báo Shift Leader ngay để sắp QA, hoặc nếu QA thật sự không kịp thì áp quy tắc last-minute request (mục 3.7) |
| 18 | Subsidiary cần 500.000 mã coupon, giao diện không làm được; bạn là Merch PIC | (1) Không chuyển ticket Merch sang COEC; (2) tạo COEC mới, ghi rõ cần ImpEx tạo 500.000 mã cho ticket nào; (3) liên kết bằng issue link; (4) ticket Merch → ON HOLD COE, comment theo mẫu A.6; (5) SLA Merch vẫn chạy: bạn đôn đốc Tech nội bộ; (6) Tech xong (đã có PC duyệt): kiểm mẫu mã, về STG SETUP, QA REVIEW (coupon là R3), Shift Leader duyệt, rồi REVIEW SETUP |
| 19 | Promotion R3 ở REVIEW SETUP, đã QA PASS + Shift Leader duyệt, go-live 00:00 mai; 23:59 vẫn chưa có duyệt của subsidiary | **Kiểm Knox approval đã gửi hoặc đã có theo path của brief**, rồi publish live như đã thống nhất, đúng thiết lập đã QA PASS và được duyệt, không sửa thêm. Comment theo mẫu A.8. Lúc go-live QA lại trên production (R3: người thứ hai kiểm trong 30', monitor 2h). Ticket có thể vẫn ở REVIEW SETUP đến khi subsidiary duyệt; không tự đóng (mục 6.5) |
| 20 | Ticket promotion cho 6 thị trường, giờ go-live khác nhau, 2 thị trường có 2 đợt | (1) >5 thị trường là E4: cần Merch Lead/Deputy duyệt thêm; (2) ghi giờ go-live từng thị trường, từng đợt theo giờ địa phương và giờ VN; (3) xem quy tắc nhiều thị trường ở MR-04 ch.5; (4) mỗi thị trường có Market Owner tham gia; (5) QA Sub-Lead sắp thứ tự kiểm theo giờ go-live; (6) priority theo số promotion trong ticket; (7) kiểm cộng dồn với promotion đang chạy; (8) sau REVIEW SETUP ticket ở PENDING LAUNCH, mỗi đợt go-live QA lại trên production rồi về PENDING LAUNCH; chỉ sang LAUNCH VERIFICATION khi mọi đợt đã live |

---

## CM-06 Quy trình sự cố và on-call (Incident)

### A. Trắc nghiệm (câu 1–14)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Trường hợp nào là **incident**? (A tạo promotion mới tuần sau; B promotion hôm qua đang giảm 51% thay vì 15%; C hỏi cách đọc báo cáo SLA; D xin quyền dashboard) | **B** | Thiết lập đã live sai giá là sự cố; A là Service Request (mục 1.2) |
| 2 | Lúc 03:00 ai xác nhận severity sự cố Merch? | **B – Shift Leader đang trực tại trung tâm** | Có mặt mọi giờ, xác nhận sự cố Merch/QA trong 15' (mục 2.3) |
| 3 | Mục tiêu nội bộ initial notification sự cố **Critical** (từ T0)? | **B – 30 phút** | 30' là nội bộ; RFP là 2h (mục 1.3, 2.5) |
| 4 | Requester chọn priority "High" trên form cho promotion mới. CoE làm gì? | **C** – xử lý như Service Request; chỉ khởi động incident khi CoE xác nhận theo severity matrix | Priority trên form không tự khởi động incident (mục 1.2) |
| 5 | On-call Tech đang trên taxi đến trung tâm. Việc nào được phép? | **C** – nghe Shift Leader đọc ticket qua điện thoại và chỉ đạo bằng lời | Không làm remote; ngoài trung tâm chỉ nghe và chỉ đạo bằng lời (mục 4.1, 4.5) |
| 6 | Gọi on-call lớp 1 từ 02:05 không ai trả lời. 02:15 gọi ai? | **B – on-call lớp 2** | Phút 10 lớp 2, phút 15 Tech Lead, phút 20 SDM hotline (mục 4.4) |
| 7 | Ai được liên hệ SDS India trong sự cố? | **C** – chỉ Tech Team Level 2, kể cả on-call Tech | Qua Maintenance Request và trên bridge (mục 2.4, 3.5) |
| 8 | 14:00 T3 thấy special price sai đã live; sau khi báo Shift Leader, việc tiếp theo? | **B** – khống chế (trả giá/ẩn SKU) trong 30' và báo RHQ + subsidiary trong 30' | Khống chế trước, phân tích sau (mục 6.2) |
| 9 | RCA sự cố Critical, tính từ T-restore? | **B** – nháp 36h, gửi 48h (nội bộ), tối đa 72h | Mục 2.9 |
| 10 | Câu nào **sai** về emergency change của Tech? | **C** – "P0 lúc 02:00 thì chạy trước, tạo PC sau trong 2 giờ" | Không có PC đã duyệt thì không thay đổi gì trên production, kể cả P0; chỉ phần ghi chép đầy đủ được làm sau trong 2h (mục 2.6) |
| 11 | PIC của CoE rời bridge khi nào? | **C – khi RHQ cho phép** | RFP 3.9 (mục 5.1) |
| 12 | Đã gửi PC cho bước sửa P1, chờ Oliver duyệt: COEC gốc ở đâu? | **B – ON HOLD HQ**, comment "PC ticket pending" | Oliver duyệt xong về IN PROGRESS (mục 2.6, 2.11) |
| 13 | COEC của P0 ở SYSTEM SUPPORT vì SDS India đang rollback. Câu nào đúng? | **B** – đồng hồ dừng nhưng CoE vẫn giữ ownership, PIC ở lại bridge, cập nhật RHQ đúng nhịp | Chờ chỉ dừng đồng hồ (mục 2.1, 2.11, 6.4) |
| 14 | Promotion sai giá đã tắt; bật lại cần sửa 200.000 mã coupon bằng ImpEx. Làm gì với ticket Shop Merch? | **B** – giữ ON HOLD COE, tạo COEC mới, liên kết, comment đang chờ Tech | Không move ticket Merch sang COEC; ON HOLD COE vẫn chạy đồng hồ; không dùng ON HOLD SUBS để dừng đồng hồ; phần ImpEx của Tech vẫn cần PC ticket (mục 6.2, 2.11) |

### B. Tình huống (câu 15–20)
| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 15 | 23:40, Shift Leader ca tối đang làm IM tạm thời cho P0; on-call đến 00:05; ca kết thúc 00:00 | Không rời lúc 00:00. Ghi sự cố vào handoff note, bàn giao queue và hotline cho Shift Leader ca đêm, ở lại giữ vai tạm thời đến khi on-call nhận vai theo checklist năm điều; giờ thêm theo CO-02 (mục 3.4, 3.6) |
| 16 | Đến giờ update sự cố Critical nhưng chưa có tin mới | Vẫn gửi đúng giờ trên Mattermost: *"Update 3 at [time] ICT ([time] SGT). No change since the last update. We are still [action]. Next update by [time]."* (mục 5.4) |
| 17 | Sai giá đã live, nhưng bản kiểm tra nội bộ (internal check) trên ticket khớp đúng brief mà subsidiary đã duyệt, và brief đó ghi giá trị sai. CoE làm gì ngay, trách nhiệm kết luận thế nào? | CoE vẫn **rollback ngay** (khống chế trong 30'), báo RHQ và subsidiary trong 30' và xử lý như incident bất kể ai sai. Nguồn sai (brief, cấu hình hay thao tác) ghi trong RCA; **kết luận trách nhiệm theo điều tra chung với RHQ (RFP 3.10), không khẳng định trước** (hộp chờ chốt mục 6.2). Bộ bằng chứng nội bộ: brief gốc đã duyệt, Knox approval (nếu có), tóm tắt giá trị chính của Doer, kết quả Checker |
| 18 | TM thấy trang tài khoản khách TH hiện đơn của khách khác, muốn chụp bằng điện thoại | Không chụp, không lưu ảnh có dữ liệu khách. Báo Shift Leader ngay; ghi mô tả bằng lời + vị trí (trang, mã đơn) lên ticket; xử lý Critical và báo sự cố an toàn thông tin trong 1 giờ theo CM-10 (mục 6.5) |
| 19 | Trên bridge subsidiary hỏi: "Will BiPlus compensate us for these orders?" | Không hứa, không bàn mức bồi thường: *"Compensation is decided after the joint investigation with RHQ. Right now our priority is to restore the service and list the affected orders within 24 hours."* Bồi thường theo CO-08 (mục 2.8) |
| 20 | 02:40 CN, bạn là IM Tech của P0; PC đã gửi + nhắn Oliver 30' trước chưa phản hồi; TM đề nghị "chạy luôn, 5 giây" | Không chạy. Ticket giữ ON HOLD HQ "PC ticket pending". Gửi update đúng nhịp ghi rõ "waiting for PC ticket approval" và nói thẳng khách vẫn bị ảnh hưởng; nhắn lại Oliver và đội RHQ trên Mattermost, COE Lead gọi — chỉ để thúc, **không có người duyệt thay** (Oliver vắng thì chờ ~3 giờ là bình thường); trong lúc chờ tiếp tục khống chế bằng cách không cần thay đổi Tech nếu có. Chạy khi chưa có PC duyệt là vi phạm quy tắc RHQ và **chắc chắn bị strike** dù chỉ 5 giây (mục 2.6, 2.9) |

---

## CM-07 Change, Problem và cải tiến liên tục

### A. Bài tập phân cấp 18 tình huống (mục 8.2)
Cột: cấp (R1/R2/R3, thay đổi Tech, emergency, Samsung-side) – có đạt E4 không (chỉ Merch) – cổng bắt buộc.

| # | Tình huống | Cấp | E4? | Cổng bắt buộc và ghi chú |
|---|---|---|---|---|
| 1 | Đổi text "Free shipping" trên trang 30 SKU ở VN | R1 | Không | Shift Leader kiểm và duyệt; doer kiểm storefront; 30 dòng nên không cần file diff |
| 2 | Upload special price 650 SKU ở TH | R3 | Có (file giá ≥500 SKU) | Price sanity, kiểm tra nội bộ, file diff (>100 dòng), QA 100%, Shift Leader, Merch Lead; Knox approval theo approval path; rollback viết trước; kiểm 30'; order monitor 2h |
| 3 | Tạo coupon 20 USD, giới hạn 100 lượt, cho SG | R3 | Không (exposure tối đa 2.000 USD) | Price sanity (có giới hạn lượt), kiểm tra nội bộ, QA, Shift Leader; Knox approval; kiểm 30'; monitor 2h |
| 4 | Cập nhật virtual stock pre-order 200 đơn vị cho 5 SKU ở MY | R2 | Không | QA nếu service có QA gate, không thì lấy mẫu; Shift Leader duyệt; doer kiểm storefront |
| 5 | Promotion BOGO áp dụng đồng thời 6 thị trường | R3 | Có (>5 thị trường) | Như R3 (gồm Knox approval) + Merch Lead duyệt thêm; go-live trong ca trực từng thị trường |
| 6 | Tech xóa user group khỏi 50 tài khoản khách qua Back Office (5 giây) | Thay đổi Tech | Không áp dụng | Vẫn cần PC do Oliver duyệt (duyệt duy nhất); làm trên staging trước, tự QA; chờ duyệt ở ON HOLD HQ |
| 7 | Thay banner trang chủ ID, có T&C campaign | Tạm R2 (CMS có T&C, chờ chốt) | Không | QA theo service hoặc lấy mẫu; Shift Leader duyệt; hỏi Shift Leader khi tiếp nhận |
| 8 | Thêm phương thức trả góp vào payment mode AU (COEC) | Thay đổi Tech rủi ro cao (payment) | Không áp dụng | Staging, tự QA, another set of eyes (người giữ chứng nhận L2 hoặc L3 của service), tự QA cả rollback trên staging; PC kèm kết quả staging; ON HOLD HQ khi chờ; kiểm kết quả sau chạy |
| 9 | VN ticket Shop Merch xin cấp EPP access cho domain email mới; toàn việc Tech | Thay đổi Tech (access rule); move ticket sang COEC | Không áp dụng | Toàn việc Tech nên move chính ticket sang COEC, không tạo mới (RHQ đã xác nhận CoE tự move, không cần quyền admin); staging, tự QA, another set of eyes, PC; kiểm quyền đúng nhóm sau chạy |
| 10 | Tạo multistore mới cho kênh SMB ở PH | R2 | Không | QA nếu có QA gate hoặc lấy mẫu; Shift Leader duyệt |
| 11 | Incident đang mở: tắt ngay promotion giảm sai đang live ở VN | Emergency change trong incident | Không áp dụng | Khống chế trong 30'; Shift Leader làm IM tạm thời, Lead duyệt, RHQ được báo trên bridge; ghi lại trong 2h; QA sau khi sửa |
| 12 | Release code hằng tháng sửa lỗi checkout | Samsung-side | Không áp dụng | Dev + Samsung L2/L3 triển khai; enhancement chỉ go-live khi BVT 100% pass + sign-off; PIC Merch/Tech của CoE xác minh sau release |
| 13 | Sửa dữ liệu hàng loạt 300 đơn trả hàng TH bằng script Groovy mới | Thay đổi Tech rủi ro cao | Không áp dụng | Script mới → kết quả staging bắt buộc; another set of eyes (người giữ chứng nhận L2 hoặc L3), file diff, rollback chuẩn bị trước; PC kèm kết quả staging và rollback; Groovy có dòng header số PC + COEC gốc (thiếu = strike, mục 10.7) |
| 14 | Đổi delivery mode 40 SKU ở VN trong 48h trước Black Friday, không liên quan campaign | R2 trong freeze | Không | Chỉ áp dụng nếu RHQ duyệt (bằng chứng trên ticket); không thì thống nhất với requester dời sau sự kiện |
| 15 | Promotion giảm 30% cho 1 SKU flagship 1.000 USD, ~400 đơn/2 ngày, SG | R3 | Có (exposure >10.000 USD) | Như R3 + Merch Lead duyệt thêm |
| 16 | Hybris hard freeze flagship: MY xin đổi giá phút chót 2 SKU flagship | R3, ngoại lệ trong freeze | Xét theo exposure | Phải có phê duyệt ngoại lệ; CoE lấy bằng chứng từ trang compliance, ghi trong body ticket; rồi đủ cổng R3 **gồm Knox approval theo approval path trong brief**. Không có phê duyệt thì không làm |
| 17 | Hard freeze flagship: SG cập nhật stock 3 SKU | R2, được phép trong hard freeze | Không | Stock luôn được cập nhật; làm theo cổng R2 như ngày thường |
| 18 | 18:00 PH được duyệt ticket 1 promotion giảm 10% cần live 00:00 cùng ngày | R3, last-minute request | Thường không | Không đủ thời gian QA: comment mẫu last-minute, subsidiary tự QA khi go-live, CoE đứng chờ hỗ trợ; vẫn price sanity, kiểm tra nội bộ, Shift Leader duyệt, **Knox approval**, người thứ hai kiểm lúc go-live (kiểm soát tối thiểu); gắn nhãn LastMinRequest để đếm |

### B. Câu hỏi kiểm tra (20 câu, bài T3)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Một promotion giảm giá thuộc cấp rủi ro nào? | **c – R3** | Mọi promotion là R3 |
| 2 | R3 đạt E4 khi nào? | **b** – exposure ≥10.000 USD, hoặc >5 thị trường, hoặc file giá ≥500 SKU | Một trong ba điều kiện là đủ |
| 3 | Khi đạt E4, ai duyệt thêm ngoài Shift Leader? | **b** – Merch Lead hoặc Deputy Lead | Deputy khi Lead vắng |
| 4 | R2 thuộc service không có QA gate được QA kiểm thế nào? | **c** – lấy mẫu 20%, tối thiểu 3/tuần/cụm; mẫu FAIL thì kiểm toàn bộ tuần đó | Quy tắc lấy mẫu của QA |
| 5 | Kiểm tra sau thay đổi R3 do ai, trong bao lâu? | **b** – người thứ hai, trong 30 phút | Không phải doer; storefront và test order |
| 6 | Order anomaly monitor sau go-live R3? | **b** – mỗi 15 phút trong 2 giờ | |
| 7 | Staging thật dùng cho việc nào? | **b** – thay đổi Tech trước khi gửi PC; promotion quá phức tạp khi đội tự quyết thử; BVT; đào tạo | STG SETUP không phải staging; Merch setup trên production |
| 8 | 48h trước Black Friday, thay đổi nào được áp dụng? | **b** – chỉ thay đổi đã được RHQ duyệt (và emergency change trong incident) | Freeze 48h |
| 9 | Ai được vượt quyết định FAIL của QA? | **c** – COE Lead, kèm báo RHQ | Merch Lead không được vượt |
| 10 | Problem record đóng khi nào? | **c** – khi không tái diễn trong 30 ngày | |
| 11 | Tech chạy ImpEx mới trên production: điều nào bắt buộc? | **c** – chạy trên staging, PC được Oliver duyệt, có dòng số PC + COEC gốc trong ImpEx | Thiếu dòng số ticket là một trong ba việc chắc chắn bị strike; ImpEx/script mới cần người kiểm thứ hai giữ chứng nhận L2 hoặc L3 |
| 12 | Chờ duyệt PC, COEC gốc ở đâu? | **b** – ON HOLD HQ "PC ticket pending" | ON HOLD HQ dừng đồng hồ; Oliver duyệt xong về IN PROGRESS |
| 13 | Promotion "thiết lập xong, chưa live" nghĩa là gì? | **b** – đã setup trên production, publish sang simulator và test bằng promotion simulator Back Office 2.0, chưa publish live | Đến giờ go-live mới publish live |
| 14 | Brief yêu cầu giảm 85% cho một điện thoại. Làm gì? | (mẫu) | Vi phạm price sanity rule: giữ ticket, không tự sửa giá trị; gửi một câu hỏi gộp (ON HOLD SUBS, giao subsidiary); chỉ làm khi subsidiary xác nhận bằng văn bản trên ticket; sau đó vẫn kiểm tra nội bộ, QA, Knox approval, duyệt như R3 |
| 15 | 22:10 giờ VN, Shift Leader thấy promotion R3 đạt E4 go-live 00:00 SGT (23:00 VN) chưa có duyệt E4; Merch Lead on-call ở nhà. Làm gì? | (mẫu) | Gọi Lead on-call ngay (trả lời 15', có mặt ≤60'); không go-live khi chưa có duyệt E4; báo requester và thống nhất giờ go-live mới trên ticket nếu Lead không kịp; ghi lại diễn biến |
| 16 | 10 phút sau go-live, người thứ hai thấy giá giảm sai. Ai làm gì, trong bao lâu? | (mẫu) | Rollback/kill switch ngay; mở incident, Shift Leader làm IM tạm thời; khống chế trong 30'; báo RHQ + subsidiary trong 30'; liệt kê đơn bị ảnh hưởng; RCA mục tiêu 48h, chậm nhất 72h (CM-06) |
| 17 | RCA ghi nguyên nhân gốc "Team Member nhập sai". Vì sao chưa đạt, sửa thế nào? | (mẫu) | Đổ lỗi cá nhân, không chỉ ra chỗ sửa hệ thống. Hỏi tiếp "vì sao hệ thống để nhập sai mà không bị chặn": runbook, checklist, mẫu kiểm tra nội bộ, QA thiếu gì; ghi bằng chứng; CAPA sửa kiểm soát. RCA vẫn ghi trung thực nếu có người không theo quy trình hoặc làm khi chưa được chứng nhận — RHQ có thể tính strike (mục 10.7) |
| 18 | TM đề xuất dán file giá của subsidiary vào công cụ AI công cộng để so với brief. Được không? | (mẫu) | Không: file giá là dữ liệu Samsung, chỉ dùng AI đã được RHQ duyệt và không bao giờ đưa dữ liệu Samsung vào. Đúng: so bằng checklist hai cột và file diff trên hệ thống Samsung; muốn tự động hóa thì ghi improvement record đề xuất RHQ |
| 19 | Tech chạy Groovy trên production đã có PC duyệt nhưng quên dòng số PC + COEC gốc. Hậu quả? CoE ngăn thế nào? | (mẫu) | Vài ngày sau RHQ/HQ gửi email yêu cầu giải trình, Lead nộp RCA và RHQ ghi **strike** đầu tiên cho người chạy (RHQ quyết định; 3 strike/năm dương lịch = loại vĩnh viễn; người nhận strike vào bậc kèm cặp L1 của people-risk ladder; BiPlus thay người trước strike thứ ba). Ngăn bằng checklist trước khi chạy (có PC duyệt, có dòng số ticket, có kết quả staging) và another set of eyes đọc lại file; ghi nguyên nhân xem có cần mở problem |
| 20 | Hard freeze flagship, subsidiary xin đổi giá phút chót và nói "không vào được trang compliance". Làm gì? | (mẫu) | CoE có quyền vào trang compliance: tìm phê duyệt ngoại lệ. Có → ghi bằng chứng vào body ticket rồi làm đủ cổng R3 (gồm Knox approval theo approval path trong brief). Không có → trả lời subsidiary cần phê duyệt ngoại lệ trước, không làm. Không tự quyết ngoại lệ |

---

## CM-08 Leo thang và giao tiếp với RHQ, thị trường, Samsung L2 và L3

### A. Bài tập viết (tiếng Anh, dùng cho phần viết của T2 và 5 tình huống giao tiếp của Merch track)
Đáp án mẫu dưới đây là bản rút gọn ý chính; bản đầy đủ theo mẫu ở CM-08 chương 4.

| # | Đề | Thao tác Jira | Ý chính của comment mẫu |
|---|---|---|---|
| 1 | Viết lại comment kém "pls send sku asap, promo cannot setup. thx" (DEMO-2101, MY, 1 promotion, thiếu danh sách SKU và giá khuyến mại) | Comment, ON HOLD SUBS, giao ticket cho requester | Chào + cảm ơn; nêu rõ cần (1) danh sách SKU, (2) giá khuyến mại từng SKU; đã giao ticket lại; "we will complete the setup within 4 hours" sau khi nhận; ghi tên owner |
| 2 | Phản hồi đầu: TH duyệt DEMO-2102 lúc 10:05; 1 BOGO, go-live 00:00 T6; thiếu T&C cho trang offer | Chuyển APPROVED-ES → STG SETUP trước 11:23 (78'), Assignee là mình, comment; sau đó ON HOLD SUBS giao requester chờ T&C; trong lúc chờ chuẩn bị promotion rule | Giới thiệu tên/team; hiểu yêu cầu (1 BOGO TH, go-live 00:00 T6, Medium); cần T&C trong một lần trả lời; đang chuẩn bị promotion rule; hẹn cập nhật trước 16:00 ICT; ghi owner |
| 3 | Báo trễ: Low DEMO-2103 (special price 40 SKU PH), hạn 18:00 ICT; kiểm tra nội bộ (price sanity) thấy 3 SKU giá thấp hơn 50% giá hiện tại, cần hỏi requester; 15:30 biết không kịp | Sau khi đăng: ON HOLD SUBS, giao requester | Xin lỗi, setup sẽ trễ; lý do: 3 SKU giá >50% dưới giá hiện tại (list ở comment trên), cần xác nhận; 37 SKU còn lại đã sẵn sàng; dự kiến xong 1 giờ sau khi xác nhận; hẹn cập nhật trước 17:30 ICT (18:30 giờ PH) |
| 4 | Chuyển Samsung L2/L3: COEC P2 DEMO-2104, từ 08:00 ICT ~25 đơn VN thanh toán nhưng không sang hệ thống đơn; đã kiểm cấu hình, đẩy lại 1 đơn không được; nghi middleware | Tech L2 tạo Maintenance Request cho SDS India, liên kết DEMO-2104, chuyển DEMO-2104 sang SYSTEM SUPPORT (đồng hồ Tech dừng), comment cho requester theo Mẫu 8 | MR gồm: ticket + priority P2 + thị trường; tác động (~25 đơn từ 08:00 ICT/09:00 SGT đã trả tiền nhưng không xử lý); cách tái hiện; bằng chứng (order ID + timestamp); đã kiểm tra (cấu hình đúng, đẩy lại thất bại, nghi middleware); yêu cầu kiểm middleware, hạn theo SGT; **CoE giữ ownership**, hẹn follow-up |
| 5 | Thông báo sự cố ban đầu (Mẫu 9): 21:10 ICT T7 coupon giảm 50% AU dùng được cho mọi sản phẩm; 8 đơn; chặn lúc 21:25 | — | `[INCIDENT] [Critical] \| AU \| Started 21:10 ICT (01:10 AEDT Sunday)`; Impact; Status: Contained (chặn 21:25 ICT); actions so far; Incident Manager = Merch Lead (on call); bridge; next update 22:40 SGT. Mức Critical/High do IM xác định theo severity matrix; 21:10 ICT T7 = 01:10 CN giờ AU |
| 6 | Từ chối lịch sự: SG xin sửa template giao diện trang giỏ hàng "cho nhanh" (enhancement của dev); Lead xác nhận ngoài phạm vi | — | Cảm ơn; việc này nằm ngoài phạm vi service của Ops CoE, template là enhancement do đội phát triển; đề xuất gửi enhancement request qua RHQ; nếu cho là trong phạm vi, CoE sẽ hỏi RHQ xác nhận |
| 7 | English note cho RHQ khi TH Market Owner trả lời requester bằng tiếng Thái (đổi banner trang chủ, xong trước 15:00, cần file đúng kích thước) | — | `[EN note for RHQ]` đã nhận yêu cầu đổi banner TH; xong trước 15:00 ICT (15:00 local); đã xin requester file banner đúng kích thước; owner |
| 8 | Call summary: gọi đầu mối ID 14:20 ICT về DEMO-2108; go-live đổi 00:00 → 06:00 ngày 12/12 giờ địa phương; requester gửi file SKU cuối trước 17:00 ICT | — | Agreed: go-live 06:00 local 12 Dec; Open: file SKU cuối – owner requester – trước 17:00 ICT; Next update: CoE xác nhận setup trước 20:00 ICT |
| 9 | Chờ COEC: Merch DEMO-2109 (MY) cần 500.000 mã coupon, cần ImpEx | Không chuyển sang COEC; tạo COEC mới (vd DEMO-2120) ghi rõ cần ImpEx 500.000 mã coupon + thị trường/go-live/hạn của DEMO-2109; issue link; DEMO-2109 → ON HOLD COE (SLA Merch vẫn chạy); đôn đốc Tech đầu ca và giữa ca; phần Tech chạy ImpEx production đi PC ticket riêng | Comment (Mẫu theo CM-13 Phụ lục B): "Tech support needed. COEC ticket DEMO-2120 has been raised and linked. Pending Tech team support."; ticket vẫn do CoE giữ; next update 15:00 SGT |
| 10 | Yêu cầu gấp: PH tạo + duyệt DEMO-2110 lúc 18:00 ICT, cần promotion live 00:00 cùng đêm (giờ PH); QA không kịp | Shift Leader quyết dùng mẫu last-minute; gắn label yêu cầu gấp (CM-09) | Comment đúng câu RHQ: "Last minute request, please QA on your own when it goes live. If any issue, please contact us." Việc thêm: label LastMinRequest đếm cho họp tuần RHQ; vẫn setup đúng runbook + trạng thái đúng (SLA vẫn chạy); R3 vẫn kiểm tra nội bộ (Doer ghi tóm tắt giá trị chính lên ticket), price sanity, Shift Leader duyệt (CM-07), **gửi Knox approval theo approval path trong brief** (QA không kịp không phải lý do bỏ Knox), người thứ hai kiểm production lúc go-live; đứng chờ hỗ trợ lúc 00:00 giờ PH (23:00 ICT) |
| 11 | PC ticket pending: COEC P1 DEMO-2111 (MY, phương thức thanh toán lỗi) cần Groovy mới; Tech đã test staging, nhờ thêm một người kiểm (script mới → cần kết quả staging và người thứ hai giữ chứng nhận L2 hoặc L3 của đúng service) và tạo PC DEMO-2112 | DEMO-2111 → ON HOLD HQ (đồng hồ Tech dừng), comment Mẫu 18; vì P1 cần sửa ngay, Tech Lead (ngoài giờ: on-call) nhắn Oliver qua Mattermost; Oliver duyệt → DEMO-2111 về IN PROGRESS, chạy Groovy theo checklist (script có dòng số PC DEMO-2112 + COEC gốc DEMO-2111) | Comment (Mẫu 18 theo CM-13 Phụ lục B): "PC ticket pending: DEMO-2112 raised for approval. Work will resume once approved… Staging result: passed… expected within 30 minutes after approval." Tin Mattermost cho Oliver: urgent PC ticket DEMO-2112 cho COEC DEMO-2111 (P1, MY), staging + ảnh dữ liệu trong PC, xin duyệt; ký tên/chức danh |
| 12 | Đã publish, chưa nhận phản hồi: DEMO-2113 (VN) ở REVIEW SETUP từ 14:00 với bằng chứng QA; go-live 00:00 mai; 23:59 subsidiary chưa duyệt | Publish như đã thống nhất (quy tắc RHQ), không chờ subsidiary đọc hết | Comment: "Published as agreed. We have not received your feedback on the QA evidence yet. The promotion for VN is published to go live at 00:00 ICT… If anything is not as expected, please let us know in this ticket." Sau đó ca trực QA lại trên production lúc go-live (MR-04) |

### B. Câu hỏi kiểm tra (Phụ lục A)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Kênh chính thức cho mọi trao đổi về một ticket? | **b – comment trên Jira Samsung** | |
| 2 | Ngoài 08:00–17:00 T2–T6, cấp leo thang thứ hai của Merch sau Shift Leader? | **c** – Merch Lead on-call (Deputy Lead tuần thứ tư) | |
| 3 | Gọi on-call không ai nghe: sau bao lâu gọi người tiếp theo? | **b – 15 phút** | |
| 4 | Ai được liên hệ trực tiếp Samsung L2/L3 về ticket Tech? | **c – Tech Team Level 2** | |
| 5 | SDM hotline 24/7 cam kết? | **a** – trả lời 15 phút, huy động team trong 30 phút | |
| 6 | Kênh chat với RHQ? | **b – Mattermost (100%)** | |
| 7 | Khi RHQ chưa chốt kênh với subsidiary, CoE trao đổi qua? | **b – comment Jira** | |
| 8 | Requester TH viết tiếng Thái lúc 22:00 T3. CoE trả lời? | **b** – bằng tiếng Thái kèm English note cho RHQ | |
| 9 | Người mới thôi duyệt tin nhắn khi? | **c** – đủ 4 tuần **và** ít nhất 50 tin đạt | |
| 10 | Thông báo sự cố ban đầu gửi RHQ với Critical? | **b** – trong 30 phút (nội bộ; RFP 2h) | |
| 11 | Câu nào phù hợp trong comment gửi subsidiary? | **b** – "The price file has 3 SKUs without a price. Could you please add them?" | Nêu việc cụ thể, lịch sự; tránh quy lỗi, viết hoa, gọi mục tiêu nội bộ là "SLA" |
| 12 | Merch cần ImpEx của Tech: cách đúng? | **b** – tạo COEC mới, liên kết, Merch sang ON HOLD COE và comment | |
| 13 | COEC P3 đã gửi PC: có nhắn Oliver không? | **b** – không, chỉ nhắn khi P0/P1 cần sửa ngay | |
| 14 | Đăng Mẫu 1 xong nhưng ticket vẫn ở APPROVED-ES: initial response? | **b** – chưa ghi nhận vì chưa chuyển STG SETUP | |

| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 15 | 02:00 CN, subsidiary gọi hotline báo checkout NZ lỗi; bạn là Shift Leader: các bước liên lạc 20 phút đầu | Phút 0: mở/tạo COEC, xác nhận ảnh hưởng (P0), gọi Tech on-call lớp 1 ngay (on-call chuyển ASSIGNED khi nhận). Phút 10 lớp 1 chưa nghe → gọi lớp 2. Phút 15 → Tech Lead. Phút 20 → SDM hotline. Mở/vào bridge; làm IM tạm thời đến khi on-call có mặt; thông báo RHQ trong 30' (Critical). Cần sửa khẩn production: PC, on-call nhắn Oliver. Mọi cuộc gọi ghi on-call log |
| 16 | RHQ nhắn Mattermost: "Can you quickly change the banner? No need for a ticket." | Không làm ngoài ticket. Trả lời trong thread: "Thanks, I have logged this as DEMO-xxxx so we can track it and keep the evidence. We will reply in the ticket." Tạo ticket trong 5 phút, ghi giờ liên hệ đầu. Việc setup cho subsidiary thì đề nghị subsidiary tạo ticket Shop Merch |
| 17 | Requester bực tức viết hoa toàn bộ, đòi gặp "manager" | Không tranh cãi, không viết hoa lại. Thừa nhận ảnh hưởng, xin lỗi về sự bất tiện, nêu sự thật và kế hoạch có giờ. Báo Sub-Lead ngay; Sub-Lead/Lead trả lời trên ticket. Nếu có khiếu nại bằng văn bản: COE Lead trả lời trong 1 ngày làm việc |
| 18 | TH Market Owner và TM tiếng Thái cùng nghỉ ốm T4; ticket tiếng Thái đến 10:00 | Người nói tiếng Thái còn lại là bench tiếng Thái: Shift Leader chuyển bench sang ca ngày. Bench cũng vắng: trả lời bằng tiếng Anh, COE Lead báo subsidiary TH trước (thường từ đầu ca); Shift Leader ghi handoff. Vắng dài ngày: lấy người từ language pool |
| 19 | Đã hỏi subsidiary bằng Mẫu 2 và chuyển ON HOLD SUBS nhưng quên đổi Assignee; 2h sau subsidiary comment trả lời | Ticket nằm ở ON HOLD SUBS với Assignee là người CoE → dashboard "ON HOLD SUBS có Assignee CoE" bắt được. Đồng hồ đang dừng sai thực tế. Phải chuyển ngay về STG SETUP, đăng Mẫu 12, làm tiếp, tính lại hạn như thể 2h đó đã tính SLA. Lần sau: comment, ON HOLD SUBS và giao requester cùng lúc |
| 20 | Ba ngày sau khi Tech chạy một ImpEx trên production (PC ticket đã được duyệt), RHQ gửi email yêu cầu giải trình vì script thiếu dòng header số PC ticket. Điều gì xảy ra tiếp và CoE làm gì? | Thiếu dòng header là một trong ba việc **chắc chắn dẫn tới strike**. Lead giải trình bằng RCA trung thực (English Coach rà trước khi gửi), nêu đúng sự việc và nguyên nhân hệ thống nếu có (vd checklist trước khi chạy chưa được dùng). **RHQ là bên quyết định ai bị strike**; người chạy script có thể nhận strike thứ nhất. Sub-Lead đưa người đó vào bậc kèm cặp L1 của people-risk ladder (làm cặp, chứng nhận lại service liên quan); Tech Lead bổ sung bước "người thứ hai kiểm dòng header" vào runbook. Ba strike trong một năm dương lịch là bị loại vĩnh viễn nên BiPlus chủ động thay người trước strike thứ ba |

---

## CM-09 Công cụ Samsung – Jira, Confluence, Mattermost, email

### A. Bài tập thực hành (Academy Day 4, trước bài T4)
| # | Đề | Đáp án mẫu |
|---|---|---|
| A.1 | Tạo 2 filter cá nhân: (a) `my-sg-golive-7d` – ticket Shop Merch Singapore có Target Start Date trong 7 ngày tới, chưa đóng, sắp theo Target Start Date; (b) `my-high-mine` – ticket bạn giữ, priority High (hoặc P0/P1 ở Tech), đang chạy SLA, dùng lại filter nền COE-F00R | JQL (a): `filter = "COE-F00 Merchandising scope" AND project = SPHME AND "Target Start Date" >= now() AND "Target Start Date" <= 7d AND status not in ("CLOSED","INVALID","NOT APPROVED") ORDER BY "Target Start Date" ASC`; (b): `filter = "COE-F00R SLA running" AND assignee = currentUser() AND priority in (High,P0,P1) ORDER BY created ASC`. Các bước: Filters → Advanced issue search (JQL) → Search → Save as tên `my-`; không chia sẻ. Đạt khi chạy không lỗi, đúng tên, không chia sẻ, không lặp danh sách trạng thái |
| A.2 | Viết comment tiếng Anh đủ 4 phần cho DEMO-5521 (TH, special price 12 SKU, go-live 10/11 00:00 giờ Bangkok; đã đối chiếu brief đã duyệt và ghi tóm tắt giá trị chính lên ticket trước khi build; đã setup trên production, price sanity đạt, chuyển QA REVIEW, QA kiểm trước 17:00 giờ VN), giờ cập nhật kế tiếp theo SGT | Status (đã setup xong trên production, hiệu lực 10 Nov 00:00 Bangkok, internal check khớp brief đã duyệt, sanity đạt, đã gửi QA) – Evidence (ảnh từng bước PowerPoint + setup summary đính kèm) – Next step (QA verification, Shift Leader approval và Knox approval theo approval path trong brief, rồi requester review) – Next update: by 18:00 SGT today (17:00 Bangkok). Lưu ý 17:00 VN = 18:00 SGT; Bangkok cùng giờ VN |
| A.3 | Ba tin nhắn từ kênh khác: (1) RHQ Mattermost 19:05 "MY asks to hide SKU XYZ-001 tonight, out of stock. Is there a ticket?"; (2) requester VN nhắn riêng 19:20 nhờ sửa banner, file gửi qua Zalo; (3) RHQ 19:40 "URGENT: AU customers see 90% discount on a TV in cart!" | (1) Tìm ticket Shop Merch của MY; có ở APPROVED-ES thì nhận ngay (STG SETUP, Assignee), Low, R1; chưa có thì trả lời RHQ trong thread đề nghị subsidiary tạo ticket (ticket chỉ vào hàng đợi CoE khi đã duyệt). (2) Không nhận file qua Zalo, không làm qua tin nhắn riêng: đề nghị requester tạo ticket Shop Merch và đính file; có ticket rồi thì ghi tóm tắt tin nhắn vào comment. (3) Khả năng sự cố sai giá, High: báo Shift Leader ngay; Shift Leader làm IM tạm thời (CM-06): phút 0–30 tắt/rollback promotion, báo RHQ + subsidiary trong 30'; ghi Jira ngay (comment ở ticket promotion gốc nếu có + ticket sự cố, liên kết nhau); trả lời RHQ trong thread bằng mã ticket |

### B. Câu hỏi kiểm tra (22 câu)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Địa chỉ đăng nhập đúng quy ước của Phạm Văn An, tên Anh Alex? (a an.pv@coe.biplus.com.vn; b alex.pham@coe.biplus.com.vn; c alex.pham@biplus.com.vn; d Gmail) | **b** – `alex.pham@coe.biplus.com.vn` | Tên tiếng Anh + họ thật, viết thường, không dấu, **miền riêng coe.biplus.com.vn** của dự án (mục 1.3); không dùng @biplus.com.vn thông thường |
| 2 | Ai tạo ticket phê duyệt xin quyền và ticket offboarding khi có người nghỉ, và ticket offboarding tạo khi nào? | **a** – Lead của team tạo thay thành viên, đúng **ngày làm việc cuối** | Lead tạo ticket theo template RHQ; Atlassian Platform Engineer chuẩn bị mẫu, theo dõi và ghi provisioning log; tài khoản còn mở sau ngày làm việc cuối là lỗi tuân thủ (mục 1.4, 1.7) |
| 3 | Người chưa đạt T1: điều nào đúng? | **b** – chưa được cấp truy cập nào | |
| 4 | Mất điện thoại có MFA lúc 20:00: làm gì, báo ai, trong bao lâu? | (mẫu) | Không cố đăng nhập cách khác; báo Atlassian Platform Engineer và DevSecOps Engineer trong 1 giờ; đang trong ca thì báo Shift Leader giao lại ticket (mục 1.5, 1.7) |
| 5 | 21:40 RHQ nhắn Mattermost báo khách SG không áp được coupon khi checkout: ghi Jira trong bao lâu, bằng ticket nào, trả lời RHQ ở đâu? | (mẫu) | Trong 5 phút; việc kỹ thuật tạo ticket COEC (mặc định NEW); trả lời trong thread bằng mã ticket, sau đó trao đổi trên ticket (mục 2.1, 5.3) |
| 6 | Filter không owner chạy bao lâu một lần, ai chạy trong ca Merch? | **b** – mỗi 30 phút, Shift Leader | Mục 3.3.3 |
| 7 | Medium vào STG SETUP 08:00, ON HOLD SUBS 10:00, về STG SETUP 13:00. Mấy giờ chạm tầng 70%, ai hành động? | **22:12** – Shift Leader rà soát, hành động trong 15' | 16h×70% = 672' (11h12'). Đã dùng 2h (08–10), dừng 3h, từ 13:00 còn 9h12' tới 70% → 22:12. Filter thay thế tính cả thời gian dừng nên báo sớm hơn; kiểm lại trên plug-in (mục 3.3.5) |
| 8 | High vào STG SETUP 10:00, luôn ở trạng thái tính SLA: mấy giờ chạm 85%, ai hành động, trong bao lâu? | **13:24** – Lead của team (on-call ngoài giờ) nhận hoặc giao lại, workaround, leo thang có evidence pack hoặc cập nhật requester, trong 30 phút | 4h×85% = 204' |
| 9 | COEC P1 đã sang SYSTEM SUPPORT: đồng hồ? Theo dõi bao lâu, ghi đâu, ai giữ ownership? | Đồng hồ **dừng**; nhóm High theo dõi 2 ngày làm việc/lần (filter COE-F11 dùng 2 ngày lịch); mỗi lần một comment Jira + cập nhật Escalation Log; **CoE giữ ownership** | |
| 10 | Vì sao filter CoE không dùng `statusCategory != Done` để lấy ticket còn mở? | (mẫu) | Status category không khớp nhóm SLA: ON HOLD SUBS có thể thuộc In Progress dù đồng hồ dừng; LAUNCH VERIFICATION có thể thuộc Done dù go-live chưa xong. CoE dùng danh sách trạng thái cụ thể trong filter nền (mục 2.5.4, 3.2) |
| 11 | ON HOLD COE nghĩa là? | **b** – cần thống nhất nội bộ hoặc chờ Tech, đồng hồ vẫn chạy | |
| 12 | Việc có QA gate; đồng nghiệp muốn chuyển thẳng STG SETUP → PRD SETUP vì "QA đang bận" | (mẫu) | Không được: phải qua QA REVIEW, có QA PASS, Shift Leader duyệt rồi mới PRD SETUP; QA bận thì báo QA dispatcher và Shift Leader. Ngoại lệ duy nhất: last-minute request có comment theo mẫu; khi đó vẫn kiểm tra nội bộ, price sanity, Shift Leader duyệt, người thứ hai kiểm trên production lúc go-live |
| 13 | Requester bấm gọi thoại trên Mattermost | (mẫu) | Không nhận; nhắn đề nghị viết lên ticket, khẩn thì gọi hotline; nếu nói qua hotline thì ghi tóm tắt lên ticket |
| 14 | Tên trang handoff note ca tối Merch 03/11/2026? | **b** – `HO-2026-11-03-E-MER` | Mục 4.4 |
| 15 | Đúng/sai: "STG SETUP nghĩa là thiết lập trên staging, chưa chạm production." | **Sai** | STG SETUP là bước workflow: CoE đã nhận và đang setup trên production; promotion test bằng promotion simulator rồi publish live đúng giờ (mục 2.5.1, 7.2) |
| 16 | BVT Notification đến lúc 21:00: ai ghi nhận, làm gì? QA có tham gia không? | Shift Leader ghi handoff note và nhắn Merch Lead + Tech Lead trên kênh nội bộ để chỉ định PIC BVT trong ngày làm việc kế tiếp. **QA không tham gia BVT** | Mục 6.1 |
| 17 | ON HOLD SUBS; subsidiary đã trả lời bằng comment nhưng không chuyển trạng thái, Assignee vẫn là bạn. Filter nào bắt, làm gì? | **COE-F02** (ON HOLD SUBS có Assignee CoE). Đồng hồ đang dừng sai thực tế → chuyển ngay về STG SETUP và làm tiếp | Mục 3.3.2 |
| 18 | Subsidiary cần 500.000 mã coupon (giả lập), giao diện không làm được, cần ImpEx của Tech: làm gì trên Jira, SLA hai ticket? | Không chuyển ticket Merch sang COEC. Tạo COEC mới ghi rõ cần ImpEx gì, issue link, Merch ON HOLD COE + comment mẫu. COEC chạy SLA Tech; Merch vẫn chạy SLA Merch; người tạo COEC đôn đốc Tech | Mục 2.6.1 |
| 19 | Ticket đã INVALID nay subsidiary muốn làm lại đúng yêu cầu đó | INVALID không mở lại được: clone ticket, ticket mới đi lại từ đầu workflow; kiểm lại Target Start Date, priority, file đính kèm; liên kết với ticket cũ | Mục 2.6.3 |
| 20 | Tech xóa user group qua Back Office (5 giây): cần gì, COEC ở trạng thái nào khi chờ, khi nào nhắn người duyệt? | PC được Oliver Leung (RHQ) duyệt, kèm kết quả staging nếu cần; COEC gốc ở ON HOLD HQ "PC ticket pending"; chỉ nhắn Oliver qua Mattermost khi P0/P1 cần sửa ngay | Oliver là người duyệt duy nhất, chờ ~3 giờ kể cả khi Oliver vắng nên tạo PC sớm (mục 2.6.4) |
| 21 | Promotion đã publish: subsidiary đổi tên promotion, sau đó đổi cả ngày kết thúc. Trường hợp nào phải gửi Knox approval lại, CoE chọn approval path thế nào? | (mẫu) | Đổi ngày (action, condition, website hoặc ngày) thì phải gửi lại; đổi tên thì không. CoE làm đúng cột approval path trong campaign brief, không tự chọn; yêu cầu gấp vẫn gửi Knox (mục 2.6.5) |
| 22 | Subsidiary nhờ Tech danh sách email khách hàng của một campaign để gửi EDM, và một báo cáo bán hàng từ 1/1 đến nay. Xử lý từng việc? | (mẫu) | Email khách để gửi EDM: **mặc định từ chối**, báo Shift Leader. Báo cáo bán hàng: subsidiary tạo **PUMI**, duyệt xong đính vào Jira, rồi Tech tạo PC ticket cho Oliver duyệt; không gửi PII qua email từ Hybris (mục 7.5) |

---

## CM-10 An toàn thông tin trong công việc hằng ngày (bài T1)

Ngưỡng đạt T1: đúng ≥18/20 (90%) **và** đúng mọi câu trọng yếu (8 câu đánh dấu ★). Không đạt T1 thì chưa được cấp truy cập hệ thống Samsung.

### A. Bài T1 – 20 câu trắc nghiệm
| # | Câu hỏi (lựa chọn) | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 ★ | Dữ liệu Samsung được lưu ở đâu? (A Google Drive BiPlus có mật khẩu; B máy cá nhân nếu xóa trong ngày; C chỉ hệ thống Samsung; D USB mã hóa) | **C** | Dữ liệu Samsung chỉ nằm trên hệ thống Samsung (quy tắc 2) |
| 2 | Thông tin nào là mật của Samsung? (A brief promotion chưa live; B giá/SKU trong file giá; C ticket, comment Jira Samsung; D tất cả) | **D** | Mọi thông tin liên quan Samsung là thông tin mật (mục 1.1) |
| 3 ★ | Được dán nội dung ticket vào công cụ AI nào? | **C** – không công cụ nào, kể cả công cụ được duyệt | RFP 3.12: không đưa thông tin mật, dữ liệu cá nhân vào bất kỳ AI nào (quy tắc 5) |
| 4 ★ | On-call được gọi lúc 01:00, đọc ticket Jira ở đâu? | **C** – chỉ tại trung tâm, trên máy trạm CoE | Không làm remote, kể cả on-call (quy tắc 1) |
| 5 | Rời bàn đi pantry 3 phút, bạn làm gì? | **B** – khóa màn hình (Windows + L) | Quy tắc 4 |
| 6 ★ | Đồng nghiệp quên mật khẩu, mượn tài khoản của bạn cho kịp SLA | **C** – từ chối; Shift Leader giao lại ticket | Tài khoản đích danh, không cho mượn (quy tắc 4) |
| 7 | Kênh trao đổi nội dung ticket với subsidiary hiện nay? | **B – comment trên Jira** | Kênh nhắn tin với subsidiary RHQ chưa chốt (quy tắc 6) |
| 8 ★ | Lỡ bấm link trong email giả danh RHQ, chưa nhập mật khẩu | **B** – báo ngay Shift Leader và DevSecOps, mẫu báo trong 1 giờ | Bấm link lạ là sự cố phải báo (quy tắc 10) |
| 9 | Điện thoại cá nhân ở tầng 6 hiện tại? | **B** – được mang, cấm chụp/quay, cấm dùng với dữ liệu Samsung | Quyết định 21/10/2026; gửi tủ khi chuẩn bị flagship |
| 10 ★ | Cách đúng để báo ca sau một lỗi trên Hybris? | **B** – mô tả + mã ticket trong Jira, handoff note | Không chụp, không kênh cá nhân (quy tắc 3, 6) |
| 11 | Bằng chứng QA (PowerPoint chụp màn hình từng bước) phải làm thế nào? | **B** – tạo trên máy trạm CoE, đính thẳng Jira, xóa bản trên máy sau khi đính | Bốn điều: máy trạm CoE, đính Jira, xóa trên máy, không chụp bằng điện thoại / không gửi kênh khác |
| 12 | Mô tả lỗi giao hàng của khách trên ticket, ghi gì? | **B – mã đơn hàng** | Không chép dữ liệu cá nhân, kể cả trong ảnh (quy tắc 7) |
| 13 ★ | Sự cố an toàn thông tin phải báo văn bản trong bao lâu? | **B** – trong 1 giờ từ khi phát hiện (báo bằng lời ngay) | Chương 3 |
| 14 | Ngoài giờ, không liên lạc được DevSecOps Engineer, báo ai? | **B – SDM hotline 24/7** | Không tự báo RHQ (mục 3.2) |
| 15 | Người mặc áo giao hàng đi sát sau bạn ở cửa tầng 6 | **B** – không cho đi theo, mời liên hệ lễ tân/SDM | Chống tailgating; khách phải có danh sách và người dẫn (quy tắc 9) |
| 16 ★ | Chuẩn bị flagship, dùng AI với thông tin sản phẩm mới thế nào? | **C** – không dùng AI với sản phẩm embargo | RFP 3.12, kể cả công cụ được duyệt (quy tắc 5) |
| 17 | Câu trả lời soạn bằng AI được duyệt, trước khi gửi phải? | **B** – người có chứng nhận rà soát, chịu trách nhiệm | RFP 3.12 |
| 18 | Bạn bè hỏi về promotion Black Friday sắp tới | **C** – không tiết lộ | Thông tin chưa công bố là mật (quy tắc 8) |
| 19 | Khi rời dự án? | **B** – bàn giao, trả thiết bị; **Lead tạo ticket offboarding đúng ngày làm việc cuối** để khóa tài khoản | Nghĩa vụ bảo mật còn hiệu lực (quy tắc 4, 8, mục 1.5) |
| 20 | RHQ có quyền gì về an ninh tại trung tâm? | **B** – audit, báo trước tối thiểu 3 ngày làm việc | RFP 3.8 |

### B. 29 tình huống Đúng/Sai (chương 2)
| # | Tình huống | Đ/S | Vì sao |
|---|---|---|---|
| 1 | Chụp màn hình Hybris bằng điện thoại để hỏi đồng nghiệp ca sau | **Sai** | Ghi mô tả + mã ticket vào Jira/handoff (quy tắc 3) |
| 2 | Làm PowerPoint bằng chứng QA trên máy trạm CoE, đính thẳng Jira, xóa file/ảnh trên máy | **Đúng** | Đúng bốn điều của hộp quy tắc |
| 3 | Subsidiary gửi file giá vào Gmail cá nhân; bạn tải về máy trạm "cho nhanh" | **Sai** | Kênh cá nhân bị cấm; đề nghị đính vào ticket; báo Shift Leader + DevSecOps |
| 4 | Gửi subsidiary link trang Confluence Samsung có danh sách đơn qua comment Jira | **Đúng** | Dữ liệu vẫn ở hệ thống Samsung, kênh chính thức |
| 5 | Dán brief promotion (không tên khách) vào công cụ dịch AI miễn phí | **Sai** | Brief là thông tin mật |
| 6 | Nhờ AI (kể cả được duyệt) viết mô tả sản phẩm sắp ra mắt khi chuẩn bị flagship | **Sai** | Cấm AI với sản phẩm embargo |
| 7 | Mang laptop CoE về nhà để on-call cho nhanh | **Sai** | Không remote, không mang laptop khỏi tầng 6 |
| 8 | Cắm USB cá nhân vào máy trạm chép slide đào tạo | **Sai** | USB bị chặn; xem tài liệu trên Confluence |
| 9 | Ra sảnh nghe điện thoại gia đình, không chụp, không mở dữ liệu Samsung | **Đúng** | Được mang điện thoại vào tầng 6, cấm chụp/quay |
| 10 | Selfie tại bàn có Jira phía sau, đăng Facebook "ngày đầu làm cho Samsung" | **Sai** | Chụp trong tầng 6 và đăng về công việc Samsung |
| 11 | In checklist QA có giá và SKU để tick bằng bút | **Sai** | Không in dữ liệu Samsung; dùng checklist trên Confluence |
| 12 | Đồng nghiệp quên mật khẩu nhờ đăng nhập tài khoản bạn | **Sai** | Tài khoản đích danh; Shift Leader giao lại ticket |
| 13 | Email "RHQ IT Security" từ địa chỉ lạ yêu cầu bấm link; bạn không bấm, báo ngay DevSecOps | **Đúng** | Phishing; báo trong 1 giờ |
| 14 | Lỡ bấm link lạ nhưng chưa nhập mật khẩu nên không báo | **Sai** | Bấm link đã có thể cài mã độc; vẫn phải báo |
| 15 | Ở quán cà phê kể mức giảm Black Friday sắp tới | **Sai** | Promotion chưa công bố là mật |
| 16 | Cập nhật LinkedIn: "Phụ trách giá và promotion cho Samsung VN, TH" | **Sai** | Không đăng chi tiết công việc Samsung; hỏi DevSecOps nếu cần |
| 17 | Giữ cửa tầng 6 cho người mặc áo giao hàng đi sát sau | **Sai** | Tailgating |
| 18 | Gửi nhầm email danh sách đơn cho người ngoài Samsung, đã thu hồi nên không báo | **Sai** | Gửi nhầm là sự cố dù đã thu hồi; báo trong 1 giờ |
| 19 | Chép tên và số điện thoại khách vào comment Jira để mô tả lỗi | **Sai** | Dùng mã đơn |
| 20 | Thấy đồng nghiệp chụp màn hình bằng điện thoại; bạn nhắc và báo Sub-Lead | **Đúng** | Thấy vi phạm thì báo |
| 21 | Gửi file PowerPoint bằng chứng QA cho người subsidiary qua Mattermost và giữ một bản trên máy | **Sai** | Bằng chứng chỉ đính Jira; không gửi kênh khác; xóa bản trên máy |
| 22 | Ngày UAT Clean Room, khách subsidiary nhờ đăng nhập Hybris bằng tài khoản bạn | **Sai** | Tài khoản đích danh; ghi yêu cầu vào Jira |
| 23 | Ngày UAT, khách đi theo bạn sang khu làm việc bảo mật "để xem đội làm việc" | **Sai** | Khách chỉ ở khu bố trí cho khách, có người dẫn |
| 24 | Subsidiary Úc xin danh sách email khách đã mua một sản phẩm để gửi EDM; bạn gửi vì "họ là chủ campaign" | **Sai** | Xin email khách để gửi EDM: **mặc định từ chối**; trả lời bằng comment trên ticket và báo Shift Leader/Lead (quy tắc 7) |
| 25 | Tech TM chạy query xem đơn hàng của một khách "cho biết", ticket không yêu cầu | **Sai** | Không truy vấn production khi không có lý do; lý do ghi trên ticket (quy tắc 7) |
| 26 | Gửi file báo cáo có tên và số điện thoại khách bằng email từ Hybris | **Sai** | Không bao giờ gửi PII qua email từ Hybris; là sự cố ATTT, báo trong 1 giờ (quy tắc 7, 10) |
| 27 | Lead tổ chức buổi đào tạo nội bộ, bật ghi hình bằng công cụ họp khi Samsung đã đồng ý; buổi chỉ dùng slide và ví dụ giả lập | **Đúng** | Ghi hình đào tạo nội bộ được phép tạm thời, không có dữ liệu Samsung trong buổi ghi (quy tắc 3, ngoại lệ thứ hai) |
| 28 | Đồng nghiệp nghỉ việc hôm nay; hai tuần sau Lead mới tạo ticket khóa tài khoản | **Sai** | Ticket offboarding phải tạo đúng ngày làm việc cuối; tài khoản còn mở sau đó là lỗi tuân thủ (quy tắc 4, mục 1.5) |
| 29 | Đăng ký tài khoản Jira bằng địa chỉ alex.tran@biplus.com.vn vì quen dùng | **Sai** | Dùng email dự án thuộc miền coe.biplus.com.vn, không dùng @biplus.com.vn thông thường (quy tắc 6) |

> Mẹo "dừng 5 giây": thông tin này có phải của Samsung/khách? nơi gửi/lưu có phải hệ thống/kênh được phép? người nhận có cần biết, đúng địa chỉ? có đang dùng AI/điện thoại/USB/máy in/kênh cá nhân? ảnh/file bằng chứng đã đính Jira và xóa khỏi máy? ngày mai RHQ audit thao tác này có giải thích được không?

---

## CM-11 Academy – chương trình, bài kiểm tra, thuật ngữ

Academy có 8 bài test (T1–T8). T3 (Foundation quiz) lấy 30 câu từ ngân hàng **68 câu** dưới đây (10 câu phần chung chọn từ câu 1–10, 46–53 và các câu quy tắc RHQ 54–68, ≥3 câu workflow Jira hoặc quy tắc RHQ; 20 câu theo track), 45 phút, không mở tài liệu, **đạt ≥24/30 (80%)**. T1 xem mục CM-10.

### A. T3 – ngân hàng 68 câu

**Phần chung: SLA và Service Management (câu 1–10)**
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Yêu cầu "tải giá mới cho 20 SKU, hiệu lực từ thứ Hai" thuộc loại việc nào? | **B – Service Request** | |
| 2 | Website một thị trường không đặt hàng được từ 10 phút trước là? | **C – Incident** | |
| 3 | Cùng lỗi hiển thị giá lặp lại 4 lần trong tháng ở nhiều ticket: CoE nên? | **A** – mở Problem record tìm nguyên nhân gốc | Lỗi lặp ≥3 lần/tháng là trigger problem |
| 4 | Initial Response theo RFP là bao lâu, đạt bao nhiêu? | **D – 2 giờ, 97%** | 78 phút/98,5% là mục tiêu nội bộ |
| 5 | Trong Composite SLA, Resolution chiếm? | **C – 75%** | |
| 6 | Ticket Shop Merch ở STG SETUP; TM ghi câu hỏi, chuyển ON HOLD SUBS và giao ticket cho subsidiary. Đồng hồ? | **B – dừng** | Đồng hồ chỉ chạy khi việc ở phía CoE; chuyển về STG SETUP thì chạy lại (CM-03 ch.2) |
| 7 | Medium (16h) đã dùng 11h12 (70%): ai rà soát, trong bao lâu? | **D – Shift Leader, 15 phút** | |
| 8 | Ở 95%, ai báo RHQ trước khi vỡ SLA? | **B – COE Lead** | |
| 9 | Composite quý 94,4%: khấu trừ? | **C – 2%** | Dải: 95,0–96,9% trừ 1%; 94% trừ 2%; 93% trừ 3%; 92,0–92,9% trừ 4%; <92% trừ 5% |
| 10 | Yêu cầu nhận qua Mattermost phải vào Jira trong? | **A – 5 phút** | |

**Merchandising (câu 11–25)**
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 11 | Ticket 1 promotion, không có yếu tố bảo mật/thiệt hại lớn: priority? | **B – Medium** | |
| 12 | Ticket 4 promotion: priority theo RFP? | **D – Low** | >2 promotion = Low 24h; 1 promotion = Medium 16h |
| 13 | Lỗi giá đang live có thể mất ~15.000 USD: priority? | **A – High (4 giờ)** | |
| 14 | Thay banner trên AEM thuộc cấp rủi ro? | **C – R1** | |
| 15 | Thiết lập stock thuộc cấp? | **B – R2** | Stock là R2; giá, promotion, coupon là R3 |
| 16 | File giá 650 SKU cho một thị trường: cấp và cổng duyệt? | **D** – R3 đạt E4: kiểm tra nội bộ, price sanity rules, QA, Shift Leader duyệt, Merch Lead (hoặc Deputy) duyệt thêm | ≥500 SKU là E4 |
| 17 | Sau khi promotion R3 go-live, việc bắt buộc trong 30 phút? | **A** – người thứ hai kiểm storefront và test order | |
| 18 | Với thay đổi R3, Doer phải làm gì trước khi build? (A hỏi lại subsidiary từng giá trị; B chỉ ghi priority; C đối chiếu cấu hình với brief đã duyệt và ghi tóm tắt giá trị chính lên ticket; D chờ QA xong rồi mới đối chiếu) | **C** – **kiểm tra nội bộ** (internal check): ghi tóm tắt SKU, giá/mức giảm, thời gian kèm múi giờ, site/store, quy tắc stack, giới hạn dùng | Thay cho read-back với requester ở v0.2; chỉ hỏi subsidiary khi brief thiếu/mâu thuẫn (CM-13 chương 7) |
| 19 | Bulk upload 180 dòng phải có? | **B** – file diff và dry run trên staging/preview trước | >100 dòng cần file diff |
| 20 | Promotion áp dụng tuần sau được thiết lập thế nào? | **D** – thiết lập trên production, publish sang simulator, test bằng promotion simulator Back Office 2.0, đến giờ go-live thì publish live | STG SETUP chỉ là tên trạng thái |
| 21 | Ai là Checker của ticket R3? | **A – QA** | |
| 22 | Ticket nội dung tiếng Thái đến T7 14:00. Ai xử lý? | **C** – người nói tiếng Thái của ca ngày T7 (TM hoặc bench Thái) | |
| 23 | Ticket Bahasa đến T7. CoE trả lời bằng? | **B – tiếng Anh** | Không dùng AI dịch |
| 24 | Z-Code là? | **D** – sản phẩm "ghost" làm quà tặng, chỉ đi kèm sản phẩm chính, không mua riêng được | |
| 25 | Brief thiếu giờ kết thúc và danh sách SKU loại trừ: cách đúng? | **A** – một câu hỏi đầy đủ cả hai điểm trong comment (ask once, completely), ON HOLD SUBS, giao ticket subsidiary | |

**Tech (câu 26–35)**
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 26 | Khách không truy cập được website một thị trường: priority Tech? | **C – P0** | |
| 27 | Resolution time Tech P1? | **B – 8 giờ** | |
| 28 | COEC P2 ở SYSTEM SUPPORT: CoE theo dõi bao lâu một lần? | **D** – 2 ngày làm việc/lần, mỗi lần một comment Jira | P0–P2 cùng nhóm High về nhịp theo dõi, dù đồng hồ dừng |
| 29 | Ticket đã chuyển Samsung L2/L3: owner là? | **A – CoE** | CoE giữ ownership |
| 30 | 21:30 T3 (ngoài khung Tech) COEC P1 mới ở NEW. Ai chịu trách nhiệm quét và nhận ticket? | **C** – Tech on-call lớp 1 quét COEC NEW mỗi 5 phút và chuyển ASSIGNED; Shift Leader có mặt tại trung tâm và gọi on-call khi thấy P0/P1 | Ticket của Tech Team do Tech Team chịu trách nhiệm, Shift Leader không nhận ticket Tech (TC-04) |
| 31 | On-call nhận cuộc gọi P0 lúc 01:00: yêu cầu? | **B** – trả lời trong 15 phút, có mặt tại trung tâm trong 60 phút | |
| 32 | Filter Open High gửi email cho on-call lớp 1 bao lâu một lần? | **D – 15 phút** | |
| 33 | Việc nào thuộc Tech Level 1? | **A** – làm theo runbook: kiểm tra đơn hằng ngày, giải phóng đơn kẹt, EPP access | |
| 34 | Evidence pack kèm Maintenance Request tối thiểu gồm? | **C** – mô tả, bước tái hiện, bằng chứng trên hệ thống Samsung, ảnh hưởng, việc đã thử | |
| 35 | Tech xóa user group khỏi nhiều tài khoản bằng ImpEx mới (vài giây): điều kiện bắt buộc? | **B** – kết quả chạy thử staging, đã tự QA và có người kiểm thứ hai, PC được Oliver Leung duyệt, ImpEx có dòng số PC + COEC gốc | Không PC được duyệt thì không thay đổi production, kể cả việc 5 giây; thiếu dòng số ticket là chắc chắn bị strike |

**QA (câu 36–45)**
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 36 | QA phát hiện promotion sai điều kiện trước go-live. QA làm gì? | **D** – trả ticket về kèm lý do và evidence | |
| 37 | Ai override quyết định trả về của QA? | **A – chỉ COE Lead** | |
| 38 | Dispatcher QA giao việc kiểm trong bao lâu? | **C – 15 phút** | |
| 39 | QA Lead kiểm lại bao nhiêu % kết quả PASS mỗi tuần? | **B – 5%** | |
| 40 | Escaped defect là? | **D** – lỗi lọt qua QA, phát hiện sau khi đã live | |
| 41 | QA Team kiểm việc nào? | **B** – công việc hằng ngày của Merch (R3 và R2 có QA gate); không BVT, không QA cho Tech | |
| 42 | Ticket đến QA REVIEW thiếu dữ liệu để QA. QA làm gì? | **D** – trả về Merch, gặp trực tiếp người làm để bổ sung | Không đoán, không nhắn kênh cá nhân |
| 43 | Ticket 2 đợt go-live (01/12, 08/12), QA PASS trên simulator: mỗi đợt làm gì? | **C** – QA lại trên production thật; xong đợt 1 trả ticket về PENDING LAUNCH chờ đợt 2 | Setup trước chỉ là môi trường giả lập trên production |
| 44 | TM bị QA trả về 2 lần trong tháng: điều gì xảy ra? | **D** – mức L1 people-risk ladder: kèm cặp, giảm WIP một nửa, chứng nhận lại trong 5 ngày làm việc | |
| 45 | Bằng chứng QA (ảnh từng bước) được tạo/lưu thế nào? | **A** – tạo trên máy trạm CoE trong khu bảo mật, đính thẳng Jira, xóa bản trên máy | |

**Workflow Jira và phối hợp (câu 46–53)**
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 46 | Initial response ticket Shop Merch được đo thế nào? | **B** – từ APPROVED-ES đến khi CoE chuyển STG SETUP | |
| 47 | Initial response ticket COEC đo thế nào? | **A** – từ NEW đến ASSIGNED | |
| 48 | 500.000 mã coupon (giả lập), ticket Merch, cần ImpEx của Tech: cách đúng? | **C** – tạo COEC mới, issue link, ticket Merch sang ON HOLD COE và comment | Không move khi Merch còn phải làm tiếp |
| 49 | Ticket Merch ở ON HOLD COE chờ Tech 5 ngày: đồng hồ? | **B** – vẫn chạy, Merch trễ theo Tech | |
| 50 | Promotion go-live 00:00 mai; 23:59 hôm nay subsidiary chưa duyệt ở REVIEW SETUP. CoE làm gì? | **A** – publish như đã thống nhất và comment đã publish, chưa nhận phản hồi | Quy tắc RHQ: không chờ subsidiary đọc hết bằng chứng |
| 51 | Ticket giảm giá R3 tạo 18:00 cần live 00:00 cùng ngày, không đủ thời gian QA | **C** – vẫn kiểm tra nội bộ, price sanity, Shift Leader duyệt và **gửi Knox approval**; comment "Last minute request, please QA on your own when it goes live. If any issue, please contact us."; gắn label đếm cho họp tuần; người thứ hai kiểm production lúc go-live và đứng chờ hỗ trợ | CM-13 chương 8 |
| 52 | Subsidiary trả lời bằng comment nhưng không chuyển trạng thái; ON HOLD SUBS và Assignee là người CoE | **D** – chuyển ngay về STG SETUP và làm tiếp | Dashboard bắt loại này; đồng hồ đang dừng sai thực tế |
| 53 | Ticket đã INVALID, nay subsidiary muốn làm lại | **C – clone ticket** | INVALID không mở lại được |

**Quy tắc RHQ theo CM-13 (câu 54–68, mới ở v0.3)** – Merch chọn 54–56, 61, 62, 65, 66; Tech 57–68; 61, 62, 65 dùng cho mọi track
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 54 | Promotion đã publish. Subsidiary đề nghị (1) đổi tên và (2) kéo dài thêm 2 ngày. Việc nào làm lần publish tiếp theo phải duyệt Knox lại? | **C** – chỉ việc (2) | Đổi action, condition, website hoặc ngày thì duyệt lại; đổi tên thì không (CM-13 ch.10) |
| 55 | Campaign brief có cột approval path do subsidiary ghi. Khi gửi Knox approval bạn làm gì? | **A** – làm đúng cột approval path, không tự chọn | Đường duyệt khác nhau theo subsidiary và product division (MX, CE) |
| 56 | Yêu cầu gấp về giá, QA không kịp. Về Knox approval? | **D** – vẫn setup rồi gửi Knox approval như thường | |
| 57 | Việc nào cần PC ticket? (A Merch setup special price theo workflow; B Tech chạy ImpEx sửa dữ liệu production dù 5 giây; C truy vấn chỉ đọc có lý do; D release code của đội phát triển) | **B** | Merch setup đi workflow + Knox; chỉ đọc có lý do không cần PC; release code không đi PC |
| 58 | Oliver Leung vắng 23/10–9/11. Tech cần một PC ticket không khẩn. Cách đúng? | **D** – PC vẫn chờ Oliver, chậm khoảng 3 giờ; tạo sớm và tính sẵn thời gian chờ | Oliver là người duyệt duy nhất, không người duyệt thay |
| 59 | 02:00, ticket P0, cách sửa nhanh nhất là chạy ImpEx trên production. Cách đúng? | **A** – tạo PC ngắn gọn, nhắn Oliver trên Mattermost ngay, chỉ chạy khi PC được duyệt | Thay đổi khẩn vẫn cần PC |
| 60 | Vừa chạy xong một thay đổi production và thấy sai, cần rollback. Rollback có cần PC không? | **C** – có | Rollback một thay đổi vừa làm cũng là thay đổi production |
| 61 | Việc nào chắc chắn dẫn tới strike? | **D** – chạy ImpEx/Groovy production thiếu dòng header số PC + số COEC gốc | Hai việc còn lại: đổi production khi chưa có PC duyệt; làm service chưa chứng nhận rồi gây sự cố |
| 62 | Ai quyết định một người bị strike, bao nhiêu strike/năm dương lịch thì bị loại vĩnh viễn? | **B** – RHQ (dựa RCA của Lead); 3 strike | BiPlus chủ động thay người trước strike thứ ba |
| 63 | Subsidiary xin danh sách email khách đã mua để gửi EDM. Cách đúng? | **C** – mặc định từ chối; không cung cấp PII để gửi EDM; không bao giờ gửi PII qua email từ Hybris | |
| 64 | Subsidiary cần báo cáo bán hàng từ 1/1 đến nay cho audit. Tech cần gì trước khi lấy dữ liệu production? | **A** – PUMI được duyệt (subsidiary tạo, đính Jira) rồi mới gửi PC ticket | |
| 65 | Ticket Shop Merch tạo nhầm: toàn bộ là việc Tech (thêm domain email vào EPP access list). Cách đúng? | **D** – move chính ticket sang COEC, comment lý do; sau move theo SLA Tech | CoE tự move được, không cần quyền admin |
| 66 | Subsidiary nói "chưa có phê duyệt, cần gấp" cho ticket tạo EPP site mới. Cách đúng? | **B** – trả lại subsidiary xin phê duyệt theo link template RHQ; chỉ khi có email phê duyệt đính Jira mới chuyển chờ RHQ duyệt | Oliver chỉ duyệt khi có email |
| 67 | Tech chạy ImpEx mới chạm giá. Ai là người kiểm thứ hai (another set of eyes)? | **A** – người giữ chứng nhận **L2 hoặc L3** của đúng service | Bắt buộc với script mới hoặc chạm giá, đơn hàng, thanh toán, quyền |
| 68 | CoE làm gì ở 3PD? | **C** – quản 4 middleware giữa Hybris và marketplace; PIC 3PD chuyên trách ở Tech Team, có backup đã chứng nhận | CoE không vận hành trên marketplace |

### B. Câu hỏi kiểm tra Academy (Phụ lục A, 19 câu; đạt ≥ mức theo CM-11)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Mức chứng nhận nào nhận ticket live với 100% đầu ra được kiểm trước production? | **B – L1** | L1 Certified: live có kiểm 100% |
| 2 | T1 đạt khi? | **B** – từ 90% và mọi câu trọng yếu đúng | |
| 3 | T3 gồm bao nhiêu câu và điểm đạt? | **B – 30 câu, 80%** | |
| 4 | Trượt T3 lần hai thì? | **B** – thêm một tuần nền tảng, việc live lùi một sprint | |
| 5 | Ngưỡng first-pass yield của T6 từ tháng 12? | **C – 95%** | 90% trong tháng 11 |
| 6 | Ai thi T7 (RHQ interview)? | **C** – COE Lead, Lead, Sub-Lead và Tech | |
| 7 | T8 giải phóng duyệt tin nhắn khi? | **C** – đủ 4 tuần **và** 50 tin nhắn đạt | Phải đủ cả hai điều kiện |
| 8 | Cohort 1 bắt đầu ngày? | **C – 01/12/2026** | |
| 9 | Ai chấm T4? | **A – Sub-Lead** | |
| 10 | Vì sao track Q không có phần BVT? | **B** – QA chỉ QA việc Merch; BVT do PIC Merch hoặc Tech làm | |
| 11 | Kể bốn loại lỗi trọng yếu trong T4 | (mẫu) | Sai giá/giá trị promotion; sai thị trường/site/store; sai múi giờ; bỏ cổng QA hoặc tự duyệt; **build R3 không ghi kiểm tra nội bộ lên ticket**; **setup giá/promotion thiếu Knox approval hoặc không duyệt lại khi đổi action/condition/website/ngày**; thao tác trên production; đưa dữ liệu ra ngoài hệ thống Samsung; dùng ON HOLD SUBS chỉ để dừng đồng hồ; với Tech: thay đổi khi chưa có PC, ImpEx/Groovy thiếu dòng bắt buộc, hoặc làm service chưa chứng nhận |
| 12 | Đạt L1 coupon creation, Shift Leader giao ticket coupon: làm thế nào? | (mẫu) | Được nhận nhưng mọi đầu ra phải được Sub-Lead/buddy kiểm trước production; ticket vẫn qua QA và Shift Leader duyệt |
| 13 | Đạt L2 price upload nhưng runbook vừa thay đổi: làm gì trước khi nhận ticket tiếp? | (mẫu) | Chứng nhận lại theo runbook mới (Sub-Lead tổ chức) |
| 14 | Muốn chụp màn hình bài replay để ôn ở nhà, được không? | (mẫu) | Không: dữ liệu Samsung, kể cả staging, không chụp/tải/mang ra ngoài (quy tắc vàng 2). Ảnh chỉ tạo trên máy trạm CoE làm bằng chứng, đính thẳng Jira. Ôn bằng runbook trên Confluence tại trung tâm |
| 15 | L1 chứng nhận L0–L3 khác L1 people-risk ladder thế nào? | (mẫu) | L1 chứng nhận = mức năng lực theo service (live có kiểm). L1 people-risk = mức kiểm soát khi có vấn đề hiệu suất (vd 2 lần QA trả về/tháng): kèm cặp, giảm WIP, chứng nhận lại |
| 16 | T4 replay thiếu múi giờ: ngoài câu hỏi cho subsidiary, ghi bước chuyển trạng thái Jira nào vào phiếu, vì sao? | (mẫu) | Ghi câu hỏi vào comment, chuyển ON HOLD SUBS và giao ticket cho subsidiary; có trả lời thì về STG SETUP. Đồng hồ chỉ dừng đúng khi việc thật sự ở phía subsidiary; dùng ON HOLD SUBS không giao ticket là lỗi trọng yếu |
| 17 | Kể ba việc chắc chắn dẫn tới strike và cho biết ai quyết định một người bị strike | (mẫu) | Thiếu dòng header (số PC + số COEC gốc) trong ImpEx/Groovy production; thay đổi production khi chưa có PC duyệt; làm service chưa chứng nhận rồi gây sự cố. **RHQ quyết định**, dựa trên RCA do Lead nộp (mục 1.7) |
| 18 | Bạn là Doer của ticket giảm giá R3. Trước khi build ghi gì lên ticket? Khi nào được hỏi subsidiary? | (mẫu) | Đối chiếu cấu hình với brief đã duyệt, ghi tóm tắt SKU, giá/mức giảm, thời gian kèm múi giờ, site/store, quy tắc stack, giới hạn dùng; chạy price sanity rules. Chỉ hỏi subsidiary khi brief thiếu, mâu thuẫn hoặc sanity bị vi phạm: một câu hỏi gộp, ON HOLD SUBS, giao subsidiary |
| 19 | Tech TM, Oliver đang vắng; cần chạy ImpEx mới gỡ một user group khỏi 1.200 tài khoản (giả lập). Các bước từ nhận ticket COEC đến LAUNCH VERIFICATION? | (mẫu) | Chạy thử staging, chụp dữ liệu trước/sau; tự QA; nhờ người kiểm thứ hai giữ chứng nhận L2 hoặc L3 của service (script mới); tạo PC sớm (thay đổi gì, vì sao, kết quả staging, rollback), liên kết COEC, COEC sang ON HOLD HQ \"PC ticket pending\"; Oliver duyệt duy nhất, chờ ~3 giờ; Oliver duyệt và chuyển COEC về IN PROGRESS; ImpEx có dòng header; chạy đúng phạm vi đã duyệt; kiểm kết quả, ghi bằng chứng, LAUNCH VERIFICATION giao người tạo |

### C. T4 Practical replay – ba đề mẫu (giả lập)
Đạt: first-pass yield ≥90% số replay của service và không lỗi trọng yếu (Merch: 20 ticket thực hành trên staging không lỗi; QA: 20 lần check ≥95% chính xác).

**M-01 (Merch) – AU special price hai đợt Black Friday.** Wave 1: 13/11 00:00–15/11 23:59; wave 2: 16/11 00:00–17/11 23:59. DEMO-A1 1.499 → 1.299 → 1.199 AUD; DEMO-A2 999 → 899 → 849; DEMO-A3 1.490 → 149 → 149. Requester không ghi múi giờ.
| Bước | Kết quả mong đợi (★ = trọng yếu) |
|---|---|
| 1. Nhận, phân loại | APPROVED-ES → STG SETUP; special price Low (24h); R3 (giá); ước tính exposure xét E4 |
| 2. Kiểm đủ thông tin ★ | Thiếu múi giờ: chưa gửi ngay, gom với các điểm khác tìm thấy ở bước 3 để hỏi MỘT lần (ask once, completely) |
| 3. Price sanity ★ | DEMO-A3 giảm 90% bất thường: dừng, không build; MỘT câu hỏi gộp (múi giờ + giá DEMO-A3) trong comment, ON HOLD SUBS và giao ticket cho subsidiary; có trả lời thì về STG SETUP |
| 4. Quy đổi giờ ★ | Giờ Sydney (UTC+11 tháng 11): 13/11 00:00 Sydney = 12/11 20:00 giờ VN |
| 5. Kiểm tra nội bộ ★ | Trước khi build: đối chiếu cấu hình dự kiến với brief đã duyệt (kèm trả lời subsidiary) và ghi tóm tắt lên ticket: SKU, giá, thời gian kèm múi giờ, store, stack, giới hạn dùng |
| 5b. Thiết lập ★ | Hai đợt không chồng (đợt 1 hết 15/11 23:59:59, đợt 2 từ 16/11 00:00); đúng store B2C AU (replay làm trên staging; việc thật trên production) |
| 6. Evidence | Giá trước/sau, thời gian hiệu lực, store theo runbook |
| 7. Cổng kiểm soát ★ | QA REVIEW; Shift Leader duyệt rồi PRD SETUP; không tự duyệt; bằng chứng QA đính Jira cho subsidiary ở REVIEW SETUP |
| 7b. Knox approval ★ | Gửi Knox approval theo approval path trong campaign brief (không tự chọn), ghi lên ticket đã gửi lúc nào, theo path nào; giá/promotion thiếu Knox là lỗi trọng yếu; không chuyển ON HOLD SUBS chỉ để chờ Knox |
| 8. Go-live hai đợt | Đợt 1: QA lại production, về PENDING LAUNCH chờ đợt 2; xong đợt 2 → LAUNCH VERIFICATION |
| 9. Hand-back | Comment tiếng Anh tóm tắt giá, giờ Sydney, mời xem bằng chứng |
Mẫu câu hỏi gộp (bước 3): *"To proceed, please confirm: 1) the time zone of both waves (we assume Sydney time, AEDT); 2) the special price for SKU DEMO-A3 is 149 AUD (regular price 1,490 AUD, 90% off) for both waves. We will resume as soon as we receive your reply."*

**T-01 (Tech) – 3 đơn MY chưa sang NERP** (`DEMO-ORD-001/002` lỗi export; `003` thiếu trường bắt buộc; phát hiện 05:30).
| Bước | Kết quả mong đợi (★ = trọng yếu) |
|---|---|
| 1. Phân loại | Stuck order remediation; P2 (16h); tạo COEC trong 5'; NEW → ASSIGNED là phản hồi đầu |
| 2. Chẩn đoán | Kiểm từng đơn theo runbook; ghi trạng thái, thời điểm, nguyên nhân nghi ngờ |
| 3. Xử lý trong runbook ★ | Đơn 001, 002: chạy lại bước export theo runbook (staging trong replay); xác nhận đã sang NERP. Bước nào đổi dữ liệu thì cần PC như bước 4 |
| 4. Ngoài runbook ★ | Đơn 003: sửa dữ liệu là việc Level 2: chạy thử staging, tự QA, nhờ người kiểm thứ hai (giữ chứng nhận L2 hoặc L3 của service), gửi PC (thay đổi gì, vì sao, kết quả staging, rollback); COEC → ON HOLD HQ "PC ticket pending"; không sửa production khi Oliver chưa duyệt |
| 5. Leo thang ★ | Nguyên nhân ở nền tảng: Maintenance Request cho SDS India kèm evidence pack, COEC → SYSTEM SUPPORT; CoE giữ ownership; theo dõi 2 ngày làm việc/lần |
| 6. Cập nhật | Comment tiếng Anh cho MY: đơn nào đã xử lý, đang xử lý, ETA |

**Q-01 (QA) – kiểm promotion BOGO TH** (mua DEMO-P1 tặng DEMO-C1; 20/11 00:00–22/11 23:59 giờ Bangkok; chỉ B2C; loại trừ DEMO-P9; tối đa 1 quà/đơn; staging có lỗi cài sẵn).
| Kiểm tra | Lỗi cài sẵn | Kết quả mong đợi |
|---|---|---|
| Hiệu lực, múi giờ | Kết thúc 22/11 23:59 giờ Singapore = 22:59 Bangkok (hết sớm 1h) | FAIL, ghi lỗi kèm evidence |
| Sản phẩm loại trừ | Thiếu DEMO-P9 | FAIL |
| Nhóm khách | Có cả nhóm EPP | FAIL |
| Giới hạn quà | Đúng (1 quà/đơn) | PASS mục này |
| Hành vi giỏ hàng | Test bằng simulator: thêm DEMO-P1 → quà tự thêm; xóa DEMO-P1 → quà tự mất | Ghi kết quả từng bước |
Đạt: tìm đủ 3 lỗi, trả ticket về với lý do + evidence từng lỗi; bỏ sót một lỗi là lỗi trọng yếu.

### D. Tiêu chí các bài test khác (tóm tắt)
- **T5 (lên L1):** thực hành 1 ticket trên staging (60–90'), walkthrough runbook (20–30', mọi bước đúng), 4 tình huống ngoại lệ (thiếu thông tin; phối hợp/phê duyệt – ON HOLD COE hoặc PC/ON HOLD HQ; ticket chạm 70%; dấu hiệu sự cố), giao tiếp (Merch, MO) theo rubric T2. Sub-Lead chấm, Lead phê duyệt; mỗi service thi riêng; trượt lần hai xử lý như T4.
- **T6 (tuần có giám sát, lên L2):** FPY ≥90% (T11) / ≥95% (từ T12); không lỗi trọng yếu; đạt mục tiêu phản hồi (78'; P0 và High 15'; P1 30') và không ticket vỡ SLA do người học; kỷ luật ca; giao tiếp. Không đạt: thêm một tuần; lần hai: rời hàng đợi, bench thay, people-risk L2.
- **T7:** RHQ phỏng vấn COE Lead, Lead, Sub-Lead, Tech trước khi cấp quyền production; RHQ không duyệt thì ứng viên thứ hai vào thay (1,5 ứng viên/ghế).
- **T8:** 4 tuần đầu mọi tin nhắn gửi subsidiary/RHQ do Shift Leader hoặc buddy duyệt trong 15'; giải phóng khi đủ 4 tuần **và** 50 tin đạt (rõ – đủ – đúng giọng – đúng sự thật – đúng mẫu trong 12 mẫu CM-08). Sau giải phóng, 2 lần bị đánh giá thấp/tháng hoặc RHQ góp ý → bật lại duyệt 2 tuần.

---

## CM-12 BVT handbook – kiểm thử nghiệp vụ enhancement

Đạt ≥80%; câu 2, 4, 6, 9, 11 và 13 phải đúng (v0.2 thêm câu 13–15).

| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | BVT của một enhancement do ai thực hiện phía CoE? | **(b)** PIC Merch hoặc Tech tùy phạm vi | QA Team không tham gia BVT (mục 1.2, 2.2) |
| 2 ★ | Hết cửa sổ, 33/34 case pass, case còn lại chờ bản sửa | **(b)** không đề xuất sign-off; comment kết thúc nêu sự thật; enhancement không go-live; RHQ quyết | 100% pass mới go-live; dùng mẫu E7; không xin gia hạn (mục 3.5, 9.3) |
| 3 | Tháng có 3 đợt BVT: 90/90 pass lần chạy cuối; 1/3 test report nộp trễ; 3/3 có User Acceptance. Composite mất bao nhiêu điểm vì BVT? | ≈ **1,0 điểm** | Report Completion 2/3 = 66,7% → mất 33,3×0,03 = 1,0 điểm; hai KPI kia 100%. Bằng ~29 ticket vỡ Resolution ở 2.200 ticket (mục 1.4) |
| 4 ★ | 21:05 T5, RHQ gửi BVT notification cho cửa sổ T3–T5 tuần sau. Bạn là Shift Leader ca E: việc theo thứ tự và việc không được làm | (mẫu) | Xác nhận là BVT notification; ghi mục 9 handoff (giờ, kênh, người gửi, mã ticket, ngày, phạm vi, "chờ PIC"); nhắn Merch Lead + Tech Lead trên `coe-leads`, tag Coordinator; có thể trả lời RHQ một câu (E1); mang qua bàn giao đến khi có PIC. **Không** gọi QA on-call, không gọi điện ban đêm (Lead có mặt 08:00 T6, trước cửa sổ), không bàn ngày/phạm vi, không hứa tên PIC (mục 8.1) |
| 5 | Case `TC-COE-SG-02` không chạy được vì chưa có tài khoản test EPP: ghi trạng thái gì, báo ai? | **Blocked**, ghi lý do và giờ báo | Báo Coordinator ngay; Coordinator báo RHQ trên Mattermost (E8), ghi lên trang BVT, nêu ở call (nếu có). Không để Not run đến ngày cuối, không ghi Pass (mục 4.4, 6.3) |
| 6 ★ | Điều nào đúng về ảnh bằng chứng? | **(b)** chụp trên máy trạm CoE, đưa thẳng lên trang BVT, xóa bản trên máy, chỉ dùng tài khoản test | CM-10 (mục 4.5) |
| 7 | Enhancement đổi khối tổng tiền ở giỏ hàng cho SG, MY, AU, ID: nêu 4 case thị trường và lý do | (mẫu) | AU: giá sau coupon vẫn có nhãn "incl. GST"; ID: số tiền lớn không số lẻ, phân cách đúng; MY: ưu đãi thành viên không hiện cho khách vãng lai; SG: coupon B2C không áp trong store EPP; (thêm) stacking với promotion đang chạy (mục 5.1) |
| 8 | Cửa sổ 4 ngày; case quan trọng chỉ chạy lần đầu ngày 3 và fail. Vì sao rủi ro? Quy tắc nào tránh? | (mẫu) | Bản sửa mất 2–3 ngày: lỗi ngày 3 sửa xong sau cửa sổ → enhancement không go-live. Chạy hết case lần đầu trong nửa đầu cửa sổ (4 ngày: hết ngày 2), ưu tiên case rủi ro cao và case thị trường (mục 3.1, 3.4) |
| 9 ★ | Tuần có BVT, tải ca D dự kiến 92% | **(c)** đưa bench vào ticket hằng ngày, chia case cho backup, giảm WIP của PIC | Không dời ngày, không mượn QA Team (chương 7, mục 7.3) |
| 10 | BA phía Spoke trả lời bug ticket "by design": làm gì với kết quả mong đợi của case? | (mẫu) | Không tự đổi. Xin xác nhận bằng văn bản của dev/RHQ; ghi link vào dòng case; nêu rủi ro thị trường ở call (nếu có) hoặc trên kênh liên lạc; chỉ cập nhật kết quả mong đợi khi có xác nhận, rồi chạy lại (mục 6.3) |
| 11 ★ | Vì sao ghi PASS cho case chưa chạy nghiêm trọng hơn nhiều so với case fail? | (mẫu) | Case fail là thông tin đúng, chặn lỗi trước go-live. PASS không test là BVT non-compliance: RHQ sẽ phát hiện; theo RFP 3.4, 3 vi phạm/năm thì RHQ có quyền yêu cầu thay người, thu quyền ngay; phía BiPlus là mức L2 people-risk (CO-05); RHQ còn có thể ghi **strike** (CM-13 ch.17) và nghi ngờ mọi PASS khác (mục 1.5, 6.5). CM-13 chưa nói BVT non-compliance có tính strike không |
| 12 | BVT trên QA server có cần PC không? Khi nào cần? | (mẫu) | Không: QA server là môi trường thử. Nếu một bước đòi thay đổi dữ liệu/cấu hình production thì dừng, hỏi Tech Lead: mọi thay đổi do Tech làm trên production cần PC do Oliver Leung duyệt, kể cả việc 5 giây (CM-13 ch.9; CM-07); thiết lập Merch theo workflow Shop Merchandising và Knox approval, không cần PC (mục 6.3) |
| 13 ★ | Một enhancement áp dụng cho cả 8 subsidiary, đội phát triển đưa 20 test case. CoE test thế nào, tổ chức trang ra sao, Lead tính nhân lực thế nào so với ticket một nước? | (mẫu) | Test case **nhân 8**: 20 case thành 160 lần chạy nếu chạy đủ ở 8 nước. CoE được làm một trang chung hoặc trang riêng mỗi nước, miễn phủ đủ 8 nước trong cùng cửa sổ BVT; không xin dời ngày. Lead tính nhiều người hơn hẳn (cận trên ở mục 7.1 là hơn 6 người toàn thời gian), chia theo nước, mở pool rộng hơn, dùng sớm lớp Cân bằng tải, Bench, báo COE Lead khả năng Surge (mục 1.2, 2.3, 7.1–7.3) |
| 14 | CoE làm hai phần việc nào trong BVT? Ai chủ yếu test frontend? | (mẫu) | (1) Hỗ trợ subsidiary kiểm **backend và cấu hình**; (2) tự test end-to-end và bổ sung case riêng của thị trường. **Subsidiary chủ yếu test frontend** (mục 1.1, 5.4) |
| 15 | Test case và defect của một đợt BVT ghi ở đâu? Cập nhật và tải lên Confluence bao lâu một lần, để làm gì? Có call với RHQ mỗi ngày không? | (mẫu) | Trong **file Excel** (sheet Test case, sheet Defect); cập nhật sau mỗi lần chạy và tải lên trang BVT **mỗi ngày, trước 16:30 SGT**, để RHQ kiểm cuối ngày. Call với RHQ chỉ có thể có, 15 phút gần cuối ngày, không mặc định mỗi ngày (mục 3.3, 4.3) |

## CM-13 Quy tắc RHQ (v1.0, trang mới 22/10/2026)
Trang tập hợp quy tắc RHQ; khi mâu thuẫn với tài liệu khác thì CM-13 thắng. Phụ lục C–D gốc gồm 12 trắc nghiệm + 8 tình huống; phần dưới chép đáp án gốc và diễn đạt lại ý chính.

### A. Trắc nghiệm (đáp án gốc: 1 d · 2 b · 3 a · 4 b · 5 c · 6 c · 7 c · 8 b · 9 b · 10 c · 11 b · 12 c)
| # | Ý chính của câu | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Trạng thái nào dừng đồng hồ SLA trong số các lựa chọn? | **d** – REVIEW SETUP | Cùng ON HOLD SUBS (đã giao Assignee), ON HOLD RHQ/HQ, SYSTEM SUPPORT; ON HOLD COE, QA REVIEW, STG SETUP vẫn chạy (mục 3) |
| 11 | Ticket đã INVALID mà subsidiary muốn làm lại | **b** – clone ticket | INVALID không mở lại được |
| 12 | Oliver Leung vắng 23/10–9/11, cần PC ticket | **c** – vẫn chờ Oliver (~3 giờ) | Oliver là người duyệt PC duy nhất, không có người thay (mục 9) |
| 2–10 | Các câu còn lại | xem dãy đáp án ở tiêu đề | Nội dung câu nằm ở Phụ lục C trang gốc; ý được tóm tắt ở các tình huống dưới và ở "Mười quy tắc" |

### B. Tình huống (8 câu)
| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 1 | Subsidiary trả lời trên ticket ON HOLD SUBS nhưng bạn quên đổi Assignee/trạng thái | Chuyển về **STG SETUP**, nhận ticket và làm tiếp; đồng hồ dừng sai thực tế là lỗi của CoE |
| 2 | Subsidiary cần 300.000 mã coupon, giao diện không làm được | Giữ ticket Merchandising, tạo ticket COEC liên kết (ImpEx), Merch → ON HOLD COE (SLA Merch vẫn chạy), người tạo COEC đôn đốc Tech |
| 3 | 18:10 có yêu cầu cần live 00:00 cùng đêm | Gắn label last-minute, kiểm tra nội bộ + price sanity, Shift Leader duyệt, Knox approval, comment câu chuẩn "Last minute request, please QA on your own when it goes live. If any issue, please contact us." |
| 4 | 23:30 ticket ở REVIEW SETUP, subsidiary chưa duyệt, go-live 00:00 | Publish đúng hạn như đã thống nhất (đã có Knox approval), comment "Published as aligned for go-live at …", ca trực kiểm lại trên production |
| 5 | Cần chạy Groovy xử lý 800 đơn trên production | Staging trước, tự QA + người thứ hai giữ chứng nhận L2/L3, PC ticket do Oliver duyệt, header số PC + COEC gốc; không có PC duyệt thì không chạy |
| 6 | Subsidiary xin danh sách email khách để gửi EDM | **Từ chối** mặc định; không gửi PII qua email Hybris; dữ liệu production cần lý do, PUMI và PC ticket |
| 7 | Ticket tạo EPP site mới chưa có email phê duyệt | Comment "New EPP site creation requires RHQ approval…", ON HOLD SUBS giao subsidiary; có email thì ON HOLD RHQ chờ duyệt; domain email vào EPP access list là việc Tech |
| 8 | Ticket Merch thực ra là việc của Tech (hoặc ngược lại) | Move **chính ticket** sang project đúng (không cần admin) kèm comment chuẩn; sau đó theo SLA của team đó |

### C. Mười quy tắc cần thuộc (tự hỏi–đáp)
| # | Câu hỏi | Đáp án |
|---|---|---|
| 1 | Đồng hồ SLA chạy khi nào? | Chỉ khi việc ở phía CoE |
| 2 | Initial response là gì? | Chuyển trạng thái (APPROVED-ES → STG SETUP; NEW → ASSIGNED), không phải comment |
| 3 | Hỏi subsidiary đúng cách? | ON HOLD SUBS **và** giao Assignee cho subsidiary |
| 4 | ON HOLD COE có dừng SLA không? Cần Tech thì làm gì? | Không dừng; tạo COEC liên kết |
| 5 | QA làm gì, không làm gì? | Chỉ QA việc Merch; không BVT, không QA Tech |
| 6 | Read-back còn không? | Không: thay bằng **kiểm tra nội bộ** trước build |
| 7 | Tech đổi production khi chưa có PC? | Không; ImpEx/Groovy phải có header số PC + COEC gốc |
| 8 | Sửa promotion đã publish nào phải duyệt Knox lại? | Đổi action/condition/website/ngày; đổi tên thì không |
| 9 | Dữ liệu production cần gì? | Lý do, PUMI, PC ticket; không PII qua email |
| 10 | Strike? | RHQ quyết định; 3 strike/năm dương lịch = loại vĩnh viễn |

---

# PHẦN II. TECH TEAM (TC)

## TC-01 Tech Operating Manual

### A. Case book Tech (10 case, giả lập – bài T4, T2, diễn tập on-call)
Ngưỡng đề xuất: đủ ý trọng yếu (★) và ≥80% tổng điểm; T4 chính thức theo CM-11 (FPY 90%, không lỗi trọng yếu).

**A.1 – Replay hủy đơn trên staging (10đ).** T4 14:20 VN tạo COEC `DEMO-7101`: hủy 2 đơn (`DEMO-ORD-8801/8802`) theo yêu cầu khách, đã sang NERP, chưa giao. Bạn là L1 ca chiều.
| Câu hỏi | Đáp án mẫu |
|---|---|
| (1) Trạng thái Jira từ NEW đến LAUNCH VERIFICATION | NEW → ASSIGNED khi nhận, chậm nhất 15:38 (78') ★; IN PROGRESS khi làm; QA REVIEW khi tự kiểm; LAUNCH VERIFICATION giao người tạo ★ |
| (2) Priority, hạn an toàn | P3, 40h; hạn 06:20 T6 |
| (3) Các bước staging | Trước: đúng mã đơn, thị trường, trạng thái cho phép hủy, chưa giao, chụp trạng thái trên máy trạm CoE; hủy theo runbook. Sau: trạng thái hủy, bản ghi hủy sang NERP, hoàn tiền được kích hoạt, bằng chứng trên ticket ★ |
| (4) Production có cần PC không? | **Có**: hủy đơn là thay đổi dữ liệu production nên cần PC được Oliver duyệt, kể cả thao tác theo runbook thường ngày (CM-13 mục 9.1) ★; trên staging thì không |
| (5) Hand-back tiếng Anh | Đủ 4 phần: Status, Evidence, Next step, Next update |

**A.2 – Healthcheck đơn kẹt hàng loạt (10đ).** T5 05:40, L1 ca sớm Team B: 37 đơn MY tạo từ 23:00 chưa sang NERP; SG, PH, AU bình thường; 22:00 có release hằng tháng; Sub-Lead và Tech Lead chưa đến.
| Câu hỏi | Đáp án mẫu |
|---|---|
| (1) SR hay sự cố? | Sự cố: đơn không sang NERP hàng loạt sau release; severity High, Tech P1 ★; lan rộng thì xem xét Critical |
| (2) 15 phút đầu | Mở COEC `[INCIDENT]` P1, ghi T0 05:40, số đơn, bước lỗi ★; gọi ngay Sub-Lead Team B, báo Tech Lead ★; ASSIGNED |
| (3) Có re-trigger export ngay cho 37 đơn? | **Không**: re-trigger đổi trạng thái đơn production, cần PC; P1 cần sửa ngay thì Sub-Lead/Tech Lead nhắn Oliver ★; lỗi do code release thì Maintenance Request cho SDS India |
| (4) Ai báo RHQ | Incident Manager báo RHQ trong 2h (High), cập nhật mỗi 2h |

**A.3 – 500.000 mã coupon (10đ).** T2 09:00 Shop Merch `DEMO-2610` (ID, Medium 16h) vào APPROVED-ES: coupon multi-code 500.000, go-live 00:00 T4; 09:30 MO tạo COEC `DEMO-5102` (P3), issue link, `DEMO-2610` → ON HOLD COE. Bạn là L2 Team A nhận lúc 09:45; ImpEx loại mới.
| Câu hỏi | Đáp án mẫu |
|---|---|
| (1) Đồng hồ nào chạy? Hạn? Vì sao không theo hạn P3? | `DEMO-2610` chạy SLA Merch (ON HOLD COE vẫn tính) ★; `DEMO-5102` chạy SLA Tech; hạn `DEMO-2610` là 01:00 T3; làm theo hạn P3 thì ticket Merch vỡ trước ★ |
| (2) Kế hoạch giờ | 09:45 ASSIGNED, comment ghi ticket liên kết; 10:00–12:00 ImpEx có dòng bắt buộc, staging, tự QA; 12:00 another set of eyes (ImpEx mới bắt buộc) ★; Tech Lead review; 13:00 PC, `DEMO-5102` ON HOLD HQ "PC ticket pending" ★; không nhắn Oliver; báo MO ETA |
| (3) Oliver duyệt 17:30 | Bạn (Level 2, còn tại chỗ đến 18:00) chạy ngay 17:30 theo checklist, kiểm mẫu mã, hand-back, `DEMO-5102` → LAUNCH VERIFICATION giao MO ★; MO đưa `DEMO-2610` về STG SETUP, QA REVIEW (coupon là R3), Shift Leader duyệt, rồi REVIEW SETUP |
| (4) QA làm/không làm | QA kiểm thiết lập coupon ở QA REVIEW của ticket Merch; **không** kiểm ImpEx ★ |

**A.4 – ImpEx thiếu dòng số PC (10đ).** T3 10:00 TM B3 nhờ another set of eyes cho ImpEx gỡ user group khỏi 1.200 tài khoản (`DEMO-6020`); chạy tốt trên staging; dòng đầu `# Remove EPP-PARTNER-OLD group`, không có dòng số PC.
| Câu hỏi | Đáp án mẫu |
|---|---|
| (1) Ghi kết quả kiểm | **"Not OK"**: thiếu dòng số PC + số COEC gốc ★; staging đúng không thay được dòng bắt buộc; trả doer thêm dòng rồi kiểm lại |
| (2) Biến thể: file đã chạy production hôm qua 16:40 | Báo ngay Sub-Lead và Tech Lead ★; ghi sự việc trên ticket đúng như đã xảy ra; **không** sửa, xóa lịch sử hay file đã chạy ★; Tech Lead quyết định cách báo RHQ |
| (3) Hậu quả | Vài ngày sau RHQ/HQ gửi email yêu cầu giải trình; Lead nộp RCA; **RHQ quyết định** ghi strike đầu tiên cho người chạy; đủ **3 strike/năm dương lịch thì bị loại khỏi đội vĩnh viễn**; người nhận strike vào bậc kèm cặp L1 của people-risk ladder và BiPlus thay người trước strike thứ ba |
| (4) CAPA | Vd mẫu file ImpEx có sẵn dòng đầu; người kiểm thứ hai xác nhận dòng này trên ticket |

**A.5 – On-call P0 02:10 CN (15đ).** AU tạo COEC `DEMO-5678`: khách không thanh toán thẻ từ ~05:50 AEDT (01:50 ICT). Shift Leader ca đêm thấy 02:12, test order thẻ lỗi. On-call lớp 1 = Tech Lead; lớp 2 = TM tuần L2 Team B.
| Câu hỏi | Đáp án mẫu |
|---|---|
| (1) Timeline đến khi on-call có mặt | 02:12 Shift Leader xác nhận lỗi, comment, gọi lớp 1 ngay ★; trả lời chậm nhất 02:27; đánh giá qua điện thoại, xác nhận Critical trong 30'; Shift Leader mở kênh sự cố, làm IM tạm thời; initial notification trước 02:40 (30' từ T0 02:10) sau khi on-call duyệt nội dung qua điện thoại ★; on-call gọi lớp 2; có mặt chậm nhất 03:12 |
| (2) Shift Leader được/không được | **Được:** đọc ticket, lỗi, storefront cho on-call; mở bridge; gửi thông báo theo mẫu; báo COE Lead, SDM. **Không được:** chuyển ASSIGNED, sửa cấu hình, liên hệ SDS India, tạo PC, nhắn Oliver ★ |
| (3) Khôi phục cấu hình cũ | ASSIGNED khi on-call đến, IN PROGRESS; thử khôi phục trên staging, tự QA; lớp 2 kiểm; PC khẩn, ON HOLD HQ, nhắn Oliver ★; duyệt thì chạy theo checklist, test order; chưa duyệt thì báo COE Lead, không chạy ★ |
| (4) Nếu lỗi code sau release | Maintenance Request cho SDS India, SYSTEM SUPPORT; CoE giữ ticket, ở trên bridge, cập nhật RHQ mỗi 30' |
| (5) Hạn khôi phục | 4h bất kể giờ làm việc từ lúc báo: 06:10 ICT, cộng thời gian dừng |

**A.6 – On-call không nghe máy (5đ).** T7 23:30 COEC P1 PH (ví điện tử không thanh toán); Shift Leader gọi lớp 1 (Sub-Lead B) 23:32, không ai nghe.
Đáp án: (1) 23:32 lớp 1, gọi lại trong 10'; 23:42 lớp 2 (TM tuần L2 Team B); 23:47 Tech Lead; 23:52 SDM hotline ★. (2) Ghi on-call log trên Confluence Samsung + comment ticket: giờ gọi, số lần, ai trả lời. (3) Sub-Lead B gọi lại 23:58: không trả lời trong 15' là vi phạm quy trình, xem lại ở weekly incident review, xử lý theo CO-05; Lead quyết định ai tiếp tục.

**A.7 – Viết incident update tiếng Anh (10đ).** Critical P0 `DEMO-5678` AU; initial notification 02:40; on-call đến 03:05; cấu hình payment mode thẻ AU bị job đồng bộ ghi đè 01:40; PC `DEMO-PC-0470` gửi 03:20, đã nhắn Oliver, chưa duyệt; bây giờ 03:30. Viết Update 2 (≤10 dòng, mẫu CM-06 mục 5.4).
Mẫu đạt: `[INCIDENT][Critical][AU] Update 2 | DEMO-5678` – "Update 2 at 03:30 ICT (04:30 SGT). Status: not yet restored." – Since the last update: cấu hình bị job đồng bộ ghi đè lúc 01:40 ICT, PC ticket restore gửi 03:20 chờ duyệt – Next steps: áp dụng ngay khi duyệt, verify bằng test order – Impact unchanged – Next update by 04:00 ICT (05:00 SGT). Chấm: tiêu đề đúng mẫu ★, giờ ICT + SGT ★, status rõ ★, nêu sự kiện không đoán/không đổ lỗi, nêu PC đang chờ, next steps cụ thể, impact, next update đúng nhịp 30' ★, không dữ liệu khách.

**A.8 – Ticket EPP access nằm nhầm chỗ (5đ).** SG tạo Shop Merch `DEMO-2701`: thêm 3 email domain cho cửa hàng EPP đối tác và cập nhật banner trang EPP.
Đáp án: (1) Liên kết: có phần Merch (banner) và phần Tech (domain) → giữ ticket Merch ở ON HOLD COE, tạo COEC liên kết cho phần domain ★. (2) Nếu chỉ có phần email domain: move chính ticket sang COEC, không tạo mới; sau đó theo SLA Tech ★. (3) RHQ đã xác nhận 21/10: move ticket giữa các project Jira không cần quyền admin, CoE tự move được; sau khi move ticket theo SLA của team mới.

**A.9 – Oliver duyệt PC lúc 21:30 (10đ).** T3 COEC `DEMO-5160` (TH, P2, sửa delivery mode): tạo 09:00 ở NEW, ASSIGNED 09:20; gửi PC và ON HOLD HQ 15:00; Oliver duyệt 21:30, ticket về IN PROGRESS.
Đáp án: (1) Đã dùng 6h (09:00–15:00 tính từ NEW); dừng 6h30; hạn mới 07:30 T4 ★. (2) 70% (11h12 đã dùng) lúc 02:42; 85% (13h36) lúc 05:06; cả hai mốc ngoài cửa sổ Tech nên thuộc on-call lớp 1 (mục 5.4); on-call ghi `[SLA 70%]` trên ticket khi ở máy trạm CoE (CM-03 mục 5.4) ★. (3) P2 không thuộc phạm vi gọi on-call đến làm; lớp 1 quyết định đến trung tâm hay để ca sớm chạy lúc 04:00, xong trước 05:06, chậm nhất 07:30 ★; rủi ro cao thì lớp 1 đến. (4) Bàn giao 19:00 lẽ ra ghi: "`DEMO-5160` chờ duyệt PC, đã dùng 6h, còn 10h; duyệt trong đêm thì đồng hồ chạy lại, ca sớm chạy trước tiên."

**A.10 – SYSTEM SUPPORT quá hạn follow-up (5đ).** T6 15:00, `DEMO-5190` (P3, NZ, lỗi Rewards trên EA App) ở SYSTEM SUPPORT từ T2 10:00, follow-up cuối T2 10:00.
Đáp án: (1) P3: 4 ngày làm việc; hạn T6 10:00; đã quá 5 giờ ★. (2) Comment ngay "Follow-up with SDS India on the Maintenance Request: [status]. We continue to track it and will update you by [time] NZDT."; cập nhật requester; nhắc trên Maintenance Request, báo Sub-Lead. (3) Báo cáo tuần: một ticket quá hạn follow-up, nguyên nhân (filter không được kiểm mỗi ca), hành động sửa.

### B. Câu hỏi kiểm tra (20 câu)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Ticket COEC tính là CoE đã nhận khi nào? | **b** – NEW → ASSIGNED | Initial response dừng khi NEW sang ASSIGNED (mục 5.1) |
| 2 | Ai được liên hệ SDS India? | **c** – Tech Team Level 2, kể cả on-call | Mục 2.3 |
| 3 | COEC ở trạng thái nào đồng hồ SLA vẫn chạy? | **c – WAITING QA** | ASSIGNED đến WAITING QA tính SLA (mục 5.2) |
| 4 | Chờ Oliver duyệt PC, COEC gốc ở đâu? | **b** – ON HOLD HQ "PC ticket pending" | Oliver duyệt xong đưa về IN PROGRESS (mục 6.2) |
| 5 | Việc nào không cần PC? | **c** – query chỉ đọc để điều tra một ticket cụ thể, có ghi lý do | ImpEx đã dùng nhiều lần vẫn cần PC; lấy dữ liệu làm báo cáo cần PUMI rồi PC (mục 6.1, 6.7) |
| 6 | ImpEx production thiếu dòng nào bị tính strike? | **b** – số PC và số ticket COEC gốc | Quy định của Suwon; một trong ba việc chắc chắn bị strike (mục 6.4) |
| 7 | Khi nào nhắn Oliver qua Mattermost về PC? | **b** – chỉ khi P0, P1 cần sửa ngay | Không gấp thì không nhắn (mục 6.5) |
| 8 | Ticket P3 đã chuyển Samsung L2/L3 follow-up tối thiểu bao lâu? | **c – 4 ngày làm việc** | P0–P2: 2 ngày làm việc; P3: 4; P4: hằng tuần (mục 2.5) |
| 9 | T7 ai làm Level 2? | **b** – hai lead không giữ on-call tuần đó | Mục 4.2 |
| 10 | On-call có mặt làm việc tại trung tâm trong bao lâu? | **c – 60 phút** | Trả lời 15, đánh giá 30, có mặt 60 (mục 4.4) |
| 11 | QA Team làm gì với thay đổi Tech? | **c** – không QA; Tech tự QA trên staging | RHQ 21/10 (mục 7.2) |
| 12 | Merch ở ON HOLD COE chờ COEC liên kết: đồng hồ Merch? | **b – vẫn chạy** | Mục 7.1 |
| 13 | 18:40 T5, bạn là L1 ca chiều; COEC P1 PH lỗi một phương thức thanh toán trong giờ bán; L2 đã về. 15 phút đầu? | (mẫu) | Chuyển ASSIGNED ngay (P1: 30'), comment phản hồi; kiểm nhanh; gọi ngay Sub-Lead Team B, báo Shift Leader; mở `[INCIDENT]`, thông báo RHQ trong 2h (High). Không sửa cấu hình khi chưa có PC được duyệt |
| 14 | Đồng nghiệp: "Chỉ đổi một checkbox Back Office, 5 giây, sửa luôn, PC gửi sau" | (mẫu) | "Không được: không có PC được Oliver duyệt thì không thay đổi production, kể cả 5 giây." Làm đúng thứ tự mục 6.2. Nếu đồng nghiệp đã sửa: báo Sub-Lead ngay, không che giấu |
| 15 | Subsidiary trả lời bằng comment 10:15; ticket vẫn ON HOLD SUBSIDIARY, Assignee vẫn là requester; bạn thấy 11:00 | (mẫu) | Đưa về IN PROGRESS ngay, giao lại Assignee cho người CoE, comment xác nhận. Từ 10:15 việc đã về phía CoE: chờ đến 11:00 là đồng hồ dừng sai thực tế; ghi giờ subsidiary trả lời, tính hạn như đồng hồ chạy lại từ 10:15 (kế hoạch an toàn) |
| 16 | COEC P3 của bạn có Merch Medium liên kết (Merch đã dùng 60%, COEC mới 15%): ưu tiên thế nào? | (mẫu) | Xếp theo hạn của ticket Merch, không theo 15% của COEC: Merch sắp tới 70%, khi đó Shift Leader đôn đốc Tech Lead. Làm ngay, gửi PC sớm nhất, báo Sub-Lead nếu cần thêm người. Comment cho MO một ETA cụ thể theo giờ SGT và điều đang chờ |
| 17 | Ai được làm another set of eyes cho một ImpEx mới? (a bất kỳ TM trên ca; b TM Tech khác, không phải doer, giữ chứng nhận L2 hoặc L3 của đúng service; c người L1 cùng ca; d Shift Leader Merch) | **b** | Người chỉ giữ L1 không làm another set of eyes cho ai (mục 6.3) |
| 18 | Subsidiary xin báo cáo bán hàng từ 1/1 đến nay. Việc đầu tiên của Tech? (a chạy query chỉ đọc rồi gửi; b yêu cầu PUMI đã duyệt, đính Jira, rồi mới gửi PC; c gửi PC ngay; d gửi file qua email Hybris) | **b** | Báo cáo cần PUMI được duyệt rồi PC ticket; không gửi PII qua email Hybris (mục 6.7) |
| 19 | Ai quyết định một người bị strike, và điều gì xảy ra khi đủ 3 strike/năm dương lịch? | **b** – RHQ quyết định; người đó bị loại khỏi đội vĩnh viễn | Ba việc chắc chắn bị strike: thiếu dòng số PC + COEC gốc; đổi production khi chưa có PC duyệt; làm service chưa chứng nhận rồi gây sự cố (mục 6.4) |
| 20 | Ai phụ trách 3PD ở CoE và CoE quản gì? | **b** – PIC chuyên trách thuộc Tech Team, có backup đã chứng nhận 3PD; quản middleware giữa Hybris và marketplace | CoE không vận hành trên marketplace (mục 3.1) |

---

## TC-02 Level 1 Shift Playbook – cẩm nang trực ca Tech Level 1

*(Dùng cho T3 và T4 track T.)*

| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Initial response của ticket COEC đo thế nào? | **(b)** từ NEW đến khi chuyển ASSIGNED | Chỉ comment là chưa đủ (mục 1.5) |
| 2 | Mục tiêu nội bộ initial response P1 và cam kết RFP? | **(b)** 30 phút và 2 giờ | RFP 3.3, đạt ≥97%/tháng |
| 3 | 04:00 T3 vào ca sớm: ba việc phải làm trước khi bắt đầu ticket mới? | (mẫu) | Đọc on-call log và mục 9 handoff note Merch (cùng phần D hôm qua); nhận bàn giao từ on-call lớp 1 (on-call log) và Shift Leader ca đêm (handoff note), gọi thử điện thoại trực; mở dashboard, đếm và ghi phần A, ký "Received by" (mục 1.3) |
| 4 | Queue qua đêm: P3 NEW 21:00; P2 NEW 23:30 (on-call lớp 1 bận một sự cố nên chưa chuyển ASSIGNED kịp); ticket đã được Oliver duyệt PC lúc 02:00 (về IN PROGRESS); P1 NEW 03:20. Xếp thứ tự | (mẫu) | **P1 ở NEW trước** (gọi Sub-Lead và Lead giữ on-call lớp 1; sự cố nếu cần) → ticket PC đã duyệt (đồng hồ chạy lại từ 02:00) → P2 23:30 → P3 21:00. Quy tắc: P0/P1 ở NEW; PC đã duyệt; NEW theo priority rồi theo thời gian; ticket on-call đã ASSIGNED mà chưa có người xử lý thì đổi Assignee sang người đúng team (mục 1.4) |
| 5 | COEC P3 hủy 2 đơn, bạn đã chứng nhận runbook: hủy ngay trên Backoffice được không? Các bước? | (mẫu) | **Không.** Hủy đơn là thay đổi dữ liệu production: chuẩn bị (đơn, ảnh trước) → tự QA → another set of eyes (chạm đơn hàng): TM Tech khác giữ chứng nhận **L2 hoặc L3** của TEC-ORD-02 (người chỉ có L1 không kiểm cho ai; chưa có người kiểm thì chưa gửi PC) → gửi PC, ticket gốc ON HOLD HQ "PC ticket pending", báo requester (A5) → Oliver (duyệt duy nhất) duyệt, về IN PROGRESS → chạy checklist, hủy, kiểm đã sang NERP → LAUNCH VERIFICATION. RHQ xác nhận không thao tác runbook nào được miễn PC (mục 5.6) |
| 6 | Healthcheck có cần PC không? | **(b)** không, vì chỉ đọc | Không được sửa gì trong lúc check (mục 4.1) |
| 7 | Vòng 05:15, HC-02: 12 đơn MY kẹt >2h, AU cũng có dấu hiệu tương tự | (mẫu) | Mở ticket cho từng thị trường theo loại lỗi (hoặc một ticket nếu cùng nguyên nhân), ghi log; hai thị trường cùng dấu hiệu là dấu hiệu sự cố hệ thống: gọi Sub-Lead + Tech Lead ngay (trước 08:00: gọi điện), kiểm HC-05 job export; không tự sửa ngoài runbook (mục 4.6) |
| 8 | Gửi PC lúc 10:00 cho ticket P2: trạng thái ticket gốc, comment, nhắn Oliver? | (mẫu) | ON HOLD HQ, comment "PC ticket pending" (CM-08 mẫu 18) + báo requester (A5); P2 không gấp nên **không** nhắn Oliver (mục 5.6) |
| 9 | Bàn giao 11:00–12:00: đang chạy thay đổi đã duyệt trên Backoffice lúc 11:50 | (mẫu) | Làm xong thao tác và kiểm kết quả rồi mới bàn giao; không bàn giao giữa chừng một thay đổi production (mục 2.3) |
| 10 | COEC P2 không có runbook, nhận lúc 05:00: giữ hay giao ai, đến khi nào? | (mẫu) | Chuyển ASSIGNED và giữ (không giao cho người chưa có mặt), thu bằng chứng, comment 4 phần; giao L2 cùng team lúc 08:00 qua phần B; P2 có dấu hiệu nghiêm trọng thì gọi Sub-Lead (mục 1.5, 5.2) |
| 11 | 18:20 có COEC P3 mới ở NEW: để lại cho Shift Leader Merch sau 19:00 không? | (mẫu) | **Không.** Ticket Tech do Tech chịu trách nhiệm, không đẩy sang Shift Leader. Ticket NEW tạo trước 18:45 phải được L1 chuyển ASSIGNED trước 19:00; để lại thì việc dồn sang on-call lớp 1 ban đêm và initial response kéo dài; ticket tạo từ 18:45 mà chưa nhận kịp thì ghi tên vào phần D cho on-call lớp 1 (mục 3.2, 3.5) |
| 12 | COEC liên kết với Merch ở ON HOLD COE chuyển ON HOLD HQ (chờ PC): đồng hồ nào dừng/chạy, báo ai? | (mẫu) | Đồng hồ Tech dừng (ON HOLD HQ); đồng hồ Merch vẫn chạy (ON HOLD COE). Báo ngay Merch PIC (người tạo COEC) trên `coe-tech` hoặc trực tiếp, cập nhật ETA bằng mẫu A9 (mục 6.4) |
| 13 | Ai được tạo Maintenance Request cho SDS India và chuyển SYSTEM SUPPORT? | **(b)** Level 2 | L2 quyết chuyển và tạo MR; L1 chỉ chuẩn bị phần 1–3 evidence pack (mục 5.1) |
| 14 | Ticket chạm 85% lúc 06:30 (trước khi L2 có mặt): báo ai, kênh nào? | (mẫu) | Báo Sub-Lead cùng team (tầng 70% đã qua) và Tech Lead (tầng 85%, xử lý trong 30') **bằng điện thoại**, vì trước 08:00 nhắn tin không được coi là đã báo (mục 5.5) |
| 15 | Được phân vào một đợt BVT: bốn quy tắc về bằng chứng và tiến độ trên trang Confluence BVT | (mẫu) | Test từ ngày đầu, không dồn cuối; mỗi case có ảnh bằng chứng của chính case đó, chụp trên máy trạm CoE, đưa thẳng lên Confluence, xóa bản trên máy; chỉ điền PASS khi đã test; cập nhật file Excel và tiến độ trước call cuối ngày (nếu có; mốc nội bộ 15:30 giờ VN); lỗi thì báo PIC ghi dòng defect trong file Excel cho đội phát triển triage; 100% pass mới go-live (mục 3.3) |
| 16 | 05:40 HC-06: khách SG không qua được bước thanh toán: ba việc đầu? | (mẫu) | Dấu hiệu P0: tạo/nhận COEC P0, ghi T0 + bước lỗi; gọi Sub-Lead cùng team và Lead giữ on-call lớp 1; người còn lại giữ queue; theo playbook "khách không đặt hàng được" CM-06 mục 6.4 (mục 4.6) |
| 17 | 19:00 còn một ticket runbook P3 của Team A đang mở: Assignee qua đêm cho ai, ghi gì vào phần D? | (mẫu) | Giao L1 ca sớm Team A (người trực 04:00 sáng mai); phần D mục D4 ghi ticket, next action, SLA còn lại (mục 3.5) |
| 18 | Ticket ON HOLD SUBSIDIARY, Assignee vẫn là bạn, comment cuối là trả lời của subsidiary lúc 14:05 | (mẫu) | Chuyển ngay về IN PROGRESS, làm tiếp (giao lại người CoE nếu cần); lỗi làm đồng hồ dừng sai thực tế trong khi việc đã về phía CoE (mục 6.5) |
| 19 | L1 có được chạy ImpEx đã dùng nhiều lần trên production khi đã có PC duyệt không? | (mẫu) | **Không.** ImpEx/Groovy trên production chỉ do L2 chạy, khi có PC đã duyệt và có dòng số PC + COEC gốc (thiếu = một trong ba việc chắc chắn bị strike); L1 chuyển L2 (mục 5.1, CM-09 mục 7.4) |
| 20 | T7 19:00 không có P0/P1 mở: có phải gọi on-call không? Phần D thứ Bảy khác gì? | (mẫu) | **Có**: thứ Bảy luôn gọi on-call lớp 1 xác nhận bàn giao vì on-call giữ đến 04:00 T2. Phần D thêm danh sách ticket cần xem ở hai lần kiểm queue CN (09:00, 17:00) và ticket đến hạn trước sáng T2 (mục 3.5) |
| 21 | Kể ba việc chắc chắn bị tính strike và hậu quả khi đủ ba strike | (mẫu) | Thiếu dòng header (số PC + số COEC gốc) ở đầu file ImpEx/Groovy; thay đổi production khi chưa có PC duyệt; làm service chưa chứng nhận rồi gây sự cố. **RHQ quyết định ai bị strike**; 3 strike/năm dương lịch thì bị loại vĩnh viễn; người nhận strike vào bậc kèm cặp, BiPlus chủ động thay người trước strike thứ ba (mục 5.6). Vi phạm ATTT chưa tính strike nhưng vẫn xử lý theo CM-10 |
| 22 | Ticket COEC từ subsidiary MY xin "tạo EPP site mới cho đối tác", chưa có email phê duyệt trên ticket: bạn làm gì, trạng thái? Cùng ngày một ticket khác xin danh sách đơn hàng từ 1/1 đến nay: trả lời thế nào? | (mẫu) | Không tạo site: hỏi phê duyệt trước. Chưa có email → trả subsidiary, comment mẫu A10 ("New EPP site creation requires RHQ approval…"), ON HOLD SUBSIDIARY (tạm) và giao Assignee cho subsidiary; có email → ON HOLD HQ để Oliver duyệt (mục 5.1). Danh sách đơn từ 1/1 đến nay là dữ liệu lịch sử: cần **PUMI** được duyệt rồi mới đến PC ticket, comment mẫu A11; không gửi danh sách qua email từ Hybris (mục 5.6) |

---

## TC-03 Quy trình Tech trên COEC và làm việc với Samsung L2/L3

### A. Trắc nghiệm (12 câu)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Trạng thái COEC nào **tính** SLA? | **(c) WAITING QA** | WAITING QA là thời gian của CoE; ON HOLD HQ, SYSTEM SUPPORT dừng; LAUNCH VERIFICATION không tính (mục 1.3) |
| 2 | Initial response của Tech đo thế nào? | **(b)** từ NEW đến khi chuyển ASSIGNED | Comment không đủ (mục 1.5.1, 3.1) |
| 3 | Ticket COEC có bước subsidiary duyệt trước khi vào hàng đợi CoE không? | **(b)** không, mặc định ở NEW | Do Merch, QA, HQ hoặc subsidiary tạo (mục 2.1) |
| 4 | Đã chạy xong staging và tự QA đạt một ImpEx mới. Bước tiếp? | **(b)** nhờ another set of eyes (người giữ chứng nhận **L2 hoặc L3** của đúng service), Tech Lead rà vì rủi ro cao, rồi gửi PC và chuyển ON HOLD HQ | Kiểm soát nội bộ nằm trước PC; ImpEx mới bắt buộc người kiểm thứ hai, không phải doer (mục 4.3, 4.4) |
| 5 | Vừa gửi PC cho thay đổi P3. Việc đúng? | **(c)** ON HOLD HQ + "PC ticket pending", không nhắn Oliver | Chỉ P0/P1 cần sửa ngay mới nhắn (mục 4.5) |
| 6 | ImpEx production thiếu dòng số PC + COEC gốc: hậu quả? | **(b)** RHQ/HQ yêu cầu giải trình và tính strike cho người chạy | Quy định của Suwon (mục 4.5) |
| 7 | Ai được liên hệ Samsung L2/L3 (SDS India)? | **(c)** chỉ Tech Team Level 2, kể cả on-call Tech | Mục 6.1 |
| 8 | COEC P3 ở SYSTEM SUPPORT: nhịp follow-up tối thiểu theo RFP? | **(c)** 4 ngày làm việc | P3 thuộc nhóm Medium, mỗi lần một comment (mục 6.5) |
| 9 | COEC ở SYSTEM SUPPORT thì Assignee là ai? | **(c)** người Tech L2 của CoE đang giữ ticket | CoE giữ ownership; chỉ ON HOLD SUBSIDIARY và LAUNCH VERIFICATION giao Assignee ra ngoài CoE (mục 1.6) |
| 10 | Merch PIC tạo COEC nhờ ImpEx; Merch ở ON HOLD COE; COEC ON HOLD HQ 3h. Đồng hồ Merch trong 3h? | **(b)** vẫn chạy | Đồng hồ Tech dừng không làm đồng hồ Merch dừng (mục 2.3) |
| 11 | Subsidiary tạo Shop Merch mà toàn bộ là việc Tech (whitelist domain EPP, tạo access code) | **(b)** move chính ticket sang COEC | Toàn bộ việc của team kia thì move, không tạo mới; CoE tự move được, không cần quyền admin (mục 2.4) |
| 12 | Tech làm xong ticket subsidiary tạo. Ticket chuyển sang? | **(b)** LAUNCH VERIFICATION, giao người tạo | Người tạo xác nhận và có thể đóng; ticket tồn thì RHQ đóng định kỳ, CoE chưa tự chuyển CLOSED (mục 7.2, 7.3) |

### B. Tình huống (8 câu, đáp án mẫu)
| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 13 | 05:20 T5, COEC P2 SG báo đơn kẹt; bạn là L1 ca sớm Team B; runbook cho thấy cần sửa dữ liệu đơn ngoài runbook. Làm gì từ 05:20 đến khi L2 nhận? | (1) 05:20 chuyển ASSIGNED ngay, comment phản hồi đầu (P2: mục tiêu 78'; tốt nhất vài phút). (2) IN REVIEW: kiểm theo runbook ở chế độ chỉ đọc; xác định cần sửa dữ liệu ngoài runbook = việc L2. (3) Khung 04:00–08:00 chỉ có L1: P2 chạm 50% lúc 13:20 (sau 08:00) nên không gọi Sub-Lead sáng sớm; thu thập bằng chứng (mã đơn, trạng thái, lỗi, ảnh chỉ đọc), soạn phần 1–6 evidence pack. (4) Có dấu hiệu sự cố (nhiều đơn/nhiều thị trường) thì gọi Sub-Lead ngay. (5) 08:00 đổi Assignee cho TM tuần L2 Team B, comment handover 4 phần (A.2), nhắn kênh nội bộ; giữ IN REVIEW (đồng hồ vẫn chạy). (6) Chờ L2 xác nhận trong 15'; chưa xác nhận thì vẫn giữ ticket |
| 14 | Hỏi subsidiary TH ba thông tin, chuyển ON HOLD SUBSIDIARY nhưng quên đổi Assignee; 2h sau requester trả lời | Sai: chuyển trạng thái chờ mà không giao ticket cho subsidiary (requester có thể không biết đang được hỏi; dashboard "chờ subsidiary có Assignee CoE" sẽ hiện ticket). Đồng hồ dừng từ lúc chuyển ON HOLD SUBSIDIARY; requester đã trả lời mà ticket còn nằm chờ → đồng hồ dừng sai thực tế. Sửa: ngay khi thấy trả lời, chuyển về trạng thái làm việc trước đó, giữ Assignee là bạn, comment làm tiếp (A.4), tính lại hạn chỉ cộng thời gian dừng đến lúc requester trả lời. Lần sau: comment, trạng thái, Assignee cùng lúc |
| 15 | Ticket EPP cần (1) thêm domain (CoE làm, cần PC) và (2) tài khoản Back Office do đội khác tạo; bạn gửi yêu cầu tài khoản 09:50, đang làm domain trên staging. Trạng thái lúc 10:00? Khi nào ON HOLD ES? | 10:00 ticket ở IN PROGRESS (CoE còn việc làm được → đồng hồ chạy). Tiếp theo: QA REVIEW, another set of eyes (quyền truy cập), PC và ON HOLD HQ khi chờ duyệt. Chỉ chuyển ON HOLD ES khi phần domain đã chạy và kiểm xong trên production và phần còn lại chỉ là chờ tài khoản; comment đội nào, mã yêu cầu, ngày nhắc (A.8) |
| 16 | SDS India comment trên Maintenance Request lúc 08:40 hỏi thêm dữ liệu một đơn mẫu; COEC ở SYSTEM SUPPORT; bạn thấy lúc 09:00 | SDS India hỏi lại = bóng về phía CoE: chuyển COEC về IN PROGRESS, chuẩn bị dữ liệu (che dữ liệu cá nhân), trả lời trên MR, rồi chuyển lại SYSTEM SUPPORT kèm comment. Lập kế hoạch tính đồng hồ từ **08:40** (lúc SDS India hỏi), không phải 09:00. Bài học: theo dõi thông báo MR, không chỉ chờ tới giờ follow-up |
| 17 | COEC P3 tạo 10:00 T2. ON HOLD SUBSIDIARY 11:00–14:00 (trả lời lúc 14:00); ON HOLD HQ 15:30 T2 – 09:30 T3. Tính hạn lập kế hoạch | Hạn ban đầu 10:00 T2 + 40h = 02:00 T4. Thời gian dừng: 3h + 18h = 21h. Hạn lập kế hoạch: 02:00 T4 + 21h = **23:00 T4** (ví dụ mục 5.6) |
| 18 | Merch PIC tạo COEC 10:15 nhờ ImpEx 500.000 mã coupon; ticket Merch Medium đã dùng 1h45 lúc đó. Bạn là Sub-Lead Tech: priority và due date nội bộ? Vì sao không xếp như P3 thường? | Priority theo catalogue ImpEx dữ liệu hàng loạt (P3, 40h), ghi lý do. Due date nội bộ = mốc sớm hơn giữa hạn SLA COEC và hạn ticket Merch trừ thời gian Merch cần sau Tech: Merch còn ~14h15, cần thêm ~2h để kiểm, QA, duyệt (có E4) → Tech trả kết quả buổi chiều cùng ngày (vd 16:00). Không xếp như P3 thường vì ticket Merch ở ON HOLD COE vẫn chạy SLA kể cả khi COEC chờ PC ở ON HOLD HQ; làm sáng hôm sau thì Merch vỡ SLA dù COEC vẫn trong hạn (mục 8.4). Thêm: ImpEx mới bắt buộc staging, another set of eyes, Tech Lead rà; báo Merch PIC mỗi lần COEC vào trạng thái chờ |
| 19 | 22:40 T3, ticket COEC mới ở NEW, Shift Leader Merch đọc như P2. Ai nhận cảnh báo? Shift Leader được/không được làm gì? On-call lớp 1 làm gì, ở đâu, theo mốc nào? | Email cảnh báo filter COEC NEW (nhịp 5') đến **on-call lớp 1 của Tech**, không đến Shift Leader. Shift Leader quét dashboard và chỉ gọi on-call khi thấy P0/P1; ticket này đọc như P2 nên không gọi, không chuyển ASSIGNED, không phân công, không xử lý ticket Tech. On-call lớp 1 chuyển ASSIGNED **tại máy trạm CoE ở trung tâm, không remote**: khi có mặt thì ASSIGNED, đăng comment Mẫu 13 (CM-08) và ghi handoff cho Level 1 ca 04:00; chưa có mặt thì ticket chờ đến lần on-call ngồi vào máy trạm hoặc 04:00 (Level 1 chuyển ASSIGNED trước tiên). Mốc TC-04: nghe máy 15', có mặt tại trung tâm 60' khi phải làm trên hệ thống. Cách đạt initial response 2 giờ cho P2–P4 khi on-call chưa có mặt: chờ RHQ/anh David chốt (TC-04 mục 4.3) |
| 20 | Cùng một ngày subsidiary gửi hai ticket COEC: (a) xuất báo cáo doanh số tháng 11 từ production; (b) tạo EPP site mới cho công ty đối tác. Mỗi ticket: kiểm gì trước, trạng thái Jira + Assignee khi thiếu điều kiện, thay đổi production qua những bước nào? | (a) Kiểm **PUMI** đã duyệt (subsidiary tạo) đã đính Jira chưa; chưa có → comment mẫu A.12, ON HOLD SUBSIDIARY và giao ticket cho subsidiary (tạm, RHQ chưa nói trạng thái chờ PUMI); có PUMI rồi mới làm, lấy dữ liệu từ production thì tiếp theo cần staging, QA REVIEW, PC ticket đã duyệt; query chỉ đọc để điều tra không cần PC nhưng ghi lý do. (b) Hỏi ngay đã có phê duyệt chưa; chưa có → comment mẫu A.11, ON HOLD SUBSIDIARY, giao subsidiary xin phê duyệt theo link template RHQ; có email phê duyệt → ON HOLD HQ, comment \"EPP approval pending\" cho Oliver duyệt (chỉ duyệt khi có email); sau đó việc tạo site vẫn đi staging, QA REVIEW, another set of eyes và PC riêng (tạm làm hai bước tách biệt) |

---

## TC-04 On-call Handbook Tech

### A. Trắc nghiệm (10 câu)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Tuần Sub-Lead B giữ lớp 1, ai là lớp 2? | **C** – TM tuần Level 2 của Team B | Lớp 2 là TM tuần L2 cùng team với lớp 1 (mục 2.2) |
| 2 | Tuần Tech Lead giữ lớp 1. 01:00 Shift Leader gọi Tech Lead, gọi lại 01:05, không ai nghe. 01:15 gọi ai? | **C** – Sub-Lead A (Deputy của Tech Lead) | Phút 15 gọi Tech Lead; nếu Tech Lead chính là lớp 1 thì gọi Sub-Lead A, Deputy (mục 2.5) |
| 3 | Bạn đang trên xe đến trung tâm. Việc nào được phép? (A mở email Samsung trên điện thoại để đọc email cảnh báo COEC NEW/Open High; B đọc kênh sự cố Mattermost bằng điện thoại; C gọi lớp 2 và nghe Shift Leader đọc tiến triển qua điện thoại; D nhắn Oliver trên Mattermost bằng điện thoại) | **C** | Ngoài trung tâm chỉ nghe và chỉ đạo bằng lời; email Samsung, Mattermost chỉ dùng trên máy trạm (mục 3.2) |
| 4 | Sự cố Critical có T0 23:10: initial notification gửi RHQ trước mấy giờ (mục tiêu nội bộ)? | **B – 23:40** | Critical: 30' từ T0 (nội bộ); RFP 2h (mục 5.2) |
| 5 | Đã gửi PC rollback cho P0 và nhắn Oliver: COEC gốc ở đâu? | **B** – ON HOLD HQ "PC ticket pending" | Mục 6.3, bước 7 |
| 6 | Việc nào lúc 02:00 **không** cần PC? (A ẩn payment mode thẻ một thị trường; B đẩy lại 20 đơn kẹt bằng ImpEx đã dùng nhiều lần; C Merch tắt một promotion sai giá theo workflow Shop Merch; D rollback delivery zone đã chạy chiều nay) | **C** | Khống chế Merch đi theo workflow Shop Merch; A, B, D là thay đổi Tech trên production, cần PC (mục 6.1) |
| 7 | Bị gọi làm 23:00–02:30 đêm T3; sáng T4 làm L2. Bắt đầu sớm nhất lúc? | **C – 10:30** | Làm 3h30 trong khung 22:00–06:00 (>2h) nên nghỉ ≥8h sau 02:30 (mục 8.4) |
| 8 | 04:00 P0 vẫn chạy: ai giữ vai Incident Manager? | **C** – lớp 1 vẫn giữ đến khi khôi phục hoặc một lead có mặt nhận vai | Team Member không làm IM (mục 8.2) |
| 9 | Lớp 2 nghe máy phút 10, lớp 1 vẫn chưa trả lời. Shift Leader làm gì tiếp? | **C** – lớp 2 lên đường; Shift Leader vẫn gọi Tech Lead phút 15 và SDM phút 20 đến khi có lead nhận vai | Lớp 2 không làm IM; call tree tiếp tục (mục 2.5) |
| 10 | Kênh báo chính cho on-call khi ở ngoài trung tâm? | **B** – cuộc gọi điện thoại của Shift Leader | Email cảnh báo (COEC NEW 5', Open High 15') chỉ đọc tại máy trạm (mục 4.1) |

### B. Tình huống (8 câu)
| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 11 | 02:10 CN, Shift Leader gọi: trang chủ và trang danh mục VN lỗi 503 từ 02:00, trang sản phẩm vẫn mở. Bạn là lớp 1: hỏi và chỉ đạo gì trong 15 phút của cuộc gọi? | Hỏi 8 câu (mục 3.4), nhất là: mã lỗi; kênh, thị trường khác; có go-live nội dung, PC hay release nào lúc 02:00 không; dấu hiệu an ninh. Quyết Critical P0. Sáu chỉ đạo: Shift Leader làm IM và PIC tạm thời; mở bridge; gọi lớp 2, báo COE Lead + SDM; thông báo duyệt trước phút 25, gửi trước phút 30 từ T0; nội dung vừa go-live thì Merch gỡ; không ai động cấu hình Tech; nói ETA (mục 7.6) |
| 12 | 00:40, PC gấp của P0 đã chờ duyệt 30'; khách vẫn không thanh toán được bằng thẻ. TM nói "Chạy luôn đi anh, chỉ 5 giây." | **Không chạy.** Ticket giữ ON HOLD HQ. Chuẩn bị sẵn để chạy ngay; tìm khống chế không cần Tech; nhắc Oliver một lần (đã quá phút 15), gọi COE Lead; COE Lead gửi Mẫu T6. Cập nhật: *"Update [n] at 00:40 ICT (01:40 SGT). Status: fix ready, waiting for PC ticket approval. Customers still cannot pay by card. Next update by 01:10 ICT (02:10 SGT)."* (mục 6.4, 5.4) |
| 13 | 21:00 T7, khách MY bị trừ tiền mà không có đơn khi trả bằng ví điện tử; thẻ và chuyển khoản vẫn chạy: workaround, ai đồng ý, bước trước khi làm production? | Tạm ẩn ví điện tử MY để khách dùng thẻ/chuyển khoản. Cần RHQ đồng ý trên bridge (ghi tên, giờ) và PC được Oliver duyệt. Trước đó: bước bật lại viết trước, staging, QA REVIEW, another set of eyes, PC, ON HOLD HQ, nhắn Oliver. Song song: Maintenance Request cho SDS India, danh sách giao dịch bị ảnh hưởng (mục 7.5) |
| 14 | 17:00 CN, bạn là lớp 1 đang ở máy trạm cho lượt kiểm queue; thấy COEC P2 vừa về IN PROGRESS 15:30 sau khi PC duyệt; SLA còn 9h. Bạn làm gì, Shift Leader có vai trò gì với ticket? | **Xử lý ngay trong lượt kiểm.** Đồng hồ chạy lại từ 15:30; còn 9h thì hạn ~00:30 T2, trước 04:00 T2 (lập kế hoạch theo giờ lịch), khớp tiêu chí đề xuất mục 4.5 (chờ Tech Lead chốt). Đi qua checklist trước khi chạy (CM-07), chạy, kiểm, LAUNCH VERIFICATION khi đã xác minh, ghi on-call log. **Shift Leader không nhận ticket này và không chuyển trạng thái**; chỉ gọi bạn khi thấy P0/P1 (mục 4.2, 4.5) |
| 15 | Viết tin Mattermost tiếng Anh cho Oliver: PC gấp P1 `DEMO-PC-44` cho COEC `DEMO-7520`, SG, đơn không về NERP; thay đổi là đẩy lại các đơn kẹt bằng ImpEx | *"Hi Oliver, urgent PC ticket for your approval: DEMO-PC-44, for COEC ticket DEMO-7520 (P1, SG, orders not reaching NERP). Change: re-push the stuck orders with an ImpEx. The data screenshots are in the PC ticket. Could you please review it? Thank you. [Name], Tech on-call, BiPlus Ops CoE"* (mục 6.3, bước 8) |
| 16 | Đồng nghiệp mới hỏi: "Quét COEC NEW mỗi 5 phút nghĩa là em phải mở Jira trên điện thoại ở nhà, cứ 5 phút một lần, đúng không?" Trả lời ba ý: nhịp 5 phút là nhịp của gì, quét ở đâu, ticket NEW không phải P0/P1 tạo lúc chưa có mặt thì sao | (mẫu) | **Không.** Nhịp 5 phút là nhịp của email cảnh báo filter COEC NEW (COE-F01T) gửi on-call lớp 1. Email nằm hộp thư Samsung nên chỉ mở và quét ở máy trạm CoE tại trung tâm; chưa có mặt thì không mở hệ thống nào (không làm remote). Ticket NEW không phải P0/P1 tạo lúc bạn chưa có mặt chờ đến khi bạn ngồi vào máy trạm hoặc Level 1 ca 04:00; cách đạt initial response 2 giờ cho nhóm này chờ Tech Lead + COO chốt (mục 4.1, 4.3) |
| 17 | 01:20, bạn là lớp 1 vừa soạn xong ImpEx rollback cho P0 và thử xong trên staging. Lớp 2 tuần này chỉ giữ chứng nhận L1 của service đó. Lớp 2 có được làm người kiểm thứ hai không? Bạn làm gì, có gửi PC ngay không? | (mẫu) | **Không.** Người chỉ giữ L1 không làm người kiểm cho ai; người kiểm phải giữ chứng nhận **L2 hoặc L3** của đúng service. Gọi thêm một TM Tech đủ chứng nhận (Sub-Lead, Tech Lead) theo call tree, nhờ kiểm file + kết quả staging, ghi comment "Second check: [tên], [giờ], [kết quả]". Chưa có người kiểm thì **chưa gửi PC**, và nói rõ trong cập nhật RHQ (mục 2.2, 6.2) |
| 18 | 02:30 bạn chạy ImpEx đẩy lại đơn kẹt sau khi PC đã duyệt nhưng quên dòng đầu file ghi số PC + số COEC gốc; nhận ra lúc 03:00. Làm gì ngay? Hậu quả và ai quyết định? | (mẫu) | Báo Lead ngay, ghi lên ticket việc đã chạy và việc còn thiếu (báo sớm được ghi nhận, giấu lỗi là vi phạm nghiêm trọng). Thiếu dòng đầu file là một trong ba việc chắc chắn dẫn tới strike; **RHQ quyết định**, không phải BiPlus; Lead giải trình bằng RCA; 3 strike/năm dương lịch bị loại vĩnh viễn. Nội bộ: người bị strike vào bậc kèm cặp L1 của people-risk ladder (MR-06 mục 6.7), BiPlus thay người trước strike thứ ba (mục 6.6) |

---

## TC-05 Runbook catalogue, PC ticket và change rules

Đạt khi đúng ≥17/20 và đúng hết câu 1, 3, 4, 11 (v0.2 thêm câu 19–20).

### A. Trắc nghiệm (10 câu)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 ★ | Xóa user group khỏi một tài khoản qua Back Office (5 giây): cần PC không? | **b – Có** | Mọi thay đổi dữ liệu do Tech trên production cần PC, kể cả việc 5 giây (mục 1.4, 3.2) |
| 2 | Ai duyệt PC của cụm SEAO? | **c** – Oliver Leung (RHQ), người duyệt duy nhất | HOD cụm SEAO gồm cả SMB; không có backup (mục 3.5) |
| 3 ★ | Chờ duyệt PC, COEC gốc ở đâu? | **b** – ON HOLD HQ, đồng hồ dừng, comment "PC ticket pending" | Oliver duyệt xong về IN PROGRESS (mục 3.3, 3.7) |
| 4 ★ | Dòng bắt buộc trong mọi ImpEx và Groovy ghi gì? | **b** – số PC và số ticket COEC gốc | Quy định của Suwon; định dạng chính thức chờ RHQ (mục 2.4) |
| 5 | Khi nào nhắn Oliver qua Mattermost về PC? | **c** – chỉ khi P0, P1 cần sửa ngay | Không gấp thì không nhắn (mục 3.6) |
| 6 | Mở đơn trên Back Office xem trạng thái và chạy query FlexibleSearch chỉ đọc để điều tra một ticket COEC: cần PC không? | **b – Không, nhưng ghi lý do trên ticket** | Groovy hoặc ImpEx chạy trên production luôn cần PC, kể cả chỉ đọc (mục 1.3, 1.4) |
| 7 | Ai được chạy Groovy trên production? | **b** – Tech Level 2 hoặc on-call được giao, khi có PC đã duyệt | Ngoài giờ là on-call; luôn có PC đã duyệt (mục 2.7) |
| 8 | ImpEx IMP-TEC-02 đã được Tech Lead đánh dấu repeat-use (thêm domain EPP). Điều nào đúng? | **b** – có thể không kèm kết quả staging nhưng vẫn cần PC, dòng bắt buộc và another set of eyes | Repeat-use chỉ bỏ được kết quả staging; thay đổi chạm quyền vẫn cần another set of eyes (mục 1.6, 4.2) |
| 9 | Ticket Shop Merch ở ON HOLD COE chờ COEC, COEC đang chờ duyệt PC. SLA Merch? | **b – Vẫn tính** | Tech chậm bao lâu thì Merch trễ bấy lâu (mục 3.7) |
| 10 | Hybris hard freeze, MY cần thêm payment mode. Cần gì? | **c** – phê duyệt ngoại lệ ghi trong body ticket, kiểm soát nội bộ rủi ro cao, rồi PC | Hai phê duyệt riêng: ngoại lệ freeze và PC; payment mode là rủi ro cao (mục 6.2, 4.2) |

### B. Tình huống (câu 11–20; ★ = ý bắt buộc)
| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 11 ★ | 02:10 CN, P0 khách MY không checkout được. On-call lớp 1 đang trên đường (45' nữa tới). Shift Leader đề nghị on-call đọc từng bước qua điện thoại để Shift Leader sửa cấu hình payment trên Back Office cho nhanh | **Từ chối**: Shift Leader không đổi cấu hình Tech; **không thay đổi production khi chưa có PC được duyệt**; không làm remote, không mở hệ thống Samsung trên điện thoại. Trên đường: chỉ đạo bằng lời việc khống chế không cần thay đổi Tech (nếu có); nhờ Shift Leader mở bridge, giữ IM tạm thời; initial notification RHQ trong 30' (Critical) sau khi on-call duyệt nội dung. Đến trung tâm: chẩn đoán, staging nếu kịp, second check với lớp 2, **tạo PC, ON HOLD HQ, nhắn Oliver qua Mattermost từ máy trạm**; chạy khi đã duyệt (mục 3.6; CM-06) |
| 12 | Chạy ImpEx gỡ user group cho 50 tài khoản lúc 15:00; 17:00 phát hiện file không có dòng số PC | **Báo Tech Lead ngay trong ca** (quy tắc vàng 8); Tech Lead báo RHQ chủ động; ghi trên COEC và PC. **Không** sửa log, không chạy lại để "che", không xóa lịch sử. Tech Lead mở improvement record + CAPA; bạn chứng nhận lại runbook trước khi chạy tiếp. Thiếu dòng này là một trong ba việc chắc chắn dẫn tới **strike**; RHQ là bên quyết định. Báo sớm được ghi nhận, giấu lỗi là vi phạm nghiêm trọng (mục 3.8) |
| 13 | PC đã duyệt cho 3 đơn kẹt; ngay trước khi chạy, healthcheck thấy đơn thứ 4 cùng lỗi; đồng nghiệp bảo "thêm luôn" | **Không thêm**: đơn thứ 4 ngoài phạm vi PC. Chạy 3 đơn như đã duyệt; **mở PC bổ sung** cho đơn thứ 4. Chạy ngoài phạm vi bị coi như chạy không có PC (mục 3.8, 3.10; 2.9 bước 10) |
| 14 | Oliver comment trên PC: "Please attach the staging result." COEC gốc đang ON HOLD HQ | Việc đã về phía CoE: **chuyển COEC gốc về IN PROGRESS** (đồng hồ chạy), bổ sung kết quả staging vào PC, comment trả lời; gửi lại thì **chuyển lại ON HOLD HQ** với comment "PC ticket pending" mới (mục 3.3) |
| 15 | Kiểm ImpEx đồng nghiệp: staging 0 lỗi, nhưng có `groups(uid)[mode=replace]` trong khi yêu cầu là gỡ một group | **Sai**: `mode=replace` thay cả danh sách group; "0 lỗi" không có nghĩa là đúng. Không đồng ý gửi PC; yêu cầu **đổi sang `mode=remove`**, chạy lại staging, kiểm group khác vẫn còn. Comment trên ticket; ghi known error vào runbook (mục 4.4) |
| 16 | Groovy staging có dòng `// PC ticket: TBC \| COEC ticket: DEMO-6031`; vừa tạo PC `DEMO-PC-0457`. Các bước tiếp theo trước khi đính file? | **Thay `TBC` bằng `DEMO-PC-0457`**; người kiểm so hai bản, **chỉ khác đúng dòng này**; đính bản cuối vào PC; bản chạy production phải giống hệt bản đã đính; sau khi duyệt không sửa (mục 2.4) |
| 17 | T4 11/11 (Sprint 2), thấy đơn PH kẹt định đẩy lại; trên COEC thấy ticket của đơn vị vận hành hiện tại (SDSAP) đang xử lý cùng đơn | **Không làm**: một ticket một owner; không chạm cùng bản ghi với đơn vị vận hành hiện tại. Comment liên kết trên ticket BiPlus, ghi vào biên bản bàn giao. Lý do: đẩy cùng lúc có thể làm đơn vào NERP hai lần (mục 5.4) |
| 18 | Đơn có log đã gửi sang NERP nhưng không có số đơn NERP: đẩy lại không? | **Không đẩy lại**: không chắc đơn đã vào NERP hay chưa nên coi là không an toàn để gửi lại (not retry-safe); đẩy lại có thể tạo đơn trùng. **Maintenance Request cho SDS India** hỏi đội NERP; COEC sang SYSTEM SUPPORT; theo dõi theo nhịp RFP (mục 2.9 bước 5; TC-03) |
| 19 | Subsidiary Úc tạo ticket COEC xin "báo cáo bán hàng từ 1/1 đến nay cho audit", kèm danh sách email khách hàng đã mua. Bạn là Tech TM nhận ticket: làm gì, không được làm gì? | **Chưa lấy dữ liệu**: báo cáo cần **PUMI được duyệt** (subsidiary tạo, đính Jira) rồi mới tới PC ticket; comment mẫu "Production data can only be provided with an approved PUMI. Please raise the PUMI, attach the approval to this ticket, and we will proceed with the approval process." (mục 3.2.1). Danh sách email khách là PII: chỉ ngoại lệ (audit) theo quy trình riêng; **không bao giờ gửi PII qua email từ Hybris**; xin email để gửi EDM thì mặc định từ chối. Có PUMI rồi: staging nếu script mới, tự QA, another set of eyes khi cần, Oliver duyệt, chạy có dòng bắt buộc. Query chỉ đọc điều tra không cần PC nhưng ghi lý do |
| 20 | Ca chiều chỉ có bạn (chứng nhận L1 cho TEC-EPP-03) và một TM khác cũng L1. Bạn chuẩn bị ImpEx access code hàng loạt (file mới) và muốn nhờ người L1 kia kiểm để gửi PC kịp trong ca. Làm vậy có đúng không? | **Không đúng**: người kiểm phải giữ chứng nhận **L2 hoặc L3** của đúng service; người L1 không kiểm cho ai (mục 4.4). Nhờ TM tuần Level 2, Sub-Lead hoặc Tech Lead giữ chứng nhận đó kiểm file và kết quả staging (ImpEx mới nên staging bắt buộc). Chưa tìm được người kiểm thì **chưa gửi PC**. Chạy trên production là việc của Level 2 hoặc on-call được giao, sau khi PC đã duyệt (mục 2.7) |

---

# PHẦN III. MERCHANDISING TEAM (MR)

## MR-01 Merchandising Operating Manual

### A. Câu hỏi kiểm tra (quiz nền tảng Merch T3, ôn trước T4)
**Trắc nghiệm (1–10)**
| # | Câu hỏi | Đáp án | Giải thích ngắn (mục) |
|---|---|---|---|
| 1 | Ticket xin 2 promotion, không ảnh hưởng bảo mật, không rủi ro >10.000 USD: priority? | **(b) Medium** | 1 hoặc 2 promotion là Medium (6.2) |
| 2 | Backup PIC thị trường ID? | **(b) Sub-Lead 2** | Sub-Lead 2 giữ span TH, ID (4.3) |
| 3 | Tech counterpart của NZ? | **(a) Tech Team A** | Team A: VN, TH, ID, NZ (4.4) |
| 4 | Ca tối T2–T6 Merch có? | **(b) Shift Leader + 4** | Gồm TM tiếng Thái và Bahasa (3.1) |
| 5 | Go-live 00:00 giờ Singapore là mấy giờ VN, ca nào kiểm? | **(b) 23:00 hôm trước, ca tối** | UTC+8 (4.5) |
| 6 | Ở 85% thời gian SLA ai hành động, trong bao lâu? | **(b)** Merch Lead (on-call ngoài giờ), 30 phút | 6.6 |
| 7 | Ngưỡng E4? | **(b)** ≥10.000 USD, hoặc >5 thị trường, hoặc file giá ≥500 SKU | 7.2 |
| 8 | Ai bác quyết định trả về của QA? | **(c) COE Lead**, và phải báo RHQ | 2.2, 9.2 |
| 9 | Mục tiêu CSAT trong proposal? | **(b)** ≥4,3/5 từ quý 2/2027, tỷ lệ phản hồi ≥20% | Cam kết proposal (8.2) |
| 10 | Initial response ticket Merch đo đến khi nào? | **(b)** CoE chuyển APPROVED-ES → STG SETUP | Chuyển trạng thái = xác nhận đã nhận; comment không đủ (6.3) |

**Đúng/Sai (11–15)**
| # | Phát biểu | Đáp án | Giải thích |
|---|---|---|---|
| 11 | Merch ở ON HOLD COE chờ COEC của Tech thì đồng hồ SLA Merch dừng | **Sai** | ON HOLD COE vẫn tính SLA; Tech mất 5 ngày thì Merch cũng trễ 5 ngày; người tạo COEC đôn đốc (6.4, 7.4) |
| 12 | Doer có thể tự làm người thứ hai kiểm sau thay đổi R3 nếu ca đêm chỉ có hai người | **Sai** | Doer, Checker, Approver và người kiểm sau thay đổi phải là người khác; Shift Leader hoặc người được giao kiểm (2.5) |
| 13 | Market Owner phải nhận làm owner mọi ticket tồn của thị trường mình trước 08:30 | **Đúng** | Morning pickup 08:00, owner mới có tên trước 08:30 (5.4) |
| 14 | STG SETUP nghĩa là Merch thiết lập trên staging | **Sai** | Thiết lập trên production; publish sang simulator, test bằng promotion simulator Back Office 2.0, đến giờ thì publish live (6.3, 6.4) |
| 15 | Hỏi subsidiary chỉ cần chuyển ON HOLD SUBS là đủ | **Sai** | Phải đủ 3 bước: câu hỏi trong comment, ON HOLD SUBS, giao ticket (Assignee) cho subsidiary; không chuyển chỉ để dừng đồng hồ (6.4) |

**Tình huống (16–20)**
| # | Tình huống | Đáp án | Giải thích |
|---|---|---|---|
| 16 | Medium vào STG SETUP 10:00 T2, go-live T5. 11:00 hỏi subsidiary (ON HOLD SUBS), 15:00 trả lời, chuyển lại STG SETUP. Hạn SLA mới và due date nội bộ? | **06:00 T3** | Đã dùng 1h (10–11h), còn 15h; 15:00 + 15h = 06:00 T3. Due date nội bộ cũng 06:00 T3 vì sớm hơn go-live T5 trừ thời gian kiểm (6.5) |
| 17 | TM bị QA trả về lần thứ hai trong tháng | Mức L1 people-risk | Kèm cặp, giảm WIP một nửa, chứng nhận lại trong 5 ngày làm việc (7.2) |
| 18 | 01:00 T4, Shift Leader cần Merch Lead on-call quyết một thay đổi E4, gọi 15' không được | Gọi SDM hotline | Bậc trên không trả lời trong 15' thì gọi bậc kế tiếp; không tự duyệt E4; ghi giờ gọi (9.1) |
| 19 | Subsidiary cần 500.000 mã coupon cho promotion, cần ImpEx: các bước của Merch PIC, đồng hồ hai ticket? | Giữ ticket, tạo COEC liên kết | Không chuyển ticket sang COEC; tạo COEC ghi rõ việc cần + issue link, ON HOLD COE + comment; hai SLA chạy song song, ON HOLD COE vẫn tính; COEC chờ PC ở ON HOLD HQ thì chỉ đồng hồ Tech dừng; phần ImpEx của Tech cần PC (7.4, A.15) |
| 20 | Ticket giá/promotion tạo 18:00 cần live 00:00 cùng ngày, QA không kịp: comment gì, kiểm soát nào vẫn phải làm (kể cả Knox), ghi nhận thế nào? | Comment last-minute | "Last minute request, please QA on your own when it goes live. If any issue, please contact us."; Shift Leader quyết; kiểm soát tối thiểu R3 (Internal check, price sanity, Shift Leader duyệt, người thứ hai kiểm trên production); **vẫn gửi Knox approval**; gắn label LastMinRequest để đếm báo họp tuần RHQ (6.8, 6.10, A.16) |

### B. Case book Merchandising (13 case, giả lập – bài T4, coaching)
Mỗi case chấm 100 điểm (đạt ≥80 và không lỗi nghiêm trọng); T4 chính thức theo CM-11 (FPY ≥90%). Lỗi nghiêm trọng: sai giá/giá trị khuyến mại; sai thị trường/site/kênh; sai thời gian/múi giờ; tự duyệt việc của mình hoặc bỏ QA với R3 khi không phải yêu cầu gấp; chuyển ON HOLD SUBS chỉ để dừng đồng hồ; **publish giá/promotion khi chưa gửi Knox approval**; đưa dữ liệu ra ngoài hệ thống Samsung/dùng AI với dữ liệu ticket. Thang chấm chung: phân loại 20, giao tiếp 20, thực hiện 30, bằng chứng và ticket 15, kiểm soát (Doer–Checker–Approver, QA, Knox, rollback) 15.

| Case | Bối cảnh và câu hỏi | Đáp án mẫu (ý chính) |
|---|---|---|
| **C01** BMSM, đường chuẩn (T4) | `DEMO-1101` AU, APPROVED-ES T4 09:50, STG SETUP 10:00: BMSM 12 phụ kiện (mua 2 giảm 10%, từ 3 giảm 15%), B2C, 00:00 T6 4/12 – 23:59 CN 6/12 giờ Sydney, brief đủ 12 trường + cột approval path, ~3.000 USD. Hỏi: phân loại; hạn SLA/due date + ca; Internal check ghi gì, có hỏi requester không; bước replay; go-live ai làm gì | Promotion Setup, **1 promotion Medium 16h**, R3, QA gate, không E4; initial response 10'. Hạn SLA 02:00 T5 3/12; go-live 00:00 T6 Sydney (UTC+11) = 20:00 T5 giờ VN; AU Market Owner làm ca ngày T4, ca tối T5 kiểm go-live. **Không hỏi requester** vì brief đủ; ghi \"Internal check: 12 SKUs …; BMSM 2 items 10%, 3+ items 15%; B2C; AU; 04/12 00:00 to 06/12 23:59 AEDT; no stacking with coupon; no usage limit. Matches approved brief v1.\" Replay: STG SETUP → phản hồi đầu 4 ý → internal check → dựng, publish simulator → price sanity → test simulator giỏ 2 và 3 món → rollback step → QA REVIEW → PRD SETUP + **gửi Knox theo approval path** + Shift Leader duyệt → REVIEW SETUP → sub-task go-live check. 23:59 chưa phản hồi và Knox xong: publish as aligned + comment, PENDING LAUNCH; Knox chưa duyệt thì không publish, báo Merch Lead. Go-live 20:00: kiểm production, người thứ hai kiểm 30' (storefront + test order), monitor 15'/2h, LAUNCH VERIFICATION |
| **C02** Special price hai đợt | `DEMO-1102` PH: 3 TV list 29.990 PHP; đợt 1 24.990 (1–7/12), đợt 2 26.990 (8–14/12); riêng SKU 2003 đợt 2 ghi **32.990**; brief không ghi múi giờ. Hỏi: priority/rủi ro; số dòng + ranh giới; phát hiện gì; múi giờ | Special price = Low 24h, R3, QA đầy đủ. **6 dòng** (3 SKU × 2 đợt), không chồng không hở (đợt 1 hết 23:59:59 7/12, đợt 2 từ 00:00:00 8/12). 32.990 > list price: không tự sửa — MỘT câu hỏi gộp (cùng câu múi giờ), ON HOLD SUBS, giao requester; trả lời thì về STG SETUP dựng đủ 6 dòng. Giả định giờ PH (UTC+8) ghi trong Internal check; brief không ghi múi giờ là brief thiếu. 00:00 Manila = 23:00 hôm trước giờ VN → ca tối làm go-live check; sau đợt 1 kiểm production rồi về PENDING LAUNCH, xong đợt 2 mới LAUNCH VERIFICATION |
| **C03** Hard bundle + cộng dồn | `DEMO-1103` NZ: tạo F-Code `DEMO-FCODE-01` (điện thoại X1 + ốp + sạc, 1.499 NZD) trong khi site chạy giảm 10%; brief: bundle không nhận thêm 10%; go-live 00:00 T2 giờ NZ | Hai việc: product setup F-Code (R2) + đổi phạm vi promotion đang chạy để loại bundle (R3); đếm 1 promotion → Medium; cấp cao nhất R3, QA đầy đủ. Stacking = nhiều ưu đãi áp cùng lúc: loại bundle khỏi phạm vi promotion 10% theo runbook, test cart: giỏ chỉ bundle = 1.499 NZD; giỏ bundle + sản phẩm khác thì chỉ sản phẩm kia giảm 10%. 00:00 T2 NZ (UTC+13) = 18:00 CN giờ VN → ca tối CN (SL+1) kiểm; ghi handoff từ T6 |
| **C04** File giá 640 SKU | `DEMO-1104` MY, hiệu lực 00:00 15/12 giờ MY; 4 dòng giá 0 + 7 dòng giảm >60%. Hỏi: cổng; xử lý 11 dòng; ai duyệt/kiểm sau; xử lý file ở đâu | R3, **E4** (≥500 SKU): file diff, dry run (staging thật/preview), price sanity cả file, Internal check tóm tắt (số SKU, khoảng thay đổi, ngày hiệu lực), QA đầy đủ, **Knox approval**, rollback step. 11 dòng: một câu hỏi gộp, ON HOLD SUBS giao requester, không upload đến khi có xác nhận bằng văn bản. Shift Leader duyệt (kiểm cả Knox) + Merch Lead/Deputy (E4); 00:00 MY = 23:00 14/12 VN (ca tối): người thứ hai kiểm 30', monitor 15'/2h. File chỉ xử lý trong môi trường làm việc được phép theo CM-10 (gắn Jira Samsung; không máy cá nhân/chat/AI) |
| **C05** Thiếu thông tin | `DEMO-1105` ID (Bahasa), APPROVED-ES T5 14:00, STG SETUP 14:10: flash sale giảm 20% 8 SKU; thiếu giờ kết thúc, múi giờ, cộng dồn coupon, giới hạn/khách. TM mới định hỏi từng câu và để STG SETUP | Medium 16h, hạn dự kiến 06:10 T6. **Một câu hỏi gộp đủ 4 điểm** có gợi ý trả lời, ID Market Owner viết Bahasa + EN note cho RHQ; rồi ON HOLD SUBS và giao requester (để STG SETUP thì đồng hồ chạy oan; không giao thì dashboard báo sai Assignee). Hỏi 14:25, requester trả lời 09:30 T6 chỉ bằng comment, MO chuyển về 09:40: đã dùng 15', còn 15h45 → hạn mới 01:25 T7; 50% lúc 17:25 T6, 85% lúc 23:01 T6. 18:00 T5 chưa trả lời: nhắc comment có mention sau 2h làm việc, bàn giao TM Bahasa ca tối, ghi rủi ro go-live; không dựng bằng giá trị đoán; 3 ngày làm việc không phản hồi thì COE Lead liên hệ |
| **C06** Yêu cầu mơ hồ | `DEMO-1106` VN: \"làm lại trang chủ giống campaign cuối năm ngoái, đẹp hơn, xong trước cuối tuần\", không file thiết kế/danh sách banner/giờ go-live/T&C | AEM CMS trang chủ: Low 24h; R1 nếu chỉ banner không T&C, R2 nếu có T&C; khuyến mại mới thì phần đó R3 và tính lại priority. **Không** tự thiết kế/sáng tác ưu đãi/dùng AI (RFP 3.12). Câu hỏi gộp kèm phạm vi đề xuất: khối cần đổi, ai cấp hình/nội dung, có T&C không, có trang ưu đãi đích không, giờ go-live cụ thể, \"trước cuối tuần\" là mấy giờ; tiếng Việt + EN note; ON HOLD SUBS giao requester. Khi có trả lời: ghi Internal check phạm vi đã chốt (danh sách) rồi mới làm; requester thêm khuyến mại là yêu cầu khác → báo Shift Leader (MR-04 ch.5), không tách ticket chỉ để đặt lại đồng hồ |
| **C07** Đổi giờ go-live | `DEMO-1107` SG: 15% cho 5 SKU, đã QA PASS + duyệt, go-live 00:00 T7 SGT (23:00 T6 VN); T6 15:30 requester xin live **18:00 SGT** hôm nay (không trong freeze) | 18:00 SGT = 17:00 VN, còn 1h30, đúng cut-off QA. **Có**: giờ hiệu lực là giá trị trọng yếu R3 → quay lại thiết lập, sửa theo giờ mới, ghi Internal check giờ mới, QA kiểm lại phần đổi, Shift Leader duyệt lại, **gửi lại Knox cho giờ mới** (đổi giờ bắt đầu = đổi DATE). Market Owner báo Shift Leader ngay, đưa vào QA REVIEW; QA không kịp thì Shift Leader đề nghị giờ muộn hơn (vd 19:00 SGT) hoặc giữ giờ cũ; nếu subsidiary vẫn cần 18:00 → quy tắc yêu cầu gấp (comment mẫu, kiểm soát tối thiểu, Knox vẫn gửi, đếm). Ca đang trực lúc go-live mới kiểm (ca ngày nếu trước 16:00 VN, tối nếu sau); cập nhật sub-task |
| **C08** Sai giá phát hiện sau live | `DEMO-1108` VN: special price tủ lạnh brief 19.990.000 VND nhưng storefront 1.990.000 VND lúc 00:25 (người thứ hai kiểm), 7 đơn; ca đêm SL + 1 TM | Sự cố sai giá (High). Shift Leader xác nhận ảnh hưởng ≤15', làm **IM tạm thời**, gọi Merch Lead on-call (có mặt 60'). 30' đầu: tắt/rollback special price theo rollback step, kiểm lại storefront, **báo RHQ (Mattermost) + subsidiary (comment) trong 30'**, ghi timeline. **Không tự hủy 7 đơn** (quyết định của subsidiary/RHQ cùng Tech; chỉ lập danh sách); Tech cần ImpEx/Groovy thì vẫn cần PC do Oliver duyệt (P0/P1 nhắn Oliver). Sau đó: định lượng đơn trong 24h, RCA 48h (≤72h) trả lời \"vì sao các lớp kiểm tra không chặn được\", CAPA có owner/ngày, sửa checklist ≤3 ngày làm việc, chứng nhận lại. RCA ghi nguồn sai; trách nhiệm theo điều tra chung RHQ (RFP 3.10); CoE vẫn rollback ngay bất kể ai sai (chờ RHQ: brief sai + internal check khớp brief) |
| **C09** Nội dung tiếng Thái | A: T5 21:30 `DEMO-1109` TH tiếng Thái, text + flag 15 SKU, go-live 09:00 T6 Bangkok, TM Thái ở ca tối. B: đến 20:00 T7. C: T7 10:00 ticket ID Bahasa | A: TM tiếng Thái nhận, trả lời tiếng Thái + EN note; R1 Low; sao chép nguyên văn từ brief; Shift Leader kiểm cấu trúc (SKU, trường, flag) và đối chiếu chuỗi ký tự; 09:00 Bangkok = 09:00 VN: TH Market Owner làm go-live check ca ngày. B: hạn Low 20:00 CN → người nói tiếng Thái on-call CN vào trung tâm; Shift Leader chuyển STG SETUP + phản hồi đầu (tiếng Anh) nêu giờ; High thì gọi người Thái vào ngay. C: trả lời bằng **tiếng Anh**. **Không** dùng công cụ dịch/AI công cộng (CM-10). Ticket Low nhập Bahasa không có người ca: chờ Merch Lead chốt |
| **C10** Coupon QA FAIL rồi đổi sau live | `DEMO-1110` MY: coupon đổi ưu đãi (RFP: Redemption eVoucher), 1 lần/khách, tổng 500, 1–31/12; QA FAIL lần 1 (giới hạn/khách \"không giới hạn\"), sửa → PASS → live. 4/12 requester xin tăng 800 và loại `DEMO-SKU-4005` | QA trả về STG SETUP kèm root cause code, giữ priority, đồng hồ chạy liên tục; đây là 1 lần QA trả về trong tháng (lần 2 cùng tháng = mức L1 people-risk). Yêu cầu 4/12 là **yêu cầu mới** (kết quả cũ đúng brief): đề nghị subsidiary tạo ticket Shop Merchandising mới qua PLANNING REVIEW/APPROVED-ES rồi liên kết; không tự tạo thay subsidiary. Coupon R3: Internal check hai giá trị mới → sửa theo runbook → QA REVIEW → Shift Leader duyệt → **gửi lại Knox** (loại một SKU = đổi CONDITION của promotion đã publish) → kiểm 30' + monitor 2h; sửa đối tượng đang live rủi ro hơn tạo mới. Chờ RHQ: cách xử lý yêu cầu sửa trên ticket đã xong (tạm: ticket mới có link; Merch Lead hỏi RHQ) |
| **C11** Ticket phụ thuộc | T2 09:00 PH: `DEMO-1111` (Low) text 5 SKU mới nhưng SKU chưa có vì `DEMO-1112` (product setup) đang ON HOLD SUBS chờ ảnh; TM mới muốn chuyển 1111 sang ON HOLD SUBS \"cho đồng bộ\" | Không dựng text cho SKU chưa tồn tại; **không** chuyển ON HOLD SUBS (không có câu hỏi nào cho subsidiary → sai quy tắc RHQ). 1111 ở STG SETUP (hoặc ON HOLD COE nếu cần thống nhất nội bộ): đồng hồ vẫn chạy, hạn 09:00 T3. Liên kết issue link (1111 bị chặn bởi 1112), ghi next action, chuẩn bị sẵn nội dung. Báo PH Market Owner + Shift Leader: gộp về một owner/ưu tiên 1112 khi có ảnh; comment cho requester; chạm 70% thì Shift Leader rà cả hai ticket |
| **C12** Coupon hàng loạt cần ImpEx | T3 09:00 `DEMO-1113` MY: 500.000 mã coupon một lần (multi-code) cho campaign cuối năm gắn luật giảm 5%; go-live 00:00 T2 tuần sau giờ MY; giao diện không làm được; TM mới định chuyển sang COEC | Với subsidiary coupon là promotion → ticket thuộc Merchandising, **không chuyển COEC** (Merch còn phải làm). STG SETUP (initial response) → tạo COEC mới `DEMO-1114` ghi rõ ticket gốc, thị trường, số mã, định dạng, luật, hạn → issue link → `DEMO-1113` ON HOLD COE + comment \"COEC ticket DEMO-1114 created, waiting for Tech support\" → báo requester. Hai SLA song song; ON HOLD COE vẫn tính; Tech làm ImpEx trên staging, tự QA, **PC kèm kết quả staging** (Oliver duyệt duy nhất; vắng thì chờ ~3h, tạo sớm); ticket COEC ở ON HOLD HQ chỉ dừng đồng hồ Tech; ImpEx có dòng PC + COEC gốc. Người tạo COEC đôn đốc (Tech Team B): 70% Shift Leader gọi Sub-Lead Tech B; 85% Merch Lead làm việc với Tech Lead + cập nhật requester; 95% COE Lead báo RHQ. Tech xong → LAUNCH VERIFICATION; Merch PIC kiểm mẫu, 1113 về STG SETUP, hoàn thiện luật + internal check, QA REVIEW (coupon R3), PRD SETUP + Knox, Shift Leader duyệt, REVIEW SETUP, PENDING LAUNCH; go-live 23:00 CN VN ca tối kiểm |
| **C13** Yêu cầu gấp 18:00 → 00:00 | T4 18:00 VN `DEMO-1115`: 1 promotion giảm 15% 6 SKU, go-live 00:00 T5 (6 giờ nữa), brief đủ, ca tối SL + 4 TM, QA ca chiều hết 19:00, ~2.000 USD | Medium 16h, R3, không E4; STG SETUP ngay. **Là yêu cầu gấp** (đến sau cut-off 17:00 cho go-live cùng tối, còn 6h, đúng ví dụ RHQ). Shift Leader quyết áp quy tắc gấp; comment \"Last minute request, please QA on your own when it goes live. If any issue, please contact us.\" + label LastMinRequest. Vẫn: Internal check (giá trị chưa rõ thì MỘT câu gộp), price sanity, Shift Leader duyệt, **Knox approval**, người thứ hai kiểm production lúc go-live; không tự duyệt. 00:00 rơi ca đêm: ca tối bàn giao handoff; ca đêm publish, người thứ hai kiểm 30', monitor 2h, đứng chờ hỗ trợ; đếm cho họp tuần (nhắc subsidiary gửi trước 2–3 ngày làm việc). Nếu ticket đến 10:00 mà CoE xếp chậm, 23:00 QA chưa xong: **không** áp quy tắc gấp (nút thắt phía CoE) — vẫn phải QA, CoE giải trình; Shift Leader báo ngay, gọi QA on-call nếu High |

### C. Bài tập nhóm cho Shift Leader (45 phút)
**A.17 – Tối T6 đông go-live.** T6 16:00, bạn là Shift Leader ca tối (bạn + 4 TM có TM Thái và Bahasa + 1 bench); 15:00 một TM báo ốm. Tối nay 9 go-live: NZ 2, AU 2 (00:00 địa phương), SG 1, MY 1, PH 1, TH 1, VN 1. 16:00 còn 3 thiết lập chưa qua QA (AU, PH, TH). 19:10 có ticket High: promotion PH đang live áp sai cho cả nhóm sản phẩm ngoài phạm vi.
| Yêu cầu | Đáp án mẫu |
|---|---|
| 1. Bảng go-live theo giờ VN, người kiểm go-live và người kiểm sau thay đổi | NZ 18:00; AU 20:00; SG/MY/PH 23:00; TH/VN 00:00 (ca đêm kiểm nhưng ca tối bàn giao) (giờ mùa hè AU, NZ). Mỗi go-live có hai người khác nhau: người kiểm go-live + người thứ hai kiểm sau thay đổi trong 30'; monitor đơn 2h. Không xếp hai go-live R3 cùng giờ cho một người |
| 2. Lấp chỗ người ốm | Đòn bẩy trong quyền Shift Leader: bench trong ca thay ghế; chuyển người giữa thị trường; vẫn thiếu thì đề nghị TM ca ngày kéo dài ca trong giới hạn giờ làm, hoặc gọi on-call/bench khác; báo Merch Lead nếu vượt quyền. Ghi roster ngay |
| 3. 3 thiết lập chưa qua QA | Chuyển sang QA REVIEW trước 17:00 theo thứ tự giờ go-live (AU → PH → TH). Đã nằm trong queue từ trước nên **không phải yêu cầu gấp**: không được bỏ QA. Không kịp cut-off: báo requester ngay bằng comment là rủi ro go-live, đề nghị giờ muộn hơn hoặc thu hẹp phạm vi; nếu trễ do nút thắt phía CoE thì CoE giải trình với subsidiary |
| 4. Ticket High 19:10 | Xác nhận ảnh hưởng trong 15'; nếu là sự cố: làm IM tạm thời, khống chế (tắt hoặc sửa phạm vi promotion theo rollback step), gọi Merch Lead (sau 17:00 là on-call); giao một TM riêng cho sự cố; các go-live khác giữ người đã giao. Báo RHQ (Mattermost) và subsidiary (comment) trong 30' |
| 5. Handoff note ca đêm | Sự cố PH (tình trạng, việc tiếp theo, ai giữ); go-live TH, VN 00:00 với người kiểm; ticket REVIEW SETUP có go-live ngày mai và ai publish lúc 23:59 địa phương nếu chưa có duyệt; go-live đang trong 2h monitor; ticket >70% với next action; ticket QA REVIEW chờ QA ca sớm 04:00; ticket ON HOLD SUBS sai Assignee (phải là 0); thay đổi roster vì người ốm |
Chấm (100đ): bảng go-live đúng giờ VN + đủ hai người (25); đòn bẩy đúng thứ tự/quyền (15); cut-off QA không bỏ bước, phân biệt yêu cầu gấp, có văn bản với requester (20); ticket High (25); handoff đủ mục (15).

**A.18 – Sự cố promotion 02:00 CN.** CN 02:10, ca đêm có bạn (Shift Leader) + 1 TM. Order anomaly monitor: từ 00:00 khách VN, TH, ID không thanh toán được giỏ hàng có bundle `DEMO-FCODE-07` sau khi promotion mới go-live 00:00 địa phương. Đơn không bundle vẫn đặt được. Tech chỉ có on-call; Merch Lead on-call.
| Yêu cầu | Đáp án mẫu |
|---|---|
| 1. Phân loại, gọi ai | **Cả hai**: nguyên nhân nghi do promotion (Merch), ảnh hưởng không đặt được hàng (Tech có thể xếp P0, ghi trên COEC). Gọi Merch Lead on-call và Tech on-call lớp 1 ngay; Shift Leader làm IM tạm thời đến khi on-call có mặt. Tech phải đổi dữ liệu/ImpEx/Groovy để khôi phục thì vẫn cần PC, on-call nhắn Oliver qua Mattermost |
| 2. Timeline 60' đầu theo I1–I9 | 02:10 phát hiện; trong 30' (ngoài giờ) phân loại xong; 02:15 gọi Merch Lead và Tech on-call; trước 02:40 thông báo ban đầu RHQ nếu Critical (30'), chậm nhất 2h nếu High; 02:25 khống chế bằng tắt promotion theo rollback step; 02:35 xác minh test order có bundle thanh toán được; cập nhật mỗi 30' (Critical) hoặc 2h (High) |
| 3. Khống chế | Khống chế trước phân tích: tắt promotion trên **cả ba thị trường** cùng lúc (cùng nguyên nhân, đang chặn thanh toán). IM (Shift Leader tạm thời, rồi Merch Lead) quyết và báo RHQ trên bridge |
| 4. Thông báo ban đầu RHQ (≤8 dòng) | "[INCIDENT] Checkout failure with bundle DEMO-FCODE-07 in VN, TH, ID since 00:00 local. Impact: customers cannot pay for carts with the bundle; other orders OK. Suspected cause: new promotion live at 00:00. Action: promotion disabled 02:25 ICT, checkout verified 02:35 ICT. Next update: 03:05 ICT. Incident Manager: Merchandising Shift Leader (acting)." |
| 5. Sau khôi phục | Định lượng đơn bị ảnh hưởng trong 24h cùng Tech; RCA mục tiêu 48h, chậm nhất 72h (gồm vì sao QA và test cart không phát hiện); CAPA có owner và ngày; checklist trong 3 ngày làm việc; người liên quan chứng nhận lại; loss register nếu có tổn thất |
Chấm (100đ): phân loại hai trụ + gọi đúng thứ tự (20); timeline (25); khống chế trước phân tích, đúng người quyết (20); thông báo tiếng Anh (20); việc sau khôi phục (15).

---

## MR-02 Shift Leader Playbook

Câu hỏi dùng cho chứng nhận Shift Leader và deputy Shift Leader (CM-11).

| # | Câu hỏi | Đáp án | Giải thích ngắn (mục) |
|---|---|---|---|
| 1 | Ba vai của Shift Leader trong ca? | **Leadership on duty** (lãnh đạo trực, đầu mối của CoE); **SLA Controller** (canh đồng hồ, bảo đảm trạng thái Jira đúng thực tế); **Approver** (duyệt mọi thay đổi Merch trước production; không duyệt thay đổi Tech) | 1.1 |
| 2 | Absent-assignee filter chạy bao lâu, mục tiêu? | **(b)** mỗi 30 phút; không ticket nào không owner quá 1 giờ | 3.2 |
| 3 | Ticket High được subsidiary duyệt lúc 13:00, không qua trạng thái dừng: mốc 70% và 85% lúc mấy giờ? Làm gì? | 70% lúc **15:48**: giao lại, thêm người, huy động, đôn đốc Tech nếu chờ COEC, trong 15'. 85% lúc **16:24**: gọi Merch Lead (sau 17:00 là on-call), Lead quyết trong 30'; nên báo luôn SDM vì 95% đến lúc 16:48. Nếu ticket từng ở trạng thái dừng (ON HOLD SUBS, ON HOLD RHQ, REVIEW SETUP) thì các mốc lùi đúng bằng thời gian dừng | 3.3 |
| 4 | Thời hạn duyệt thay đổi của Shift Leader? | **(a)** 15' cho High, 30' cho ticket khác | 4.1 |
| 5 | Promotion cho 6 thị trường, giá trị ảnh hưởng ước tính 4.000 USD: có gọi Merch Lead duyệt thêm? | **Có**: E4 khi đạt một trong ba điều kiện; >5 thị trường là đủ, dù giá trị <10.000 USD | 4.4 |
| 6 | Ticket R3 đã QA PASS 15:00; 17:30 Doer sửa ngày kết thúc theo yêu cầu mới của requester. Duyệt ngay được không? | **Không**: ticket đã sửa sau QA PASS phải được QA kiểm lại; Doer cập nhật dòng Internal check cho khớp brief đã duyệt (yêu cầu đổi ngày phải nằm trong brief đã duyệt lại; nếu promotion đã publish thì đổi NGÀY phải duyệt Knox lại) | 4.3, 4.10 |
| 7 | 22:00 dashboard COEC NEW có ticket P3. Ai chuyển nó sang ASSIGNED, và bạn làm gì? | Tech đang trực (**on-call lớp 1**, TC-04) quét COEC NEW mỗi 5' và chuyển ASSIGNED; ticket của Tech do Tech Team chịu trách nhiệm, không đẩy sang Shift Leader. Bạn **không chuyển ASSIGNED, không xử lý ticket P3**; chỉ khi thấy P0/P1 thì gọi on-call lớp 1 ngay; cuộc gọi on-call (nếu có) ghi vào handoff note cho Tech L1 ca 04:00. Còn chờ: cách đạt/đo initial response 2h ngoài giờ | 5.2 |
| 8 | 21:00 RHQ gọi báo khách không thanh toán được: năm việc đầu theo thứ tự? | Tạo COEC P0 trong 5'; kiểm storefront xác nhận tác động; gọi on-call lớp 1 ngay; mở bridge trong 15' và ghi timeline; gửi thông báo ban đầu (Critical 30') theo chỉ đạo của lớp 1 và báo SDM | 6.2, 6.4 |
| 9 | On-call lớp 1 không trả lời: chuỗi gọi theo phút? | Phút 0 gọi lớp 1 (hai lần trong 10'); phút 10 lớp 2; phút 15 Tech Lead (hoặc Sub-Lead A); phút 20 SDM hotline; ghi vi phạm quy trình | 5.2 |
| 10 | BVT notification đến 20:00 T6 | **(b)** ghi handoff (mục 9) và nhắn Merch Lead + Tech Lead để chỉ định PIC trong ngày làm việc kế tiếp | Không gọi QA on-call (QA không tham gia BVT); ngày BVT không thương lượng (5.3) |
| 11 | Vì sao IM on-call không tự gửi thông báo cho RHQ từ nhà? | Không làm remote: ngoài trung tâm on-call chỉ nghe và hướng dẫn; mọi việc trên hệ thống Samsung, kể cả email và kênh sự cố, làm tại trung tâm. Shift Leader gửi theo chỉ đạo đến khi on-call có mặt | 6.4 |
| 12 | Ba TM báo ốm trước ca ngày T2: việc theo giờ 0, 1, 2? | Giờ 0: giao lại ticket cho backup có tên, kiểm quân số, báo Lead. Giờ 1: gọi bench, mời người ca sau đến sớm trong giới hạn. Giờ 2: dời ticket Low sang ca sau kèm cập nhật requester, báo MO; Lead xác nhận phương án launch với RHQ. Ghi log | 7.5 |
| 13 | Bốn lớp dự phòng và ai quyết mở? | Cân bằng tải; bench; surge từ đội BiPlus Samsung khác (tối đa 2 tuần, RHQ duyệt); thời gian làm việc. Merch Lead và COE Lead quyết | 7.3 |
| 14 | 23:50 ticket High đạt 85% đang sửa dở. Bàn giao cho ca đêm lúc 00:00 không? | **Không** bàn giao giữa chừng: người đang làm và bạn ở lại đến khi xong (trong giới hạn làm thêm giờ), gọi Lead ở 85% và báo SDM; handoff ghi "ca tối giữ đến khi xong" | 3.5, 8.3 |
| 15 | Người mới gửi nháp "We will fix it asap": sửa theo tiêu chí nào? | Đúng kênh; cấu trúc chào – nêu lại yêu cầu – việc tiếp và giờ (ICT + giờ địa phương) – cần gì từ requester; tiếng Anh rõ, lịch sự; không hứa vượt SLA; không đưa dữ liệu ra ngoài kênh Samsung | 9.3 |
| 16 | Dẫn ca đêm và phải tự làm một thay đổi R3: ai duyệt? Điểm chờ chốt? | Không tự duyệt. Người duyệt thay khi Shift Leader là Doer đang chờ Merch Lead chốt (đề xuất: Merch Lead hoặc Deputy Lead có mặt tại trung tâm) | 4.6 |
| 17 | 23:30 promotion go-live 00:00 ngày mai, đã QA PASS, bạn đã duyệt và Knox approval đã duyệt, nhưng subsidiary chưa duyệt ở REVIEW SETUP và không có comment. Nếu Knox chưa duyệt thì khác thế nào? | Bạn (Shift Leader ca tối) quyết publish như đã thống nhất; owner publish và comment trước 23:59: "Published as agreed. We have not received your feedback on the QA evidence yet." Ghi handoff 00:00 để ca đêm kiểm go-live. **Nếu Knox chưa duyệt: không publish, báo Merch Lead** (tạm thời, chờ RHQ xác nhận) | 4.8, 4.10 |
| 18 | 18:00 subsidiary tạo ticket R3 cần live 00:00 cùng đêm; QA không kịp | Nhận diện yêu cầu gấp; vẫn giữ kiểm soát tối thiểu R3 (internal check, price sanity, bạn duyệt, người thứ hai kiểm production lúc go-live); **gửi Knox approval theo approval path trong brief**; comment "Last minute request, please QA on your own when it goes live. If any issue, please contact us."; gắn nhãn `LastMinRequest`; ghi mục 8 handoff; đứng chờ hỗ trợ lúc go-live | 4.9 |
| 19 | Vòng 30 phút: ON HOLD SUBS có Assignee CoE; comment cuối là câu hỏi của CoE lúc 14:00 | CoE quên giao ticket cho subsidiary khi hỏi → subsidiary có thể không biết đang được hỏi. Giao Assignee cho subsidiary (người tạo ticket), kiểm câu hỏi đã nằm trong comment. Nếu comment cuối là câu trả lời của subsidiary thì chuyển ngay về STG SETUP | 3.2.3 |
| 20 | 22:30 on-call Tech cần sửa cấu hình Back Office để khôi phục P0 và hỏi bạn duyệt. Bạn trả lời thế nào, và nếu on-call vẫn làm khi chưa có PC được duyệt thì hậu quả gì? | Bạn **không duyệt thay đổi Tech**. Thay đổi production cần PC do Oliver Leung duyệt (duy nhất, không người duyệt thay; vắng vẫn chờ); vì P0, on-call lập PC, COEC gốc → ON HOLD HQ "PC ticket pending", nhắn Oliver qua Mattermost. Làm khi chưa có PC duyệt là một trong ba việc **chắc chắn dẫn tới strike** (RHQ quyết định). Bạn ghi PC đang chờ vào handoff | 1.4, 5.2, 6.1, 9.4 |

---

## MR-03 Market Owner Playbook

### A. Trắc nghiệm (1–8)
| # | Câu hỏi | Đáp án | Giải thích ngắn (mục) |
|---|---|---|---|
| 1 | Market Owner làm ca nào? | **(a)** ca ngày 08:00–16:00 T2–T6 | 1.1 |
| 2 | Backup PIC của MY? | **(b) Sub-Lead 3** | Sub-Lead 3 giữ span MY, SG (1.4) |
| 3 | Ai là PIC chính của nhóm kênh EPP, SMB, O2O, và ai phụ trách 3PD? (a Merch Lead cho cả hai; b Sub-Lead 4 cho EPP/SMB/O2O, 3PD do PIC 3PD chuyên trách ở Tech Team; c MY Market Owner cho cả hai) | **(b)** | Sub-Lead 4 giữ EPP, SMB, O2O (backup Merch Lead); 3PD do PIC 3PD chuyên trách ở Tech Team, backup là Tech TM đã chứng nhận 3PD (1.4) |
| 4 | Owner mới của mọi ticket tồn phải có tên trước? | **(b) 08:30** | Morning pickup (7.2) |
| 5 | Ai trả lời đầu tiên một khiếu nại viết của subsidiary, trong bao lâu? | **(b)** COE Lead, 1 ngày làm việc | SDM điều tra 3 ngày; đóng 10 ngày (3.5) |
| 6 | Mục tiêu CSAT trong proposal? | **(b)** ≥4,3 từ quý 2/2027, phản hồi ≥20% | 3.4 |
| 7 | Cần hỏi subsidiary, việc đúng? | **(b)** comment câu hỏi, ON HOLD SUBS và giao ticket cho subsidiary | Đủ 3 bước; ON HOLD COE vẫn tính SLA và không dùng để chờ subsidiary (2.5) |
| 8 | Kênh trao đổi với subsidiary hiện nay? | **(c)** comment Jira, cho đến khi RHQ chốt kênh chat | RHQ đang kiểm tra kênh chat (6.1) |

### B. Tình huống (12 câu; đáp án đánh số 9–20 trong bảng gốc)
| # | Tình huống | Đáp án mẫu (mục) |
|---|---|---|
| 1 | 08:30 có 3 ticket: A Low R3 hạn 18:00 hôm nay; B Medium R3 vào STG SETUP 08:20, brief thiếu múi giờ kết thúc nên phải hỏi subsidiary, hạn 00:20 ngày mai; C Low R1 hạn 22:00. Thứ tự? | **B, A, C**: gửi MỘT câu hỏi gộp cho B trước (vài phút, comment, ON HOLD SUBS, giao requester); làm A theo hạn SLA, R3 cần vào QA REVIEW trước khoảng 15:00; C là R1 ngắn, làm xen khi chờ QA (2.3, 2.5) |
| 2 | Requester TH viết bằng tiếng Thái lúc 10:00. Trả lời thế nào để RHQ cũng hiểu? | Trả lời tiếng Thái, **kèm EN note** 1–3 câu: yêu cầu, trả lời, bước tiếp theo (6.2, 6.5) |
| 3 | Weekly sync: subsidiary nói từ tháng sau mọi promotion kết thúc 23:59:59 thay vì 23:59. Làm gì sau họp? | **Cập nhật market rules page**: sửa mục quy tắc promotion, ghi nguồn sync, lịch sử thay đổi, Sub-Lead rà soát, báo các ca qua handoff; nếu runbook bị ảnh hưởng thì báo Process and Knowledge Lead (4.5) |
| 4 | Nghỉ phép 5 ngày làm việc tuần sau: các bước? | Vắng có kế hoạch: xin nghỉ, backup xác nhận trên roster, ghi lịch nghỉ trên trang CoE; brief; biên bản bàn giao viết (>3 ngày làm việc); báo subsidiary bằng comment hoặc weekly sync; chuyển Assignee (8.3) |
| 5 | TH Market Owner ốm đột xuất T3: ai làm PIC tạm, ca tối ai phủ tiếng Thái? | **TM tiếng Thái** chuyển lên ca ngày làm PIC tạm; bench tiếng Thái phủ ca tối; Sub-Lead 2 là backup PIC có tên (8.2) |
| 6 | Ticket ca đêm của thị trường bạn đã dùng 75% SLA lúc 08:05 | **Báo Shift Leader ngay**: đã qua 70%, nhận owner, ghi next action, không chờ stand-up (7.2) |
| 7 | Introduction call 4/11, subsidiary hỏi: "Can you guarantee all our tickets will be done in 4 hours from now?" | **Không hứa ngoài SLA**: giải thích SLA theo priority (High 4h, Medium 16h, Low 24h), tính trên thời gian ticket ở phía CoE; trong tháng 11 SDSAP vẫn vận hành phần lớn; ghi câu hỏi vào ghi chú cho Merch Lead (A.3) |
| 8 | 10:00 subsidiary comment "Confirmed" trên ticket ON HOLD SUBS nhưng không đổi trạng thái, không giao lại | **Chuyển về STG SETUP ngay**, đổi Assignee về bạn, comment đã nhận, tính lại hạn SLA và due date. Không chuyển thì đồng hồ dừng sai thực tế, không ai làm, go-live trễ (2.5) |
| 9 | Promotion go-live 00:00 T6 giờ địa phương; ticket ở REVIEW SETUP từ T3, subsidiary chưa duyệt. Chiều T5 làm gì? | Chuẩn bị publish 23:59: ghi vào handoff ai publish; đến 23:59 T5 giờ địa phương chưa có duyệt thì publish như đã thống nhất, comment Mẫu 7, chuyển PENDING LAUNCH; ca trực go-live kiểm lại trên production. Giá/promotion chưa có **Knox approval** thì không publish phần đó, báo Shift Leader và Merch Lead (tạm thời, chờ RHQ) (2.6) |
| 10 | Ticket của thị trường bạn tạo 18:00 cần live 00:00 cùng ngày | **Áp quy tắc yêu cầu gấp**: báo Shift Leader; comment Mẫu 8 ("Last minute request, please QA on your own when it goes live. If any issue, please contact us."), nhãn `LastMinRequest` để đếm; R3 vẫn kiểm tra nội bộ, price sanity, Shift Leader duyệt, **Knox approval**, người thứ hai kiểm lúc go-live; đứng chờ hỗ trợ; nêu ở weekly sync và nhắc gửi promotion sớm (2.7) |
| 11 | Subsidiary muốn đổi một promotion đã publish: (a) đổi tên; (b) đổi ngày kết thúc. Việc nào phải duyệt Knox lại, đường duyệt lấy ở đâu? | **(b)** cần Knox approval lại; (a) không. Đổi ACTION, CONDITION, WEBSITE hoặc ngày của promotion đã publish thì lần publish tiếp theo phải duyệt lại. Đường duyệt lấy ở **cột approval path trong brief**, không tự chọn (2.9) |
| 12 | Trước khi build một promotion R3, bạn phải ghi gì lên ticket? Khi nào được hỏi lại subsidiary? | Ghi **Internal check**: SKU, giá/mức giảm, thời gian kèm múi giờ, site/store, quy tắc stack, giới hạn dùng, kết thúc bằng "Matches approved brief vX"; chạy price sanity rules. Chỉ hỏi subsidiary (MỘT câu hỏi gộp, ON HOLD SUBS, giao ticket) khi brief thiếu/mâu thuẫn hoặc price sanity cảnh báo (2.9) |

---

## MR-04 Quy trình Merchandising chi tiết

### A. Trắc nghiệm (14 câu)
| # | Câu hỏi | Đáp án | Giải thích ngắn (mục) |
|---|---|---|---|
| 1 | STG SETUP trên workflow Shop Merch là gì? | **(b)** CoE đã nhận, đang thiết lập trên production ở trạng thái chưa live | Không phải staging (3.3, 4.4) |
| 2 | Initial response ticket Merch đo thế nào? | **(b)** từ APPROVED-ES đến khi CoE chuyển STG SETUP | Chuyển STG SETUP là xác nhận đã nhận; comment không đủ (3.2) |
| 3 | Trạng thái chờ nào vẫn tính SLA? | **(c) ON HOLD COE** | ON HOLD SUBS, ON HOLD RHQ, REVIEW SETUP dừng (2.1, 4.6) |
| 4 | Cần hỏi subsidiary thông tin còn thiếu: cách đúng? | **(b)** comment, ON HOLD SUBS và giao ticket cho subsidiary | 2.1 |
| 5 | Ticket ON HOLD SUBS mà Assignee là người CoE nghĩa là gì? | **(b)** CoE quên giao hoặc subsidiary đã trả lời: kiểm ngay, đã trả lời thì về STG SETUP | Đồng hồ có thể đang dừng sai thực tế (2.1) |
| 6 | Ticket có 3 promotion cùng thị trường: priority? | **(c) Low** | Từ 3 promotion là Low 24h (5.1) |
| 7 | Ticket promotion cho 6 thị trường? | **(b)** là E4, Merch Lead hoặc Deputy duyệt thêm | >5 thị trường là E4 (5.3) |
| 8 | 500.000 mã coupon cần ImpEx: cách đúng? | **(b)** tạo COEC mới, liên kết, Merch sang ON HOLD COE + comment | Không chuyển ticket Merch sang COEC; hai SLA song song (7.5) |
| 9 | Ticket đã INVALID nhưng subsidiary muốn làm lại | **(b) clone ticket** | INVALID không mở lại được (2.2) |
| 10 | Go-live ngày mai, ticket ở REVIEW SETUP, 23:59 hôm nay chưa duyệt (giả sử Knox approval đã có) | **(b)** publish như đã thống nhất và comment đã publish, chưa nhận phản hồi | Quy tắc 23:59 của RHQ (3.7); chưa có Knox approval thì không publish phần giá/promotion đó |
| 11 | Ticket có 2 promotion cùng thị trường, bắt đầu 02/12 và 05/12. Sau đợt 02/12? | **(b)** QA lại trên production thật rồi về PENDING LAUNCH chờ đợt 05/12 | Một ticket nhiều đợt; mỗi đợt QA lại; đợt cuối mới đóng (5.2) |
| 12 | Thay đổi R3 go-live 23:00: kiểm tra người thứ hai phải xong trong? | **(b) 30 phút** | E4: 15'; monitor đơn 2h (3.9) |
| 13 | Phát hiện giá sai trên production lúc QA lại sau go-live | **(b)** xử lý như sự cố: tắt/rollback trong 30' đầu, báo RHQ + subsidiary trong 30' | Sai sau go-live là sự cố theo CM-06 (3.9) |
| 14 | Enhancement đổi màn hình promotion (phạm vi Merch) có cửa sổ BVT: ai làm BVT phía CoE? | **(b)** PIC Merch do Merch Lead chỉ định, QA không tham gia | 7.3 |

### B. Tình huống (6 câu)
| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 15 | Ticket AU vừa vào APPROVED-ES: brief ghi "start midnight", không có ngày kết thúc; go-live trong 10h | (1) Phân loại, giao owner, chuyển STG SETUP ngay (initial response). (2) Ghi giờ go-live dự kiến: "midnight" giờ Sydney = 20:00 giờ VN (giờ mùa hè), phải xác nhận. (3) MỘT câu hỏi gộp trong comment (múi giờ bắt đầu, ngày giờ kết thúc, điểm còn thiếu); ON HOLD SUBS, giao requester, nêu hạn trả lời để kịp go-live. (4) Theo dõi dashboard; subsidiary trả lời thì về STG SETUP ngay, rồi ghi Internal check lên ticket và chạy price sanity trước khi thiết lập. (5) Không đủ thời gian QA: Shift Leader xác định yêu cầu gấp (mục 6.5). **Không tự đoán ngày kết thúc** |
| 16 | 15:50, Market Owner đang thiết lập dở coupon R3 (STG SETUP) go-live 00:00; trước khi rời ca 16:00? | (1) Dừng ở điểm an toàn, thiết lập vẫn chưa live. (2) Comment: đã làm gì, còn gì, rủi ro, go-live 00:00, dòng Internal check đã ghi trên ticket chưa. (3) Ghi ticket vào handoff; Shift Leader ca tối chỉ định owner mới; đổi Assignee trước khi rời ca. (4) Nói trực tiếp owner mới trong 15' chồng ca vì là R3 và go-live trong ca sau. (5) Không chuyển QA REVIEW khi chưa self-check xong |
| 17 | Ticket promotion R3 TH vào APPROVED-ES 18:00, cần live 00:00 cùng đêm | (1) Chuyển STG SETUP để xác nhận đã nhận. (2) Shift Leader xác định yêu cầu gấp (không đủ thời gian QA). (3) Đối chiếu cấu hình với brief đã duyệt, ghi Internal check lên ticket, chạy price sanity; không chờ subsidiary. Chỉ khi brief thiếu hoặc mâu thuẫn mới gửi MỘT câu hỏi gộp, ON HOLD SUBS và giao requester. (4) Comment nguyên văn "Last minute request, please QA on your own when it goes live. If any issue, please contact us." + label `LastMinRequest`. (5) Kiểm soát tối thiểu: Internal check, price sanity, Shift Leader duyệt, người thứ hai kiểm production lúc go-live; bằng chứng self-check ở REVIEW SETUP; quy tắc 23:59. (6) Giá và promotion vẫn phải gửi Knox approval theo approval path trong brief, kể cả yêu cầu gấp. (7) Ca đêm đứng chờ hỗ trợ lúc go-live; Merch Lead đưa vào số liệu họp tuần |
| 18 | Subsidiary gửi ticket Merch xin cấp quyền EPP (domain, email, access code) cho đối tác mới; toàn bộ là cấu hình Tech. Nếu sau đó Merch còn phải thiết lập giá EPP? | Toàn bộ việc thuộc Tech: **move chính ticket sang COEC**, không tạo mới (SLA chỉ theo dõi trên từng ticket); sau đó theo SLA Tech. CoE tự move được, không cần quyền admin; comment "Moved to project as this request is fully handled by the Tech/Merchandising team." (A.11). Nếu Merch còn phải thiết lập giá EPP: giữ ticket Merch, tạo COEC liên kết cho phần quyền EPP, Merch → ON HOLD COE (vẫn tính SLA), đôn đốc Tech; Tech xong thì về STG SETUP và tiếp luồng chuẩn |
| 19 | Ca đêm chỉ có Shift Leader + 1 TM. Thay đổi R3 (không phải yêu cầu gấp, Medium) go-live 06:00. Ai làm, ai kiểm, ai duyệt? | Doer, Checker, Approver phải là ba người: TM có chứng nhận làm Doer; Shift Leader là Approver; Checker là QA. Medium không gọi QA on-call nên thiết lập phải tới QA trong giờ QA (ca sớm từ 04:00, chờ chốt giờ QA) và xong trước 06:00; lập kế hoạch ngược từ giờ go-live. Không bỏ QA vì không phải yêu cầu gấp. QA không kịp vì phía CoE: Shift Leader báo Merch Lead ngay để huy động; trễ thì CoE giải trình với subsidiary (A.9). TM chưa có chứng nhận service đó: không giao; gọi deputy Shift Leader hoặc Merch Lead on-call đến trung tâm (≤60'). Sau go-live, người thứ hai kiểm trong 30': Shift Leader làm vì không phải Doer. Nếu Shift Leader phải làm Doer thì không tự duyệt; người duyệt thay là đề xuất tạm, chờ chốt (Merch Lead hoặc Deputy Lead có mặt tại trung tâm, MR-02 mục 4.6) |
| 20 | Ticket ở REVIEW SETUP, subsidiary comment: "SKU X phải là 15%, không phải 10%." Làm gì, đồng hồ SLA? | (1) Chuyển REVIEW SETUP → STG SETUP; đồng hồ chạy tiếp với ngân sách còn lại (REVIEW SETUP đang dừng). (2) R3 và giá trị đổi: brief gốc ghi 10% mà subsidiary nay nói 15% là mâu thuẫn, nên gửi MỘT câu hỏi gộp ở ON HOLD SUBS (giao ticket cho subsidiary) để có brief cập nhật được duyệt; sau đó ghi lại Internal check theo brief mới (Matches approved brief v2) và chạy lại price sanity. (3) Sửa trên production ở trạng thái chưa live, test lại bằng promotion simulator, self-check. (4) QA REVIEW lại, bằng chứng mới, Shift Leader duyệt, PRD SETUP; mức giảm là ACTION của promotion nên Knox approval phải khớp giá trị mới: đã gửi theo giá trị cũ thì gửi lại theo approval path. Rồi REVIEW SETUP lại. (5) Go-live gần: Shift Leader ưu tiên ticket và báo subsidiary nguy cơ trễ |

---

## MR-05 Danh mục service và chuẩn runbook Merchandising

| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Merch có bao nhiêu service trong catalogue 143, chia bao nhiêu nhóm? | **b** – 58 service, 17 nhóm RFP cộng 2 nhóm bổ sung | Mục 1.1 |
| 2 | Ticket yêu cầu 3 promotion trong một lần: service nào, priority mặc định? | MER-PRM-09 Multi-promotion batch (>2 promotion); **Low (24h)**; R3, QA bắt buộc | Từng promotion làm theo runbook của loại promotion đó |
| 3 | MER-PRC-01 Price upload thuộc cấp rủi ro nào, kiểm soát gì trước khi publish live? | **R3**: internal check (tóm tắt giá trị chính của brief đã duyệt ghi trên ticket trước khi build), price sanity rules, QA bắt buộc, Shift Leader duyệt, Knox approval theo approval path của brief; thêm Merch Lead/Deputy khi đạt E4 (≥10.000 USD, >5 thị trường, ≥500 SKU); bulk >100 dòng có file diff và chạy thử; kiểm sau thay đổi trong 30' | |
| 4 | "QA gate: Lấy mẫu" nghĩa là gì? Còn cần Shift Leader duyệt không? Thời gian QA có nằm trong SLA không? | QA kiểm theo sampling plan thay vì toàn bộ; **Shift Leader vẫn duyệt mọi thay đổi** trước khi publish live. **Có**: Merch và QA dùng chung một SLA, thời gian QA nằm trong SLA ticket Merch | |
| 5 | Kể 6/16 mục bắt buộc của runbook, trong đó có hai mục mới v0.2 | Bất kỳ 6 trong: purpose and scope; when to use; who can do it; preconditions; internal check and sanity; steps; self-check; warnings; evidence; QA evidence required; post-change and go-live check; rollback and safe stop; when Tech is needed; escalation; market notes and templates; change history. **Hai mục mới: QA evidence required, when Tech is needed** (ví dụ trả lời: QA evidence required và when Tech is needed) | |
| 6 | Đ/S: "Giá trị cần điền có trong ảnh minh họa là đủ, không cần ghi bằng chữ." | **Sai** | Giá trị phải ghi bằng chữ trong bước hoặc bảng; ảnh chỉ minh họa và có thể lỗi thời |
| 7 | Cảnh báo trong runbook đặt ở đâu, cấu trúc? | Ngay trước bước có rủi ro, dùng macro Warning: điều gì có thể sai, hậu quả, cách tránh | |
| 8 | Trước khi sửa một thiết lập R3, Doer ghi gì lên ticket để rollback được? | **Before value**: giá trị trước thay đổi (vd giá hiện tại, promotion đang chạy) | |
| 9 | SRL3 nghĩa là gì? Service chuyển sang BiPlus Sprint 2 đạt SRL3 lúc nào? | **Ready**: cách ghi service trên Jira đã thử và có người chứng nhận trên mọi ca cần service; phải đạt trước khi Sprint 2 bắt đầu (09/11) | |
| 10 | Class A phải đạt mức nào tại CP1 và cổng G4 (31/12)? | **SRL3 tại CP1 (31/10); SRL4 tại G4** (4 tuần live đạt mục tiêu) | Phạm vi CP1 thực tế đang chờ SDM thống nhất với RHQ |
| 11 | Service pack có bao nhiêu khối, mấy nhóm? Runbook thuộc nhóm nào? | **12 khối, 4 nhóm** (Define, Know, Do, Check and improve); runbook thuộc nhóm **Do** | |
| 12 | Ticket đang ở QA REVIEW theo internal check 15%, subsidiary comment đổi thành 20% | Không sửa ngay; xác nhận thay đổi nằm trong brief mới đã duyệt (chưa rõ thì MỘT câu hỏi gộp, ON HOLD SUBS, giao subsidiary); mức giảm là ACTION nên cần Knox approval cho giá trị mới theo approval path trong brief; làm lại internal check và price sanity với 20%; sửa rule khi chưa publish live, publish lại sang simulator và test lại, bằng chứng mới, QA kiểm lại, Shift Leader duyệt lại; ghi dòng thời gian trên ticket | |
| 13 | Ai chứng nhận một runbook, khi nào đủ điều kiện? | **Merch Lead** chứng nhận; đủ điều kiện khi đã có **hai người** làm theo thành công | |
| 14 | Runbook mô tả một tab không còn tồn tại sau release | Dừng, không đoán; báo Shift Leader; Sub-Lead kiểm và cập nhật runbook (phiên bản mới, Change history); ticket chờ trong phạm vi SLA nếu cần | |
| 15 | Ticket promotion ở STG SETUP: setup ở đâu, test bằng gì, khi nào publish live? | STG SETUP không phải staging. **Setup trên production**, publish sang môi trường simulator, test bằng promotion simulator Back Office 2.0; publish live đúng giờ go-live sau QA PASS, Shift Leader duyệt và Knox approval; mỗi đợt go-live QA lại trên production thật | Mục 4.2 |
| 16 | Subsidiary gửi cấu hình add-on page có thêm một tab ngoài guide HQ nhưng thiếu một SKU bắt buộc trong tab bắt buộc | Tab thêm được; **thiếu SKU bắt buộc thì không được**. Không setup thiếu: hỏi subsidiary bằng MỘT câu hỏi gộp trong comment, chuyển ON HOLD SUBS và đổi Assignee sang subsidiary; khi đủ thì setup và đối chiếu guide trong self-check | Mục 1.3, 2.6 |
| 17 | Subsidiary cần 500.000 mã coupon: MER-CPN-01 ghi gì, làm gì trên Jira? | MER-CPN-01: "tạo hàng loạt mã coupon cần ticket COEC liên kết (ImpEx)". Giữ ticket Merchandising, tạo ticket COEC ghi rõ cần gì (số mã, prefix, thời hạn, link brief), issue link, ON HOLD COE và comment; SLA Merchandising vẫn chạy, người tạo ticket COEC đôn đốc Tech. Phần Tech đi PC ticket, phần Merchandising không cần | Mục 2.5 |
| 18 | Bằng chứng QA của một promotion giá gồm gì, tạo và lưu ở đâu? | PowerPoint chụp từng bước: rule đã cấu hình, kết quả promotion simulator cho SKU và ngày trong và ngoài phạm vi, PDP và giỏ hàng sau publish live mỗi đợt; phải chứng minh promotion chạy đúng. Tạo trên máy trạm CoE, đính thẳng ticket Jira, xóa bản trên máy, không video | Mục 2.4 |
| 19 | Một promotion đã publish: subsidiary đề nghị đổi tên promotion, và sau đó đổi ngày kết thúc. Trường hợp nào phải duyệt Knox lại, approval path lấy ở đâu? | Đổi ngày kết thúc thì phải duyệt Knox lại trước lần publish tiếp theo (đổi ACTION, CONDITION, WEBSITE hoặc NGÀY đều phải duyệt lại); đổi tên promotion thì không. Approval path lấy từ cột approval path trong campaign brief, không tự chọn; cách gửi do Market Owner ghi trong runbook | Mục 2.9 |
| 20 | Subsidiary tạo ticket xin EPP site mới nhưng chưa đính email phê duyệt. Làm gì, và ai làm phần domain email? | Comment mẫu "New EPP site creation requires RHQ approval. Please seek approval first using the approval template link and attach the approval email to this ticket.", chuyển ON HOLD SUBS và giao subsidiary. Khi có email phê duyệt: chuyển ON HOLD RHQ (đồng hồ dừng), chờ RHQ duyệt, duyệt xong ticket về STG SETUP. Thêm domain email vào EPP access list là việc của Tech trên COEC | Mục 1.3 |

---

## MR-06 Kiểm soát chất lượng và rủi ro thiết lập

Đạt ≥80%; câu 1, 4, 6, 9, 11 và 14 là câu trọng yếu, phải đúng (bộ đề gồm 12 trắc nghiệm + 8 tình huống đánh số 13–20).

### A. Trắc nghiệm (13 câu)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | Thay đổi R3 là E4 khi nào? | **d** – bất kỳ một trong: ≥10.000 USD exposure; >5 thị trường; file giá ≥500 SKU | Một trong ba tiêu chí là đủ (4.1) |
| 2 | Price sanity rules chạy mấy lần trên một thay đổi R3? | **b** – hai lần: Doer trước khi build, QA trước khi PASS | Lần 1 trên brief, lần 2 trên kết quả build (2.1) |
| 3 | Subsidiary trả lời "OK" + ngón tay cái khi Doer hỏi lại giá trị của brief | **b** – chỉ coi là xác nhận khi có trả lời rõ giá trị; "OK" và emoji không đủ, nhắc lại giá trị rồi mới build | Không ai được xác nhận thay subsidiary (3.3) |
| 4 | Ai được bỏ qua (override) QA FAIL? | **c** – COE Lead, có thông báo RHQ | Merch Lead không có quyền này (1.1) |
| 5 | Post-change check của thay đổi E4 phải xong trong bao lâu? | **a – 15 phút** | R3 thường: 30' (4.5, 5.1) |
| 6 | Order anomaly monitor sau go-live R3 chạy thế nào? | **b** – mỗi 15 phút trong 2 giờ | 8 mốc (5.5) |
| 7 | File price upload 160 dòng: kiểm soát bắt buộc thêm so với 40 dòng? | **b** – diff file và dry run | >100 dòng: diff + dry run theo 2.4 (không mặc định staging); duyệt cấp hai chỉ khi ≥500 SKU hoặc tiêu chí E4 khác |
| 8 | FPY tính thế nào? | **b** – số thay đổi có QA gate PASS ở lần kiểm đầu / tổng số thay đổi có QA gate được kiểm lần đầu | Chương 6.1 |
| 9 | Doer, Checker, Approver trên ticket R3 ca đêm chỉ có Shift Leader + 1 TM | **c** – ba vai vẫn phải là ba người khác nhau; QA kiểm ở QA REVIEW trước go-live, hoặc chờ, hoặc gọi QA on-call với ticket High cần QA gate; yêu cầu gấp thì áp mục 1.7 | Ngoại lệ QA chỉ là yêu cầu gấp (1.1, 1.7, 5.7) |
| 10 | Mã root cause nào KHÔNG tính vào lần trả về của Doer? | **c** – RC-BRF khi internal check của Doer khớp brief đã duyệt | Bảng mã 6.5 |
| 11 | STG SETUP nghĩa là gì? | **b** – CoE đã nhận; Merch setup trên production ở trạng thái chưa live, promotion publish sang simulator để test | STG SETUP là tên trạng thái, không phải staging (1.5, 1.6) |
| 12 | Hard freeze flagship, subsidiary xin đổi giá một SKU và nói "RHQ đã đồng ý" | **c** – ngoại lệ phải có phê duyệt: CoE tra trang compliance, ghi bằng chứng phê duyệt vào body ticket rồi mới build, chạy sanity và internal check như R3 | PS-11, mục 7.4 |
| 13 | Khi nào Doer được hỏi subsidiary trong lúc làm một ticket R3? (a bất cứ khi nào chưa chắc thao tác Backoffice; b chỉ khi brief thiếu hoặc mâu thuẫn, hoặc một price sanity rule bị vi phạm; c mọi câu hỏi phải qua Shift Leader; d bỏ QA vì đã có internal check) | **b** – hỏi MỘT câu gộp, chuyển ON HOLD SUBS và giao ticket cho subsidiary | Brief đủ thì Doer chỉ ghi Internal check và build (chương 3.5, 2.3) |

### B. Tình huống (câu 14–22 theo thứ tự đề)
| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 13 | Special price PH: giá bán 600 USD, giá mới 90 USD, brief không giải thích | Vi phạm PS-02 (giảm từ 20%), PS-03 (tỷ lệ 0,15, dưới 0,5), PS-05 nếu là khuyến mại vượt khoảng, có thể PS-01 (dưới floor hoặc dưới 50% RRP). Bước: dừng build; comment "Sanity hold" với mã quy tắc + giá trị; một câu hỏi tổng hợp kèm số lượng dự kiến; ON HOLD SUBS giao requester (đồng hồ dừng); báo Shift Leader nếu go-live trong 8h; requester xác nhận viết nhắc rõ giá trị thì về STG SETUP rồi mới build. Requester chỉ comment mà không chuyển trạng thái: CoE tự chuyển về STG SETUP ngay |
| 14 | 23:30, monitor mốc 2: 5 đơn giảm 120 USD trong khi internal check ghi giảm 40 USD. 30 phút tiếp theo? | (1) Báo Shift Leader ngay, ghi giờ phát hiện. (2) Shift Leader xác nhận tác động trong 15', làm IM tạm thời. (3) Kill switch trong 30': disable promotion hoặc rollback theo rollback step. (4) Thông báo RHQ + subsidiary trong 30' theo mẫu CM-06. (5) Không tự điều tra trước khi khống chế. Sau: danh sách đơn trong 24h, RCA 48h (chậm nhất 72h) |
| 15 | Giảm 10% cho 8 SKU ở SG, MY, PH, VN, TH, ID; exposure ~4.000 USD: cấp duyệt? | 6 thị trường (>5) nên là **E4** dù exposure <10.000 USD. Cần QA kiểm toàn bộ, Shift Leader duyệt cấp 1, Merch Lead/Deputy duyệt cấp 2 (khác người cấp 1), post-change check 15' ở từng thị trường theo giờ go-live. Còn phải có Knox approval theo approval path trong brief trước khi publish live |
| 16 | TM có QA FAIL lần hai trong tháng: lần 1 `RC-ENT`, lần 2 `RC-SCP` | Cả hai mã đều tính vào lần trả về của Doer → kích hoạt **L1**. QA Sub-Lead báo Shift Leader phụ trách market span trong ngày; Shift Leader mở L1 trong 1 ngày làm việc: kèm cặp với senior hoặc L3 Coach, giảm WIP một nửa, peer check mọi ticket trước QA, chứng nhận lại runbook trong 5 ngày làm việc. Không đạt thì Merch Lead quyết theo CO-05. Báo cáo tuần ghi một dòng ẩn danh |
| 17 | QA Lead kiểm lại 5% PASS tuần trước: coupon đã PASS nhưng thiếu giới hạn mỗi khách, đang live | **QA miss trên production = escaped defect** (category Coupon; mã `RC-LIM` cho Doer, ghi QA miss cho Checker). Báo Shift Leader ngay để sửa giới hạn; kiểm order monitor xem có lượt dùng vượt chưa; nếu có tiền thì xử lý như incident (CM-06) và ghi loss register. CAPA: checklist sửa trong 3 ngày làm việc; Doer và Checker chứng nhận lại |
| 18 | Viết comment internal check bằng tiếng Anh cho promotion giả lập: BOGO `DEMO-BUDS-3` tặng `DEMO-CASE-3`, TH B2C, 00:00 11/12/2026 – 23:59 13/12/2026 ICT, tối đa 1 quà/đơn | Mẫu: SKU DEMO-BUDS-3 (buy) and DEMO-CASE-3 (free gift); BOGO, buy 1 get 1 DEMO-CASE-3 free; 11-Dec-2026 00:00 to 13-Dec-2026 23:59 ICT; store TH B2C; max 1 free item per order; stacking {per brief}; customer group {per brief}. Matches approved brief v{n}. Chấm: đủ kỳ và múi giờ, store scope, cơ chế bằng mã SKU, giới hạn, stacking, dòng "Matches approved brief"; comment viết trước khi build; brief đủ thì không chuyển ON HOLD SUBS |
| 19 | `DEMO-2801` TH hai promotion (P1 go-live 01/12 00:00, P2 08/12 00:00), đã QA PASS + duyệt; 23:59 30/11 subsidiary chưa duyệt ở REVIEW SETUP: việc của CoE đến khi đóng? | 23:59 30/11: publish như đã thống nhất, comment mẫu C.8. 00:00 01/12: go-live check P1, người thứ hai QA lại trên production trong 30', monitor 8 mốc đến 02:00, comment "Go-live batch 1/2". Ticket chờ đợt sau ở PENDING LAUNCH (nếu còn ở REVIEW SETUP vì chưa duyệt thì ghi rõ trong comment). 00:00 08/12: lặp lại cho P2, rồi LAUNCH VERIFICATION và CLOSED. Chấm: có QA lại production ở cả hai đợt, không đóng ticket sau đợt 1 |
| 20 | 18:00 ICT `DEMO-2802` (cart discount 20 USD MY, R3, exposure ~3.000 USD) cần live 00:00 MYT (23:00 ICT); QA không kịp. Bạn là Shift Leader | (1) Nhận diện last-minute (đến sau mốc nội bộ 17:00, không kịp QA); comment câu RHQ (mẫu C.9) và gắn label đếm `LastMinRequest` (CM-09). (2) Áp kiểm soát tối thiểu (CEO chốt 22/10/2026, CM-13 chương 8): price sanity rules, internal check ghi trên ticket trước khi build, Shift Leader duyệt, Knox approval theo approval path trong brief, người thứ hai kiểm trên production thật lúc go-live và chạy monitor. (3) Không đủ thời gian cho các bước trên: báo subsidiary bằng văn bản, đề nghị giờ mới, không publish live khi chưa duyệt và chưa có Knox approval. (4) Đứng chờ hỗ trợ lúc go-live. (5) Trễ vì nút thắt phía CoE thì giải trình với subsidiary. Số yêu cầu gấp vào báo cáo tuần |
| 21 | Ticket R3 này cần những cấp duyệt nào, và còn phê duyệt nào của Samsung trước khi publish live? | Cấp nội bộ: Doer ghi internal check, QA kiểm, Shift Leader duyệt (người khác Doer và Checker). Ngoài ra giá và promotion còn phải có **Knox approval** theo approval path trong brief trước khi publish live; chưa có thì không publish |
| 22 | Nếu RHQ ghi strike cho một người vì không theo quy trình, người đó vào mức nào của people-risk ladder, và BiPlus phải làm gì trước strike thứ ba? | Nếu RHQ quyết định ghi strike (dựa trên RCA của Lead), người nhận strike vào bậc kèm cặp **L1**; ba strike trong một năm dương lịch là bị loại vĩnh viễn nên BiPlus chủ động thay người trước strike thứ ba (mục 6.6–6.7) |

---

## MR-07 Peak, launch và campaign playbook

Đạt ≥80%; câu 2, 5, 8, 13 trọng yếu.

### A. Trắc nghiệm (13 câu)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | 11.11/2026 do ai làm thay đổi của chiến dịch? | **b** – SDSAP (đơn vị vận hành hiện tại); BiPlus quan sát và ghi bài học | Mục 1.2 |
| 2 ★ | Go-live 00:00 AEDT ngày 27/11/2026 là mấy giờ ở VN? | **c – 20:00 ngày 26/11** | AEDT UTC+11, sớm hơn VN 4 giờ (1.5) |
| 3 | Cut-off QA cho thiết lập go-live cùng tối? | **c – 17:00** | Ngưỡng nội bộ để nhận diện yêu cầu gấp; RHQ chưa chốt mốc last-minute (3.2) |
| 4 | 48h trước Black Friday, thay đổi nào được làm? | **b** – chỉ thay đổi được RHQ duyệt, và emergency change trong incident | Mục 2.3 |
| 5 ★ | Ticket PH nhận từ T-3, QA FAIL 22:30, Doer đang sửa; go-live 23:00 đã qua chưa có QA PASS | **b** – không go-live; báo requester bằng văn bản, đề nghị giờ mới, báo Peak Lead | Không "bật trước, kiểm sau"; go/no-go theo thị trường; không phải yêu cầu gấp (3.4) |
| 6 | Lớp dự phòng dùng người đã chứng nhận từ các đội BiPlus Samsung khác, tối đa 2 tuần, RHQ duyệt? | **c – Surge** | Mục 2.4 |
| 7 | Với subsidiary, trao đổi đêm peak hiện qua kênh nào? | **b** – comment Jira, trong lúc chờ RHQ chốt kênh | Mục 5.3 |
| 8 ★ | Peak Lead ở nhà, theo dõi qua điện thoại: điều nào đúng? | **b** – không có war room ảo; được gọi thì có mặt tại trung tâm trong 60 phút | Không làm remote (5.1) |
| 9 | "Clean Room" trong ngày VN Clean Room là gì? | **b** – phòng UAT flagship của RHQ đặt tại văn phòng BiPlus, nơi RHQ, HQ, đội India, subsidiary làm UAT cùng nhau | Khác khu làm việc bảo mật và war room (1.3, 5.1) |
| 10 | 12.12 (T7) thêm người thế nào (dashboard v1.4)? | **b** – +4 người ca ngày (gồm 3 bench), +2 người ca tối, Merch Lead có mặt | Mục 1.2 |
| 11 | BVT của một enhancement trong CoE do ai thực hiện? | **b** – PIC Merch hoặc Tech tùy phạm vi; QA không tham gia | Mục 4.4 |
| 12 | Cuối cửa sổ BVT, 49/50 case pass | **b** – không go-live; ghi defect vào file Excel cho đội phát triển triage, sửa xong retest, 100% pass mới sign-off | 99% là không go-live; điền pass không test sẽ bị RHQ phát hiện (4.4) |
| 13 ★ | Đêm peak, Tech cần xóa một user group qua Back Office sửa lỗi checkout (P1) | **b** – cần PC do Oliver duyệt; P1 nhắn Oliver qua Mattermost; COEC gốc ON HOLD HQ "PC ticket pending". Không có phương án (c) Tech Lead duyệt thay Oliver | Kể cả việc 5 giây và thay đổi khẩn trong sự cố; Oliver là người duyệt duy nhất, không có người thay (4.3) |

### B. Tình huống (7 câu)
| # | Tình huống | Đáp án mẫu |
|---|---|---|
| 14 | Bảng giờ go-live Cyber Monday 30/11/2026 ở 8 thị trường (giờ VN), ca phụ trách, vì sao là điểm nóng? | NZ 18:00 ngày 29/11, AU 20:00 ngày 29/11, SG/MY/PH 23:00 ngày 29/11 (ca tối); VN/TH/ID 00:00 ngày 30/11 (ca đêm, giờ bàn giao). Điểm nóng: 29/11 là **Chủ nhật** (mỗi ca chỉ SL+1) và 30/11 là **ngày takeover**; Merch Lead cần chốt người thêm (1.2) |
| 15 | Shift Leader ca tối đêm 26/11: 4 việc từ 23:00 đến 00:15 | (1) Go-live SG, MY, PH đúng 23:00 + go-live check; (2) post-change check (QA lại production) trước 23:30, E4 trước 23:15; (3) viết handoff note lúc 23:30 với mọi go-live, monitor đang chạy, tên người; (4) giữ người monitor SG/MY/PH đến 01:00 hoặc giao bench; bàn giao 00:00 bằng handoff viết, không bàn giao miệng |
| 16 | T4 25/11 (freeze), SG xin đổi mức giảm promotion Black Friday 15% → 20% | Trong freeze 48h chỉ thay đổi RHQ duyệt mới được làm. Ghi yêu cầu lên ticket, báo Peak Lead + COE Lead xin RHQ duyệt; có duyệt thì ghi bằng chứng vào body ticket. Rồi sanity và internal check lại với mức 20% theo brief cập nhật của subsidiary (chưa có brief cập nhật: hỏi MỘT câu gộp, ON HOLD SUBS, giao subsidiary), Knox approval mới (mức giảm là ACTION của promotion nên phải duyệt lại; đổi tên promotion thì không cần), QA (hai lớp với Black Friday), Shift Leader duyệt; tính lại E4. Không có duyệt: giữ thiết lập cũ, comment cho requester |
| 17 | Post-peak review: hai brief đến muộn, QA lớp 2 dồn sau 15:00. Viết hai CAPA có owner, hạn | Vd "MO nhắc hạn brief ở T-10 và T-7 cho 12.12" (owner MO từng thị trường, hạn 27/11); "QA dispatcher chia lớp 2 thành hai đợt 11:00 và 14:00, E4 vào trước" (owner QA Sub-Lead 2, hạn trước 12.12). Mỗi CAPA có cách kiểm là đã xong |
| 18 | Hard freeze flagship, VN gửi 2 yêu cầu: đổi giá phút chót một SKU flagship ("RHQ đã đồng ý", không có bằng chứng) và cập nhật stock 3 SKU khác | Đổi giá phút chót là ngoại lệ, luôn cần phê duyệt: CoE tra trang compliance; có thì ghi bằng chứng (ai duyệt, ngày, phạm vi, link) vào body rồi làm như R3 (sanity, internal check, Knox approval, QA, Shift Leader duyệt, E4 nếu đạt); không có phê duyệt ngoại lệ thì không làm, comment requester, báo Peak Lead. Cập nhật stock **luôn được phép** trong hard freeze: làm như ngày thường theo cấp rủi ro (2.3) |
| 19 | T6 20:00 RHQ gửi thông báo BVT T3–T5 tuần sau cho enhancement ảnh hưởng hiển thị promotion. Bạn là Shift Leader ca tối; sau đó là Merch Lead sáng T2 | **Shift Leader:** ghi thông báo BVT vào handoff note và nhắn Merch Lead + Tech Lead trên kênh nội bộ để chỉ định PIC trong ngày làm việc kế tiếp; không gọi QA. **Merch Lead sáng T2:** phạm vi Merch → chỉ định PIC + backup, giảm WIP của PIC, cộng giờ BVT vào bảng tải, bench nếu cần; PIC dự kickoff, comment bắt đầu trên ticket enhancement, thêm case thị trường, test từ ngày đầu, cập nhật file Excel và Confluence hằng ngày, dự call cuối ngày (nếu có); lỗi → ghi defect vào file Excel cho đội phát triển triage; chỉ sign-off khi 100% pass. Ngày BVT không thương lượng (4.4) |
| 20 | Trước Black Friday, MY cần 500.000 mã coupon, cần ImpEx của Tech: các bước từ ticket Merch đến khi mã chạy production | (1) Ticket Merchandising (coupon là promotion) giữ nguyên, không chuyển sang COEC; phần setup coupon vẫn đi workflow Shop Merchandising và Knox approval theo approval path trong brief. (2) Merch PIC tạo COEC mới ghi rõ cần ImpEx 500.000 mã, issue link. (3) Merch → ON HOLD COE + comment (SLA Merch vẫn chạy, người tạo COEC đôn đốc Tech). (4) Tech: NEW → ASSIGNED → ImpEx trên staging, tự QA (QA REVIEW), another set of eyes (người giữ chứng nhận L2 hoặc L3 của service; bắt buộc nếu ImpEx mới). (5) PC kèm kết quả staging; COEC → ON HOLD HQ "PC ticket pending"; Oliver duyệt → COEC về IN PROGRESS. (6) Chạy ImpEx production có dòng số PC + COEC gốc; COEC → LAUNCH VERIFICATION. (7) Merch PIC đưa ticket Merch khỏi ON HOLD COE về bước đang làm, kiểm kết quả, QA nếu cần, trả subsidiary (REVIEW SETUP). Làm sớm từ T-14 vì PC ticket chỉ có một người duyệt (Oliver Leung), chậm khoảng 3 giờ |

---

# PHẦN IV. SAP / HYBRIS (SAP)

## SAP – SAP và nghiệp vụ Samsung SEAO
Giáo trình nền tảng; chương 09 của trang gốc chỉ còn đáp án, nên 15 câu dưới đây diễn đạt lại từ các đáp án đó.

### A. 15 câu tự kiểm tra (chương 09)
| # | Câu hỏi | Đáp án | Giải thích ngắn |
|---|---|---|---|
| 1 | AEM và N-ERP giữ gì? | AEM chỉ nội dung trang; N-ERP giữ giá gốc | Chương 02–03 |
| 2 | Sửa dữ liệu ở Staged có đủ để hiện lên site không? | Không; phải **sync** | Chương 03 |
| 3 | Sản phẩm Purchasable + Unapproved hiện gì? | Nút "Where to buy" | CTA, chương 03 |
| 4 | Nhiều quy tắc cùng áp, cái nào thắng? | Multistore ưu tiên cao nhất | Chương 03–04 |
| 5 | Order và consignment liên quan thế nào? | Một order có một hoặc nhiều consignment; trạng thái order theo gói chậm nhất | Chương 05 |
| 6 | T-Code là gì? | Thiết bị trade-in do cronjob tạo, luôn Archived, gắn bằng AVAILABLE_SERVICE | Chương 04 |
| 7 | Muốn nhập tồn kho ảo phải làm gì? | Chặn đồng bộ N-ERP (Stock Import Override), vì cronjob có thể ghi đè | Chương 03 |
| 8 | Đổi gì ở promotion đã publish thì phải duyệt Knox lại? | Action, điều kiện, website, ngày; đổi tên/trạng thái thì không | Liên hệ CM-13 mục 10 |
| 9 | Chương trình mới dùng voucher hay coupon? | Coupon; chỉ RNPL còn voucher | Chương N |
| 10 | Lỗi thiếu Customer Number do đâu? | Cửa hàng O2O chưa có ship-to trên N-ERP | Chương 06 |
| 11 | Truy vấn dữ liệu bằng gì? | HAC Console › FlexibleSearch | Chương 07 |
| 12 | Trường status chỉ lưu pk, muốn đọc tên? | JOIN bảng OrderStatus | Chương N, 07 |
| 13 | Ai được ImpEx/Groovy sửa dữ liệu, điều kiện? | Chỉ Tech, có PC ticket, qua staging, có dòng header | CM-13 mục 9 |
| 14 | Authorize khác capture? | Authorize giữ tiền; capture thu tiền sau kiểm tra gian lận | Chương N |
| 15 | Production và staging khác nhau thế nào? | Production là thật; staging để thử, học ở staging | Chương N |

### B. Bài tập tính RDD (BN3)
RDD = ngày đặt + lead time + lead time vận hành kho (mặc định 0) + 1 nếu quá cut-off (thường 15:00) + số ngày không giao + số ngày lễ.
| # | Tình huống | Đáp án |
|---|---|---|
| 1 | Thứ Năm 10:00, lead 3, cut-off 15:00 | **Thứ Ba** |
| 2 | Đặt 16:30 (quá cut-off) | **Thứ Tư** |
| 3 | Thứ Hai là ngày lễ | **Thứ Tư** |
| Ví dụ gốc | Đặt Thứ Tư 12/6, lead 5 | Chuẩn: Thứ Tư 19/6; sau 15:00: Thứ Năm 20/6; 2 ngày lễ: Thứ Sáu 21/6; giao cả tuần: Thứ Hai 17/6 |

### C. Bài nộp BN1–BN6 (không có đáp án đúng/sai; tiêu chí)
- **BN1** vẽ kiến trúc: ≥ 6 kênh, 3PD middleware, N-ERP, OMS, cổng thanh toán, đối tác, kho; mũi tên có nhãn; bảng ≥ 6 thành phần.
- **BN2** kịch bản Thái Lan ra mắt điện thoại mới (QA trước ngày ra mắt, special price 2 tuần, quà Z-Code 500 khách đầu, trade-in, sau 2 tuần promotion theo payment mode) → phiếu setup.
- **BN4** sổ tay 6 thao tác: CTA của SKU, tồn kho từng kho, promotion áp website nào/đã publish chưa, trạng thái + số consignment, payment mode của khách EPP, cronjob tồn kho lần cuối.
- **BN5** chép phiếu ghi chép + ≥ 3 câu hỏi gửi RHQ. **BN6** "Hybris SEAO bằng lời của tôi" kèm 3 điểm khác biệt giữa các nước và 3 ý từ một trang KB chưa nhắc.
