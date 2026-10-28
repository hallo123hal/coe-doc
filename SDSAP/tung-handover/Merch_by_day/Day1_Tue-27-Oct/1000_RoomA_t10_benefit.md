# Day1 - Tue-27-Oct 10:00 Room A - Topic 10 Benefit

> Merch services in this session: MER-TXT-02 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 24 | MER-TXT-02 | Benefits setup | Optional | Sprint 4 | Trang | 39 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696930 |

## Session: Topic 10 - Benefit

| Field | Value |
|---|---|
| Inventory topic | #10 - Benefit |
| Call (BiPlus plan v3) | Tue 27 Oct 10:00, Room A |
| SDSAP date / status | 27-Oct |
| Component / area | Product / Service |
| SDSAP PIC | Ong Hee Hui |
| Samsung Confluence link | KB - Benefits V4.0 |
| Maps to (BiPlus) | MER-TXT-02 Benefits; MER-BYP-02 Offers (benefits) configuration on buying page |
| Priority | Tier 1, Sprint 4, Optional |
| Verdict | **Reuse** |
| BiPlus PIC for the topic | Thanh |

**Why this verdict:** KB Benefits V4.0 matches benefits setup.

**Questions for SDSAP (from the sheet):** Is V4.0 used by all markets?

## MER-TXT-02 - Benefits setup

> Tier 1 #24 | Optional | Sprint 4 | Owner: Trang | QA: Xuan, Nga | ~39 tickets/month | M3 Promotion & Offer

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696930  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
Benefit entries (free gift, bundle, cashback, payment, instalment, warranty or service offers) are created, amended, extended or removed on the right SKUs and sites, so the **PD page, the Buying Configurator (BC) page and the cart** show exactly the approved offer from go-live to end. A wrong, missing or expired benefit misleads customers and creates claims.

## Key facts
| Item | Detail |
|---|---|
| Volume | 359 tickets in 2026, ~39/month, 8 markets (NZ 115, ID 84, PH 45, TH 34, VN 32) |
| Roles | Doer: Merch operator (NZ pod early shift). Checker: second certified operator (peer check of the file before upload); QA team on request or sample (QAS-MER-01). Approver: Shift Leader (R1); Sub-Lead for launch packages and multi-group EPP |
| SLA | Low 24h / 2h initial; internal 15h36 / 78 min. High 4h via MER-INC-01 (wrong benefit live, loss >10,000 USD or legal exposure) |
| Change class | Standard request, risk tier R1; **no Knox, no PC**. Tech work (upload failure, AEM sync, rendering) = linked COEC |
| Biggest risk | A value benefit (gift, discount, cashback) live **without its mechanic**, or still showing after the campaign ends |

## Recognise the ticket
Titles: *[EXTEND BENEFIT], [UPDATE BENEFIT DESCRIPTION], HA Benefit on cart and PDP, get free, bundle*. The benefit is a **message**; the mechanic (gift, discount, bundle) is delivered elsewhere and must be linked. **Not this service:** the mechanic -> MER-PRM-01..08, PRF-04/05, PRD-04/05, CPN-01 - buying-page box layout/order/disclaimers -> MER-BYP-02 (rule: a change to the benefit *record* is this service) - gift selection page -> MER-BYP-03 - text and flags -> MER-TXT-03/01 - offer page + T&C -> MER-AEM-02 - EPP 2.0 Local Benefits / tiles -> MER-AEM-04 - Shop App -> MER-SAC-01.

Variants: **V1 new campaign benefits** and **V4 extend/shorten period** (most common; ID refrigerator bundles) - V3 amend benefit - V5 remove/take out (NZ weekly) - V2 launch benefits for new models - V6 benefit codes for bundles and gifts.

## Rules to remember
- Upload with Product Cockpit > Bulk Upload > `PRODUCT_BENEFITS` (job `tokoProductBenefitsBulkUploadJob`); check job result **SUCCESS** (staging: 55 ERROR of 75 runs since June). Verify rows in Backoffice > Benefit > ProductBenefit by code.
- **Page type matters**: PD benefit = field Title, no HTML, one line, <=62 chars (53 with CTA), only the 2 highest-priority benefits show; BC benefit = Description, approved icons only (112x112), offer text <=127, localizedTitle <=58, flag <=26. Many launch models and EPP2.0 use BC - a PD brief does not display as briefed there (KE-02).
- **`site` is never blank and has no spaces** (blank = every country of the cluster, KE-11). Dates in UTC `YYYY/MM/DD HH:MM:SS`. `productsAction = APPEND` so other requesters' benefits are not overwritten (KE-06).
- Never touch benefits labelled `DO_NOT_DELETE` (RHQ-owned). Since 25 Jun 2026 BC benefits come from Hybris (AEM "Offers" on BC discontinued).
- Request AEM sync through Tech at least 1 hour before go-live for launches; verify within 30 min of go-live on PD, BC and cart.

## Known errors
Not showing after upload (future start / job ERROR / AEM sync / cache - check in that order) - looks different from brief (PD vs BC) - duplicates on EPP sites - still showing after campaign (no end date, mechanic extended alone) - missing on some EPP sites - popup not shown (isNewDescription) - broken Thai/Vietnamese characters (use UTF-8).

## QA checklist
Action lines cover the brief; mechanic linked; before export; copy equals brief within limits; page type correct per model; dates in UTC = market time; site never blank and group complete; job SUCCESS and rows = file; AEM sync confirmed; PD/BC/cart show benefits; T&C link works; no `DO_NOT_DELETE` touched.

## Samsung KB to read first
KB Benefits V4.0 (2477327393) - 5. PDP PAGE BENEFIT (2477556650) - 6. CART BENEFIT (2477360334) - 1-4. BC benefit pages (NO CTA / HYPERLINK / POPUP) - KB Search Restriction - Frontend Benefit (2477950654).

