# MER-2. System setup (hands-on)

> Nguồn: page 2482929740.

Module thực hành trên Backoffice staging: product reference, benefit, special price, promotion rule, coupon, tra cứu cấu hình multistore, content gắn với SKU. Khái niệm đã gặp ở G3.3, G3.4, G4.2, G5.1; ở đây tự làm từng task, kiểm kết quả, dọn data, và học luật RHQ cho biết *khi nào từ chối hoặc chuyển cho RHQ/Tech*.

**Quyền cần có:** account Backoffice staging s2 với quyền edit trên child catalog `vn` B2C (Staged), Product Cockpit, Marketing (Promotion Rules, Coupon Management), quyền xem Multistore và WCMS. Quyền *single-SKU sync* và *Preview-promotion-module* chưa xác nhận — Lead xác nhận trước cohort. Mọi bài thực hành có phương án giấy; screenshot evidence đưa thẳng lên Samsung Jira/Confluence, không lưu thư mục local.

| Session | Thời lượng | Mục tiêu chính |
|---|---|---|
| [MER-2.1 Product: SKU setup, flags, product references, add-on, benefit](MER-2.1-Product.md) | 90' | Tạo, kiểm, xóa product reference ở Staged child catalog và xác minh bản Online sau sync |
| [MER-2.2 Price and Knox price approval](MER-2.2-Price-Knox.md) | 60' | Tạo SPECIAL price row ở Staged, sync, kiểm staging PDP, dọn data |
| [MER-2.3 Promotion rule, coupon, naming, Knox promotion](MER-2.3-Promotion-Coupon.md) | 130' | Build promotion rule trên staging đúng code, tên, website, rule group, priority, condition, action, dates |
| [MER-2.4 Multistore: EPP, SMB, O2O](MER-2.4-Multistore.md) | 60' | Viết request form tạo 1 EPP site theo 8 bước với data cụ thể |
| [MER-2.5 Content: AEM, CMS Hybris, Shop App CMS](MER-2.5-Content.md) | 50' | Biết content nào quản ở AEM, WMC EPP 2.0, Hybris (AEMAdditionalInfo, CMS Restriction) hay Shop App CMS, kèm service & QA gate |
| **Tổng** | **390 phút (~6.5h)** | |
