# Day2 - Wed-28-Oct 14:30 Room A - Part C #3 Live merchandising error correction (wrong price or promotion on the live site)

> Merch services in this session: MER-INC-01 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 31 | MER-INC-01 | Live merchandising error correction | Optional | Sprint 4 | Trang | 21 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728742 |

## Session: Part C #3 - Live merchandising error correction (wrong price or promotion on the live site)

| Field | Value |
|---|---|
| Part C item | #3 - Live merchandising error correction (wrong price or promotion on the live site) |
| Call plan | Added: Wed 28 Oct 14:30, Room A |
| BiPlus mapping | MER-INC-01 Live merchandising error correction, Tier 1, Sprint 4; feeds MER-SOP-02 P0 Process. |
| BiPlus PIC for the item | Thuy Trang |

**What to ask SDSAP (from the sheet):** A session with the last real cases (keys only).

## MER-INC-01 - Live merchandising error correction

> Tier 1 #31 | Optional | Sprint 4 | Owner: Trang | QA: Xuan, Nga | ~21 tickets/month | M7 Errors, checks & BVT

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728742  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
Live merchandising data on production (wrong price, promotion, voucher/coupon, stock, or offer content) is **contained fast, corrected, checked by a second person and QA on the live storefront, and handed to incident reporting**. Every hour a wrong price or generous promotion stays live becomes orders Samsung must honour or cancel, so **containment comes before investigation**.

## Key facts
| Item | Detail |
|---|---|
| Volume | 199 tickets in 2026, ~21/month, 8 markets (MY 50, PH 43, VN 28, SG 26) |
| Roles | Doer: certified Merch operator (on-call only if certified on MER-PRC-02, PRM-01 and CPN-01). Checker: a second checker (not the fixer) within 30 min, then QA team / QA on-call. Approver: Incident Manager authorises the emergency action; Shift Leader approves re-enable |
| SLA | **High 4h** at any hour if expected loss >10,000 USD or data security affected (unknown loss on a high-traffic SKU is High until estimated; only the Merchandising Lead downgrades). Internal: acknowledge 15 min (30 out of hours), contain within 30 min of T0 with a kill switch (60 without), tell RHQ + subsidiary within 30 min, resolve in 2h36 |
| Change class | **Emergency change** on production, handled on the original ticket; no PC for Merch actions (Tech actions: COEC + PC). Knox again before the next publish if ACTION / CONDITION / WEBSITE / DATE of a promotion changes |
| Biggest risk | Loss keeps running while the team investigates, or the fix creates a new error |

## Recognise the ticket
A comment `[INCIDENT]` on the original Shop Merchandising ticket, or from RHQ (Mattermost), CS, a post-change check, the order anomaly monitor or a QA go-live check. Many arrive as ordinary Low tickets ("not applying", "wrong price", "cannot use voucher") - **if it is live and customers see it, it is this service**. If not live or the set-up works as briefed, send back to the original service. **Not this service:** report/RCA/CAPA -> COE-INC-02 - several markets or checkout blocked -> COE-INC-01 bridge - engine/cache/sync defects -> Tech via COEC - cancelling or adjusting placed orders (subsidiary decides, Tech executes; BiPlus never touches orders or contacts customers).

Variants: **V2 promotion wrong/not triggering** and **V3 voucher/coupon not working or leaking** (most common) - V1 wrong price live - V5 wrong offer content/links/references - V4 stock/availability/product missing - V6 data-security exposure (always High/Critical).

## Workflow (first 15 minutes, then variant)
1. Record **T0** and comment `[INCIDENT]` within 5 min; confirm it is live on the real storefront (private window, right customer group). 2. Shift Leader sets severity and loss estimate; High -> call the Merchandising Lead (out of hours: Merchandising escalation on-call), open COE-INC-02. 3. Find the source (original ticket, rule/coupon code, Knox record, last modified time). 4. Suspect a technical cause when data did not change but behaviour did -> linked COEC in parallel. 5. Notify RHQ and the subsidiary within 30 min (template A).
- **Containment ladder**: correct the value if the approved one is known -> end only the faulty rule/coupon on the affected sites -> make the SKU not purchasable -> hide the page/banner/GNB item. Export the before state and write the rollback *before* acting. Never delete objects (needed for the RCA).
- V1 price: correct the Price Row in Staged, sync only the affected product, Knox with prefix "URGENT LIVE ERROR" and call the approver; check F-code = sum of components. V2: look first for a higher-priority **halt rule** in the same promotion group and rules published to the preview module only (KE-11). V3: deactivate the coupon at once if leaking; a leaked code *file* is V6.
- Verify on the live storefront; second checker within 30 min; Market Owner monitors orders every 15 min for 2h; Tech counts orders at the wrong value via a linked COEC.
- All work on Samsung systems happens in the **secure work area of the Hanoi centre**; an on-call person outside only advises by phone.

## Known errors
Old price still shows (not synced / cache / overlapping Price Row validity) - promotion stops when a new campaign starts (halt rule) - works on B2C not EA/SMB - promotion disappears when a voucher is applied (stacking) - restricted coupon usable by non-eligible users - F-code price differs from cart - wrong tax basis - fix blocked by a freeze (Lead asks RHQ exception) - correction waits hours for Knox.

## QA checklist
Priority matches the loss estimate; before export + rollback written first; containment stopped the loss; corrected value equals the approved source; only affected sites/objects changed; PDP, cart and checkout correct; other promotions still work; voucher tested with eligible and non-eligible accounts; bundles/gifts/attached services; timeline complete; RHQ + subsidiary notified, COE-INC-02 linked.

## Samsung KB to read first
KB API check: Product References, Benefit, etc (2477785727) - KB Storefront API (2477917209) - Overselling Common Mistake (2477851857). Only 5 KB pages map here; the steps come from the v0.2 runbook.

