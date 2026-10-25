# CM-13 Quy tắc RHQ: workflow, SLA, phê duyệt và tuân thủ trên hệ thống Samsung

> Tóm tắt từ trang Confluence CM-13 (v1.0, ban hành 21/10/2026; trang sửa lần cuối 22/10/2026). Trang song ngữ, bản tóm tắt này dựa trên phần tiếng Việt. Ví dụ trong tài liệu gốc là dữ liệu giả lập (mã DEMO-xxxx).

## 1. Vị trí của tài liệu
- Gom toàn bộ quy tắc RHQ nói trong **hai buổi training hệ thống ngày 21/10/2026** (người trình bày: Oliver Leung, RHQ) cùng các quyết định CEO BiPlus chốt ngay sau đó.
- **CM-13 thắng** mọi tài liệu v0.1/v0.2 về workflow, trạng thái Jira, đồng hồ SLA, phê duyệt, PC ticket, Knox approval, dữ liệu, strike, BVT. Thấy mâu thuẫn: làm theo CM-13 và báo Lead.
- Áp dụng cho Merchandising, Tech, QA, COE Lead, SDM, CSM, CoE Operations Office. Không thay handbook chuyên sâu (SLA → CM-03, Service Request → CM-05, Change/Problem → CM-07, công cụ → CM-09, ATTT → CM-10, BVT → CM-12, Merch → MR-04, Tech/COEC → TC-03, PC ticket → TC-05).
- "Cam kết hợp đồng (RFP)" = số RHQ dùng để đo và trừ phí; "mục tiêu nội bộ BiPlus" = số chặt hơn để hành động sớm, không phải cam kết với RHQ.

### Bốn quyết định CEO (21/10/2026)
| # | Chủ đề | Quyết định |
|---|---|---|
| 1 | PIC 3PD | Có một PIC 3PD chuyên trách, **đặt tại Tech Team**, có backup |
| 2 | Read-back | **Bỏ** bước nhờ requester xác nhận giá trị trước khi build; thay bằng **kiểm tra nội bộ** |
| 3 | Phạm vi PC ticket | Theo Oliver: PC ticket cho thay đổi do **Tech** làm trên production; setup Merchandising đi workflow Shop Merchandising + Knox approval |
| 4 | Proposal v9.5 làm phụ lục SoW | Việc của CoE Office, không đổi cách làm việc |

## 2. Các bên, project Jira, quyền hạn
- Bên liên quan: 8 subsidiary (VN, TH, ID, MY, SG, PH, AU, NZ); RHQ SEAO (chủ dịch vụ, đo SLA, duyệt PC ticket, chủ trì họp tuần); HQ Suwon (quy định toàn cầu: header ImpEx, guide add-on page, freeze plan); SDS India (Samsung L2/L3); đội phát triển/BA Spoke/global release; middleware 3PD; SDSAP (bàn giao, kết thúc 30/11/2026).
- CoE tự thực hiện thay đổi production sau khi PC ticket được duyệt (không phụ thuộc đội phát triển).
- Project/issue type: **Shop Merchandising** (Merch + QA, 8 nước), **COEC** (chỉ Tech), **PC** (Prod Change, Tech tạo, RHQ duyệt), **Maintenance Request** (Tech tạo cho L2/L3, không phải hàng đợi CoE), ticket enhancement của đội phát triển (BVT, không có project BVT riêng).
- **Confluence RHQ = single source of truth**; mỗi trang có PIC duy trì.
- **Không ai có quyền admin**: không super admin Hybris, không admin Jira; Tech có thể được semi-admin sau nếu RHQ thấy đội tuân thủ. Move ticket giữa project không cần admin. Việc cần quyền cao (workflow, automation, dashboard chung, IP whitelist) phải đề xuất RHQ.

## 3. Workflow Shop Merchandising và SLA
- Một workflow dùng chung 8 nước. **Đồng hồ chỉ chạy ở STG SETUP, QA REVIEW, PRD SETUP, ON HOLD COE.** Chờ subsidiary/RHQ đều dừng.
- Merch và QA **dùng chung một SLA**; RHQ không đo SLA riêng cho QA.
- SLA hợp đồng: High 4 giờ (bất kể giờ làm việc; ảnh hưởng bảo mật dữ liệu hoặc mất doanh số > 10.000 USD), Medium 16 giờ (một promotion; yêu cầu phức tạp), Low 24 giờ (nhiều promotion > 2, thiết lập SP, giá, CMS); initial response 2 giờ; ≥ 97%/tháng. Nội bộ: 78 phút; P0/High 15 phút. **Medium/Low tính giờ lịch 24/7 hay giờ làm việc: RHQ chưa trả lời, tạm lập kế hoạch theo giờ lịch 24/7.**

| Trạng thái | Ai | SLA |
|---|---|---|
| PLANNING, PLANNING REVIEW | Subsidiary | chưa tính |
| APPROVED-ES / NOT APPROVED | Subsidiary duyệt, CoE nhận | bắt đầu đo initial response |
| STG SETUP | Merch | **tính** (CoE chuyển vào = xác nhận đã nhận; không phải môi trường staging) |
| QA REVIEW | QA | **tính** |
| PRD SETUP | Merch | **tính** (đi thẳng từ STG SETUP hoặc qua QA) |
| ON HOLD SUBS | Subsidiary | dừng |
| ON HOLD COE | CoE | **tính** |
| ON HOLD RHQ | RHQ | dừng (duyệt xong về STG SETUP) |
| REVIEW SETUP | Subsidiary | dừng |
| PENDING LAUNCH, LAUNCH VERIFICATION, CLOSED | CoE | không tính |
| INVALID | bất kỳ | không tính; đóng hẳn, muốn làm lại phải **clone** |

- **L.V. APPROVAL** (Launch Event Approval) có trên Jira nhưng RHQ không trình bày; không dạy là bước bắt buộc, gặp thì hỏi Shift Leader.
- **Initial response = chuyển trạng thái** từ APPROVED-ES sang STG SETUP; comment thôi không đủ. Mỗi ca cần dashboard ticket ở APPROVED-ES giao CoE.
- **STG SETUP = setup trên production**: promotion setup trên production, publish sang simulator, test bằng promotion simulator (Back Office 2.0), đến giờ go-live publish live. Promotion quá phức tạp thì người làm được tự chọn thử trên staging thật (không bắt buộc, vẫn tính SLA).
- **ON HOLD SUBS**: một câu hỏi gộp trong comment, chuyển trạng thái **và** đổi Assignee sang subsidiary; không chuyển chỉ để dừng đồng hồ. Cần dashboard "ON HOLD SUBS mà Assignee là người CoE" (subsidiary đã trả lời nhưng quên chuyển) → chuyển ngay về STG SETUP.
- **REVIEW SETUP**: bằng chứng QA đính Jira để subsidiary duyệt. Nếu go-live 00:00 mà đến 23:59 chưa có duyệt, **vẫn publish đúng hạn** và comment "published, no feedback". RHQ sẽ dọn hàng loạt ticket treo. Việc publish trước/sau REVIEW SETUP theo loại yêu cầu: chờ RHQ (tạm áp promotion và giá có ngày go-live đã thống nhất).
- **PENDING LAUNCH**: ticket nhiều promotion ngày bắt đầu khác nhau → mỗi lần promotion live phải **QA lại trên production**, rồi quay PENDING LAUNCH tới đợt sau; xong hết → LAUNCH VERIFICATION → CLOSED.

## 4. Workflow Tech trên COEC
- Ticket COEC do Merch/QA/HQ/subsidiary tạo, mặc định **NEW** (không có bước subsidiary duyệt). **Initial response = NEW → ASSIGNED** (Tech Lead hoặc người ủy quyền). Cần dashboard COEC ở NEW.
- SLA Tech: P0 4 giờ (bất kể giờ), P1 8, P2 16, P3 40, P4 120; initial response 2 giờ; 97%. Nội bộ: P0 15', P1 30', còn lại 78'.
- Tính SLA: ASSIGNED, IN REVIEW, IN PROGRESS, QA REVIEW (Tech tự QA), WAITING QA (chờ người thứ hai trong Tech). Dừng: ON HOLD SUBSIDIARY, SYSTEM SUPPORT (SDS India), ON HOLD HQ (gồm chờ PC ticket), ON HOLD ES (đội khác; nghĩa "ES" chưa rõ: quyền Hybris, tài khoản, reset mật khẩu Back Office). LAUNCH VERIFICATION giao cho người tạo ticket (không tính).
- **QA REVIEW của Tech** = tự kiểm trên staging trước PC ticket; chưa chắc thì nhờ thêm một người Tech (another set of eyes). QA Team chỉ phục vụ Merch.
- **SYSTEM SUPPORT**: tạo Maintenance Request trong project nước, liên kết COEC, chuyển SYSTEM SUPPORT. CoE vẫn giữ ownership, theo dõi bằng comment: High 2 ngày làm việc, Medium 4, Low hằng tuần.
- RHQ định kỳ đóng ticket LAUNCH VERIFICATION không cập nhật quá 1 tháng.
- **Ngoài giờ Tech** (Level 1 hai ca 04–12 và 11–19, T2–T7; ngoài đó 19:00–04:00 và CN): bản CM-13 ghi cách tạm là **Shift Leader quét COEC ở NEW**; P0/P1 gọi Tech on-call lớp 1 chuyển ASSIGNED và xử lý tại trung tâm; ticket khác ghi handoff note cho Level 1 ca 04:00. **Điểm lệch cần lưu ý:** các trang CM/TC/MR bản v0.3 (22/10) quy định **Tech on-call lớp 1 tự quét COEC ở NEW mỗi 5 phút** ngoài giờ Tech và xử lý tại trung tâm (Shift Leader chỉ gọi on-call khi thấy P0/P1); mục 4.6 của CM-13 v1.0 vẫn ghi Shift Leader quét. Theo các trang v0.3, làm theo bản on-call lớp 1: nhịp 5 phút là nhịp của bộ lọc COE-F01T và email cảnh báo; on-call chỉ đọc/chuyển ASSIGNED khi đã ngồi ở máy trạm tại trung tâm (không remote), nên ticket P2–P4 tạo lúc on-call chưa có mặt có thể chờ đến 04:00 hoặc lượt kiểm CN 09:00 (chưa bảo đảm initial response 2 giờ; TC-04 mục 4.3). CM-13 sẽ được đồng bộ ở phiên bản sau.

## 5. Phối hợp Merch – Tech
- Merch cần Tech một phần: Merchandising PIC **giữ ticket**, tạo **ticket COEC mới** (ghi rõ việc Tech: số mã, prefix, thời hạn, link brief), **liên kết** (Jira issue link tốt nhất), chuyển ticket Merch sang **ON HOLD COE** (vẫn tính SLA) và comment. Hai SLA chạy song song; Tech ưu tiên COEC đang có ticket Merch chờ. Ví dụ: 500.000 mã coupon multi-code.
- Ticket nhầm team, toàn bộ việc thuộc team kia: **move chính ticket** sang project đúng (không tạo ticket mới, không cần admin); sau move theo SLA team mới.

## 6. QA Team
- QA việc hằng ngày của Merch; **không BVT, không QA Tech**; RHQ không đo SLA riêng cho QA, BiPlus có OLA nội bộ.
- Vào QA REVIEW: kiểm có đủ dữ liệu (brief, file SKU, giờ go-live, bằng chứng setup); thiếu → trả Merch và **đến bàn người làm** hỏi.
- **Bằng chứng QA = PowerPoint chụp màn hình từng bước**, đính comment Jira; Jira giới hạn 15 MB/file; **không dùng video**, chưa dùng link ghi hình (Meet, Loom). Tạo trên máy trạm CoE, đính Jira rồi xóa bản trên máy; không chụp bằng điện thoại, không gửi kênh khác.
- Giảm tỷ lệ trả về: Merch **tự QA trước**; ticket bị trả **2 lần** phải tìm nguyên nhân gốc.
- QA phải hiểu giá promotion Hybris, stackability, trade-in.

## 7. Kiểm tra nội bộ thay read-back
- Bỏ bước nhờ requester xác nhận; chỉ hỏi subsidiary khi brief thiếu hoặc mâu thuẫn (RHQ: quy trình phải dễ cho subsidiary; brief đã qua phê duyệt của subsidiary).
- Quy trình: (1) **Doer** đối chiếu cấu hình với brief đã duyệt và ghi tóm tắt giá trị chính lên ticket trước build (SKU, giá/mức giảm, thời gian kèm múi giờ, site/store, quy tắc stack, giới hạn dùng); (2) chạy **price sanity rules**; (3) **Checker** theo rủi ro: R1 Shift Leader; R2 qua QA nếu có QA gate hoặc lấy mẫu rồi Shift Leader duyệt; R3 qua QA, Shift Leader duyệt, thêm Merch Lead/Deputy duyệt khi mức E4; (4) brief thiếu/mâu thuẫn → một câu hỏi gộp, ON HOLD SUBS, giao subsidiary.
- Price sanity vẫn giữ: giảm ngoài khoảng ngành hàng (vd 85%); giá cuối dưới sàn; coupon không giới hạn lượt; ngày đã qua, > 90 ngày hoặc sai múi giờ; stack ngoài dự kiến → dừng, hỏi subsidiary bằng văn bản trước khi build.

## 8. Yêu cầu gấp (last-minute)
- Promotion cần gửi trước khoảng 2–3 ngày làm việc. Ticket sát giờ: **subsidiary chịu trách nhiệm và tự QA khi live**; CoE phải comment: *"Last minute request, please QA on your own when it goes live. If any issue, please contact us."* và đứng chờ hỗ trợ. Vẫn **gửi Knox approval** như thường.
- Mỗi yêu cầu gấp gắn label (đang dùng LastMinRequest) để đếm cho họp tuần; Shift Leader kiểm label trong handoff, Merch Lead tổng hợp. Ngưỡng tạm: cần live cùng tối mà đến sau **17:00 giờ VN** là yêu cầu gấp (RHQ chưa chốt 2 hay 3 ngày).
- Đề xuất chờ CEO: R3 vẫn bắt buộc kiểm tra nội bộ + price sanity + Shift Leader duyệt + người thứ hai kiểm trên production lúc go-live.

## 9. PC ticket (Prod Change, project PC)
- **Mọi thay đổi do Tech làm trên production** đều cần PC ticket do **Oliver Leung** duyệt, kể cả việc 5 giây. Release code của đội phát triển không đi PC ticket.

| Việc | PC ticket? |
|---|---|
| Tech tạo/xóa/sửa dữ liệu production, đổi cấu hình Back Office, mọi ImpEx/Groovy, tạo cronjob báo cáo (sau PUMI) | Có |
| Merch setup giá, promotion, sản phẩm, CMS theo workflow | Không; workflow + Knox approval |
| Merch cần ImpEx của Tech | Phần Tech: COEC + PC ticket |
| Truy vấn chỉ đọc để điều tra | Không, nhưng phải có lý do |
| Release code | Không |

- Các bước: (1) staging trước (kết quả + ảnh dữ liệu vào PC ticket; ImpEx dùng lại nhiều lần có thể bỏ, loại mới **bắt buộc**); (2) tự QA / another set of eyes; (3) tạo PC ticket liên kết COEC gốc (gì, vì sao, kết quả staging, rollback); (4) COEC sang **ON HOLD HQ** + comment "PC ticket pending"; (5) P0/P1 cần gấp: nhắn Oliver qua Mattermost; (6) Oliver duyệt và **tự chuyển COEC về IN PROGRESS**; (7) chạy đúng nội dung đã duyệt; (8) kiểm, ghi bằng chứng, LAUNCH VERIFICATION giao người tạo.
- **Dòng header bắt buộc** trong ImpEx/Groovy theo HQ Suwon: số PC ticket + số ticket COEC gốc; thiếu → vài ngày sau RHQ/HQ email giải trình và người chạy nhận **strike đầu**.
- Oliver là người duyệt **duy nhất** (HOD cụm SEAO, gồm SMB), không backup. Vắng **23/10–9/11/2026**: vẫn chờ Oliver, chậm ~3 giờ → tạo PC ticket sớm, nhất là trước peak.
- Thay đổi khẩn trong P0/P1 vẫn cần PC ticket; rollback cũng là thay đổi production.

## 10. Knox approval cho giá và promotion
- Giá và promotion phải duyệt qua Knox. Promotion đã publish: đổi **action, condition, website hoặc ngày** → lần publish sau **phải duyệt lại**; đổi cấu hình khác (vd tên) → không.
- Approval path khác nhau theo subsidiary và division (MX mobile, CE consumer electronics); campaign brief có cột **approval path** do subsidiary ghi, CoE làm theo, không tự chọn. Cách gửi/loại approval: hỏi đội CoE hiện tại trong KT; Market Owner ghi vào runbook.
- Trạng thái Jira khi chờ Knox: RHQ chưa nói; tạm ghi trên ticket đã gửi lúc nào, path nào; Shift Leader theo dõi trong handoff; không tự chuyển ON HOLD SUBS.

## 11. Quyền truy cập, tài khoản, offboarding
- Mọi quyền/tài khoản (kể cả middleware 3PD) qua **ticket phê duyệt theo template**, thường **COE Lead/Lead tạo thay thành viên**. Tên ticket/project chính xác: xem Confluence RHQ.
- **Offboarding**: Lead tạo ticket đúng **ngày làm việc cuối**, khóa tài khoản mọi hệ thống Samsung; tài khoản còn mở sau ngày cuối là lỗi tuân thủ (quy trình nội bộ ở CM-10).
- IP whitelist: RHQ làm (BiPlus gửi 2 IP). Jira account mới: RHQ xử lý. Mattermost, Shop App: RHQ tạo phê duyệt. O2O: quy trình riêng nhiều user group; reset mật khẩu/kích hoạt lại thường do subsidiary yêu cầu, CoE tạo ticket thay. Đổi CDN cần phê duyệt. Confluence: người chưa có Samsung business account mất 2–3 ngày.
- Email hệ thống Samsung: tên tiếng Anh + họ thật, miền BiPlus (ví dụ giả lập alex.tran@biplus.com.vn trong CM-13; CM-10 v0.3 nhắc miền dự án coe.biplus.com.vn).

## 12. Dữ liệu, báo cáo, PII
- Không truy vấn production khi không có lý do. Báo cáo, dữ liệu lịch sử, cronjob báo cáo, thêm/bớt recipient: cần **PUMI** được duyệt rồi mới PC ticket. Thêm/bớt trường **không PII** được; **PII** chỉ ngoại lệ (audit) theo quy trình riêng. Xin email khách để gửi EDM: **mặc định từ chối**. Không gửi PII qua email từ Hybris. FTP theo quy trình riêng.
- Có database do RHQ quản lý toàn bộ: **không bao giờ sửa**.
- Chờ xác nhận: nghĩa đầy đủ của PUMI, ai duyệt/bao lâu, trạng thái khi chờ PUMI; tên database; "contract creation" (coi là tạo cronjob).

## 13. EPP site mới/kích hoạt lại
- Subsidiary phải có **email phê duyệt** đính vào ticket; CoE chuyển chờ RHQ (ON HOLD RHQ trên Shop Merch, ON HOLD HQ trên COEC) để Oliver duyệt; không có email thì Oliver từ chối. Chưa có phê duyệt → trả subsidiary yêu cầu xin theo template RHQ (tạm ON HOLD SUBS + giao subsidiary; INVALID hay ON HOLD SUBS RHQ chưa nói).

## 14. Template, promotion brief, RHQ guidelines
- Template do RHQ duyệt, chỉ dùng **bản mới nhất**, ưu tiên subsidiary dễ điền; muốn đổi thì đề xuất RHQ. Template thường gặp: new product registration, SC+/SC++ (MX, CE), high-risk benefit, special price/promotion brief, new delivery mode, new site/app site creation.
- **Promotion brief**: nhiều sheet, mỗi sheet một loại; trường do subsidiary điền và trường do CoE điền. Trường chung: site áp dụng (liệt kê đủ), target main SKU, stack, ngày bắt đầu/kết thúc (kèm múi giờ), coupon type/prefix, kiểu giảm (trừ tiền, giá cố định, %, % theo RRP), cart message, remarks, FOC tách consignment (3 nước). Loại: FOC BOGO, priority BOGO, PWP, buy more save more, F-code, payment/BIN promo, delivery mode/service promo, selection of gift.
- Không có quy tắc nào áp cho mọi subsidiary: tách phần chung/riêng, ghi vào market book (MR-03). Knowledge base đội hiện tại (product setup, SKU setup, product archive bắt buộc, sales status → CTA, $0 checkout…); trang dữ liệu 2025 đã cũ.
- **RHQ guidelines**: coupon thay voucher (trừ RNPL); GNB mới cho EPP; long-term financing (một site Singapore); Samsung Members EPP site; Knox approval.

## 15. 3PD
- CoE không vận hành marketplace; quản **middleware** giữa Hybris và marketplace: **4 middleware** (không chỉ LogicBroker); luồng order, stock, product data.
- **PIC 3PD chuyên trách đặt tại Tech Team**, có backup đã chứng nhận; chọn từ người từng làm dự án 3PD của BiPlus; ca do Tech Lead xếp roster; quyền middleware qua ticket phê duyệt do Tech Lead tạo; thay đổi dữ liệu 3PD production đi PC ticket. Danh sách 4 middleware và PIC 3PD hiện tại để mời vào KT: chờ RHQ.

## 16. BVT (tóm tắt)
- PIC BVT là Merch hoặc Tech tùy phạm vi; **QA Team không tham gia**.
- 8 bước: lịch release hằng tháng của HQ → ma trận PIC (RHQ xin khoảng 1 tuần trước; cửa sổ ngày cố định, không thương lượng) → kickoff (đội phát triển chủ trì) → PIC xác nhận bắt đầu trên ticket + trang Confluence → test hằng ngày bằng Excel, tải lên Confluence → hai phần việc (hỗ trợ subsidiary kiểm backend/cấu hình + tự test E2E, thêm case riêng nước) → defect (đội phát triển triage, BA Spoke đôn đốc, 2–3 ngày; blocker báo ngay) → **sign-off 100% pass** (99% là không go-live; RHQ kiểm bằng chứng từng case).
- Ticket áp dụng 8 subsidiary: test case nhân 8. BVT trong SLA RFP (Test Case Pass Rate 6%, Test Report Completion 3%, User Acceptance 1% của Composite). BVT Coordinator tạm là một Tech Sub-Lead (chờ CEO, DL-01). Thông báo BVT ngoài giờ: handoff note + nhắn Merch Lead, Tech Lead.

## 17. Strike và trách nhiệm cá nhân
- **RHQ quyết định** ai bị strike, dựa trên **RCA của Lead**. Không theo quy trình/không biết mà vẫn làm gây sự cố → strike; lỗi do hệ thống (vd sau deployment) → không. **3 strike trong một năm dương lịch = loại vĩnh viễn**; tính lại mỗi năm dương lịch.
- Chắc chắn dẫn tới strike: ImpEx/Groovy production thiếu header; thay đổi production khi chưa có PC ticket duyệt; làm service chưa chứng nhận rồi gây sự cố.
- Nội bộ: Lead viết RCA trung thực; người nhận strike vào bậc kèm cặp của people-risk ladder (MR-06, CM-07), chứng nhận lại; BiPlus chủ động thay người trước strike thứ ba.

## 18. Kiến thức, đào tạo, giao tiếp RHQ
- Kiến thức vận hành chính thức phải nằm trên Confluence RHQ (kể cả khi có hệ thống nội bộ). Thư viện ImpEx hiện không có quản lý phiên bản → CoE tự đặt (Tech Lead chốt ở TC-05: phiên bản, ngày, người sửa, ticket COEC).
- Ghi hình mọi buổi đào tạo; link phải truy cập được, tải được, **không hết hạn**. Mỗi tháng phân công người viết nội dung kiến thức.
- Kênh chính với RHQ: **Mattermost** (toàn đội có tài khoản); câu hỏi nhiều → Excel + email; việc gấp → gọi (Oliver vắng thì nhắn đội RHQ; duyệt PC vẫn chờ Oliver); kế hoạch nghỉ báo trong họp tuần. Kênh với subsidiary chờ RHQ (tạm comment Jira; Knox Messenger/Teams chờ xác nhận).
- Trang CoE (auxiliary page) trên Confluence RHQ: danh sách Lead, ngày lễ VN và nghỉ phép, roster, danh sách team, trang workflow ticket.

## 19. Clean Room và flagship
- Add-on page: guide HQ (khoảng 5 tab bắt buộc); CoE bảo đảm tối thiểu đúng guide: **được thêm, không được thiếu**.
- Trang flagship giới hạn quyền, có freeze plan: soft freeze, hard freeze, Hybris hard freeze (thường 2–3 ngày sau Galaxy Unpacked), Shop App freeze. Ngoại lệ luôn cần phê duyệt (bằng chứng ghi trong body ticket); trong hard freeze vẫn được cập nhật stock.
- **VN Clean Room** (trước là MY): ngày RHQ, HQ, India và các subsidiary đến BiPlus làm UAT; yêu cầu tầng 6: phòng 40 chỗ chia đôi được, khoảng 4 phòng họp subsidiary, 20–25 chỗ đội lõi. Clean Room ≠ khu làm việc bảo mật (quy tắc ở CM-10). Lịch freeze 2027 và ngày VN Clean Room: chờ RHQ.

## 20. Checklist trước ticket thật đầu tiên
Dashboard (APPROVED-ES; ON HOLD SUBS có Assignee là CoE; COEC ở NEW; COEC ở ON HOLD HQ chờ PC; SYSTEM SUPPORT đến hạn follow-up); mẫu comment tiếng Anh trong runbook; checklist trước khi chạy ImpEx/Groovy in tại bàn Tech; label last-minute; trang CoE trên Confluence RHQ; tài khoản Mattermost/Jira/Confluence; PIC 3PD + backup đăng ký KT; quy tắc phiên bản thư viện ImpEx.

### 23 điểm còn chờ RHQ (tóm tắt)
Đã rõ: phạm vi PC ticket; Oliver vắng 23/10–9/11 vẫn chờ (~3 giờ); move ticket nhầm team được; bằng chứng QA giữ nguyên, không video; setup Merch không cần PC ticket. Còn mở/một phần: nghĩa "ES"; Shift Leader/on-call chuyển NEW → ASSIGNED ngoài giờ Tech; ai đóng ticket tồn ở REVIEW SETUP/LAUNCH VERIFICATION (RHQ đóng LV quá 1 tháng); mốc last-minute; publish trước/sau REVIEW SETUP; kênh với subsidiary/Teams; lịch freeze 2027 và ngày VN Clean Room; đầu mối thông báo BVT; tên ticket xin quyền; PUMI; "contract creation"; database RHQ; RNPL; 4 middleware + PIC 3PD hiện tại; EPP thiếu phê duyệt (INVALID hay ON HOLD SUBS); L.V. APPROVAL; trạng thái chờ Knox; Medium/Low theo giờ lịch hay giờ làm việc.

## 21. Mười quy tắc cần thuộc
1. Đồng hồ SLA chỉ chạy khi việc ở phía CoE. 2. Initial response là chuyển trạng thái (APPROVED-ES → STG SETUP; NEW → ASSIGNED). 3. Hỏi subsidiary = ON HOLD SUBS **và** giao ticket. 4. ON HOLD COE vẫn tính SLA; cần Tech thì tạo COEC liên kết. 5. QA chỉ QA việc Merch; không BVT, không QA Tech. 6. Kiểm tra nội bộ thay read-back. 7. Không PC ticket duyệt thì Tech không đổi production; ImpEx/Groovy phải có header. 8. Sửa action/condition/website/ngày promotion đã publish → duyệt Knox lại. 9. Dữ liệu production cần lý do, PUMI, PC ticket; không PII qua email. 10. 3 strike/năm dương lịch = loại vĩnh viễn.

## 22. Mẫu comment tiếng Anh (Phụ lục B, rút gọn)
Nhận ticket ("Received and acknowledged… Target completion…"); cần làm rõ ("To proceed, please confirm…"); đã tạo COEC ("Tech support needed. COEC ticket … has been raised and linked."); yêu cầu gấp (câu chuẩn ở mục 8); đã publish chưa có phản hồi ("Published as aligned for go-live at …"); chờ PC ("PC ticket pending: … Work will resume once approved."); EPP thiếu phê duyệt; move ticket; báo cáo cần PUMI; offboarding.

## 23. Câu hỏi kiểm tra (Phụ lục C–D)
12 trắc nghiệm + 8 tình huống. Đáp án trắc nghiệm: 1 d (REVIEW SETUP dừng đồng hồ), 2 b, 3 a, 4 b, 5 c, 6 c, 7 c, 8 b, 9 b, 10 c, 11 b (clone), 12 c (vẫn chờ Oliver ~3 giờ). Tình huống: quên đổi Assignee → chuyển STG SETUP và làm tiếp; 300.000 coupon → giữ ticket Merch, COEC liên kết, ON HOLD COE; yêu cầu gấp 18:10 → label, kiểm tra nội bộ, Knox, comment chuẩn; 23:30 chưa duyệt → publish đúng hạn + comment; Groovy 800 đơn → staging, tự QA + người thứ hai, PC ticket, header; xin email khách cho EDM → từ chối; EPP chưa phê duyệt → trả subsidiary; ticket nhầm team → move chính ticket.
