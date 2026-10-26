# MER-PRF-04 - Must purchase with (freebie) reference setup

> Day 3 - Thu-29-Oct | Owner: **Tùng** | QA: Xuan, Nga | Tier 1 #27 | Optional | Sprint 4 | ~33 tickets/month | Module: M3 Promotion & Offer

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483598148  
*Summary of the Service Pack page (condensed v0.2, revised 25 Oct 2026). Always re-read the page itself before the session - this is a study aid, not a replacement.*

## Session (SDSAP handover)
| Field | Value |
|---|---|
| Inventory topic | #8 - Z-code, F-code Setup |
| Call (BiPlus plan v3) | Dated 26-Oct; follow-up on Thu 29 Oct 14:15, Room A |
| SDSAP date / status | 26-Oct |
| Component / area | Product / Service |
| SDSAP PIC | CHONG HAW EONG |
| Samsung Confluence link | KB - SEAO Z-code Setup Standardisation |
| Maps to (BiPlus) | MER-PRD-04 Z-Code, MER-PRD-05 F-Code; MER-PRF-04 Must purchase with (freebie) reference setup (freebie) |
| Priority | Tier 2; MER-PRF-04 Must purchase with (freebie) reference setup Tier 1 Optional |
| Verdict | **Clarify** |
| BiPlus PIC for the topic | Thuy Trang |

**Why this verdict:** The page covers Z-code standardisation; F-code (bundles) is not visible.

**Questions for SDSAP (from the sheet):** Which page covers F-code bundles (virtual and hard bundle)?

## What to focus on in this session

- Follow-up of the 26-Oct topics 6-8 (Thu 29 Oct 14:15, Room A). Topic 8 is Tùng's: Z-code / F-code setup, which feeds the freebie (MER-PRF-04 maps via *Z-code gift*; Z-Code creation itself is MER-PRD-04, F-Code MER-PRD-05).
- Verdict Clarify: the KB page covers Z-code standardisation only. Ask which page covers **F-code bundles** (virtual and hard bundle).
- Check gift readiness rules end to end: Z-Code sales/approval status (PURCHASABLE_NOT_VISIBLE / Approved), price 0 at checkout, stock source (NERP or virtual stock), and the 'must purchase with' reference.

## What the service does
The requester gets a **free gift added to the cart automatically at zero price**, only when a qualifying main product is bought, on the requested sites and for an exact period. The gift is a **free-gift promotion rule**. A "must purchase with" reference (MUST_PURCHASE_WITH) is used *only* for a mandatory companion (e.g. indoor + outdoor air-conditioner units). A wrong rule gives stock away, misses a promised gift, or gives it with the wrong product, quantity or site.

## Key facts
| Item | Detail |
|---|---|
| Priority / sprint | Optional, Sprint 4 (Tier 1 #27) |
| Volume | 311 tickets in 2026, ~33/month (MY 94, ID 88, TH 38, VN 36) |
| Roles | Doer: Merch operator certified on promotions (MER-PRM-01). Checker: QA team - round 1 on the simulator, round 2 live at each go-live wave. Approver: subsidiary at REVIEW SETUP; Knox only where Hybris triggers it |
| SLA | **Medium** for one gift promotion: 16h resolution, 2h initial (internal 10h24 / 78 min, confirm with RHQ). Low 24h for reference-only work (V6) and for more than 2 promotions (MER-PRM-09). High 4h via MER-INC-01 |
| Change class | Standard, no PC ticket. Sub-Lead review for an always-on gift on all sites, or gift landed cost >=100 USD (PS-07). Tech changes on production = Normal under a PC ticket |
| Biggest risk | Giving stock away: wrong site, wrong ratio/maximum, gift not ready, or a paid item added automatically |

## Recognise the ticket
Titles: *get free, FOC, free gift, GWP, free installation, [EXTEND PROMOTION], [EXTEND BENEFIT]*. A gift table (main SKU/category, gift SKU, ratio, max per order, sites, period); in ID a master offer file with row references, in MY a campaign template. Same offer returns monthly as an extension.

**Not this service:** Z-Code creation -> MER-PRD-04 (same ticket, before the rule); F-Code components (CONSISTS_OF) -> MER-PRD-05; gift by code -> MER-CPN-02; gift on cart value -> MER-PRM-02; customer chooses gift -> MER-BYP-03; discounted 2nd unit -> MER-PRM-03; combo price -> MER-PRM-04; free SC+ months -> MER-PRM-07; gift text -> MER-TXT-02 / MER-BYP-02; >2 promotions in one ticket -> MER-PRM-09 owns it (you build each gift rule with this runbook); live gift given wrongly -> MER-INC-01.

Variants: V3 extend/shorten/end a gift (most common, ~77 of 311) - V1 new product-triggered gift (base build) - V5 free installation / service item (MY) - V2 priority gift with fallback (ID, VN) - V4 change gift/products/sites - V6 must-purchase-with reference.

## Workflow (V1 - base build)
1. APPROVED-ES -> STG SETUP (work is on production Backoffice; "STG SETUP" is a status, not a staging system). Classify trigger; split mixed tickets.
2. **Gift readiness in every target catalog:** gift exists (Z-Code via MER-PRD-04, or real SKU), approved, can be in cart but not sold alone (Z-Code: `PURCHASABLE_NOT_VISIBLE` / Approved), has a stock source (NERP or committed virtual stock via MER-STK-02); Z-Code price must be 0 at checkout.
3. Sites: list included/excluded site IDs; "all sites" = every site where the main SKU sells incl. SMB and EA unless excluded in writing. Create the rule in the **site's own promotion group**.
4. Export the before state (HAC Q1 by `{website}`; check for an overlapping gift on the same main SKU/site).
5. Build the free-gift rule **UNPUBLISHED** from a template (Marketing > Promotion Templates): `product_buy_x_get_y_free`, `2025_choose_free_gift_based_available_stock`, `..._availability_stockPriority`, `..._with_trigger_rule_msg`, `2025_target_bundle_price_with_free_gift_based_availability`. Set ratio, Maximum Rule Executions, schedule, qualifying products. **Name per convention:** `{CC}_{Site}_{Platform}_{Category}_{Start}_{End}_{Promotion type}_{free text}` - a wrong name is the most frequent strike; one rule per channel/site group; names cannot be changed after the code is set (clone instead).
6. Publish to the **preview module** (`<cc>-preview-promotions-module`), test on the promotion simulator (eligible cart gets gift at 0; ineligible cart/other SKU/below quantity/excluded site/outside period gets none).
7. QA REVIEW (round 1) -> REVIEW SETUP (subsidiary approves; no feedback at go-live = publish on time + template D). Knox only if Hybris shows a Knox status; do not publish a discount rule and a free-gift rule in one bulk.
8. Publish to the live module at go-live (PENDING LAUNCH until start); QA round 2 live per site type at each wave. Record end date + MER-HSK-01 clean-up date.

**V3 extend** (most common): list *every* channel copy (B2C, O2O, EPP groups, SMB, EA) from the original ticket via code prefix; change End Date/Time on all copies in market time; republish; simulator inside the new period and after the end; ask whether the gift text ends too (MER-TXT-02).
**V2:** one rule per channel with the stock-priority template; Stock Check Type CHECK_PROMO_STOCK / CHECK_STOCK_AVAILABILITY / DISABLED. **V6:** Bulk Upload `PRODUCT_REFERENCES` (MUST_PURCHASE_WITH); if the companion cannot be added the main is refused - expected.

## Known errors to remember
Gift not added though rule active (not cart-able, wrong promotion group, excluded site, only in preview module, KE-01) - out-of-stock gift still offered (Stock Check Type, KE-02) - gift on excluded sites ("all sites" read too wide, KE-03) - main refused after reference upload (KE-04) - rule not live at start (KE-07) - wrong rule name (KE-08) - gift shows stock alert/can be bought alone (KE-09) - gift missing on some sites (clone to that group, KE-10) - wrong quantity / two gifts (ratio/max or overlapping copies, KE-11).

## QA checklist
All main SKUs/variants listed; gift code correct, price 0; gift only with listed main (PS-07 exposure); name per convention, website = site promotion group; dates in market time; ratio/max/stacking as briefed; sites included/excluded; not live before approval; published live; live gift line correct per site type at each wave; end date + clean-up recorded; checkout reaches payment step.

## Samsung KB to read first
KB - Product Reference - Bundle and Gift (2477655578) - KB - Promotion Creation (2477688331) - KB - Promotion Rule Knox Approval (2477949466) - KB - Bulk Upload Product Reference (2477949982) - 0. KB - Product Active/Archive (2477360434) - MY promotion-specific scenarios (2477557060, free installation) - SG Z-code shipping/freebie message (2477491606) - SEAU: Promotion (2477852019).

## Open points the pack marks "confirm in KT"
Which template the market standard uses for a plain FOC - rule priority/group per market (VN Package/FOC 600 vs 150/999 on staging) - how a published rule is set to INACTIVE - whether free-gift rules ever go through Knox - PH free gifts raised as BOGO (MER-PRM-03). Practice only with `TRAINING_` rules on staging.

