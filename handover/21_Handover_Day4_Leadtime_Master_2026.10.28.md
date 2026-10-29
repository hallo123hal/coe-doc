# CoE Meeting Notes – Handover Day 4: Leadtime Master (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487681055
Sub-pages not yet summarised in this file (personal notes): Quocdm – Recap 28/10 (2487156750), Trangdtt – Leadtime (2488008705), TungNS – Leadtime (2487156839), Quynhltn – Leadtime (2487222356), Trangnnt – Leadtime (2487681237), Thanhvd – Leadtime (2487255293), NgaVT – Leadtime (2487550149).

Meeting: morning of 28/10/2026, recording starts 10:17 (~36 min), Teams + meeting room. Group: Fulfillment. Presenter Swalehat Ummus (SDSAP); Shamni Krishnan is PIC per schedule. All BiPlus CoE members (Merch, Tech, QA) sit in one room. The Xdock topic was presented inside this session (see 22_Handover_Day4_Xdock).

## 1. Who needs to attend
Lead time is mostly set up by Tech (a few configs; data files come from the subsidiary). Merch does not do any part, but BiPlus agreed the whole team joins every session. No KB page is listed for this topic in the schedule (ask the PIC).

## 2. Leadtime Master – overview and prerequisite configs
KB: **KB – LeadTime Master ENH** (Samsung Confluence). Lead time is calculated at **checkout**, after the customer enters details and picks a delivery mode, from **warehouse + postal code + delivery mode** (shipping type, shipping condition, special processing ID). KB scope: TH, PH, SG, NZ.

- TokoConfigProperty: `split.order.by.preferred.warehouse.enabled.{countrycode}` = true (e.g. `.th`) and `toko.oversell.leadtime.enabled` = true.
- Delivery mode: **Enable RDD For Non-Calendar** = true (for modes without calendar) and, in the Administration tab, `ZoneDeliveryMode.supportsRequestedDeliveryDates` = true.
- **Display Calendar** true/false is per subsidiary: true = calendar delivery mode (customer picks the date), false = non-calendar. Creation of delivery modes was covered on Day 3 (Delivery Mode and Service).

### 2.1 GERP data of the delivery mode must match the LeadTime master
Three mandatory values: **ERP delivery mode**, **ERP shipping condition**, **ERP S Proc Ind**.
- Backoffice → Delivery Costs → delivery mode (e.g. `sg-delivery-standard`) → tab **GERP Data**: Erp delivery mode = M1, Erp Shipping Condition = D1, Erp S Proc Ind = NORM.
- Mapping to the LeadTime master file: shippingType = ERP Delivery Mode, shippingCondition = ERP Shipping Condition, spiProcIndicator = ERP S Proc Ind; the `crossDock` column (e.g. PH1000_1820) shows as Cross Dock in Backoffice.
- Values in the file and on the delivery mode must be identical; the data comes from the subsidiary.

### 2.2 Type LeadTime and file upload
- Backoffice → Types → **LeadTime**. Fields: Business Days Only, Cross Dock (e.g. SG_000000_999999), Cut Off Schedule per weekday (e.g. WEDNESDAY → 150000, SUNDAY → 000000), Days Of Week, ERP Delivery Mode, Lead Time. SG example: Monday–Saturday delivery, no Sunday.
- Sample file on KB: **TH_LeadTime Master_FINAL_v1.xlsx**. Columns: crossDock, shippingType, shippingCondition, leadTime, spiProcIndicator, warehouseOpLeadTime, mondayDelivery … sundayDelivery (Y/N), mondayCutOffTime … (e.g. 120000, 150000).
- The subsidiary sends the file; if it has none, the team pulls the current data, sends it to them to check, and they send it back.
- Upload: Types → LeadTime → **LeadTime File Upload** → choose base store (country code) → Upload LeadTime. The system reports status and the cronjob name (e.g. `postCode2XDockLeadTimeImport_…`); note the name for follow-up.
- KB notes: file must be **decrypted (no NASCA encryption)** or the upload errors; naming `(country_code) Leadtime Master_FINAL_(version#).xlsx`; **no duplicate rows**; if you lack NASCA rights ask L2 to upload via a maintenance ticket; re-upload by **changing the version in the file name** – the system overwrites, no need to delete old data.

## 3. Xdock (PostCode2XDock) and preferred warehouse
(Details in 22_Handover_Day4_Xdock.)
- Backoffice → Types → PostCode2XDock: each postal code maps to a warehouse and a cross dock ID. Fields: Postal Code, Cross Dock, Country, Ship To, Warehouse, Address. VN example: 00213 → cross dock VN-01_WV07-S551, warehouse WV07-S551.
- Upload file columns: country, postalCode (optional), postalCodeStart, postalCodeEnd (optional), warehouse, crossDock (TH example 10100–11150, WC03, `TH10100_11150_WC03_THBKK001`); sample TH xDock Master_20240402.xlsx; name `(country_code) xDock Master_(date).xlsx`.
- Upload: Types → PostCode2XDock → PostCode2XDock File Upload; cronjob `postCode2XDockImport_delta_…`.
- **Warehouse selection**: Hybris reads the warehouses configured on the Site (`CMSSite.warehouses`); with several, the one with the highest `Warehouse.Priority` wins (WC03 = 100 beats WC11-S501 = 50). If it is out of stock, it **falls back** to the next. If the Site has no warehouse, the Store's warehouse is used.

## 4. How Requested Delivery Date (RDD) is calculated
Properties: **leadTime** (days, e.g. 1 → today+1); **whOpLeadTime** (extra warehouse operation days, default 0); **cutOffSchedule** per day (150000 = 3 PM; ordering after cut-off adds 1 day); **daysOfWeek** (delivery days; a date landing on an excluded day shifts +1 per day, e.g. no Sat/Sun → +2); **publicHolidays** (Backoffice → Base Store → Administration → `BaseStore.publicHolidays`; supplied by the subsidiary; timestamp 9:00 AM GMT; on calendar modes holidays are locked on the date picker).

Formula (KB): **RDD = Current Date + (LeadTime + whOpLeadTime + cutOffSchedule + daysOfWeek + publicHoliday)**.

| Case (postal code 1400, ordered Wed 12/06/2024, LeadTime 5, Mon–Fri) | RDD |
| --- | --- |
| Before cut-off, no holiday | 19/06/2024 (Wed) |
| After cut-off (+1) | 20/06/2024 (Thu) |
| Two holidays 13/06 and 17/06 (+2) | 21/06/2024 (Fri) |

- See RDD on an order: Backoffice → Orders → order → order entry → **Requested time** tab (RDD in Backoffice user time and in BaseStore time, Requested Time From/To, Original RDD).
- Customer journey: calendar delivery mode shows a calendar, non-calendar only picks the mode. Days shown = Base Store → Administration → **Delivery Calendar Slot duration** (7, 14 …); most subsidiaries use 14 (SG: 14).

## 5. Q&A
- **Xdock vs postal code→warehouse mapping?** Ummus: hard to explain; the cross dock ID links LeadTime to warehouse and postal code. SG has no postal mapping (only SG_000000_999999); mainly TH and VN use it; VN was done recently with ~691 records, all supplied by the subsidiary. Subsidiary must provide the mapping; if it doesn't know, the team pulls current data. Ummus will add a reference PC ticket (VN batch) to the handover inventory; the VN team has no PC project access yet; such requests are rare.
- **Warehouse priority – larger or smaller number first?** After an unclear first answer: **larger number = higher priority** (matches the KB example). Set in Backoffice → Warehouse; order decided by the subsidiary.
- **Who owns TH lead time / warehouse data?** The subsidiary (business) supplies it, including holidays; every subsidiary has lead time; TH is configured.
- **Cluster Scripting step on the KB (run script in HAC after changing TokoConfigProperty)?** Was needed before, **no longer needed**.
- **Scripts**: Groovy, Tech only. **Every production change (including script data pulls) needs a PC ticket**; running without one gets flagged. Always test on staging (stg 1–4), write a check/fetch script after importing, verify on the front end.
- **Does uploading a subsidiary file need a PC ticket?** Yes, always. Confluence page *Data Update* (07 – Approval Processes) lists change types needing PC approval: Impex/Scripting, Cronjob Creation, Backoffice Config Change, Custom Trade-In Listing.

## 6. Open issues
- Business meaning of Xdock and the cross dock ID naming convention are not explained.
- Priority rule needs verification on real data (the VN SMS session later the same day said smaller = higher; see 33_Handover_Day4_VN_SMS_OTP_and_Notifications).
- KB scope (TH, PH, SG, NZ) vs meeting scope (mainly TH, VN) unclear.
- KB still contains the obsolete Cluster Scripting step.
- VN team has no PC project access; no subsidiary PIC for lead time / warehouse data.

## 7. Next steps
SDSAP (Ummus) adds reference PC tickets; VN team requests PC project access, asks for the cross dock convention and per-subsidiary scope, inspects LeadTime / PostCode2XDock / Warehouse priority / `BaseStore.publicHolidays` on staging, tries the two sample uploads, and asks SDSAP to update the KB.

Recording: Handover_Day4_lt_2026.10.28.mp4 (attached to the Confluence page).
