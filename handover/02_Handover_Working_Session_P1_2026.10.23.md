# CoE Meeting Notes – Handover Working Session P1 (2026.10.23)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2481559662

Meeting: first handover session from the current CoE team (SDSAP) to BiPlus, 23/10/2026 afternoon on Teams (~73 min). Chair Boon Kiat Teo (SEAO RHQ); presenter Chong Haw Eong (SDSAP). Also attending: Oliver Leung (RHQ), SDSAP members, and BiPlus leads (Dinh Minh Quoc, David Bui, CoE VN team leads). RHQ confirmed only leads need to attend and pass knowledge on. The page follows the recording with per-section screenshots and the original script.

## Five handover topics (all under "Operation CoE" on Confluence, split by Merchandising, Tech, QA, 3PD)
1. Jira operation and detailed workflow (Shop Merchandising v3, COEC v3). 2. SOPs for Merch, Tech, QA. 3. Templates used with subsidiaries. 4. BVT SOP and staging/test data. 5. Jira dashboards and filters.

## Jira – Shop Merchandising (8 country projects)
- Subsidiary raises ticket in its country project, fills mandatory fields, attaches documents, sets **APPROVED-ES** (or NOT APPROVED). The CoE sub-lead reviews and assigns a Merch PIC by workload/capability. Tickets not approved within **5 working days** are closed; the subsidiary must raise a new one.
- Mandatory fields: Request type = Shop Merchandising (Maintenance Request is for L2/L3); Priority High/Medium/Low only; Component (pricing, promotion, product, XC+, remote changes…); Label (flagship, complexity, PIC); summary/attachments; Status Approved before execution; Assignee = sub-lead (subsidiaries must not assign members); target date and promotion brief.
- Priority/SLA (working days): High 1 day (data security impact, loss of sales); Medium 2 days (single promotion, complex requests such as multistore setup, site/access management, whitelisting, campaign); Low 3 days (tickets bundling many promotions, e.g. a whole month). Reporters nearly always pick High, so the sub-lead reassesses before assigning; Chong Haw Eong reviews priorities weekly before reporting. No formal RHQ guideline; it has worked this way for 4 years.
- Linking: use More → Link so related earlier tickets are visible.
- Workflow statuses: Planning → Planning Review → APPROVED-ES → STG SETUP / PRD SETUP → QA REVIEW → REVIEW SETUP (reporter checks evidence and comments a green light before Knox approval) → PENDING LAUNCH (future-dated, QA on go-live day) → L.V. APPROVAL → LAUNCH VERIFICATION; ON HOLD RHQ / COE / SUBS; INVALID (not approved and aging, duplicate, cancelled, no CoE action).
- On-hold rules: ON HOLD RHQ for multistore requests, requests against regional guidelines, new multistore setup (continue only with written approval on the ticket); ON HOLD SUBS for unclear/duplicated/mismatching info (weekly list to subsidiaries; no reply in 5 working days → close); ON HOLD COE for Tech help (user groups, coupons) via a COEC ticket. Subsidiaries often reopen closed tickets by changing status – SOP is to refuse and ask for a new ticket.
- Knox approval submission (summary of detailed wiki SOP): for price, check file name/content, no spaces around SKUs, never edit the template (return discrepancies to the subsidiary), submit via the correct approval line, never add/remove approvers (needs a separate ticket), set On Hold Subs while pending, then sync data, front-end QA, Review Setup. For promotion, CoE builds the rule to match the approved request, publishes after approval and sends to QA. The VN team noted it has not been trained on the Knox tool; the session explains only the existing workflow.
- QA methods: promotion simulator (most common; publish to preview promotion module and check by time/site/SKU), test user group, Hybris special price report, live QA for ongoing promotions, finance price calculation tool for special price rules. No-QA tickets (Merch self-check with evidence): product activation, warehouse/stock setup, multistore config change, remote changes, multistore access management that cannot be verified on the front end. Mandatory QA: any upload template, price approval, external services (XC+, QF code), price rules, new/changed promotions, product-related changes, AEM CMS and Shop App CMS. A daily filter detects tickets that skipped QA.
- SLA counts: APPROVED-ES, STG SETUP, PRD SETUP, QA REVIEW, ON HOLD COE. Excluded: Planning/Planning Review, Not Approved, On Hold Subs/RHQ, Review Setup, Pending Launch, L.V. Approval, Launch Verification, Closed.

## Jira – COEC (Tech)
- Project COEC (COEC-n), issue type Maintenance Request; component/sub-category mandatory but often wrong (team fixes for reporting); priority P0–P4 (subsidiaries over-pick P0/P1; P0–P4 definitions agreed with RHQ will be added to the deck); assignee usually a shared mailbox; descriptions are often just a screenshot, so daily follow-up is needed; link previous tickets for recurring issues.
- Workflow: NEW → ASSIGNED → IN REVIEW → SUBSIDIARY / SYSTEM SUPPORT (L2/L3: code change, hotfix, RCA) / ON HOLD ES (another project must grant access, e.g. AUTEU) / ON HOLD RHQ → IN PROGRESS → QA REVIEW (not needed for e.g. back-office access or user-group creation) → L.V. APPROVAL → LAUNCH VERIFICATION → CLOSED. SLA counts New, Assigned, In Review, In Progress, QA Review.
- 3PD (middleware team) uses COEC with a similar process. Last-minute/urgent requests have a dedicated SOP; the VN team may update outdated SOPs after aligning with RHQ.

## Merchandising Operations Handbook
Merch handles about 60–70% of workload. Key rules: requirement review and a no-assumption policy (check ticket, related issues, approvals, country, SKU, change type, promotion mechanics, eligibility, dependencies); Jira is the single source of truth (chat, phone, WhatsApp don't count); On Hold and Pending Launch must not be used to dodge SLA (always comment the reason); template/setup governance; complete evidence before handover.

## Templates, documents, test data
- Standard templates built with subsidiaries; some have macros and are encrypted (Chong Haw Eong to decrypt and upload). Most used: XC+ (with change log), Benefit, Promotion, Multistore new site. A separate session is needed.
- Also: Merchandising BVT guide, input content guideline, generating staging access, per-country test data sets (accounts, payment data, URLs), AEM author copy and pre-QA AEM access.
- Hybris issue monitoring: promotion rules often deactivate on their own; a daily report triggers republish and approval resubmission. Internal training recordings and the Merchandising knowledge base (section 10) exist.

## Dashboards and SLA tracking
Official dashboards: SEAO Shop Merchandising, last-minute/urgent, aging, COEC and Tech aging, QA dashboard (tickets stuck in QA by days, QA Review/Pending Launch by member). They are built on official filters listed on Confluence; the VN team is free to build its own. There is no SLA tool: SLA is calculated manually from the Jira status-transition export in Excel.

## RHQ SOP series, QA and Tech documents
- SOPs (RHQ-approved): Knox approval submission, RNPL SKU archiving, running promotions in campaigns, 3PD, etc.
- QA: QA Returned Policy (weekly return rate by team/PIC), ticket flowchart, cross-checking, negative testing required, training/onboarding, QA tools and promotion simulator guide.
- Tech: approval process (PC ticket), COEC workflow, order validation, Knox approval path changes when subsidiary members join/leave (very common), daily order monitoring; most technical content is in the knowledge base. Impex/scripting library and BVT results handed over later.

## Q&A and next steps
VN team asked to walk through each Confluence page next time (agreed). Action items: Chong Haw Eong to add country project names, COEC P0–P4 definitions, fix dashboard sharing, upload the deck and decrypted templates by end of 23/10; arrange a template session; VN team to read the handbook/SOPs, gather questions, and set up Jira-export SLA tracking, aligning workflow/SOP changes with RHQ.
