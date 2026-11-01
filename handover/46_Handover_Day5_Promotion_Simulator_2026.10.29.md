# CoE Meeting Notes – Handover Day 5: Promotion Simulator (2026.10.29)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2489221223
Sub-pages (personal notes, not summarised in detail): NgaVT – Setup Promotion Simulator (2489516470), Ayu (2489942231), Thanhvd (2489254446), TungNS (2489057837), Quynhltn (2489942254).

Meeting: HELD on 29/10/2026, recording starts 17:11 (about 45 minutes). Group: Promotion. Chair/presenter: Woody Yoo (SDSAP, QA, PIC); an unnamed SDSAP QA member gave the live demo. BiPlus: all CoE members (Merch, Tech, QA). Materials: deck **BIPLUS_Handover to QA Team.pptx** (12 slides) and PDF **CoEC QA Promotion Simulator** (17 pages). Reference (Samsung Confluence SEAORHQ): *Promotion Simulator Guide* (323376136). Related: Day 3 Promotion Rule and Pre-order (see 05_Handover_Day3_Promotion_Rule_and_Pre-order_2026.10.27).

## Main content

### 1. CoE QA process and promotion types to check
**Jira workflow and QA scope (01:00–02:20).** Jira operation workflow (Project Country, Shop Merchandising): Planning → Planning Review (Approved / Not Approved) → **Setup at Production** → **QA Review** → Review Setup → L.V. Approval → Pending Launch → Launch Verification → Closed.
- At QA Review: the **Merch PIC sets up the promotion in a restricted environment using a testusergroup**, does level-1 QA, then moves to QA Review. CoE QA checks with **(1) Promotion simulator** and **(2) QA** (UX/UI, promotion, price, user journey, Flagship, UAT).
- Promo simulator has two versions: **Staged** (before Knox approval) and **Online** (after the subsidiary approves; front-end check).
- QA requires **RHQ registration for backoffice / testers group**. **UAT** is used when RHQ or Merch has a migration (coupon migration, delivery mode…).

**Promotion checking (02:20–05:40).**
- **BOGO**: gift auto-added; each eligible Main SKU gets **exactly 1** gift; result per SKU or per cart; a gift may also be triggered by a **voucher**. Check **Staged** first, then the front end after approval.
- **Voucher (now coupon)**: **SKU discount** (right % / amount) and **cart discount** (cart threshold e.g. 1M or 10M VND); also check **promotion text** (changes with Black Friday, Cyber Monday, local festivals).
- **PWP**: main product + designated SKU (e.g. tablet + Buds) → second SKU gets the exact discount.
- **Trade-in boost (over-trade)**: extra trade-in deduction only on valid SKUs, exact amount.
- **Tier discount**: purchase thresholds (e.g. 5M / 10M VND); check voucher amount and front-end text.

**QA checklist for Reward Boost (05:40–06:30).** Not testable on the front end (QA has no rewards). QA **checks the promotion rule in BO before publish** and records: Rule, Applicable sites, Qualifying SKU, Start/End Date/Time (sub's **local time**), Boost Discount (%), Minimum redeemable Points (dollar value), Rewards Boost max Discount (dollar value), Promotion Text. Send BO screenshots to the **subsidiary to confirm**, then go live.

### 2. Promotion Simulator
**Guide: notes and opening (06:30–10:00).**
- Promo sim is in effect a **cart page check** for Free Gifts (BOGO), PWP, Bundles, Buy More Save More, Vouchers, Special Price. Gift Selection SKUs (from the Add-on page) on LIVE must be added via **API**; reopen the session after long idle.
- Open: BO → **Administration Cockpit → Samsung Backoffice Extension → Promotion Simulator**. First time: download and run the **Samsung HBE installer** (Download Promotion Simulator App Installer); the background icon must be running.
- Choose **Country**, **Catalog Version & Site** (Staged = before approval, shows future promotions; Online = after approval; eStore / EPP / SMB / EA).
- **Date is in Malaysia time (GMT+8)** – convert to the sub's timezone (Vietnam is 1h behind: promo ending 21:00 VN → enter 22:00). Pick a time a few minutes **after the start**.
- Copy SKUs from the Jira ticket → Add → select SKU (check all pages) → **Simulate**.

**Testing and evidence (10:00–12:24).**
- Simulate opens the **cart page** under the testers group; session info at top right. Enter voucher/coupon; special price shows by default.
- **Unavailable / OOS** SKU → session fails; **remove the SKU** from the simulator and rerun.
- Evidence: because of a system bug, screenshots do not work immediately; **open a new tab** then capture; note site and discount amount. **Do not close the Main Tab**.
- Stackable promotions (e.g. first-time user 5%) change the price; QA recalculates.
- Q&A: removing a SKU and refreshing does not keep it; re-adding means rerunning.

**Live demo (12:24–19:00).**
- Hybris → Administration Cockpit → **Samsung Backoffice Extension** → Promotion Simulator (hbe.ecom-stg.samsung.com). Menu: Pricing Management, Super Sync, Promotion Simulator, Bulk Update, Trade-in, Delivery Mode, Flagship Progress, Samsung Care +, Gatekeeper.
- Access to HBE: ask RHQ to add you to the **testers group** (also for staging) via a ticket; once approved you get credentials.
- Example **Toko MY Store**: Select Sites (Staged/Online); **Samsung MY** = eStore, others EPP (e.g. EA). Add SKUs through **SKU Search** (Solr / Database).
- Simulate as **Anonymous** or by **email** (logged-in state). A **stock-check tool** filters SKUs before simulating.
- Results: tab **Positions & Price** (Entries, Total Price, Below Margin) and **Promotions Engine Results** (which rule fired, discount); after applying a voucher click **Get Current Cart**. **Special price is not shown** in engine results (not triggered by the promotion engine).
- Can go up to the **payment page**. eStore: Home, BC, PD page; **EPP: cart to checkout only**.

**Special price QA via report (19:00–22:00).** A daily **special price report** is emailed (Excel: Catalog, SKU, Website, ApprovalStatus, SaleStatus, PriceType, Currency, Price, StartDate, EndDate, LastUpdateDate…), times in the **subsidiary's time**. Download Merch's setup file from the Jira ticket and **VLOOKUP** against the report per site and day; match → mark QA valid on the ticket, mismatch → tell Merch / ask the sub. To receive the report ask tech to add recipients (a Jira ticket exists for adding QA and Merch).

### 3. Q&A
- Simulator goes to checkout and **payment** but **cannot complete the order** (no order number). Indonesia has **bank discount / rebate**, so QA must reach bank selection.
- Each ticket is tested **at least twice**: Staged before approval and the front end after approval (Online simulator or production directly).
- Passes on simulator but fails after go-live: rare; if nothing changed, Online follows Staged. If it happens, **tech investigates** and Merch rechecks BO. After push to production still check on production, only up to before payment.
- **Anonymous** = guest, **eStore only**. EPP is for selected users, so use **email**; the email must be **whitelisted** (ask RHQ). eStore can use a real customer account; for BiPlus the EPP email is **unclear**, ask RHQ.

### 4. Flagship/AEM QA via WMC (24:30–28:30)
- QA of flagship launches uses **Samsung WMC** (Website Management Center): register online, log in with SingleID. WMC has **P6 AEM** with groups Global, Europe, America, **QA** (QA, Preqa, Preqa2, Preqa3, Preprd, PreUS), Request, China, **Flagship** (Author, QA…), Dotcom Operation Jira (P6), Samsung.com Guide.
- P6 previews AEM / UI-UX before live; AEM setup gets a separate session. RHQ must set up a dedicated **secure laptop** before flagship QA. Choose the country (e.g. Vietnam); the QA URL comes in the ticket. Access must be **requested** (VN team still waiting).

### 5. After QA
- QA types: **UX/UI**, **Price** (special price, RRP), **user journey** (SC+, trade-in), **promotion**, **UAT** (regression when subs/RHQ change process or other teams change code).
- After QA move the ticket to **Review Setup** and reassign the reporter. Future promotions: sub approves (**L.V. Approval**) → QA sets **Pending Launch** → **on the live day** QA verifies the front end (e.g. live 01/11 → check on 01/11). Defects go to tech or the setup team.
- **SOP Negative Testing – QA** (Confluence page "4. Negative Testing – QA" under "1. SOP – QA", by Woody Yoo): attachments **QA Sharing_Positive & Negative Scenario Testing.pdf** and **Negative Testing checklists.xlsx**; checklists by type: BOGO (a–k: right time, right website, child SKU filter, OOS/priority, duplicate gift, message, stackability, random SKU…), PWP, Fixed Discount, voucher… Example: sub wants 10% off one SKU but an old voucher may still apply to others; QA tries an **invalid SKU** (e.g. washing machine) to make sure it does not trigger. Negative tests work on Staged too.
- Only **Promotion Simulator** is used from HBE; the app installs on **Windows laptops only**, **not on Mac** (security). Session ended at 44:40.

## Difficult points and open issues
- Access: RHQ must add the team to the **testers group** (BO, HBE), **email whitelist** for EPP, **WMC** registration and **secure laptop** for flagship QA; WMC still pending.
- Windows only; input time is **GMT+8**, convert for each sub.
- Orders cannot be completed in the simulator; reward boost is checked in BO only.
- OOS SKUs break the session; screenshots need a new tab; never close the Main Tab.
- Special price is absent from engine results → QA via the report (VLOOKUP) and being on the recipient list.
- Unclear which email BiPlus uses for EPP and who issues it.

## Next steps
- QA: request from Woody Yoo the deck **BIPLUS_Handover to QA Team.pptx** and the PDF **CoEC QA Promotion Simulator**.
- Raise tickets with RHQ: testers group, EPP email whitelist, WMC, secure laptop.
- Ask tech to add QA and Merch to the daily special price report.
- QA: prepare a Windows machine, install the **HBE installer**; read the Negative Testing page and checklist; ask SDSAP about the stock-check tool.
