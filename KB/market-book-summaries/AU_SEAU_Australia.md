# AU Market Rules Page – SEAU Australia (summary)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486534626 (page ID 2486534626, last modified 2026-10-28, author Thao Bui Phuong)

## Profile
| Item | Value |
|---|---|
| Market / subsidiary | Australia – SEAU (newly moved to CoE SEAO) |
| Jira project | AUME |
| Timezone | AEDT UTC+11 (summer) / AEST UTC+10 – ahead of Vietnam, early-shift dependent |
| Business model | Direct; FI posting including second FI posting |
| Volume | ~150 requests/month; ~25% arrive before 08:00 Vietnam time |
| Signals | 22 Tech aging tickets (12/2025); 27 3PD tickets in 2026 |
| Platform | Hybris + AEM, highly site/catalog-scoped configuration |

Open validation items: payment matrix details, vendor ownership, 3PD ownership and integration route, cluster placement, and statements inherited from KT materials.

## Contacts
- NERP: Cindy (FI posting and SC Plus SME), Niraj (Hybris PIC, process staging orders), Yoon Hee (1st escalation), Ryan Kim (2nd escalation); copy `nerp.seau@samsung.com` on all emails.
- Ika Swatika – AEM maintenance PIC.
- 3PD owner to confirm: Daniel Pollitt vs Joseph Chen.
- Many vendor contacts masked or "to be provided by Rudi / Daniel": payment, order, O2O, Asurion (trade-in), MSA/TPG (SIM), rewards.

## Communication
- Jira primary; email for vendors/NERP/escalations; separate RHQ channel; meetings for KT. Define a named route for each recurring category: NERP posting, payment failures, CommBank Yello EPP incidents, SIM plan, trade-in journey, parcel locker, 3PD.

## Price
- Only Special price is used (no discount row). RRP syncs from NERP, except TV SKU RRP which is set manually. Always-on price = Special price without validity; hot-sale = Special price with validity, auto-reverting to always-on. RRP includes tax. Service SKUs may need manual handling.
- Validate source, approval, staging/online alignment, front-end price, and downstream behaviour (financing, trade-in, bundles). Check basket/checkout, not just PDP.

## Promotion and coupon
- Patterns: overtrade, CRP, Multi Buy, ShopApp/EPP first purchase, PPX, evoucher, bundle, GWP, delivery-fee discount, SC Plus discount (CE), voucher discount.
- Priority: product level → trade-in → CRP & PPX → site level. Multiple vouchers are allowed in one order, so build multi-voucher test cases.
- CommBank Yello (CBA) uses a hybrid base-offer + bonus-points model, one bonus promotion at a time.
- Build a reusable coupon test library (single/multiple voucher, excluded SKU/site/payment, voucher + trade-in).

## Product rules
- Four catalogs: B2C, EPP, SMB, 3PD; mappings are set at child catalog then synced online. Reference types: ACCESSORIES, AVAILABLE_SERVICE, MUST_PURCHASE_WITH, CONSISTS_OF, DELIVER_TOGETHER. Benefits still use HTML code; stock syncs from NERP.
- AEM readiness is separate from Hybris sellability readiness; CommBank Yello needs a new Hybris API exposing points/offers to AEM for PLP/PDP.

## Service products
- SC Plus (AVAILABLE_SERVICE + pack code), Extended Warranty, New Galaxy Club, SIM Plan, Knox Manage, trade-in, trade-up.
- SIM Plan: base `AU_SIM_<PROVIDER>_BASE`, variant `AU_SIM_<PROVIDER>_SKU` (e.g. Vodafone); supercategory `sim_plan`, manufacturer NG_PROVIDER, variant EXTERNAL_SERVICE with PDP_NOT_AVAILABLE and blocked price/stock import; Tariff Plan Mappings in Product Cockpit.
- Knox Manage: models SM AU KM1Y/2Y/3Y in category `knox_manage`; external service type KNOX_MANAGE; manual identifier; Manufacturer AID from NERP; Force in Stock; variant PURCHASEABLE_NOT_VISIBLE; AVAILABLE_SERVICE with Preselected true.
- New Galaxy Club: SC Plus flavour (upgrade offer after 12 months); NGC true in Payment Provider Parameters, External Service Type Insurance on main device, base store config `AddedServiceConfigs INSURANCE` and `isClubSCPlus true`; hide with `GALAXYCLUBSERVICE` in excluded types.

## Delivery
- Four warehouses by area, NERP stock sync every 15 or 30 min (to confirm), new CE delivery modes need Toko property updates, MX must be added to Australia Post for relevant flows.
- Parcel Locker: delivery mode `au-parcel-locker-delivery`, enabled by `toko.parcel.locker.enabled.au`, eligibility strategy `tokoLockerDeliveryModeEligibilityStrategy`; MX only, max one MX item, CE not eligible; uses provider `AUSPOST_PARCEL_LOCKER`, OAuth token (`getAuspostLockerToken`), Google address suggestion limited to AU.

## Payment
- Credit Card (Visa/MC/Amex, saved card, 3DS V2, BIN lock), Samsung Pay, Google Pay, AliPay (WeChat Pay not enabled), Samsung Finance by Glow (12/24 months above $250; 36 months above $1666.67), Latitude (thresholds $300/600/900/1200 for 12/24/36/48 months), AfterPay (up to $4000, via Adyen), PayPal (Pay Now / Pay in 4 via Adyen), TreviPay (selected EPP/SMB), Dummy Payment (redemption, 0.00 only), Marketplace Payment Mode (3PD, e.g. eBay, MyDeals).
- Rules: cart minimum 5 cents; trade-in value must not exceed main SKU value; the payment matrix is flagged as pending AU team confirmation.

## Channels
- EPP: 50+ active sites, 30+ being updated; CommBank Yello with external SSO (CBASSO), app-only mobile web, dynamic pricing, CBA payment restrictions, cooling-off period for redemption API, quota controls.
- SMB: commercially distinct; TreviPay. O2O: ownership incomplete. 3PD: marketplace route inconsistent across sources (eBay, MyDeal, Woolworths, Logicbroker) – validate.

## Risks and transition
Risks: EPP complexity, payment diversity, service-product complexity, early-shift demand, FI sensitivity, 3PD ambiguity, payment matrix uncertainty, Tech backlog, unverified SMA cluster statement, "no clawback" statement needs validation. Transition steps: validate contacts, complete site inventory, confirm payment matrix, mandatory product checklist, runbooks (SIM, Knox Manage, NGC, trade-in/overtrade, trade-up, CommBank Yello), issue routing matrix, review aging/3PD tickets, tune early-shift model during hypercare.

## Reference matrices
Operational profile, payment thresholds and modes, and service/setup references (MX trade-in with T codes and T ASURION TRADEIN; overtrade bulk-upload fields OfferID, VariantSKU, VariantReturnSKU, SamsungDiscount, StartDate, EndDate, CMSSite; CE trade-up baseline WM 100, VC 50, REF 150, TV 50, Monitor 50). Discovery questions are on the page but not reproduced here.
