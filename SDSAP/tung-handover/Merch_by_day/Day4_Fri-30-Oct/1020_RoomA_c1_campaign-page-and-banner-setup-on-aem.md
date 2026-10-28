# Day4 - Fri-30-Oct 10:20 Room A - Part C #1 Campaign page and banner setup on AEM

> Merch services in this session: MER-AEM-04 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 2 | MER-AEM-04 | Campaign page and banner setup | Must | Sprint 1 | Tùng | 54 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483697164 |

## Session: Part C #1 - Campaign page and banner setup on AEM

| Field | Value |
|---|---|
| Part C item | #1 - Campaign page and banner setup on AEM |
| Call plan | Added: Fri 30 Oct 10:20, Room A |
| BiPlus mapping | MER-AEM-04 Campaign page and banner setup, Tier 1, Sprint 1, Must: a daily request type. |
| BiPlus PIC for the item | Ayu |

**What to ask SDSAP (from the sheet):** A session and the KB page.

## MER-AEM-04 - Campaign page and banner setup (Tùng's service)

> Tier 1 #2 | Must | Sprint 1 | Owner: Tùng | QA: Xuan, Nga | ~54 tickets/month | M5 Banner & Site content

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483697164  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

Focused notes for this service: [Day4_Fri-30-Oct/1020_RoomA_MER-AEM-04_campaign-page-and-banner.md](../../Day4_Fri-30-Oct/1020_RoomA_MER-AEM-04_campaign-page-and-banner.md)

## What the service does
Campaign landing pages are created, and **banners** (homepage hero KVs, merchandising tiles, unfold/skinny banners, category, buying page, cart and PDP banners) are added, swapped, reordered or removed on every site in the brief - live at campaign start and gone at campaign end. A banner that is early, late, on the wrong site group, or has a wrong link breaks a launch or promises an offer that is not set up.

## Key facts
| Item | Detail |
|---|---|
| Priority / sprint | Must, Sprint 1 (Tier 1 #2) |
| Volume | 515 tickets in 2026, ~54/month, 8 markets (ID and VN more than half) |
| Roles | Doer: AEM-certified Merch operator. Checker: QA team by sampling rule (100% for launch-flagged sets and campaign pages); peer or Shift Leader for copy-only changes and removals. Approver: Shift Leader |
| SLA | Low: 24h resolution, 2h initial. "Urgent"/"from now" does not change priority; High 4h only via MER-INC-01 |
| Change class | Standard, risk R1; no PC ticket, **no Knox** (no price change) |
| Biggest risk | Banner live before its offer is set up; wrong link on one site group; expired banner left live |

## Recognise the ticket
Titles: *hero banner, merchandising banner, KV, unfold, skinny, campaign page, site cosmetic update (banner), remove banner*. Brief cites slide numbers of a shared deck, lists site groups (EPP internal/external, O2O, SMB, EA, 3PD), desktop + mobile assets, go-live hour and end date. The same title returns every campaign week.

**Not this service:** standing homepage sections/PF/FAQ/footer -> MER-AEM-01; offer pages with T&C -> MER-AEM-02; GNB -> MER-AEM-03; Buying Configurator pages -> MER-BCF-04 (never edit here); Shop App banners -> MER-SAC-01 (linked ticket, same go-live); the promo/price/coupon behind the banner -> MER-PRM / PRC / CPN; sites run by RHQ Platform (EA OE, Samsung Members, SESP financing EPP) or with AEM disabled -> return to requester.

**Two tools:** EPP stores = EPP 2.0 CMS (PIM > EPP v.2 > CMS > Page Mgmt). B2C and other WMS pages = AEM author. Check the site type before opening a page.

Variants: V1 hero KV add/replace/reorder (most common, ~33%) - V2 merch tiles/secondary banners - V3 buying page/cart/PDP banners - V4 campaign landing page creation - V5 copy-only change - V6 banner removal (~8%) - V7 cross-channel set (eStore, EA, Shop App).

## Workflow (V1)
1. APPROVED-ES -> STG SETUP (a comment alone is not the initial response). Send template A with go-live/end in market time.
2. **Build the banner matrix**: rows = banners (slot, position, asset, CTA, link, start, end); columns = site groups; mark where assets/links differ. Expand groups to site IDs from the versioned KB site list.
3. Check preconditions: AEM-enabled site (Q3/Q4), not RHQ-run, freeze calendar (AEM/BC hard freeze around Unpacked; EPP2.0 flagship pages locked), linked offer ticket live at the same start (Q2) - ask once if none exists.
4. Capture before state (desktop + mobile), label a page version with the ticket key. Prepare assets (desktop and mobile per banner; internal vs external variants not swapped; only approved icons; wrong text inside an image needs a corrected file from the requester).
5. Configure KV, set order, preview desktop + mobile, click every CTA. Roll out to the site group (broken inheritance = edit site by site).
6. Self-check -> QA REVIEW (or peer) -> Shift Leader approval -> PRD SETUP; publish at go-live.
7. Live check one site per group (RHQ-approved EPP test account where needed), private window. REVIEW SETUP with evidence; 23:59 no-feedback rule (template D); create the **removal sub-task** for the end date.
8. Last-minute rule: created after 17:00 VN for same-night go-live -> label `LastMinRequest` + standard comment.

## Known errors to remember
Banner missing at go-live (time zone/not published, KE-01) - old banner after publish (cache; wait 5-10 min then COEC purge, KE-02) - wrong position (KE-03) - desktop crop on mobile (mobile asset missing, KE-04) - CTA to wrong product/error page (KE-05) - external asset on internal site (KE-06) - expired banner left live (KE-07) - BC page changed by mistake (KE-10) - banner cannot be added (site AEM-disabled or RHQ-run, KE-11).

## QA checklist
Matrix complete vs brief; versions taken; right asset per group/device; position; CTA label/link per group (click test); landing products live (Q1); linked offer live at same time (Q2); schedule/end time; live check on sampled sites; removed banners gone; no BC component or embargoed content touched.

## Access to line up
EPP 2.0 CMS / AEM author account (RHQ-approved), AEM QA access via QA Auth (wds.samsung.com, ~24h), Backoffice read, VPN.

## Samsung KB to read first
KB - Homepage Components (2477686995) - KB - Offer & Offer Detail (offers_epp) Components (2477654273) - Creating/Managing a Multistore (2477687474) - market site lists: ID EPP structure (2477884136), PH EPP Structure (2477458156), MY EPP structure (2477982361), SEAU EPP site Matrix (2478113485).

## Open points the pack marks "confirm in KT"
AEM server time zone - version menu / versioning in EPP 2.0 CMS - mapping of market terms ("PDB slide") to components - whether scheduled publication is supported - QA-01 vs QA-02 conflict on the QA gate for AEM-04 (sampling vs R1 no gate).

