# CoE Meeting Notes – Handover Day 3: Auto MBO Flag and Price (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2485289223
Afternoon of 27/10/2026, Merchandising session (recording ~minutes 112–121, 9 min). Presenter Ira Humairah (Saidatul Humairah Binti Abdul Razak, SDSAP) with Chong Haw Eong's flagship example. Reference KB: Automated Addon Page Discount (Auto MBO).

## What it is
Auto MBO reads the promotion and automatically shows the **flag** (discount level, e.g. 5%/10%/30%, English only for now) and the **discounted price** (blue price shown with strikethrough) on the add-on page. Previously done by hand. Rolled out to most subsidiaries in the last flagship; still being refined; standard for flagship launches (check RHQ for the latest guideline).

## Merchandising steps
1. Create the promotion rule (e.g. buy A, get B at a price or 20% off), save and publish (needs Knox approval).
2. Create the benefit: Admin Cockpit → Benefit, new or cloned; make sure the flags are false; add the target SKUs; benefit type **add-on benefit**; save.
3. A cronjob then runs and calculates product prices, usually within about half an hour after go-live. The flag and price follow any later change of the promotion or benefit.
KB note: uploading offer SKUs through the benefit template doesn't work yet.

## Tech configuration (done by Tech, not Merch)
Four tokoconfigs must be true per country: `promotion price enable site.<country>` (MY, ID, PH…), simulated add-on pricing enabled, simulated MBO pricing enabled, dynamic commercial flag. If any is false, the front end shows nothing. If enabled but not showing: re-run the cronjob; if still missing, check the toko config admin (currency and site present) and the product price through the SKU's product reference.

## Supported action types
Percentage or fixed discounts on products and on partner products – the common forms of PWP promotions. Normal tickets rarely ask for this; it is mainly used in flagships.

## Next steps
Read the Auto MBO KB; Tech to check the four tokoconfigs per country; get the RTF Override recording and other Auto MBO config sessions.
