# TEC-1.4 Tech on-call

> Nguồn: page 2483191855 · 45 phút (Study 15' · Demo 10' · Quiz 10' · Practice 10') · Lecture + role play cuộc gọi nửa đêm; facilitator: Tech Lead · Tài liệu chính: TC-04. Cần xong TEC-1.3, G2.5; không cần hệ thống, thực hành giấy theo cặp.

## Mục tiêu
Nêu ai được gọi ở phút 0/10/15/20 và target phản hồi on-call; làm phone assessment (4 điểm, 8 câu hỏi, quyết định, 6 chỉ dẫn); sắp 10 bước emergency change và nêu việc được phép khi chờ Oliver duyệt; soạn thông báo Critical đầu tiên cho RHQ đúng hạn với giờ ICT/SGT; nói ai quét COEC NEW ngoài giờ Tech, nhịp bao lâu, việc nào giao ca 04:00.

## Thuật ngữ
**Layer 1** (một lead — Tech Lead, Sub-Lead A hoặc B — giữ on-call cả tuần; là Tech Incident Manager ngoài giờ; "layer" là vai on-call, không phải ca Level 1 hay L1 certification); **Layer 2** (Team Member trong tuần Level 2 cùng team; Doer, chạy staging, nháp PC); **On-call week** (08:00 T2 → 08:00 T2 sau); **Phone assessment** (5 bước layer 1 làm khi nhận cuộc gọi để quyết severity trước khi vào trung tâm); **Emergency change** (change khẩn trong incident, vẫn cần PC duyệt trước khi chạy); **Containment** (hành động giảm tác động không cần Tech change, VD Merch tắt promotion sai); **On-call log** (trang Confluence Samsung ghi mọi cuộc gọi & quyết định ban đêm).

## Nội dung
### 1. Giờ on-call, COEC NEW ban đêm, ba luật bất biến
On-call Tech: 19:00–04:00 T2–T7, cả Chủ nhật (tới 04:00 T2) và ngày lễ chung của 8 market; khối dài nhất 19:00 T7 → 04:00 T2 = 33 giờ. Ngoài giờ Tech, COEC vẫn là việc Tech: on-call layer 1 quét dashboard COEC NEW **mỗi 5' khi ở workstation**, chuyển ASSIGNED và xử lý theo runbook; việc không gấp giao ca T4 04:00 qua on-call log. Shift Leader Merch ở trung tâm quét cùng filter mỗi 5' và gọi layer 1 ngay khi có Tech P0/P1, **không nhận COEC** (CM-04 §5.6, CM-06 §4.2, CM-08 §1.3).
Ba luật không đổi dù 02:00: **không remote**; **không change production nếu chưa có PC duyệt**; CoE giữ ownership khi chờ SDS India hay Oliver. Ngoài trung tâm on-call chỉ nghe Shift Leader đọc ticket và chỉ dẫn bằng giọng nói — không mở Jira, email, Mattermost, Backoffice trên điện thoại, không nhận screenshot.

### 2. Hai layer và call tree
Ba lead luân phiên, mỗi người giữ layer 1 một tuần trong ba.

| Hạng mục | Ai/Gì |
|---|---|
| Layer 1 | Một lead/tuần; IM ngoài giờ; đồng ý nội bộ cho fix P0/P1; nhắn Oliver; liên hệ SDS India; quét COEC NEW mỗi 5' khi ở workstation |
| Layer 2 | TM tuần Level 2 cùng team; Doer, staging, nháp PC & Maintenance Request; không là IM, không tự xác nhận severity, không nhắn Oliver trừ khi được yêu cầu |
| Trả lời cuộc gọi | ≤15' kể từ cuộc gọi; không trả lời là vi phạm quy trình |
| Xác nhận severity | ≤30' từ T0 |
| Có mặt tại trung tâm | ≤60' từ cuộc gọi (ra khỏi nhà trong 10') |
| Thông báo Critical đầu tiên | ≤30' từ T0; layer 1 duyệt nội dung trước phút 25 |
| Thông báo High đầu tiên | ≤2h, update mỗi 2h |
| RCA Critical | 48h (tối đa 72h) |

**Call tree** bắt đầu từ cuộc gọi đầu của Shift Leader: phút 0 gọi layer 1 (không nghe thì gọi lại 1 lần trong 10'); phút 10 gọi layer 2 (layer 2 nghe máy thì call tree *chưa dừng*, vẫn phải tìm lead); phút 15 gọi Tech Lead (nếu Tech Lead là layer 1 tuần đó thì gọi Sub-Lead A – Deputy); phút 20 gọi hotline SDM. Gọi điện, không nhắn tin; mở đầu bằng 4 điểm: ticket, market, impact, cần gì.

### 3. Phone assessment và severity Tech
Khoảng 15': (1) nghe 4 điểm (2'); (2) hỏi 8 câu: triệu chứng; từ khi nào; phạm vi (tất cả hay một phần khách, market nào, kênh nào: B2C, EPP, SMB, Shop App); order còn vào không; vừa đổi gì không; có phải lỗi đã biết không; data có bị lộ không; RHQ đã biết/có bridge chưa; (3) quyết severity (3'), phân vân chọn mức cao hơn; (4) 6 chỉ dẫn: Shift Leader làm IM tạm; mở bridge; gọi layer 2, báo COE Lead & SDM nếu Critical; nháp thông báo; tìm containment không cần Tech change; không ai đụng cấu hình Tech; (5) ghi on-call log.
**Severity Tech** (bổ sung bảng G2.5): P0 — cả market không đặt hàng/thanh toán/mở site/đăng nhập được, hoặc Shop App sập; lộ data; mất >500 USD. P1 — mất 100–500 USD; một phần khách bị ảnh hưởng; một payment method lỗi; khách bị trừ tiền không có order; order hàng loạt không tới NERP.
Thông báo RHQ trên Mattermost: Critical gửi lần đầu ≤30' từ T0 (target nội bộ; RFP cho 2h), update mỗi 30'; layer 1 duyệt nội dung trước phút 25; nhịp update không dừng khi COEC ở ON HOLD HQ hay SYSTEM SUPPORT; không bao giờ viết "SLA paused" trong thông báo.

### 4. Emergency change 10 bước
1) Quyết định fix gì. 2) Viết rollback trước. 3) Chạy trên staging (bắt buộc với ImpEx/Groovy mới). 4) Self-QA (COEC ở QA REVIEW). 5) Người thứ hai có L2/L3 cùng service check — ban đêm áp dụng cho *mọi* emergency change. 6) Chuẩn bị PC. 7) COEC sang ON HOLD HQ comment "PC ticket pending" (CM-08 Template 18). 8) Layer 1 nhắn Oliver trên Mattermost từ workstation trung tâm (chỉ P0/P1). 9) Thông báo mọi người trên bridge. 10) Oliver duyệt và tự đưa COEC về IN PROGRESS; chạy theo checklist; checker xác nhận.
**SEAO không có post-approval**: không gì chạy trên production trước khi Oliver duyệt, không có phần PC nào "hoàn tất sau" (CM-13 §9.5). Trong lúc chờ mà khách vẫn bị ảnh hưởng: phút 0–15 tìm containment không cần Tech change (VD Merch tắt promotion/ẩn SKU qua workflow Shop Merchandising, hướng khách sang kênh còn chạy); phút 15 nhắc Oliver một lần và gọi COE Lead. **Cấm:** "chạy trước, hỏi sau"; nhờ SDS India chạy hộ; nhắn Oliver nhiều lần hoặc qua kênh cá nhân.

### 5. Playbook P0, bàn giao 04:00, nghỉ bù
Ba playbook P0: không đặt hàng được (đặt test order từng bước để tìm điểm gãy; "rollback trước, fix sau"); lỗi payment (test từng payment method; đề xuất ẩn method lỗi — RHQ đồng ý, PC cũng gồm bước bật lại); site không truy cập được (kiểm từng loại trang, chuẩn bị evidence pack sớm). 30' vẫn chưa thấy nguyên nhân phía CoE → mở Maintenance Request cho SDS India. Sau khi khôi phục theo dõi order mỗi 15' trong 2h.
Bàn giao 04:00 cho ca T4: đọc on-call log, handoff note on-call 11 section và section 9 handoff Merch; PC duyệt qua đêm làm trước; incident còn mở lúc 04:00 thì layer 1 vẫn là IM. Chủ nhật layer 1 có mặt ở trung tâm lúc 09:00 và 17:00 để kiểm queue. **Nghỉ bù:** làm >2h trong khoảng 22:00–06:00 thì nghỉ ≥8h trước ca kế.

## Quiz (đáp án)
1 Tech Lead giữ layer 1 tuần này; 01:00 Shift Leader gọi 2 lần không ai nghe; 01:10 layer 2 không nghe → 01:15 gọi **Sub-Lead A (Deputy)**. 2 Critical có T0 23:10 → thông báo RHQ đầu tiên muộn nhất **23:40**. 3 Lúc 02:00 hành động không cần PC → **Merch tắt promotion sai trong workflow của họ**. 4 Layer 1 đang ở nhà khi có cuộc gọi P0 → **chỉ nghe và chỉ dẫn bằng giọng nói**. 5 On-call 23:00–02:30 T3, sáng T4 xếp Level 2 → sớm nhất **10:30**. 6 Chờ Oliver duyệt PC cho P0, khách vẫn bị ảnh hưởng → **tìm containment không cần Tech change; nhắc Oliver ở phút 15**. 7 Layer 2 chỉ có L1 cho service cần fix, có thể check lần hai? → **không; gọi người có L2/L3**. 8 T3 22:10 có P3 COEC mới ở NEW → **layer 1 giao ASSIGNED từ vòng quét 5', rồi làm hoặc ghi log cho 04:00**.

## Practice
**PR-TEC-1.4-1 Role play P0 lúc 02:00** (giấy, cặp, 10'): một người đóng Shift Leader đọc case "SG checkout lỗi từ 01:50, nhiều khách, không có order từ 01:52, một promotion go-live lúc 01:45"; người kia là layer 1: nghe 4 điểm, hỏi 8 câu, quyết severity, đưa 6 chỉ dẫn trong 15' mô phỏng; rồi soạn thông báo Critical đầu tiên và tin nhắn Mattermost gửi Oliver (data DEMO). Pass: hỏi đủ 8 câu, gồm "vừa đổi gì" để tìm ra promotion vừa live; severity xác nhận trước phút 30; containment không cần Tech change (Merch tắt promotion qua workflow); thông báo có ICT, SGT và "Next update by", không hứa giờ fix, không PII; không bước nào đổi production trước khi PC được duyệt.
