# SG Market Rules Page – SESP Singapore (summary)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486731199 (page ID 2486731199, last modified 2026-10-27, author Thao Bui Phuong)

## Profile
| Item | Value |
|---|---|
| Market / subsidiary | Singapore – SESP |
| Jira project | SPHME |
| Timezone | SGT, UTC+8 (one hour ahead of Hanoi) |
| Business model | Direct (one secondary source says Indirect – flagged as a conflict); FI posting and SO posting active |
| Volume | ~150 requests/month; go-live in the first week of each month |
| Aging | 31 Tech aging tickets (Dec 2025) – highest of the 8 markets |
| RHQ proximity | RHQ stakeholders based in Singapore (Oliver Leung, Srashti, BK) – issues get fast regional visibility |

Operating guide, not policy of record; latest approved Samsung instruction prevails.

## Contacts
- Ashley – key 3PD contact (backup route to confirm). Other groups to validate: business lead, requesters, Tech, payment owners, tax/finance contacts, SC+ owners. Weekly review on incidents, launches, payments, tax and 3PD health.

## Staffing
- One primary Market Owner (senior), named backup, stable QA, specialist access for payments, SC+, 3PD; plan a dedicated aging-reduction track. Launch events need standby coverage and partner (Intrepid) escalation readiness.

## Price and promotion
- RHQ governance with approval evidence; price errors propagate into invoices, posting and refunds. Warehouse WC91 for both CE and MX.
- Long Term Financing EPP: promotions allowed; special price/discount rows only if provided by SESP; Trade Up off.
- SMB GST rules: prescribed goods eligible for tax relief → use only Percentage Discount on Products (no conflicting price/discount rows); non-prescribed goods → Target Fixed Price on Products. GST reversal depends on GST-registered customer, CA threshold above SGD 10,000 for prescribed goods, non-VAT sold-to behaviour and mixed-cart effects on FI/SO posting.

## Trade-in, trade-up, Singpass
- TIPLUS middleware between Hybris and providers such as CompAsia. T SKUs are created by `sg tiplus product price imports`, then must be approved and synced to the child catalog; questionnaires come from `sgtiplus question imports`.
- Singpass Myinfo verification is mandatory for Trade-In orders after customer details and delivery slot, before payment; data is stored encrypted on the order; failure blocks checkout. Applies to Home Delivery and BOPIS.
- Trade-Up supported (especially CE); daily clawback report cronjob exists.

## SC+
- Bundle, standalone and subscription; standardized SKU formats (bundle upfront/monthly, standalone upfront, New Galaxy Club monthly). Recurring billing via `sg tokoRecurringBillingJob` daily 05:00 SGT. Supported on 3PD via virtual F-code or physical card patterns. Long Term Financing EPP requires CE SC+ on all sellable SKUs mimicking B2C.

## Payment
- Adyen (cards, 3DS2, Samsung Pay) and 2C2P (PayNow, instalment, GrabPay, Atome). Manual refund follow-up with a 2C2P refund-status cronjob; gateway and Hybris states can diverge. Triage must go beyond the storefront symptom.

## Delivery
- Home delivery modes AM/PM/EV; BOPIS with `sg o2o pickup new`. Ghost/Z-code products (shipping notices, freebies, 3PD climate voucher lines) still need valid delivery modes.

## EPP / SMB
- EPP site codes follow `sg_` naming; Long Term Financing EPP rules: CE-only SKUs provided by SESP, no login type, all B2C delivery modes and services on; AEM side: no GNB, footer required, no homepage/general offer pages; code changes only by the RHQ D2C Platform team.

## 3PD
- Shopee, Lazada, TikTok Shop, Qoo10 (Intrepid / Logicbroker patterns). Climate voucher orders use Z-climate SKUs as FOC bundle lines (ratio 100/0), arrive as order type YS02, are manually reconciled with the Singapore government by SESP, and must sit in the same consignment as the main product. Intrepid flagship readiness: load test results, scale-up of at least 6× capacity, two emergency contacts.

## Compliance and risks
- Singpass (fraud), GST reversal, doer/checker/approver split, post-go-live QA, evidence retention in Jira.
- Risks: direct-flow complexity, flagship launches, Singpass/TIPLUS failures, SMB tax setup, 3PD partner readiness, fragmented knowledge.

## Transition
Early deep-dive market. Five workstreams: site/owner inventory, Trade-In + Singpass validation, SC+ recurring-billing runbook, payment/tax/posting matrix, flagship and 3PD readiness. Readiness walkthroughs: SMB prescribed-goods promo, Trade-In with Singpass, SC+ subscription, climate voucher 3PD flow, checkout-to-posting validation.

## Reference matrices
Key attributes (incl. WC91, TIPLUS, Singpass, SC+ subscription), payment landscape, specialist capabilities (Trade-In, Trade-Up, Singpass, SC+ bundle/standalone/subscription, BOPIS, SMB GST reversal, climate voucher, Z-code message products). Discovery questions are on the page but not reproduced here.
