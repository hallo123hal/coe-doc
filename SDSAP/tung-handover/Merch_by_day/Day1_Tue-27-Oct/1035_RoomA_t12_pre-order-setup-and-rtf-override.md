# Day1 - Tue-27-Oct 10:35 Room A - Topic 12 Pre-order setup and RTF Override

> Merch services in this session: MER-STK-02, MER-STK-03 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 13 | MER-STK-02 | Sell-in-advance virtual stock setup | Must | Sprint 3 | Trang | 80 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483598407 |
| 17 | MER-STK-03 | Pre-order stock setup | Must | Sprint 3 | Ayu | 44 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696664 |

## Session: Topic 12 - Pre-order setup and RTF Override

| Field | Value |
|---|---|
| Inventory topic | #12 - Pre-order setup and RTF Override |
| Call (BiPlus plan v3) | Tue 27 Oct 10:35, Room A |
| SDSAP date / status | 27-Oct |
| Component / area | Product / Service |
| SDSAP PIC | Saidatul Humairah Binti Abdul Razak |
| Samsung Confluence link | ID RTF Override |
| Maps to (BiPlus) | MER-STK-03 Pre-order; MER-STK-02 Sell-in-advance virtual stock setup |
| Priority | Tier 1, Sprint 3, Must |
| Verdict | **Clarify** |
| BiPlus PIC for the topic | Thuy Trang |

**Why this verdict:** The linked page is for ID only.

**Questions for SDSAP (from the sheet):** Cover pre-order setup for all markets; what RTF override means and when it is used.

## MER-STK-02 - Sell-in-advance virtual stock setup

> Tier 1 #13 | Must | Sprint 3 | Owner: Trang | QA: Xuan, Nga | ~80 tickets/month | M1 SKU & Catalog

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483598407  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
SKUs can be sold **before physical stock reaches the eStore warehouse**: a virtual quantity is set on the market's virtual warehouse, never above the quantity the subsidiary commits in writing. A wrong quantity oversells (orders that cannot ship) or leaves a launch SKU out of stock.

## Key facts
| Item | Detail |
|---|---|
| Volume | 745 tickets in 2026, ~80/month, 7 markets (MY ~70%, dedicated MY pod) |
| Roles | Doer: Merch operator. Checker: QA team, 100% **before selling starts**. Approver: the subsidiary's written commitment; Shift Leader in PRD SETUP; Sub-Lead for 500 units or more |
| SLA | Low: 24h, 2h initial; internal 15h36 / 78 min. High 4h via MER-INC-01 only for V4 (held order, loss >10,000 USD) |
| Change class | Standard, no PC. A block flag set TRUE on an MX SKU needs RHQ D2C Platform approval (ON HOLD RHQ). ImpEx/Groovy on production is Tech + PC |
| Biggest risk | Quantity above the commitment: orders that cannot be fulfilled |

## Recognise the ticket
Titles: *dummy, SKU Dummy Setup (& Activate), virtual stock, release dummy, increase dummy qty*. A SKU file with a quantity per SKU, start date-time, expected arrival week, often a long fixed MY site list; usually mixed with activate / archive / shipment-notice lines -> split into one line per action. **Not this service:** hand back to NERP stock ("release dummy" after stock arrived) -> MER-STK-01 V2 - pre-order window / overselling weeks -> MER-STK-03 - activate/archive -> MER-PRD-01 - shipment message -> MER-DLV-02 - one-site exclusion -> MER-MST-02 - reserved stock clean-up -> TEC-MON-02.

Variants: **V1 new virtual stock** (most common, "Dummy Setup", "Set virtual stock SKUs") - V2 change quantity ("set to" vs "change by"!) - V3 stock import override (ID and PH CE SKUs only) - V4 urgent virtual stock to release held orders (mostly PH) - V5 backorder set-up (mostly VN) - V6 remove virtual stock.

## Rules to remember
- **Never without a written commitment**; quantity must be within it. 500 units or more = PS-14 sanity hold (ask expected quantity); dates in the past / >90 days / no time zone = PS-10 hold.
- **Never combine virtual stock and overselling on the same SKU** (virtual stock disables overselling; KE-09).
- Set `Available Amount` on the row `VirtualWarehouse-<cc>` (Base Commerce > Stock Level, or *Stock Level File Upload*). Stock Level has no catalog version - it is live at once.
- Block flags on MX SKUs stay FALSE (RHQ GSCM guideline); ask the Shift Leader before setting any flag TRUE. Staging shows the old "block on every set-up" practice and the hard-freeze list still names "Block Stock Import" - conflict kept on the KT list.
- If the SKU shows sold out although available > 0, check **reserved quantity** on the virtual warehouse - Merch never clears it: COEC for TEC-MON-02.
- Record the handback: Jira due date = expected arrival week and the owner in a "Go-live schedule" comment; a MER-STK-01 V2 ticket is raised at that date.

## Known errors
Still out of stock after set-up (wrong warehouse / not approved / not synced / reserved) - quantity back to NERP value next day - double quantity after top-up - stock on an unwanted channel (shared warehouse) - marketplace refuses virtual stock - orders exceed commitment (no handback) - next-day delivery shown with no stock.

## QA checklist (QCL-STK-01)
[Blocking] quantity equals brief and commitment present; [Blocking] start/end of the period and switch-back date in two time zones; "set to"/"change by" resolved; before export; flags FALSE (or RHQ reference); available on the right warehouse; reserved noted; PDP sellable and a quantity above stock refused; handback due date and owner recorded.

## Samsung KB to read first
Product Stock (2477262087) - Overselling Common Mistake (2477851857) - Pre-order/Pre-order Overselling RTF Interface (2477556495) - KB [VN] Overselling (Backorder) feature (2477982894).

## Open points the pack marks "confirm in KT"
Which warehouse the sites read (associatedVirtualWarehouse is empty on staging) - meaning of `releaseDate` - the ID "RTF override" request has no variant in this pack (ask the Shift Leader) - block-flag conflict above.

## MER-STK-03 - Pre-order stock setup

> Tier 1 #17 | Must | Sprint 3 | Owner: Ayu | QA: Xuan, Nga | ~44 tickets/month | M1 SKU & Catalog

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696664  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
SKUs are open for **pre-order** on the requested sites for an exact window, with the delivery date (RDD) shown on the storefront and a **maximum pre-order quantity per warehouse**. Orders stop at the committed quantity. A wrong quantity, date or time zone oversells a launch, promises the wrong delivery date or closes pre-orders early.

## Key facts
| Item | Detail |
|---|---|
| Volume | 410 tickets in 2026, ~44/month, 8 markets (TH ~72%); peaks in March, July, August |
| Roles | Doer: Merch operator (dedicated TH pod for daily batches). Checker: QA team before the window opens and after each quantity/date change. Approver: subsidiary commitment (GSCM quantity where GSCM drives the pre-order); Shift Leader in PRD SETUP; Sub-Lead for 500 units or more |
| SLA | Low 24h / 2h initial. High 4h via MER-INC-01 if a live window oversells or closes during a launch |
| Change class | Standard, no PC. Tech work (save errors, purchase limits, GSCM jobs) = COEC + PC |
| Biggest risk | Wrong window, time zone or maximum: oversold launch or early close |

## Recognise the ticket
Titles: *pre-order, set pre-order, To set pre-order AV*. A week-based SKU table with window (start/end), delivery date (RDD), often four week numbers and a maximum per warehouse; TH sends it daily with activate/deactivate lines. **Not this service:** virtual stock, backorder -> MER-STK-02 - hand back to NERP stock -> MER-STK-01 V2 - activate -> MER-PRD-01 - shipping text -> MER-DLV-02 - badge -> MER-TXT-03 - cart purchase limit -> TEC-SIT-07 - GSCM interface failure -> TEC-TSP-06.

Variants: **V1 open a pre-order window** (~52% for the top 5 titles) - V2 change maximum ("add N" vs "set to") - V3 change RDD / dates / weeks - V4 end pre-order and move to normal sale - V5 GSCM-fed flagship pre-order (mostly TH) - V6 remove SKUs from pre-order.

## Rules to remember
- Convert every date-time to market time and write the zone on the ticket (requests mix local, SGT, GMT, KST; exports may show UTC) - KE-03.
- Weeks are `YYYYWW`; **overselling start week = initial end week + 1**, no overlap (KE-01).
- Settings live in Staged: Catalog > Products > SKU > tab *Pre-order Settings* (date range, delivery date, weeks; site-level overrides exist) -> **Synchronize to Online** -> set `Max PreOrder` on each serving warehouse in Stock Level (the system counts `Pre Order`; never type it).
- **GSCM-driven SKUs** (flagship MX): never force above the GSCM limit - "initial pre-order max limit" error -> set to the limit and report the rest (V5); GSCM dates are changed by the subsidiary in GSCM, not in Hybris.
- **Never run Super Sync STOCK on a pre-order SKU** (past NZ error). Block Stock Import is not needed for pre-order.
- Record the end date-time (two zones) and the next action (MER-STK-01 V2, MER-STK-02 V5 or stop) in the "Go-live schedule" comment.

## Known errors
Weeks cannot be saved (overlap) - maximum refused (GSCM) - window opens/closes hours off (zone) - SKU not available (attributes missing in one catalog / Online not synced / maximum not on serving warehouse) - cart refuses (purchase limit, TEC-SIT-07) - new RDD in Hybris but old date on BC page (AEM copy) - CTA still "pre-order" after end - manual maximum overwritten (auto copy TRUE).

## QA checklist (QCL-STK-01)
[Blocking] quantity equals brief and commitment; [Blocking] window and switch-back date in two zones; before export; date range and delivery date equal the file in every catalog version; weeks consistent; flags FALSE; maximum on each serving warehouse and within GSCM limit; PDP CTA / RDD correct per site type; quantity above maximum refused; linked lines handled; end date and next action recorded.

## Samsung KB to read first
Product Stock (2477262087) - Pre-order/Pre-order Overselling RTF Interface (2477556495) - 0. KB Product Status (CTA) (2477524107) - SEAU: Pre-Order (2477949916). The main setup guide and the RDD page have **no readable text** in the copy.

