# CoE Meeting Notes – Handover Day 6: All SEAO Cronjob (2026.10.30)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2491580488
Sub-pages (personal notes, not summarised in detail): NgaVT (2491646308), Baopg (2491253107), TungNS (2491711892), Thanhvd (2492006606), Quynhltn (2492170301), Trangnnt (2492203071).

Meeting: HELD on 30/10/2026 (originally scheduled 14:30–15:00). There was **no separate session**: the topic was presented by Aldwin John Gavino (SDSAP) inside the Samsung Rewards recording (13:18), from 05:10 to 27:15. Group: Config. BiPlus: all CoE members. Reference: Confluence **KB – Cronjobs** (Samsung SEAORHQ page 578082942; copy in BiPlus Knowledge Base page 2478081494). Related: Day 4 All Scripting (31_), Day 3 3PD Ticket Handling and Middleware (16_). The full step-by-step detail (screens, field names, ticket numbers) is in **51_Handover_Day6_Samsung_Rewards_Enable_Rewards_for_Site_2026.10.30**; this file keeps the cronjob-specific summary.

## Main content

### 1. KB – Cronjobs by country (05:10 – 07:25)
- All active cronjobs are consolidated per country in **KB – Cronjobs**: [NZ], [VN], GCRM Cronjobs, MY Reports, **SEAU**, SEIN, **SENZ**, **SEPCO**, **SESP**, SME, SMS/SMA, TSE. Each lists **name, purpose, schedule** (e.g. SEPCO, Manila time: ph_*tokoPromoQuotaDeactivationJob every 6 h; ph_TokoGCRMPointsAllocationJob every 30 min; ph_TokoRewardsReviewCampaignInfoImportJob every 30 min).
- Cronjobs are **normally not modified**; the system runs them on schedule; Tech steps in only for incidents.

### 2. Investigating incidents (07:25 – 10:16)
- Backoffice → System → Background Processes → CronJobs. Example **tokoSalesReportJob : sg-Report-nonPII-Email-Sub-o2oSalesReport**, Time Schedule cron **0 0 6,13,17,22 ? * ***.
- **Sub does not receive a sales report** → open the report's cronjob → **Log** tab → download the log; recipients are in the Administration tab.
- **Trade-in missing items / wrong prices** → find the country's trade-in cronjob and read the log to see whether Hybris imported the provider data correctly.
- **Never rerun a cronjob without RHQ approval or a sub request.** Tech can **deactivate/reactivate** and **reschedule** on approved request.

### 3. Job categories and typical tickets (10:16 – 12:40)
- **Sales reports** (daily, weekly, bi-weekly, quarterly; the majority), **order/consignment status updates**, **trade-in data import**, **price sync**, **navigation and product sync from AEM**, **abandoned cart cleanup**, **email sending**.
- Requests: **enable/disable**, **change schedule**, **create new job**; mostly log investigation. New cronjobs on production are created **manually** after **approval**.

### 4. Creating cronjobs (12:40 – 18:35)
- Backoffice → CronJobs → "+" → job type. Two ways:
  1. **Ready type, e.g. tokoSalesReportJob** (needs a **sales query**, SQL): configure in the Administration tab – Recipients, Sales Query, delivery (**email/SFTP**), Headers (Excel columns), File Name Prefix, Email Subject/Body; Time Schedule = trigger; Log = log. Reuse an existing query when possible.
  2. **Groovy script**: **Scripting** (System → Scripting → Scripting, engine GROOVY, first line notes the ticket, e.g. //NOTE ITGC_JIRA:PC-56040 (COEC-39342)) → **Scripting Job** (Script URI = model://<script name>, Spring ID scriptingJobPerformable) → **CronJob** (Job definition = that scripting job). Example created 30/10 for AU: **au-PayToANZOrderStatusRejectedUpdateJob** (orders in PAYMENT_NOT_CAPTURED with payment mode au-PayToANZPaymentMode, placed more than 60 min before the run, set to REJECTED).
- Checks: cronjob **Active = true**; script **Disabled = false** and **Active flag = true**.

### 5. Cron expressions and rerun rule (18:35 – 20:05)
- Rerun/re-execute needs prior approval. The PayToANZ trigger **0 0 * * * ?** runs **every hour**. Learn to read cron expressions (a web cron generator was shown).

### 6. Q&A (20:05 – 27:15)
- Sales query and Groovy script are **different cronjobs**, not chained. Aldwin prefers **Groovy**: faster and more flexible than multi-join SQL.
- To change behaviour edit the script (e.g. add credit card to the PayToANZ job; add a report column in Headers). Aldwin migrated an AU report from sales query to Groovy (au-nonPII-tokoSalesReportScript).
- Sample **PC (PROD Change)** tickets: [SEPCO] Add Login Type; [SEAU] Deactivate Zip Payment Modes; AU sales report PC-34409, PC-34604, PC-35602, PC-35938, PC-39608, PC-43403, PC-43852 (PC-39685 one-time report). Typical changes: add columns, update report query, fix script errors, enable/disable jobs. Aldwin will put the most useful PC tickets on Confluence.

## Difficult points and open issues
- SG schedule: screen cron **0 0 6,13,17,22 ? * *** vs spoken "6, 1, 5 and 11 SGT" – confirm server timezone vs the KB times.
- No rerun / new job / schedule change without approval; shared jobs affect several subs.
- Script jobs need the full Scripting → Scripting Job → CronJob chain with all flags active.

## Next steps
- Read the per-country KB – Cronjobs pages.
- Practise the Groovy chain on staging (never production).
- Ask Aldwin for the sample PC tickets (PC-56040, Groovy migration, column/query changes) and cron timezone confirmation.
