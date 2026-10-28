# TH Market Rules Page – TSE Thailand (summary)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486829397 (page ID 2486829397, last modified 2026-10-27, author Thao Bui Phuong)

## Profile
| Item | Value |
|---|---|
| Market / subsidiary | Thailand – TSE |
| Jira project | THAME |
| Timezone | ICT, UTC+7 |
| Business model | Direct; FI posting applies |
| Key pattern | ~35% of requests arrive after 16:00 ICT; Thai-language support needed for day, evening and weekend |
| Complexity | Very high – extreme site fragmentation across eStore, EPP, SMB, O2O, Shop App, 3PD |

Open verification items: Knox approver ownership by division/channel, full payment-mode matrix by site, fraud rule inventory, whether SC+ standalone is live, Shop App vs web parity, and whether historical site inventories are still active.

## Contacts
- Local PIC: Emika (partially known). 3PD business owner: Tippy, Head of Sub Part (Shopee, Makro Pro, KTC, K+ scope to confirm).
- 2C2P escalation (vendor, not subsidiary owners): Cynthia (Technical Account Management, 1st), Lim Yu Feng (Global Support, 2nd).
- Unconfirmed: Knox approvers per division (MX, VD EB, VD TV, HA, AC, SMB), trade-in grading file owner, e-invoice owner, payment escalation owner, SC+ owner.

## Hours and channels
- Songkran (13–15 April) must be treated as a support-roster event. Weekend and evening support are mandatory.
- Jira comments under THAME are the formal channel; Thai content still needs an English summary on the ticket. Email for escalation/vendors; chat never replaces Jira.

## Price
- Knox approval mandatory; paths differ by division (MX vs CE) and SMB (incl. MON/MEM). Knox approval cronjob polls every 45 minutes – do not escalate before the window passes.
- FI posting sensitivity; align with accounting/GCRM/FI cycles. Price/stock sync from N ERP via super sync – escalate source issues instead of local workarounds. RNPL voucher FI treatment raises downstream risk.

## Promotion
- Mandatory rule: split bulk campaign requests into smaller controlled sub-tickets ("one business campaign does not always equal one execution ticket"). TSE is the largest contributor of multi-promotion batches in the region.
- Check site list, channel scope, Knox route, voucher/payment/trade-in/SMB interaction, and record QA evidence per sub-ticket. Trade-up exclusion logic applies.

## Coupon
- RHQ baseline plus local exceptions: RNPL vouchers on SMB sites, cash voucher with separate display, VAT and FI posting, and partial self-service cancellation restrictions.

## Products and content
- Base code is category-sensitive (MX first 5 chars, accessories first 6, CE family-based). English and Thai identifiers required. Super sync: DOTCOM, STOCK, PRICE, IMAGE.
- NON SAMSUNG product type is prohibited (N ERP posting impact) unless an exception is explicitly approved.
- Extended Warranty uses item category YNS5. SC+ subscription is not confirmed live (feature matrix says no; THAME-15524 is TBD).
- Feature matrix: BO return/replace yes; trade-up and multiple trade-in yes; no clawback.

## AEM, Shop App, add-on
- No full AEM inventory. DOTCOM sync failure → check publication first. Shop App codes: `th_genzapp` (education), `epptse` (corporate), `th_ea_one`.
- Add-ons come from AVAILABLE_SERVICE references (T ADDON, T REMOBILE TRADEIN for MX, T TRADEUP for CE) – check catalog reference integrity before blaming the storefront.

## Delivery and trade-in
- Delivery mode families per channel, e.g. `th-delivery-standard-UPC-MX`, `th-delivery-standard-BKK-MX`, `th-o2o-store-pickup`, `th-tradein-o2o(-2)`, `th-delivery-standard-boxdamage`, large CE regional calendar families (AC, AV, HA/REF/WM, small appliance), SMB (`th-smb-b2b*`), 3PD (`th-marketplace-*`).
- Trade-in partner Remobie, manual (not API): subsidiary sends monthly grading files, CoE uploads T SKU configs and maintains prices. Missing T SKU → use brand base SKU (e.g. `T-APPLE-REMOBIE`, `T-SAMSUNG-REMOBIE`) and create variants. 16 base T SKUs are listed (Apple, Huawei, Motorola, OnePlus, Oppo, Samsung, Sony, Vivo, Xiaomi, Realme, Honor, Asus, Nothing, IQOO, HP, Lenovo).
- PINMAP is not a defining dependency; warehouse/lead-time ownership matrix is not documented.

## Channels
- ~190 SMB sites (regional dealer zones, service centers, named dealers) and ~50 EPP/B2B sites; access types: Company Domain, Access Code, Verification Code, Hash Code, O2O Cockpit. Exact site IDs are mandatory in every request.
- 3PD (Shopee/SPX, Makro Pro, KTC, K+; Logicbroker pattern) is one of the heaviest ticket generators.

## Payment and fraud
- KBank, 2C2P (full payment, seamless instalment, 123 bank direct, automated refund), Atome, GrabPay, QR, bank transfer, SC+ tokenized monthly payment. Local e-invoice (Checkout 2.0) is a compliance requirement. MSA fraud rules apply but the exact list is not on the page.

## Risks and transition
Risks: site targeting, bulk tickets, late-day load, manual trade-in upkeep, payment/FI posting, 3PD volume, Thai-language dependency. Not suitable for inexperienced owners: staff a senior, Thai-capable Market Owner, strong Sub Lead, Tech strong in payment/catalog/3PD, and channel-aware QA. Checklist items include contact matrix, Knox paths, authoritative EPP/SMB inventory, payment matrix, monthly trade-in calendar, evening/weekend Thai roster, 3PD playbook, fraud rule inventory.

## Reference matrices and discovery questions
Matrices: EPP/SMB site-group matrix, delivery-mode matrix, T SKU base list, payment-mode matrix. The page ends with 52 discovery questions (general, contacts, hours, price, promotion, coupon, product, delivery, trade-in, EPP, SMB, 3PD, payment, e-invoice, fraud, transition).
