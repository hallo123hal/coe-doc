# CoE Meeting Notes – Handover Day 6: EPP Structure and Login Type and EPP Checklist (2026.10.30)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2491613217
Sub-pages (personal notes, not summarised in detail): Baopg (2491810186), Trangnnt (2491744812), Thanhvd (2491646324), TungNS (2491220324), NgaVT (2492006644), Ayu (2491810226), Quynhltn (2491810292).

Meeting: HELD on 30/10/2026, recording starts 13:54 (about 37 minutes), Teams + meeting room. Group: Multistore. Presenters: Hana (Siti Nur Farhanah Binti Mohd Noor, SDSAP) for EPP Structure and the New EPP Setup Checklist; Chong Haw Eong (SDSAP) for EPP classification, promotion groups and the RHQ approval flow. BiPlus: all CoE members. From about 11:30 to 23:55 the shared screen froze on the EPP Structure pages, so the promotion rule / Hybris parts have no screenshots. References: **Country EPP Structure** (Samsung SEAORHQ page 444929927; copy in BiPlus Knowledge Base page 2477490822). Related: Day 5 Open EPP and AEM (36_), Day 5 Bulk Order (39_), Day 4 VN SMS OTP (33_), Day 6 EPP Multi Login (50_).

## Main content

### 1. EPP Structure: EPP sites and login types per country
**Country pages (00:00–02:00).** SDSAP consolidated the EPP structure from Hybris into one Confluence page per country, **<Country> EPP Structure** (tree KB – Multistore → KB – EPP). Main columns: **Site ID**, Description, **Catalog version**, **Access Type** (= **login type**), **Active**, **Channel Type**, **Partner Number**, **Channel**, **URL**. TH example: group **D2C** (th: Guest; th_secretsale: Access code), group **EA_O2O** (th_tgcellular, th_powerfull, th_jaymart… login type **O2O_Cockpit**, channel type th_ea), Test Site (epptse2), VIP (ssvip), Internal (tsestaff).

**AU page, partner number, O2O cockpit (02:00–04:50).**
- In Hybris EPP sites are under **Multistore**; filter **is active = true**.
- AU page adds **Is SSO Disabled**, **MX Tier**, **CE Tier**, **Promotion Group** (e.g. anz_auPromotionGroup), Catalog (Toko AU EPP Product Catalog); latest source file "Company EPP MASTER (28_10_26).xlsx". E.g. anz_au EMAIL_OTP, Tier 2; asc_ea_au O2OCOCKPIT, SSO disabled TRUE, Estore Price.
- **Partner number / sold-to** are **NERP** numbers and are **always supplied by the sub** for a new EPP site.
- **O2O cockpit** login through the O2O login screen on Hybris, either **via BO** or **EA Direct Access** (add yourself to the **EA Direct Access** user group, then open the URL).

**EPP classification (04:50–07:00).** Each sub manages EPP differently; the sub knows each site's purpose. **Internal EPP** (Samsung staff or very close partners, **highest discounts**), **External EPP** (partners), **affiliate**, **SMB partner**. TH has many SMB/EA O2O sites, only some active; other TH groups: **Aggregator** (shared scheme, e.g. sligeneral, scgid, kbank), **Targeted** (genz, epphos, eppgov), **B2B MX**, **SMB CE** (dealer ordering). Subs may request promotions **for one multistore** or **for many sites at once** (via Jira). MY and SG also have education sites; PH has EDU, government, internal, external.

**Promotion group (07:00–09:05).** PH page columns: ID, Name/Description, Channel, Login Type, Catalog, **Promotion Group**, CMSSite.HomepageUrl. EPP promotions apply **by the site's promotion group**: channel phepp → **pheppChannelPromotionGroup**, EDU → **pheduChannelPromotionGroup**, plus phss, phfl (OFW). For a 10–15 site request know which promotion group each site is in. OFW can use phflChannelPromotionGroup with a site ofw condition or its own group. phlazada / phshopee = **marketplace**; **samsung_loyalty_store** = special promotions for a customer group. **Test EPP** = sites only CoE accesses, to test CMS, promotion, referral, campaign (sometimes testing on a real EPP site is needed).

**Q&A (09:05–19:30).**
- Multistore properties contain **Mobile Login Type** next to Login Type; it **must always equal the normal login type**.
- **Sold-to code** and partner number are provided by the sub when requesting a new site.
- **Promotion group** groups promotions; a site in a group can use that group's promotions. Rule creation always has e-store, EPP and SMB types (e.g. PH affiliate in pheppChannelPromotionGroup). One group has many EPP multistores and **many rules can belong to one group**. **Gotcha:** a rule set to the **wrong promotion group** will **not trigger** for the site.
- Changing a site's promotion group is almost never requested: a default is **mapped automatically when the EPP site is created**. EPP sites go to the **EPP channel promotion group**; e-store to the country group (e.g. **AU promotion group**). AU: **AU SMB** group for SMB/business only; **AU EPP channel promotion group** for all EPP sites. (The live Hybris demo was lost because the screen froze.)

### 2. New EPP Setup Checklist: creating a new EPP site
**Checklist and RHQ approval (19:30–23:00).** Page **0. KB – New EPP Setup Checklist (WIP)** (KB – Multistore): columns Field name, Description, Example of info subs provide, Documentation (screenshots of the backoffice Properties tab). A new-site ticket must include **catalog version**, **access type** (login type), **channel**, **delivery mode**, **payment mode**, **warehouse**, **recurrence**, **cart quantity limit**, **cart purchase limit**, **category purchase limit** (if any), and usually **which site to clone**. Example: catalog nzEppProductCatalog, access type EMAIL_OTP, sold-to 2407111. **If the sub gives no domain for email OTP, enter a dummy domain** (e.g. dummy.com).
- Flow: the sub must **get RHQ approval first** (usually attached to the ticket). On receipt CoE **asks RHQ to confirm in writing on the ticket** before acting, and checks the info is sufficient with this checklist.

**Sample AU ticket and New Site Template (23:00–25:30).** Ticket **AUME-18211** "New EPP site creation – Member Benefits" with an Excel **New Site Template**: Which site can we clone from (au_seniors, "excluding Partner Number and new ERP/ERP FI configs need to be created"), **New Site ID** (must start with AU_), New Site Name, Business background; then fields that differ from the cloned site: Catalog version (Estore/EPP/SMB), Access Type (Domain / Access code / Verify Code / EA O2O), Sold to code and Partner Number (**NERP data**), Channel (**30 B2C & SMB / 31 B2B**), Delivery Mode, …

**Login types (25:30–27:50).** Email OTP = login by email, system sends an **OTP by email**. Dropdown **Login Type** in Multistore → Properties (e.g. woolworths_au). Most used: **email OTP**, **access code**, **O2O cockpit**; others: **SSO access code**, **domain**, **verification code**, **GenID**. Values on screen: EMAIL_OTP, EMAIL_MOBILE_OTP, EMAIL_OTP_APP, EMAILID_ACCESSCODE, NOSSO_ACCESSCODE_EMAIL_SMS_OTP, O2OCOCKPIT, SSO_ACCESSCODE, SSO_ACCESSCODE_OTP, SSO_DIRECT_ACCESS, SSO_DIRECT_ACCESS_V2, SSO_DOMAIN, SSO_DOMAIN_OTP, SSO_DOMAIN_GENID_VERIFICATIONCODE, SSO_GENID, SSO_HASHACCESSCODE, SSO_VERIFICATIONCODE. **Mobile Login Type** and **Multi Login Type List** are also on the screen, but Multi Login Type List was **not explained** (see EPP Multi Login session).

**Creating the multistore (clone) and the Tech part (27:50–31:30).** Fields in the checklist/template are blank on a clone and must be filled in backoffice. Wizard **Create New MultiStore**: 1 **Basic Data** (Name = site ID, Description, Is Active, Channel, **Template Site** = site to clone, Login Type), 2 **LoginType details**, 3 **ERP Config Data**, 4 **Homepage Content**. **Raise to Tech**: **sold-to code**, **partner number**, **ERP config** (Merch has no permission). Template ERP rows: GERP config clone from, GERP.Description, **GERP.PartnerNumber** (NERP site Sold To Code), GERP.SalesOrg, DistributionChannel, Division, CompanyCode, ERPFI config clone from, ERPFI.description, **ERPFI.Sold To** (NERP site Payercode), ERPFI.Costcenter. Other rows: Disable Back Order, Anonymous cart removal age / Cart removal age (seconds, e.g. 1209600), Account Expiry (EPP link validity, e.g. 31536000), Registration Expiry (OTP validity, e.g. 1800), Send Renewal Reminder Email, Enabled Min Order Quantity, isSme, Use Multistore Pricing, **Is SSO Disabled**.

**COEC ticket for ERP config (31:30–34:25).** After Merch creates the multistore, raise a **COEC** ticket (e.g. **COEC-29110** "[SEAU] Setup ERP Config new site (au_member_benefits)") to update **ERP and ERP FI config**; Tech reads the same template; checklist GERP rows say "tech" and explain taking the PK from the cloned site's ERP config. Summary flow: receive request → **RHQ approval on ticket** → do own part → raise **COEC** (Tech) → finish the rest. The VN team asked to attach sample tickets to the doc; Hana agreed.

**New site is empty (34:25–36:45).** A new EPP site has **no price and no promotion**: always ask the sub for the **price list** and which promotion applies. Delivery mode is part of the template info from the sub. The next session (SMB promotion) uses another Teams link.

## Difficult points and open issues
- Site must be in the right **EPP channel promotion group**; a wrong group means no trigger. The promotion rule practice was not visible (screen froze 11:30–23:55).
- The full list of login types and their meaning (SSO_*, GENID, HASHACCESSCODE, DIRECT_ACCESS_V2…) and **Multi Login Type List** are unexplained.
- Merch cannot update **sold-to, partner number, ERP / ERP FI config**; must raise COEC to Tech – unclear how BiPlus Tech will take this.
- Two RHQ approvals (sub first, CoE again on the ticket) must be done before creating a site.
- New sites are empty: price list and promotions are easy to forget.
- Steps 2–4 of the Create New MultiStore wizard were not demonstrated.

## Next steps
- Read the <Country> EPP Structure pages (AU, TH, PH, MY, SG, VN…) and the New EPP Setup Checklist.
- On staging compare a real EPP multistore (Login Type, Mobile Login Type, Promotion Group, sold-to/partner number) with its EPP Structure page.
- Ask Hana to attach sample tickets (AUME-18211, COEC-29110) and the New Site Template; ask SDSAP about the remaining login types and Multi Login Type List, and to redo the lost promotion group demo.
- Tech: learn to create ERP / ERP FI config for a new site (take the PK from the cloned site).
