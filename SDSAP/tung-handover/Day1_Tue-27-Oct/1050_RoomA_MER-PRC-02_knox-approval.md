# MER-PRC-02 - Special price setup

> Day 1 - Tue-27-Oct | Owner: **Tùng** | QA: Xuan, Nga | Tier 1 #11 | Must | Sprint 3 | ~117 tickets/month | Module: M4 Price & Trade-in

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483598300  
*Summary of the Service Pack page (condensed v0.2, revised 25 Oct 2026). Always re-read the page itself before the session - this is a study aid, not a replacement.*

## Session (SDSAP handover)
| Field | Value |
|---|---|
| Inventory topic | #15 - Knox Approval |
| Call (BiPlus plan v3) | Tue 27 Oct 10:50, Room A |
| SDSAP date / status | 27-Oct |
| Component / area | Process / Service and operations |
| SDSAP PIC | CHONG HAW EONG |
| Samsung Confluence link | KB - Special Price Knox Approval |
| Maps to (BiPlus) | MER-PRC-02 Special price; COE-SOP-03 Change Management (CM) (Knox); catalogue v0.3 proposal: Knox as its own service |
| Priority | Tier 1, Sprint 3, Must |
| Verdict | **Reuse** |
| BiPlus PIC for the topic | Thanh |

**Why this verdict:** The special price Knox page fits. Knox waits are often longer than a day and drive the SLA.

**Questions for SDSAP (from the sheet):** Include Knox for promotions, vouchers and batches; the approval line per market; what to do when Knox is stuck or rejected; does the SLA clock stop while waiting?

## What to focus on in this session

- This session is the Knox side of special price: which actions raise a PriceInfoChange, who approves on each path, what SDSAP writes in the submit (Approval Title, Comment, Business PIC, Approval Process).
- Confirm the rules the Service Pack relies on: path follows the highest discount in the submit, max 300 rows per submit, submit the same working day, chase at 50% of SLA / go-live minus 1 working day / minus 4h.
- Ask what SDSAP does when an approver is on leave (error APE017) and when Knox rejects (KNOXREJECTED); who owns the KnoxAccount fix (Tech via COEC).
- BiPlus proposal in the catalogue (v0.3): treat Knox as its own service - hear whether SDSAP agrees.

## What the service does
The requester gets a **time-bound special selling price**, shown against the RRP, for a campaign window on the requested sites. Approved in Knox and checked by a second person at the **start and at the end** of the window. Overlap, stacking with a promotion, wrong start/end or a price that stays after the window are direct margin loss.

## Key facts
| Item | Detail |
|---|---|
| Priority / sprint | Must, Sprint 3 (Tier 1 #11) |
| Volume | 1,100 tickets in 2026, ~117/month, 8 markets (most: PH, VN, ID, NZ, MY) |
| Roles | Doer: price-certified Merch operator. Checker: QA team (Check A on file, overlap and stacking before Knox). Second person: Check B at start, Check C at end. Approver: Shift Leader (+ Merch Lead/Deputy for E4), then Knox approver |
| SLA | Low: 24h resolution, 2h initial response; internal 15h36 / 78 min. Submit Knox within 4 working hours of complete intake |
| Change class | R3. Standard within thresholds; **Normal** for: >500 rows, discount >=30% (PS-05) or drop >=20% (PS-02), window <72h starting outside market hours, F-Code bundle prices, Tech removal of rows, first upload of a market (E4) |
| Biggest risk | Overlap with another window or stacking with a promotion; wrong start/end time; window ends but price stays |

## Recognise the ticket
Titles: *special price, flash sale, payday, price match, clearance, single price, [W18]*. File on the Special Price template with validityFrom + validityTo and either price or discountPercent per SKU; a named window and a list of promotions that may/may not combine. **Not this service:** no end date -> MER-PRC-01; discount rows -> MER-PRC-03; cart/BOGO/bundle/coupon -> MER-PRM / MER-CPN; freebie removal -> MER-PRF-04; wrong price already live -> MER-INC-01.

Variants: V1 campaign/tactical - V2 short-window sale (most common: NZ "Flash Sale") - V3 price match (AU "HA Price Match", weekly) - V4 clearance/aging stock - V5 single price setting (VN, final non-stackable price) - V6 update/extend/remove.

## Workflow (V1)
1. STG SETUP + internal check line (SKUs, price/discount, start/end with time zone, sites, stacking, usage limit, "Matches approved brief vX"). Run PS-01..05, 10, 13.
2. Export before state: regular, **RRP** and special rows (current and future). **No RRP = the upload fails** -> raise MER-PRC-01 first.
3. **Overlap check** (Q1/Q2): any overlap, from this or another ticket, goes to the requester before upload. Never upload an overlapping row. (A discount row cannot hold the same SKU with different validity - error "duplicated PriceInfoChange" - price rows allow it.)
4. **Stackability**: list promotions active on the SKUs/sites during the window (Marketing > Promotion Rules) and compare with the brief.
5. Upload `SPECIAL_PRICE` per catalog; prove records VALID on 100% of rows.
6. QA REVIEW (Check A) -> Shift Leader approval (PRD SETUP) -> submit Knox same day (<=300 rows/submit; path follows highest discount in the submit).
7. Cron jobs as MER-PRC-01 (KNOXAPPROVED -> COMPLETED). Sync **before the start**, only after approval. Approval after start: stop, new start in writing. Approval after end: do not sync, close as not run.
8. Align linked "Save" text / flags / benefit offers (MER-TXT-03 / -02) to the same validity.
9. **Check B** within 30 min of start (E4: 15); **Check C** within 60 min after the end (next market morning, sample, for windows >14 days). Several windows = one sub-task and one B/C per window; ticket sits in PENDING LAUNCH between waves.
10. Out-of-hours start/end: book the checks at intake (COE-LCH-04).

Template window: start and end are mandatory; end is 23:59:59 local unless the brief says otherwise. Use the same UTC table as MER-PRC-01 (SG/MY/PH 16:00 prev. day; TH/VN/ID 17:00; NZ NZDT 11:00; AU AEDT 13:00).

## Known errors to remember
Approved but price never appears (stuck KNOXAPPROVED / clash with earlier window, KE-01) - old special price still shows (overlap, KE-02) - cart lower than intended (stacked with a promotion, KE-03) - bundle total differs from components (KE-04) - starts at 08:00 not midnight (local typed as UTC, KE-05) - RRP shows after window instead of AON (KE-07) - "Save" text outside price validity (KE-08) - Check B impossible, SKU out of stock (use price report, KE-09) - KNOXREJECTED (KE-10) - wrong/missing was-price (`disableSavingInfo` true or <2 special rows, KE-11).

## QA checklist
Data sufficient; start/end UTC = local; special price below RRP; discount equals brief; no overlap; stacking list checked; bundle equals component sum; record export = file on 100% rows; sync after approval; price report diff zero; PDP special price + RRP struck through at start; cart/checkout totals; no unintended stacking; agreed price after end.

## Samsung KB to read first
Special Price Knox Approval (2477982196) - KB - Product Price (2477949955) - 0. KB - SEAO Multistore Site Matrix and Price Template (2477622304) - Knox Price Approval (2477916752) - KB - Was Price / wasprice (2477491909) - SEAU: Price (2477622358) - KB - Special Price Setup Checklist (2477622337; body is an embedded file, ask your lead for the Samsung original).

## Open points the pack marks "confirm in KT"
Whether the AON price resumes after a special price ends (SEAU page says yes; tickets show RRP appearing) - meaning of VN "single price" - Products Sync Selector vs Synchronize for this ticket - how Tech removes a clashing row (COEC TEC-TSP-03 + PC ticket).

