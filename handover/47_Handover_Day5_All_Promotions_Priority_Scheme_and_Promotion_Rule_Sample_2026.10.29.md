# CoE Meeting Notes – Handover Day 5: All Promotions Priority Scheme and Promotion Rule Sample (2026.10.29)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2489548830
Sub-pages (personal notes, not summarised in detail): Baopg (2489288319), Trangnnt (2491515310), Thanhvd (2489680165), TungNS – All Promotion (2489352557), Quynhltn (2489352566), Ngavt (2489385457), Ayu (2489385475), Trangdtt (2491908136).

Meeting: HELD on 29/10/2026, three recordings: 15:16 (~12 min), 15:28 (~81 min), 16:50 (~2 min, attendee screen only). Group: Promotion. Chair: Chong Haw Eong (SDSAP). Presenters: an SDSAP member in the room for PH/MY/ID/TH (recording 15:16); an unnamed SDSAP member for SG and VN (15:28, to 09:45); Chong Haw Eong from 09:45 on naming and rule configuration. PIC on Teams: Lee May Yie. BiPlus: all CoE members. References (Samsung Confluence SEAORHQ): **<Country> – Common Promotion Setup** for VN (444930499), AU (439469605), NZ (695889203), SG (444930509), TH (444930497), PH (697088558), MY (697088553), ID (697100811). Related: Day 3 Promotion Rule and Pre-order (see 05_Handover_Day3_Promotion_Rule_and_Pre-order_2026.10.27).

## Main content

### 1. Promotion priority and scheme per country
**Page frame.** Each country has a KB page *<Country> – Common Promotion Setup* (under *KB – Type of Promotion Rule*): (1) **Promotion Priority & Scheme** where the country has one; (2) **Common Promotion setup** = list of running rules **to use as templates**.

**PH (15:16, 00:00–03:50).** Table: Group, Stacking rule, Items, Voucher/Prefix, Remarks, Priority, Rule Group.
- **Group A** (rule group **phPromotionGroup**) **stacks with everything**: special price/discount row, add-on eVoucher, PWP/MBO (4600), F-code bundle (8000), Samsung Rewards (5000), Direct Discount (5000), **BOGO (9000000)**, payment offer (below 3000), VIP voucher (3060).
- **Group C** (**PH_MX_GROUP-C**) **not stackable with each other**: live voucher, ePromoter, CRP, Affiliate, Galaxy campus, Trade-in promo; mostly "Not work w tradein".
- Rule: **within one group no stacking, between different groups stacking is allowed**. PH also has a **QA matrix** (test maximum combinations: F-code + direct discount + BOGO + MBO + trade-in + SC+ + coupon + Rewards + delivery discount + payment discount).
- **Higher priority runs first** (F-code 8000 before PWP/MBO 4600; BOGO on top). Two stackable rules with the same priority both apply; run order is not fixed.

**MY (03:50–04:55).** Columns: Priority (for COE), Group, Promo 1–6, Remarks. Special price/discount row cannot be excluded from any promotion. **100000020 G1_CRP** (CRP, E-Promoter, RNPL distribution) is a **halt rule**; BOGO 1500; auto trigger without voucher 1400; **1000–1200 G2_Voucher** (first purchase, livestream, RNPL redeem, internal award, roadshow, campaign voucher) also halt rule; PWP, cart/tier discount, BMSM, SKU discount, rewards boost, payment promo stack. Only **two groups G1, G2**; no stacking within a group. If the sub gives no group, treat as stacking with all.
- Same priority inside a non-stacking group → the system picks **randomly**; if the sub wants a specific one (e.g. % over fixed), **change the priority**.

**ID and TH (04:55–07:00).** **ID has no priority scheme**: everything stacks unless the sub says otherwise; order unknown, no issues reported so far; for wrong-promotion tickets check which rules apply to the SKU in the system. ID page only has a sample table. **TH**: only **CE e-store** has priority (CE Estore Promotion Priority, groups 1–11, "all promos within a group cannot stack"; CRP 99–80 + halt rule, BMSM/tier 80, NEWMEM 35–40). **MX** stacks unless the sub's template says e.g. "PWP cannot stack with BOGO".

**Q&A (07:00–11:59).** **PWP** = purchase with purchase; **CRP** = customer relation program (e.g. compensation voucher). **Three BOGO types**: **priority BOGO** (sub gives several gift SKUs, next one used when the first runs out), **hard BOGO** (gift SKU out of stock → customer **cannot checkout**, configurable popup) and one by **stock availability** (stock check condition). The Common Promotion table lists running promotions: find the code, open the rule in backoffice and use as a template.

**SG (15:28, 00:30–02:50).** Setup is the same as other countries; **priority differs** by agreed scheme. SG always has a **VIP discount** that stacks with nothing: **priority above 1000** and **halt rule**. The page also has e-store and EPP priority tables (first purchase 303/203, RRP/promo price %, SKU target/fixed/distributed discount, BOGO), "Halt promo 1000+", "Always on promo 1000+". Common promotions are set up monthly; reading rules in backoffice is faster than the page; usually only SKU and amount change.

**VN (02:50–09:45).** Priority table: Package (600, exclusivePackagePromotionGroup, highest), FOC (600, same group), Ecobundle (400–500), voucher product level (200–300), voucher cart level and next-purchase voucher (50–100, cart threshold), payment promo (0–10–30, lowest); others use productPromotionRuleGroup.
- **Product level** = per SKU discount (2 SKUs → discounted twice); **cart/order level** = once for the whole cart; both % or amount.
- SAVINA allows **one voucher per order**; other countries check the **voucher limit** (agreed with RHQ).
- **Trigger sequence**: single price (= special price, always first) → package/FOC → direct discount (voucher or cart discount) → welcome instant discount (ad hoc) → marketing voucher → payment promotion.
- **Ecobundle** (SAVINA) = PWP (SG) = MBO: same setup (partner discount), names differ per sub; search "eco-bundle" in Jira. Priority 500 runs before 100.
- VN team has no P1 access yet. SAVINA's scheme is simple but **changes very often** (weekly price/promo changes).

### 2. Creating a promotion rule (Chong)
**Naming (15:28, 09:45–18:10).**
- The **standard name** matters because **RHQ reports** identify promotion types from it; wrong naming is a serious error and **names cannot be changed**.
- Use the Excel **promotion rule naming generator** (RHQ Confluence): Country Code, Site (B2C, EPP, SMB, O2O or EA), Platform (WEB, APP, CRP, ePromoter, **LS** for livestream), Category (free), start/end date, Promotion Type (BOGO, PWP, BMSM, PROMOTEXT, DISCOUNT, REWARDS, PAYMENT, TRADEIN, RNPL…), Free Text. "Rule Name generated" gives the name; Validation shows READY or ERROR.
- Example: **SG_SMB_WEB_SP_12AUG26_31AUG26_PROMOTEXT_AUSPECIAL-SPHME13535**.
- **Category** is tricky (promotion for TV later extended to fridges…); Chong usually uses **CE/MX**; to discuss with RHQ.
- **Free text**: ticket number or voucher code; **no underscores** (error), use hyphens. Platform **CRP** changes the list by CRP type (PPX, ESG, NRM); ePromoter has its own. Common mistakes: forgetting it is a CRP promotion, wrong month/year from copy-paste. Always use the generator.

**Create and basic fields (18:10–22:00).** Two ways: **clone** (easiest) or **bulk upload**. Manual: **Administration Cockpit → Marketing → Promotion Rules → +** → Code, Name → Done. **Code** is unique in the promotion engine (from the generator). **Name** helps the setter filter; customers do not see it **except SG SMB**, where it appears on the invoice (use "voucher apply"/"promotion apply").

**Rule Properties (22:00–25:55).** Fields: Code, Name, Status, Version, **Website**, **Priority**, **Rule Group**, **Maximum Rule Executions**, Description, Campaigns, Is Quota Enabled, Is Rewards Boost Promotion Enabled, Is Bundle, Start/End Date/Time, Deployments, Funding Type, Cost Centre, Approval Title/Description, Business PIC.
- **Website** (mandatory) = website group; empty → no site (e.g. **vnPromotionGroup** = VN e-store, EA, showcase). **Rule group** usually **productPromotionRuleGroup**; use an **exclusive group** for non-stacking. **Maximum Rule Executions** always 1. **Rewards Boost** = True only for rewards boost promotions (e.g. 1,000 points = $1, boost x8 = $8). **Do not use Campaign**; use Start/End Date. Approval Title from the ticket.

**Promotion quota (25:55–33:30).**
- **Is Quota Enabled = True** limits uses; configured in **Types → TokoPromotionQuota** (manual or bulk): Promotion Display Rule, **Max Quota**, Available, Consumed, **User Limit**. Example ID: max 300, available 261, consumed 39.
- Weakness: **temporary orders and cancelled orders also consume quota** (subs ask "10 ordered but only 5 orders").
- **Max Quota can only be increased**; to reduce, create a new rule. **One quota per rule**, no shared quota. Used mostly in **ID** and **SG** (BIN promo: first 6 card digits, bank-funded, e.g. 500 then +100); MY once for deep deals (quota 10, user limit 1). When exhausted, increase quota or publish a new rule.

**Versions (33:30–38:30).** New rule = **v0 Unpublished** (edits stay v0). After publishing v0, each edit+save creates **v1 Unpublished**; publishing v1 makes earlier versions **Inactive**. An old version can be republished (the other becomes Inactive, not Unpublished). Editing from an older version creates a new one (e.g. v3) and locks v1 until v3 is published.

**Modules, website and qualifying site (38:30–42:30).** Two promotion modules: **preview** (no approval, self-QA) and the main module (approval types are auto-published after approval). E-store websites are named **<country>PromotionGroup**. **Website** = high level; **qualifying site** (in condition) = low level (present → only that site; absent → all sites in the website group). Payment/delivery mode lookup order: **SKU → multistore → website → base store**; website and multistore of the same channel (e.g. EPP) must match. A qualifying site must belong to the chosen group; **PH EPP sits in 4 promotion groups** (PH EDU, PH EPP…), so one EPP promotion needs **4 rules**.

**Priority and verification (42:30–47:40).** Priority sets order of application; fixed-then-% differs from %-then-fixed and affects revenue. For a new promotion type put products in the cart, create a **temporary order** (go to payment without paying), capture the calculation, send it to the sub in the ticket; use the **promotion simulator** or **staging**. **Exclusive rule group** (exclusivity = true, e.g. F56 exclusive promotion group): rules inside do not stack; highest priority wins, ties chosen by the system (MY "G2 voucher" = vouchers A, B, C in one exclusive group). **Funding type** is unused.

**Why not Campaign (47:40–51:30).** Campaign attaches several periods to one rule, but editing a campaign (e.g. +10 days) creates **no new version and no approval**, and a campaign used by 100 rules extends all 100 – against HQ guidelines. Create separate rules with different dates via **bulk upload**; download to check before publishing. Self-check before and after publish is standard.

**Payment promo and cart order (51:30–55:50).** **Payment mode promo**: choose the mode to get the discount; **BIN promo**: enter card digits (6, 9 or 12 by enhancement). **Description** appears under the payment mode (e.g. "5% off selected item"); the cart on the right recalculates when the right payment mode is chosen; heavily used in flagship (HSBC card, VN NAPAS +5%). Higher priority runs first and its **message shows higher in the cart** (e.g. multi-buy 4000 above voucher WELCOME1000 3000). Deployments: only modules prefixed with the country (e.g. **PH promotion module** / **PH preview promotion module**; NZ likewise).

**Conditions & Actions (55:50–1:00:53).** **Message** = text the customer sees in cart/checkout. **Conditions**: AND by default, use a **Group** for OR. **Actions**: discount/gift (drag from Available Actions). **Second key rule: an empty condition applies to everything** (no coupon code → any coupon; no qualifying product → any product) – never leave empty. **Exercise for the VN team (staging)**: MX product condition + **cart total** ≥ 2000 → 10% off; buy an MX under 2000 plus a TV to exceed 2000 and see whether the promotion runs (cart total is over the **whole cart**).

**15 KB limit and categories (1:00:53–1:10:30).** Hybris limits a promotion rule to **15 KB**; above that it **cannot be published**. About 50 qualifying products with voucher is near the limit; **60–70 SKUs** will exceed. Fix: create a **new category** with the SKUs and switch to **qualifying categories** (existing categories only if **all products qualify**). Create under **Catalog → Categories** in the **Master catalog** (no super/sub category), add SKUs via **Include Products Upload File** (**Append** to add, Override for new) or directly; then **sync to all child catalogs**, Staged → Online. **Serious common error**: bulk editing categories on products **without append** overwrites all old categories; same for **delivery mode**. Edit only in master; if wrong, export from a child catalog to recover.

**Target customer and actions (1:10:30–1:12:20).** Target customer = selected group. Condition **coupon code** (not voucher anymore). Actions: fixed discount, percentage discount, free gift, **halt rule execution**. **Halt rule** blocks other promotions: set a very high priority plus halt for deep discounts; know the current priorities.

**Publish and checking (1:12:20–1:16:20).** **Always publish to the preview module first** for self-QA (customers cannot access it, only backoffice users via the Samsung extension). **Undeploy** stops a promotion. **Clone** is fastest (new code, dates). Unsure of the site's catalog → website **properties**. Front-end check: cart → DevTools → Network → filter "promotion" → **appliedProductPromotions** (code, description, endDate); a MY cart showed two BOGO rules applied together.

**Final Q&A (1:16:20–1:21:00).** AU has a very complete guide (Chong to update with the AU PIC the next day). **VIP discount** (SG): voucher code tied to a customer, very deep, always top priority, no other discounts. **Package promotion** (TV A + soundbar A): use the **exclusive package promotion group** so one customer buying 1 TV + 2 soundbars does not get both. **Product level** vs **order level** (e.g. 5% for NAPAS). **Welcome**: new members who never bought (extra 5%), not in every sub. The last session of the day began at 17:00.

## Difficult points and open issues
- Same priority in a non-stacking group → random pick; ID has no priority scheme so run order is unknown.
- Category in the rule name: if the sub adds product groups later the name cannot change; handling with RHQ not agreed.
- Quota: temporary and cancelled orders still consume it; increase only; no sharing between rules.
- 15 KB limit: from 60–70 SKUs use categories; bulk edit without append wipes old categories/delivery modes.
- Empty conditions apply to everything; cart-total + product condition behaviour must be verified (Chong's exercise).
- VN team lacks P1/production backoffice access to view the running sample rules.

## Next steps
- Read the 8 country Common Promotion Setup pages and the rule-creation guide (PowerPoint by Chong's team).
- Get the **promotion rule naming generator** and use it for every rule.
- Request P1 / production backoffice access.
- Do the cart-total exercise on staging and report to Chong.
- Search "eco-bundle" and promotion types in Jira (tickets of the last 3–4 months).
- Ask the SDSAP PIC: category handling in rule names; the 4 PH EPP promotion groups.
