# CoE Meeting Notes – Handover Day 3: Trade-in T-Base Code (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2485420533
Afternoon of 27/10/2026, Merchandising session (recording ~minutes 92–99, 7 min). Chong Haw Eong presented (schedule lists Lee Chia Yee and Tai Sheau Yann as PICs); Ira Humairah followed with RTF Override. Reference KB: Bulk Upload Product Reference; per-country T-BASE pages ([AU]…[VN]) linked from 02-18 Handover Inventory.

## Mapping a new SKU to a T-base code
- New MX SKUs (phones, tablets) that need trade-in require an **external service** at SKU level plus a **product reference** to a **T-base code**. T codes come in two kinds, T-base and T-variant; the product reference uses T-base. This is part of the fundamental setup.
- Bulk upload: Product Cockpit → Bulk upload → PRODUCT_REFERENCES, per KB – Bulk Upload Product Reference. Columns: source code (SKU), reference type **AVAILABLE_SERVICE**, target T-base code, catalog, active, excluded site (only if the subsidiary says so; most trade-ins apply to all sites).
- Trade-in has no start/end date; it lasts until the SKU is discontinued. Always mirror a similar SKU's earlier setup.

## Checking on the SKU
Update the **Staged catalog** (Master doesn't show it). Open the SKU's category system / "products referenced by this product": AVAILABLE_SERVICE → T-base code must be present, and the SKU needs the trade-in **external service type** for the feature to work.

## New T codes
T codes are imported from trade-in providers into Hybris by a cronjob (TokoSelection); the provider or the tech team prices and maps devices. CoE cannot see new T codes automatically – there is no report; only the subsidiary PIC knows. When informed, check the T code is in Hybris and set approval status, sales status (PDP not available) and enable it for trade-in. Applies to all countries **except Vietnam**, which uses a different system (covered separately).

## Next
Chong handed over to Ira for RTF Override (continuing the morning's pre-order overselling topic); the recording stops at the introduction. Next steps: read the product-reference KB and T-BASE pages, agree with subsidiaries how new T codes are announced, get the RTF Override recording.
