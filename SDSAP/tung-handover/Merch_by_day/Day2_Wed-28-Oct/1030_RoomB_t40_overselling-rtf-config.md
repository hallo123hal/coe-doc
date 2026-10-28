# Day2 - Wed-28-Oct 10:30 Room B - Topic 40 Overselling RTF - Config

> Merch services in this session: MER-STK-02, MER-STK-03 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 13 | MER-STK-02 | Sell-in-advance virtual stock setup | Must | Sprint 3 | Trang | 80 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483598407 |
| 17 | MER-STK-03 | Pre-order stock setup | Must | Sprint 3 | Ayu | 44 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696664 |

## Session: Topic 40 - Overselling RTF - Config

| Field | Value |
|---|---|
| Inventory topic | #40 - Overselling RTF - Config |
| Call (BiPlus plan v3) | Wed 28 Oct 10:30, Room B |
| SDSAP date / status | 28-Oct |
| Component / area | Config / Service |
| SDSAP PIC | Swalehat Ummus |
| Samsung Confluence link | Pre-order Pre-order Overselling RTF Interface |
| Maps to (BiPlus) | MER-STK-02 Sell-in-advance virtual stock setup, MER-STK-03 Pre-order stock setup |
| Priority | Tier 1, Sprint 3, Must |
| Verdict | **Reuse** |
| BiPlus PIC for the topic | Thuy Trang |

**Why this verdict:** Pre-order overselling RTF interface page.

**Questions for SDSAP (from the sheet):** Which part is Merchandising and which is Tech?

## MER-STK-02 - Sell-in-advance virtual stock setup

> Tier 1 #13 | Must | Sprint 3 | Owner: Trang | QA: Xuan, Nga | ~80 tickets/month | M1 SKU & Catalog

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483598407  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

*Full summary already given earlier in the week (first session: Day1_Tue-27-Oct/1035_RoomA_t12_pre-order-setup-and-rtf-override.md); only the definition is repeated here.*

## What the service does
SKUs can be sold **before physical stock reaches the eStore warehouse**: a virtual quantity is set on the market's virtual warehouse, never above the quantity the subsidiary commits in writing. A wrong quantity oversells (orders that cannot ship) or leaves a launch SKU out of stock.

## MER-STK-03 - Pre-order stock setup

> Tier 1 #17 | Must | Sprint 3 | Owner: Ayu | QA: Xuan, Nga | ~44 tickets/month | M1 SKU & Catalog

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696664  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

*Full summary already given earlier in the week (first session: Day1_Tue-27-Oct/1035_RoomA_t12_pre-order-setup-and-rtf-override.md); only the definition is repeated here.*

## What the service does
SKUs are open for **pre-order** on the requested sites for an exact window, with the delivery date (RDD) shown on the storefront and a **maximum pre-order quantity per warehouse**. Orders stop at the committed quantity. A wrong quantity, date or time zone oversells a launch, promises the wrong delivery date or closes pre-orders early.

