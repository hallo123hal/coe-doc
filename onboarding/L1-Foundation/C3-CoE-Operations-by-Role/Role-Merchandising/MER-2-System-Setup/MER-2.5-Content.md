# MER-2.5 Content: AEM, CMS Hybris, Shop App CMS

> Nguồn: page 2483257500 · 50 phút (Study 15' · Demo 10' · Quiz 8' · Practice 17') · Facilitator: Market Owner có kinh nghiệm AEM & Shop App CMS · Cần xong G3.2, G5.1, MER-1.3 (AEM, BCF, SAC); staging s2 chỉ xem. AEM pre-QA, EPP CMS 2.0 (WMC), Shop App CMS thường chưa sẵn tuần đầu.

## Mục tiêu
Biết content nào quản ở AEM, WMC EPP 2.0, Hybris (AEMAdditionalInfo, CMS Restriction) hay Shop App CMS, kèm service & QA gate; kiểm 1 record AEMAdditionalInfoTypeData; liệt kê access cần và kênh xin; áp luật freeze và Shop App campaign guideline.

## Nội dung
### 1. Content nằm ở đâu

| Content | Quản ở | Service (Risk / QA gate) |
|---|---|---|
| Homepage, PF, FAQ, footer | AEM | AEM-01 (R1 / SL checks) |
| Offer page có T&C | AEM | AEM-02 (R2 tạm / Mandatory) |
| GNB, gồm EPP 2.0 | AEM | AEM-03 (Medium cho EPP 2.0 / Mandatory, người có kinh nghiệm làm) |
| Campaign page, banner | AEM | AEM-04 (R1 / SL checks; R2 nếu có T&C) |
| Hiển thị SKU trên EPP 2.0, Buying Configurator EPP 2.0 | WMC EPP (Ver.2) | BCF-01…04 (R2, R1) |
| Text/parameter theo SKU trên buy page | Hybris AEMAdditionalInfoTypeData | theo service gốc (PRF-05, BYP-03…) |
| Content Shop App | Shop App CMS | SAC-01 (R1 / SL checks) |

Build trên author, check preview rồi publish; rollback = unpublish hoặc khôi phục bản trước; content không qua Knox. Banner/CMS page có T&C tạm là R2 theo QA gate (CM-07 §2.2); R1 không qua QA Team mà do Shift Leader check. Content CoE dùng Jira project **COESEAO** (briefing template) để yêu cầu sản xuất content/asset.

### 2. Ẩn/hiện SKU trên EPP 2.0
**Không phụ thuộc Approval/Sales Status của Hybris.** WMC › Product Detail Mgmt › Update › Model Management → tick/untick Display → Save → QA → Live; rồi **Product Data Copy** (tick "Model Display Y/N") để áp cho mọi EPP site.

### 3. Record Hybris: AEMAdditionalInfoTypeData và CMS Restriction
Key thường dùng: DELIVERY_MESSAGE (chỉ còn dùng ở MY), RECOMMEND (mainTitle), Gift (mainTitle và subTitle đều bắt buộc), disableCTA (khi Sales Status là PDP Not Available). Bulk upload: Product Cockpit › Bulk Upload › AEM_ADDITIONAL_INFO; cột cuối đặt định dạng text để "30" không thành "0.3"; **Unique Key đã tồn tại thì dữ liệu mới ghi đè**. Kiểm ở Types › AEMAdditionalInfoData / AEMAdditionalInfoTypeData. **CMS Restriction:** `TokoMultiStoreCMSSiteRestriction` chỉ hiện component ở site đích; `CMSInverseRestriction` hiện ở mọi site trừ site đích. KB CMS Hybris gần như trống — kiến thức hữu ích nằm ở KB CMS Restriction.

### 4. Shop App CMS: role, access, campaign guideline
RHQ D2C Platform Head kiểm soát. BiPlus (không phải SEC) không tự raise AUTEU, phải email team D2C Platform. Ops COE có SECURE (bắt buộc cho flagship), VIEW B2C/EPP (bắt buộc), EDIT, REQUEST-APPROVAL, PUBLISH; **chỉ RHQ có APPROVE và SECURE-FREEZE-EXCEPTION**. Access cần IP whitelist (RHQ, COE, vendor của RHQ được xin; subsidiary & vendor subsidiary không). APK test xin qua AUTEU do Lead raise hộ (CM-13 §11.1); người quay lại cần dùng thì Knox chat cho RHQ platform PIC; không chia sẻ account. Chế tài: lần 1–2 giám sát; >3 lần bị gỡ access.
**One Launch (VD/DA):** Android — VD/DA RTB đứng trước, Square KV ở vị trí 1; iOS — chỉ hiện VD/DA RTB, ẩn RTB khác, dùng Long KV và ẩn KV khác; thứ tự Product Category Widget: VD, MX (chỉ Android), DA, Others; nhớ thêm Title.

### 5. AEM pre-QA và freeze
AEM pre-QA: tự đăng ký "QA Auth" trên wds.samsung.com, **không chọn PREPRD**. Hard freeze flagship: không cập nhật AEM EPP 2.0 và Shop App (QBH8 2); ngoại lệ cần bằng chứng duyệt ghi trong thân ticket; đọc freeze plan hiện hành trước khi đụng content (MER-3.2). Sửa B2C BC authoring trong giờ HQ → bị gỡ access ngay.

## Quiz (đáp án)
1 Đã Live thay đổi untick Display, muốn ẩn trên mọi EPP → **Product Data Copy**. 2 Role Ops COE không có → **APPROVE**. 3 Upload AEM_ADDITIONAL_INFO trùng Unique Key → **ghi đè**. 4 Subsidiary tự xin IP whitelist Shop App CMS → **không: chỉ RHQ, COE, vendor RHQ**. 5 Hard freeze, đổi banner Shop App → **chỉ khi có exception được duyệt**. 6 Tạo AEM pre-QA access không được chọn → **PREPRD**.

## Practice
- **PR-MER-2.5-1** (staging view): System › Types → `AEMAdditionalInfoTypeData` → Search by type, lọc SKU flagship, mở 1 record, ghi key, SKU, site, start, end, text; giải thích điều gì xảy ra khi upload lại cùng Unique Key và vì sao Display trên EPP 2.0 có thể khác status Hybris.
- **PR-MER-2.5-2**: bảng 5 dòng access (WDS QA Auth, EPP CMS 2.0, Shop App CMS role, IP whitelist văn phòng, Shop App APK) với kênh xin / người duyệt / đã có hay chưa; không ghi password hay IP. Kênh: WDS QA Auth & EPP CMS 2.0 tự đăng ký trên WDS; Shop App CMS email team RHQ D2C Platform; IP whitelist & APK qua AUTEU Lead raise hộ (hoặc Knox chat cho RHQ platform PIC nếu cần APK lại). Nêu rõ role APPROVE không xin được.
- **PR-MER-2.5-3**: phân loại 5 request — banner homepage không T&C (AEM-01/04, R1, SL checks); offer page có T&C (AEM-02, R2 tạm, Mandatory); GNB EPP 2.0 (AEM-03, người có kinh nghiệm); đổi thứ tự widget Shop App chiến dịch TV trên iOS (SAC-01, theo One Launch iOS: chỉ hiện VD/DA RTB); sửa BC page flagship trong giờ HQ (không được).
