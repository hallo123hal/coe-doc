# CoE Meeting Notes – Introduction to SEAO CoE (2026.10.22)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2477328258
Parent: Handover Inventory from SDSAP_Meeting Notes. Child pages covered here: SOP for Managing Merchandising, Technical, and BVT Tickets (2477459637) and SOP for Managing RHQ Confluence Documentation, Approvals, QA, and BVT Support (2477264154).

Meeting: SEAO RHQ knowledge transfer (KT) to BiPlus, 21/10/2026, two sessions (phase 1 and 2). Chair/presenter Oliver Leung (SEAO RHQ), with Boon Kiat Teo; BiPlus attendees Dinh Minh Quoc, David Bui and the CoE project team. Notes written by Quý Trần Đức on 22/10/2026. The page is bilingual (Vietnamese, then English) and links both transcripts and Loom recordings.

## 1. SEAO CoE overview
- The VN team takes over Operations CoE for 8 subsidiaries in SE Asia and Oceania, in three streams: Merchandising, QA, Tech. Performance is measured by Jira SLA and compliance with approval processes.
- Stakeholders: RHQ (assigns work, monitors SLA, approves PC tickets), Subsidiaries (raise tickets, fill templates, approve setup), Suwon HQ (global rules, Shop App, PMO), L2/L3 (SDS India/Korea), Spoke dev team (its BA is the BVT contact), Team VN.
- Tools: Confluence space SEAORHQ; Jira Shop Merchandising per country (Merch/QA tickets); Jira COEC (Tech); Jira AUTEU (access requests); PC ticket (production change approval); PUMI and Knox (internal approvals); Mattermost (RHQ chat); Microsoft Teams (meetings).

## 2. What the VN team must maintain
- Confluence pages under 02 – Operations COE: CoE Team Overview (02-1), Public Holiday Support Roster, per-team member pages. Some are stale from the previous vendor.
- Monthly knowledge-base article per team on RHQ Confluence (even if an internal system exists); internal trainings must be recorded with non-expiring, downloadable links.
- Strikes (Monitoring of Breach): RCA required after an incident; human error = 1 strike, system issue = none; 3 strikes in a calendar year = permanent removal; strikes reset yearly. Running Impex/Groovy on production without the PC ticket line is an immediate strike.

## 3. Product launches
- RHQ posts an Online Content Playbook per launch; the Add-on Page defines mandatory tabs/SKUs (may add, may not omit).
- Freeze plan: hard freeze (EPP2.0 CMS – edit pages but no flagship publish), Hybris soft freeze (only approved promotion/price changes via PUMI), hot freeze 2–3 days after Unpacked (stock updates and stop-selling only). A SEAO Timeline page records the last flagship day by day.
- Next flagship clean room will be at the VN office (70-person capacity, 50 seats now): 8 subsidiaries plus D2C, Shop App, WiseWire and RHQ desks, movable wall, 4 extra meeting rooms, 20–25 core-team seats nearby.

## 4. Tickets and SLA
- SLA counts only while a ticket is in a CoE-owned status; acknowledging means changing status (comments don't count). Each team needs a Jira dashboard for unacknowledged tickets.
- Shop Merchandising workflow: Planning/Planning Review (Subs) → Approved → STG Setup (Merch, SLA starts) → QA Review → PRD Setup; On Hold COE (SLA runs), On Hold Subs / On Hold RHQ (SLA paused); Review Setup, L.V. Approval, Pending Launch, Invalid (clone to reopen). Merch and QA share one SLA.
- Operating notes: subsidiaries answer by comment without moving the ticket – team must move it back; publish at the deadline if Review Setup is not approved; last-minute requests are the subsidiary's responsibility (comment and count in the weekly report); RHQ bulk-closes tickets idle over 1 month.
- Tech (COEC): initial response = New → Assigned; SLA runs Assigned → QA Review (Tech's own check); pauses for subsidiary/RHQ/L2-L3/access waits; finish by moving to Launch Verification.
- Merch needs partial Tech help → keep Merch ticket, create linked COEC ticket, set Merch to On Hold COE (both SLAs run). Fully Tech work → move the ticket. Moving between Jira projects needs no admin rights.
- QA: no separate SLA; evidence is a PowerPoint with step screenshots (no videos in Jira, 15 MB limit); high rejection rates signal missing self-check.
- Aging: over 7 days since Approved/Assigned; Monday week-on-week report; sub-leads resolve in 2 working days or justify.

## 5. Production change rules
- Every production data/config change needs prior approval. PC ticket for any change/delete/create and Backoffice config change; single approver (Oliver Leung), no backup yet; urgent P0/P1 → message the approver directly.
- Impex/Groovy: run new scripts on staging first with results attached; every script must carry the PC ticket ID and origin ticket line; reusable scripts live in section 08 (no version control).
- No self-created cronjobs; DB managed by RHQ; new or reactivated EPP sites need the subsidiary's approval email (then On Hold RHQ), otherwise reject.
- Data queries: avoid production queries without reason; large extracts need approved PUMI then PC ticket; PII and non-PII follow different paths; no PII by email; Hybris EDM requests rejected by default.

## 6. Access and accounts
- All access via AUTEU tickets (usually raised by leads using the template); per-system naming rules; offboarding ticket on the last working day; locked/inactive (30 days) subsidiary accounts handled via ticket.
- No super admin on Hybris for the VN team (Tech may get admin later). Existing Samsung business accounts get access same day, others 2–3 days. Jira/Confluence need whitelisted static IPs (send IP, company, office, address, purpose to RHQ D2C Platform team); "Access denied – Error 16" means the IP is not whitelisted.

## 7. Pricing and promotions
- RHQ-approved templates (new product, SC+, merchandising tag, price, special price, promotion brief, delivery mode, site/EPP site). Changes must be agreed with RHQ; some files are encrypted and need re-upload.
- Promotion brief fields: scope/sites, SKU, stacking, dates, code type/prefix, discount, cart message, special cases (FOC consignment, BOGO out-of-stock). Types: product discount, FOC/BOGO, PWP, buy more save more, F-code, payment, delivery, gift selection.
- Knox approval for price and promotion; changing actions/conditions/website/dates needs re-approval at next publish, name/status doesn't. Path varies by subsidiary and division (MX vs CE).
- RHQ guidelines: use coupons instead of vouchers except RNPL; new EPP GMB guideline; long-term financing (a Singapore site) and Samsung Members have own rules.

## 8. BVT and 3PD
- BVT (business verification test before enhancement go-live): Merch and Tech only. Monthly global release; RHQ sends ticket list ~1 week ahead; CoE assigns PICs; kickoff by dev team; PIC acknowledges on ticket; test from day 1; daily Excel tracker on Confluence; bugs go to the dev team (2–3 days, Spoke BA chases); sign-off needs 100% pass with evidence (99% blocks release); RHQ checks every 2 days. Dates are non-negotiable; add country-specific cases; SEAO-wide tickets need evidence for all 8 countries.
- 3PD: team manages data flow between Hybris and 4 middleware (orders, stock, product data), not marketplaces. Needs a dedicated full-time PIC; the old vendor has only one person left, so start handover early.

## 9. Communication, next steps, glossary
- Mattermost for RHQ, Teams for meetings, batch page questions into one Excel and email RHQ, keep current practice until RHQ agrees changes.
- 13 next-step items include: finish Confluence/Jira access, send static IPs, raise AUTEU tickets, update team pages and leave roster, build Jira dashboards, agree standard comments, find a backup PC approver, choose the 3PD PIC, read templates/Impex library/guidelines/Knox, plan monthly KB and recorded trainings, control QA rejection rate, confirm clean-room seating, prepare the BVT participant list.
- A glossary defines RHQ, COEC, AUTEU, PC ticket, Impex/Groovy, HAC, PUMI, PII, EDM, BVT, 3PD, MX/CE, RNPL, GMB, strike, etc.

## Child page: SOP for Managing Merchandising, Technical, and BVT Tickets (from KT session 1)
A 23-step SOP (with Loom timestamps) covering: confirming approval path and flagship content; freeze rules (stock updates must stay possible); phase timeline and clean-room support; seating and meeting-room allocation; keeping RHQ/Ops pages current; using the Shop Merchandising ticket type (Maintenance only for L2/L3 SDS India); workflow and SLA boundaries; setup → QA → production; correct use of On-hold Subs (SLA pauses), On-hold COE (SLA runs), On-hold RHQ (SLA pauses); invalid tickets (clone, don't reopen); Pending Launch and closure; linking a separate COEC ticket for tech work and keeping the original ticket on hold; dual-SLA tracking; acknowledgment rules; tech workflow; PC tickets and mandatory Groovy/Impex ID lines; urgent P0/P1 approvals; merch-vs-tech classification; BVT evidence, timing and defect handling; communication tools (Mattermost; Google Meet default) and access. Cautions: don't count paused time against SLA, don't create unlinked tickets, don't skip PC approval, watch for workflow drift, don't delay BVT.

## Child page: SOP for Managing RHQ Confluence Documentation, Approvals, QA, and BVT Support (from KT session 2)
A 21-step SOP covering: keeping monthly knowledge-base content in RHQ Confluence (one PIC per team); recorded internal training with accessible links; using approved templates and handling encrypted files; completing promotion briefs; country-specific onboarding variations; 3PD as middleware management with a dedicated PIC; tech documentation and leave planning; QA workflow and lowering rejection rates (self-QA); approval process and AUTEU access (including offboarding); account/IP whitelist requests; RHQ-controlled changes such as EPP site creation (attach approval email); reporting/data access (PUMI, PII rules, no PII email); Jira hygiene and bulk-closing stale tickets; QA evidence as links not big videos; reusable scripts and KB upkeep; policy updates and Knox paths; strike/RCA rules; BVT calendar, matrix, kickoff and daily tracking; organising BVT pages per subsidiary or shared; escalating questions in batches.
