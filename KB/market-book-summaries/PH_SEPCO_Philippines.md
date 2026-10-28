# PH Market Rules Page – SEPCO Philippines (summary)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486731216 (page ID 2486731216, last modified 2026-10-27, author Thao Bui Phuong)

## Profile
| Item | Value |
|---|---|
| Market / subsidiary | Philippines – SEPCO |
| Jira project | PME |
| Timezone | PHT, UTC+8 (one hour ahead of Vietnam) |
| Business model | Direct; FI posting yes |
| Platform | New Hybris (restricted handling, similar to Indonesia) |
| Volume | ~225 requests/month; go-live concentrated on day 1 of each month |
| Notable | Island logistics (PIN map / TAT), heavy MX overtrade, one of the highest 3PD ticket volumes |

Document status: working market book, to be validated with SEPCO in intro calls, follow-ups and hypercare.

## Contacts
- 3PD: Jewel Regal (business owner), Raymond (operations backup).
- Placeholders to fill: business lead, merchandising PIC, Tech PIC, Knox approval owner, Bolttech trade-in counterpart, payment vendor counterpart, logistics/PIN map owner. Map contacts in four layers: working PICs, approvers, subject-matter owners, escalation owners.

## Staffing and channels
- Plan for a peak market: primary owner who understands New Hybris, PIN map and the monthly rhythm; backup for day-1 and 3PD; Tech pod for payment/logistics/order/integration; QA for trade-in and SC+.
- Jira comments are primary; email for formal follow-up; Mattermost/RHQ chat for RHQ; record approved vendor routes (Bolttech, payment gateway, serviceability, 3PD).

## Price
- NERP sync for standard products; Knox approval required. External-service/maintenance-pack SKUs may need manual handling. Three-step discipline: confirm source & sync → confirm documented approval → confirm displayed price and basket outcome. Trade-in value is shown as an incentive – ownership of checks must be defined.

## Promotion and coupon
- Knox approval before production. Overtrade is heavy on MX and may need extra permissions or product manager support; check trade-in/service interaction at basket level; separate 3PD readiness tracker.
- Coupon format 4-4-4-4; validate channel scope, payment interaction and trade-in interaction.

## Product rules
- Catalog selling matrix: eStore, EPP and SMB sell MX and CE; 3PD sells CE only (no MX).
- Setup elements: warehouse mapping per catalog, delivery modes (MX standard + O2O pickup; CE standard), PIN map for new CE SKUs, benefit setup for blue-bubble offers, external service type at child catalog. Mandatory checklist: category, sync, warehouse, delivery mode, PIN map, benefit, external service type, price, site-level verification.
- AEM readiness is only one release gate (AEM + Super Sync + Hybris + front-end verification).
- Service products: SC+ (all four types) and CE Maintenance Pack; standalone SC+ requires a normal product plus an EXT product, manual RRP for the EXT SKU and dedicated toko config.

## Delivery
- PIN map and TAT data ownership/cadence must be defined; validate Metro and non-Metro scenarios; define cut-off before campaign launches and an escalation path for serviceability-related checkout failures.
- Warehouses/delivery modes: eStore & EPP MX `WC3L-S513` (`ph-delivery-standard`, `ph-o2o-pickup`), CE `WCOL-S513` (`ph-delivery-standard-ce`); 3PD CE `WC3B-S513`; SMB MX/CE `WC1B-S513`.

## Payment
- iPay88 ecosystem (Atome, Home Credit, BillEase, EastWest Bank), COD with OTP, CreditLine. Need a payment/checkout incident routing matrix (failed, pending, duplicate, mismatch states) with vendor touchpoints.

## Channels
- EPP: OFW, government, education, banks. SMB: non-VAT checkout behaviour. O2O: tied to MX pickup. 3PD: CE-dominated, high volume, needs dedicated tracker and ownership.

## Risks and transition
Risks: 3PD load, PIN map/TAT dependency, New Hybris limits, overtrade intensity, month-opening spike, payment diversity, service-product complexity. PH should not be treated as a clone of Indonesia. Recommended approach: validate contacts, site inventory, product setup checklist, test packs (overtrade, Bolttech trade-in, COD OTP, service products), monthly day-1 readiness ritual, payment routing matrix, and hypercare tracking of recurring issues (possible standing 3PD/serviceability specialist). Trade-in partner is Bolttech.

## Reference matrices
Operational profile summary, warehouse/delivery references, a 52-question discovery set, and a source list (Feature for each SUB, PH Fundamental SKU setup pages for MX and CE, SC+ On Demand Standalone KB, Warehouse Mapping, handover meeting notes, Bolttech trade-in flow and API spec PDFs).
