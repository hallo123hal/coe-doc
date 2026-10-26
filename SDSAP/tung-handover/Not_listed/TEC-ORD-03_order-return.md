# TEC-ORD-03 - Order return

> Part C #8 (with TEC-ORD-02) | Tier 1 #23 | Must | Sprint 4 | ~23 tickets/month | Tier 1 owner: Minh, Quý | Part C PIC: Tung

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483631394  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

## Session
Same item as TEC-ORD-02: Part C #8 *Order cancellation and return*, **asked inside topic 22 *Order processes E2E*** (Tue 27 Oct 10:30, Room B; SDSAP PIC Aldwin John Gavino; link *D2C COE - Order Remediation*; verdict Clarify). See [TEC-ORD-02_order-cancellation.md](TEC-ORD-02_order-cancellation.md) for the session table.

## Focus
- The KB has **no page for the return steps** themselves. The V3 reset sequence comes from *D2C COE - Order Remediation* case 3 ("Cancel Return Request"), which is not among the pages mapped to this service - get SDSAP to show it live and say where it is documented.
- Ask which job times out/cancels returns (`<cc>-tokoReturnsProcessCheckStatusJob`?), how an order is restored to COMPLETED after a reset (not in the KB), the per-market return policy (window, type, exclusions), and the return action HOLD vs IMMEDIATE per market.
- Ask about the recurring **TH** "unable to create return" list and how SDSAP gets the NERP-side confirmation that RSO/RDO are deleted.

## What the service does
A return is created or unblocked in Hybris for a delivered or in-transit order, accepted by NERP, and followed until the refund triggers at the gateway or is handed to finance. A wrong one refunds goods that never came back or posts a wrong credit note.

## Key facts
| Item | Detail |
|---|---|
| Volume | 204 tickets in 2026, ~23/month, 7 markets (TH, SG, AU, NZ, VN lead) |
| Roles | Tech order desk (Thai-speaking engineer in the TH pod). L1 doer; L2 for NERP rejections, self-cancelling returns, in-transit returns, any script. Checker: after execution for all, **before** execution for V3 and any status reset. Approver: requester's written instruction within market policy; subsidiary approval for out-of-policy returns; RHQ via PC |
| SLA | P3: 40h, 2h response; internal 26h / 78 min. P2 (16h): refunds blocked >5 working days, or >10 returns blocked in one market |
| Change class | Repeat-use runbook; every create/reset/process action is a production data change with approved PC + second pair of eyes. A return request can be cancelled before receipt; **a sent refund cannot be reversed** |
| Biggest risk | Refund sent without goods back; duplicate refund; wrong credit note |

## Rules to remember
- **Never push a refund before the goods are received** unless market policy allows IMMEDIATE. A normal return refunds on NERP goods receipt; refund after receipt is a scheduled check, not a reason to keep the ticket open.
- A return outside the market policy needs written subsidiary approval first.
- Order not yet dispatched -> TEC-ORD-02. Replacement order -> TEC-ORD-04 (its return leg stays here). Credit-note document -> TEC-ORD-07.

## Variants
V2 return cannot be created (~63% of titles, TH/SG) - V3 reset after a failed return (batch, TH) - V1 create return for a delivered order - V4 refund missing/wrong (AU compensation refund) - V5 return stuck or cancelling itself (SG, NZ) - V6 in-transit/failed-delivery return (VN) - V7 return data wrong in NERP/FI.

## Workflow
1. ASSIGNED; template A. Per order: full/partial + lines, reason, return type, refund value if not full, masked error screenshot, RMA. Gaps -> one clarification.
2. **Three-system before state:** Hybris (OrderStatus, ReturnRequest/ReturnEntry status WAIT/RECEIVING/RECEIVED/COMPLETED/CANCELLING/CANCELED, payment entries) - NERP (SO/DO/billing, existing return order, FI) - gateway (captured, payment mode, disputes, earlier refunds).
3. **V1 create:** after PC approval create the return in CS Cockpit (entries, quantities, RefundReason, returnType, refund value, delivery fee per instruction, HOLD/IMMEDIATE). RMA generated; order -> RETURN_REQUESTED. Confirm the NERP return order (RDO, `externalReturnRequestId`); set the refund follow-up date to the expected receipt date; Launch Verification once it exists in both systems. Z-code gift returns with its main item unless waived; warranty/SC+ with the device; bundles together; FOC/Parent Entry Number errors per Order Remediation cases 1, 15, 24.
4. **V2 diagnose in this order** (confirm one cause before changing anything): old request still linked (CANCELLING/CANCELED) -> V3 - order not fully completed - "entries from different consignments" (return per main product with its FOC) - "Return Order cannot be created! (Wrong Ref.Billing or Available return quantity is zero)" (already exists; fix in NERP) - NERP rejects (item category not defined -> NERP team/TEC-SIT-03) - feature unavailable in market (partial return disabled for ph, sg, th, vn cash vouchers) - self-service defect (TEC-TSP-05) - action errors (TEC-TSP-01).
5. **V3 reset (batch):** validate statuses -> **checker pre-check: no goods receipt and no refund on any old request** (else V4/V7) -> subsidiary NERP user confirms RSO and RDO deleted -> Backoffice: clear Return Delivery Order Nr and ERP Doc No, Return Status = WAIT -> CS agent Cancel Request, trigger `isReturnRequestCancelling2` on process `return-refund-process-v8-33` -> restore the order to COMPLETED (approved action not in KB: TEC-ORD-05 with Sub-Lead review) -> hand back before/after table -> link COE-PRB-01 for the recurring cause.
6. **V4 refund:** goods not received -> refund not due. `REFUND_FOLLOW_ON` ACCEPTED -> give requestId, don't re-trigger. REJECTED/ERROR -> read `transactionStatusDetails`; dispute -> subsidiary + gateway; else TEC-TSP-04. No refund entry after receipt -> L2 re-triggers **once** (`isReturnComplete`, `sendRefundNotification`; PC required). Over-refund -> COE-INC-02 + finance.

Stuck patterns (V5): WAIT at `returnRewardOption` (`shouldInvokeWarehouseReturnV2`); stuck CANCELLING (`Isreturnrequestcancellingv2`); `CancelExternalServices` failed (`IsRefundhandledInSubprocess`). Same symptom 3 times a month -> COE-PRB-01.

## Known errors
"Unable to create return" (KE-01) - return cancels by itself (KE-02) - NERP item category not defined (KE-03) - blocked on upgrade programme entries (KE-04) - partial refund rejected: dispute (KE-05) - self-service return will not submit (KE-06) - refund action inactive for a delivery mode (KE-07) - partial in-transit return in NERP not Hybris (KE-08) - wrong receipt date/credit note (KE-09) - return with FOC fails (KE-10) - return order cannot be created (KE-11).

## QA checklist
Instruction complete/within policy; pre-execution check for V3 and resets; PC approved first; RMA lines/quantities and refund value correct; linked lines handled; NERP return order accepted; no refund before receipt; no duplicate refund; old requests CANCELED without refund (V3); follow-up date set; no customer data.

## Samsung KB
KB - Common Error returned from Nerp (2477687754, read first) - Updated Bulk Store EPP (2477621961) - 0) 3PD end to end flows Hybris-Logicbroker (2477359346) - eBay Integration (2477359425) - KB - [AU] MX Trade-In (2478114822) - KB - [AU] Warehouse (2477328066) - KB - Order remediation process (2478113729) - KB - Kibana log (2477721036) - KB - Authorization Holds (2477327239) - Refund Reward Points (2477983349). Ask the Sub-Lead where to read Order Remediation case 3 before your first V3.
