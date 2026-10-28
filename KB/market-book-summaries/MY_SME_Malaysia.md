# MY Market Rules Page – SME Malaysia (summary)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486829431 (page ID 2486829431, last modified 2026-10-27, author Thao Bui Phuong)

## Profile
| Item | Value |
|---|---|
| Market / subsidiary | Malaysia – SME |
| Jira project | MYME |
| Timezone | MYT, UTC+8 (one hour ahead of Hanoi) |
| Business model | Indirect; no FI posting |
| Language | English |
| Volume | ~300 requests/month – highest tier together with Vietnam |
| Pattern | Strong day-1-of-month launch concentration; state-specific and ad hoc public holidays |

The page is an operating guide, not a policy source of record; the latest approved Samsung instruction prevails. (Note: the page has a section-numbering glitch – product setup content sits under the "Promotion rules" heading.)

## Contacts
- Calvin – Head of Part and primary 3PD business owner.
- Stakeholder groups to map: business lead, merchandising requesters, Tech counterparts, payment vendors, tax/legal contacts. Classify each as requester, approver, validator, technical dependency owner or escalation owner. Weekly rhythm with the subsidiary recommended.

## Staffing
- One primary Market Owner, one named backup, QA not shared too thinly with another peak market at month opening. SG cross-skilling helps, but MY must not be treated as a simplified SG. Readiness review one business day before month opening; holiday watch process for state/ad hoc holidays.

## Price and promotion governance
- RHQ and Knox approval; PC ticket reference where required; platform promotion prohibited after the policy date. Warehouses: CE WC10 S506, MX WC11 S506. If a correctly priced item is not purchasable, check approval, delivery mode, stock and warehouse before blaming price.
- Treat launch + price + payment + SC+ tax changes as one launch package. Doer / checker / approver separation is mandatory.

## Product setup
- Lowest-level category in bulk upload (MX: SP, TB, WR, AS; CE: AC, AV, REF, Monitor, TV, VC, MWO, WSM…). Super sync DOTCOM/STOCK/PRICE with the usual failure handling.
- External service types: smartphones/tablets/Watch6 use BENEFIT, ACCESSORIES, TRADE_IN, INSURANCE; other MX accessories may add TRADE_UP. IMEI required for mobile/tablet.
- Delivery modes: MX `my-delivery-standard`, `my-sfs-express`, `my-o2o-pickup`, `my-o2o-pickup-expres(s)`; SMB CE adds `my-delivery-standard-bulk-chargeable`, `my-ce-schedule-delivery`.
- References: AVAILABLE_SERVICE to T-ADDON, trade-in T SKUs, TRADE_UP. Benefit config via CSAdmin master lists (`MY_MASTER_BC_DO_NOT_DELETE`, etc.).
- F-code products (notably air conditioners): services may anchor on a main child SKU rather than the displayed F-code.

## Trade-in, trade-up, overtrade
- Provider CompAsia; daily morning sync cronjob; only IMEI-eligible models appear. Overtrade is present – clarify whether a request means trade-in, overtrade top-up or trade-up service.

## SC+ and e-invoice
- SC+ has standalone warranty setup, pack-code logic, subscription flow and a legal monthly e-invoice requirement (B2Bi invoice request config). Treat as a service-product domain with a dedicated runbook, not simple add-on merchandising.

## Payment
- iPay88 (online banking, instalment, eWallet, SC+ monthly), Razer (Samsung Pay by Razer – production status TBD, MYME-17890), Samsung Finance. Document by provider, mode and business rule.

## Delivery / OMS
- OMS 2.0 and BOPIS for West Malaysia; O2O needs store onboarding, IP whitelist and store-agent access. A "product problem" may really be a missing delivery mode or store scope.

## EPP / SMB
- Login types SSO_ACCESSCODE, SSO_DOMAIN, SSO_VERIFICATIONCODE, all on `myb2bProductCatalog`; 19 listed sites (e.g. `epp_aiavitality`, `epp_cuckoo`, `eppsme`, `government_my`, `epp_education`, `my_member`). AIA Vitality uses external SSO – define ownership boundaries.

## 3PD, compliance, risks
- 3PD: TikTok Shop and Lazada; integration path needs confirming; CE SC+ on 3PD is a local nuance.
- E-invoice is a legal requirement (also SC+ monthly); MSA fraud rules may masquerade as checkout failures; three QC layers: doer/checker split, sensitive-change review, post-go-live verification.
- Risks: volume overload, day-1 launch failure, SC+ invoice defects, EPP complexity (EPP 2.0 aging issues), holiday disruption, payment misconfiguration.

## Transition
Early deep-dive market. Five workstreams: site/EPP inventory, SC+ & e-invoice runbook, payment matrix, trade-in/overtrade clarity, day-1 readiness discipline. Readiness should be proven by walkthroughs (product setup, SC+ with invoice effect, payment validation, EPP access triage, month-opening launch package), not just documents.

## Reference matrices
Key attributes, payment landscape, specialist capabilities (trade-in, overtrade, F-code, SC+ standalone/subscription invoice flow, BOPIS, OMS 2.0, external SSO). Discovery questions are on the page but not reproduced here.
