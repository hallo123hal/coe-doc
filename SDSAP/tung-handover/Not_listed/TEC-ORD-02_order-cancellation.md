# TEC-ORD-02 - Order cancellation

> Part C #8 (with TEC-ORD-03) | Tier 1 #21 | Must | Sprint 4 | ~26 tickets/month | Tier 1 owner: Minh, Quý | Part C PIC: Tung

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483728928  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## Session
| Field | Value |
|---|---|
| Part C item | #8 Order cancellation and return |
| Call plan | **Asked inside topic 22 (Tue 27 Oct 10:30, Room B)** |
| Topic 22 | *Order processes E2E* - category Fulfillment, SDSAP PIC Aldwin John Gavino; link *D2C COE - Order Remediation*; priority Tier 1, Sprint 3, Must; verdict **Clarify** |
| Maps to | TEC-ORD-05, TEC-MON-02, TEC-ORD-01, TEC-ORD-02, TEC-ORD-03 |
| Why Clarify | The link is Order Remediation only, not the end-to-end flow |
| Questions (sheet) | Include the order flow from Hybris to NERP with statuses, stuck orders, cancellation and return |

## Focus
- Get the Hybris -> NERP flow with statuses end to end; the Samsung KB has only two cancellation pages (both Level 2 scripts) and no page for the CS-agent cancel steps.
- Ask: the exact CS Cockpit cancel button/path, which markets refund automatically vs manually (ID, SG, MY manual), how the three-system check (Hybris / NERP / gateway) is done in practice, and how NERP is read (Kibana, interface log, NERP user).
- Ask about the `toko.enable.cancel.order.after.do.my` rule, the market age threshold, the bulk-store parent/child split rule, and whether the "ORDER_SPLIT + WAITING_FOR_TRANSFER" status trick (KB case 18) is allowed for Level 2.

## What the service does
Full or partial order cancellation done in Hybris when the CS agent view cannot do it, confirmed in NERP and at the payment gateway, or handed to finance as a manual refund. **A cancellation cannot be undone**; a missing or duplicate refund means complaints and financial loss.

## Key facts
| Item | Detail |
|---|---|
| Volume | 231 tickets in 2026, ~26/month, 8 markets |
| Roles | Tech order desk (VN hours + AU/NZ morning). L1 doer; L2 for partial, fraud batch, blocked cancellations, any ImpEx/Groovy. Checker: another certified engineer - before execution for V2, V4 and batches >5 orders, after execution for all |
| SLA | P3: 40h, 2h response (NEW -> ASSIGNED); internal 26h / 78 min. P2 (16h): goods must be stopped before dispatch today, or a promised refund is blocked >5 working days. Fraud waves with revenue loss -> COE-INC-01 |
| Change class | Repeat-use runbook; every cancel is a production data change with an **approved PC ticket** and a second set of eyes; one PC per COEC may list many orders; fraud batch >20 orders: inform Sub-Lead |
| Biggest risk | Wrong order cancelled (no rollback); missing or duplicate refund |

## Variants
V1 full cancellation before dispatch (~29%) - V5 blocked cancellation (~9%) - V6 cancelled but refund/NERP update missing (~5%) - V2 partial (line) - V3 linked lines (Z-code gift, SC+/warranty plan, F-code bundle) - V4 fraud/risk batch (VN) - V7 cancellation without refund (unpaid/temporary/test/duplicate).

**Not this service:** goods already dispatched (DO or billing exists) -> TEC-ORD-03; exchange -> TEC-ORD-04; other status corrections -> TEC-ORD-05; stuck order -> TEC-MON-02; gateway fault -> TEC-TSP-04; points -> TEC-REW-02; credit note -> TEC-ORD-07.

## Workflow (V1)
1. NEW -> ASSIGNED; template A. Each order needs: full/partial + lines, refund Y/N, **CancelReason** (one global enum, 35 values), "goods not dispatched". Gaps -> one clarification (template B). Keep order numbers only; no customer data.
2. **Dispatch check:** a DO or billing number, or status SHIPPING_PREPARATION or later = stop -> TEC-ORD-03 (unless the subsidiary confirms in writing that goods are held, V5).
3. **Three-system before state:** Hybris (OrderStatus/ConsignmentStatus, order process state, payment entries, vouchers/points/linked lines) - NERP (`gerpSalesOrderNr`, `gerpDeliveryOrderNr`, `gerpBillingNr`, `gerpFIStatus`) - gateway (captured vs authorised, open dispute).
4. Checker confirms the list; create the **PC ticket**; COEC ON HOLD HQ until RHQ approves. **Nothing is cancelled before approval.**
5. Cancel via the CS agent action on all entries with CancelReason and refund option, COEC number in the comment. Status -> CANCELLING -> CANCELLED; consignment CANCELLED.
6. **Refund proof:** `REFUND_FOLLOW_ON` entry, `transactionStatus` ACCEPTED, amount = paid, requestId (or CANCEL/VOID for an uncaptured authorisation). Manual refund (template D) for COD, bank transfer, instalment, finance provider, and ID/SG/MY.
7. NERP: cancellation message success; SO cancelled/rejected (or re-created for remaining lines); FI revert if the payment was posted.
8. Check linked services (points, trade-in, SC+, invoice); send to the checker with the after table (QA REVIEW / WAITING QA).

Refund method by market: ID and SG manual; MY offline via CS; NZ, TH, PH from Hybris; VN automatic and manual.

- **V2 partial:** compute the net paid line value (after discount/voucher/points); agree the NERP sequence (subsidiary NERP user deletes the old SO first where the market re-creates it); config `product.cancel.enabled.<cc>`, `toko.disable.partial.cancel.cash.voucher.<cc>`.
- **V3 linked lines:** Z-code gift cancels with its main item; SC+/warranty with the device; virtual bundle components together.
- **V5 blocker order:** shipped status but no DO -> TEC-ORD-05; stuck SHIPPED without in-transit return -> choose return or cancel + manual refund; cancel button off -> KB case 18 status trick under PC (confirm L2 may use it); fraud-review state -> L2; pending NERP step (TH) -> NERP user.

## Rollback
None once cancelled or refunded: stop further refunds, inform Sub-Lead + requester, the customer re-orders through the subsidiary, **COE-INC-02**. Reversal of a refund only via finance + gateway.

## Known errors
Cancel button disabled (KE-01) - cancelled but no refund entry (KE-02) - refund rejected: dispute/expired authorisation (KE-03) - will not cancel after fraud rejection (KE-04) - no auto refund for partially cancelled plan line (KE-05) - remaining lines not sent after partial cancel (KE-06) - shipped order cancelled, no refund (KE-07) - **duplicate refund** from re-trigger while first is pending (KE-08) - order stuck ORDER_SPLIT after cancel (`isFullyFulfilled`, KE-09).

## QA checklist
Instruction complete; pre-execution check (V2, V4, >5 orders); PC approved before execution; no order dispatched; Hybris cancelled for all; refund accepted, amount right, no duplicate; manual refund hand-off; SO cancelled/rejected/re-created; FI revert; linked lines consistent; no customer data.

## Samsung KB
Cancel order without refund (2478081657) and Script to cancel order (2477983370) - Level 2 scripts under PC. KB - Internal Fraud Rule setup (2477949629), KB - MSA Fraud rules (2477851136), KB - Authorization Holds (2477327239), Updated Bulk Store EPP (2477621961), KB - Order remediation process (2478113729), KB - Kibana log (2477721036), KB - Common Error returned from Nerp (2477687754), D2C COE - Order Remediation (2478744233, case-based).

## Safety on staging
Never cancel an order you did not place; practise with your own order on a test site.
