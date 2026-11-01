# MER-2.4 Multistore: EPP, SMB, O2O

> Nguồn: page 2483388546 · 60 phút (Study 20' · Demo 7' · Quiz 8' · Practice 25') · Facilitator: Sub-Lead 4 (PIC nhóm kênh EPP/SMB/O2O) hoặc Merch Lead · Cần xong G4.2, G5.1, MER-1.3; staging s2 chỉ xem; giữ mở template A.12 (MR-04 App. A).

## Mục tiêu
Viết request form tạo 1 EPP site theo 8 bước; kiểm 4 setting EPP 2.0 và số exclusion của EPP có sẵn; áp đúng flow duyệt cho EPP mới/kích hoạt lại (có/không có email); phân loại request multistore là việc Merch, Tech hay RHQ; áp luật RHQ cho EA OE, Samsung Members, store merge.

## Nội dung
### 1. EPP mới / kích hoạt lại: RHQ duyệt trước (MST-01)
Subsidiary email RHQ D2C Platform Head và D2C EPP PIC; sau duyệt Head comment hoặc subsidiary đính email. **Có email** → ON HOLD RHQ chờ Oliver Leung duyệt, rồi về STG SETUP. **Không email** → không build; comment A.12, ON HOLD SUBS, assign subsidiary. Requestor phải nêu: Site ID, lý do, vì sao không dùng site chung Corp/EDU/Gov/SMB, số user, doanh thu kỳ vọng 3 năm, login type. Login type verification code bị cấm trừ khi có lớp hạn chế thứ hai. Tạo xong site thì gửi ticket RHQ để AEM redirect (ID, Hybris URL, AEM URL; RHQ xử lý trong 1 tuần).

### 2. 8 bước dựng EPP
1) Kiểm email duyệt. 2) Tạo multistore (Backoffice › Multistore › "+") với Site ID đúng convention. 3) Chọn login type (SSO_DOMAIN thì thêm domain). 4) Cart restriction. 5) **4 setting EPP 2.0 trên Website**: `CMSSite.aemHomepageUrl` kết thúc "/"; Redirect to External PDP = TRUE; `CMSSite.isAemEnableSite` = TRUE; `CMSSite.urlRedirects` có code `countryCode-siteID`, 2 regex urlPattern, inclusive = True. 6) Tạo store ở WMC EPP (Ver.2) và chạy shop sync. 7) Quota. 8) Kiểm bằng test account.
Site ID `xx_yyyyy`: mã nước chữ thường, chỉ chữ/số/`_`/`-`; `sg_accenture-2025` đúng, `SG_Accenture`/`sgbankxepp` sai. Checklist EPP mới (WIP) ~50 field (catalog version, Access Type, Sold-to/Partner number, Channel 30 cho B2C & SMB / 31 cho B2B, delivery/payment mode, warehouse, quota, expiry, renewal email); ERP/ERPFI config do Tech qua PC.

### 3. Ba cấp cấu hình & exclusion
Multistore có giá trị thì thắng, trống thì xuống Website rồi Base Store (VD Base Store 7 delivery mode, Website 9, Multistore chỉ `my-schedule-delivery` → EPP chỉ thấy cái đó). Payment mode thêm vào multistore phải có sẵn ở base store; gỡ phải gỡ cả base store và website. **Exclusion ≤75 sản phẩm và 7 category/site**; vượt thì DISPLAY "NO" phía AEM; định kỳ xóa SKU EOL. MST-02 là R2, QA sampling.

### 4. EA OE, Samsung Members, store merge
- **EA OE không dùng exclusion Hybris** (vỡ API): làm trên AEM; login O2O Cockpit; CMS & GNB do RHQ Platform quản.
- **Samsung Members EPP:** 5% sitewide trên giá B2C; không special price/discount row/promotion khác trừ HR và RNPL; login Access Code (OTP ở VN); không tạo access code mới nếu không có RHQ duyệt.
- **Store merge (MST-03):** gộp site phải thêm site mới vào mọi promotion rule đang chạy, nếu không khách site mới mất ưu đãi; việc này đổi website của rule → Knox lại, ticket lấy tier R3.

### 5. O2O account, Knox, ai làm gì
O2O Backoffice account `country_code.o2o.email` (cần RHQ Online Platform Lead + Suwon duyệt, mỗi người một account). Tên: `XX_pos_adm_o2o`, `XX_pos_adm_ZZZ`, `XX_store_usergroup_ZZZ_VVV_PPP`. Cấu hình multistore không qua Knox mà qua email RHQ; special price/discount row cho EPP vẫn R3 + Knox. Ticket multistore/EPP/O2O là Medium 16h.

| Request | Ai làm | Điều kiện |
|---|---|---|
| EPP mới / kích hoạt lại | Merch (MST-01) | Có email: ON HOLD RHQ; không: A.12, ON HOLD SUBS |
| Thêm email domain/retiree/user vào access list | Tech (COEC) | Move ticket (A.11) |
| Store config, ERP/ERPFI, payment mode cấp site | Tech + PC | Ticket Merch ON HOLD COE nếu còn việc |
| Excluded products | Merch (MST-02) | ≤75/7, vượt thì AEM |
| Access code mới Samsung Members | Chỉ khi RHQ duyệt | Không duyệt thì từ chối |
| Duyệt đăng ký SMB | Merch trong Backoffice | Không cần RHQ; bắt buộc email công ty |

## Quiz (đáp án)
1 EPP mới thiếu email RHQ → **không build; ON HOLD SUBS**. 2 Reactivate có email → **ON HOLD RHQ rồi STG SETUP**. 3 Exclusion 90 sản phẩm → **giữ ≤75, ẩn phần còn lại trên AEM**. 4 EA OE ẩn SKU → **trên AEM**. 5 Special price riêng cho Members → **từ chối**. 6 Merge 11 site → **hay quên thêm site mới vào rule đang chạy**.

## Practice
- **PR-MER-2.4-1**: form 8 bước cho EPP bank X của SESP (email `@bankx.com.sg` hoặc access code, tối đa 3 máy, chỉ thẻ & PayNow). Pass: đủ 8 bước, quota 3, payment mode ở cấp multistore (đã có ở base store); không email → A.12/ON HOLD SUBS; Site ID `sg_bankx_epp`.
- **PR-MER-2.4-2** (staging view): ghi 4 setting Website + login type, cart restriction, số exclusion, payment mode cấp multistore của một EPP `sg_…`.
- **PR-MER-2.4-3**: phân loại 6 request (ON HOLD RHQ; A.12 + ON HOLD SUBS; ON HOLD RHQ; move COEC; từ chối; làm trên AEM).
