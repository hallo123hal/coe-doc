# Day3 - Thu-29-Oct 10:00 Room A - Topic 43 Price Row

> Merch services in this session: MER-PRC-01 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 8 | MER-PRC-01 | Price upload | Must | Sprint 2 | Tùng | 101 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483631159 |

## Session: Topic 43 - Price Row

| Field | Value |
|---|---|
| Inventory topic | #43 - Price Row |
| Call (BiPlus plan v3) | Thu 29 Oct 10:00, Room A |
| SDSAP date / status | 29-Oct |
| Component / area | Price / Service |
| SDSAP PIC | Ong Hee Hui |
| Samsung Confluence link | No link |
| Maps to (BiPlus) | MER-PRC-01 Price upload |
| Priority | Tier 1, Sprint 2, Must |
| Verdict | **Add** |
| BiPlus PIC for the topic | Thanh |

**Why this verdict:** No page for a daily service.

**Questions for SDSAP (from the sheet):** Share the price upload page, the template and the checks before go-live.

## MER-PRC-01 - Price upload (Tùng's service)

> Tier 1 #8 | Must | Sprint 2 | Owner: Tùng | QA: Xuan, Nga | ~101 tickets/month | M4 Price & Trade-in

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483631159  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

Focused notes for this service: [Day3_Thu-29-Oct/1000_RoomA_MER-PRC-01_price-row.md](../../Day3_Thu-29-Oct/1000_RoomA_MER-PRC-01_price-row.md)

## What the service does
The requester gets new or changed **regular, RRP and always-on (AON) prices** live at an exact date/time in the market time zone, approved in Knox where required, and checked by a second person on PDP, cart and checkout. A missing zero, wrong time zone or a price live before approval sells at a loss within minutes on every site that shares it.

## Key facts
| Item | Detail |
|---|---|
| Priority / sprint | Must, Sprint 2 (Tier 1 #8) |
| Volume | 961 tickets in 2026, ~101/month, 8 markets (most: TH, ID, AU) |
| Roles | Doer: price-certified Merch operator. Checker: QA team (Check A, before Knox). Second person (not the Doer) does Check B at go-live. Approver: Shift Leader, then the Knox approver of the path in the brief |
| SLA | Low: 24h resolution, 2h initial response (APPROVED-ES to STG SETUP); internal 15h36 / 78 min. Waiting for Knox has no status and the clock keeps running: submit Knox within 4 working hours of complete intake |
| Change class | R3. Standard within thresholds, no PC ticket. **Normal** (Sub-Lead review before Knox) when: >100 rows without a diff file, >500 rows, a row trips a sanity rule (PS-02 drop >=20% needs written confirmation; PS-05 discount >=30% is a hold; PS-03 new/old ratio <0.5 or >2; PS-04 price above RRP or zero), RRP change for a whole division, go-live inside a Hybris freeze, first upload of a market, or E4 exposure >=10,000 USD / >=500 SKUs |
| Biggest risk | Wrong price or wrong time zone; price live before Knox approval |

## Recognise the ticket
Shop Merchandising issue in a market project (AUME, NZHME, VNME, THAME, IDME, MYME, SPHME, PME); title words *price upload, update price, RRP, strike, AON, [W22]*; a price file per catalog (one row per SKU, validityFrom in GMT/UTC). **Prices with no end date** = this service; with an end date it is a campaign price (MER-PRC-02).

Variants: V1 regular price list update (most common) - V2 price for new SKUs (RRP first, then regular) - V3 channel/tiered price incl. AON (EPP tiers, VIP, staff, SMB, EA, 3PD) - V4 RRP change / block price / NERP refresh (NZ "Update Price Strike details") - V5 extension or removal - V6 SC+ plan and service-pack price.

## Workflow (V1)
1. APPROVED-ES -> **STG SETUP** (the status change is the initial response). Write the *internal check line* (SKUs, prices, currency, start with time zone, sites, "Matches approved brief vX"). Run price sanity rules PS-01..05.
2. Export the **before state** (Backoffice > Catalog > Products > Prices tab, or HAC FlexibleSearch Q1/Q2). Check the block-price flag (`blockPriceUpdatesFromExternalSystems`).
3. Reconcile the file in the BiPlus sheet (change %, implied discount, UTC validity). Flagged rows go out in **one combined clarification** (ON HOLD SUBS, assignee = subsidiary). Never retype a requester file; never guess a price.
4. Upload per catalog: Product Cockpit > Bulk Upload > `SPECIAL_PRICE` (job `tokoSpecialPriceImportJob`). Prove the records in Price Settings > Prices > PriceInfoChange: all VALID and equal to the file on 100% of rows.
5. **QA REVIEW (Check A)** - no Knox before it passes.
6. **PRD SETUP**: Shift Leader approval, then submit Knox the same working day (max **300 rows per submit**; path from the approval-path column of the brief, never chosen by you). Write Knox reference, time and path in a comment.
7. Cron jobs: `knoxPromotionStatusJob` (hourly :02) -> KNOXAPPROVED; `knoxPriceApplyingJob` (hourly :45) -> COMPLETED and rows in Staged. Still KNOXAPPROVED after two :45 runs -> linked COEC to Tech, ticket to ON HOLD COE.
8. Sync to Online only when Knox approved + records COMPLETED + Check A passed. Approval after validityFrom: stop, get a new go-live in writing; never backdate.
9. **Check B** within 30 min of start (E4: 15) by a second person: PDP price and strike-through, cart line/subtotal, checkout total before payment, price report difference zero. Ticket waits in PENDING LAUNCH.
10. Hand back with template C; only RHQ closes.

### Time zone cheat-sheet (template validity is GMT/UTC)
| Market | Local 00:00 in template (UTC) |
|---|---|
| SG, MY, PH (+8) | 16:00 previous day |
| TH, VN, ID WIB (+7) | 17:00 previous day |
| NZ NZDT (+13) | 11:00 previous day |
| AU AEDT (+11) | 13:00 previous day |

## Known errors to remember
Price starts 7-13h off (local typed as UTC, KE-01) - approved but not live (stuck KNOXAPPROVED, KE-02) - live except one site (site/tier/catalog missing, KE-03) - price returns to old value (block price false, NERP overwrote, KE-06) - after a time-bound price RRP shows instead of AON (KE-07) - unsubmitted records removed by `periodicPriceCleanupCronJob` (daily 23:00, KE-08) - KNOXREJECTED (too deep a discount, KE-09) - no Knox popup (`knox.price.approval.disabled.<store>` true, KE-10) - APE017 (approver on leave, KE-11).

## QA checklist (what the Checker looks at)
Data sufficient; template current; flagged rows confirmed in writing; UTC = local; record export equals file on 100% of rows; no overlap with existing rows; block-price flag correct; Knox <=300 rows and path matches the brief; sync only after approval; price report diff zero; PDP/strike-through, cart, checkout totals.

## Samsung KB to read first
- Special Price Knox Approval (2477982196) and Knox Price Approval (2477916752)
- 0. KB - SEAO Multistore Site Matrix and Price Template (2477622304)
- KB - Product Price (2477949955), KB - Knox Approval Cronjob (Price) (2478080459)
- Market: SEAU: Price (2477622358) for AU

## Open points the pack marks "confirm in KT"
Whether the Special Price template is the right route for RRP/regular rows - whether Merch may run the Knox cronjob by hand - scope of `periodicPriceCleanupCronJob` - product-level sync option - whether a price upload is allowed during a hard freeze (not on the exception list).

