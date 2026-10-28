# CoE Meeting Notes – Handover Day 3: Order Remediation (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486075656
Afternoon of 27/10/2026, Teams meeting "Handover days 3 – Tech" (recording ~minutes 3–23). Chair Shamni Krishnan (SDSAP); presenter Aldwin John Gavino ("AJ", CoE tech support, SDSAP) because the delivery-mode PIC (Mohammad Ashhar Mushtaq) was not ready. ~10 BiPlus Tech people attended. Reference page: D2C COE – Order Remediation (02 Operations CoE → 02-3 Tech Team).

## Context
The most common daily issue is **stuck orders**. Order remediation = correcting the status and pushing the order flow end to end, which requires understanding the order process. The Confluence page lists each order-process step (fraudCheck, takePayment, splitOrder, isFullyFulfilled, FI posting to NERP, completion), order and consignment status tables per country, and status-update cronjobs.

## Happy flow and statuses
| Step | Object | Status |
|---|---|---|
| Customer places order | Order | CREATED |
| Internal checks: fraud, cancelled in CS Cockpit?, virtual stock reserved | Order | (in order process) |
| Waiting for payment capture | Order | WAITING_FOR_PAYMENT_CAPTURE |
| FI posting (financial record) Hybris → NERP | Order | WAITING_FOR_SEND_FINANCIAL |
| splitOrder, consignment created | Order / Consignment | ORDER_SPLIT / READY |
| Waiting for consignment | Consignment | WAITING_FOR_CONSIGNMENT |
| SO created and sent to NERP | Consignment | SHIPPING_REQUESTED |
| NERP creates DO and reports back | Consignment | SHIPPING_PREPARATION |
| 1st GI (in transit) | Consignment | SHIPPED |
| 2nd GI / billing | Consignment | COMPLETED |

## Cronjobs
Status-update cronjobs are listed on the page; each country has its own, named with the ISO code (e.g. AU, MY). Only check them when many orders (~100) stop updating, to see whether the job finished or failed.

## Remediating in Backoffice
1. Open the order (Backoffice → Orders), e.g. AU261027-50329517 stuck at WAITING_FOR_SEND_FINANCIAL.
2. Administration tab → Order Process: find the [WAITING] process.
3. Identify the step to re-run via the data dictionary on the page (here `waitForFinancialInitialUpdate`).
4. Open the process task and re-run it; the order moves on (here to ORDER_SPLIT).

Common root causes: third-party API problems (payment, trade-in, service providers) or system glitches.

## Q&A
- Few orders (<10–20): investigate each in the logs (e.g. trade-in ID missing from the payload to the provider), fix, then re-run the step in Order Process. Around 100 orders: check the cronjob. Hundreds: use a **Groovy script** to update statuses.
- The page has a mapping between Hybris order status, consignment status and My Account status.
- The ~27-case "order remediation steps" table is outdated; its tickets belong to another cluster and are not accessible to the current team (only CoE tickets). AJ will consolidate SEAO stuck-order tickets and update the page.

## Next steps
Study the Order Remediation page; practise re-running an Order Process step on staging; get the per-country status cronjob list and remediation Groovy scripts; AJ to update the page; get recordings of delivery mode/service, Direct EA access and GCIC sessions.
