# Day2 - Wed-28-Oct 14:45 Room A - Part C #4 Shop App content management

> Merch services in this session: MER-SAC-01 | BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP

## Services in this session (Tier 1)

| Tier 1 # | Service | Name | Prio | Sprint | Owner | ~tickets/mo | Service Pack (BiPlus Wiki) |
|---|---|---|---|---|---|---|---|
| 26 | MER-SAC-01 | Shop App content management | Optional | Sprint 4 | Tùng | 34 | https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483631521 |

## Session: Part C #4 - Shop App content management

| Field | Value |
|---|---|
| Part C item | #4 - Shop App content management |
| Call plan | Added: Wed 28 Oct 14:45, Room A |
| BiPlus mapping | MER-SAC-01 Shop App content management, Tier 1, Sprint 4, Optional. |
| BiPlus PIC for the item | Ayu |

**What to ask SDSAP (from the sheet):** A session and the KB page.

## MER-SAC-01 - Shop App content management (Tùng's service)

> Tier 1 #26 | Optional | Sprint 4 | Owner: Tùng | QA: Xuan, Nga | ~34 tickets/month | M5 Banner & Site content

**BiPlus Wiki (Service Pack):** https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2483631521  
*Summary of the condensed v0.2 pack, revised 25 Oct 2026. Re-read the page before the session.*

Focused notes for this service: [Day2_Wed-28-Oct/1445_RoomA_MER-SAC-01_shop-app-content.md](../../Day2_Wed-28-Oct/1445_RoomA_MER-SAC-01_shop-app-content.md)

## What the service does
Samsung **Shop App** content (home KVs, banners, widgets, offer KVs, campaign sets, voucher/benefit display) is set up, rotated and removed in the Shop App CMS on Android (AOS) and iOS, for the areas Ops COE may edit. The service also **triages every daily Shop App QA finding**: fixes what COE owns and routes the rest the same day.

## Key facts
| Item | Detail |
|---|---|
| Priority / sprint | Optional, Sprint 4 (Tier 1 #26) |
| Volume | 320 tickets in 2026, ~34/month. >50% are daily QA findings (TH and AU most), the rest content requests (AU and MY most) |
| Roles | Doer: Shop App-certified Merch operator. Checker: peer check on AOS and iOS. Approver: Shift Leader; ASC then Suwon Office approve content where the policy requires. For findings, the QA owner retests and completes its own ticket |
| How it arrives | Content: Shop Merchandising ticket in the market project. Findings: issue type **ASC_Operation QA Request** (NEW, COMPLETE, CLOSED), titles like "[TH] [Daily QA] [Offer] [AOS & iOS] ...\_D\_051" |
| SLA | Low: 24h resolution, 2h initial (internal 15h36 / 78 min). Findings: triage within response target (SLA table for ASC_Operation QA Request: confirm in KT). Wrong offer claim / blocked purchase -> MER-INC-01 |
| Change class | Standard, R1; no QA Team gate (Shift Leader checks evidence); no PC ticket; Knox only for the linked voucher/promotion |
| Biggest risk | Editing content COE does not own; dead link, past date or pre-order asset live in the app; offer shown before its promotion is live |

## Ownership matrix (Shop App operation policy, SEAO-ASC, 2026-09-10)
| Area | ASC | COE / Subs |
|---|---|---|
| B2C Home | edits | **not allowed** (PTK only since 01/01/2026) - route to ASC |
| B2C Offer | edits | allowed: RTB no approval; category filter and KV image changes need approval (ASC then Suwon Office) |
| B2C Shop | edits | allowed with ASC approval |
| EPP Home / Offer / Shop / Account | edits | allowed |

Never edit content COE does not own. Approval chain for an Offer local campaign: asset -> ASC 1st approval -> Suwon Office 2nd -> ASC EC team publishes; submit one week ahead; if ASC/HQ do not answer within 24h after the Jira post, comment the ticket and go live (template E). Urgent: Knox room "ASC Urgent Ops Room", approved after live.

## Variants
V5 daily QA finding (~55% of tickets) - V1 weekly offer rotation (AU, "Offer Rotation") - V4 voucher/coupon/benefits display (MY monthly live-commerce vouchers) - V2 content on COE-editable areas - V3 campaign set across stores - V6 scheduled expiry / phase switch (teaser, pre-order, buy, extension).

**V5 categories:** A content entry (wrong/dead link, KV not clickable, missing/duplicate, past date, pre-order asset in buy period) - COE fixes at once. B asset/copy (copy-image mismatch, numbers in head copy, wrong asset for phone/tablet) - ask owner for corrected asset. C app behaviour (pop-ups, disappearing widgets, CTA rendering per platform) - route to Tech by linked COEC. D commerce data (not purchasable, wrong price, voucher not applying) - route to the right MER/TEC service.

## Workflow highlights
- **V1 rotation:** open production document + approval ticket (ASC-xxxx) -> record current entries (CMS list + AOS/iOS screenshots) -> create new KV entries -> end last week's at the new start (no gap, keep the minimum offer KV count) -> test each KV on AOS and iOS, phone and tablet -> request approval where required, publish/schedule -> peer check, Shift Leader approval, verify live per store -> REVIEW SETUP (23:59 rule).
- **V5 finding:** read and reproduce in the production app + CMS entry -> classify A-D -> post triage verdict (template D) within the response target -> fix A at once (keep before screenshot) / request asset for B / route C and D the same working day -> peer check the fix -> the QA owner retests and completes the ticket.
- **V6:** schedule every entry end and pre-order-to-buy switch (Jira due-date sub-tasks if the CMS cannot schedule); daily sweep at each market's start of day.
- **V4:** voucher *creation* is MER-CPN-01; here you only confirm it is live and set/test the app display. Do not create new `isMobileSpecific` vouchers (RHQ bans platform-specific promotions since 01/12/2025).

## Content rules
No numeric values in head copy (09/2026); no "Buy now" CTA on any KV incl. Offer KV (04/2026); Samsung Sharp Sans with special fonts for TH/VN; VN and TH have own KV templates; RTB icons 128x128.

## Access to line up
Shop App CMS role (`SHOP-CMS-B2C/EPP-VIEW / -EDIT / -REQUEST-APPROVAL / -PUBLISH`; `-APPROVE` is RHQ only) via RHQ D2C Platform Head; IP whitelist via AUTEU; STG shared OTP, PROD OTP to Samsung email; AOS/iOS test devices (Bluestacks on PC). CMS URLs: STG `opstools-s1-<cc>.seasam.org/ops-web/login`, PROD `opstools-<cc>.seasam.org/ops-web/login`. Hard freeze around Unpacked; flagship content only in Shop App Secure CMS (cleanroom, RHQ-run).

## Known errors to remember
KV opens wrong page (KE-01) - KV not clickable (KE-02) - past date on KV (KE-03) - pre-order asset in buy period (KE-04) - duplicate KV (KE-05) - fewer KVs than required (KE-06) - copy does not match image (KE-07) - CTA differs per platform (-> COEC, KE-08) - number in head copy / "Buy now" (KE-09) - category missing in app (route, KE-10).

## Samsung KB to read first
SHOP APP: in-store mode & promotion setup (2477524477) - ShopApp Voucher Display (2477688255) - My Voucher Component (2477917560) - KB - ShopApp Voucher Creation (2477458838) - GEO Location Function (2477557171) - ShopApp Category Update (GNB) (2477688507, route only). The KB has nothing on weekly rotation or daily QA - this is where SDSAP's session adds the most.

## Open points the pack marks "confirm in KT"
SLA table for ASC_Operation QA Request - minimum offer KV count (three seen) - preview/test-build method - which B2C Home module (device-upgrade widget) is editable - small Shop App items not covered by V1-V6 (GNB category update, in-store content, geo widgets, dynamic pages): ask the Sub-Lead before acting.

