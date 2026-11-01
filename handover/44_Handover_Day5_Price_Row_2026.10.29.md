# CoE Meeting Notes – Handover Day 5: Price Row (2026.10.29)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2489352206
Sub-pages (personal notes, not summarised in detail): TungNS (2489581972), Thanhvd (2489221860), Ayu (2489288163), Ngavt (2489090463), Quynhltn (2489057690), Trangdtt (2491875404), Trangnnt (2491416990), Kienna (2491417242), one untitled (2489057702).

Meeting: HELD on 29/10/2026, recording starts 14:07 (about 44 minutes). Group: Price. Chair/presenter: Chong Haw Eong (SDSAP), shared the deck **Special Price Upload V4 (1).pptx** (12 slides). PIC per schedule: Ong Hee Hui (attendance unclear). BiPlus: all CoE members. No KB page is listed for this topic. Related: 45_Handover_Day5_Discount_Row.

## Main content

### 1. Price row (special price): process and upload template
**Process (00:00–01:00).** **Price row = special price**.
- Old process (before Knox approval): sub sends info → CoE uploads to **Staged** → QA → sync **Online** → QA again on the front end when the price starts.
- Current process (**Knox approval for pricing**): the sub provides the file, CoE **uploads exactly what the sub sent without changing content**, then **submits approval**. CoE no longer does stage/front-end QA. The template must still be understood to check files.

**RRP vs special price (01:00–05:00).** Nearly the same template. RRP has **no start/end time and no site**.
- **RRP is uploaded on the master catalog** and applies to **all sites**; never leave the site blank-vs-filled differences (do not fill site even if the sub supplies one).
- **Special price is uploaded on a child catalog, not master**, always to the **Staged** catalog (e-store, EPP, EA … per site).
- AU: the presenter first said special price goes from master, then **corrected it as wrong**: AU also uploads per catalog.

**Special Price input – what to check (05:00–08:40).**
- Columns (sample **nzProductCatalog.xlsx**): modelCode, price, currency, unit, cmsSite, minqtd, discountPercent, userPriceGroup, validityFrom, validityTo, priceType (default=SPECIAL), productGroup, channel, customerDiscountGroup.
1. Verify prices; confirm any **decimals** (Excel may display rounded numbers).
2. **No spaces** before/after SKU, price, currency … in any column.
3. **Correct currency** – the commonest error.
4. **unit = pieces**, **minqtd = 1** (minqtd 2 = must buy 2 for that price; used for **bulk-order tier pricing**, SMB 5/10; e-store and EPP always 1).
5. **cmsSite**: multiple sites **comma-separated with no spaces** (a space makes **the whole upload fail**); check names against the **multistore**. Slide: for **eStore** catalog leave cmsSite empty; for **EPP** an empty cmsSite applies to **all sites** using the catalog.
6. **Correct catalog** – taken from the **file name**: E-Store = **nzProductCatalog**, EPP = **nzEppProductCatalog**.
7. **Cell format = TEXT**; **timezone default GMT**; format **YYYY-MM-DD HH:MM:SS**; convert local time to GMT (Malaysia GMT+8 → **minus 8h** on start and end). The slide's example "NZ: Start/End time – 4 hours" conflicts with the timezone slide.
- If reusing a template, **clear all old data** first.

**Examples (08:40–12:27).**
- Empty cmsSite: price applies to **every site using that catalog**. E-store codes: Malaysia **my**, Singapore **sg**, Vietnam **vn**; **EA** follows the same rule.
- Same SKU, several periods → **multiple rows** with different ranges in one file.
- Columns I and J (validityFrom/To) must be **Text**, not Date. Example **phEppProductCatalog.xlsx** (currency PHP). **Do not drag cells** in Excel (auto-increments values).
- **userPriceGroup** is sometimes used; mostly just model, price, currency, site.
- The file price is the **direct selling price**: RRP 2,999, special 1,999 → site shows struck-through RRP and 1,999 for the period (sometimes 1 day).
- **Timezone example (NZ)**: Hybris template uses GMT+0. Price from 16/08/2024 12:00 AM to 31/12/2024 11:59 PM NZ: **NZST (GMT+12) minus 12h** → 2024-08-15 12:00:00 to 2024-12-31 11:59:59; **NZDT (GMT+13) minus 13h** → 2024-08-15 11:00:00 to 2024-12-31 10:59:59. The sub normally supplies the timezone; files must be directly uploadable.
- Jira: slide "JIRA ticket to download the file", example ticket NZHME-7015 "s.com – W12 TV Price Match" (special price file, QA cross-check file, brief attached). CoE downloads the upload file from the ticket.

**Rules and common errors (12:27–16:00).**
- You may **rename the file** (name decides the catalog) but **never edit content**; if wrong, **return to the sub**. Editing makes CoE accountable for wrong prices.
- **Catalog mistake**: sites are EPP but file named for e-store → price goes to the e-store catalog, uploads and gets approved, but **no price shows** on EPP. The list of **all sites and catalogs** exists on Confluence and will be shared.
- Check only: complete info, **correct site names**, **no spaces**, **correct date format**.
- **Frequent error**: same SKU, **overlapping time, different price** → one row **fails** (same price: the system keeps one).
- After upload read the job result: **completed / fail / partial success**; on partial success **download the log**, find the bad rows, tell the sub.
- **One line item per site** in PriceInfoChange; **max 10,000 rows per approval submit**, so large files need many submits.

### 2. Upload, approval and checks in Backoffice
- All prices need **approval**. Old deck flow: login to BO → upload → **verify pricing at the Staged catalog**: Products → **Prices** tab (price, price type, validity); BO times show in **local GMT+8**; **Price Type = SPECIAL**. Single SKU sync can be done on the product screen.
- **Bulk sync Staged → Online**: tick all SKUs in Staged → Sync → popup → pick e.g. **NZ estore product catalog: Online** → verify the cronjob is green. After sync **cart updates immediately, PDP takes a while**.
- **Edit special price** (Staged only): any change **re-triggers Knox approval**. **Remove special price** (Staged only): price row → 3 dots → Remove → Save → Sync online; if removed by mistake click **Refresh, not Save**.
- **Product Cockpit → Bulk Upload**: templates **PRICE** (for **RRP**) and **SPECIAL_PRICE** (media template **specialPriceTemplate**, handler **specialPriceBulkUploadHandler**); also TRADE_IN_DEVICE_PRICE(_SELECTION). Choose template → Upload file → Import. Results in job **tokoSpecialPriceImportJob** (SUCCESS / PARTIAL_SUCCESS / ERROR). Sample folders per catalog, e.g. Vietnam: SME, e-store, EPP, EA Retail, Refurbished, 3PD.
- Upload creates **PriceInfoChange** records (Administration Cockpit → Price Settings → Prices → **PriceInfoChange**); **submit approval** from there and track the status (e.g. **VALID**, Discount Rate %, Model PriceRow, Product Code, Price, Currency; details include User Price Group, DiscountRow & MultiStore, uploaded values). Start/end there are **GMT**; product screens show local time.
- View prices: Catalog → Products → product in the site's catalog (e.g. WW10DB7U34GBSV – vn EPP Catalog : Staged) → **Prices** tab (Valid From/To, **Customer Price List**, Price, Currency).
- **Each site has its own price group** (e.g. savinaPriceGroup). In the file **always fill site, not price group**: a row holds one price group but several comma-separated sites; the group is filled automatically.
- **Sync online** is required for the front end. After sync **PD and cart update in seconds**; **PF (listing)** takes longer to show the slash price.
- **Never create price rows manually** (Create Price Row): fields like **net/gross** are auto-filled by upload. Each product has **only one RRP**. Price type **D2C** (e.g. eaPriceGroup on vn EPP Catalog) = e-store price synced to EA (speaker not certain); others are **SPECIAL**.

### 3. Price row vs discount row (partly belongs to the Discount Row session)
- Same template: fill **price** → price row; fill **discountPercent** (e.g. 30) instead → **discount row** (Discounts of the product), **percentage only, no amount discounts**. Special price is the direct selling price.
- Both present: allowed but **the system picks the special price**; **special price always beats discount row regardless of %**. If the sub fills both, return it: **price or percentage, not both**.
- **Always on**: long-term base discount row (e.g. 30% for a quarter/year; PH usually 1 year, MY 1–2 quarters). EPP has **tiered discounts** (MY: employees 35%, other EPP 30%, affiliate 25%). On special days subs set a lower special price (RM100, always-on 30% → 70; special 65 → shows **65**); afterwards back to 30%. **E-store** usually uses only special price per campaign, **normally no discount row**.
- On vn EPP products there are **nz/ph/sg/th/vn_memberCustomerDiscountGroup** rows with **…_memberDiscount 5%**: a **site-wide member discount**; only **vn_member** takes effect on the VN EPP site (corrected several times).
- Refurbished catalog: no price setup in the example. **Toko VN EaRetail Product Catalog**: EA sites (EA Showcase, EA SWL, SWL VIP, SWL Student …) with price groups like vn_ea_swl_eppPriceGroup, vn_ea_swl_studentPriceGroup, vn_ea_swl_vipPriceGroup.
- Template always uses **site** (comma-separated); user price group fills automatically.
- **Splitting periods when a new price is inserted (35:15–40:55)**: price 100 from 1/10 to 31/12; upload 90 for 1/11–10/11 → the system **auto-splits**: 1/10–31/10 = 100, 1/11–10/11 = 90, 11/11–31/12 = 100. Inserting 85 for 9/11–12/11 adjusts the rows again (90 ends 8/11, 100 starts 13/11). This logic is **recent**; before, a new row cut off the old row. Common in NZ and AU (**price matching with offline**). It sometimes **does not work as expected** (possibly after deployments), so always verify in the system.
- **Special price is not a promotion**: it cannot be excluded from a promotion or set non-stackable; it **always stands**. A promotion (e.g. 50 off RRP) may override but there is no way to "turn off" a price row. Price row and discount row are **uploaded separately**.

## Difficult points and open issues
- **Timezone**: GMT template; subtract the right hours per country and season (NZST 12, NZDT 13, MY 8); the "NZ – 4 hours" slide contradicts the timezone slide.
- **Catalog comes from the file name**: wrong catalog still uploads and gets approved but shows no price.
- Spaces in cmsSite fail the whole file; date columns must be Text; dragging cells shifts values.
- **10,000-row limit per approval submit**; one line item per site.
- Auto-splitting logic is new and sometimes unreliable; overlapping times with different prices fail one row.
- AU information was retracted; the D2C price role is uncertain.

## Next steps
- Request from PIC (Ong Hee Hui) the deck **Special Price Upload V4 (1).pptx** and sample templates per catalog (VN: SME, e-store, EPP, EA Retail, Refurbished, 3PD).
- Get the Confluence page listing **all sites and catalogs**.
- Confirm timezone conversions per country with SDSAP (especially NZ/AU daylight saving) and AU handling.
- Get access/instructions for submitting approval from PriceInfoChange (Knox approval) and for reading logs on PARTIAL_SUCCESS.
- Attend the Discount Row session.
