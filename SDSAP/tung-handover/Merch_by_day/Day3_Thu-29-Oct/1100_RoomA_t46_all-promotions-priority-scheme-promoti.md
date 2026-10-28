# Day3 - Thu-29-Oct 11:00 Room A - Topic 46 All promotions - Priority Scheme - Promotion rule sample

> Merch services in this session: MER-PRM-01, MER-PRM-04, MER-PRM-02, MER-PRM-09 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 10 | MER-PRM-01 | Product discount promotion (fixed price, percentage) | Must | Sprint 3 | Thành | 150 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483630781 |
| 15 | MER-PRM-04 | COMBO promotion | Must | Sprint 3 | Ayu | 52 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483630951 |
| 25 | MER-PRM-02 | Cart discount promotion (discount on total cart) | Optional | Sprint 4 | Thành | 36 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728289 |
| 28 | MER-PRM-09 | Multi-promotion batch (more than 2 promotions) | Optional | Sprint 4 | Thành | 23 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728859 |

## Session: Topic 46 - All promotions - Priority Scheme - Promotion rule sample

| Field | Value |
|---|---|
| Inventory topic | #46 - All promotions - Priority Scheme - Promotion rule sample |
| Call (BiPlus plan v3) | Thu 29 Oct 11:00, Room A |
| SDSAP date / status | 29-Oct |
| Component / area | Promotion / Service |
| SDSAP PIC | Siti Nur Farhanah Binti Mohd Noor, LEE MAY YIE |
| Samsung Confluence link | VN - Common Promotion Setup; AU - Common Promotion Setup; NZ- Common Promotion Setup; SG - Common Promotion Setup; TH - Common Promotion Setup; PH - Common Promotion Setup; MY - Common Promotion Setup; ID - Common Promotion Setup |
| Maps to (BiPlus) | MER-PRM-01 Product discount promotion (fixed price, percentage), MER-PRM-02 Cart discount promotion (discount on total cart), MER-PRM-03 BOGO promotion, MER-PRM-04 COMBO promotion, MER-PRM-09 Multi-promotion batch (more than 2 promotions) |
| Priority | Tier 1, Sprint 3, Must |
| Verdict | **Reuse** |
| BiPlus PIC for the topic | Ayu |

**Why this verdict:** Now links the Common Promotion Setup page of all 8 markets.

**Questions for SDSAP (from the sheet):** Where is the priority (stacking) scheme written? Which market rules differ most?

## MER-PRM-01 - Product discount promotion (fixed price, percentage)

> Tier 1 #10 | Must | Sprint 3 | Owner: Thành | QA: Xuan, Nga | ~150 tickets/month | M3 Promotion & Offer

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483630781  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
A **product-level discount rule** (target fixed price, percentage off or fixed amount off on named SKUs or categories) built in the Hybris promotion engine, live at the exact start date-time in market time and ended on time. A wrong value, missing exclusion or unplanned stack sells devices below the approved price on many sites at once.

## Key facts
| Item | Detail |
|---|---|
| Volume | 1,420 tickets in 2026, ~150/month, 8 markets |
| Roles | Doer: Merch operator. Checker: QA team member (mandatory) in the promotion simulator. Approver: Shift Leader (+ Lead/Deputy for E4), then the subsidiary approvers in Knox. Sub-Lead review for sitewide rules, >30% off, long EPP site lists |
| SLA | **Medium**: 16h resolution, 2h initial; internal 10h24 / 78 min - for 1 or 2 promotions. 3 or more -> MER-PRM-09 (Low 24h). Waiting for Knox is not a pause |
| Change class | **Normal change, R3**: QA pass -> Shift Leader -> Knox -> live publish. E4: exposure >=10,000 USD, >5 markets or a 500-SKU file |
| Biggest risk | Wrong value, missing exclusion or unplanned stack |

## Recognise the ticket
Titles: *offers, promotion, payment promotion, EPP, targeted, extend, live stream, code, go live*. A brief (12 fields: SKUs, value, basis RRP vs selling price, cap, period + time zone, sites, stacking, Knox path). **Not this service:** regular/special/discount-row price MER-PRC-01/02/03 - cart total discount, bank cashback, BMSM MER-PRM-02 - BOGO PRM-03 - combo/MBO/PWP PRM-04 - cross-sell PRM-05 - 3+ promotions PRM-09 - codes CPN-01/02 - offer page AEM-02 - benefit text TXT-02 - expired rule clean-up HSK-01 - wrong discount live INC-01.

Variants: **V1 new product discount** (most common, weekly AU/NZ "Offers") - V3 EPP/targeted-store (~36%) - V2 payment-conditioned (VN, SG; bank/BIN/instalment) - V5 extend or amend (~11%) - V6 deactivate/supersede/remove (~12%) - V4 live-stream / code-gated.

## Workflow (V1, key steps)
1. Count promotions at intake (1 rule = 1 promotion, one store scope; mirrors may count - confirm with RHQ). 2. Price sanity PS-01..PS-10 (PS-02 drop >=20% needs written confirmation; PS-05 >=30% is a hold). 3. SKU readiness (approved, PURCHASABLE, priced). 4. Search overlapping rules - **Website filter is mandatory** (unfiltered search times out) - and fill the stacking matrix STACK-01. 5. Rule code `{CC}_{Site}_{Platform}_{Category}_{ddMMMyy}_{ddMMMyy}_{Type}_{free text}` - the commonest strike cause when wrong; code cannot be changed later. 6. Action: *Percentage / (RRP) Percentage / Fixed discount / Target fixed price on products*; mirror every channel in its own promotion group. 7. Save -> publish to `<cc>-preview-promotions-module` -> simulator (qualifying + non-qualifying cart per channel, stacking). 8. Internal check line -> QA REVIEW -> Shift Leader -> publish to the live module -> Knox popup. 9. Knox jobs: status `0 2 * * *`, publishing hourly at :12 -> visible up to ~70 min after approval. 10. REVIEW SETUP (no feedback by 23:59 the day before go-live: publish on time, template D) -> live check within 30 min -> LAUNCH VERIFICATION with end date for MER-HSK-01.
- **v0.2 says QA in the preview module first and Knox after QA pass**; the Samsung KB page says publish after Knox then QA. Follow v0.2 (confirm in KT).
- Edit of date, action, condition or website needs Knox again; never leave two versions KNOXAPPROVED. A rule is limited to 15 KB (use categories for long SKU lists). Platform-specific conditions are banned since 1 Dec 2025.

## Known errors
Not visible after approval (publish job / time zone) - price below approved (unplanned stack) - price off by a few units (RRP % rounding -> target fixed price) - discount on accessories (category too wide) - works on B2C not O2O/EPP (mirror missing) - far above expectation (no cap) - edit not visible (not republished/re-approved).

## QA checklist
Count 1-2 and other actions split; brief version; code standard; sites and mirrors; dates in market time; SKUs and exclusions; value to 2 decimals; cap/max runs; non-qualifying SKU not discounted; stacking as matrix; message per language; live check passed.

## Samsung KB to read first
KB Promotion Rule Knox Approval (2477949466) - KB Promotion Creation (2477688331) - KB Knox Approval Promotion (2477916786) - Knox Approval FAQ (2477359759, APE017) - the market Common Promotion Setup page (VN, SG, SEAU).

## MER-PRM-04 - COMBO promotion

> Tier 1 #15 | Must | Sprint 3 | Owner: Ayu | QA: Xuan, Nga | ~52 tickets/month | M3 Promotion & Offer

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483630951  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
A **combo offer** in the promotion engine: a discount or fixed price on companion (child) SKUs when bought with a main product - multi-buy offer (MBO), purchase-with-purchase (PWP) price, eco bundle or package. One wrong pair, ratio or base price sells accessories below cost or fails to apply an advertised bundle.

## Key facts
| Item | Detail |
|---|---|
| Volume | 487 tickets in 2026, ~52/month, 8 markets (ID and VN ~two thirds) |
| Roles | Doer: Merch operator. Checker: QA (mandatory), pair/ratio/special-price tests in the simulator. Approver: Shift Leader (+ Lead/Deputy E4), then Knox. Sub-Lead review above 50 pairs or several child categories |
| SLA | **Medium** 16h / 2h initial for 1-2 promotions; 3+ -> MER-PRM-09. Waiting for Knox is not a pause |
| Change class | Normal change R3 (QA -> Shift Leader -> Knox -> publish). E4 as MER-PRM-01 |
| Biggest risk | Combo price stacks on a child's special price and sells it below the display price; wrong pair or ratio discounts the wrong SKU |

## Recognise the ticket
Titles: *bundle, package, MBO, multi-buy, PWP, eco bundle, get ... free, single price setting, [EXTEND PROMOTION]*. A **pair matrix COMBO-01** (main -> child, value, basis, ratio, display price per channel). **Not this service:** one SKU sold as a bundle (F-code) -> MER-PRD-05 - PWP choice on the buying/add-on page -> MER-PRF-05 / MER-BYP-01 - free gift -> MER-PRM-03 - cross-sell at add-on step -> MER-PRM-05 - SC+ plan discounts -> MER-PRM-07 - one product only -> MER-PRM-01.

Variants: **V3 package/bundle** (~80% of tickets: ID refrigerators/AC, VN eco bundle) - V1 MBO (~31%) - V4 extend/amend (~30%, month-end) - V2 PWP fixed child price - V5 deactivate/remove.

## Workflow (key points)
- **Price check first**: compare each combo price with active/planned special price (PriceRow SPECIAL). Engine behaviour when both apply is not documented, so the simulator test with the child on special price is **mandatory** (KE-01).
- Partner-product actions: *Percentage / (RRP) Percentage / Fixed / (RRP) fixed / Target fixed price on partner products*; container A = main n, container B = child m (ratio); selection strategy (MOST_EXPENSIVE, CHEAPEST...) decides which child; Maximum Rule Executions limits children. Use the *(RRP)* action when the base is RRP (KE-07).
- Package: all items must be present - *Target bundle price* (one container per item) or *Distributed discount on target products* (Knox D111); rule groups `bundleFixedPriceRuleGroup` / `exclusivePackagePromotionGroup`; VN priority Package/FOC 600 > eco bundle 400-500. Hard bundles (indoor/outdoor AC) also need the product reference MUST_PURCHASE_WITH / CONSISTS_OF (MER-PRF-04).
- Rule code Type = DISCOUNT or PWP (MBO/BUNDLE/PACKAGE are not Type tokens - put them in the free text).
- Same lifecycle as MER-PRM-01: preview module -> simulator -> QA -> Shift Leader -> Knox -> live check; extension = End Date only, same code, but Knox again.
- Add-on journey price display: `cartLevelProductPromotionalPrice` refreshed by `<cc>_Toko_UpdateProductCartLevelPromotionPriceJob`; if missing, check the reference (PRF-05/BYP-01), the job, then TEC-TSP-05. The "Auto MBO" enhancement was **dropped by RHQ** - do not build from it.

## Known errors
Child below display price (stacked on special price) - discount on child without main - two children for one main (ratio/max runs) - package applies with one unit - not working on O2O/EPP (mirror) - offer missing after month end (extension not raised) - wrong base (percentage vs RRP action) - combo price not on add-on page.

## QA checklist
Matrix version + codes; each pair gets the value; child alone not discounted; ratio / max children; special-price interaction as agreed; package needs all items; exclusions; mirrors per channel; dates; stacking; message and add-on display; live check.

## Samsung KB to read first
KB Promotion Rule Knox Approval (2477949466) - KB Product Reference - Bundle and Gift (2477655578) - KB Promotion Creation (2477688331) - KB [VN] Promo setup for BMSM (2477327751) - VN Common Promotion Setup (2477458904).

## MER-PRM-02 - Cart discount promotion (discount on total cart)

> Tier 1 #25 | Optional | Sprint 4 | Owner: Thành | QA: Xuan, Nga | ~36 tickets/month | M3 Promotion & Offer

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728289  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
An **order-level discount on the cart total**, triggered by a payment condition (bank/card cashback, card BIN, instalment tenure) or by spend/quantity thresholds (buy more save more, minimum spend), live for the exact period. A wrong tier, bank or threshold gives the wrong amount on every qualifying order and is hard to recover after the order is placed.

## Key facts
| Item | Detail |
|---|---|
| Volume | 336 tickets in 2026, ~36/month, 8 markets (ID ~half, then VN, SG) |
| Roles | Doer: Merch operator. Checker: QA (mandatory), cart tests at each tier boundary in the simulator. Approver: Shift Leader (+ Lead/Deputy E4), then Knox. Sub-Lead review for sitewide offers or >5 tiers |
| SLA | **Medium** 16h for 1-2 promotions; **each bank or scheme counts as one promotion** (confirm with RHQ), so 3+ -> MER-PRM-09 |
| Change class | Normal change R3, Knox required |
| Biggest risk | Wrong tier or threshold, cashback without the bank, or a stack with product offers |

## Recognise the ticket
Titles: *bank cashback, tiering, IPP, instalment, payment promotion, BMSM, minimum spend, cart discount*. A **CART-TIER table** (tier, min cart/qty, value, cap, bank, card type, BIN range, tenure). **Not this service:** a discount on the product line incl. "6% on the product with bank card" -> **MER-PRM-01 V2** (most live BIN/bank rules actually use product-line actions - decide cart vs product from the brief first) - coupon-triggered -> MER-CPN-02 - cashback paid by the bank after purchase is display only -> MER-BYP-02 / TXT-02 - payment option missing on a site -> TEC-SIT-05 / TEC-CFG-02.

Variants: **V1 bank/card cashback on cart** (~72%) - V3 buy more save more (~25%; VN per category) - V2 instalment tenure discount (SG, PH, TH) - V5 extend/amend - V6 stop/deactivate - V4 minimum-spend cart discount.

## Rules to remember
- BMSM is built as a **SKU-level volume discount** (action *Quantity based percentage discount on target products*, Knox D122), not a cart-total discount; if the brief wants an amount off the cart total use V4.
- One rule per tier; priorities descending in one exclusive group so only the best tier applies (KE-01). Conditions: *Cart total*, *Included Payment Mode / Bank / Bin / Installment*; actions *Fixed / Percentage discount on cart*; optional *Halt rule execution*.
- Test every boundary in the simulator (just below / at / above each threshold, best tier only, other payment, excluded SKU). **Test cards only**, never real card data.
- Decide the basis (threshold before or after product discounts) and exclude accessories / SC+ that push the cart over the threshold (KE-02, KE-05).
- Code Type token = PAYMENT (CASHBACK/IPP/SPEND are not valid tokens). Quota: Rule Properties > *Is Quota Enabled*; quota counts from the Temporary order and is **not refunded** on cancel/return after split (KE-08).
- Knox: submit in the path from the brief; an approval that expired before go-live is re-submitted from the same codes. Same v0.2 order as MER-PRM-01 (QA in preview first, Knox after).

## Known errors
Two tiers apply together - discount at a cart just below the threshold (wrong basis) - cashback without the bank (mirror missing the payment condition) - bank option not shown at checkout (payment mode not enabled, TEC-SIT-05) - accessories push the cart over threshold - approved promo not live (Knox expired / publish job) - BMSM tier kept after an item is removed - quota used up too early.

## QA checklist
Cart (not product) mechanic; tier table version and code per tier; thresholds and values per boundary; best tier only; cap; payment condition enforced; exclusions; channel mirrors incl. O2O tiers; stacking with product offers; dates; message; live check per tier.

## Samsung KB to read first
KB Promotion Rule Knox Approval (2477949466) - KB [VN] Promo setup for Payment with promotion scenario (2477655834) - BIN code bulk upload (2477262160) - KB [VN] Promo setup for BMSM (2477327751) - KB Promotion Rule Conditions (2477556982).

## MER-PRM-09 - Multi-promotion batch (more than 2 promotions)

> Tier 1 #28 | Optional | Sprint 4 | Owner: Thành | QA: Xuan, Nga | ~23 tickets/month | M3 Promotion & Offer

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728859  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
A **campaign batch of more than 2 promotions** (monthly pack, later version, split, mega/flash sale, launch set) is built, approved and live together, and the combinations behave as the stacking matrix says. One wrong line or one untested combination gives a double discount across the range.

## Key facts
| Item | Detail |
|---|---|
| Volume | 216 tickets in 2026, ~23/month, 6 markets (**TH 196 of 216**). Senior role - needs MER-PRM-01, PRM-03 and CPN-02 first |
| Roles | Senior batch owner (register, line assignment, stacking design, Knox grouping); line Doers per mechanic; Checker: QA team on every line and the baskets (QAS-PRM-02); Approver: Shift Leader before Knox; Sub-Lead signs the register for V4 (mega/flash) and V5 (launch set) |
| SLA | Low 24h / 2h initial. **Count rule: only lines to build, change or end count**; 1 or 2 counted lines go to the mechanic service (Medium 16h) |
| Change class | Standard per line; no PC (large code batches = Tech COEC + PC). Waiting for Knox does not pause the clock - submit Knox at **T-3 working days** |
| Biggest risk | Double discounts: a missing exclusion, an untested combination, or an old value rebuilt over a newer one |

## Recognise the ticket
Titles: *[TSE] Promotion D2C Aug 26 V4, Split 2 - [TSE] CE August 2026 promotion, New product promotion*. A promotion workbook with one row per promotion and many "continue, already set" rows, resent as V1, V2... or split n. **Not this service:** 1-2 counted lines -> the mechanic service - codes -> CPN-01/02 - prices -> PRC-01..03 - offer pages -> AEM-02 - clean-up -> HSK-01 - live double discount -> MER-INC-01.

Variants: **V1 monthly pack** and **V2 version update** (~52%) - V3 split ticket (~27%) - V5 launch set - V4 mega/flash sale - V6 batch enable/disable/end (e.g. re-enable rules so returns can be processed, with TEC-ORD-03).

## Workflow (key points)
- **One batch register per batch key** (e.g. TH-D2C-2026-09), shared by all versions and splits: Line ID, source row, action (New/Change/End/Continue), mechanic + service, scope, benefit, period, rule code, stacking, Knox ref, Doer/Checker, status.
- **Version control**: diff V(n) against V(n-1) row by row (New / Changed / Ended / Unchanged), **build only New, Changed and Ended** - never rebuild unchanged rules from the new file (KE-02). A changed line already live uses the mechanic's change variant, Knox again, and re-runs its baskets.
- **Stacking matrix**: rows/columns = batch lines + live promotions on the same SKUs; each cell Combine / Exclusive / Best of / No shared SKU (Exclusive = same exclusive rule group, priority decides; "Best of" has no verified native setting). **Mandatory baskets**: overlap per SKU group, one per code, one maximum-discount basket on the highest-value SKU (price floor).
- Bulk tools: export a sample rule -> fill columns -> import (check the cronjob result); `PROMOTION_ATTRIBUTE_BULK_UPLOAD` for priority/quota/dates (UTC)/Business PIC (test with a 2-row file first). **Bulk publish**: path by highest discount, every Business PIC must approve, one rejection rejects all; never mix discount and non-discount rules; never leave two versions of a rule KNOXAPPROVED (both become INACTIVE). Rule limit 15 KB.
- Publish per wave; PENDING LAUNCH between waves; wave checks on the live storefront. Start/end are set in the rule itself, **not through a campaign** (bypasses Knox: disciplinary). Last month's overlapping rules become End lines.

## Known errors
Code meant to exclude a discount still triggers it (exclusion missing) - later change reverted (unchanged line rebuilt) - part of batch not live at go-live (Knox pending) - return orders fail (promotions unpublished -> V6) - splits pass alone but fail combined (no cross-split test) - last month's rule overlaps (End line missing).

## QA checklist
Register complete; version diff logged and unchanged rules untouched; each line matches its file row; sites/targeted EPP sites; periods; matrix complete; overlap and code baskets pass; max-discount basket above floor; Knox approved per line; ended lines no longer apply; linked non-promotion lines done.

## Samsung KB to read first
KB Promotion Rule Knox Approval (2477949466) - 0. Bulk Upload Promotion Rules (2478081250) - [AU] End-date Update in Bulk Upload (2477360814) - Common Promotion Setup pages (VN, SG, SEAU). There is **no TH market page with content**.

