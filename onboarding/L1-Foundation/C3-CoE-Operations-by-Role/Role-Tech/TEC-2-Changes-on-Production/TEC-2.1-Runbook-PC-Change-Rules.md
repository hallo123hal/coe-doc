# TEC-2.1 Runbook catalogue, PC ticket, change rules

> Nguồn: page 2483224727 · 75 phút (Study 25' · Demo 10' · Quiz 10' · Practice 30') · Lecture + bài phân loại theo cặp; facilitator: Tech Lead · Tài liệu chính: TC-05. Cần xong G2.6, TEC-1.2; thực hành trên giấy hoặc trang Confluence nháp, không cần Jira.

## Mục tiêu
Đọc một dòng catalogue runbook và nói change có cần PC, second check, Tech Lead review không; phân loại 10 request bằng bảng quyết định 12 dòng của TC-05; viết PC ticket đầy đủ (đổi gì, vì sao, scope, kết quả staging, rollback, run window); chọn đúng đường duyệt RHQ cho ImpEx/Groovy, cronjob mới, đổi cấu hình Back Office.

## Thuật ngữ
**Runbook catalogue** (bảng service Tech ở TC-05, mỗi dòng có service code, runbook và 3 cột control); **Repeat use** (Standard runbook / ImpEx template / New each time); **Self-QA** (control lớp 1: Doer check trên staging với 5 câu hỏi); **Tech Lead review** (lớp 3: Tech Lead duyệt nội bộ việc rủi ro cao và mọi fix P0/P1 trước khi gửi PC); **Idempotent** (chạy lần hai không gây thay đổi thêm; "đặt status = CANCELLED" là idempotent, "cộng 500 Rewards point" thì không); **Irreversible** (không hoàn tác được, VD order đã đẩy sang NERP); **Safe stop**; **Simple / Advanced ImpEx** (hai mức RHQ cho data-fix; người duyệt đầu tiên quyết mức); **HQ GMO** (cấp duyệt HQ cho thay đổi lớn: catalog mới, 3PD mới, payment mode mới, cronjob mới).

## Nội dung
### 1. Catalogue runbook và bảng quyết định
Nhắc lại G2.6: mọi Tech change production cần PC do Oliver Leung duyệt — kể cả việc 5 giây và rollback. Catalogue ở TC-05 §1.3; service code `TEC-XXX-NN`, runbook `RB-TEC-XXX-NN`. Mỗi dòng có 3 cột control: **PC ticket** (Yes / No / Depends on the fix); **Another set of eyes** (Mandatory / Mandatory + TL / When unsure); **Repeat use**. VD ORD-02 (hủy order): Yes / Mandatory / Standard runbook; CFG-02 (payment/delivery mode): Yes / Mandatory + TL; ORD-01 (điều tra lỗi order): No vì chỉ đọc.

| Việc | PC | Ghi chú |
|---|---|---|
| Chạy trên staging | Không | |
| Xem Back Office, đọc log | Không | |
| FlexibleSearch chỉ đọc để điều tra 1 ticket | Không | Ghi lý do lên COEC |
| Report, historical data, đổi người nhận cronjob report | Có | PUMI duyệt trước rồi PC |
| Nhờ team khác (access, account) | Không | ON HOLD ES |
| Maintenance Request cho SDS India | Không | SYSTEM SUPPORT |
| Nút action trên order: re-send NERP, cancel, return | Có | Second check bắt buộc |
| Tạo/sửa/xóa record: coupon, user group, access code, domain | Có | Kể cả việc 5 giây |
| Cấu hình Back Office: site, base store, payment mode, quota | Có | Payment mode, base store: thêm Tech Lead review |
| ImpEx/Groovy trên production | Có | Kể cả script chỉ đọc và file dùng lại |
| Chạy lại cronjob, sync tay | Có | Không hoàn tác; chỉ Tech; Merch/QA không bao giờ chạy cronjob |
| Rollback | Có | Viết kế hoạch rollback trong PC gốc; chạy rollback có cần duyệt mới không còn chờ RHQ (CM-07 §3.7) — tới khi RHQ xác nhận, chỉ chạy rollback khi Oliver duyệt rõ ràng |

Ba dòng hay sai: đọc data để điều tra không cần PC; report mới/người nhận mới/data lịch sử cần PUMI rồi PC (thêm/bớt field không-PII không cần PUMI nhưng vẫn PC); rollback cũng là change cần PC.

### 2. Ba lớp control nội bộ trước khi gửi PC
- **Lớp 1 – self-QA trên staging:** 5 câu: đúng task? đúng scope? idempotent? rollback chạy được? có làm hỏng thứ khác?
- **Lớp 2 – another set of eyes:** một Tech Team Member khác, có certification **L2/L3** cho service đó; bắt buộc với ImpEx/Groovy mới và mọi change đụng price, order, payment, access. Checker kiểm 5 điểm: scope, số record, data trước/sau, header line PC + COEC, kế hoạch rollback. Comment mẫu: "Second check done by [name]: scope, record count, rollback verified on staging. OK to raise PC ticket."
- **Lớp 3 – Tech Lead review:** việc rủi ro cao (payment mode, base store, NERP, FI, access rule, External SSO, bulk data fix, sửa order bằng script) và mọi fix P0/P1; ngoài giờ do on-call layer 1 làm.
- **Không tìm được checker thì không gửi PC.** Doer, Checker, Approver là 3 người khác nhau; QA Team không QA việc Tech.

### 3. Viết PC ticket, rollback, safe stop
Nội dung PC (template đề xuất, TC-05 §3.4): Summary `[PC] [Market] [Short change] (COEC [number])` (VD `[PC] [SG] Re-push 2 orders to NERP (COEC-DEMO-7520)`); What; Why; Scope (danh sách code chính xác + số lượng, không PII); screenshot trước thay đổi (ẩn PII) và kết quả staging hoặc ghi "repeat-use"; file script có header + các control nội bộ đã làm; rollback hoặc "irreversible" kèm lý do và cách giảm rủi ro; run window theo ICT & SGT, ai chạy, các check sau khi chạy.
Có việc không hoàn tác được (đẩy order sang NERP, hủy order, return, chạy lại cronjob) → kiểm từng record trước khi chạy. **ImpEx hỏng giữa chừng:** dừng, không chạy lại cả file, ghi các dòng đã vào, báo Tech Lead (ngoài giờ: on-call layer 1), chỉ tiếp tục trong scope PC. PC là *quyền* hành động, không phải nghĩa vụ: requester rút yêu cầu thì không chạy dù đã duyệt; Oliver hỏi hay từ chối thì COEC về IN PROGRESS để bổ sung, gửi lại thì sang ON HOLD HQ. Lỗi kinh điển: viết `[mode=replace]` thay vì `[mode=remove]` để gỡ một user group → ImpEx báo "0 errors" nhưng xóa hết các group khác — **"0 errors" không có nghĩa kết quả đúng**, luôn đếm lại record sau khi chạy.

### 4. Đường duyệt RHQ cho ImpEx và scripting (07 Impex/Scripting)
**Simple:** RHQ D2C Platform Head. **Advanced:** thêm L2/L3 và Tech Lead hoặc Spoke SA. **Thay đổi lớn** (catalog mới, 3PD mới, payment mode mới, ENH deploy ngoài commit): thêm HQ GMO. Luôn đính bằng chứng test staging; không test được thì ghi lý do trong PC. **SEAO không có post-approval**: khẩn cấp thì tạo PC ngắn, nhắn Oliver trên Mattermost và chỉ chạy sau khi duyệt (CM-13 §9.5). Tạo account bằng ImpEx *không* theo đường này mà qua AUTEU. Cronjob mới và đổi cấu hình Back Office có đường riêng (TEC-2.3).

### 5. Freeze, peak, strike
Trong cửa sổ freeze cần **hai duyệt riêng**: duyệt ngoại lệ ghi trong thân ticket *và* PC. Timeline peak: T-14 lập danh sách change; T-14→T-7 chuẩn bị & gửi PC; T-2 mọi PC đã duyệt; D chạy; T+1 healthcheck. Strike (G2.6, CM-13 ch.17): hai ca quan trọng nhất với Tech trong danh sách breach RHQ là chạy ImpEx update không duyệt và đổi sync property không có PC.

## Quiz (đáp án)
1 Gỡ một user group khỏi account trong Back Office (~5 giây) → **vẫn cần PC như mọi data change production**. 2 Another set of eyes cho ImpEx sửa order status → **Tech Team Member khác có L2/L3 cho service đó**. 3 Hành vi KHÔNG nằm trong 3 hành vi luôn bị strike → **promotion sai sau code deploy của dev team** (lỗi hệ thống). 4 PC duyệt cho 3 order, lúc chạy thấy order thứ 4 cùng lỗi → **chỉ chạy 3 order; mở PC mới cho order thứ 4**. 5 Payment mode mới tạo bằng ImpEx theo 07 Impex/Scripting → **Platform Head, L2/L3, Tech Lead/Spoke SA, rồi HQ GMO**. 6 Hybris đang hard freeze, MY cần thêm payment mode → **ngoại lệ + control rủi ro cao + PC**. 7 Requester rút yêu cầu sau khi PC được duyệt → **không chạy; COEC sang INVALID (Withdrawn)**. 8 "Is it idempotent?" trong self-QA kiểm → **chạy lần hai không gây thay đổi thêm**.

## Practice
- **PR-TEC-2.1-1** (giấy, cặp, 12'): với 10 request, ghi cần PC không, PUMI không, second check bắt buộc không, cần Tech Lead review không, COEC chờ ở status nào. Đáp án (TC-05 §1.4, 1.5, 4.2): (1) hủy 2 order SG → PC, second check, ON HOLD HQ; (2) FlexibleSearch chỉ đọc 1 order → không PC, ghi lý do, ở IN PROGRESS; (3) thêm người nhận cho cronjob report TH → PUMI rồi PC; (4) thêm EPP domain bằng file repeat-use IMP-TEC-02 → PC, second check, header line, chỉ được bỏ kết quả staging; (5) đổi EPP quota → PC, second check khi chưa chắc; (6) reset password Back Office → không PC, ON HOLD ES; (7) chạy lại cronjob áp giá AU → PC, second check vì đụng giá; (8) payment mode mới cho MY → PC, second check, Tech Lead review, RHQ duyệt tới HQ GMO; (9) rollback ImpEx coupon → PC, second check vì đụng giá; (10) ẩn payment method lỗi lúc 02:00 trong P0 → PC, second check (ban đêm áp cho mọi emergency change), Tech Lead review qua layer 1, nhắn Oliver vì P0. Pass ≥9/10 và đúng dòng (2), (3), (6), (8).
- **PR-TEC-2.1-2** (18'): case DEMO COEC-DEMO-7520, SG, P2: order DEMO-ORD-7701 và 7702 export NERP FAILED chưa có số NERP; DEMO-ORD-7703 đã có số NERP. Viết PC theo template §3.4 (Summary, What, Why, Scope, Before, Staging result, Script dòng 1 là header, Internal checks, Rollback, Execution window ICT & SGT), comment "PC ticket pending" trên COEC và comment second-check. Pass: scope chỉ 2 order và nêu lý do loại 7703 ("already in NERP, not retry-safe"); rollback ghi "irreversible" + cách giảm rủi ro (kiểm từng order chưa có NERP number ngay trước khi chạy); không PII; người khác đọc không cần hỏi lại.
