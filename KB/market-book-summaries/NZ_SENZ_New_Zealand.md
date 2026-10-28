# NZ Market Rules Page – SENZ New Zealand (summary)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486763864 (page ID 2486763864, last modified 2026-10-28, author Thao Bui Phuong)

## Profile
| Item | Value |
|---|---|
| Market / subsidiary | New Zealand – SENZ |
| Jira project | NZHME |
| Timezone | NZST / NZDT – during daylight saving the market day starts ~03:00 Vietnam time |
| Business model | Direct |
| Volume | ~150 requests/month, driven by campaign windows |
| Timing | ~35% of requests arrive before 08:00 Vietnam time |
| Tech aging | 9 tickets (lower than most markets) |
| Distinctive features | Assurant trade-in, enhanced overtrade with local-date dependency, SC+ legal icon rule, Farmlands EDI card, NZ Post address validation, Resene colour integration |

Smaller by volume but timing-sensitive and rule-heavy; the page consolidates available information and lists items needing validation with the subsidiary and RHQ.

## Contacts
- Cooper Ma – 3PD point of contact. All other roles (business owner, Tech, trade-in/Assurant, payment, EPP/Farmlands, approval authority) are placeholders to confirm. Recommend a weekly market sync and named on-call routing; keep NZ roles explicit even if AU and NZ share a sub team.

## Staffing
- Most time-sensitive market in the portfolio. Needs an early-shift primary owner plus backup, a morning triage checklist (price, promotion, payment, order exceptions), agreed weekend/public-holiday expectations (e.g. Waitangi Day) and daylight-saving tracking in the roster. Do not assume AU coverage protects NZ.

## Channels
- Jira is primary; email for escalation/vendors, summarized back to Jira; weekly sync; defined emergency escalation. Define subject format, evidence/screenshot convention and turnaround commitments.

## Price
- RHQ ticket and approval governance applies; local approval chain to confirm. Clarify how list, campaign, EPP price, overtrade value and trade-in offsets interact. EPP pricing (including Farmlands) needs approval, upload method and evidence defined; check customer/account-specific contract logic. SC+ legal icon affects price/value display.

## Promotion and coupon
- Supports overtrade and enhanced overtrade. Enhanced overtrade file upload uses NZ local date, not UTC – validate dates, site scope and customer communication before every release. Promotions by platform are prohibited under RHQ policy.
- Coupons follow the common 4-4-4-4 format; site scope, conflict rules with trade-in/overtrade/financing, and issuance/deactivation processes need confirming.

## Products and content
- SC+ must use a dedicated icon in NZ for legal reasons (page-level legal QA). Resene colour integration for Bespoke refrigerators. Obtain NZ fundamental SKU setup (warehouses, delivery modes, service types, references) – do not copy AU assumptions.
- AEM: embed legal display rules in QA; complete content QA before the NZ business day opens; no detailed AEM inventory yet. Add-on/service pages (SC+, trade-in, financing, Farmlands flows) need inventory.

## Logistics and payment
- NZ Post is used for address validation; delivery-mode mapping, service-area logic, lead times and holidays still to document.
- Payments: Adyen, PayPal, Laybuy, POLi, Flexi card, and the Farmlands card integrated by EDI on the Farmlands EPP site. Test Farmlands separately from baseline payment flows.

## Channels
- EPP: Farmlands is a distinct partner environment with EDI; count of EPP sites and login types unknown. SMB and O2O: nothing highlighted – validate presence. 3PD: "The Market" is the 3PD channel; smaller footprint but lower team familiarity.

## Risks and transition
Risks: early market start, enhanced-overtrade date dependency, Assurant trade-in/clawback, Farmlands payment complexity, SC+ legal display, low-familiarity risk. Transition priorities: stakeholder and approval map, Assurant operating model (incl. clawback), overtrade upload process with local date control, payment and Farmlands behaviour, SC+ icon review, NZ Post exception process, The Market 3PD model, and early-shift model with daylight saving.

## Reference matrices
Table of known data with confidence levels (e.g. trade-in vendor Assurant/Assurant V2 – medium; enhanced overtrade – high; payment methods – medium; address validation NZ Post – high) and a 52-question discovery set (including "top five concerns SENZ has about the transition").
