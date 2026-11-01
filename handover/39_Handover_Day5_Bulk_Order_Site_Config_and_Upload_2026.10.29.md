# CoE Meeting Notes – Handover Day 5: Bulk Order Site Config and Bulk Order Upload (2026.10.29)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2488991784
Sub-pages (personal notes, not summarised in detail): Baopg (2489287919), Ngavt (2489090292), TungNS (2488959273), Quynhltn (2489647230), Ayu (2488959308), Thanhvd (2489090444), Trangdtt (2491875395), Trangnnt (2491744787), Kienna (2491679298).

Meeting: HELD on 29/10/2026, recording starts 13:44 (about 20 minutes). Group: Multistore. Presenter: Efni (Teams display name, Samsung). BiPlus: all CoE members. References (Samsung Confluence SEAORHQ): *Updated Bulk Store EPP* (477538927), *Bulk order site config and feature* (617668789). Related: 36_Handover_Day5_Open_EPP_and_AEM.

## Main content

### 1. What a Bulk Order EPP site is (00:00 – 01:37)
- Creating a Bulk Order site is **basically the same as creating a normal EPP site**; the session covers only the differences.
- **Bulk Order EPP site**: a portal to place **many orders with one upload**, for employees/customers of a group or **partners**; a partner uploads one template with orders for **many customers and addresses**.
- Although the template holds many orders, the submit is processed as **one (single) order** and split afterwards (see 4.3).
- KB features: inherits EPP store benefits with a separate **Bulk Order Cart and Checkout**; ordering by **Excel (.xls)** file; **real-time on-screen validation**; checkout only collects B2B-relevant information.

### 2. Bulk Order Portal: template, upload, validation (01:37 – 05:00)
- Example live NZ site **nz_amihomehub** (AMI HomeHub), URL /nz/multistore/epp/nz_amihomehub/bulk-order. No test order placed (live site).
- Like EPP, the user must **log in**, then lands directly on the **Bulk Order Portal**: **no homepage, offers or PDP**, only the upload portal.
- "How To Complete Your Bulk Order": (1) fill the .XLS template (**DOWNLOAD TEMPLATE**); (2) upload it for validation; (3) fix reported errors and retry; (4) on success click **Calculate my order**.
- Validation table (from KB test) columns: ROW ID, SKU, QUANTITY, EMAIL, FIRST NAME, LAST NAME, COMPANY NAME, PHONE, LINE1, LINE2, CITY, ZIPCODE, PARTNER CODE, UNIQUE PARTNER ID, WAREHOUSE CODE, DELIVERY CODE, CUSTOM PO; tick = valid, X = error; **Download Error Log** link.
- SKU errors are usually **out of stock** or **not active**; the sub contacts CoE to enable/check the SKU, then the customer **re-uploads** and recalculates.
- **Cart page**: shows the template products; **quantity cannot be edited, lines cannot be removed, no services can be added** → finalise the template before uploading. Checkout then follows normal EPP.
- KB: the delivery step shows only the **billing address**; **one delivery mode is preset**, not chosen by the customer; shipping addresses are not re-entered.

### 3. Creating a Bulk Order site in Backoffice (05:00 – 08:30)
- Backoffice → **MultiStore** → **+**. Wizard: Basic Data, LoginType details, ERP Config Data, Homepage Content. Fields: **Name\***, Description, **Active = TRUE**, **Channel**, **Template Site**, **Login Type**; no spaces.
- **Name (URL ID)**: lowercase **country code + underscore + free text**, no spaces/special characters; KB suggests **vn_bulk, au_bulk, nz_bulk**. **Cannot be changed after creation**; the sub normally supplies the ID. Other data from ticket/brief.
- **Login Type** default **SSO_VERIFICATION** or per sub; Properties tab also has Login Type, Payment Modes, Domain Info (Email OTP only).
- **The only Bulk-specific flag**: multistore → **Configurations** → **Is Bulk Order Store? = True** → Save. If **False/N/A** the Bulk Order Store is **not accessible**. (nz_amihomehub: Is SSO Disabled = False, Is allow Guest Access = False.)
- **Delivery mode**: Website → the site (AMI HomeHub) → Administration, **CMSSite.deliveryModes**, because subs usually want a **dedicated delivery mode** (AMI HomeHub has Standard Delivery [nz-parcel-home-delivery2] and [nz-mercury-parcel-home-delivery2]). KB: bulk store has **one delivery mode** set via **Forced Delivery Mode** (Admin tab; only one since 06/2025) and no normal delivery mode setup at multistore/website.
- **No homepage, no CMS setup needed** (KB). Configure only multistore and site.
- **No promotions** on Bulk Order sites **except Special Price** (KB).
- After creation the **sub places test orders** (sometimes Tech helps).

## Q&A
- **Role permission to access the bulk screen?** Only the multistore flag.
- **Login needed?** Yes, **no guest**; login type decided by the sub. NZ uses **EMAIL_OTP** (Login Type EMAIL_OTP, Mobile Login Type EMAIL_OTP_APP, Channel epp), login page "Welcome to the Samsung Partnership Program".
- **Who logs in to order?** The **partner** (NZ: AMI HomeHub) orders on behalf of customers; only **specific partners** may use the site. Allowed emails are in multistore → **Retirees** tab (Retiree Information). A partner must **request via the sub**; once approved the email is added to the retiree list and an **email OTP** is sent on login.
- **Limits (cart restriction, promotional quota)?** Depends on requirements; NZ has none. Multistore → **Cart Restrictions** tab (Overall Cart Restriction, Purchase Restriction, **Promotional Quota Limits**, Quota Product Exclusion) is empty on nz_amihomehub. Normal EPP has yearly/category quotas; bulk orders 10, 20… units at once, so no quota.
- **Who pays?** The **agent/partner** who uploads and checks out, not the end customer (end customers cannot access the portal). Example confirmed: 10 customers paid at the partner's store → partner fills the template → uploads → pays → goods delivered to each.
- **Order structure**: one **parent order**, then **child orders per customer address**. KB: each row is a child order, except rows with the same contact (phone, email) and address which are merged. KB (My Account): only the buyer sees order details; child orders are anonymous and hidden, a **child order CSV** with status can be downloaded.
- **Reverse flows (KB)**: **Cancellation** only for the **bulk parent order** and only **before it is split** (before fraud check completes). **Return**: **no refund** for bulk orders (parent or child). **Exchange**: parent not exchangeable; child exchangeable under normal conditions.
- **Template per country?** Should be the same; mainly **NZ** is active, AU recently got a site (not checked). KB says templates may vary by the shipping address fields a sub requests.

## Difficult points and open issues
- **Delivery mode inconsistent**: session configured CMSSite.deliveryModes on the Website (2 modes on AMI HomeHub), KB says a single mode via Forced Delivery Mode and no normal setup.
- **URL ID cannot be changed**; a mistake means recreating the site.
- Access depends on the **Retirees** list and sub-chosen login type; unclear who (sub or CoE) updates the list and the partner request process.
- Reverse flow is limited (cancel parent before split only, no refund).
- Country templates unclear (NZ active, AU unchecked).
- Special Price is the only allowed promotion; SKU upload errors are usually stock/active issues routed to CoE.

## Next steps
- Read both KBs and compare with the real **nz_amihomehub** multistore/website.
- Ask Efni: which is the standard place for the bulk delivery mode; who updates **Retirees** (sub or CoE, file or manual) and a sample ticket for new bulk sites; live bulk sites (NZ, AU…) and country templates.
- When receiving a "create bulk site" ticket, verify **Name / URL ID** with the sub first.
