# VN Market Rules Page – SAVINA Vietnam (summary)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486763771 (page ID 2486763771, last modified 2026-10-27, author Thao Bui Phuong)

## Profile
| Item | Value |
|---|---|
| Market / subsidiary | Vietnam – SAVINA |
| Jira project | VNME |
| Timezone | ICT, UTC+7 (same as the Vietnam CoE team) |
| FI posting | Yes (FI due date, RNPL posting, COD per-SO amount enhancements) |
| Working language | Vietnamese or English (English note required on ticket if Vietnamese is used) |
| Peak pattern | Business hours; go-live concentrated in the first week of the month |
| Complexity | Among the most complex SEAO subsidiaries; must be staffed with a senior Market Owner from day 1 |

Open verification items flagged on the page: trade-in target model, overtrade scope, final warehouse codes by channel, SC+ subscription scope, and the Backup Sub Lead definition conflict between MR-03 and MER-HB-01.

## Contacts
- 3PD: Nguyễn Thị Quỳnh Anh, Nguyễn Trung Hiếu, D2C Sales (known).
- Knox price approval: D2C Sales SAVINA at the Consent step; Head of Part and e-Commerce CoE Part members are notified (partially known; named approvers per MX/VD/HA/AC not captured).
- Unconfirmed: Planning Review approver, Review Setup evidence reviewer, warehouse validation owner, O2O store-mapping owner, payment escalation owner (subsidiary vs PG vendor vs Tech).
- Trade-in partner path (TCV) needs review – conflicts with manual rollout / Trade In Plus direction.

## Communication
- Jira comments are the mandatory, formal channel; every action/decision must be on the ticket.
- Email for escalation/vendor; Mattermost (RHQ) or Teams only for fast coordination, never a replacement for Jira evidence.
- Vietnam office has a clean room / large working-group capacity useful for war-room style launches.
- No direct SLA tool: Team VN must build SLA tracking from Jira transition exports.

## Price
- Knox approval is required before live; paths are split by division: `PRICE_SAVINA_MX_DIVISIONCONFIG`, `PRICE_SAVINA_VD`, `PRICE_SAVINA_HA`, `PRICE_SAVINA_AC` (Draft → Consent → Notification).
- Super sync = DOTCOM, STOCK, PRICE. PRICE failure → subsidiary fixes with the NERP team; urgent price bulk upload is allowed as temporary RRP fallback only if approved.
- Prices interact with EPP, O2O, 3PD, bundles, add-on references and FI posting.

## Promotion
- Priority hierarchy (high → low): Package (600) → FOC (600) → Ecobundle (400–500) → product-level voucher (200–300) → cart-level voucher / next-purchase voucher (50–100) → payment promotion (0–30).
- Trigger sequence: single price → package/FOC → direct discount → welcome instant discount → marketing voucher → payment promotion.
- Platform promotions are not allowed after 2025-12-01.
- BMSM setups need separate rules per D2C / EPP / SME, site restrictions, F-code logic, trigger-message limits and anti double-trigger rules.
- Payment promotions need exact payment-mode codes, site list, qualifying SKU/category list and thresholds; stackable with non-payment schemes only.
- Overtrade is conflicting across sources (one note says it does not apply to VN; other sources show VN overtrade report cronjobs) – must be confirmed before writing an SOP.

## Coupon
- RHQ guideline, 4-4-4-4 format; behaviour must be checked against priority sequence and stackability. Voucher analysis often needs Tech and shows up in aging tickets.

## Products and content
- SKU setup flow: bulk upload at lowest category → category/delivery mode/promotion quota → super sync → IMEI for mobiles → variant SKU at master → sync master→child → approval and sales status → product references → sync child→online.
- Sync failure handling: DOTCOM (AEM not published – wait and rerun), STOCK (align on stock import override), PRICE (NERP source).
- Status: regular/F-code = Approved + Purchasable; component = Approved + PDP_NOT_AVAILABLE.
- Product references: Available Service (trade-in), Accessories (add-on), Recommendation/FBT, Bundle, Must Purchase With, Consists Of.
- Samsung Members: Access Code OTP login, strict merchandising-text length and basic-HTML-only rules.
- Catalog notes: `vnEaRetailProductCatalog` (retail migration), `vn_corporate` (merged EPP target).
- SC+ scope unsettled (bundle/standalone documented; subscription needs RHQ confirmation).

## AEM / Shop App / Add-on
- DOTCOM sync failure usually means an AEM publish issue, not a product setup error. Shop App is in scope for some tickets – do not assume parity with web.
- Add-on depends on product references and accessories; Auto MBO has its own KB; aging tickets show "add-on not working + block checkout".

## Delivery, warehouse, services
- Multi-warehouse logic (no forecast stock like other MX markets). `siteToWarehouseMap` overrides site/region config; highest-priority warehouse with stock is chosen.
- Warehouse code conflict unresolved: overview says MX WV05/WV10 with S552, CE WV09 with S551/S552; preferred-warehouse KB says S520 (North: WV05→WV10; South: WV10→WV05).
- Lead time/RDD driven by warehouse, postcode, delivery mode, cut-off, holidays; uploads (LeadTime Master, PostCode2XDock) may need NASCA rights/L2.
- Block-stock-vs-OMS logic for O2O; overselling via Overselling Shipping Date in Stock Level admin.
- O2O site configs (walk-out, preferred warehouse selection, omni stock) often need Tech tickets; IMEI scanner for mobiles.
- Delivery modes include `vn-im-parcel-express`, `vn-o2o-pickup`, `vn-o2o-pickup-both-tradein`, `vn-o2o-Samsung68/SWL-walk-out(-CE)`, `vn-ce-parcel-express(-d2c)`, `vn-dsc-parcel-express`, `vn-marketplace-ce-parcel-express`, ring/sizing-kit modes, `vn-ce-calendar`.
- `vn-pay-at-shop` is controlled by store type (CS_STORE).
- Same Day BOPIS and Express Delivery 4H (prepaid only, district eligibility, cut-off, NERP mapping) exist.
- Trade-in model conflicting: historical TCV integration with cronjobs vs. Manual Trade-in Rollout and Trade In Plus (multi-vendor). PINMAP is not a defining dependency for VN.

## Channels
- EPP: very complex – internal Samsung, banks, dealers; legacy sites merged into `vn_corporate` (Email OTP / Access Code, single sold-to).
- O2O: mission critical and the largest incident generator.
- SMB: active but less documented.
- 3PD: Lazada, Shopee, Tiki, TikTok via Logicbroker middleware; VN CoE manages the Hybris↔middleware data flow, not the marketplace business; 26 3PD tickets in the cited 2026 summary.

## Payment and fraud
- Broadest payment set in the region: OnePay, Cybersource (incl. Samsung Pay), Cybersource instalment (bank × tenure), VNPT, VNPay QR, NAPAS/virtual account, COD, Pay at Shop, FE Credit/BNPL; Payoo appears inactive.
- 10 MSA fraud rules per overview (voucher-heavy orders, marketplace orders, special characters), but the rule list itself is not on the page.

## Risks
Warehouse mapping conflicts, O2O volume, trade-in model ambiguity, payment/FI variants, add-on/checkout blockage, stuck orders and returns, 3PD volume, knowledge scattered across Jira/KB history. Vendor readiness pages exist for TCV, Cybersource, OnePay, VNPT, Vietguys/Zalo.

## Transition implications
Treat as priority market; senior Market Owner, strong backup/Sub Lead, Tech counterpart strong in order flow/stock/O2O/payments, QA comfortable with payment and O2O scenarios. Readiness checklist: contact matrix, Knox approvers per division, channel × warehouse matrix, confirmed trade-in model, active payment matrix with FI notes, `vn_corporate` EPP documentation, issue playbooks (O2O, stuck order, return/refund, voucher, add-on), link to Tech-owned 3PD/cronjob references.

## Reference matrices on the page
Feature/rule matrix with verification needs; a table of ~15 operational cronjobs (stock import every 30 min, order push every 30 min, order status every 25 min, price import every 2 h, trade-in and promotion reports, daily QC/stock reports). The discovery-question table was present on the page but is not reproduced here.
