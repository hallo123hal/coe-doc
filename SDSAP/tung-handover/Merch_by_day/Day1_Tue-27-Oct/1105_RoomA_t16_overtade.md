# Day1 - Tue-27-Oct 11:05 Room A - Topic 16 Overtade

> Merch services in this session: MER-PRM-06 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 30 | MER-PRM-06 | Overtrade (trade-in) promotion | Optional | Sprint 4 | Tùng | 21 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696835 |

## Session: Topic 16 - Overtade

| Field | Value |
|---|---|
| Inventory topic | #16 - Overtade |
| Call (BiPlus plan v3) | Tue 27 Oct 11:05, Room A |
| SDSAP date / status | 27-Oct |
| Component / area | Added Service / Service |
| SDSAP PIC | Ong Hee Hui |
| Samsung Confluence link | KB - NZ Enhanced Overtrade |
| Maps to (BiPlus) | MER-PRM-06 Overtrade; catalogue v0.3 proposal (overtrade as AddedService discount) |
| Priority | Tier 1, Sprint 4, Optional |
| Verdict | **Clarify** |
| BiPlus PIC for the topic | Thanh |

**Why this verdict:** Now links KB - [NZ] Enhanced Overtrade: NZ only.

**Questions for SDSAP (from the sheet):** Is overtrade set up the same way in the other seven markets? Confirm the setup (AddedService discount on the base store).

## MER-PRM-06 - Overtrade (trade-in) promotion (Tùng's service)

> Tier 1 #30 | Optional | Sprint 4 | Owner: Tùng | QA: Xuan, Nga | ~21 tickets/month | M4 Price & Trade-in

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483696835  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

Focused notes for this service: [Day1_Tue-27-Oct/1105_RoomA_MER-PRM-06_overtrade.md](../../Day1_Tue-27-Oct/1105_RoomA_MER-PRM-06_overtrade.md)

## What the service does
Extra **trade-in value** (overtrade, trade-in bonus, trade-up value, double trade-up) on top of the partner's quote for the eligible new devices, sites and period in the brief - and it must end exactly at the end time. A wrong amount, missing site or missed end time pays unfunded value on every trade-in order, or under-pays customers who were promised the bonus.

## Key facts
| Item | Detail |
|---|---|
| Priority / sprint | Optional, Sprint 4 (Tier 1 #30) |
| Volume | 196 tickets in 2026, ~21/month (AU 65, NZ 55, ID 27, PH 24). Read the file, not only the title - the five top title patterns cover only ~10% |
| Roles | Doer: Merch operator (AU/NZ early pod). Checker: QA team member, **mandatory**, before PRD SETUP and at go-live. Approver: Shift Leader (+ Lead/Deputy for E4) - three different people |
| SLA | **Medium**: 16h resolution, 2h initial (internal 10h24 / 78 min). More than 2 promotion lines -> MER-PRM-09 (Low 24h). High 4h via MER-INC-01 |
| Change class | **Normal change, R3** - not a pre-approved standard change. No Knox path is documented for overtrade configurations; Knox applies to a rule-based bonus with a discount action. E4: exposure >=10,000 USD, >5 markets, or price file >=500 SKUs |
| Biggest risk | Value paid that the partner did not confirm, or still running after the end time |

## Decide the mechanism first (v0.1 wrongly treated all as promotion rules)
| Code | Mechanism | Where |
|---|---|---|
| **M1** | Overtrade = discount configuration (ExternalServiceDiscountConfig) on the store's TRADE_IN AddedServiceConfig; made by hand or by `TRADE_IN_DEVICE_PRICE` bulk upload (offer ID becomes config code). NZ, MY, ID, PH, TH (SG likely) | Backoffice > Base Commerce > Base Store > (store) > Administration > AddedService Configs > Discount Configuration |
| **M2** | CE trade-up value: base discount in MSA, mapped in Hybris (MSA Uploads / Trade in Configuration); extra discount via promotion rule with Qualifying Service Types = Trade Up | MSA Uploads, Product Cockpit |
| **M3** | Rule-based trade-in bonus (SEAU): promotion rule, name type TRADE-IN; **Knox applies** | Marketing > Promotion Rules |
| **M4** | Post-purchase cashback: discount mode CASHBACK on an M1 configuration | AddedServiceConfig |

**A discount configuration has no publish/status field** - it is effective from its Start Date when saved. Keep it non-live with a future Start Date or Open discount = false. End it with End Date or Open discount = false; **never delete** (orders and returns reference it).

## Recognise the ticket
Titles: *trade up, trade-in bonus, overtrade, double trade-up, ETI*. A table: device SKU/model, trade-in group, extra value, currency, cap (or SKU, value, set number); a start and end per set; AU/NZ ad-hoc windows with exact end time, ID monthly windows.

**Not this service:** T-Code sync -> MER-TRD-01; base trade-in values -> MER-TRD-02; trade-in reference on product -> MER-PRF-03; flags/badges -> MER-TXT-03; offer page/T&C -> MER-AEM-02; voucher rule -> MER-CPN-02; trade-in order/partner fault -> TEC-VAS-01; middleware -> TEC-TSP-02.

Variants: V2 trade-up value per SKU (most common, CE/DA/monitor, AU/NZ/ID) - V1 new overtrade/bonus (PH, SG, NZ, TH, ID) - V3 double/clearance trade-up - V4 change/extend - V5 end/remove - V6 stacking change.

## Workflow (V1, M1)
1. STG SETUP. Prerequisites: T-Codes active (MER-TRD-01), trade-in reference on each device (MER-PRF-03; without an active reference the cart cannot add trade-in), base values current (MER-TRD-02), provider enabled on the store (Q3).
2. **Amount table with partner confirmation** (on top of the quote or total? cap per order? funding party? instant or cashback?). Missing -> one combined question (template B), ON HOLD SUBS. **Never publish an unconfirmed amount.** PS-09: value above the confirmed partner table is a hold. No IMEI/serial/customer data in tickets.
3. Export before state (HAC Q1 or Discount Configuration screen). Check for overlaps.
4. Build the configuration (or upload `TRADE_IN_DEVICE_PRICE`, role productmanagerrole). Time zones: CSV method dates in GMT+8; NZ in NZT/NZDT (write both zones); stored UTC. "Compute Upto Price" button for the up-to price display.
5. Self-test on a storefront trade-in cart: each tier gets the bonus; no trade-in / non-eligible device / excluded site get none.
6. Internal check line -> QA REVIEW (trade-in cart + negative tests) -> Shift Leader approval -> PRD SETUP -> REVIEW SETUP (23:59 rule) -> PENDING LAUNCH (config starts itself at Start Date).
7. Live check within 30 min of start by a second person; QA repeats the main basket on one site per catalog type; monitor 2h. **Schedule the end verification 15 min after End Date** (AU/NZ midnight = VN evening; COE-LCH-04).

**V2 (CE trade-up):** validate the file (one row per SKU and site group, SKUs approved on the sites, no blanks); export current values incl. always-on to restore; upload through MSA Uploads (Base Store mandatory; store IDs comma-separated without spaces); set 2 / End Date = removal or revert to always-on; excluded sites (SME, business) carry no value; one quantity only per SKU.

## Known errors to remember
Some SKUs show no value (blank rows / SKU not approved, KE-01) - double trade-up missing (no base value, KE-02) - value not upgraded for the window (set not published / middleware delay, KE-03) - trade-up still shown after end (no remove set, KE-04) - overtrade combines with a voucher it should exclude (rule group mismatch, KE-05) - bonus on non-eligible brand (KE-06) - live on B2C missing on EPP (site/customer group missing, KE-07) - built as promotion rule instead of discount configuration (KE-08) - bonus active before intended start (no publish state, KE-10) - no trade-in option on PDP (T-Code/reference missing, KE-09).

## QA checklist
Table version + partner confirmation on ticket; prerequisites active; before export attached; rule/config name standard; sites and exclusions; each trade-in group gets the right value; no value without trade-in or on non-eligible device; cap respected at highest tier; stacking as instructed; start/end in market time and remove set scheduled; cart message and PDP section in local language; Knox approved before publish where used.

## Samsung KB to read first
Overtrade 2.0 (2477327681) - KB - Overtrade via csv import (2477360656) - KB - 3. External Service Trade-in (MX Overtrade) (2477916625) - KB - [NZ] Enhanced Overtrade (2477196782) - Bulk Upload CE Trade-up (Revamp) (2477523394) - KB - TV/CE Trade-up Mapping Setup in Hybris (2477687257) - SEAU: Trade-in/Overtrade/Trade up (2477195677) - KB - Promotion Rule Condition (2478114280).

## Open points the pack marks "confirm in KT"
Whether SG uses M1 - how QA tests a configuration before its start date - exact order of reduction (Promotion -> Trade-in -> Overtrade) - VariantTradeinMapping type name - TradeInBonus link to the "Overtrade Discount Bonus" screen - test IMEI/quote method. Catalogue proposal: move overtrade / CE trade-up to a MER-TRD group (new MER-TRD-03); until then follow the v0.2 runbook. Practise only on `TRAINING_` configs on staging.

