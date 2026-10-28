# CoE Meeting Notes – Handover Day 3: Benefits and BC (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486239263
Afternoon of 27/10/2026 on Teams (19-min recording). PIC Ong Hee Hui (Irene Ong, SDSAP) presented Benefit Template V4.1; Chong Haw Eong answered questions and explained setup. ~20 people on Teams. BC = Buying Configurator page. KB: KB – Benefits V4.0.

## Benefit Template V4.1 (tabs: BC Page, PD Page, Cart, Benefit Icon, Country Specific Benefit Icon)
- Subsidiary fills mandatory fields: site, start/end date (local time), eligible products, priority.
- Mapping to the BC page and limits: Flag (blue text) max 26 characters; Title max 58, black text only, no HTML; Description / localized offer text max 127, black text only, no HTML, line breaks allowed; Icon image URL 112 × 112 px. The subsidiary template is locked to these limits (Excel errors if exceeded); if the subsidiary writes the request in the ticket instead, count characters yourself.
- PD page shows only the two highest-priority benefits, however many are configured.
- Benefit Icon: subsidiary picks an icon (fill country code and icon name → image URL generated → paste in template). Country Specific Benefit Icon: country code, type (SC+, PWP, bank, Grab…) and URL; New Zealand must use its own SC+ image for legal reasons.

## How to set up in Hybris
- Two ways: manual clone of an existing benefit (CS Admin Cockpit) or **bulk upload** (recommended): Backoffice Product Cockpit → Bulk upload → search "benefit" → PRODUCT_BENEFITS → drop file → Import. The KB has sample files; rename them for the country catalog (format identical, only catalog name differs).
- Verify afterwards in CS Admin by searching "benefit" (uploaded benefits appear in ProductBenefit). Philippines and Indonesia (new Hybris) use the normal Backoffice instead of CS Admin.
- Site and timing come from the subsidiary brief; the benefit goes live on its start date (can be in the future).

## Storefront types
| Type | Display |
|---|---|
| BC no CTA | Information only |
| BC direct hyperlink | Learn more button to an external/T&C page |
| BC popup (no hyperlink) | Learn more opens a detail popup |
| BC popup with hyperlink | Popup plus another link (e.g. bank page) |
| PD page | Two lines only; optional external URL |
| Cart page | Text, or benefit with image (more attractive) |
The KB has 6 pre-filled sample files (one per type). Remove the " - BC / - PD…" suffix the wiki adds to file names before uploading. CTA vs hyperlink is the subsidiary's design decision.

## Icons, URLs and AEM
- During flagship launches RHQ supplies BC benefit images; otherwise ask RHQ to add a missing icon and get the hyperlink. RHQ has a standard URL set. For new links, ask the subsidiary to obtain the URL from its content team.
- EPP and eStore benefits use the same method; a benefit can take up to 1 hour to show (ask for a CDN purge if urgent).
- Since 2026 B2C benefits moved from AEM to Hybris; AEM Offers (EPP 2.0, Local Benefits) are deprecated from 25/06/2026. If a benefit shows twice, ask the subsidiary to check that the AEM team turned off the AEM setup. Do not set up EPP benefits in AEM.
- Hybris can't upload PDFs; for T&C PDFs, get the URL from the local AEM team.

## Next steps
Read KB – Benefits V4.0 and download the 6 samples; get Benefit Template V4.1; confirm CS Admin access (not needed for PH/ID); check AEM benefit is turned off per request; obtain recordings of Irene's later topics.
