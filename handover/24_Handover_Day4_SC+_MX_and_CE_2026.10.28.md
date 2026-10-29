# CoE Meeting Notes – Handover Day 4: SC+ MX and CE (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487713853
Sub-pages not yet summarised in this file (personal notes): Trangdtt – SC+ MX (2487943234), Ayu SX + MX and CE (2487615539), MinhVT – SC+ MX and CE (2487681106), Baopg – Note – SC+ MX and CE (2487550014), TungNS – SC+ MX/CE (2487845001), Quynhltn – SC+ MX (2487189597), Ngavt – SC+ MX/CE (2487222377), Trangnnt – SC+ MX/CE (2487320801), Thanhvd – SC+ MX & CE (2488107154).

Meeting: 28/10/2026, recording 11:11 (~59 min, MX SC+) and 13:47 (~46 min, CE SC+). Group: Product. Chair and presenter Chong Haw Eong (SDSAP, PIC). BiPlus: all CoE members (Merch, Tech, QA) in the room and on Teams. The 11:11 recording starts mid-way, so the opening of the session (before the category section) is missing. SC+ on 3PD is on its own page (25_Handover_Day4_SC+_MX_and_CE_on_3PD_Platform).

References: KB – PH CE SC Bundle Monthly; CE SC+ Standalone Setup Guide; KB 0 – STANDARDIZED SC+ SKU Format; KB – BULK Upload SC+ SKU; slide "MX SC+ Bulk Upload Verification"; related: Day 3 EA Direct Access and Warranty.

# Part 1 – MX SC+ (Samsung Care+ for MX devices)

## 1.1 Category, standardised base codes, five SC+ types
- Category **[insurance]** (VN Master Product Catalog) sits under supercategory **3 = external service**, with sub-categories monthly and standalone. Assign the **base code** to the category (not each variant). Base codes have already been standardised and migrated.
- Base SKUs per country: `SMC-<CC>-BUNDLE-UPFRONT`, `SMC-<CC>-BUNDLE-MONTHLY`, `SMC-<CC>-STANDALONE-UPFRONT`, standalone monthly, and **NGC** (e.g. SMC-AU-NGC-MONTHLY). New variant SKU format: `[SUBS]-[SC+ Type]-[Payment Type]-[Categories]-[Duration]-[Product type]-[free text for Promo]`; old SKUs do not follow it.
- Types: **bundle upfront** (bought with the phone, paid once), **bundle monthly** (e.g. 24 months), **standalone upfront / monthly** (bought later; enter IMEI on the standalone page; 1/2/3 years). Each subsidiary has a standalone page on shop.samsung.com (e.g. /vn/samsung-care-standalone) fed from Hybris.
- **NGC (New Galaxy Club)** exists only in **AU and SG**; enabling other subsidiaries is in progress (Chong will send a tracking page).

## 1.2 Subsidiary request template and RRP
- The subsidiary fills a standard template (shared with RHQ, on Confluence): sheets Template, SKU Mapping, **COE ONLY (RRP)**, DO NOT DELETE. Columns: Subs, SC+ Type, Payment Type, Categories, Duration, Product Type, Free Text for Promo → **Hybris SKU** auto-generated; Identifier, RRP, Start Date…
- SC+ portal code: previously **P-GT…**, moving to **MI-…** (Malaysia already moved). **Manufacturer AID** and **perks** (payment provider parameter, shown on the front end) are mandatory; subscription info only for monthly.
- Some subsidiaries overwrite the generated SKU with their own – check.
- **RRP comes from no system**: upload it yourself and raise price approval using the RRP template.

## 1.3 Bulk upload columns
Product Cockpit → download the SMC product template, always from the **master catalog**.
- BaseProduct from dropdown; VariantProduct and Identifier from the subsidiary template; Summary (monthly SKUs) in local language and English; no short description.
- Initial **Approval = check**, **sales status = archive** so nothing goes live before verification.
- **Manufacturer**: bundle = **SMC**, standalone = **standalone SMC**. **Manufacturer AID** is the key linking Hybris to the **SC+ server**.
- Subscription only for subscription SKUs; the "three months" free (charged from month 4) only if the subsidiary says so.
- **Product type**: bundle = **EXTERNAL_SERVICE_SKU**. Standalone needs **two SKUs**: a normal SKU and an **EXT** SKU with product type **external service** (not external service SKU) – easy to confuse.
- Tax class per subsidiary; **perks** (e.g. ADH accidental damage, EW extended warranty) supplied by the subsidiary and shown in the SC+ section of the PDP.
- Warehouse per subsidiary (VN uses **4 warehouses** for SC+); available 9999; in-stock status blank (default forceInStock); service content / feature key blank.

## 1.4 Verification in Backoffice
Using the slide MX SC+ Bulk Upload Verification: Identifier, sales status archive, manufacturer AID (Extended Attributes tab), number of subscription (e.g. 36), recurring cycle = monthly, free months default **0** (never blank). **Block stock/price import = true** by default (SC+ is linked to the SC+ portal, not NERP, so no ERP stock). Payment provider parameter shows the perks; each warehouse has its available amount. **Images**: standalone must have an image (it enters the cart as its own item); only HQ/RHQ-approved images; bundle needs none.

## 1.5 KB – BULK Upload SC+ SKU
Per-column checklist: bundle = external service SKU; standalone normal = normal; standalone EXT = external service; tax class per subsidiary; warehouses per subsidiary. Perks may be multiple, separated by `|`. **Known bug when deleting perks**: clicking X then Save keeps the value – use **Bulk edit → payment provider parameter → remove this attribute**, then enter the new value. After upload check cronjob **tokoSMCVariantProductBulkUploadJob**.

## 1.6 Setup not covered by the upload file
- Unit = pieces (master). **Company code** mandatory for two countries: **VN = C5H2**, **TH = C540** (missing → posting errors downstream; VN entered in Hybris, TH in NERP). Package quantity = SC+ term (12, 24, 36).
- **RRP** uploaded separately (master) and submitted to Knox approval via priceinfochange.
- **Delivery mode** (child): bundle follows the MX delivery mode; standalone uses `XX-SMC-DIGITAL-DELIVERY` (XX = country code); exception SEPCO: `ph-smc-digital-delivery-mx-standalone-monthly` for standalone monthly.
- Additional info (legacy) for standalone: T&C `EXTERNAL_SERVICE_LEGAL_INFO` (shared by all SKUs; the tick box when entering the IMEI).
- **Product reference**: bundle → main phone **AVAILABLE_SERVICE** → SC+ SKU; standalone → **AUTO_ADDED_SERVICE** between the standalone SKU and its EXT SKU, in every catalog **except 3PD**.
- **Critical**: every new SC+ subscription (Monthly or Standalone Monthly) needs a ticket to the **Tech team** to configure **AddedServiceConfig (smcPaymentTypeOverride)** before the SKU goes live; without it later months are not collected (dunning payment). Merch cannot see this config, so double-check.

## 1.7 Crosscheck before selling
Export the Hybris report and compare with table "5. Crosscheck again for setup".
- **Bundle**: normal SKU variant, master catalog; product type EXTERNAL_SERVICE_SKU (wrong type → order errors and SC+ cannot register); RRP synced to all catalogs; identifier; company code VN/TH; **TH has its own sales organisation** (screen shows 5A02, speech said 5802 – to confirm); package quantity; manufacturer SMC; warehouse = the country's MX warehouse; perks; product reference (child); MX delivery mode; PID (manufacturer AID); approved; sales status archived; subscription 12/24/36, recurring monthly, free months 0 unless requested.
- **Standalone**: normal SKU with the subsidiary's RRP; **EXT SKU must have RRP = 0** (never sold, only for SC+ server ↔ Hybris communication). Subsidiaries with an SC+ price approval path (e.g. VN) may ask why 0 – they know the answer. EXT: no identifier, manufacturer standalone SMC, no warehouse / product reference / additional service. Normal SKU approved, **purchasable not visible**; EXT approved and **archive**.

## 1.8 Backoffice examples
- `SMC-VN-BUNDLE-MONTHLY-MA-3Y-PROMO-A5-FE-ADH-3MF`: bundle monthly, mobile (A series), 3 years, perks ADH, 3 free months, identifier "Gói Samsung Care+ tháng"; Extended Attributes: manufacturer SMC, AID, package quantity 36.
- A subsidiary may change terms (e.g. drop the 3 free months → 0) on an old SKU: **do not change the SKU code**, only attributes/names. TH often reuses old SKUs (many P-GT codes) and only changes the manufacturer ID; approval is needed only for new SKUs.
- Standalone: each normal SKU has its own `-EXT` SKU. **Never share EXT SKUs** even with the same PID: 25 standalone SKUs → 25 EXT SKUs. The AUTO_ADDED_SERVICE reference must exist **in every catalog**.

## 1.9 No discount on MX SC+; scope
**MX SC+ must never be discounted** – no discount, special price, discount row, promotion or voucher. A discount makes **SC+ registration/activation fail**; this is an SC+ server requirement, not the subsidiary's. Allowed: buy SC+ → discount on the phone. Not allowed: buy a phone → discount on SC+. Promotion rules must **exclude SMC**. The add-on page only shows normal products (accessories). Standalone is sold **only on the e-store** (shop.samsung.com/vn), no EPP/multistore.

## 1.10 Samsung Backoffice Extension → Samsung Care+, PDP content source
- Tabs **Hybris → SC+ (eStore)**, **SC+ → Hybris (eStore)**, **Standalone**: pick country/catalog, search the phone SKU to see the SC+ items and the **PID attached on the SC+ portal**, start/end date, status (e.g. Missing Normal Variant, Expired). Used to verify when a subsidiary says "set up but not visible": nothing for the SKU means the SC+ portal has not registered the SKU with that PID. Happens very often; subsidiaries report via Jira.
- On the PDP: perks, short description, name, price, identifier come from **Hybris**; layout and detailed content from **AEM** (global design; contact AEM to change). Chong has access to the AEM Jira project and raises tickets for subsidiaries; the VN team should request access (Chong will send the contact).

## 1.11 Q&A
- **Price approval for every country?** Mostly. An enhancement to pull the price from the SC+ portal is planned (no date). Until then every SC+ (MX and CE) not in NERP needs RRP approval; EXT must be **0**, not blank.
- **Buying standalone**: enter IMEI (time limit after phone purchase – a few weeks to a month, not configured in Hybris) → pick SC+ → tick T&C → shared e-store cart; **max 1 product per cart**, no mixed cart, no discount; checkout skips fulfilment.
- **Testing**: needs an IMEI from the subsidiary; the IMEI generator works only sometimes, mostly on staging. The setup owner self-tests, then moves the ticket to **QA review**; testing is done on production with subsidiary-provided data.
- **3PD**: a different setup, see the 3PD page. Chong: SC+ is the most time-consuming and error-prone area – be extremely careful.

# Part 2 – CE SC+ (Samsung Care+ / Extended Warranty for CE)

## 2.1 Differences from MX and the front end
CE SC+ is similar to MX but the manufacturer is **GCIC** (MX = SMC). KB under *KB – 2. External Service Warranty (CE SC+)*. **TH is still on the old CE SC+ phase**; other subsidiaries moved to the new phase. Chong could not find SC+ on the TH and MY PDP demo and will check.

## 2.2 Types, SKU rules, pre-check
Two types: **bundle** and **standalone**; a server enhancement for **monthly** is coming. Model codes start with **P** (P-GT, P-QT…); CE has **no naming standard**, use the subsidiary's code. **Pre-check**: if a SKU already exists in Hybris for another purpose (e.g. CE SC+ bundle) it cannot be used for another type (e.g. standalone) – check per country and ask the subsidiary to revise; assign the pack code to the right base product. The **base product is the only way** to tell bundle / monthly / standalone apart.

## 2.3 GCIC base codes and Warranty category
**PH** was the first country on the new CE SC+; MY, ID and others follow; TH has no extended warranty on production yet. Backoffice → Categories → **Samsung Care+ Warranty [warranty]** (PH Master Product Catalog) → base codes: standalone, **GCIC-PH-MONTHLY**, bundle (old base codes kept). New countries: use a standard like `GCIC-MY-MONTHLY` or agree naming with RHQ. The subsidiary must also send the **TAT / pin map** file. Source: warranty playbook and user guide from the spoke team; each new enhancement is handed to the CoE with setup/operation guidelines, known errors and local config; ~**14 days** of hypercare, then maintenance (issues → L2).

## 2.4 PH front end
PDP offers **bundle** and **monthly**. Unlike MX, **CE SC+ can be discounted** (handled by GCIC, not the SC+ portal): special price, PWP etc. FOC: SKU is an external service SKU so **BOGO usually does not work** – use **partner product discount 100%**. The new PH cart layout: popup **Warranty Extension** → Payment Type (One-time / Monthly) → **Plan Type** (Samsung Care+ / **Samsung Care+ Premium**) → Plan (1–4 years). The SKU must have a plan type assigned or the list is empty; Premium is recognised from the SKU name.

## 2.5 SKU setup for bundle / bundle monthly (KB PH CE SC+ Bundle Monthly)
- Bundle and monthly are the same, monthly adds free months, subscription cycle, recurring charge. Base code PH `GCIC-PH-MONTHLY`. **Do not rename** the subsidiary's SKU.
- **RRP** does not come from NERP: copy from the subsidiary into the template, upload, raise price info change approval (path varies by subsidiary).
- **PH only**: upload the **pin map** (postal code delivery TAT, postal code zone map, then check product-to-postal-code map) and the OS file.
- Base code assigned to the warranty category; manufacturer **GCIC**; product type **EXTERNAL_SERVICE_SKU**; identifier (PH en_PH); **external service type = Warranty**.
- Warehouse: PH **WCOL-S513** (plant + storage location; TH only WC03). **No bulk upload** – manual per SKU; stock import upload possible; Stock import override configuration only PH.
- Content unit months; package quantity; **Block status update / block updates from external / block price import / block stock import = true** (all four).
- **GRP sync type and GRP return sync type**: PH = **CY**, others **CT**.
- Manufacturer warranty period (1 year = 12), number of subscription, recurring cycle = month, free months if any.
- TokoVariantProduct additional attribute **plan type** = Samsung Care+ or Premium – manual per SKU (100 SKUs can take a whole day).

## 2.6 Approval, product reference, T&C, PWP
Approval = approved; sales status per KB. Main phone: product reference **AVAILABLE_SERVICE** → CE SC+ pack code, for every catalog the subsidiary sells in. **T&C line item** in the cart: Administration Cockpit → Terms → terms condition components; the insurance disclaimer / warranty fragment needs the **Tech team**. **PWP example**: container A = main SKU, container B = SC+ SKUs; action percentage discount on partner product 50%, selection strategy **cheapest**. The main SKU needs **external service type = warranty** for PDP/cart display.

## 2.7 Roadmap, warehouses, on-demand standalone
PH deployed; **MY, NZ, SG, ID** coming; standalone monthly coming. Each country differs from PH – request the setup guide from the spoke team after each deploy. Warehouse names are in **product fundamentals**: MY has 2 (MX, CE), SG one shared, PH MX / CE / SMB, VN ~20 by region plus EA retail (warehouse handover comes separately). **On-demand standalone** (KB PH CE SC+ On Demand Standalone) is on hold, never sold.

## 2.8 CE SC+ Standalone Setup Guide (AU)
Like MX: **one normal SKU and one external SKU**. RRP: external SKU always **0**. Base code → **GCIC standalone**; Administration → **Max Standalone Service Limit Per Line = 1**; manufacturer **GCIC STANDALONE**. GCIC **Manufacturer ID** format `company code-pack code` (always ask the subsidiary too). Content unit months (odd values like 27–30 exist, e.g. ID); manufacturer warranty period usually = package quantity. Normal SKU: approved, purchasable not visible, GRP sync type **CT**, four block flags true, product type **normal**, delivery mode e.g. AU-warranty-delivery, **auto added service** to the external SKU in all catalogs **except 3PD**. External SKU name = pack code + `-ext`. Agree names/base codes with RHQ first. Biggest pitfall: **product type** – bundle = external service (SKU); standalone = normal + external service.

# Difficult points
- MX SC+ must never be discounted (even voucher / PWP) – failure shows only after the customer buys; CE SC+ is the opposite.
- New SC+ subscriptions need Tech's AddedServiceConfig before activation; Merch cannot check it.
- Product type confusion (bundle EXTERNAL_SERVICE_SKU; standalone normal + EXT, EXT RRP 0, no shared EXT, auto added service in all catalogs but 3PD).
- RRP never comes from a system; the price-from-portal enhancement has no date.
- CE SC+ has no bulk upload; each new country differs from PH.
- Testing depends on subsidiary IMEIs and is done on production.

# Next steps
Read the KBs and slides above; request the SC+/NGC status page and the AEM contact and AEM Jira access; build a go-live checklist; agree CE base-code naming with RHQ (e.g. GCIC-MY-MONTHLY) before MY/ID/SG/NZ deploy; ask Chong to confirm the TH sales organisation (5A02 vs 5802), the standalone purchase window and why SC+ was missing on the TH/MY PDP.

Recordings: Handover_Day4_sc1_2026.10.28.mp4 and Handover_Day4_sc2_2026.10.28.mp4.
