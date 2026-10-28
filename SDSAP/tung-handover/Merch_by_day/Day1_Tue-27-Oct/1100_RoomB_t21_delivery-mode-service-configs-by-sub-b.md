# Day1 - Tue-27-Oct 11:00 Room B - Topic 21 Delivery mode/service configs by sub by site by product

> Merch services in this session: MER-DLV-01 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 32 | MER-DLV-01 | Product delivery mode and service setup | Optional | Sprint 4 | Ayu | 20 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696374 |

## Session: Topic 21 - Delivery mode/service configs by sub by site by product

| Field | Value |
|---|---|
| Inventory topic | #21 - Delivery mode/service configs by sub by site by product |
| Call (BiPlus plan v3) | Tue 27 Oct 11:00, Room B |
| SDSAP date / status | 27-Oct |
| Component / area | Fulfillment / Service |
| SDSAP PIC | Mohammad Ashhar Mushtaq |
| Samsung Confluence link | No link |
| Maps to (BiPlus) | MER-DLV-01 Product delivery mode and service setup (product level); TEC-CFG-02 Payment mode and delivery mode configuration, TEC-SIT-05 Website payment and delivery mode configuration (site level) |
| Priority | Tier 1 (MER-DLV-01 Product delivery mode and service setup), Sprint 4, Optional |
| Verdict | **Add** |
| BiPlus PIC for the topic | Thuy Trang |

**Why this verdict:** No page; product level is Merchandising, site level is Tech.

**Questions for SDSAP (from the sheet):** Share the delivery mode and service setup by subsidiary, site and product, and who does which part.

## MER-DLV-01 - Product delivery mode and service setup

> Tier 1 #32 | Optional | Sprint 4 | Owner: Ayu | QA: Xuan, Nga | ~20 tickets/month | M5 Banner & Site content

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696374  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
The right **delivery modes** (standard, express, small/large item, marketplace, store pick-up) and **delivery services** (installation) are set on the listed SKUs in each catalog, one by one or in bulk, plus fee promotions when free or discounted delivery is requested. A wrong set-up blocks checkout, charges the wrong fee, shows installation twice in the cart or promises a service logistics cannot deliver.

## Key facts
| Item | Detail |
|---|---|
| Volume | 192 tickets in 2026, ~20/month, 8 markets (TH 69, PH 22, AU 22, NZ 20) |
| Roles | Doer: Merch operator (V4 certified on MER-PRM-01; TH/VN tickets to the language pods). Checker: peer; QA team samples 20% per week per cluster (min 3), V4 always. Approver: Knox approver (V4 only) |
| SLA | Low 24h / 2h initial. V4 single promotion: Medium 16h (confirm with RHQ). High 4h via MER-INC-01 (live SKU cannot be checked out / wrong fee) |
| Change class | Standard (V1, V2, V3, V5); V4 fee promotion = standard with Knox, QA 100%. Normal + Sub-Lead for re-mapping a whole category. Tech parts (new mode, fee, site-level mode, ImpEx/Groovy) = COEC + PC |
| Biggest risk | A SKU on sale with **no deliverable mode**, or a free fee that is too wide |

## Recognise the ticket
Titles: *delivery mode, set up delivery, installation, free delivery, pick-up, BOPIS*; the most repeated: "**Create SKU & Set Up Delivery Mode... Live date**" (12%). A file DLV-01-SKU (SKU, catalog, codes to add, codes to remove, service code; for 3PD also the marketplace mode and storage location). **Not this service:** new delivery mode / cost / base fee -> TEC-CFG-02 - mode missing on a site -> TEC-SIT-05 - postcode coverage -> MER-DLV-03 - shipping messages -> MER-DLV-02 - SKU creation/activation -> MER-PRD-01 - installation Z-code -> MER-PRD-04 - fee banners -> MER-AEM-04 - stock sync -> MER-STK-01.

Variants: **V2 delivery set-up for new SKUs** (incl. 3PD marketplace mode, ~12%) - V1 assign/change/remove modes on existing SKUs - V3 delivery service (installation) set-up - V4 delivery/installation fee promotion - V5 store pick-up (BOPIS) for a period.

## Workflow (key points)
- First confirm the requested modes **exist and are active on the site** (Base Store > Delivery Modes; CMSSite.deliveryModes). If not, it is Tech work: COEC for TEC-SIT-05 (TEC-CFG-02 for a new mode) and the Merch ticket goes to ON HOLD COE.
- Export the before state (Staged and Online), then edit **Product > Administration > Delivery Modes** in Staged (or Bulk Edit > "Append to existing"; whether it supports removal is a KT point; there is no delivery-mode bulk upload template). Repeat per catalog (B2C, EPP, SMB, EA, 3PD are separate) and **synchronise Staged -> Online**; verify with Q3 that Online equals Staged.
- 3PD: use the marketplace mode (e.g. `th-marketplace-delivery-standard`) and check its ERP values (Erp delivery mode, Shipping Condition, S Proc Ind) under Price Settings > Delivery Costs > GERP Data. A 3PD site uses only 3PD modes. A new-SKU ticket is **one chain**: PRD-01 -> delivery -> storage location (STK-01) -> activation.
- V3: installation is modelled three ways (delivery service on the product, installation delivery modes, NERP delivery SKU mapping); flags such as `allowMultipleDeliveryService` are **Tech config - read only**. V4: template `2025_free_deliveryMode`, rule created in the site's own promotion group (Q8), simulator, QA 100%, Knox. V5: removal sub-task and PENDING LAUNCH until the end date.
- **Never remove the last deliverable mode** from a SKU on sale. Test checkout (not only PDP) with a postcode inside PINMAP coverage.

## Known errors
No delivery option at checkout (modes do not intersect site modes / postcode outside PINMAP) - installation twice in cart - visible in Backoffice but not on site (not synced) - delivery promotion not applied for business buyers - promotion not live after Knox (job) - file includes an unintended catalog - cannot start because the SKU does not exist - rule created in the wrong promotion group.

## QA checklist
Scope matches request; modes exist and active on each site; before export; added/removed codes correct; no SKU without a deliverable mode; all catalogs covered; Online = Staged; checkout options and fees correct; service appears once; rule name/period/group/Knox (V4); end action recorded (V4, V5).

## Samsung KB to read first
Delivery mode documentations and important key setup/configs (2477687721) + the *Fundamental SKU setup* page of your market (TH, VN, PH). Others by case: Add-on Installation via Delivery Service (2477884461), 3PD Shopee/Logicbroker delivery pages.

