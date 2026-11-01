# MER-1.2 Detailed Merchandising process from ticket to launch verification

> Nguồn: page 2483192027 · 90 phút (Study 35' · Demo 15' · Quiz 10' · Practice 30') · Talk + demo Jira, thực hành cặp; facilitator: Shift Leader (Sub-Lead) có kinh nghiệm KT · Tài liệu chính: MR-04 (giữ mở Appendix A: 13 template A.1–A.13). Cần xong G2.2, G2.3, G2.6, MER-1.1; chưa có Jira thì làm PR-1 trên form giấy 8 dòng (status, Assignee, comment).

## Mục tiêu
Thực hiện output + comment template của từng bước M1–M8; viết dòng internal check cho brief R3 trước khi build; quyết định đúng ở từng bước với Knox, subsidiary chưa duyệt lúc 23:59, ticket nhiều wave; phân biệt ticket thật sự urgent với ticket trễ do chính CoE.

## Thuật ngữ
**M1–M8** (8 bước CoE trên ticket Shop Merchandising, từ nhận ticket M1 đến LAUNCH VERIFICATION M8); **Template A.1–A.13** (13 template comment tiếng Anh ở MR-04 Appendix A; A.1 nhận ticket, A.4 "Published as aligned"); **NOT APPROVED** (status subsidiary dùng để từ chối brief; khác INVALID là hủy ticket); **Shortcut** (từ STG SETUP thẳng sang PRD SETUP khi service không có QA gate); **Wave** (một lần go-live trong ticket có nhiều promotion bắt đầu khác ngày); **Go-live check**; **Rework** (làm lại việc QA trả hoặc subsidiary đổi yêu cầu → ticket về STG SETUP).

## Nội dung
### 1. Bản đồ M1–M8

| Bước | Status | Ai | Phải xong | Template |
|---|---|---|---|---|
| M1 | APPROVED-ES → STG SETUP | Doer | Nhận ticket, rà priority | A.1 |
| M2 | STG SETUP | Doer | Internal check (R3), setup chưa live, tự test | A.10; A.2 nếu hỏi |
| M3 | QA REVIEW | QA Team | QA PASS/FAIL, evidence PowerPoint | kết quả QA |
| M4 | PRD SETUP | Shift Leader (+ Lead nếu E4) | Duyệt, gửi Knox | comment duyệt, A.13 |
| M5 | REVIEW SETUP | Subsidiary | Duyệt evidence; sau 23:59 vẫn publish | A.3, A.4 |
| M6, M7 | PENDING LAUNCH | Owner ca | Publish từng wave, QA lại production | A.7 |
| M8 | LAUNCH VERIFICATION | Doer + người check thứ hai | Go-live check, theo dõi order | Log |

### 2. M1 — nhận ticket và rà priority
Chuyển APPROVED-ES → STG SETUP rồi comment A.1: service, priority, go-live (giờ local + VN), owner, giờ update kế tiếp. Phần lớn ca TM trực intake làm bước này và đề xuất owner, Shift Leader xác nhận (MER-1.4). **Rà priority:** một promotion = một promotion rule (BOGO áp 10 SKU vẫn là 1); 2 promotion = Medium tạm; ≥3 = Low (MER-PRM-09); không tách/gộp ticket để đổi priority.

### 3. M2 — setup trên production *chưa live* và internal check
Cách làm theo loại việc: promotion → build rule, publish simulator, test; price/product → ngày hiệu lực tương lai hoặc bản Staged chưa sync; AEM/Shop App CMS → build trên author, check preview.
**Ghi internal check (A.10) trước khi build bất kỳ việc R3 nào** — một dòng gồm SKU, giá/discount, thời gian kèm time zone, site/store, stacking, usage limit, kết thúc bằng "Matches approved brief vX". Ví dụ DEMO-5101: "Internal check: 14 SKUs per brief sheet 1; buy 2 get 10% off; 01-Dec-2026 00:00 to 07-Dec-2026 23:59 ICT; site vn B2C; stacks with cart coupons per brief; no usage limit. Matches approved brief v1."
Brief thiếu/mâu thuẫn → hỏi subsidiary bằng 3 hành động của G2.2 + A.2; khi họ trả lời đưa ticket về STG SETUP ngay, lấy lại Assignee, tính lại deadline. Brief đủ thì không hỏi lại.

### 4. M3–M4 — QA REVIEW, duyệt và Knox
- **M3:** trước khi chuyển QA đính 4 thứ: brief; SKU file (>100 dòng kèm diff file); giờ go-live (local + VN); setup evidence (internal check + self-test). OLA QA: nhận trong 15'; ticket High có kết quả trong 30'; 1–2 item trong 2 giờ làm việc. **QA FAIL** → về STG SETUP với một comment liệt kê mọi lỗi. QA trả cùng ticket lần hai → Sub-Lead tìm nguyên nhân (vì sao lại trả, vì sao self-QA bỏ sót) và ghi lên ticket (CM-07 §3.3, CM-13 §6.4). Hai FAIL tính cho bạn trong một tháng → tier L1 của people-risk ladder (MER-3.1).
- **M4:** Shift Leader duyệt bằng comment "Approved by Shift Leader [shift], [time]. Checks: brief, runbook, evidence, QA PASS, internal check, sanity, rollback, Knox [sent/approved/N.A.], E4 = No." (thêm Merch Lead nếu E4). Knox cho giá & promotion phải gửi theo path trong brief trước khi publish live; Shift Leader kiểm đã/sẽ gửi, path & giờ gửi đã ghi trên ticket — không có là không duyệt. Trong Hybris, giá tạo PriceInfoChange ngay khi Save nên Knox giá có thể đi trước duyệt; promotion chỉ khởi Knox khi publish vào country module nên duyệt trước rồi Knox ngay sau. RHQ chưa chốt thời điểm chính xác — theo Shift Leader. **Gửi Knox không đổi status**: ghi giờ & path bằng A.13 và theo dõi qua handoff note.

### 5. M5 — REVIEW SETUP và luật 23:59
Mời subsidiary review evidence bằng A.3, kèm giờ publish. 16:00 Shift Leader ca E lấy danh sách ticket go-live ngày mai còn ở REVIEW SETUP. Đến 23:59 giờ local subsidiary chưa duyệt → vẫn publish đúng giờ, comment A.4, chuyển PENDING LAUNCH. **Không publish nếu:** subsidiary vừa hỏi câu mới; brief vừa đổi; chưa có QA PASS; Knox chưa duyệt (báo Merch Lead).

### 6. M6–M8 — wave, go-live, launch verification
**Mỗi wave là một vòng riêng (M6, M7):** publish live → QA lại trên production → comment A.7 → trả ticket về PENDING LAUNCH; chỉ sau wave cuối mới sang LAUNCH VERIFICATION; **không tách ticket theo wave**. M8: với R3 người thứ hai check trong 30' (15' với E4) và theo dõi order mỗi 15' trong 2h (MER-3.1). CoE không tự CLOSE ticket; RHQ đóng ticket LAUNCH VERIFICATION không cập nhật >1 tháng.

### 7. Urgent, cần Tech, lỗi thường gặp
- Urgent (G2.6: A.5, label `LastMinRequest`): ticket last-minute thật vẫn đi QA nếu QA kịp; chỉ bỏ QA khi thật sự không kịp và vẫn giữ control tối thiểu (CM-05 §3.7, CM-07 §3.6). **Không phải urgent:** ticket trễ vì CoE xếp việc muộn (không bỏ QA; giải thích bằng A.9); QA FAIL sau giờ go-live (không go-live).
- Cần Tech: Merch còn việc → linked COEC + A.6; toàn bộ việc là của Tech → move ticket + A.11 (G2.2).
- Lỗi hay gặp: comment mà không đổi status khi nhận ticket; chuyển ON HOLD SUBS nhưng quên đổi Assignee; ON HOLD SUBS chỉ vì chờ Knox; tách ticket nhiều wave; subsidiary đã trả lời mà ticket vẫn ở ON HOLD SUBS.

### Điểm đáng nhớ từ KT
SLA "High 1 ngày, Medium 2, Low 3 ngày làm việc" là thực hành nội bộ của vendor cũ — hợp đồng là **High 4h, Medium 16h, Low 24h** theo status Jira. Intake chuyển STG SETUP và đề xuất owner (MO ca ngày, TM ca E/N), Shift Leader xác nhận. CoE chỉ nhặt ticket đã duyệt; NOT APPROVED không bao giờ tới CoE. "5 ngày làm việc không duyệt thì đóng" — CoE không tự INVALID vì requester im lặng (CM-05 §3.5). Chỉ dùng High/Medium/Low; Maintenance Request thuộc L2/L3 (CoE không nhận việc qua Maintenance Request). Link ticket liên quan bằng More › Link.

## Quiz (đáp án)
1 Ticket có 1 BOGO cho 10 SKU + 1 rule giảm 5% phụ kiện, không ảnh hưởng bảo mật, rủi ro <10k USD → **Medium (2 promotion)**. 2 Subsidiary comment "Confirmed" nhưng không đổi status/Assignee → **về STG SETUP, nhận lại ticket, tính lại deadline**. 3 Ticket 2 promotion bắt đầu 02/12 và 05/12, wave 02/12 đã live & check → **comment A.7, trả về PENDING LAUNCH chờ 05/12**. 4 23:30, REVIEW SETUP, subsidiary chưa trả lời, Knox chưa duyệt → **không publish; báo Merch Lead**. 5 Shift Leader vừa duyệt và Doer vừa gửi Knox → **giữ status; ghi giờ & path bằng A.13**. 6 16:30 phát hiện ticket go-live tối nay bị quên chưa build → **không phải urgent; vẫn phải QA**. 7 Medium vào STG SETUP 10:00 T2, hỏi đúng lúc 11:00, trả lời 15:00 → **deadline mới 06:00 T3** (đã dùng 1h, còn 15h). 8 Ticket giá ở STG SETUP, hành động đúng "setup chưa live" → **đặt ngày hiệu lực tương lai hoặc sửa bản Staged chưa sync**.

## Practice
- **PR-MER-1.2-1** (15'): DEMO-5101 (14 SKU, buy 2 get 10% off, VN B2C, 01–07/12/2026; brief thiếu time zone của end date). Thực hiện: APPROVED-ES → STG SETUP + A.1; một câu hỏi gộp về time zone (A.2, ON HOLD SUBS, đổi Assignee); facilitator (đóng subsidiary) trả lời "ICT" → về STG SETUP; viết A.10; chuyển QA REVIEW; comment Knox A.13; sang REVIEW SETUP với A.3. Pass: mỗi lần đổi status đúng template; Assignee là subsidiary khi ON HOLD SUBS; gửi Knox không đổi status.
- **PR-MER-1.2-2** (8'): Medium 16h: vào STG SETUP 09:10; ON HOLD SUBS 10:40–14:10; STG SETUP 14:10–15:00; ON HOLD COE 15:00–18:00; QA REVIEW từ 18:00, còn đó lúc 20:00. Kết quả: ON HOLD COE tính, ON HOLD SUBS không; đã dùng **7h20** lúc 20:00; deadline **04:40 hôm sau**; 50% lúc 20:40, 70% lúc 23:52, 85% lúc 02:16, 95% lúc 03:52 (giờ lịch 24/7, quy tắc tạm CM-03 §2.1 tới khi RHQ trả lời).
- **PR-MER-1.2-3** (7'): (a) MY cần 500.000 multi-code coupon → viết A.6, mô tả COEC ticket (title, link, việc Tech làm), Merch ticket ở **ON HOLD COE** (không move, không ON HOLD SUBS), người tạo COEC theo dõi Tech; (b) 16:30 phát hiện ticket TH go-live tối nay bị bỏ sót chưa build → không gắn `LastMinRequest`, vẫn QA, báo subsidiary bằng A.9 kèm giờ đề xuất mới nếu cần.
