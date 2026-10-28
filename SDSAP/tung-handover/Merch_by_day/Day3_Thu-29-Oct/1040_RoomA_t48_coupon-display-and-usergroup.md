# Day3 - Thu-29-Oct 10:40 Room A - Topic 48 Coupon display and Usergroup

> Merch services in this session: MER-CPN-01 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 6 | MER-CPN-01 | Coupon and voucher creation | Must | Sprint 2 | Thành | 202 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728552 |

## Session: Topic 48 - Coupon display and Usergroup

| Field | Value |
|---|---|
| Inventory topic | #48 - Coupon display and Usergroup |
| Call (BiPlus plan v3) | Thu 29 Oct 10:40, Room A |
| SDSAP date / status | 29-Oct |
| Component / area | Promotion / Service |
| SDSAP PIC | Siti Sarah Binti Azman |
| Samsung Confluence link | Coupon; KB - Coupon Usergroup Setup HGE-11315 |
| Maps to (BiPlus) | MER-CPN-01 Coupon and voucher creation, MER-CPN-02 Coupon promotion rule setup and linking |
| Priority | Tier 1, Sprint 2, Must |
| Verdict | **Reuse** |
| BiPlus PIC for the topic | Thanh |

**Why this verdict:** Coupon display and usergroup, now also with the Coupon page; coupon creation is topic 47.

**Questions for SDSAP (from the sheet):** Which customer groups exist per market; how a usergroup coupon is tested before go-live.

## MER-CPN-01 - Coupon and voucher creation

> Tier 1 #6 | Must | Sprint 2 | Owner: Thành | QA: Xuan, Nga | ~202 tickets/month | M2 Voucher & Access code

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728552  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

*Full summary already given earlier in the week (first session: Day3_Thu-29-Oct/1020_RoomA_t47-c6_coupon-single-code-vs-multicode-extern.md); only the definition is repeated here.*

## What the service does
The requester gets a coupon - one public code or a batch of unique codes - that works on the requested sites for the agreed period, with redemption limits that cap the cost. A wrong value, missing cap or wrong stacking gives away margin in minutes; a leaked code or code file is a data security event.

