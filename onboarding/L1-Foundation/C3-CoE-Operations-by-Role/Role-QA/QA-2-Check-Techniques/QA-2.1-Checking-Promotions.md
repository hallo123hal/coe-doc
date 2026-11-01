# QA-2.1 Checking promotions: promotion simulator, test user group, special price report

> Nguồn: page 2483389114 · 90 phút (Study 30' · Demo/thảo luận 15' · Quiz 10' · Practice 35') · Facilitator demo một check đầy đủ trên Backoffice staging rồi mỗi người tự làm với data cho sẵn; facilitator: QA Lead hoặc QA Sub-Lead có L2 service promotion · Cần xong G3.4, G5.1, QA-1.3; cần tài khoản Backoffice staging cụm SMS (s2) + VPN/IP whitelist, tài khoản frontend staging riêng, mở `getcookie.html` của staging trước khi vào storefront. Facilitator chuẩn bị rule `TRAINING_<tên>_PROMO01`, coupon `TRAINING_<tên>_CPN`, 1 customer group với 2 test account, file Excel special price mẫu, bộ ảnh simulator dự phòng. Không có quyền staging hoặc simulator không chạy trên S2 thì xem màn hình facilitator + ảnh dự phòng.

## Mục tiêu
Đọc rule promotion trong Backoffice và so 6 giá trị với internal check; chạy bộ T1–T7 trên simulator, mỗi run ghi 5 input + 3 output; kiểm promotion giới hạn customer group bằng 2 test account; so requestor file với Special Price Report trong cross-check sheet và giải thích ô N/A.

## Thuật ngữ
**Preview promotion module** (nơi publish rule để thử trên simulator, chưa áp dụng cho khách thật); **Backoffice Extension** (tool riêng chạy simulator; promotion vẫn tạo ở Backoffice chính); **Positive/negative/exploratory test**; **T1–T7** (bộ 7 run tối thiểu cho discount promotion theo `QCL-PRM-01`); **Stacking (interaction)**; **Test user group** (kiểm bằng account trong/ngoài customer group); **Target customer**; **Tester group, restriction** (setup chỉ mở cho tester group; mở cho mọi khách cần subsidiary xác nhận); **Special Price Report** (report Hybris liệt kê special price đã upload); **Requestor file**; **Cross-check sheet** (Excel dùng VLOOKUP + EXACT); **Pre-test / live-test** (trước và sau go-live).

## Nội dung
### 1. Vì sao promotion là lõi việc QA
Promotion là R3: sai một số là mất tiền thật (coupon 20 USD để trống "total uses" = không giới hạn, có thể bị dùng hàng nghìn lần trong một đêm). Đường đi: Doer build rule trên production ở trạng thái Unpublished, publish vào preview promotion module để chạy simulator; QA kiểm khi rule chưa live. Sau PASS: Shift Leader duyệt → PRD SETUP, Doer gửi Knox; owner hand-back ở REVIEW SETUP kèm evidence; rule chỉ publish live đúng giờ go-live. **Đổi action, condition, website hoặc dates sau khi publish phải gửi Knox lại**; đổi tên hoặc status thì không. Vendor hiện dùng 3 cách: promotion simulator, test user group (dự phòng), special price report.

**KT:** simulator phổ biến nhất; test user group khi không dùng được simulator; Special Price Report để cross-check — CoE giữ cả ba. Vendor nói QA đính evidence rồi chuyển Review Setup và reporter phải comment green light; CoE: Shift Leader chuyển PRD SETUP, owner hand-back; không duyệt trước 23:59 hôm trước thì publish đúng giờ và comment (CM-13 §3.6). "L.V. Approval" không dạy. Promotion đang chạy mà đổi → Knox mới + QA mới trước lần publish kế (CM-05 §6.4).

### 2. Đọc rule trước khi chạy cart (BO-1)
Rule có 3 phần: **Properties** (code, website, rule group, priority, start/end), **Conditions** (sản phẩm/category đủ điều kiện, ngưỡng, Qualifying Sites cho EPP, customer group), **Actions** (% off, amount off, fixed price, gift). So từng giá trị với 6 giá trị trong internal check. Cẩn thận: condition "Category Price Threshold" tính **cả giỏ**, kể cả category không đủ điều kiện (VD tablet không đủ điều kiện vẫn giúp cart chạm ngưỡng nên promotion vẫn kích hoạt — kết quả sai, xem KB Promotion Rule Conditions).

### 3. Simulator và T1–T7
Simulator là giỏ hàng giả lập: chọn store, customer group, SKU + số lượng, coupon nếu có, ngày giờ giả lập, chạy; kết quả cho biết promotion nào áp dụng, giảm mỗi dòng và tổng cart — như thử voucher ở quầy trước ngày mở bán.
- **T1, T2** positive (1 SKU, rồi nhiều SKU); **T3** SKU ngoài danh sách; **T4** 1 phút trước start; **T5** 1 phút sau end; **T6** store/customer group không có quyền (VD EPP store); **T7** cùng cart thêm SKU đang có promotion khác.
- **Mẹo time zone:** đồng hồ simulator là giờ Malaysia (GMT+8) cho mọi market, nên quy đổi trước khi nhập. VN kết thúc 21:00 ICT thì mô phỏng 22:00; SG, MY, PH đã là GMT+8; AU, NZ sớm hơn vài giờ. Lỗi time zone trong rule thường lệch đúng 1 giờ (SG/MY/PH so với VN/TH/ID). VD: SG hết hạn 07-Dec 23:59 SGT nhưng Doer nhập theo ICT → T5 lúc 08-Dec 00:00 SGT vẫn còn giảm giá (MER-PRM-01 runbook).

| Run (số mô phỏng) | Input chính | Kết quả mong đợi |
|---|---|---|
| T1 | `vn`, regular, 1 × SKU-A (8,000,000), 02-Dec 10:00 ICT | PROMO01 áp dụng, giảm 800,000, tổng 7,200,000 |
| T2 | 1 × SKU-A + 2 × SKU-B (5,000,000) | Áp cho cả 3 unit, giảm 1,800,000, tổng 16,200,000 |
| T3 | 1 × SKU-C (3,000,000) | Không áp, tổng 3,000,000 |
| T4 | SKU-A, 30-Nov 23:59 ICT (start 01-Dec 00:00) | Không áp |
| T5 | SKU-A, 04-Dec 00:00 ICT (end 03-Dec 23:59) | Không áp |
| T6 | SKU-A, EPP store của `vn` | Không áp (rule chỉ B2C) |
| T7 | SKU-A + SKU-D có promotion khác | Theo internal check về stacking |

### 4. Negative test theo loại và coupon
- **BOGO:** cart chỉ có quà, không có main device → không giảm; quà hết hàng thì dùng quà ưu tiên kế tiếp; thử biến thể màu/dung lượng.
- **Tiered/BMSM:** dưới ngưỡng không giảm; trên tier cao nhất chỉ áp mức tối đa; vượt số lượng tối đa thì phần dư không giảm.
- **Voucher/coupon:** thử ngày sau khi hết hạn (hết 4/5 23:59 thì thử 5/5); bỏ SKU đủ điều kiện khỏi cart xem coupon còn áp không.
- **Coupon có 3 trường bắt buộc:** value, total uses, uses per customer. **Trống = không giới hạn.** Exposure = value × total uses; từ 10,000 USD là E4 (VD 25 × 500 = 12,500 USD → E4). Dùng lại code với cùng account khi limit 1 lần/khách phải bị từ chối. **Không bao giờ copy danh sách code ra file, comment hay PowerPoint.**

### 5. Test user group và tester group
Dùng khi promotion chỉ cho một nhóm khách hoặc simulator không dùng được. Kiểm cả hai chiều: account trong nhóm được offer, account ngoài nhóm không. Xem group của account: Customers › mở customer › tab General › Groups. Trên production tạo customer group là việc Tech; danh sách khách là PII nên subsidiary gửi qua email có mật khẩu. Setup còn trong tester group thì phải có subsidiary xác nhận mới gỡ restriction; **QA không bao giờ tự gỡ để đẩy live**, kể cả khi Merch yêu cầu.

### 6. Special Price Report, pre-test/live-test, trade-in
Report tồn tại trên staging và production; VN dùng Discount Row. Các bước: lọc requestor file và report cùng site group + cùng start/end → dán vào hai tab Requested/Uploaded của cross-check sheet → `VLOOKUP(SKU, Uploaded, cột giá, 0)` lấy giá đã upload, `EXACT()` so với giá yêu cầu → lọc FALSE và N/A. **N/A** thường là SKU thiếu trong report (kiểm filter site/date; vẫn thiếu thì hỏi Merch PIC upload có sót không) hoặc giá có ký hiệu `$` (bỏ rồi so lại). **FALSE** là chênh giá thật → ghi defect.
Pre-test/live-test: voucher, BOGO, Combo, BMSM → simulator trước, cart storefront sau. Special price → Special Price Report trước, sau đó Web Scrapping + ảnh PDP. Trade-in và text merchandising → so upload file rồi kiểm cart. Web Scrapping tối đa 199 SKU/lần; không đính file query lên Jira.
**Trade-in** (QAS-PRC-01, CM-13 §6.5): so file trade-in với bảng giá partner đã xác nhận — giá trade-in cao hơn giá partner là sanity hold (PS-09, MR-06 §2.2). Với model mẫu, thêm thiết bị mới + trade-in vào cart storefront, kiểm khấu trừ bằng giá trị trong file. Stacking: ôn rule group + priority ở G3.4.

## Quiz (đáp án)
1 SG chạy 01-Dec 00:00 → 07-Dec 23:59 SGT, cặp run bắt Doer nhập ICT → **C: 30-Nov 23:59 SGT và 08-Dec 00:00 SGT**. 2 BOGO, cart chỉ có quà → **A: không giảm**. 3 Coupon 20 USD, 1 lần/khách, total uses trống → **B: Defect, trống = không giới hạn** (PS-08). 4 Khi nào dùng test user group → **D: promotion theo customer group, hoặc simulator hỏng**. 5 Cross-check ra N/A → **A: kiểm filter site/date của report và định dạng giá**. 6 Voucher hết hạn 4/5 23:59 → **C: chạy simulator ngày 5/5, voucher không được áp**. 7 Promotion đã publish, Merch thêm 1 SKU vào condition container → **B: Knox mới, QA mới, chạy lại simulator**. 8 T7: SKU-D có promotion khác, internal check nói "no stacking" mà simulator áp cả hai → **B: Defect `RC-STK`**. 9 Trade-in file 300 USD, bảng partner 250 USD → **C: sanity hold PS-09, trả kèm lý do**.

## Practice
- **PR-QA2.1-1** (6', Backoffice staging chỉ xem): Marketing › Promotion Rules › tìm `TRAINING_` › mở `TRAINING_<tên>_PROMO01`, điền form 9 dòng (code, website, rule group, priority, start/end, publish status + version, conditions, actions, cách kiểm stock quà). Đóng không lưu. Pass: đủ 9 dòng; rule C2 có rule group `productPromotionRuleGroup`, priority 350, condition Qualifying products trỏ container X, action Percentage discount trỏ X, chưa publish live. Không có access: dùng ảnh in 3 tab.
- **PR-QA2.1-2** (14'): data bảng: website `vn`; SKU-A, SKU-B giảm 10%; SKU-C có hàng nhưng ngoài danh sách; SKU-D có promotion khác; hiệu lực D 00:00 → D+2 23:59 ICT; chỉ B2C. Việc: BO-1 so 6 giá trị; BO-2 xác nhận chưa live; chạy T1–T7; chụp màn hình mỗi run (thấy store + ngày giả lập); điền bảng Input/Expected/Actual; viết kết luận PASS (A.3) hoặc FAIL (A.4) trong Confluence nháp. Facilitator có thể cài lỗi (thiếu SKU-B, end date D+1). Pass: 7 run đủ 5 input + 3 output, tính giá khớp simulator, tìm ra lỗi cài và ghi đúng category/RC (thiếu SKU-B → Promotion logic `RC-SCP`). Simulator không chạy trên S2: facilitator phát 7 ảnh kết quả.
- **PR-QA2.1-3** (5'): Marketing › Coupon Management › Coupons › `TRAINING_<tên>_CPN`; ghi Active, dates, Max Redemptions per Customer/Total; chạy cart T1 có và không code; tính exposure (25 USD × 500; 20 USD total trống). Pass: đọc 1 lần/khách và 100 tổng; có code thì áp, không có thì không; 12,500 USD là E4; coupon thứ hai là Defect blocking vì không giới hạn; ảnh không lộ danh sách code.
- **PR-QA2.1-4** (5'): customers › account A (trong nhóm) › General › Groups xác nhận tên nhóm; kiểm offer bằng simulator (chọn customer group của A rồi B) hoặc đăng nhập frontend staging bằng A rồi B cùng SKU. Pass: A được offer, B không; ghi input/output; email account được che trong ảnh.
- **PR-QA2.1-5** (5', Excel): site `sg`, 01–07-Dec SGT. Requested: DEMO-SKU-201 1099; 202 899; 203 549; 204 299; 205 1599; 206 199. Uploaded: 201 1099; 202 899; 203 $549; 204 299; 205 1499; không có 206. Pass: 203 lỗi định dạng `$`, bỏ rồi khớp nên không phải defect; 205 chênh giá thật = Price defect `RC-ENT`; 206 thiếu trong report → kiểm filter, rồi hỏi Merch PIC, nếu upload sót thì `RC-SCP` (mã 205/206 là đáp án tham khảo, Lead xác nhận); kết luận FAIL; xóa file khỏi máy sau bài.
