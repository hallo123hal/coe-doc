# CoE Meeting Notes – Handover Day 5: Coupon Single Code vs Multicode and Coupon Ingestion (2026.10.29)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2489057307
Sub-pages (personal notes, not summarised in detail): Baopg (2489581730), Ngavt (2489254015), Ayu (2489516275), Trangdtt (2489320765), Thanhvd – Coupon code creation (2488959105), Quynhltn (2489221395), Trangnnt (2489680015), KienNA (2492006952), one untitled draft (2489287941).

Meeting: HELD on 29/10/2026, recording starts 10:27 (about 75 minutes); this page covers 00:00–42:50, the rest is in 38_Handover_Day5_Coupon_Display_and_Usergroup. Group: Promotion. Chair/presenter: Chong Haw Eong (SDSAP, PIC); also Siti Sarah Binti Azman (SDSAP). BiPlus: all CoE members (Merch, Tech, QA). References (Samsung Confluence SEAORHQ): *Coupon* (581409234), *KB – Serial Voucher Code GCDM Ingestion* (444930600). Related: Day 4 RNPL (see 28_Handover_Day4_RNPL).

## Main content

### 1. Voucher vs coupon: current state and general config
**State (00:00–04:05)**
- BBT and UAT for **coupon** ran in May this year; SEAO now uses coupon.
- **Serial voucher is still used for RNPL** because coupon does not yet support RNPL for **FI posting**.
- Otherwise **do not create new vouchers** (Backoffice → Marketing → Vouchers → "+" → Promotional / Serial Voucher) and do not create new promotions using vouchers.
- Running promotions that use vouchers continue; if a sub needs more codes, still **generate more voucher codes** for that promotion. Singapore example: CRP vouchers **SL6** ("SG CRP"), SL8, TV1, TV4; RHQ confirmed by email SG may continue until they migrate to coupon (no plan yet).
- A ticket asking for a new promotion with a voucher code → **check with RHQ**; normally not allowed unless justified (e.g. access promotion, CRP code).

**Coupon Code Generation Configuration and Redemption (04:05–06:30)**
- Same function as voucher, different UI: Backoffice → Marketing → **Coupon Management** → Coupons / Coupon Code Generation Configuration / Coupon Redemption.
- Code Generation Configuration defines **Coupon Part Count** and **Coupon Part Length**; standardised per country (**MULTI_CODE_CONFIG_VN**, _MY, _SG, _TH, _PH, _ID, _NZ, _TW …). For multi-code **use the existing config of that country**, do not create a new one; CoE has its own config for testing.
- Taiwan, Hong Kong: nothing to do here. AU lives in a different environment (unclear, transcript sounds like "P1").
- **Coupon Redemption** = lookup of who used which coupon on which order (equivalent to Voucher Invalidation).
- A promotion uses **either coupon or voucher**, never both; mixed does not run.

**Overview and enabling coupon (06:30–08:30)**
- **No automatic migration** voucher → coupon; recreate as coupon.
- **Serial voucher → Multi-Code Coupon** (one-time code per customer; prefix now **4 alphanumeric characters**, previously 3). **Promotional voucher → Single-Code Coupon** (one shared code, per-customer and total redemption limits).
- Pros (slide): unlimited prefixes for multi-code, customisable format (now fixed by config). Con: a specific coupon cannot be found from the promotion rule.
- Enable per country: Backoffice → Admin Cockpit → Types → **TokoConfigProperty** → **toko.voucher2coupon.migration.enabled.xx** (xx = country code) → **true**; then customers can use both voucher and coupon codes in the cart.

### 2. Creating coupons
**Single-Code Coupon (08:30–16:20)**
- Administration Cockpit → Coupon → arrow next to "+" → **Single-Code Coupon** → fill popup → Finish. Codes normally **UPPERCASE**.
- **Coupon codes share one pool across all countries**: a code created for country A cannot be reused by B, even for regional campaigns; check creator in the system or search the code in Jira. Do not reserve codes in advance on sub request (SAVINA once asked for 10–20).
- **Name**: shown in the cart under the coupon code; usually **leave blank**, no Jira ticket number or odd text.
- **Maximum Redemptions per Customer** / **Maximum Total Redemptions** (e.g. 10 and 18: one customer using 10 leaves 8 for others; one redemption = one order).
- **Start/End Date**: normally blank, validity follows the **promotion rule**. Only set when narrower than the promotion (e.g. a 3-hour live code); must stay within the promotion period.
- **Active** = false → cannot be applied even if the promotion is published. Edit details after creation.
- Q&A: must coupon start date be after promotion start date? Answer: it must fall within the promotion period, otherwise it cannot be applied.

**Multi-Code Coupon (16:20–23:05)**
- Administration Cockpit → Coupon → "+" → **Multi-Code Coupon**. **Do not edit** Coupon Alphabet, Coupon Code Seed Number, Coupon Code Signature (auto-generated); ignore Time Created, Exclusive.
- **Coupon Code Generation Configuration**: pick the country config (e.g. MULTI_CODE_CONFIG_VN). Per RHQ: separator "-", **part count 3**, **part length 4** → **XXXX-abcd-efgh-ijkl**.
- **Coupon Prefix**: 4 letters/digits, usually uppercase, no symbols (slide); **cannot change after generating**. Prefix given by the sub or chosen by CoE; avoid sensitive letter combinations. Active = true.
- Generate: open the coupon (e.g. **QBH8**, Singapore) → enter number of codes → **Generate** → Save → file under Generated Coupon Codes. 1 million codes was generated in a few minutes.
- Codes are sensitive: **encrypt and email** to the ticket creator, **never attach in the ticket**.
- Multi-code is always single-use per code, so no redemption limit is needed; total = codes generated.

**Promotion rule with coupon and Sign-up Coupon (AU only) (23:05–26:15)**
- Promotion rule: instead of the voucher code condition use **coupon code** (Promotion Rules → Conditions & Actions → Use Coupon code). The cart shows coupon code and name.
- **Sign-up coupon (AU only)**: website has promo configuration and a sign-up flag; a newly registered customer receives the configured coupon. The online store's base store has a **coupon config**; coupons are issued only if the website allows sign-up promotion.
- AU also has **Customer Coupon** in Administration Cockpit; promotion rule condition **Carts Using Sign-up Coupons** (e.g. SIGNUPTEST) plus SKU condition, then a discount action.

### 3. External coupon and GCDM ingestion
**External coupon code (26:15–31:00)**
- Q&A: what differs between coupon and voucher on the NERP side? NERP checked all fields and F5 posting before rollout; coupon is posted like voucher **except RNPL** (still voucher). Customers/business cannot tell them apart.
- Used when a sub has its own code list (track source, affiliate…). Step 1: create a **Multi-Code Coupon** (no edits, choose config, Save).
- Step 2: Coupons → **External MultiCode Coupon File Upload** → select the coupon → attach a one-column **.xlsx** whose first row is **externalSerialVoucherCode** (file name irrelevant) → Upload → Submit. Format is the sub's; if none, use the sample format (ABCD-…-…-…).
- System says "Data upload in progress for file … Cron job name is …"; check that cronjob succeeded.
- Verify: log in as **csadmin** (not admin) → **External Serial Voucher** and **External Serial Voucher Codes**.
- RNPL with coupon: **not applied**, possibly in future.

**GCDM ingestion – prepare the code file (31:00–36:45)**
- **GCDM** is the sub's CRM / mass-email system (like eDM); codes are sent to customers from there, not from the site. A ticket saying "ingest" means pushing codes to GCDM. Doc: **KB – Serial Voucher Code GCDM Ingestion** (still valid).
- Steps 1–2: create the coupon (not voucher) and **generate** the requested number, Save.
- Step 3: open the generated csv (Generated Coupon Codes) → change **Identifier** and **Real filename** to: **{country lowercase}_{quantity}_{prefix}_vouchercodes_{created YYYYMMDD000000}_{start YYYYMMDD}_{end YYYYMMDD}.csv**. "vouchercodes" stays unchanged; time = 000000.
- Example: **sg_180000_QBH8_vouchercodes_20260625000000_20260722_20260813.csv** (180,000 codes, prefix QBH8, created 25/06/2026, valid 22/07–13/08 per promotion rule).
- KB note: if codes are not tied to a promotion or used all year, set end date to next year.

**GCDM ingestion – cronjob SEAO-GCDM2.0-voucher-interface-v1 (36:45–42:50)**
- Backoffice → CronJobs → **SEAO-GCDM2.0-voucher-interface-v1** (tokoVoucherCodeGCPUploadJob) → **Administration** tab.
- **serialVoucher** blank, **storeId** blank, **GCP Folder Name = SEAO**, **Voucher Codes Media** = the renamed file. Change nothing else. Save → Run.
- Verify: Log tab → download log; successful upload line (KB: File Transfer Status = true, "Cronjob is done"). KB: files on GCP are picked up at minute 10 and 40 each hour.
- The cronjob is **shared**: a failed run breaks later runs by others; check the format carefully.
- Q&A: is the file name set by the system? No, rename manually (Identifier and Real filename) per Confluence, then select that file in the cronjob.
- Afterwards: download the file and email to the ticket creator if needed; **share codes with QA** for testing. Only **coupon** is ingested now, not voucher.

## Difficult points and open issues
- **Coupon code pool is shared across countries**: check existing codes (system, Jira) before use.
- RNPL still runs on serial voucher; old voucher promotions (SG CRP SL6, SL8, TV1, TV4) still run — distinguish when receiving tickets.
- GCDM ingestion depends on exact file naming and a shared cronjob.
- Prefix characters: slide says letters/digits only, but the session said "dash, underscore yes"; confirm. Prefix is immutable after generation.
- AU environment (sign-up coupon, Customer Coupon) differs from other countries' BO; access unclear.
- External coupon checks need **csadmin**.

## Next steps
- Read the Coupon page and KB – Serial Voucher Code GCDM Ingestion; request the coupon guide slides (PDF/PowerPoint).
- Build checklists: coupon creation (single/multi, country config, prefix, blank name, limits, active, duplicate check) and GCDM ingestion (file name, 3 cronjob fields, log).
- Agree how to send codes by encrypted email to ticket creators and QA.
- Ask Chong Haw Eong: list of voucher promotions still allowed (SG CRP …) and RHQ process when a sub wants vouchers; allowed prefix characters; csadmin and AU access for the VN team.
