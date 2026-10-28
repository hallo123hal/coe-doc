# CoE Meeting Notes – Handover Day 3: Promotion Rule and Pre-order (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2485649721
Part 2 of the Day 3 morning session (about minutes 34–69), continuing [04 Knox Approval](04_Handover_Day3_Knox_Approval_2026.10.27.md). Presenter Chong Haw Eong (SDSAP); BiPlus CoE VN team in the room/Teams (~20–23 people). Recording is 35 min, screen only (no audio transcription, no captions).

## 1. Knox approval for Promotion Rules (continued)
- **Approval path (SG demo, SPHME-11921 Aircon SC+ Addon 5%):** paths by product group `SG_MX_DIVISIONCONFIG`, `SG_VD_DIVISIONCONFIG`, `SG_DA_DIVISIONCONFIG`, `SG_MX_DM_DIVISIONCONFIG`; approvers shown are requester, Business PIC (consent), Online Head (approval) and several Online Heads (notification). Demo cancelled, nothing submitted.
- **Publish notes (step 2):** campaign-duration rules don't show Period in the approval; rules with qualifying categories list every SKU in the category; bulk publish is possible and the path follows the rule with the highest discount; publishing in preview-promotion-module needs no Knox approval; bulk publish shows only summary information (no SKU/condition/action detail).
- **Step 4:** OK creates the Knox approval along the preset path (follows subsidiary org structure; deeper discount = longer path; highest discount in the submission decides). New: with several Business PICs in a bulk publish, **all** must approve and one rejection rejects everything.
- **Statuses:** UNPUBLISHED → KNOXPENDINGAPPROVAL (withdrawing returns it to UNPUBLISHED) → KNOXAPPROVED (`knoxPromotionStatusJob`) → PUBLISHED (`knoxPromotionPublishingJob`), then QA verification. A rejection gives KNOXREJECTED; editing a KNOXREJECTED rule creates a new UNPUBLISHED rule.
- **Step 9 – which actions need Knox approval:** discount actions do (cart discounts % / fixed; product discounts incl. RRP-based, fixed, target fixed price, distributed discount, quantity-based %, target bundle price; partner-product discounts; delivery-mode discounts; Rewards Boost Discount). Non-discount actions don't (add action type on target products, choose free gifts and the free-gift variants, quantity-based free gift, send abandoned-cart or external vouchers, trigger rule/promotional messages for payment mode/product/cart threshold/category, halt rule execution). They must be published separately: a mixed bulk publish errors with "Discount Promotion and Non-Discount Promotion are mixed".
- **Step 10 – edit edge cases:** V0 in approval, V1 saved and rejected → V0 stays pending, V1 KNOXREJECTED; when V0 is approved and the cronjob runs, V0 is published and V1 becomes INACTIVE (publishing V1 fails with "Promotion status is not approved"). If V2 and V3 (both amended versions) are KNOXAPPROVED when the cronjob runs, **the cronjob fails and both become INACTIVE** – never leave two versions of the same rule approved at once.

## 2. Submitted approvals in Knox Portal
Approval → Submission lists your own approvals. Real VN example: `[Max 15.38% Discount rate/eStore/Promotion] VNME-29960 [SAVINA] Revise AV Voucher Livestream` – Draft (e-Commerce CoE Part submitter) → Consent (SAVINA D2C Sales, with master approval attached) → Notification to D2C Sales Head of Part and e-Commerce CoE Part members.

## 3. Pre-order setup and RTF Override (PICs Chong Haw Eong, Saidatul Humairah Binti Abdul Razak; doc: ID RTF Override)
- Example SKU SM-S938BAKBXSP (Galaxy S25 Ultra) in SG Estore Product Catalog: Staged.
- **Pre-order Settings tab (Backoffice → Catalog → Products):** Is Pre-Order; site-level pre-order date range/shipment last day/delivery date; Pre-Order Date Range (e.g. 26/12/2024–13/02/2025); Pre-order Delivery Date to Storefront (14/02/2025); Pre-Order Transfer To Warehouse Date; Initial Pre-order Start/End Week (e.g. 202504/202507); Pre-order Overselling Start/End Week; Pre Reserve Coupon Max Total Redemptions.
- **Per-warehouse stock fields (e.g. WC91):** Initial Pre-order Quantity, Initial Preorder Max Limit, Forecasted Stocks, RTF Backorder Week, Backorder Counter, Treat Negative Stock Level as Zero, Normal Order Counter, Safety Stock, Promo Stock Available/Reserved.
- **Pre-Order Setup-2026.pptx (12 slides):** four Hybris configs must be FALSE or GSCM setup is blocked – Block Status Update from ExternalSystem, Is blocked for Stock Import, Is blocked for GSCM Stock Import, Block Updates from External Systems.
  - Set up: Product → SKU → Administration tab → Pre-Order Date Range (start in the past, end in the future). To cancel, clear Pre-Order Date Range and Pre-order Delivery Date to Storefront.
  - Stock: product Stock tab → Find Stock Levels for Product → choose warehouse → edit Pre-Order (items already ordered) and Max Pre-Order (cap); remaining = Max − Pre-Order (e.g. 100 − 10 = 90). Don't change inStockStatus.

## Next steps
Read the whole Promotion Rule Knox KB (steps 9 and 10); avoid two KNOXAPPROVED versions; obtain Pre-Order Setup-2026.pptx and ID RTF Override; check the four stock-block configs; get recordings of the remaining 27/10 sessions.
