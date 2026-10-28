# ID Market Rules Page – SEIN Indonesia (summary)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486534558 (page ID 2486534558, last modified 2026-10-27, author Thao Bui Phuong)

## Profile
| Item | Value |
|---|---|
| Market / subsidiary | Indonesia – SEIN |
| Jira project | IDME |
| Timezone | WIB, UTC+7 |
| Business model | Indirect; no FI posting in the feature matrix |
| Platform | New Hybris – tighter permissions than legacy markets |
| Language | Bahasa and English (English note required on ticket) |
| Demand pattern | ~50% of requests after 16:00; sharp spikes on the 29th and 30th of each month |

Open verification items: self-service cancellation scope, trade-in/trade-up partner naming and whether trade-up is live, PIN/MAP status, full payment matrix, fraud rule inventory, and rights model for stock-override deletion and Payment Captured handling.

## Contacts
- 3PD business owners: Haikal Arviansyah, Hafizh Alfath.
- Vendor payment escalation (Midtrans): Michael Peopsha, Giovani Thamri – not subsidiary approvers. GoPay SNAP project contacts: Angel, Clair, Sachin (project context only).
- Unconfirmed: trade-up bulk upload owner, payment escalation owner, stock-override governance owner, Knox approvers.

## Price
- Follows RHQ approval; price import from NERP depends on upstream accuracy. SKUs can be deliberately blocked from price import – check before troubleshooting sync.
- Tax change runbook (14 steps): NERP updates price → stop price import cron → shut ID sites with maintenance page (3PD keeps running; samsung.com ID only shows a banner) → impex for new tax/tax row → expire old TaxRow → groovy to associate products → clear temporary orders → rerun price import → enable test site → verify → enable all sites → smoke test → order monitoring.

## Promotion
- Strict Z-code checklist (Samsung free/ghost products: catalog, price, delivery mode, service type Benefits, warehouse, stock import override; RRP required though checkout amount is zero except RNPL and SME installation).
- Preorder uses RTF override: disable GSCM auto-copy, get week/warehouse/override quantity from subsidiary, update forecast stock carefully.
- Trade-up: handover says 10,000–12,000 row scheme uploads are handled by MSA, but feature matrix says trade-up = No – unresolved conflict.
- Z-code flows are not used on 3PD.

## Coupon
- RHQ baseline; no dedicated Indonesia exception page. Voucher fraud cronjobs and RNPL reporting jobs show coupons can create stuck orders.

## Products and content
- Benefit checks are done in Backoffice, not CS Admin. Z-code product type is usually NON SAMSUNG or GHOST_PRODUCT (documented for Z-code only). Sales status PURCHASABLE_NON_VISIBLE.
- PIN/MAP evolved over time (handover says no longer required; Z-code checklist still references MAP) – do not remove from runbooks without validation.
- Feature matrix shows SC+ bundle, standalone and subscription.

## AEM / Shop App / add-on
- AEM sync cronjobs for eStore, EPP and SMB navigation/footer. Shop App was in GoPay SNAP testing scope (D2C, EPP, Shop App; SMB no). No authoritative add-on runbook exists – needs confirmation.

## Delivery, warehouse, stock
- Delivery modes: standard, same day, next day, O2O pickup. Warehouses: MX WC27/WC28, CE WC31/WC33/WC51, 3PD WC26 (MX) / WC33 (CE); VIP sites use WC27 for MX.
- Stock override is a key risk: blocked stock needs override; deleting override to resync with NERP needs special permission.
- Trade-in partner naming conflict: feature matrix says NBS with LAKU6 and ENB; KB describes Laku6 via an EzTrade layer between Hybris and the vendor.

## Channels
- Very broad multistore inventory: public eStore `vc`, O2O `sein_o2o`, core EPP (`epp`, `friendandfamily`, `samsung_alumni`), staff/VIP, a large bank EPP/affiliate group (BCA, BNI, BRI, Mandiri, etc.), CDM/event programs, partner sites, SMB (`idsme`, `smb_biz`), marketplace (`idlazada`, `idshopee`, `idtokopedia`), `id_members`. Exact site ID is mandatory in every request.

## Payment and fraud
- Midtrans is the core gateway; SNAP (Bank Indonesia) governs Bank Transfer and GoPay API integration. Other methods: ShopeePay, Kredivo, Indodana, Home Credit; PayPal listed in training material.
- Recurring Payment Captured aging tickets need a dedicated playbook. Six MSA fraud rules plus voucher-fraud cronjobs.

## Risks and transition
Permission sensitivity, late-day load, month-end burst, payment incidents, stock override/resync, trade-in/trade-up ambiguity, PIN/MAP uncertainty, multistore targeting. Needs a senior Bahasa-capable Market Owner, strong backup, Tech strong in payment/cronjobs/New Hybris permissions/stock override, and multichannel QA. Checklist: contact matrix, cancellation scope, active-site inventory, payment matrix (SNAP/BNPL), stock override playbook, trade-in/up terminology, PIN/MAP status, evening/month-end roster.

## Reference matrices
EPP/multistore site-group matrix; Z-code and delivery-mode matrix per catalog (ID Estore, idEpp, ID SME, ID 3PD – one SME CE mode is spelled `iid-delivery-standard-ce`, possibly a typo); warehouse matrix; ~21-row cronjob matrix (stock import every 30 min, payment-gateway check every 10 min, Midtrans BT status hourly, price import daily, fraud checks, EzTrade imports, SC+ recurring billing every 2 h, AEM syncs); payment-mode matrix; the 14-step tax-change runbook. Discovery questions are on the page but not reproduced here.
