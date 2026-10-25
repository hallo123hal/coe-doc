# CM-10 An toàn thông tin trong công việc hằng ngày (bài T1)

> Tóm tắt từ trang Confluence CM-10 (**v0.3, bản nháp 22/10/2026**, song ngữ). **Cập nhật v0.3** (theo [CM-13](CM-13-quy-tac-rhq.md) + quyết định CEO 22/10): thêm **offboarding** (mục 1.5), **dữ liệu và PII** (không gửi PII qua email Hybris; xin email khách để gửi EDM mặc định từ chối; Tech không truy vấn production khi không có lý do; PUMI → PC cho báo cáo/cronjob; database RHQ quản lý không bao giờ sửa), **email dự án miền `coe.biplus.com.vn`** (không dùng @biplus.com.vn thông thường), **strike** (RHQ quyết định; 3 strike/năm dương lịch = loại vĩnh viễn; ATTT chưa tính strike) và **ngoại lệ thứ hai của quy tắc 3: ghi hình đào tạo nội bộ**; tình huống đúng/sai tăng từ 23 lên **29**; bằng chứng QA không dùng video; đề T1 vẫn 20 câu (câu 19 thêm ý ticket offboarding). Chủ sở hữu: DevSecOps Engineer; biên soạn: CoE Office; ký duyệt: CEO. Người đọc: toàn đội Ops CoE (Merchandising, Tech, QA, bench, CoE Operations Office). Chu kỳ rà soát: ≥ 3 tháng/lần hoặc ngay sau sự cố có bài học. Tài liệu liên quan: CM-01, CM-06, CM-09, CM-11, CO-04 (văn bản gốc về ATTT/dữ liệu/AI), CO-05 (xử lý vi phạm), CO-06.

## 1. Bối cảnh và nguyên tắc nền
- CoE được cấp quyền vào hệ thống bán hàng thật của 8 thị trường (giá, promotion chưa công bố, sản phẩm sắp ra mắt, đơn hàng, dữ liệu cá nhân khách). Lộ dữ liệu nghiêm trọng hơn vỡ SLA.
- Mọi thông tin liên quan Samsung = **Samsung Confidential Information** (NDA, RFP 1.1), chỉ cho người **need to know**. RFP 3.12: quy tắc AI; RFP 3.9: báo ngay sự cố bảo mật; RFP 3.8: RHQ audit, báo trước ≥ 3 ngày làm việc; RFP 3.4: RHQ có quyền thu hồi truy cập/yêu cầu thay người.
- Vi phạm nghiêm trọng về an ninh/AI là căn cứ để Samsung chấm dứt hợp đồng ngay.
- Khi khác biệt, **CO-04** là văn bản gốc.

### Ba loại thông tin
| Loại | Ví dụ | Được nằm ở đâu |
|---|---|---|
| Mật Samsung + dữ liệu cá nhân khách | Ticket, brief, file giá, SKU, promotion chưa live, đơn hàng, thông tin khách | Chỉ hệ thống Samsung: Jira, Confluence, email Samsung, Hybris Backoffice, AEM, Shop App CMS; Mattermost (kênh RHQ) ở mức tối thiểu |
| Nội bộ BiPlus | Roster, nghỉ phép, tài liệu Academy không chứa dữ liệu Samsung | Hệ thống BiPlus (vd BiPower) |
| Công khai | Trang Samsung.com đang hiển thị | Ai cũng xem, nhưng không bình luận thay Samsung |

## 2. Mười quy tắc bắt buộc
1. **Chỉ làm tại khu làm việc bảo mật tầng 6, trên máy trạm CoE** – không remote kể cả on-call. Máy trạm: mã hóa ổ đĩa, diệt virus, chặn USB, chỉ mạng dây; không cài phần mềm, không tắt bảo vệ, không phát Wifi điện thoại.
2. **Dữ liệu chỉ nằm trên hệ thống Samsung** – không export/tải về/USB/Drive/email cá nhân/hệ thống BiPlus; dẫn chiếu bằng link hoặc mã ticket.
3. **Không chụp bằng điện thoại, không quay, in, chép tay** – bàn giao bằng comment Jira và handoff note. Ngoại lệ: ảnh bằng chứng QA (xem mục 3).
4. **Tài khoản là của riêng bạn** – có MFA, không cho mượn/dùng chung/đăng nhập hộ; khóa màn hình (Win+L) khi rời chỗ; rời dự án thì Lead tạo **ticket offboarding đúng ngày làm việc cuối** để khóa tài khoản trên mọi hệ thống Samsung.
5. **AI không bao giờ có dữ liệu Samsung** – chỉ công cụ AI RHQ duyệt; không đưa thông tin mật/dữ liệu cá nhân/mã nguồn/mật khẩu; **cấm AI với sản phẩm embargo/flagship**; kết quả AI phải do người có chứng nhận rà soát.
6. **Chỉ dùng kênh được phép** – RHQ: Mattermost; subsidiary: comment Jira (kênh nhắn tin chưa chốt; Knox Messenger chỉ khi RHQ cấp); email Samsung, hotline CoE. Cấm Zalo/Messenger/Telegram/Gmail/email @biplus.com.vn thông thường cho nội dung Samsung; email chỉ dùng **email dự án miền coe.biplus.com.vn** (tên tiếng Anh + họ thật, chỉ mở trên máy trạm CoE; nơi lưu hộp thư chờ CEO/DevSecOps xác nhận). Gửi nhầm người = sự cố.
7. **Dữ liệu cá nhân khách (PII)** – chỉ xem khi ticket cần; dùng mã đơn thay tên/SĐT/địa chỉ; CoE không liên hệ khách cuối; áp dụng luật bảo vệ dữ liệu VN và PDPA các thị trường. **Không bao giờ gửi PII qua email từ Hybris**; subsidiary xin email khách để gửi EDM: **mặc định từ chối** (comment ticket + báo Shift Leader/Lead); Tech không truy vấn production khi không có lý do (ghi trên ticket; truy vấn chỉ đọc không cần PC); báo cáo/dữ liệu lịch sử/cronjob báo cáo/đổi recipient cần **PUMI** (subsidiary tạo) rồi mới PC ticket; thêm-bớt trường không-PII được; PII chỉ ngoại lệ audit; FTP theo quy trình riêng; database do RHQ quản lý CoE không bao giờ sửa.
8. **Không nói/đăng ra ngoài** – không mạng xã hội, không bàn ở nơi công cộng; báo chí hỏi chuyển SDM; nghĩa vụ bảo mật còn sau khi rời dự án.
9. **Giữ cửa, giữ bàn** – vào tầng 6 bằng nhận diện khuôn mặt của chính mình, không tailgating; khách phải nằm trong danh sách SDM và có người dẫn; clean desk. Phân biệt **khu làm việc bảo mật** (CoE làm hằng ngày) với **Clean Room** (phòng UAT flagship của RHQ, 40 chỗ, cửa khóa chìa).
10. **Báo trong 1 giờ** – báo lời ngay, văn bản trong 1 giờ; báo sớm không bị phạt, giấu mới bị phạt.

Đối chiếu: ứng với mười quy tắc vàng ở CM-01 (quy tắc 1↔vàng #1; quy tắc 2, 3, 6↔#2; quy tắc 5↔#3; quy tắc 10↔#8).

## 2b. Offboarding (mục 1.5, mới v0.3)
Phải xong **đúng ngày làm việc cuối**; tài khoản Samsung còn mở sau ngày đó là lỗi tuân thủ (báo như sự cố ATTT). Các bước: (1) Lead báo ngày cuối trong họp tuần (ai nghỉ, ai backup, kế hoạch phủ việc); (2) người nghỉ bàn giao ticket bằng handoff note trước ngày cuối; (3) **ngày cuối Lead tạo ticket offboarding** theo template RHQ, liệt kê từng hệ thống cần khóa (Jira, Confluence, Mattermost, Hybris Backoffice, AEM, Shop App CMS…) — mẫu: "Offboarding: [name, role] last working day [date]. Please deactivate all Samsung system accounts listed below: [list]."; (4) cùng ngày trả thiết bị và chìa, thu hồi quyền ra vào tầng 6, khóa email dự án (không cấp lại địa chỉ cho người khác); (5) Atlassian Platform Engineer đối chiếu provisioning log với danh sách nhân sự, còn mở thì báo DevSecOps như sự cố; (6) nghĩa vụ NDA còn hiệu lực.

## 2c. Strike (mục 1.1, mới v0.3)
RHQ quyết định dựa RCA của Lead (lỗi hệ thống không tính); 3 strike/năm dương lịch = loại vĩnh viễn; ba việc chắc chắn strike: thiếu header ImpEx/Groovy (số PC + số COEC gốc), đổi production khi chưa có PC duyệt, làm service chưa chứng nhận gây sự cố. Vi phạm ATTT **chưa tính** strike (Samsung chưa yêu cầu) nhưng vẫn xử lý theo CO-04/CO-05. Nội bộ: người nhận strike vào bậc kèm cặp L1 (MR-06), BiPlus chủ động thay người trước strike thứ ba.

## 3. Hai ngoại lệ có kiểm soát của quy tắc 3
**(1) Ảnh bằng chứng QA (từ training RHQ 21/10; không dùng video — Jira giới hạn 15 MB/file, link ghi hình còn vướng quyền).**
Bằng chứng QA hiện là file PowerPoint chụp màn hình từng bước, đính vào comment Jira để subsidiary duyệt ở REVIEW SETUP. Chỉ đúng khi đủ 4 điều:
1. Tạo trên máy trạm CoE trong khu bảo mật.
2. Đính thẳng vào ticket Jira.
3. Xóa bản trên máy ngay sau khi đính (cả Downloads và thùng rác).
4. Không chụp bằng điện thoại; không gửi qua kênh khác. Tránh vùng có dữ liệu cá nhân khách.

**(2) Ghi hình đào tạo nội bộ (mới v0.3)** — RHQ yêu cầu đào tạo trực tiếp định kỳ phải được ghi hình; được phép **tạm thời, chỉ khi Samsung đồng ý**: chưa chắc thì hỏi Lead trước; người tổ chức bật ghi hình bằng công cụ họp (người dự không tự quay); chỉ dùng tài liệu và ví dụ giả lập, không chia sẻ màn hình hệ thống Samsung; link ghi hình truy cập được, tải được, không hết hạn, lưu trên trang tài liệu liên quan.

## 4. Các điểm còn chờ chốt
- Danh sách công cụ AI được duyệt: DevSecOps công bố sau khi công bố cho RHQ (CP1, C1-16); **đến lúc đó không dùng AI nào cho việc Samsung**.
- Bằng chứng QA bắt buộc PowerPoint hay ghi trực tiếp Jira: chờ RHQ. File làm việc khác (file giá bulk upload, file diff) tạm áp dụng 4 điều trên.
- Laptop QA/Tech (chỉ dùng cho Samsung; image chuẩn; mạng dây; không mang khỏi tầng 6 trừ khi SDM duyệt) chờ CEO xác nhận; MFA có dùng điện thoại hay không chờ RHQ.
- Quyết định 21/10/2026: **chưa thu giữ điện thoại** ở tầng 6 nhưng **cấm chụp, quay** và cấm dùng với dữ liệu Samsung; chuẩn bị flagship thì gửi điện thoại vào tủ ở sảnh thang máy.
- "VN Clean Room" mỗi flagship: RHQ, HQ, India, subsidiary đến văn phòng BiPlus làm UAT. Khách không đăng ký khuôn mặt, vào theo danh sách SDM, có người dẫn, chỉ ở khu dành cho khách; không dùng máy/tài khoản CoE; yêu cầu sửa setup vẫn qua Jira. Cách vận hành chi tiết RHQ hướng dẫn sau.

## 5. Tình huống đúng/sai (29 tình huống, rút gọn)
- **Đúng**: làm PPT bằng chứng QA trên máy CoE → đính Jira → xóa; gửi link Confluence Samsung bằng comment Jira; ra sảnh nghe điện thoại không chụp; không bấm email phishing và báo DevSecOps; nhắc & báo Sub-Lead khi thấy đồng nghiệp chụp màn hình.
- **Sai**: chụp Hybris bằng điện thoại; tải file giá từ Gmail cá nhân; dán brief vào AI dịch; dùng AI mô tả sản phẩm sắp ra mắt; mang laptop CoE về nhà; cắm USB; selfie/đăng Facebook/LinkedIn về công việc; in checklist có giá/SKU; cho mượn tài khoản (kể cả khách UAT); giữ cửa cho người lạ; gửi nhầm email rồi không báo; chép tên/SĐT khách vào Jira; lỡ bấm link lạ mà không báo; gửi PPT bằng chứng qua Mattermost hoặc giữ bản dự phòng; dẫn khách UAT sang khu làm việc CoE; **(mới v0.3)** gửi danh sách email khách cho subsidiary để gửi EDM; Tech chạy query xem đơn khách "cho biết" khi ticket không yêu cầu; gửi file báo cáo có tên/SĐT khách bằng email Hybris; để hai tuần sau mới tạo ticket khóa tài khoản người nghỉ; đăng ký tài khoản bằng @biplus.com.vn thông thường.
- **Đúng (mới)**: Lead bật ghi hình buổi đào tạo nội bộ bằng công cụ họp khi Samsung đã đồng ý, chỉ dùng slide và ví dụ giả lập.
- Hầu hết lỗi thuộc 4 nhóm: chụp/in, kênh cá nhân, AI, thiết bị/tài khoản.

**Checklist 5 giây trước khi bấm**: có phải thông tin Samsung/khách? nơi gửi/lưu có phải hệ thống/kênh được phép? người nhận có cần biết, đúng địa chỉ? có dùng AI/điện thoại/USB/in/kênh cá nhân? ảnh/file bằng chứng đã đính Jira & xóa? nếu mai RHQ audit có giải thích được không?

## 6. Phát hiện và báo sự cố ATTT trong 1 giờ
- **Sự cố** = bất kỳ việc đã/có thể làm lộ, dùng sai, mất an toàn thông tin mật/dữ liệu khách/tài khoản/khu làm việc. Nghi ngờ là đủ để báo. Ví dụ: gửi nhầm, lộ mật khẩu, bấm link/mở tệp đáng ngờ, mất laptop/thẻ/chìa Clean Room, USB lạ, dữ liệu vào công cụ AI, người lạ trong tầng 6, khóa/camera hỏng.
- **Báo ai/kênh**: ngay → Shift Leader/Sub-Lead/Lead đang trực **và** DevSecOps Engineer (lời/điện thoại); ngoài giờ hoặc không liên lạc được → SDM hotline 24/7; trong 1 giờ → mẫu văn bản gửi DevSecOps + SDM, cc Lead; ảnh hưởng dữ liệu Samsung/khách → COE Lead hoặc SDM báo RHQ theo RFP 3.9 và CM-06 (**bạn không tự báo RHQ**).
- **5 bước giờ đầu**: Dừng → Giữ nguyên (không xóa email/lịch sử, không tắt máy trừ khi được yêu cầu) → Báo lời ngay → Viết mẫu báo trong 1 giờ → Làm theo hướng dẫn (đổi mật khẩu, thu hồi email…). Không chụp/chuyển tiếp dữ liệu bị lộ, không giấu, không tự liên hệ RHQ/subsidiary.
- **Mẫu `[SECURITY INCIDENT] Báo cáo ban đầu`** (9 mục): người báo; thời điểm (ICT); loại; chuyện gì xảy ra; ở đâu (hệ thống/trang/mã ticket); dữ liệu có thể ảnh hưởng; phạm vi ước tính; đã làm gì; hiện trạng. Không đính kèm dữ liệu bị lộ.
- **Sau báo**: DevSecOps đánh giá, khắc phục, ghi sổ theo CO-04. Nếu ảnh hưởng dữ liệu → xử lý như sự cố **Critical** theo CM-06 (bridge; thông báo RHQ trong 30 phút nội bộ, RFP 2 giờ; RCA trong 48h, tối đa 72h). Sự cố AI báo RHQ ngay (RFP 3.12). Sau RCA: CAPA, có thể đào tạo/chứng nhận lại. Người báo sớm được ghi nhận.

## 7. Bài T1 và bản cam kết
- **T1 Security, data and AI quiz** – bài đầu tiên của Academy (CM-11). Không đạt T1 = chưa cấp truy cập hệ thống Samsung.
- Khi nào: Day 0, trong security onboarding, trước ca live đầu tiên. Ai: mọi người vào Ops CoE.
- Hình thức: 20 câu trắc nghiệm (4 lựa chọn), cá nhân, không xem tài liệu. **Đạt**: ≥ 90% (18/20) **và** đúng cả 8 câu trọng yếu. Người chấm: DevSecOps Engineer.
- Không đạt: nghe briefing lại, làm lại trong ngày; Workforce Lead quyết định bước tiếp (CO-06). Đạt thì ký **cam kết Phụ lục A** (10 cam kết tương ứng 10 quy tắc, xác nhận hiểu chế tài theo CO-04/CO-05, nghĩa vụ NDA sau khi rời dự án, đồng ý xử lý dữ liệu khuôn mặt ký riêng).
- Mốc: đợt W0 ngày 22/10, toàn bộ trước 26/10/2026 (dashboard v1.4, S-03).
- Đề gồm 20 câu bao quát: nơi lưu dữ liệu, AI, on-call, khóa màn hình, mượn tài khoản, kênh subsidiary (Jira), phishing, điện thoại ở tầng 6, bàn giao lỗi Hybris, bằng chứng QA, mã đơn thay dữ liệu khách, báo 1 giờ, SDM hotline, tailgating, AI với embargo, rà soát kết quả AI, khi rời dự án, quyền audit RHQ. Đáp án ở Phụ lục B (câu trọng yếu: 1, 3, 4, 6, 8, 10, 13, 16).
