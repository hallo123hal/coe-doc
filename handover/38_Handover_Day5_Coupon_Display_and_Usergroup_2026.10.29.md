# CoE Meeting Notes – Handover Day 5: Coupon Display and Usergroup (2026.10.29)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2489024604
Sub-pages (personal notes, not summarised in detail): Baopg (2489778185), TungNS (2489417876), Ngavt (2489288029), Quynhltn – Restricting Coupons by User Group and Email (2489581872), Trangnnt (2489516383), Ayu (2489680054), Thanhvd (2489647319), Trangdtt (2489321206).

Meeting: HELD on 29/10/2026, shared recording 10:27 (about 75 minutes); this page covers 42:50 to the end (Siti Sarah starts presenting about 45:30). The first part is in 37_Handover_Day5_Coupon_Single_Code_vs_Multicode_and_Ingestion. Group: Promotion. Chair: Chong Haw Eong (SDSAP); presenters Siti Sarah Binti Azman (SDSAP, PIC) and Chong Haw Eong. BiPlus: all CoE members. References (Samsung Confluence SEAORHQ): *Coupon* (581409234), *KB – Coupon Usergroup Setup HGE-11315* (620243061).

## Main content

### 1. Displaying coupons on My Voucher (42:50 – 44:50)
- Administration Cockpit → Coupon → select coupon → **Administration** tab → **Hide in My Voucher Page** = **False** → the coupon shows on the front end (My Account → My Voucher); customers can copy and apply it.
- My Voucher: usable coupons in tab **Available**, used ones in **Redeemed**.
- Each tile shows: **promotion name** (title, from the promotion rule), **coupon code**, **promotion description**, promotion **end date**, a **Copy** button. **Exclusive** promotions carry an Exclusive label at top left.

### 2. Restricting display by customer group (Sarah) (44:50 – 51:00)
- Based on KB **Coupon Usergroup Setup (HGE-11315)**. Background: coupons used to show to customers who were not eligible; vouchers were already filtered, coupons need the same so customers only see promotions they qualify for.
- Three methods: **User group**, **Customer email**, **Email hash**.
  - **User group**: Coupon → Admin → **SingleCodeCoupon.couponRestrictions** (or MultiCodeCoupon.couponRestrictions) → create Coupon Restriction → open it → add User Group → Save.
  - **Email**: in the same restriction, enter the customer/email requested by the sub.
  - **Email hash**: enter the email; the hash is generated on Save.
- Demo for all three: not logged in / not in the group / wrong email → coupon **not visible** (popup says voucher code not available); correct account → coupon visible in My Voucher.
- Q&A: customer lists usually come from the sub as an **email list sent by email**. Few customers → enter individually via email; many (1,000 or 10,000) → **user group** restriction; user group creation is the same as in promotion and will be explained in the promotion session.

### 3. Restriction and promotion rule setup (Chong) (51:00 – 1:13:30)
- Use case: **next-purchase** (retention) promotion: the sub collects customers who bought this month and next month creates a promotion with a dedicated coupon. The customer sees it in cart/My Voucher after logging in even if they never read the email.
- Two restrictions are needed: one on the **promotion rule**, one on the **coupon**.
- Applies to **single-code coupon**; multi-code are separately distributed, so not used here.
- Coupon → Administration → **SingleCodeCoupon.couponRestrictions**; fields **Customer** (multiple customers), **Email** (one email), **Email Hash**, **User Group**. Difference between Email and Email Hash: Chong did not remember, to answer later; the team does not use email hash in practice.
- Many customers: raise a ticket to **create a user group**, then attach it to the restriction. Chong recommends **creating a new user group each time**. VN team should create its own test user group of team members.
- Customer lists are personal data: **never on the ticket**; subs send by email; ask them to remove it if posted.
- Q&A: is "Customer" a customer with orders? No, a customer who **registered a Samsung account**.
- **Multi-code** is normally not displayed (only the prefix would show); distributed offline, via CRM, **e-promoters**, in-store sales agents, so the business knows who handed out codes. **Single-code** is reusable by anyone, so it is shown on the website/cart.
- Logged-in customers see a button in the cart (VN: "Xem mã khuyến mãi") opening a popup "Mã khuyến mãi của tôi" listing their coupons.
- **Site-level config** decides whether vouchers are displayed at all (name not stated), plus coupon-level **Hide in My Voucher Page**. If the site is off, the coupon is hidden regardless. Many subs choose **not to display** to avoid VOC (customer sees a code that cannot be applied). Malaysia displays to **internal employees** (sport award, mobile subsidy, birthday voucher).
- **Must match the promotion rule**: (1) user group in the **coupon restriction**; (2) the **same user group** in the **promotion rule** (customer condition: user group or customer email by Samsung account). Mismatch → coupon may show to everyone and cause VOC. KB (Promotion Setup): Customers → Customer ID → General → Groups → add User Group.
- Chong's verification: after setup keep **Hide = True** and publish; then set False and test with a correct and an incorrect account; if OK go live, otherwise hide again and review.
- Prefer **Customer** (multi-select) over **Email** (single; works for non-logged-in). This promotion type is usually for existing accounts; if a customer is not found, tell the sub.
- Test result (global ticket): not in group / wrong customer / email hash → not visible and not applicable; correct group → visible and **Apply code** auto-applies to the cart.
- New coupons default to **Hide in My Voucher Page = True**; set False to show. Careful: when live it appears on My page and the cart of every customer in scope.
- Q&A: must both sides use the same type? Yes — customer email on both or user group on both. Display only informs; who gets a discount and how much is decided by the promotion rule.
- Reference ticket **HGE-11315** and the coupon guide (PDF/PowerPoint) were shown; no more questions.

## Difficult points and open issues
- User group/customer must match between coupon restriction and promotion rule, otherwise coupon shows to everyone or is visible but unusable (VOC).
- Email vs Email Hash difference unexplained.
- Site-level display config name/location not shown; need to know which sites have it on.
- New coupons are hidden by default; flipping to False exposes them to all in scope, so test first.
- Email lists are personal data; need a safe receiving/storing method.
- Large customer lists need a user group; creation demo is deferred to the promotion session.

## Next steps
- Read KB – Coupon Usergroup Setup (HGE-11315) and the Coupon page; request the guide slides.
- Create a VN-team-only test user group to test display.
- Build a display checklist: restriction, same user group/customer in promotion rule, Hide = True while configuring, test right/wrong accounts, then False.
- Ask Chong: Email vs Email Hash; site-level voucher display config and which sites enabled. Ask Siti Sarah: user group creation and bulk adding customers (or wait for the promotion session).
