# CoE Meeting Notes – Handover Day 3: Delivery Mode and Service (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2485551286
Afternoon of 27/10/2026, Teams "Handover days 3 – Tech" (recording ~minutes 65–89, end of the session). Chair Shamni Krishnan; presenter Mohammad Ashhar Mushtaq (SDSAP), working directly in Backoffice. Topic: delivery mode / service configs by subsidiary, site and product. Two sample PC tickets (delivery mode, delivery service) are on the topic's Confluence page.

## Creating a delivery mode
Subsidiary requests a new mode → **clone** an existing one in Backoffice (the subsidiary usually names the mode to copy; or choose one, e.g. split "my-delivery-installation" into a refrigerator-only copy). All configuration is copied and the mode is attached to the same base store and sites, but the new mode is created with **active = false**; adjust and enable it.
After cloning you must still: assign the mode to the **SKU** (Tech or Merch) and create the **delivery cost** (cloning does not copy it; use manual entry or ImpEx).

## Configuration levels and fallback
| Level | Backoffice location | Note |
|---|---|---|
| SKU | Product → Administration → Delivery Modes | Mandatory; a mode not on the SKU never shows |
| Website | WCMS → Website → CMSSite delivery modes | Empty = fall back |
| Multistore | Site's multistore config | Some sites set it here |
| Base store | Base Commerce → Base Store → Delivery Modes | Mode must exist here to be usable |
Fallback order: website → multistore → base store. What the customer sees is the **intersection** of SKU modes and the modes from that order (3 on SKU, 5 on site → 3 shown). For "delivery mode not showing" tickets, check SKU, site, multistore, base store in turn.

## Delivery cost by postcode
Postcode enablement lives in the mode's Delivery Costs: one PostCodeRange row per postcode (start = end) with price. For "postcode has no delivery mode", use the Confluence script (to be added by Ashhar) to list a mode's postcodes, then add the missing one. Before creating a PostCodeRange, search the table for an existing identical row and reuse it by PK.

## Delivery services
A delivery service (e.g. `my-tv-installation-basic-setup-0-59`, named by size range) attaches to a delivery mode and holds eligible products (Online catalog only), tax class, price, ERP code, and the "Disable DO split in NERP" flag (fee stays on the same DO). Assign either from the service (add products) or from the SKU's Administration tab – one-to-one. Tech does this. Display content is described in the two sample PC tickets.

## Q&A – when is a PC ticket needed?
Nearly every config change (add/edit/remove) to core site parts – base store, website, delivery mode, delivery service, payment mode, warehouse – needs a PC ticket; mandatory for ImpEx and HAC queries. Only a few small manual actions do not. Manual order remediation needs none; script-based remediation does.

## Wrap-up
The afternoon covered order process E2E, delivery mode/service, Direct EA access and GCIC. Warehouse setup per subsidiary and priority warehouse will be rescheduled (PIC absent); 3PD E2E is done separately by the 3PD team.

## Next steps
Review the two sample PC tickets; Ashhar to add the postcode script; when cloning remember SKU assignment, delivery cost, activation; raise PC tickets for core config changes; follow the rescheduled sessions.
