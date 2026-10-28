# CoE Meeting Notes – Handover Day 3: Add-on Page eVoucher (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486731016
Sub-page not summarised separately: TungNS – Add on page evoucher (2486731084).

Afternoon of 27/10/2026, Merchandising session (recording ~minutes 44–54, 10 min). Presenter Ong Hee Hui (Irene Ong, SDSAP) with Chong Haw Eong's introduction and exclusion notes. Reference: KB – eVoucher Page and Promo Setup. NZ is the example.

## What the eVoucher page is
Unlike a normal add-on page (customer picks products then pays), the eVoucher page has **its own promotion**. The page calculates against the eVoucher balance; leaving with credit unused triggers a reminder. Three things to set up: **main title** (e.g. "Don't forget to use your $100 eVoucher"), **subtitle** and **eVoucher value** (title value and eVoucher value must tally). Accessories/Buds are added against the balance; the excess appears as Extra Charge. BC and PD layouts differ but setup is the same.

## Promotion rule
- No eVoucher-specific product reference – the normal accessory reference on the main device is enough.
- Conditions: **Container A** = eligible main device (e.g. Galaxy S23 Ultra, quantity 1, CONTAINS ANY). **Container B** = accessories eligible for the eVoucher; with hundreds of accessories, **create a category** (e.g. `NZHME4804_CONTAINER_B`) and use qualifying categories – listing products makes the rule too large to publish (the KB says not to use AEM_CATEGORY). Add a **product final price threshold** > 0 so free/BOGO items are skipped.
- Actions (product discount): fill the five fields in the KB (source container, target container, target product threshold…). **Quantity discount map** (container A): 1 main device = 100, 2 = 200 … 5 = 500, set per request.

## AEM additional info type data
Backoffice → Types → **AEMAdditionalInfoTypeData**. The KB shows creating new records, but in practice **reuse expired records of type Voucher** (they can't be deleted and get messy). The eVoucher needs **three records** (gift selection needs two): main title, subtitle, eVoucher value (number only, no currency). Fill unique key, start/end date, product codes (main SKU), base store, site list, **AEM Additional Info Type = Voucher**, **Enable This Type = True**, Save.

## Order and exclusions (Chong Haw Eong)
Set up the **add-on page first**, then the eVoucher page. **AU** can skip the eVoucher when the customer chose trade-in or a SIM plan on BC (they see only the add-on page). The region is moving this way (NZ working on it): skip when the customer already has trade-in, SC+ or another benefit of equal value. The subsidiary provides the exclusion logic; testing is on S2 with many sample setups.

## Next steps
Read KB eVoucher, Gift Selection and Product Reference – Bundle and Gift; get the earlier part of the session recording; use a category for container B and reuse expired AEM records; review exclusion setups on S2 and ask AU/NZ for the logic.
