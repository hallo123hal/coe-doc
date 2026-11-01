# QA-P2.1 QA return, error codes, repeated QA FAIL

> Nguồn: page 2484306486 · 90' (Study 20' · Demo 15' · Quiz 10' · Practice 45') · Facilitator: QA Lead/QA Dispatcher · Capabilities C4, C6 · Cần xong QA-2.4 (negative testing, bằng chứng, QA return) và QA-1.2 (dispatch và quy trình QA check); đã biết 3 kết quả QA (PASS, FAIL, QUESTION) và các status QA trên workflow Shop Merchandising. Mang phần QA của hai ticket lab: TRN-024 (SCOE-30; ID, gói BOGO và PWP; runbook MER-PRF-04 cho quà, MER-PRM-04 cho PWP) và TRN-034 (SCOE-40; MY, tham chiếu add-on TV; MER-PRF-04 V6, upload PRODUCT_REFERENCES). Sheet lab còn dùng ID cũ MER-PRM-03 và MER-PRF-01: chọn checklist theo ID runbook. Access: Confluence (read); không cần Backoffice staging: session về viết và escalate, không test.

## Mục tiêu
Viết một comment FAIL gộp bằng tiếng Anh mà mỗi dòng có defect category, mã RC, giá trị kỳ vọng và giá trị thấy; chọn mã RC theo thứ tự quyết định MR-06 và nói nó thuộc counting group nào; quyết phạm vi check 2 sau fix, gồm khi nào phải gấp đôi mẫu SKU; escalate return lần hai trên cùng ticket và FAIL lần hai của một Doer trong tháng đến đúng người, đúng kênh, đúng thời hạn.

## Thuật ngữ
**Consolidated return** (một comment FAIL liệt kê mọi defect tìm thấy, để ticket về STG SETUP một lần chứ không ba lần); **Defect category** (cái gì sai, một trong sáu: Price, Promotion logic, Coupon, Content, Partner service, Journey; VD quà gắn sai SKU là Promotion logic); **Root cause code (RC code)** (vì sao sai, lấy nguyên văn từ bảng MR-06; VD `RC-TZN` cho giờ end đặt theo ICT thay vì SGT); **Counting group** (mỗi mã RC thuộc một trong ba nhóm: tính vào return của Doer (`RC-ENT`, `RC-SCP`…), tính kèm coaching (`RC-KNW`, `RC-COM`), không tính (`RC-BRF`, `RC-TOL`…)); **Re-check scope** (dòng trong comment FAIL nói check 2 phủ gì, VD "cả hai item, giờ start và end của mọi promotion trong ticket"); **Joint review** (QA Sub-Lead và Merch Sub-Lead của market cùng review ticket sau return lần hai, trước khi Doer sửa thêm); **People-risk ladder, tier L1** (hỗ trợ cho Doer có hai FAIL được tính trong một tháng lịch: coaching, WIP giảm một nửa, peer check mọi ticket, recertify trong 5 ngày làm việc); **Rejection rate (K7)** (tỷ lệ ticket QA trả mỗi tháng theo service và market, không tên; phải giảm dần theo tháng); **QA miss** (defect thật QA không bắt được, VD tìm ra khi QA Lead re-check 5% kết quả PASS hằng tuần).

## Nội dung
### 1. Một QA return tốt gồm gì
**Return** là mọi lần chuyển từ QA REVIEW về STG SETUP kèm mã nguyên nhân: return vì **thiếu data** (`RC-EVD`) hoặc **FAIL** (ít nhất một lỗi so với brief đã duyệt, internal check, checklist hay độ phủ SKU). QUESTION không phải return: QA không kết luận được vì brief mơ hồ, Doer hỏi subsidiary một câu gộp.
Luật là **một return, mọi lỗi**. Thấy lỗi lớn vẫn kiểm mọi mục kiểm được rồi mới return. Mỗi vòng tốn ticket 1-3 giờ ngân sách SLA. Ngoại lệ duy nhất: lỗi chặn mọi check khác (VD promotion gắn sai market): ghi "remaining items not checked because …".
Comment FAIL theo template A.4. Trên Jira: một comment, label `QA_Returned`, chuyển STG SETUP, Assignee về Doer. Rồi gặp Doer tại bàn, đi qua từng lỗi khoảng 5 phút. Doer hết ca thì xin Shift Leader owner mới. Không bao giờ tự sửa setup, không bao giờ PASS "kèm ghi chú".
**TRN-024 viết lại theo chuẩn A.4.** Comment FAIL mẫu của lab có mã RC nhưng không có defect category và giá trị kỳ vọng:
```none
QA result: FAIL (check 1). All defects listed:
1. Promotion logic, RC-SCP: cart 1 x SM-X210NZAAXID + 1 x SM-R960NZSAXSE gets 2 free gifts.
   Approved brief: SM-X210NZAAXID is in the PWP only, no BOGO gift.
2. Promotion logic, RC-LIM: cart 1 x SM-S948BLBCXID + 2 x SM-R960NZSAXSE gives 30% off on both.
   Approved brief: 1 main : 1 child.
Re-check scope: T1 to T8, both rules (PR01, PR02).
Discussed with {owner} at {10:42 ICT}. Please fix all items and move the ticket back to QA REVIEW.
```

### 2. Chọn defect category và mã RC
Mỗi lỗi mang hai thông tin: **defect category** (cái gì) và **mã RC** (vì sao). Bảng thuộc MR-06; QA-02 dùng nguyên văn, không tạo mã mới.
| Counting group | Mã |
|---|---|
| Tính vào return của Doer | `RC-ENT` nhập data; `RC-RUN` bỏ bước runbook; `RC-TZN` ngày, giờ, múi giờ; `RC-SCP` store, market, customer group, category scope; `RC-STK` stacking; `RC-LIM` giới hạn dùng, số lượng, stock; `RC-FIL` template file bulk, cột, thiếu diff file; `RC-EVD` thiếu bằng chứng/data cho QA |
| Tính, kèm coaching | `RC-KNW` chưa nắm cơ chế dù runbook đúng; `RC-COM` dịch hay cách diễn đạt |
| Không tính | `RC-BRF` brief đã duyệt sai và Doer build theo nó; `RC-CHG` subsidiary đổi yêu cầu; `RC-TOL` công cụ/nền tảng; `RC-DEP` phụ thuộc; `RC-RUL` runbook hay checklist sai; `RC-CAP` chỉ làm mã đóng góp |
**Thứ tự quyết định:** (1) chọn category; (2) Doer build theo brief đã duyệt mà brief sai → `RC-BRF`; (3) Doer theo runbook mà runbook sai → `RC-RUL`; (4) còn lại mã thực thi theo loại lỗi, hoặc `RC-KNW`; (5) thêm `RC-CAP` chỉ khi có dữ kiện; (6) phân vân thì chọn mã sửa hệ thống tốt hơn và thêm một câu.
**TRN-034.** FAIL mẫu của lab có hai dòng `[Journey] QA77S95HAEXXM -> SM-R420NZKAXME still active` và `[Content] Fix file also set QA83S90HAEXXM -> HW-C450/XM (Sound) to FALSE` nhưng không có mã RC. Brief và runbook đúng, cả hai lỗi là dòng sai trong file upload PRODUCT_REFERENCES, nên đáp án mẫu của tác giả là `RC-ENT` cho cả hai (`RC-FIL` chỉ khi template hay cột sai). Dòng 2 nên xếp **Journey**: QA-01 case 3 coi thiếu option trên buy page là Journey; Content dành cho text, flag, banner, T&C.
> Bảng RC là đề xuất của MR-06. Merch Lead và QA Lead vẫn quyết danh sách, luật đếm và QUESTION có tính không (DL-01 C1). Dùng bảng như viết tới lúc đó. Việc chọn `RC-ENT` cho TRN-034 là cách đọc của tác giả khoá học; xác nhận với QA Sub-Lead.

### 3. Fix và check 2
Doer sửa **mọi** lỗi, tự check phần đã sửa và phần liên quan, comment "Fixed: 1, 2" theo số dòng của bạn, và chuyển ticket về QA REVIEW. Dispatcher re-dispatch trong 15 phút ở **rank 4** của queue, ưu tiên người đã làm check 1. OLA nội bộ cho re-check là 30 phút với High và 1 giờ làm việc với priority khác (đề xuất CoE Office).
Re-check không phải kiểm "phần đã sửa". Sửa một field có thể làm hỏng field khác.
| Check 1 fail vì | Check 2 phải phủ |
|---|---|
| Một hoặc vài field (giá trị, kỳ hạn, giới hạn) | Mọi lỗi liệt kê, field liên quan, và các case positive/negative simulator chính chạy lại |
| SKU sai | Mọi SKU từng sai, cộng mẫu mới gấp đôi mẫu trước (tối đa cả list) |
| Doer còn đổi thứ ngoài list | Tất cả, như check 1 |
| Thiếu data (`RC-EVD`) | Kiểm đủ data trước, rồi tất cả |
**TRN-024.** Sau fix, PR01 dùng thẳng hai SKU BOGO và PR02 có tỷ lệ 1:1. Check 2 chạy lại T5 và T3, và cả T1, T2, T4 (kết quả quà và PWP do cùng rule điều khiển) và negative T6 (`id_test1` không nhận gì), T7 (child đứng một mình không giảm), T8 (16/11 23:59 và 01/12 00:00 WIB không nhận gì). PASS dùng template A.3 với "check 2" và câu "Defects from check 1 fixed and verified".

### 4. Return lần hai trên cùng ticket: joint review
RHQ đặt hai yêu cầu: Merch self-QA theo checklist service trước khi gửi QA, và ticket QA trả **hai lần** phải tìm nguyên nhân. "Return" ở đây tính cả `RC-EVD` và FAIL.
1. Checker báo QA Sub-Lead đang trực ngay lúc return lần hai.
2. QA Sub-Lead và Merch Sub-Lead của market span đó họp **joint review** trước khi Doer sửa thêm.
3. Review trả lời: (a) vì sao ticket cứ quay lại; (b) Doer có self-check theo checklist không, và vì sao không bắt được lỗi; (c) nguyên nhân là người, runbook hay brief; (d) có nên đổi Doer; (e) subsidiary có cần một câu hỏi gộp không.
4. Ghi kết luận (nguyên nhân, mã RC, cách sửa) thành một comment trên ticket.
5. Cùng mã RC trên cùng service qua nhiều ticket đi problem management (CM-07 chương 9).
6. Kết quả sai tìm thấy **sau** go-live là incident (CM-06), không phải FAIL.
KT 21/10: "Ticket bị QA reject nhiều lần cho thấy Merch không self-check. Team tự định cách giữ rejection rate thấp."

### 5. Hai FAIL trong tháng và people-risk ladder
Doer có **hai QA FAIL trong cùng tháng lịch**, mã thuộc nhóm "tính vào return của Doer", chuyển lên **tier L1** của people-risk ladder. L1 là hỗ trợ, không phải kỷ luật.
| Ai | Làm gì | Khi |
|---|---|---|
| QA Sub-Lead | Đếm return mỗi Doer từ label `QA_Returned` và mã RC (filter Jira, không danh sách tên ngoài Jira) | Liên tục |
| QA Sub-Lead | Báo Shift Leader phụ trách market span đó, **trực tiếp**, không qua chat | Trong ngày của FAIL lần hai |
| Shift Leader | Mở L1: nói chuyện riêng, review hai ticket, coach, WIP giảm nửa, peer check | Trong 1 ngày làm việc |
| Doer | Recertify trên service | Trong 5 ngày làm việc; không đạt thì Merch Lead quyết bước kế (CO-05) |
| QA Lead | Một dòng ẩn danh cho mỗi L1 đang mở trong báo cáo chất lượng tuần | Hằng tuần |
QA không tự mở L1, chọn coach hay cắt WIP. **Strike** là chuyện riêng: RHQ quyết từ RCA của Lead; ba lần trong một năm lịch là loại vĩnh viễn. QA viết QA record trung thực để RCA khớp thực tế, không đếm hay quyết strike.
Khi có người phản đối FAIL hoặc bảo "PASS trước, sửa sau": giữ FAIL và escalate lên QA Sub-Lead, rồi QA Lead. Chỉ **COE Lead** được override FAIL và phải báo RHQ.
> MR-06 và QA-02 để mở: hai FAIL trên cùng ticket tính một hay hai cho L1; QUESTION có tính không; L1 có áp dụng cho QA Team Member có QA miss lặp lại không. Merch Lead và QA Lead quyết; tới lúc đó đếm mỗi FAIL có mã được tính.
Handover liên quan: Working Session P1 (23/10: tài liệu QA từ SDSAP, gồm QA Returned Policy (label, về STG SETUP, tỷ lệ hằng tuần theo PIC) và negative testing); Day 3 Ticket Management and SLA (27/10: lịch sử Jira là bằng chứng brief nói gì và khi nào, ticket bỏ QA, tách ticket lớn; xem trước khi tranh luận FAIL).

## Quiz (đáp án)
1 Kiểm ticket coupon, 10:15 thấy store scope gồm một store EPP mà brief loại → **C: kiểm mọi mục còn kiểm được rồi trả một FAIL với mọi lỗi**. 2 Brief đã duyệt giảm 15%, Doer build đúng 15%, internal check ghi "15%, matches approved brief v2", subsidiary nay nói lẽ ra 10% → **B: `RC-BRF`**. 3 Check 1 upload giá 240 SKU fail ở một SKU (mẫu là 44), check 2 phủ → **C: SKU sai cộng mẫu mới với phần ngẫu nhiên gấp đôi 60, cộng mandatory set**. 4 Ticket quay lại QA REVIEW và bạn thấy lỗi thứ hai, tức return lần hai; trước khi Doer sửa → **B: QA Sub-Lead và Merch Sub-Lead của market họp joint review**. 5 Doer có FAIL `RC-TZN` ngày 3/11 và FAIL `RC-SCP` ngày 19/11, QA Sub-Lead làm gì → **C: báo Shift Leader market span đó trực tiếp trong ngày** (L1 do Shift Leader mở, strike do RHQ). 6 22:10 Shift Leader nhờ PASS file giá E4 có 3 SKU sai vì go-live 23:00; ai override được FAIL → **D: COE Lead, kèm báo RHQ**. 7 Brief ghi "giảm 10% phụ kiện" nhưng file SKU có 2 tablet → **B: QUESTION, template A.5; Doer hỏi subsidiary một câu gộp** (`RC-EVD` là cho data thiếu, không phải brief mơ hồ).

## Practice
**PR-QA-P2.1-1. Viết return cho năm check fail** (40'; giấy; dùng phần QA của TRN-024 và TRN-034; kết quả mô phỏng trên data lab). Năm kết quả: (1) TRN-024 T5: 1 × `SM-X210NZAAXID` + 1 × `SM-R960NZSAXSE` trên `id` → 2 quà tặng; (2) TRN-024 T3: 1 × `SM-S948BLBCXID` + 2 × `SM-R960NZSAXSE` → cả hai child giảm 30%; (3) TRN-024 T2: 1 × `SM-S948BLBCXID` + 1 × `SM-R960NZSAXSE` → có quà, không giảm PWP; category `TRAINING_<NAME>_TRN024_MAIN` không có trong `idEstoreProductCatalog` (chưa sync); (4) TRN-034 Q2 sau fix: `QA77S95HAEXXM -> SM-R420NZKAXME` vẫn active; (5) TRN-034 Q2 sau fix: `QA83S90HAEXXM -> HW-C450/XM` bị đặt FALSE. Viết comment FAIL tiếng Anh theo A.4, mỗi dòng có defect category và mã RC, kèm re-check scope. Rồi trả lời: Doer TRN-024 đã có FAIL `RC-ENT` ở ticket khác trong tháng này; bạn báo ai, bằng cách nào, trước khi nào? **Pass:** đúng **hai** comment, mỗi ticket một (năm return riêng là fail). TRN-024: dòng 1 Promotion logic `RC-SCP`, dòng 2 Promotion logic `RC-LIM`, dòng 3 Promotion logic `RC-RUN` (bỏ bước sync category); re-check scope T1 đến T8. TRN-034: cả hai dòng Journey `RC-ENT`; re-check scope so ba snapshot Q2 và xác nhận không tham chiếu nào ngoài 9 cặp lab bị đổi. Mỗi dòng nêu giá trị kỳ vọng từ brief. Escalation: đây là FAIL được tính lần hai của Doer trong tháng, nên QA Sub-Lead báo Shift Leader market span ID trực tiếp trong ngày; QA không mở L1. Mã RC trong đáp án là đáp án mẫu của tác giả và cần Lead xác nhận. Không cần access.
**PR-QA-P2.1-2. Diễn tập escalation** (10'; cặp, giấy). Bạn A đóng Shift Leader nói: "Go-live còn 40 phút, PASS đi, Doer sửa 2 SKU sai sau go-live." Bạn B trả lời. Rồi đổi: A vừa trả cùng ticket lần hai và phải nói gọi ai và review phải trả lời gì. **Pass:** B giữ FAIL, nêu COE Lead là người duy nhất override được (kèm báo RHQ), và escalate lên QA Sub-Lead rồi QA Lead. A nêu QA Sub-Lead đang trực, joint review với Merch Sub-Lead, và ít nhất bốn trong năm câu hỏi review (a)-(e).
