# CoE Meeting Notes – Handover Day 4: OOW (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487910414
Sub-pages not yet summarised in this file (personal notes): Baopg – Note – OOW (2487320746), TungNS – OOW (2487320778), ngavt – oow (2487877836), Quynhltn – OOW Product setup (2488172564), Ayu – OOW (2487648406), Trangdtt – OOW (2487517214).

Meeting: 28/10/2026, recording starts 15:07 (~16 min); combined session "OOW | RNPL" (RNPL is on 28_Handover_Day4_RNPL). Group: Product. Chair and presenter Chong Haw Eong (SDSAP). Scope: Out of Warranty product setup – general guideline for all subsidiaries and a separate setup for Indonesia.

References: KB – OOW Out of Warranty (Samsung Confluence, page 586633425); related Day 3 EA Direct Access and Warranty, Day 4 RNPL.

## 1. What OOW is
OOW is for **EOL** device SKUs (e.g. X23, X24 lines). When a customer wants a **part replaced** (battery, screen) they buy a service pack in the store. The front end calls it **Smartphone Care Pack** (wording may differ on production); Hybris calls it **OOW**. Example: screen replacement pack for Galaxy Z Fold7 (TH). The PDP takes content from **AEM**, so the SKU needs AEM, price and warehouse sync.

## 2. Setup for all subsidiaries except Indonesia
KB: *OOW Product Setup (All subs except ID)*.
- **SKU format `P-GT-XXXXXX`**. Products starting with **P** are **pack codes**: virtual products for service/maintenance packs such as **SC+** and OOW.
- **Standard category** for all: identifier **servicepacks**, name **Out of Warranty Service Packs**, assigned to **External_Service** (category 3). **Base code `P-SERVICEPACK`**. Bulk upload template: modelCode (SKU), modelName = P-SERVICEPACK, category = servicepacks, unit = pieces.
- Orders **are sent to NERP** for all subsidiaries **except Indonesia**. Reference tickets: THAME-16129 ([TSE] MX OOW Voucher Project), PME-11921 ([SEPCO] MX OOW Product Register). Each subsidiary is quite customised – always follow its guideline.
- **Supersync (master catalogue)** for **AEM (DOTCOM)** and **Price** (Products Sync Selector Wizard, result SUCCESS). AEM has no cronjob pushing SKUs back; sometimes the SKU already exists in AEM, sometimes not. Asked how to know AEM created the SKU: only AEM knows; register an email to receive the report (mechanism unclear).
- **Warehouse and Stock (master catalogue)**: ask the subsidiary (may differ from MX). KB values: **SG WC91**, **PH WC3L-S513**, **TH WC04**, **AU WEC2**; VN and NZ do not sell; MY to check. **Available amount = 99999**, Product Code = SKU, **Is Blocked for Stock Import = TRUE**.
- **Fundamental setup (master)**: Sales unit = pieces; Identifier from the subsidiary; Tax class per country; **External Service Type = BENEFIT**; **Product Type = NORMAL** (because it goes to NERP); **TokoVariantProduct.gspSchedType = CT**. Sync all child catalogues Staged then Online.
- **Delivery mode (child, fixed production values)**: SG `sg-warranty-delivery`, PH `ph-servicepack-digital-delivery`, TH `th-delivery-standard-ce`, AU `au-servicepack-digital-delivery`.
- Crosscheck by **exporting the product report**.
- **Order Type and Item Category**: raise a **COEC ticket** to Tech with the subsidiary's info. So far only **Order Type YS10** and **Item Category YNS5** (PH, TH). For NERP the **ERP item category must be MAIN_PRODUCT**, configured in Admin Cockpit → Types → **ErpItemTypeDetail** (create ErpItemTypeDetail and ErpItemTypeDetailRef per table Product Code / Warehouse / Order Type / Scheduled categories (CT) / Item Categories / ErpItemTypeValue; sample PC ticket "[SEPCO] To add the servicepack codes in item category"). CoE does product setup, Tech does this config.
- **Status**: Approval = **APPROVED**, Sales Status = **PURCHASABLE**. User journey e.g. samsung.com/th/care-pack/smartphones-care-pack/oow-p-gt-lcxos1pw: add to cart and pay like a normal product.

## 3. Indonesia (ID) specific setup
KB: *OOW Product Setup (ID specific setup)*. SKU format, category (servicepacks) and base code (P-SERVICEPACK) are the same.
- **Orders are not sent to NERP**: configured at delivery mode level `id-servicepack-digital-delivery` with flag **Skip Fulfilment = true**.
- Because the ID SKU is not created in NERP, **AEM must be synced manually** (AEM/.com ≠ NERP) and the **RRP submitted by the CoE** (KB "Submit RRP via knox Approval").
- **Blocked price & stock**: available amount **1000000**, **Warehouse = WC28 & WC27**, **Is Blocked for Stock Import = TRUE**, **Is Blocked for Price Import = TRUE** (the KB screenshot may be outdated; text value is right). **Stock Import Override Configuration** is no longer used – only block stock.
- Fundamental setup: ID tax class; **External Service Type = BENEFIT** (otherwise a benefit placed on the PD does not show); **Product Type = NORMAL** (kept NORMAL although nothing goes to NERP; follow the guideline).
- ID **does not need** the order type / item category / ERP item category config.
- **Discount/promotion on OOW?** Chong: normally never run because subsidiaries haven't requested; check if a request comes. Yet the live ID page (e.g. **Display Repair for Galaxy S25 Ultra**, P-GT-LCDXS1PB) shows a struck-through price and "Diskon tambahan" – a **special price / price row**, so discounts can be run via a price row.

## 4. Link with SC+
Administration Cockpit → Catalog → Categories, e.g. **Samsung Care+ Warranty [warranty] – PH Master Product Catalog**, supercategory **External_Service [3]**, products like P-PACKCODES, GCIC-PH-STANDALONE, GCIC-PH-MONTHLY. MX SC+, CE SC+ and OOW all sit under this branch (SC+ has its own session). The last Q&A (≈15:00–15:25) is inaudible.

## Difficult points
- Setups differ per subsidiary; KB tables only cover SG, PH, TH, AU (+ ID); **MY unclear**, VN/NZ don't sell.
- No clear way to know whether AEM created the SKU before supersync.
- Order type / item category / ErpItemTypeDetail = MAIN_PRODUCT is done by Tech via ticket; without it OOW orders to NERP can be wrong.
- ID: no NERP (Skip Fulfilment on delivery mode), manual RRP and AEM sync, product type still NORMAL.
- Unclear rule on discount/promotion for OOW (Chong said never, ID cart shows a price-row discount).
- Some ID KB screenshots outdated (Blocked for Price Import).

## Next steps
Read both KB pages; build an OOW checklist (P-GT SKU, servicepacks category, P-SERVICEPACK base code, AEM/price supersync, warehouse + block stock, BENEFIT, NORMAL, gspSchedType CT, delivery mode, order type/item category ticket, APPROVED/PURCHASABLE); ask Chong about MY, the AEM report email / SKU check, discount rules (especially ID); get a sample COEC/PC ticket for ErpItemTypeDetail (MAIN_PRODUCT).

Recording: Handover_Day4_or1_2026.10.28.mp4.
