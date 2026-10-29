# CoE Meeting Notes – Handover Day 4: All Scripting (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487320624
Sub-pages not yet summarised in this file (personal notes): TungNS – All scripting (2488172655), Quynhltn – All Scripting (2488270912), NgaVT – All scriptng (2487648529).

Meeting: 28/10/2026, 17:00–17:30 scheduled, recording starts 17:10 (~22 min). Group: Content. Presenter Tan Soon Kit Amos (SDSAP). Scope: skim the scripts in *KB – Script / Scripting* (Samsung Confluence, space SEAORHQ, page 687735128). The recording starts mid-way through the [SEIN] Order Remediation page. Related: Day 3 Order Remediation, NERP Configs.

## 1. [SEIN] Order Remediation scripts
- Background: SEIN processes fulfilment **manually in NERP**, outside the standard flow, so many orders get stuck; **SC+ needs the order Completed** to trigger its API.
- **Order Data Update Script**: take from SAP the **order number, SKU, DO, IMEI, billing no, billing date, completion date, 2nd GI date** and ingest them into Hybris per order. **IMEI** is needed for SC+ registration; **format must match the script** (Excel formulas may be needed to transform the subsidiary's data). HAC/cronjob **limits the number of lines** – **test on staging** first.
- **SC+ Order remediation Script**: finds order entries with SC+ and runs the **processExternalServices** task on the consignment, also changing external services **ERROR → NEW**. Then a script moves the order to **Completed** (adapt the consignment process to the scenario). Results are not immediate (small tasks need time) – use a **separate query** to check the status.
- A member asked to put the KB script link into the handover page; the link in the schedule points elsewhere – Amos will fix it.

## 2. Scripts in KB – Script / Scripting
1. **Cancel order without refund** – repair, check, set the process failed, run `releaseVirtualStockIfApplicable`, then set the order cancelled **without refund**; only repairs processes not yet in a final state (SUCCEEDED / FAILED).
2. **Cloning of ERP & ERPFi Configs** – each site has an ERP and ERP FI config; clone from an existing site instead of typing values. Page says use it when several sites map to **one ERP config** and one must be split off; loads the site (e.g. `vn_ea_intepp_activation`), `modelService.clone`s both configs, sets a new description, reassigns; set extra values if needed. (Details and the ph_gaming example: 29_Handover_Day4_NERP_Configs_by_Subs_by_Site.)
3. **Creating a New PoS Using the Script** – also a clone of an existing point of service, then set parameters; ticket reference **PC-15860 [SAVINA] Clone Samsung Showcase PoS**. One page was skipped as no longer needed.
4. **Reports / employee & user group per multistore** – quick pass over TokoCategoryPurchaseLimit and UserPurchaseLimit reports. *Get the Detail of Each Employee and Its Usergroups*: set the group suffix (e.g. `GROUP_NAME_POST_FIX = "_eadirectemployeegroup"`); output uid, email, active, allGroups, allStores, **unmappedGroups** (stores the o2o direct user group isn't mapped to); adjust lines 19, 28, 66 as needed.
5. **Groovy Script for Wait For Manual Check Approval** – Step 1 query the order processes of affected orders; Step 2 feed the list to a script running `restartProcess(…, "orderManualChecked")` (order manager check); Step 3 query the order status to verify. Used when orders need **CS agent approval** and the list is too long for CS.
6. **KB – [VN] Modify Promotion Action** – **not recommended**: queries all promotion actions and conditions; an **impex updates the actions** (PromotionSourceRule); another script **publishes** them (compileAndPublishRules).
7. **KB – Cart – temporary order** – simple query for **temporary orders**/carts (e.g. anonymous user); a **flood of temporary orders** may signal a payment issue, so **check regularly**.
8. **KB – O2O Script [MY]** – query for **point of service** data (Ctry, Type, POS PK, name, Ext ID, IP, partner, ShipTo, SoldTo, WH code, delivery mode, user group, address…); conditions per scenario.
9. **Postal Code Range** – a delivery mode's **postcodes can't be queried** (collection), so a script pulls the **postcode range**; used when a subsidiary asks why a delivery mode doesn't show.
10. **Pull – SKU has negative stock AND HAVE preorder EXPIRED** – simple, skippable; one script said to be **no longer used** (screen was on Refund Reward Points, not certain).
11. **SC+ Activation** – run the query first, then fill the consignment PK and external service PK into the script (note PC-18618) to change the status and re-run the external service.
12. **Script for pushing the consignment to the NERP** – for consignments **stuck** before NERP. Example **Indonesia**: many orders wait for the **cronjob**, which only handles a set number per run/batch; in **flagship** periods orders pile up and the script pushes them.
13. **[SEAO] To Pull MultistoreLink details** – tickets ask to **remove a user's access** from an **EPP site**; multistore has many login types and querying **PII** returns only **hashes**; the script pulls UserToMultiStoreLink details (company email, employee id…).
14. **[SEAU] Script for Special Price Validity Check** – every **special price upload** goes through **Knox approval** and then syncs to the Staged catalog; when the new dates **clash** with an active special price, an **existing code bug** sets the current price's end date **earlier than its start date**. The script (run as a cronjob) gets **approved PriceInfoChange** (by site, special price only), re-queries existing special prices, checks **overlap** and adjusts the existing price row's **start or end date** accordingly.
15. **Voucher code generation** – used day to day because Backoffice can generate only a **limited number of voucher codes**. Voucher use is fading; **coupon and voucher** will be explained in the next day's session. Remaining scripts are mostly data pulls.

Agreed wrap-up: the script list is **already shared** with BiPlus, who read it and ask questions; the next session is **RNPL**.

## Difficult points
- Recording starts mid-way through Order Remediation.
- Many scripts run on production (HAC/cronjob) with line limits; must be tested on staging and edited at the right lines.
- Most of the list was only skimmed or skipped.
- The special price bug (end date before start date) is handled by script, no root fix discussed.
- Scripting link in the schedule points to the wrong part (Amos to fix).
- Unclear which scripts are still used or retired.

## Next steps
Read the whole KB – Script / Scripting tree and send questions to Amos; check the link fix; ask SDSAP for the list of used/retired scripts and those to run regularly (temporary order check, special price validity); try manual check approval, push consignment to NERP and cancel order without refund on staging; prepare voucher code questions for the coupon and voucher session.

Recording: Handover_Day4_scr_2026.10.28.mp4.
