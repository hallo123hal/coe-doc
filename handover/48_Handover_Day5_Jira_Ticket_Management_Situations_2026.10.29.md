# CoE Meeting Notes – Handover Day 5: Jira Ticket Management Situations (2026.10.29)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2488959507
Sub-pages (member notes): TungNS – Ticket management situations (2488992227), Trangdtt – Communication tips (2489321153), Ngavt – Tip manage ticket on the Jira (2489516550).

Note: the main page is **empty** (created by TungNS, no meeting template or recording). The content below is taken from the three member sub-pages, which record the trainer's guidance in the Day 5 QA/promotion sessions (trainer "Mr. Chon", most likely Chong Haw Eong, SDSAP; see 46_Handover_Day5_Promotion_Simulator and 47_Handover_Day5_All_Promotions_Priority_Scheme). Items marked "proposed" are the note-takers' own suggestions, not confirmed by Samsung.

## Main content

### 1. Situations and how to respond (TungNS, Trangdtt)
- **Sub changes the request when QA has just started** → ask them to **close the current ticket and create a new one**, explaining that CoE has an **SLA to keep**. When QA comments, attach the **latest file uploaded by the sub** for reference.
- **Small changes** → can be done right away.
- **Sub insists something is possible but we think it is not** → ask for a **reference ticket** showing how they set it up before. **Do not say "cannot do"**, as they may escalate. Ask subs to share old tickets with the same config.
- **Busy period (e.g. Flagship) and an urgent ticket arrives** → ask the sub to **set the priority** among tickets.
- Only when **RHQ says it cannot be done** (e.g. **system freeze**) may you say it is not possible.

### 2. Promotion ticket workflow and the two QA rounds (Ngavt)
Flow: Operation Setup → Operation Self-check → **First QA (pre-live, Preview Promotion Module)** → Confirm and Submit Approval → Approval and Go-live (sync/publish) → **Second QA (live check on the Frontend)**.
- **First QA**: before approval/go-live, on the Preview module; if it fails the ticket goes back for fix and retest. Proposed scope: configuration (SKU, site, date, condition, action), positive and negative scenarios, calculation, priority/stacking, BOGO/PWP (gift, stock, checkout), coupon/BIN, quota and user limit, cart/checkout messages.
- **Second QA**: after go-live, on the live frontend, as an extra safety layer; the trainer did not say whether it is a full regression or a smoke test. Proposed minimum: promotion appears and triggers correctly, right SKU/site/customer group, right discount/free gift, no cart/checkout errors, no application outside scope.

### 3. Jira updates and SLA
- A ticket must show who is doing what, which step is done and what is next, so anyone can take over if the owner is on leave or sick. **SLA keeps running** regardless of absence; a wrong status can hurt SLA a lot.
- Information to keep current: promotion rule created and key config, QA status (handed over / testing / done), approval (submitted / waiting / approved), **Stage to Online sync**, **live check** result, and pending/blocked reason with the owner of the next step.
- Volume: at month end about **100 tickets/day** (estimate, not KPI): **promotion 60–70%**, **EPP/content updates 10–20%**, product setup and others the rest.
- Proposed QA comment template: QA status (e.g. First QA Completed – PASS), promotion rule, site/market, environment (Preview Promotion Module), test scope (positive, negative, discount calculation, priority/stacking, cart/checkout), evidence link, next action, remarks. For the second round use "Post-live QA Completed" with live frontend, time and result.

### 4. Change requests during or after QA
- Very frequent: after handover to QA or after **Submit Approval**, the sub asks to add/remove SKUs, change the scheme or conditions, costing QA **2–3 extra hours** while new tickets keep arriving.
- Answer: ask the sub to **raise a new ticket** and explain the SLA; closing the old ticket must follow the approved closing conditions (not closing it before the original request is legitimately resolved).
- Do not assume earlier QA results still hold; identify what changed and the retest scope.

### 5. Handling requests whose feasibility is unclear
1. Receive the request → 2. **Ask for a reference ticket** → 3. Review the historical setup (rule, configuration, result) → 4. Consult a senior / the technical team → 5. Reply with a clear conclusion (possible or not, why, next step). Historical tickets are also useful to QA for expected results, but check they still match the current system. Don't say "Cannot"/"No" casually, especially when the sub knows SDS did it before.

### 6. Managing the subsidiary's expectations and priorities
- Subs are under management pressure too. If busy, do not say "I'm busy"; give a **concrete response time** (within 1 h, 2 h, 3 h).
- Example phrases: "Let me check the previous setup and get back to you within two hours." / "Could you share a similar ticket that was completed previously? We will review it before confirming." / "Since the promotion has already been submitted for approval, could you please raise a new ticket for the additional changes?" / "Could you help us prioritize the tickets based on your business urgency?"
- **Flagship period**: MX (Mobile Experience) flagship work is heavy, yet CE (Consumer Electronics) still has sales targets (Thailand CE is notably urgent). Don't tell CE "we are busy with Flagship"; **ask the sub for a priority list**; subs normally cooperate.
- **System freeze**: explain the cause ("not that I don't want to help, the system is in a freeze period").

## Open questions (from Ngavt's note, to clarify with the Samsung QA lead)
- Does First QA need all positive/negative cases or only verification of Operation's outcome? Is Second QA a full regression or a smoke test?
- QA SLA for each round and when the clock starts/stops.
- If the sub changes the promotion after First QA (before approval), retest in the same ticket or new ticket, and who decides? Can a new ticket reuse earlier results?
- Mandatory QA evidence and Jira status at each handover point.
- Who sets priority when many promotion tickets wait for QA during flagship periods?
- During a system freeze, can QA still do preview testing and live verification?
