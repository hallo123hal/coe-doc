# CoE Meeting Notes – Handover Day 3: Overtrade (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486599681
Afternoon of 27/10/2026, Merchandising session (recording ~minutes 63–72, 9 min). PIC Ong Hee Hui (Irene Ong, SDSAP) presented the template and checks; Chong Haw Eong explained the bonus and country usage. Reference KB: [NZ] Enhanced Overtrade. ~18–21 attendees.

## What overtrade is
An **extra amount added on top of the trade-in value**, MX only. MSA sets the base trade-in price; when a subsidiary wants a boost for certain SKUs over a period, CoE sets overtrade. It shows as an "overtrade bonus" under the trade-in line in the cart and can be tied to the main SKU, an amount and a service product (a specific old device, or any Samsung device).

## Upload file
Download the master catalog from TRADE_IN_DEVICE_PRICE and fill: Offer ID (unique, traceable), applicable VariantSKU, SamsungDiscount (the boost), OpenPromotion (always TRUE), StartDate / EndDate, CMSSites, serviceBasedProducts (T-SKUs such as `T_PHONE_APPLE…`). **Start and end dates are in the subsidiary's local time (NZ: NZT/NZDT), not UTC** – the only upload that does not use UTC. T-SKU lists for other countries come from the trade-in session.

## Checking after upload (Backoffice)
Base Store (e.g. Toko NZ Store) → **Added Service Configs** → each subsidiary has its own trade-in provider (NZ = ASSURANTV2) → Discount Configuration → find the Offer ID. Verify discount amount, start/end, T-SKUs, applicable sites, external discount config "open discount" = TRUE and main products. A cronjob cleans up expired configs.

## Q&A
- Not every country uses overtrade; some still use promotion rules for extra trade-in discounts – align with the subsidiary and RHQ (these are controlled discounts).
- Does **not** apply to Vietnam; SAVINA trade-in/overtrade will have its own session.
- The heaviest MX user is the **Philippines** (provider per the speaker: Bolttech); its config is under Added Service Configs like NZ.
- Overtrade applies from its start date; whether QA can test earlier with the promotion simulator should be confirmed in the QA session.

## Next steps
Read KB [NZ] Enhanced Overtrade and get the template; remember local-time dates; ask QA how to test before the start date; follow up on the SAVINA session.
