# Day1 - Tue-27-Oct 11:20 Room A - Topic 18 Trade-in setup (With T-base code)

> Services: MER-TRD-01, MER-TRD-02, MER-PRF-03 (all **not Tier 1**) | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

**No Service Pack exists** on BiPlus Wiki for these three services (searched space COE by service ID and by title). The summary below is therefore built from the Samsung KB pages copied into BiPlus Wiki (space SamsungCoETech, copied 21 Oct 2026). Which KB step belongs to which service is **my reading**, not something the sheet states.

## Session
| Field | Value |
|---|---|
| Inventory topic | #18 - Trade-in setup (With T-base code) |
| Call (BiPlus plan v3) | Tue 27 Oct 11:20, Room A (right after topic 16 Overtrade) |
| SDSAP date / status | 27-Oct |
| Component / area | Added Service / Service |
| SDSAP PIC | Lee Chia Yee, Tai Sheau Yann |
| Samsung Confluence link | No link |
| Maps to (BiPlus) | MER-TRD-01 Trade-in SKU (T-Code) sync and activation, MER-TRD-02 Trade-in price update; MER-PRF-03 Available service (SC+, trade-in) reference setup |
| Priority | Tier 2 |
| Verdict | **Add** (no page) |
| BiPlus PIC for the topic | Thanh |

**Why this verdict:** No page.

**Questions for SDSAP (from the sheet):** Share the trade-in setup page, or BiPlus writes it from the recording; how T-codes are synced and activated.

## Why it matters to the other Merch services
From the MER-PRM-06 Overtrade pack (topic 16, the session just before): overtrade only works if **T-codes are active (MER-TRD-01)**, each device has an **active trade-in reference (MER-PRF-03)** - without it the cart cannot add trade-in - and **base values are current (MER-TRD-02)**. MER-PRD-01 also needs the external service type `TRADE_IN` / `TRADE_UP` on the SKU. MER-DLV-01 (V2) names the TH T-SKU page below as the way to register a missing trade-in T-SKU.

## What the KB says, by step

### 1. T-code (T-SKU) registration and activation - likely MER-TRD-01
Source: *KB - TSE MX Tradein - Register T- SKU* (2477457932, TH, updated 2026-04).
- Only when the T-SKU is **missing**. T-codes hang under brand base SKUs named `T-<BRAND>-REMOBIE` (16 listed: Apple, Huawei, Motorola, OnePlus, Oppo, Samsung, Sony, Vivo, Xiaomi, Realme, Honor, Asus, Nothing, iQOO, HP, Lenovo).
- Upload file columns: `modelCode` (e.g. `T-Apple-iPad-10-10.9-inch-Wi-Fi-64GB`), `modelName` (the base SKU), `category` (default 1234; example row shows `tradein`), `unit` (pieces). Follow the model names in the subsidiary's file.
- Sync to the child catalog and set, per site: delivery modes, approval = Approved, sales status = `PDP_NOT_AVAILABLE`, product type = EXTERNAL SERVICE.
  - Estore (All MX / SC+): `th-delivery-standard-UPC-MX`, `th-delivery-standard-BKK-MX`, `th-o2o-store-pickup`, `th-tradein-o2o`.
  - EPP (All MX): the two `th-delivery-standard-*-MX` modes.
- Sync to Online, then continue with the trade-in grading page (step 2).
- SEAU note: in AU, new T-code SKUs are **uploaded automatically and set to approved**; ASURION is the trade-in provider.

### 2. Trade-in price: grading, min/max value, compute - likely MER-TRD-02
Source: *TSE Tradein/TradeUP+ Grading + Register New Model* (2477982009, TH, updated 2026-02).
- Trade-in SKU upload (Product Cockpit > `TRADE_IN_DEVICE_SELECTIONS`): change only `MaxExchangeValue` / `MinExchangeValue`, taken from the Grading file (A = max, F = min). **Always Append**, unless the subsidiary asks to remove SKUs.
- Then **Compute the price in Base Store**; the storefront price updates immediately.
- Grading upload: take the subsidiary's table, keep only ID and prices A to C2 (C2 = grade D+, called that on the Remobie side), save and upload in the cockpit; check the cronjob is **SUCCESS**.
- New model: the subsidiary sends a monthly file; fill Name, Brand, Model, ModelDisplayname (repeat the model), Memory, min/max from the grading file; the rest is the same.
- This page answers the topic-28 question: the link is **trade-in/trade-up grading (TH)**, not SC+.

### 3. Product reference: which T-codes a device can trade in - likely MER-PRF-03
Source: *SEAU: Trade-in/Overtrade/Trade up* (2477195677) and *KB - TV/CE Trade-up Mapping Setup in Hybris* (2477687257).
- Reference is set **in the child catalog**. Bulk-upload product references: `sourceCode` = main SKU (e.g. SM-S938BZGFATS), `referenceType` = `AVAILABLE_SERVICE`, `active` = TRUE, `targetCode` = the T-code (e.g. `T_PHONE_APPLE`, `T_TABLET_SAMSUNG`, `T_WATCH_SAMSUNG`, `T-ASURION-TRADEIN`, `T-ADDON`).
- Verify in Administration Cockpit > Products > SKU > **Category System** tab that the T-codes are mapped with `AVAILABLE_SERVICE`.
- CE/TV trade-up: Category System > Product References > target `T-TRADEUP-VARIANT`, type `AVAILABLE_SERVICE`; check `External Service Type` contains `TRADE_IN`; sync Staged -> Online.

### 4. Trade-up (TV/CE) configuration - related, MER-TRD-01/02 per the sheet
- Prerequisites: the business fills a trade-up file, **MSA** uploads the base discounts. The `tradeup` category and `T-TRADEUP` / `T-TRADEUP-VARIANT` must exist, be synced and approved.
- Site level: Backoffice > WCMS > Website (CMSSite) > tab *Promo Price List* > Get All Price List > select > Update Price List (`price_promo_1` = eStore, also usable for EPP; `price_promo_2..5` = EPP sites).
- Product level: Product Cockpit > select products > **Trade in Configuration**: category TV, brand, models, Discount Amount (0), Start/End date, sites > Save Mapping > Finish. Extra discount beyond MSA's base is set on the Hybris side.
- Check via Administration Cockpit > `VariantTradeinMapping` (filter Main variant / Site ID - the Site ID must match or it will not show).
- CE trade-up bulk (Revamp, 2477523394): Administration Cockpit > **MSA Uploads** > Base Store > *MSA File Download Template*; fields CE SKU, Store IDs (comma-separated, no spaces), Device IDs (from the subsidiary), additional discount, Start date (blank = immediately), End date (blank = runs indefinitely).
- EPP: trade-up T&C is a `TermsCondition` (context SERVICE, name DISCLAIMER, context code `tradeup_tc`). Only **1 unit of the same SKU** is eligible; more removes the trade-up from the cart.

### 5. Trade-in bonus / overtrade (topic 16 link)
`TRADE_IN_DEVICE_PRICE` upload (OfferID, VariantSKU = main SKU, VariantReturnSKU = T-code variant, SamsungDiscount, OpenPromotion, dates, CMSSite), then check Product Manager > *Overtrade Discounts Bonus*. SEAU page flags this bulk upload as **pending an issue (AUME-16626)**; the alternative is a promotion rule of name type TRADE-IN. The AU example front-end total = provider amount + Samsung amount.

## What to ask SDSAP in this session
- Share the trade-in setup page, or confirm the recording is the source (verdict Add).
- Is the **TH "Register T-SKU" procedure the same in all markets**? Where is the T-code base list kept, and what is the correct `category` default?
- Who activates T-codes in markets with auto-upload (AU): Merch or the provider/middleware (TEC-VAS-01)?
- Who maintains the **device mapping and the partner price list** (topic 17 question): Merch or Tech? How does the min/max from the grading file reach `TRADE_IN_DEVICE_SELECTIONS`?
- Is the `TRADE_IN_DEVICE_PRICE` bulk upload still affected by AUME-16626, and which route (rule or Overtrade Discounts Bonus) do they use now?
- What is the **test method** (device, IMEI, quote) on staging? (same open point as MER-PRM-06)

## Related sessions on Day 2 (Wed 28 Oct, Room A, both BiPlus PIC Thanh)
| Time | Topic | SDSAP PIC | Link | Verdict | Question in the sheet |
|---|---|---|---|---|---|
| 10:00 | #28 SC+ Grading (TH) | Kasma Sama-Air | TSE Tradein TradeUP Grading Register New Model | Clarify | Is this trade-in grading or SC+? Is it TH only? |
| 14:00 | #17 Trade-up | Saidatul Humairah Binti Abdul Razak | Bulk Upload CE Trade-up Revamp | Reuse | Who keeps the device mapping and the partner price list: Merchandising or Tech? |

Both read the same KB pages summarised above (sections 2 and 4). Topic 28's link is the grading page, so the title "SC+ Grading" is most likely a naming mistake - confirm with SDSAP.

## Pages to read before the session
KB - TSE MX Tradein - Register T- SKU (2477457932) - TSE Tradein/TradeUP+ Grading + Register New Model (2477982009) - SEAU: Trade-in/Overtrade/Trade up (2477195677) - KB - TV/CE Trade-up Mapping Setup in Hybris (2477687257) - Bulk Upload CE Trade-up (Revamp) (2477523394). All under `https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/<id>`.
