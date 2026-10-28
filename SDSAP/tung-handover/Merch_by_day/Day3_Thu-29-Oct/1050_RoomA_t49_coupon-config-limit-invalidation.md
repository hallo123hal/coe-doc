# Day3 - Thu-29-Oct 10:50 Room A - Topic 49 Coupon config Limit Invalidation

> Merch services in this session: MER-CPN-01, MER-INC-01 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 6 | MER-CPN-01 | Coupon and voucher creation | Must | Sprint 2 | Thành | 202 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728552 |
| 31 | MER-INC-01 | Live merchandising error correction | Optional | Sprint 4 | Trang | 21 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728742 |

## Session: Topic 49 - Coupon config Limit Invalidation

| Field | Value |
|---|---|
| Inventory topic | #49 - Coupon config Limit Invalidation |
| Call (BiPlus plan v3) | Thu 29 Oct 10:50, Room A |
| SDSAP date / status | 29-Oct |
| Component / area | Config / Service |
| SDSAP PIC | Aldwin John Gavino |
| Samsung Confluence link | No link |
| Maps to (BiPlus) | MER-CPN-01 Coupon and voucher creation, MER-CPN-02 Coupon promotion rule setup and linking; MER-INC-01 Live merchandising error correction |
| Priority | Tier 1, Sprint 2 |
| Verdict | **Add** |
| BiPlus PIC for the topic | Thanh |

**Why this verdict:** No page.

**Questions for SDSAP (from the sheet):** Share the page; when and how limits are invalidated.

## MER-CPN-01 - Coupon and voucher creation

> Tier 1 #6 | Must | Sprint 2 | Owner: Thành | QA: Xuan, Nga | ~202 tickets/month | M2 Voucher & Access code

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728552  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

*Full summary already given earlier in the week (first session: Day3_Thu-29-Oct/1020_RoomA_t47-c6_coupon-single-code-vs-multicode-extern.md); only the definition is repeated here.*

## What the service does
The requester gets a coupon - one public code or a batch of unique codes - that works on the requested sites for the agreed period, with redemption limits that cap the cost. A wrong value, missing cap or wrong stacking gives away margin in minutes; a leaked code or code file is a data security event.

## MER-INC-01 - Live merchandising error correction

> Tier 1 #31 | Optional | Sprint 4 | Owner: Trang | QA: Xuan, Nga | ~21 tickets/month | M7 Errors, checks & BVT

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728742  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

*Full summary already given earlier in the week (first session: Day2_Wed-28-Oct/1430_RoomA_c3_live-merchandising-error-correction-wr.md); only the definition is repeated here.*

## What the service does
Live merchandising data on production (wrong price, promotion, voucher/coupon, stock, or offer content) is **contained fast, corrected, checked by a second person and QA on the live storefront, and handed to incident reporting**. Every hour a wrong price or generous promotion stays live becomes orders Samsung must honour or cancel, so **containment comes before investigation**.

