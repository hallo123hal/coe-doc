# MER-P4.3 BVT PIC routine

> Nguồn: page 2484240801 · 45 phút (Study 10' · Demo 5' · Quiz 5' · Practice 25') · Facilitator: Shift Leader/Sub-Lead · Capability C3 · Cần xong MER-3.3 (L1). Mang template tiếng Anh E1–E8 của CM-12 (Appendix A), các phần A–F của trang BVT, layout Excel trống với sheet `Test case` và `Defect` (giấy cũng được). Drill trên giấy; không cần staging (Merch không có HAC). Không có Confluence: facilitator in các mục CM-12.

## Mục tiêu
Lập kế hoạch một vòng BVT từ thông báo tới sign-off với mục tiêu ngày 1, ngày 2 khớp thời gian fix 2–3 ngày; viết market case có một expected result kiểm được bằng mười câu hỏi; ghi run, evidence, defect, blocker đúng chuẩn CM-12 ngay trong ngày; quyết định CoE có thể đề xuất sign-off không và viết comment kết E6 hoặc E7.

## Thuật ngữ
**BVT window** (ngày cố định RHQ đặt cho một vòng BVT, thường 3–5 ngày làm việc, báo trước tối đa 1 tuần; không thương lượng); **Lead PIC** (PIC tạo trang BVT, đăng comment bắt đầu và kết thúc, dẫn khi cả Merch và Tech cùng test); **Market case** (test case CoE thêm theo cách market thật sự dùng tính năng, ID `TC-COE-[market]-[number]`, VD `TC-COE-AU-01` (nhãn GST sau coupon)); **Run** (một lần chạy case; mỗi lần chạy lại là run mới với evidence mới, run cũ không bao giờ sửa/xóa); **Blocked** (case không chạy được vì môi trường, quyền truy cập, dữ liệu hoặc phụ thuộc; không bao giờ dùng để giấu lỗi); **Test report** (phần F trang BVT: case đã chạy, kết quả cuối và lịch sử, defect log; hạn trong 4 giờ làm việc sau khi case cuối pass, trong window); **User Acceptance** (người dùng cuối xác nhận tính năng đáp ứng yêu cầu, ghi trên trang BVT kèm vai trò, ngày, link).

## Nội dung
### 1. BVT trong một trang: luật RHQ
BVT (Business Validation Testing) kiểm enhancement trước go-live theo cách 8 market thật sự dùng. CoE làm hai việc: hỗ trợ subsidiary kiểm backend và cấu hình, và tự chạy end-to-end, thêm market case. Tám luật RHQ: window cố định và không thương lượng; BVT theo dõi trên enhancement ticket của development team; PIC là Merch hoặc Tech theo scope, QA Team không tham gia; sau kickoff (ngày 1) PIC comment "received, understood, starting" và tạo trang Confluence; file Excel cập nhật hằng ngày và upload để kiểm cuối ngày; go-live chỉ khi pass 100% (99% là không go-live); RHQ kiểm evidence; không sign-off đúng hạn thì enhancement không go-live. SEAO shared ticket nhân số case lên 8 lần.
BVT không phải ticket SLA của CoE nhưng chiếm 10% Composite SLA tháng: Pass Rate 6%, Report Completion 3%, User Acceptance 1%. Một test report trễ mất bằng ~44 ticket breach Resolution. Ghi PASS khi chưa test, dùng lại ảnh, giấu blocker là BVT non-compliance (RFP 3.4).

### 2. Trước window: thông báo, PIC, readiness, market case
- **Thông báo ngoài giờ làm việc:** Shift Leader ghi mục 9 handoff note (giờ, kênh, vai trò người gửi, ticket key, ngày window, scope một dòng), nhắn Merch Lead và Tech Lead trên `coe-leads` tag Coordinator trong 15', có thể trả lời RHQ một câu (E1), và mang dòng đó qua mọi lần bàn giao. Không gọi QA on-call, không gọi điện đêm, không bàn ngày hay scope.
- **PIC:** chọn trong ngày làm việc (trước 10:00 ngày làm việc kế nếu thông báo ngoài giờ), từ pool BVT-ready, có backup; chỉ chọn người đã có quyền truy cập.
- **Readiness checklist:** mở được enhancement ticket, tạo được trang và upload Excel; đăng nhập được môi trường test với test account mỗi market, store, customer group; đã đọc case của development team; Excel đã chuẩn bị với market case nháp; biết giờ họp, nơi upload và BA phía Spoke; tải ca đã giảm. Thiếu quyền hay test account là blocker, báo cùng ngày.
- **Market case:** duyệt mười khía cạnh (ngôn ngữ, tiền tệ, nhãn thuế và giá, time zone, kênh và store, customer group, giao hàng, order và payment, stacking, kênh hiển thị và sản phẩm). Mỗi case có ID, tiêu đề một câu, market, store và group, precondition, bước đánh số, một expected result, nguồn và lý do. Đề xuất ở kickoff, muộn nhất ngày 1.
**DEMO-7001 (mô phỏng):** ô nhập coupon ở cart và khối totals thay đổi ở checkout cho SG, MY, AU; 28 case của development team. PIC soạn 6 market case (GST ở AU, EPP ở SG, member MY, làm tròn số tiền, stacking, Shop App SG): `TC-COE-AU-01. GST label kept after coupon at cart and checkout.` Expected: tổng giảm 50 AUD; "incl. GST" hiện ở cart và checkout.

### 3. Trong window: nhịp hằng ngày
Fix mất 2–3 ngày nên chạy mọi case một lần trong nửa đầu window. Window 4 ngày: ≥50% ngày 1 và 100% cuối ngày 2. Thứ tự: case rủi ro cao (tiền, order, payment), market case, case nhiều bước, rồi UI đơn giản.
| Giờ (ICT) | Việc |
|---|---|
| 08:00 | Đọc comment, trạng thái defect, fix đã deploy; lên kế hoạch ngày |
| 08:30–15:30 | Chạy case; ghi evidence ngay sau mỗi case; retest fix cùng ngày fix lên môi trường test |
| 13:30 | Coordinator kiểm giữa ngày |
| Trước 15:30 (16:30 SGT) | Excel đã cập nhật và upload; phần D daily progress xong; mọi evidence đã upload |
| Nếu RHQ đặt | Cuộc họp 15' cuối ngày |
Ba thứ không bao giờ để cuối: evidence (ngay sau mỗi case), defect (trong Excel cùng ngày, mục tiêu trong 1 giờ làm việc), blocker (báo ngay trên kênh). Trạng thái case: Not run, Pass, Fail, Blocked. Chú thích evidence: `Case ID | Run | dd-Mon hh:mm SGT | Environment | Market store | Result`; chỉ chụp trên CoE workstation, upload thẳng vào trang BVT, xóa bản local; chỉ test account; không công cụ AI.
**Khi case fail:** chạy lại đúng các bước; ghi Fail kèm evidence; thêm dòng defect (`DEF-nn`, tiêu đề `[enhancement code] [market] actual result`, case ID, môi trường, bước, expected/actual, evidence, severity, impact); ghi mã defect lên dòng case và đăng comment defect (E5); upload Excel; báo BA phía Spoke; theo dõi hằng ngày. Retest: chạy case fail và các case liên quan như một run mới.

### 4. Báo cáo và sign-off
Phía CoE chỉ đề xuất sign-off khi 100% case đã chạy pass, không case Blocked hay Not run, defect log đã đóng, test report đủ, User Acceptance đã ghi. PIC đề xuất, Lead của scope xác nhận, RHQ sign-off cuối và quyết go-live. Không đề xuất sign-off khi còn case Fail, Blocked hay Not run; không ký thay team khác; không nộp test report trước khi Lead review.
**DEMO-7001:** Thứ Năm 10:30 fix cho `DEF-02` tới; retest cộng 2 case liên quan pass; 34/34 pass. 14:00 ghi User Acceptance; 15:00 test report, Lead review; 15:30 comment kết E6:
```
BVT result for DEMO-7001: all 34 test cases passed on the last
run (2 defects logged and fixed: DEF-01, DEF-02).
Test report: [link]. User acceptance: confirmed by [role] on [date].
The Ops CoE proposes sign-off. Final sign-off and the go-live decision
are with RHQ.
```
Nếu 15:00 Thứ Năm `DEF-02` chưa có fix (ETA thứ Hai tới): 33/34 pass, không sign-off; viết E7 với sự kiện; không ai xin gia hạn hay "conditional go-live"; Market Owner comment lên từng ticket promotion 12.12 phụ thuộc coupon mới rằng chưa go-live được.
> RHQ chưa đưa template trang BVT và test report, template Excel và luật đặt tên, giờ họp cuối ngày, hay ai ký User Acceptance (CM-12 §4.6 chờ quyết). Tới đó theo CM-12: đính phiên bản Excel mới có ngày mỗi ngày và giữ bản cũ. BVT non-compliance có tính strike hay không cũng còn mở (CM-12 §1.5).

## Quiz (đáp án)
1 RHQ gửi thông báo BVT Thứ Sáu 20:15 ICT cho window bắt đầu Thứ Hai; bạn là Shift Leader ca tối → **C: ghi mục 9 handoff note, nhắn cả hai Lead trên `coe-leads` tag Coordinator trong 15', trả lời RHQ một câu, mang qua các lần bàn giao** (không gọi QA on-call, không xin dời window). 2 Window 4 ngày bắt đầu Thứ Hai; fix 2–3 ngày; mục tiêu chạy mọi case lần đầu → **A: 100% cuối Thứ Ba (ngày 2), ít nhất 50% ngày 1**. 3 Market case viết đúng chuẩn → **B: "TC-COE-AU-01. GST label kept after coupon at cart and checkout. AU, B2C, logged-in test account; one product, one valid 50 AUD coupon; steps 1-4; expected: total reduced by 50 AUD and 'incl. GST' shown in cart and checkout."** 4 Test account EPP SG không có, 2 case không chạy được → **C: Blocked kèm lý do và giờ báo; Coordinator báo RHQ ngay (E8)**. 5 Development team nói case fail là "by design" → **B: xin xác nhận bằng văn bản trên enhancement ticket hoặc trang BVT, link vào dòng case, nêu với RHQ nếu market vẫn bị ảnh hưởng**. 6 Thứ Năm 15:00, ngày cuối: 33/34 pass, `DEF-02` ETA thứ Hai → **D: không sign-off; comment kết E7 với sự kiện, Lead review; RHQ quyết**.

## Practice
**PR-MER-P4.3-1. Drill BVT DEMO-7001** (25'; drill giấy từ CM-12 ch.9, nhóm 2–4 người mỗi người một vai: Shift Leader ca tối, Coordinator, Merch PIC, Market Owner AU). Facilitator đọc đề: Thứ Sáu 04/12/2026 20:15 ICT, BVT cho `DEMO-7001` (ô coupon ở cart, khối totals checkout thay đổi), SG, MY, AU, window Thứ Hai 07/12 → Thứ Năm 10/12, 28 case, peak 12.12 vào Thứ Bảy, tải ca D Merch 88% trước BVT. Viết từng hành động kèm giờ và owner: ghi nhận tối Thứ Sáu; ai chọn PIC và khi nào; kế hoạch tải Thứ Hai; kế hoạch từng ngày kèm market case; chuyện xảy ra khi Thứ Hai 2 case fail và 1 blocked, Thứ Ba account EPP vẫn thiếu; comment kết cho 34/34 pass, và nhánh E7 cho 33/34. **Pass:** thỏa tiêu chí CM-12 §9.4: mục 9 có giờ, kênh, ticket key, ngày và scope, cả hai Lead được nhắn trong 15' và mang qua bàn giao; không gọi QA on-call, không xin đổi ngày; hai PIC theo scope với backup từ pool BVT-ready và Lead PIC rõ; mọi case chạy xong cuối Thứ Ba, defect vào Excel cùng ngày, Excel upload hằng ngày, run fail được giữ; kế hoạch có dòng hỗ trợ subsidiary và market case của CoE; chỉ đề xuất sign-off khi 34/34 kèm User Acceptance; nhánh E7 nêu sự kiện và Market Owner báo các ticket 12.12 phụ thuộc. Không cần truy cập hệ thống.
