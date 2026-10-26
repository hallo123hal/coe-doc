# TEC-ORD-07 - Invoice and e-invoice generation and correction

> Part C #7 | Tier 1 #14 | Must | Sprint 3 | ~56 tickets/month | Tier 1 owner: Minh, Quý | Part C PIC: Tung

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483729047  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## Session
| Field | Value |
|---|---|
| Part C item | #7 Invoice and e-invoice generation and correction |
| Call plan | **Asked inside topic 56 (Thu 29 Oct 11:20, Room B)** |
| Topic 56 | *FI Posting* - SDSAP PIC Mohammad Ashhar Mushtaq; pages: Create NERP FI NERP Config; Push Orders to Cancelled with FI Posting; KB - RNPL FI Posting; verdict Reuse |
| Maps to | TEC-SIT-04 FI configuration; TEC-ORD-02 Order cancellation; TEC-ORD-07 |
| Sheet note | "Cover it inside FI posting." Question for SDSAP: include invoice and e-invoice generation and correction |

## Focus
- The KB has only 2 core pages (Tax Invoice Generation script; SG SMB GST order remediation) and **nothing on the daily MY batch** or the MY e-invoice flow - use topic 56 to get it from SDSAP.
- Ask who submits an e-invoice (Hybris, NERP or provider), what comes back (validation link/QR), and the role of the MY revalidation jobs (`my-tokoB2BITaxInvoiceRevalidation*`).
- Ask whether Completed triggers invoice generation in production (on staging Completed alone does not populate `invoiceNo`), the approved push/generate action or Impex template, and the batch limit (the pack assumes 50 orders/run).
- Ask whether a standing PC pattern for routine MY batches exists (open RHQ proposal) and where the NERP billing check is read.

## What the service does
The requester gets a valid invoice, e-invoice, credit note or e-receipt for an order, and delivered orders reach **Completed with their invoice**. A wrong push gives an invalid tax document, fires completion events (emails, Rewards points, SC+ activation) too early, or unbalances NERP FI.

## Key facts
| Item | Detail |
|---|---|
| Volume | 507 tickets in 2026, ~56/month, 8 markets (mostly **MY**) |
| Roles | Tech L1/L2 (GMT+8 order pod): L1 runs V1-V3, L2 runs V4-V6. Checker: peer. Approvers: subsidiary (delivery + data, in writing), finance (tax content/reversals), PC approver |
| SLA | P3: 40h resolution, 2h response (NEW -> ASSIGNED); internal 26h / 78 min. P2 (16h) only with a dated legal/finance deadline or dated customer escalation. P1/P0 if wrong documents reach many customers or expose personal data (COE-INC-01) |
| Change class | **Normal**: every production push, regeneration or FI re-send needs an approved PC ticket, one per batch ticket |
| Biggest risk | Invalid tax document; double FI posting; completion events for an undelivered order; identity data left in ticket text |
| Arrives as | Jira COEC (Order > Invoice Generation) with an order table (code, status, target status, delivery/pickup date, invoice action, SC+ Y/N); e.g. "Generate Invoices and push orders to Completed", "Modify invoice details", "Push order to COMPLETED (E-Invoice)", "[TSE] Request sent FI posting" |

## Variants
V1 generate invoice + push delivered orders to Completed (~57%, mostly MY) - V3 modify invoice details and regenerate (~28%) - V2 Completed with e-invoice (customer gave a tax ID, ~4%; if a tax ID is given it is V2 even if the title says V1) - V4 missing/wrong tax invoice, credit note, e-receipt - V5 FI posting missing/wrong/re-send - V6 invoice content or tax logic change (finance sign-off; defects via TEC-OWN-01 to Samsung L3, new needs via TEC-ADH-02).

**Not this service:** push to Cancelled / Pickup Complete / undelivered / no NERP billing -> TEC-ORD-05; cancel -> TEC-ORD-02; return -> TEC-ORD-03; order never reached NERP -> TEC-MON-02; trade-in FI -> TEC-VAS-01; SC+ -> TEC-VAS-02; marketplace FI -> TEC-TSP-02; FI mapping -> TEC-SIT-04.

## Workflow (V1)
1. NEW -> ASSIGNED (initial response); template A. Validate the table: one market, no duplicates, status + **delivery date on every line**, target Completed only. Never push without a delivery date.
2. **Read-only pre-check** per order (Backoffice or HAC): order/consignment status, NERP SO/DO/billing, invoice number field, open return/cancellation, SC+ lines. Orders found must equal lines.
3. **List exceptions** (not found, already invoiced, open return, consignment Cancelled, no NERP billing) - exclude and report, never process silently.
4. Check side effects (completion email, Rewards earn, SC+ activation, survey) and write them in the plan comment. Export the before state.
5. Self-QA, raise the PC ticket -> COEC ON HOLD HQ ("PC ticket pending") until the RHQ approver approves.
6. Push consignments, then orders, to Completed with the approved action/template and PC+COEC header; generate the invoice. Check `invoiceNo`, `taxInvoice` media and `taxInvoiceCreationDate`.
7. Post-check: all Completed with invoice number; open 10% of PDFs (min 2) against the order; SC+ activation verified (error -> TEC-VAS-02).
8. Peer check; hand back with after table + exceptions (template C).

- **V2:** set `Address.isUserWantTaxInvoice` + tax fields (`companyTaxNumber`, `personalTaxNumber`, `tinICPassport`, `taxBranch`, `invoiceType`) on the order's billing address; on rejection correct with the requester and resubmit **once**.
- **V3:** if an e-invoice is validated or the invoice already went to finance - **STOP**; finance decides in writing (credit note vs new invoice vs cancellation). Never blank a mandatory field. Re-send to NERP if NERP carries the field (V5).
- **V5:** no second FI posting before a **written reversal** by finance/NERP FI; never re-send twice.

## Protected data
Names, tax IDs, TIN, addresses and phones belong only in the Jira protected field / restricted attachment. If typed in the description, ask the requester to move them and never repeat them.

## Known errors
Completed but no invoice number (KE-01) - order returns to Shipped (feed still active, KE-02) - billing field empty after edit (KE-03) - unclear ID field (ask once with screenshot, KE-04) - e-invoice rejected (format/provider outage, KE-05) - completion fails on SC+ (KE-06) - duplicate delivery lines with SC+ / wrong card details (template logic -> L3, KE-07/08) - cannot regenerate old order (KE-09) - marketplace return lacks FI posting (TEC-TSP-02, KE-10).

## QA checklist
Variant right and route-outs linked; delivery date on every line; pre-check counts recorded; exceptions listed; before export attached; side effects noted; orders and consignments Completed; invoice number on every order; sample PDFs match; e-invoice reference (V2); V3 values equal protected field; FI confirmed and reversal before re-send (V5); no personal data outside protected field.

## Samsung KB
Tax Invoice Generation (2477524723) - [SG] Order remediation for SMB GST-free orders (2477196237) - KB - SME Cronjobs (2478081513) - [SEIN] Order Remediation (2477557510) - KB - Order remediation process status dictionary (2478113729). The MY e-invoice flow is not in the KB.

## Access note
Production rights are granted **by wave from 29 Oct 2026**; ImpEx/Groovy on production needs an approved PC and the approved template.

## Open points ("confirm in KT")
Run-size limit (50) - whether Completed triggers invoice generation - approved push/generate action - protected-field location - who submits MY e-invoices - role of revalidation jobs - `gerpFIStatus` enum - standing PC for routine MY batches.
