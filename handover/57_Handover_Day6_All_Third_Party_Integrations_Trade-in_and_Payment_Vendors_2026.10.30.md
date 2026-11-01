# CoE Meeting Notes – Handover Day 6: All Third Party Integrations – Trade-in and Payment Vendors (2026.10.30)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2491580527
Sub-pages (personal notes, not summarised in detail): TungNS – All third party integration (2491318728), NgaVT (2491449776), Quynhltn – Integrations (2492072019), Ayu – Payment Mode Configuration and Trade-in Integration (2491580916).

Meeting: HELD on 30/10/2026, recording starts 14:58 (about 25 minutes), Teams + meeting room. Group: Integration. Chair/presenter: Manikanta Vaddisetti (SDSAP, PIC). BiPlus: all CoE members. Confluence pages used (02-3 : Tech Team): **Payment Mode Configuration and Trade-in Integration Overview**, **Tech COEC team** (table "SUB's Functionality Wise Distinguish"), **Warehouse fulfillment for an order**; KB – [MY] Trade-in Customer Journey. The last part (section 4, warehouse selection) is an extra topic added with the remaining time. Related: Day 3 Trade-in T-Base Code (13_), Day 3 Trade-up (12_), Day 3 EA Direct Access and Warranty (08_), Day 6 Samsung Vault (52_), Day 6 All SEAO Cronjob (54_).

## Main content

### 1. Payment mode configuration (00:00 – 07:24)
**Overview (00:00–01:07).** Active payment modes per country are listed on the **Tech COEC team** page, table **SUB's Functionality Wise Distinguish**, column **Payment Modes** (ID example: id-contactlessPaymentMode, id-goPayWalletSNAPPaymentMethod, id-kredivoMORPaymentMode, id-midtransBankTransferSNAPPaymentMode, id-rewardsPaymentMode, id-zeroPaymentMode-SMB …). Opening a payment mode in Backoffice shows its **vendor** information.

**Display conditions, strategy, provider, new payment mode (01:07–03:53).** Backoffice → **Payment Modes**; example **Trả Góp 0% Qua Thẻ Tín Dụng [vn-CybersourceCreditInstalmentPaymentMode]**.
- For a payment mode to be shown on the front end it needs: **Is Active = True** (Properties tab); **Payment Provider Parameters** (e.g. useCertificate, forceSendOrderCompletionEmail, captureUrlRest = /pts/v2/payments/%s/captures, isDynamicCalculation, doRefundRewardsWhenTempExpired, sendPromotionResultsForFraudCheck); **strategies** in the Administration tab.
- Strategies seen: **Payment Mode Eligibility Strategy** = tokoCybersourceCreditInstalmentEligiblityStrategy, **Payment Response Strategy** = cybersourceCreditCardPaymentResponseStrategy, **Payment Response Subscription Create Strategy** = cybersourceCreditCardPaymentInfoCreateStrategy; PaymentMode.paymentModeType = **INSTALLMENT**. **Payment provider** = **cybersourceCreditInstallment** (the vendor, CyberSource).
- A new payment mode: **clone** an existing one or create new. Process: **test on staging** (end-to-end with **NERP**) → **soft launch** on production → **go live** for the country (soft launch details not given).

**Filtering order: base store, website, multi-store (03:53–07:24).**
- Site types: **e-store**, **EPP** (staff only), **SMB**. All usable payment modes of a country are set at the **base store**; per-site modes at the **website**.
- **Regular e-store**: check **website** first; if empty **fall back to base store**. **Multi-store**: **multi-store → its website → base store**; an empty level falls through.
- Website: WCMS → **Website** (e.g. **vn_ea_swl_epp**) → Administration → **CMSSite.paymentModes** (Trả Góp 0% Qua Thẻ Tín Dụng, Pay At Shop [vn-pay-at-shop]); next to it **Site Payment Config** (no value).
- Multi-store: Properties tab → **Payment Modes** (popup Edit item vn_ea_swl_epp with tabs Configurations, Properties, Cart Restrictions, MultiMedia, Retirees, F&F Configurations, Shop App, Administration); seen: OnePay ATM/QR, Bank Transfer, Pay on POS [vn-payOnPosNonASM], Rewards Redeem, Trả Góp 0%. If empty here, the site-level modes apply. No questions.

### 2. Trade-in vendors per country (07:24 – 11:34)
- How trade-in works (SG TIPLUS) was covered in the morning handover, so only a summary here. Customer journey: KB – [MY] Trade-in Customer Journey (KB – External Service → 3. External Service Trade-in (MX Overtrade)). Trade-in can be chosen on the **BC (buy) page** before add to cart or **after add to cart**: enter a **zip code** (must be in the vendor's service area, e.g. COMPASIA) → device type (mobile, tablet, watch) → specifications → checkout.
- One vendor per country; the vendor pushes data; each country has **its own cronjobs**: one imports data into **TokoSelection**, one creates the **trade-in price/product (T_SKU)** in Hybris so trade-in works.

| Country | Vendor | Cronjobs (per Confluence page) |
| --- | --- | --- |
| VN | TCV | Prices via TCV API; **vn-tcvTradeInImportData** (Toko Selection), **vn-tcv-product-price-imports** (creates T-SKU) |
| SG | TIPLUS | **sg-tiplusTradeInImportData** (fetch TIPLUS data into Hybris), **sg-tiplus-product-price-imports** (turns TokoSelection into Products; run whenever TIPLUS adds trade-in products; creates T_SKU, then **sync to child catalog**) |
| MY | CompAsia | my-compasiaTradeInImportData, my-compasia-product-price-imports |
| TH | Remobie | (empty on the page) |
| PH | Bolttech | ph-boltechTradeInImportData, ph-boltech-product-price-imports |
| NZ | Assurant | nz-assurantTradeInImportData, nz-AssurantV2-product-price-imports |
| AU | Asurion | au-asurionTradeInImportData, au-asurion-product-price-imports |
| ID | EZTRADE | id-TokoEZTradeInImportData, id-eztrade-product-price-imports |

- Manikanta will add more cronjob details to the page. The **Tech COEC team** page also has columns TradeIn, Overtrade, SC+, OrderProcess, FI Posting, Cancellation, Refund, Delivery Mode, Warehouse, Payment Modes per country. ID: TradeIn integrates **EZTRADE** (a middleware between the real trade-in vendors; data in Hybris DB, TokoSelection data shown on the front end; ref KB – [ID] Multi vendor tradeIn Flow); Overtrade is **not used** in ID (promotion rules are used). **Overtrade** is unused in some countries. No questions.

### 3. Extra topic: warehouse selection when ordering (11:34 – 24:40)
Page **Warehouse fulfillment for an order** (02-3 : Tech Team), a technical summary.
- **Config prerequisites**: create a **warehouse** with **default = true** and priority level (needed or not depends on country; VN selects differently); **assign the warehouse to the base store**; it must **have stock** for the SKUs; **map the warehouse to the allowed website**.
- **Priority order (first match wins)**: 1 **External (3PA)** → 2 **Marketplace** (3PD orders) → 3 **Walkout** (O2O) → 4 **BOPIS** (Click & Collect) → 5 **Preferred warehouse** → 6 **PostCode2XDock** → 7 **Region warehouse** → 8 **Delivery Mode WH** → 9 **Division warehouse** → 10 **POS warehouse** → 11 **Site/Store default**. (External 3PA is code only, not relevant to the team.)
- **Walkout order**: a customer in a store wants a SKU the store lacks; staff help buy it online and it is **delivered to the customer's address**. Three conditions: (1) **ENABLE_PREFERRED_SELECTION_FOR_WALKOUT_WAREHOUSE = true** in **o2oConfig** at site or store; (2) **deliveryMode.walkOut = true** on the chosen delivery mode; (3) the warehouse is in **deliveryMode.partnerWarehouses** and **site.posWarehouses**. Example website **vn_ea_swl_epp** → Administration → **CMSSite.o2oConfig**: ENABLE_WALKOUT_IN_ADDRESS_STO… = true, ENABLE_PREFERRED_SELECTION_FO… = true, ENABLE_WALKOUT_WAREHOUSE_IN_A… = true, REQUIRE_ADDITIONAL_INFO_ON_CART = true. Delivery mode **Walkout SWL MX [vn-o2o-SamsungSWL-walk-out-MX]**: **ZoneDeliveryMode.walkOut = True**, Vendor id = walkout, partnerWarehouses include WV27-S520 MX_eShop Lotte HAN. Website **POS Warehouses**: WV10-S552 Extended Warranty, WV27-S520 MX_eShop Lotte HAN.
- **Click & Collect (BOPIS)**: **deliveryMode.clickAndCollect = true** → **order.pickupPointOfService ≠ null** → **pickupPointOfService.warehouses not empty** → hasStockForOrderInWarehouse(order, [WH_POS_WH]) = true. Delivery mode e.g. **Store Pickup [vn-o2o-pickup]**. For O2O orders the warehouse comes **only from the chosen point of service**. Backoffice → Base Commerce → **Point of Service** (e.g. **SDV**, SEV_TN) → Location → **Warehouses**; SDV currently has **no warehouse** (the sub once asked to **remove the warehouse from the POS** so customers cannot pick up there). Typical tickets: **add a warehouse to a POS** or **remove one**.
- **Preferred → PostCode2XDock → Region**: **PostCode2XDock** maps the delivery postcode to a dock warehouse (when no division mapping). If a valid X-dock exists the warehouse comes from it with **no fallback** to site/store/POS warehouses; it is skipped when a higher level matched (External, Marketplace, Walkout, BOPIS, Preferred), a division mapping exists, or there is no record for the postcode. **Region**: Backoffice → Internationalization → **Regions** (ISO Code VN) → e.g. **Thành phố Hà Nội [VN-HN]** → Administration: Region Virtual Warehouse (VirtualWarehouse-North), **Warehouses** (WV24-S552, WV35-S520 MX_D2C_Home North 8%, WV27-S520 …), **Site-Warehouse Ordered Mapping** (siteToOrderedWarehouseMap, 81 rows, e.g. INTERNAL-sevt → WV05-S520 MX_D2C Master). Rule: if **region.siteToWarehouseMap** has a row for the order's site → use those warehouses (default = true); else **region.warehouses** ∩ the site/store warehouses, default = true.
- **Division warehouse** is used by no country. If none of levels 1–10 matches, **BASESTORE.warehouses** is the fallback. Warehouses are set at **base store**, **website**, **region** and, for walkout, the delivery mode's **partner warehouses**. No questions.

## Difficult points and open issues
- The **soft launch on production** step for new payment modes was not specified (where enabled, who checks).
- The multistore popup "Edit item vn_ea_swl_epp" lists payment modes that differ from the same-named website's CMSSite.paymentModes; unclear which object is the multistore and which level truly applies.
- Trade-in cronjob details (schedule, trigger, child-catalog sync for T_SKU) not yet on the page; TH (Remobie) has no cronjob listed.
- The 11-level warehouse order is complex; Preferred, Delivery Mode WH and Division were not demoed; whether warehouse priority level is needed per country is unclear.
- Removing a warehouse from a POS disables pickup there – easy to confuse when investigating pickup orders.
- PostCode2XDock blocks fallback: wrong X-dock data sends an order to the wrong warehouse without falling back.

## Next steps
- Read Payment Mode Configuration and Trade-in Integration Overview, Tech COEC team (SUB's Functionality Wise Distinguish), KB – [MY] Trade-in Customer Journey and Warehouse fulfillment for an order.
- On staging open a VN payment mode, check the 3 display conditions, and follow the website / multi-store / base store filtering.
- Build checklists: add/remove warehouse for a POS, new payment mode (clone, staging test with NERP, soft launch, live).
- Ask Manikanta: how to soft launch a payment mode on production, the full trade-in cronjob list (schedule, trigger, catalog sync) and TH Remobie, which warehouse level VN uses, and what the multistore popup represents.
