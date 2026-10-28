# CoE Meeting Notes – Handover Day 3: Ticket Management and SLA (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2485485884
End of day 27/10/2026, in-person handover at the office. Chair/presenter Chong Haw Eong (SDSAP); BiPlus CoE VN team in the room. The 57-min Loom recording is audio only (no screenshots) and the room-audio transcript is partly unclear.

## 1. Learning from Jira history
- Search Jira by keyword (e.g. "SAVINA trade-in cronjob") to see how past tickets were handled – the fastest way to learn. SAVINA trade-in example: subsidiary requests via Knox Portal, partner confirms in the ticket, CoE runs the cronjob to import prices (the SKU must already have trade-in configured or the run fails), QA then checks daily.
- No page of common mistakes/RCAs exists; prevention is following the process and reviewing.
- Work split: tickets go to a senior, who assigns; the team is two groups of four countries each sharing work. The Philippines and Indonesia run **new Hybris** with tighter permissions: stock blocking needs a stock import override (deleting it to resync NERP needs delete rights); PH needs PIN map and TAT file uploads; overtrade bonus upload needs the product manager role. Every country has many customisations.

## 2. SLA tracking and aging
- Chong checks the Jira dashboard every 2–3 days to report and spot workflow drift (e.g. rising on-hold counts).
- **Month-end surge:** some days ~100 tickets; a Sunday go-live is often raised on Friday (possible Saturday overtime). Subsidiaries often bundle a month of requests in one ticket, creating aging.
- **Pending Launch:** e.g. ticket raised 15/9 for a 1/12 promotion – set Pending Launch and do the work about a week before go-live (earlier work gets redone). No RHQ approval needed but it must be justifiable; always comment the reason or it looks like SLA gaming. Some tickets run for months (April–December promotion checked monthly); start dates can change at any time.
- **On Hold Subsidiary:** every Friday email subsidiaries a list of tickets waiting on them and comment in the tickets. After **5 working days and at least 2 reminders** the ticket can be closed (agreed in the RHQ workflow). Nothing done → **Invalid** (RHQ does not count invalid tickets in SLA); partly done → Launch Verification with a comment. Use the standard line "please raise a new ticket for new requests".
- Don't rush to close tickets waiting on AEM sync or NERP sync failures (a new ticket goes to someone who must recheck everything); keep on hold, close after ~2 months unresolved. Consider risk before closing: a set-up promotion that is not yet live has no checker once closed – ask for it to be undeployed from the simulator if unconfirmed.
- Typical go-live: MY and PH on the 1st; SG, TH, VN first week; NZ and AU by campaign (AU weekly EPP updates); Indonesia raises tickets around the 29th–30th.

## 3. Jira as source of truth
- Every comment, assignee change and transition stays in history even if deleted; common issue is subsidiaries editing the brief after sharing. CoE only works **Approved** tickets. A senior periodically checks tickets skipping QA, wrong assignees or statuses.
- Big tickets (e.g. Thailand bundles) should be **split into several tickets** for different PICs and QA; the senior owns the main ticket, links the sub-tickets and comments on the main one. A strict SOP is needed so nothing is missed and stackable vs non-stackable requests are handled.
- QA keeps screenshot evidence the VN team can study. Align with RHQ before adding any new process with subsidiaries.
- Remote work during peaks is possible via Samsung VPN (SVPN) with management approval (access reset every 6 months).

## 4. Schedule and next steps
- 28/10: flagship setup, SC+ MX/CE (5 MX and 4 CE types), SC+ on 3PD, OOW, RNPL, AU SIM. 29/10: promotions, coupons (single code, multicode, external serial coupon, ingestion), coupon display, user groups, coupon config, Open EPP, multi login. Two Tech topics move to the next day (PIC on medical leave); next day includes hands-on ticket demos.
- Actions: browse past tickets by request type; draft standard comments (on-hold reminder, Invalid closure, completion, Pending Launch); write an SOP for splitting big tickets; schedule the Friday on-hold email; request SVPN access where needed.
