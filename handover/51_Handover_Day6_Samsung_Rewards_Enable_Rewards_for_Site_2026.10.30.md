# CoE Meeting Notes – Handover Day 6: Samsung Rewards – Enable Rewards for Site (2026.10.30)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2491220031
Sub-pages (personal notes, not summarised in detail): TungNS – Samsung Reward (2491449670), NgaVT (2491711870), Thanhvd (2491810150), Baopg – Enable Rewards (2491515202), Trangnnt (2492104834), Quynhltn (2491974080), Ayu (2491646458).

Meeting: HELD on 30/10/2026, recording starts 13:18 (about 27 minutes; originally scheduled 11:30–12:00). Group: Config. Teams meeting organised by David Bui. Presenter: Aldwin John Gavino (SDSAP, PIC per schedule), for Samsung Rewards and then cronjobs. BiPlus: all CoE members. After about 05:00 the recording moves to **cronjobs** (belongs to the "All SEAO Cronjob" item of the schedule; see 56_Handover_Day6_All_SEAO_Cronjob). Related: Day 5 All Promotions (47_), Day 4 All Scripting (31_), Day 6 Third Party Integrations.

## Main content

### 1. Samsung Rewards: enabling a site
**SOP and config (00:00–03:15).** KB **Enable Site Samsung Rewards (Site Level)** (KB – Tokoconfig). Applies when a sub asks to enable Samsung Rewards for a **new site** or a **running site without rewards**.
- **Prerequisites (done by the sub)**: (1) the sub submits a **PUMI** (heard as "FUME") approved by **HQ** to enable the site in the **HQ Rewards System**; (2) PUMI and HQ confirmation go to **RHQ**; (3) once RHQ agrees, the sub raises a ticket to the tech team.
- **Hybris side (one line)**: Backoffice → Types → **TokoConfigProperty**, key **toko.rewards.epp.account.enabled.<site_uid>** = **true** (manual or by Impex).
- Afterwards the site supports both **earning** and **redeeming** points.
- **It must be enabled in both places** (HQ Rewards System and Hybris). Enabling only Hybris leaves Samsung Rewards **not working**. In practice RHQ asks whether the sub has done the HQ step before approving the ticket.

**Rewards payment mode (03:15–05:10).**
- Q&A: can the Rewards screen be shown on/off? Not possible; points are needed and staging/production have none to test. Rewards are based on **tiering** (e.g. buying a Fold earns points per config).
- Instead: Backoffice → Payment Modes → **Samsung Rewards [ph-rewardsPaymentMode]** → **Payment Provider Parameters**. PH values seen: **tierCountry** = PH, **maxRewardAmount** = 100000, **contactIdOriginEppShopApp** = EPP_APP, **sendPromotionResultsForFraudCheck** = true, **objectType** = ESTORE_PH, **customerTierDetailsAPI** (GCDM loyalty rewards API URL), enrollEstoreHeaderPID …
- The KB was extended during the session with the line **Payment Mode: ph-rewardsPaymentMode**.

### 2. Cronjobs (content of the All SEAO Cronjob item)
**KB – Cronjobs by country (05:10–07:25).** Running cronjobs are summarised per country in Confluence **KB – Cronjobs**: [NZ], [VN], GCRM Cronjobs, MY Reports, **SEAU**, SEIN, **SENZ**, **SEPCO**, **SESP**, SME, SMS/SMA, TSE. Each page lists cronjob name, purpose and schedule (SEPCO example, Manila time: ph_*tokoPromoQuotaDeactivationJob every 6 h; ph_TokoGCRMPointsAllocationJob grants points for approved TokoEventSignUp every 30 min; ph_TokoRewardsReviewCampaignInfoImportJob syncs GCRM data every 30 min). Names are self-explanatory. Principle: **normally do not edit cronjobs**; let them run on schedule and enter only on incidents.

**Investigating incidents (07:25–10:16).**
- Example **tokoSalesReportJob : sg-Report-nonPII-Email-Sub-o2oSalesReport** (Backoffice → System → Background Processes → CronJobs). Time Schedule tab: **cron expression 0 0 6,13,17,22 ? * ***.
- Incident 1: **sub does not receive a sales report** → open the cronjob of that report → **Log** tab → download the log; recipients are in the Administration tab.
- Incident 2: **trade-in** missing products or wrong prices → find that country's trade-in cronjob (KB – Cronjobs) and read the log to see whether Hybris imported the provider data correctly.
- **Never rerun a cronjob without RHQ approval or a sub request.** Tech can **deactivate/reactivate** a cronjob and **change its schedule** on approved request.

**Job groups and ticket types (10:16–12:40).** Main groups: **sales reports** (daily, weekly, bi-weekly, quarterly; the majority), status updates (**order status**, **consignment status**), **trade-in data import** from providers, **price sync**, **navigation/product sync** from AEM, **abandoned cart cleanup**, **email sending**. Ticket requests: **enable/disable**, **change schedule**, **create new job**; mostly log investigation. Creating a new cronjob on production is **manual and needs prior approval**. Sample tickets will be shared.

**Creating a Sales Report job (12:40–15:20).** Backoffice → CronJobs → "+" → choose job type. Two ways: a ready job type (e.g. sales report) or a **script**. A sales report needs a **sales query** (SQL); reuse an existing query if possible, new sub requests usually need a new one. **tokoSalesReportJob** is configured on screen (Administration tab): **Recipients**, **Sales Query**, delivery (**email** or **SFTP**), **Headers** (Excel columns e.g. Site, Sales_application, product_name, product_code, Order_code), **File Name Prefix**, **Email Subject**, **Email Body**; Time Schedule = trigger; Log = log.

**Creating a cronjob with Groovy (15:20–18:35).** Example created on 30/10 for AU: **au-PayToANZOrderStatusRejectedUpdateJob** – orders in **PAYMENT_NOT_CAPTURED**, payment mode **au-PayToANZPaymentMode**, placed more than **60 minutes** before the run, are set to **REJECTED**.
1. **Scripting** (Backoffice → System → Scripting → Scripting): script **au-PayToANZOrderStatusRejectedUpdateScript**, engine **GROOVY**; first line notes the ticket (**//NOTE ITGC_JIRA:PC-56040 (COEC-39342)**). It uses FlexibleSearch (order code LIKE 'AU%', status, payment mode, date < cutoff), gets PKs, **setStatus(REJECTED)**, saves and logs success/failure counts.
2. **Scripting Job**: **au-PayToANZOrderStatusRejectedUpdateScriptJob**, **Script URI = model://au-PayToANZOrderStatusRejectedUpdateScript** (Spring ID scriptingJobPerformable).
3. **CronJob**: create it and pick the scripting job as **Job definition**.
- Checks: cronjob **Active = true**; script **Disabled = false** and **Active flag = true**. This job has type **CronJob** (unlike tokoSalesReportJob with a sales query).

**Cron expression and rerun rules (18:35–20:05).** Rerun requires prior approval. The PayToANZ trigger **0 0 * * * ?** = **every hour**. Learn to read cron expressions (a web cron generator was shown).

**Q&A (20:05–23:50).** Sales query and Groovy script are **two different cronjobs**, not chained. Aldwin prefers **Groovy**: **faster** than a sales query, more **flexible**, easier than multi-join SQL. To update, edit the script (e.g. add credit card payment mode to the PayToANZ job; add a column by editing Headers). Aldwin once **converted an AU report from sales query to Groovy** (au-nonPII-tokoSalesReportScript).

**Sample PC tickets (23:50–27:15).** Jira project **PC (PROD Change)**: [SEPCO] Add Login Type; [SEAU] Deactivate Zip Payment Modes; AU sales report group: **PC-34409** Enable New Job, Disable Old Job; **PC-34604** Add IsBulkOrderParent Column; **PC-35602** Fix Sales Report Script Error; **PC-35938** Update Report SQL Query (include au_mydeal); **PC-39608** Add 2 New Columns and Update Mailing List; **PC-43403** Add Missing Shipping_Method; **PC-43852** Add au_myer site to the SQL condition (PC-39685 one-time off-sales report). Typical changes: add columns, edit report query, fix script, enable/disable job. Aldwin will compile the most useful PC tickets on Confluence.

## Difficult points and open issues
- Samsung Rewards must be enabled in **two places**; Hybris-only gives no error but does not work. Check PUMI / HQ and RHQ approval before the ticket.
- No test points on staging/production, so the earn/redeem UI is not visible; earning logic sits in the rewards payment mode's Payment Provider Parameters (not explained one by one).
- SG sales report schedule: screen shows cron **0 0 6,13,17,22 ? * ***, the speaker said "6, 1, 5 and 11 SGT" – confirm server timezone vs the SGT/Manila time in the KB.
- No rerun / new job / schedule change without approval; shared jobs (sales report, trade-in import) affect many subs.
- Script jobs need the full chain Scripting (Disabled=false, Active=true) → Scripting Job (Script URI model://…) → CronJob (Job definition, Active=true).
- The cronjob part should be cross-checked with the All SEAO Cronjob page.

## Next steps
- Read KB – Enable Site Samsung Rewards (Site Level) and the KB – Cronjobs pages per country.
- On staging, open TokoConfigProperty toko.rewards.epp.account.enabled.* and ph-rewardsPaymentMode to see which countries have Rewards on; practise Scripting → Scripting Job → CronJob with a simple Groovy script (never on production).
- Ask Aldwin: sample PC tickets (PayToANZ PC-56040, conversion to Groovy, add column/edit query), a way to verify Rewards after enabling a site (test account with points, GCDM loyalty API log), and cron timezone.
