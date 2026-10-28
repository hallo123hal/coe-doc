# CoE Meeting Notes – Handover Day 3: Category Structure (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486566913
Afternoon of 27/10/2026, Merchandising session (Teams "COE handover session 27/10" and meeting room; recording ~minutes 55–63, 7 min). PIC Ong Hee Hui (Irene Ong, SDSAP) presented the country trees; Chong Haw Eong added the super categories. ~18–21 people. Reference: Category Structure page on RHQ Confluence.

## Category tree per country
- Level 0 = root; Level 1 = main groups (AC accessories, TV, TA smartphones/tablets, HA home appliance, MO monitor…); Level 2 = sub-groups (e.g. under accessories: smartphone, tablet, power, TV, water filter, wearable); some groups such as HA have Level 3 (laundry → top load, front load, dryer). The New Zealand file was the example; every country has its own tree on the page.
- Register every SKU under the **most specific** category (top-load washer → the top-load code; Galaxy S → TA01, not a Level 1 code).
- Category codes are also used in promotion rules (top-load promo → top-load code; all appliances → HA), depending on the subsidiary request.

## Where it goes in the upload file
The product upload file needs just three inputs: SKU (from subsidiary), base SKU and category (from the country's category structure file).

## Super categories 1–4 (Chong Haw Eong)
Trees differ per subsidiary because they were built before the current team took over, and the team kept them. Hybris always has top-level super categories 1–4: **1** = all MX; **2** = usually CE (can differ by country); **3** = external services (insurance, SC+, extended warranty, trade-in); **4** = products without price (very old EOL SKUs without RRP; Hybris data can't be deleted so they are parked there). Search categories 1–4 in Hybris to see the contents per country.

## Next steps
Download each country's category structure file; check SKU registration uses the most specific code in the right country tree. The session ended by moving on to Overtrade ("trade-in boost for MX only").
