# TEC-3.3 Data, reports, PII, PUMI

> Nguồn: page 2483191957 · 30 phút (Study 10' · Demo 5' · Quiz 5' · Practice 10') · Lecture ngắn + bài phân loại data request; facilitator: Tech Lead · Cần xong G1.3, G5.2, TEC-2.1; không cần hệ thống.

## Mục tiêu
Phân biệt query điều tra với report và nêu approval từng loại cần; nhận các field PII trong danh sách RHQ; chọn đúng đường PUMI cho report có/không PII và ticket cần tạo sau duyệt; từ chối đúng cách các data request vi phạm luật.

## Thuật ngữ
**Investigation query** (FlexibleSearch chỉ đọc để xử lý một ticket cụ thể; không cần PC nhưng phải ghi lý do); **Report** (data gửi ra ngoài: một lần, định kỳ, hay data lịch sử — report mới, người nhận mới, data lịch sử cần PUMI; chạy trên production còn cần PC); **Report non-PII / with PII**; **ONE-OFF** (report chạy một lần; report có PII *chỉ* được ONE-OFF); **EDM** (email marketing hàng loạt — yêu cầu lấy email khách để gửi EDM bị từ chối mặc định); **Re-run saved query** (chạy lại query report đã có PUMI, TEC-RPT-03, kèm PC duyệt — việc report duy nhất Level 1 được làm); **CS ticket** (ticket trang 07 Reports with PII yêu cầu sau khi report PII được duyệt; RHQ chưa xác nhận project/type — tới lúc đó giữ việc trên COEC).

## Nội dung
### 1. Query điều tra hay report?
Luật nền (CM-13 ch.12, G5.2): không query production khi không có lý do. Report, data lịch sử, data một lần, cronjob report, thêm/bớt người nhận → **PUMI trước, PC sau**. Thêm/bớt field không-PII được phép không cần PUMI nhưng vẫn cần PC vì đổi production (CM-13 §12.1). Query điều tra cho một ticket: FlexibleSearch chỉ đọc, không PC; ghi lý do lên ticket, chỉ chọn cột cần, không export data về máy. Level 1 chỉ được chạy lại query report đã có PUMI (TEC-RPT-03) với PC duyệt.

### 2. Field PII theo danh sách RHQ
SA GUID, email, họ tên, giới tính, địa chỉ billing & shipping, postal code, số điện thoại, IP, mã số thuế công ty, IMEI, serial number, employee ID, tên & email store agent, số airline loyalty.

### 3. Hai đường PUMI
**Report không PII (07 Reports without PII)** vẫn cần PUMI, 3 trường hợp: report/cronjob mới (người nhận, field, lịch theo SGT hoặc ONE-OFF); cập nhật cronjob có sẵn; data lịch sử (khoảng ngày, field). Đường duyệt: Requestor → Subs Online HOD → RHQ D2C Platform Head → Suwon (Consent). Sau duyệt: tạo COEC ticket đính PUMI.
**Report có PII (07 Reports with PII):** chỉ ONE-OFF, cấm report PII định kỳ; không gửi gì trước khi được duyệt; contractor, vendor, affiliate không được nhận (địa chỉ `@partner.samsung.com` cũng không được là người nhận). Đường duyệt: Requestor → Subs Online HOD → RHQ D2C Platform Head → Suwon eshop.sec (Consent) → D2C Engineering Group Head (Notice). Sau duyệt: tạo CS ticket đính PUMI.
Bảng "Data Query via HAC or Cronjob" bổ sung: report không PII gửi qua email hoặc FTP; report PII chỉ qua FTP và nằm trên máy tối đa 3 tháng; không đưa report PII vào Jira; file Excel phải có password kể cả gửi FTP; luôn CC team RHQ D2C Platform khi gửi report cho subsidiary.

### 4. Luôn từ chối và cách bảo vệ data
**4 yêu cầu luôn từ chối:** email khách để gửi EDM; gửi PII bằng email từ Hybris; report PII định kỳ; sửa database do RHQ quản. Evidence/screenshot chỉ tạo trên workstation CoE, đã mask PII, đính thẳng vào Jira; không đưa script hay data Samsung vào AI (G1.3). **Nghi lộ data = incident bảo mật P0:** báo ngay Sub-Lead, Tech Lead, DevSecOps Engineer (ngoài giờ hoặc không liên lạc được DevSecOps: hotline SDM); trong 1 giờ gửi báo cáo văn bản cho DevSecOps và SDM, cc Lead; không tự liên hệ RHQ (COE Lead/SDM làm — CM-10 §3.2–3.3); không chụp hay copy data bị lộ.

### Điểm đáng nhớ từ KT
Không query production khi không có lý do; trang Data Query via HAC or Cronjob liệt kê cái gì cần PUMI, PC hay approval khác. Extract lớn (VD toàn bộ data từ 1/1 cho audit): PUMI trước rồi PC kèm PUMI. BI data có quy trình riêng; PII và non-PII khác đường duyệt. **Không bao giờ gửi PII bằng email từ Hybris**; EDM bị từ chối mặc định; FTP có quy trình riêng. Trang RHQ "email PUMI" bị CM-13 ghi đè: không gửi PII bằng email.

## Quiz (đáp án)
1 Subsidiary xin báo cáo bán hàng tháng trước không PII gửi email → **PUMI duyệt, đính vào COEC, PC, rồi chạy và gửi**. 2 Field PII theo RHQ → **IP address của khách**. 3 Subsidiary muốn report PII hằng tuần → **không: report có PII chỉ ONE-OFF**. 4 Tech chạy FlexibleSearch chỉ đọc điều tra 1 order trong COEC → **không PC; ghi lý do và chỉ chọn cột cần**. 5 Xin danh sách email khách đã mua để gửi EDM → **từ chối mặc định, trích luật RHQ trong comment**.

## Practice
**PR-TEC-3.3-1** (giấy, 10'): phân loại 6 yêu cầu — (1) điều tra 1 order kẹt; (2) báo cáo sales một lần không PII; (3) thêm người nhận cho cronjob report SG; (4) báo cáo order có email & địa chỉ cho audit; (5) danh sách email khách để gửi EDM; (6) report PII hằng tuần cho vendor. Với mỗi cái ghi: được/không, cần PUMI không, cần PC không, kênh gửi, ticket sau PUMI, và 1–2 câu trả lời tiếng Anh. Pass: đúng cả 6 quyết định được/không; không câu trả lời nào gửi PII bằng email; comment từ chối lịch sự và trích đúng luật RHQ.
