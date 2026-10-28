# Day3 - Thu-29-Oct 10:20 Room A - Topic 47 Coupon Single Code VS Multicode External Serial Coupon Coupon Ingestion + Part C #6 Coupon and voucher creation, unique code batches

> Merch services in this session: MER-CPN-01 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 6 | MER-CPN-01 | Coupon and voucher creation | Must | Sprint 2 | Thành | 202 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728552 |

## Session: Topic 47 - Coupon Single Code VS Multicode External Serial Coupon Coupon Ingestion

| Field | Value |
|---|---|
| Inventory topic | #47 - Coupon Single Code VS Multicode External Serial Coupon Coupon Ingestion |
| Call (BiPlus plan v3) | Thu 29 Oct 10:20, Room A |
| SDSAP date / status | 29-Oct |
| Component / area | Promotion / Service |
| SDSAP PIC | CHONG HAW EONG |
| Samsung Confluence link | Coupon; KB - Serial Voucher Code GCDM Ingestion |
| Maps to (BiPlus) | MER-CPN-01 Coupon and voucher creation; MER-CPN-02 Coupon promotion rule setup and linking |
| Priority | Tier 1, Sprint 2, Must |
| Verdict | **Reuse** |
| BiPlus PIC for the topic | Thanh |

**Why this verdict:** New topic (26 Oct): single code, multi-code and external serial coupons and coupon ingestion, with the Coupon page and KB - Serial Voucher Code GCDM Ingestion. It covers MER-CPN-01 Coupon and voucher creation, the second biggest service, which BiPlus had asked for.

**Questions for SDSAP (from the sheet):** How code files are delivered to the market; limits per market; who approves a batch; what to do when an ingestion fails.

## Session: Part C #6 - Coupon and voucher creation, unique code batches

| Field | Value |
|---|---|
| Part C item | #6 - Coupon and voucher creation, unique code batches |
| Call plan | Covered by the new topic 47 (Thu 29 Oct 10:20, Room A) |
| BiPlus mapping | MER-CPN-01 Coupon and voucher creation, Tier 1, Sprint 2, Must: the second biggest service. |
| BiPlus PIC for the item | Thanh |

**What to ask SDSAP (from the sheet):** SDSAP added topic 47 on 26 Oct; ask how code files reach the market and the limits per market.

## MER-CPN-01 - Coupon and voucher creation

> Tier 1 #6 | Must | Sprint 2 | Owner: Thành | QA: Xuan, Nga | ~202 tickets/month | M2 Voucher & Access code

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728552  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## What the service does
The requester gets a coupon - one public code or a batch of unique codes - that works on the requested sites for the agreed period, with redemption limits that cap the cost. A wrong value, missing cap or wrong stacking gives away margin in minutes; a leaked code or code file is a data security event.

## Key facts
| Item | Detail |
|---|---|
| Volume | 1,918 tickets in 2026, ~202/month, 8 markets (PH, MY, VN most). Second biggest Merch service |
| Roles | Doer: Merch operator (senior for large unique-code batches, credit batches, migrations). Checker: QA team, mandatory on the restricted set-up. Approver: Shift Leader, then the Knox approver of the rule |
| SLA | Low: 24h, 2h initial; internal 15h36 / 78 min. High 4h via MER-INC-01 if a code or code file is exposed or loss >10,000 USD. Waiting for Knox never pauses the clock |
| Change class | Standard (Knox applies to the **rule** behind the code, not the coupon). Normal + Sub-Lead for migration / ImpEx loads (batches above ~500,000 codes: Tech via COEC + PC). E4 when value x total uses >= 10,000 USD |
| Biggest risk | Wrong value, missing cap or wrong stacking live; code or code file leaked |

## Recognise the ticket
Titles: *voucher, coupon, promo code, reinstate, extend, live commerce*. Brief **VOU-01** (code/prefix, quantity, dates, total and per-customer limits) and stacking matrix **VOU-02**. The rule behind the code is a MER-CPN-02 action line in the same ticket. **Not this service:** referral vouchers TEC-RFL-02 - redemption eVoucher MER-PRM-08 - add-on page eVoucher MER-BYP-04 - EPP access codes TEC-EPP-03/06 - customer questions TEC-ORD-06 - My Voucher page defects TEC-TSP-05 - live error MER-INC-01.

Since **1 May 2026 every new promotion uses coupons** (SingleCodeCoupon, MultiCodeCoupon, EmailRestrictedMultiCodeCoupon); serial/promotional vouchers stay only for RNPL and legacy. If the brief says "voucher", check which object it means.

Variants: **V1 single public code** (most common) - V2 unique code batch - V3 EPP/SMB/CRP/corporate coupon - V4 VOC compensation and reinstatement (MY "Reinstate voucher") - V5 live-commerce coupon (one window per session) - V6 voucher credit batch and My Voucher page - V7 change existing coupon.

## Workflow (V1, key steps)
1. Check the code is free (Marketing > Coupon Management > Coupons). 2. Create the SingleCodeCoupon: code upper case, Start/End in market time, Maximum Total Redemptions, Maximum Redemptions per Customer, Hide in My Voucher Page. 3. Internal-check comment on the ticket. 4. Link the rule ("Coupon code" condition). 5. Apply the **test restriction** (user group / email / email hash). 6. Self-simulate five scenarios in the promotion simulator. 7. QA REVIEW. 8. After QA + Shift Leader: remove the restriction, fill the Approval section, Publish to Knox (no Knox status in Jira - write reference and path in a comment). 9. Rule goes live up to ~1h after approval; check on one site per channel.
- Plan Knox at least **one working day before go-live**. The requester read-back is no longer a step (CEO decision 21 Oct 2026).
- A customer group cannot be created by Merch - COEC ticket to Tech.
- Code format: 4-character prefix + 3 parts of 4 characters (RHQ 24 Apr 2026), e.g. CEOD-5BM9-9GML-GCNK.
- **Unique codes leave Hybris only through the RHQ-approved channel**, password-protected, password sent separately; never Jira, email, chat or an AI tool.
- Extending a coupon: change the coupon End Date **and** the rule End Date (Knox again), otherwise the voucher stops at the old date (KE-06).

## Known errors
Code "not valid" after go-live (restriction left on, Knox pending, site missing, inactive, time zone) - wrong stacking - discount on the wrong base - rules inactive after resubmission (two KNOXAPPROVED versions) - old end date - excluded product discounted - My Voucher name wrong/English only.

## QA checklist
VOU-01 complete and code conflict-free; dates and time zone on coupon and rule; both limits set; sites/channels/customer group; value and mechanic; min spend and exclusions; every stacking pair of VOU-02; second use by the same customer refused; batch count (V2); no code list on the ticket; Knox reference recorded.

## Samsung KB to read first
Coupon (2478114191) - KB Coupon Usergroup Setup HGE-11315 (2477458683) - Assign Multi-Code Coupon to Specific Customer E-mails (2477950184) - My Voucher Component (2477917560) - KB Promotion Rule Knox Approval (2477949466).

## Open points the pack marks "confirm in KT"
Max batch size (KB says 1 million, runbook says ~500,000 -> Tech ImpEx) - what CRP covers per market - coupon use of the GCDM CRM ingestion - uniqueness of a code per instance - where the approved file channel/tool/retention is defined.

