# MER-AEM-01 - AEM page creation and update (Homepage, PF, FAQ, Footer)

> Day 4 - Fri-30-Oct | Owner: **Tùng** | QA: Xuan, Nga | Tier 1 #4 | Must | Sprint 1 | ~33 tickets/month | Module: M5 Banner & Site content

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483598824  
*Summary of the Service Pack page (condensed v0.2, revised 25 Oct 2026). Always re-read the page itself before the session - this is a study aid, not a replacement.*

**Note from Tier 1 sheet:** Ayu covers on site for Geraldus; Geraldus joins the AEM sessions remotely and works it with Ayu from 2 Nov.

## Session (SDSAP handover)
| Field | Value |
|---|---|
| Inventory topic | #61 - EPP CMS - Country EPP structure - All AEM component |
| Call (BiPlus plan v3) | Fri 30 Oct 10:00, Room A |
| SDSAP date / status | 30-Oct |
| Component / area | Multistore / Service |
| SDSAP PIC | Siti Sarah Binti Azman, Thananya Phattanatreekup |
| Samsung Confluence link | KB - Homepage Offer Offer Detail PF Components |
| Maps to (BiPlus) | MER-AEM-01 AEM page creation and update (Homepage, PF, FAQ, Footer); MER-AEM-02 AEM offer page with T&C; MER-BCF Buying Configurator (AEM) EPP2.0 (EPP2.0) |
| Priority | Tier 1 (MER-AEM-01 AEM page creation and update (Homepage, PF, FAQ, Footer)), Sprint 1, Must |
| Verdict | **Reuse** |
| BiPlus PIC for the topic | Ayu |

**Why this verdict:** KB page for homepage, offer and PF components.

**Questions for SDSAP (from the sheet):** Where is the EPP CMS structure per country? Campaign page and banner (MER-AEM-04 Campaign page and banner setup) is missing from the inventory.

## What to focus on in this session

- Verdict Reuse: KB 'Homepage Offer Offer Detail PF Components' matches MER-AEM-01. The topic also maps to MER-AEM-02 and MER-BCF (EPP2.0) - those belong to other PICs.
- Walk the component limits live (HD01 headline 30 / description 78, PD10 curation max 12, image sizes) and the per-country component comparison sheet.
- Resolve the pack's KT points: AEM server time zone, versioning in EPP 2.0 CMS, scheduled publication, cache purge, who approves before PRD SETUP, boundary with MER-AEM-04.

## What the service does
Homepage, product finder (PF), FAQ, footer, cart-page copy and other **standing pages** are created or updated on every site named in the brief, published at the requested market time. Most requests touch many sites at once; a wrong tile, link, price text or CTA misleads customers on the most visited pages, and temporary content left live shows offers that no longer exist.

## Key facts
| Item | Detail |
|---|---|
| Priority / sprint | Must, Sprint 1 (Tier 1 #4) |
| Volume | 314 tickets in 2026, ~33/month, 8 markets |
| Roles | Doer: AEM-certified Merch operator (language pods TH, VN, ID, MY). Checker: second certified operator (peer); QA team (QAS-AEM-01) for packs above 10 sites. Approver: requester previews revamps/new pages |
| SLA | Low: 24h resolution, 2h initial; internal 15h36 / 78 min. High 4h only via MER-INC-01 |
| Change class | Standard; no PC ticket; no Knox for page content (Knox only for a price/promotion line in the same ticket) |
| Biggest risk | Wrong tile/link/price text on a high-traffic page; PF price differing from selling price; temporary content left live |

## Recognise the ticket
Titles: *homepage, site cosmetic update, revamp, PF, cart page, FAQ, footer, create link*. A slide brief with as-is and to-be marked per page and site group, an asset zip and a list of 10-20 sites; validity period or end date for temporary content; monthly packs return with a new number (MY).

**Not this service:** hero banners/merch tiles/campaign pages -> MER-AEM-04 (boundary confirmed in KT); offer pages with T&C -> MER-AEM-02; GNB/LNB -> MER-AEM-03; Buying Configurator -> MER-BCF-04; Shop App -> MER-SAC-01; prices -> MER-PRC-01; component defects -> TEC-TSP-05.

**Two tools:** EPP homepage/offers/PF/GNB = EPP 2.0 CMS (Save > QA > Live); B2C and Buying Configurator = AEM author (WMS). Relative links in EPP 2.0 get the `https://www.samsung.com/<cc>/multistore/<store>` prefix - use the site path, not a B2C path.

Variants: V1 homepage section update (~25%) - V2 multi-site cosmetic pack (numbered, validity period, groups Internal/SRC/External/SME B2B2C/EA) - V3 PF update - V4 category/clearance page - V5 cart page copy - V6 FAQ/footer/link - V7 new standing page or image link ("help create link").

## Workflow (V1)
1. STG SETUP; expand the site list from the versioned KB group list (ask once about any site not on it); cross-check EPP sites in Hybris (Q1 active flag, Q2 `aemHomepageUrl`).
2. Build the **change matrix** (row per change, column per site group), every cell filled before editing. Pack incomplete (as-is/to-be, language, CTA, desktop+mobile assets) -> one clarification, ON HOLD SUBS.
3. Version per site labelled with the ticket key + before screenshots. Upload assets to market DAM (component sizes e.g. HD01 KV 1440x810 / 720x1280).
4. Edit components respecting limits (HD01 headline 30 chars, description 78; curation card PD10 max 12 cards, SKU only). Preview desktop + mobile against the slide; tick the matrix **only after preview**.
5. Peer check (QA REVIEW above 10 sites: one site per group + 10% of the rest, min 2). Publish at go-live (AEM: Create Workflow > Samsung Direct Workflow; EPP 2.0: Save > QA > Live), clear cache, live check one site per group in a private window (front end can lag 5-10 min).
6. Set the **removal date** / Jira due date for temporary content.

PF specifics (V3): names/images/prices come from Hybris through the Samsung API (`aem.host.value`); if the brief price differs from the site price **stop and ask** (MER-PRC-01). SKU not selectable -> check Family Change Notice / Product Detail Mgmt, Hybris approval (MER-PRD-01); sync jobs are run by Tech (`[AEM SYNC] No result returned from .com CMS API` is the common error).

## Known errors to remember
Change in author but not live (not published/cache, KE-01) - element missing on one group (page absent/inheritance broken, KE-02) - tile link errors on one site (B2C path on EPP site, KE-03) - brief price differs from PF (KE-04) - curation block refuses SKUs (limit 12, KE-05) - whole label replaced when only a number should change (KE-06) - EPP looks different from B2C (TEC-TSP-05, KE-07) - expired cosmetic still live (no removal scheduled, KE-08).

## QA checklist
Site list complete; versions before change; text equals brief in right language; images right on desktop and mobile; order/position; every CTA/link opens the right page per group; PF price and CTA state match site; unchanged elements untouched; schedule in market time; live after cache clear; removal date set; no embargoed content.

## Samsung KB to read first
KB - Homepage Components (2477686995) - KB - PF Components (2477195550) - Homepage, Offer, Offer Detail, PF Components log (2478080200) - Creating/Managing a Multistore (2477687474) - SEAU: EPP2.0 (2477687052) - market site registers (ID/PH/MY EPP structure).

## Open points the pack marks "confirm in KT"
AEM server time zone - versioning in EPP 2.0 CMS - scheduled (un)publication - cache purge procedure - who approves before PRD SETUP - whether peer-check tickets use QA REVIEW - inheritance behaviour per market - boundary with MER-AEM-04 for homepage hero/tiles.

