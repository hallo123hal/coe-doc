# Day1 - Tue-27-Oct 10:25 Room A - Topic 13 Category Structure

> Merch services in this session: MER-PRD-01 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 1 | MER-PRD-01 | Samsung SKU setup and update | Must | Sprint 1 | Trang | 246 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483695947 |

## Session: Topic 13 - Category Structure

| Field | Value |
|---|---|
| Inventory topic | #13 - Category Structure |
| Call (BiPlus plan v3) | Tue 27 Oct 10:25, Room A |
| SDSAP date / status | 27-Oct |
| Component / area | Product / Service |
| SDSAP PIC | Ong Hee Hui |
| Samsung Confluence link | Category Structure |
| Maps to (BiPlus) | MER-PRD-01 Samsung SKU setup and update (category) |
| Priority | Tier 1, Sprint 1 |
| Verdict | **Reuse** |
| BiPlus PIC for the topic | Thuy Trang |

**Why this verdict:** Category structure supports SKU setup.

**Questions for SDSAP (from the sheet):** Where are the category trees per market kept; who approves a new category?

## MER-PRD-01 - Samsung SKU setup and update

> Tier 1 #1 | Must | Sprint 1 | Owner: Trang | QA: Xuan, Nga | ~246 tickets/month | M1 SKU & Catalog

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483695947  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
Samsung SKUs are registered in Hybris with complete attributes and the **exact requested status on each catalog at go-live**. A wrong status sells a discontinued SKU, breaks a launch embargo, hides a selling product or blocks marketplace orders.

## Key facts
| Item | Detail |
|---|---|
| Volume | 2,303 tickets in 2026, ~246/month, 8 markets (VN, MY, PH, TH high volume). The biggest Merch service |
| Roles | Doer: Merch operator (V1 needs registration certification). Checker: second certified operator; QA team for flagships and a weekly 20% sample. Approver: Shift Leader |
| SLA | Low: 24h resolution, 2h initial; internal 15h36 / 78 min. High 4h only via MER-INC-01 |
| Change class | Standard, no PC ticket. Normal + Sub-Lead review for: whole-category archive, >200 SKU-catalog lines (confirm in KT), base product / product type change on a live SKU |
| Biggest risk | Wrong status on a catalog: selling SKU archived, discontinued SKU sold, embargo broken |

## Recognise the ticket
Titles: *activate, deactivate, active/archive, archive, set product*. A file with one row per SKU and an action per catalog or site (often >10 site IDs). **Not this service:** pre-order lines -> MER-STK-03; stock lines -> MER-STK-01/02; hide on one site only -> MER-MST-02; price -> MER-PRC-01/02; delivery text -> MER-DLV-02; custom SKU, SC+, Z/F-code -> MER-PRD-02..05; Super Sync job failure -> TEC-TSP-06.

Variants: **V4 recurring status file** (most common, TH/VN/PH ~37%) - V3 deactivate/archive/hide (~11%) - V1 new SKU registration (~12%) - V2 activate - V5 embargo hold and scheduled activation - V6 attribute update - V7 3PD catalog enablement - V8 status extract.

## Rules to remember
- Edit the **child catalog in version Staged**, then synchronise to Online. The Jira status STG SETUP is *not* the staging system - the work is on production Backoffice.
- A status set in a shared catalog applies to all its sites; one-site exclusion is MER-MST-02. Map each site to its catalog (query V-PRD01-04) and apply to **every** catalog serving the site (KE-05).
- Meaning of "deactivate" varies: PH = approval *check* + sales status ARCHIVED; activate = approved + PURCHASABLE. Ambiguous words ("remove", "takeout") -> one clarification, never guess.
- Split mixed files by remark: pre-order -> STK-03, stock -> STK-01/02, delivery text -> DLV-02.

## Workflow (V1 new SKU, key steps)
1. Readiness: NERP material with RRP, AEM PDP live or dated. 2. Check existing records / base code. 3. `PRODUCT` bulk upload to the master catalog (Product Cockpit > Bulk Upload). 4. Bulk-approve base product, then variants. 5. Super Sync (DOTCOM, PRICE, STOCK, IMAGE) via *Products Sync Selector*. 6. Master attributes: Identifier, product type NORMAL, unit, required additional info IMEI / SERIALNO. 7. External service types, warehouse mapping, delivery modes (MER-DLV-01). 8. Synchronize master -> child Staged; set initial status per child (usually ARCHIVED until go-live). 9. Compare RRP with the brief (never override). 10. Sync Staged -> Online at go-live; storefront check.
AEM auto-creation is on for MY, SG, TH, TW, VN (the operator completes category, service types, delivery, status) and off for HK, ID, NZ, PH (manual upload).

## Known errors
AEM sync "no result" (model not published) - RRP missing/different - plant/storage location not populated - activated but not purchasable - still visible after hide (one catalog only) - base code already used - marketplace orders stuck (SKU inactive in 3PD catalog) - bulk edit skips SKUs (spaces in codes) - checkout fails on a new phone (IMEI/SERIALNO missing on the base product).

## QA checklist
Every line has a result and routed lines are linked; before export; approval + sales status per catalog; row counts equal; base/category/required info (V1); Super Sync results and failures explained; RRP equals brief; storefront sample per catalog type; embargo SKUs unapproved until go-live.

## Samsung KB to read first
Product Active/Archive (2477360434) - Product Catalog & product setup (2477261954) - Auto SKU creation on Hybris from AEM (2477524142) - Product Setup (no auto creation) (2477720611) - the *Fundamental SKU setup* page of your market.

## Open points the pack marks "confirm in KT"
Same-day cut-off for recurring files - AEM model check API key - whether Merch operators have HAC access - embargo state (PURCHASABLE_NOT_VISIBLE vs ARCHIVED) per market - target choice inside the Synchronize dialog.

