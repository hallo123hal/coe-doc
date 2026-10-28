# CoE Meeting Notes – Handover Day 3: EA Direct Access and Warranty (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2485911826
Afternoon of 27/10/2026, Teams "Handover days 3 – Tech" (recording ~minutes 24–64, 40 min). Chair Shamni Krishnan; presenter Tan Soon Kit Amos (SDSAP). ~10 BiPlus Tech attendees.

## 1. EA Direct Access (EA Direct Access.pptx)
- **Problem solved:** Backoffice is restricted to whitelisted IPs, which makes it hard for in-store (O2O) staff to open the store. EA Direct Access lets them log in on the Samsung site, bypassing O2O Cockpit and needing no static IP.
- **Flow:** staff open the Direct Access URL, enter username/password, Hybris validates and emails an **OTP** (valid 5 minutes; length 6); with a valid OTP they reach the home page and order as normal, credited to their store.
- **Prerequisites:** O2O Cockpit still needed to monitor orders per store; EA web must exist; staff need the new user group.
- **Tokoconfigs:** `ENABLE_EA_DIRECT_ACCESS` (default false), `EA_DIRECT_ACCESS_USER_GROUP` (default `eadirectemployeegroup`, limits staff to assigned sites), `EA_DIRECT_ACCESS_OTP_LENGTH` (6), plus OTP validity/retry/time-limit settings. The slide says site-level, the presenter said base store level – confirm before changing.
- **Q&A:** configure only on subsidiary request (most already use it; share cart not covered). The usual task is the user group; the page has a tokoconfig ImpEx for reference only. Create the Direct Access user group via a PC ticket; assigning groups to staff accounts is not done by CoE – raise an access ticket (spoken as "AUTU") so the owning team assigns. Indonesia sends a list in template format attached to the ticket.

## 2. Extended Warranty (GCIC) for CE products (Extended Warranty Playbook and User Guide)
GCIC is the warranty system for CE, similar to Samsung Care+ for MX.
- **Purchase flow:** customer buys CE + warranty → order splits by product type, consignments, SO to NERP → NERP billing returns the serial number to Hybris → on completion Hybris sends a **certificate request** to GCIC (per-country certificate cronjob, already existing) → on success an **activation request** activates it and emails the customer.
- **Refunds:** mostly manual by subsidiaries; skipped.
- **Common GCIC errors:** pack_begin_date/pack_end_date error on the update API (check the pack code has the company-code prefix, e.g. `C480-P-QT-…`); "Sales order number does not exists" on the creation API (NERP SO not yet synced to GCIC – a NERP–GCIC issue if the Hybris order is already in NERP); web service process errors (list truncated in the source).
- **Product setup** (upfront and subscription pack codes) is done by Merchandising, but Tech must know it for troubleshooting (manufacturer AID, quantity, product type, sales status; defaults identical except warranty months and description).
- **Monthly subscription packs:** "Number of subscription" = number of payments (36 = 36 months); recurring cycle is Monthly only; free months configurable (3 = first 3 months free). Warranty products have their own stock/warehouse.
- **Editing warranty T&C:** Backoffice → Terms and Condition Component → find the warranty fragment by catalog → edit HTML; checkout payment page disclaimer is edited the same way. Subsidiaries send plain text, CoE writes the HTML and hyperlinks. Hybris–GCIC connectivity config is not changeable by CoE.
- **Mapping warranty SKUs:** product reference from CE product to warranty product must be **available service**; the service type on the product must be **warranty** (not insurance). Wrong reference type is a common reason the warranty doesn't show.
- **Subscription info:** Backoffice → Orders shows payment token, policy start date, payment date, cycle.
- **Dunning:** failed recurring payments retried (default 3 times, interval via `toko.subscription.retry.days.*`); the total is the grace period, then the insurance is cancelled (example Sweden 45 days).
- **Two-step payment:** first payment for the CE product, then the customer picks a method for the recurring part; configured in Base Store → Payment Mode → Payment Provider Parameters (`eligibleForStandaloneExternalService`). A payment mode can be shared by several sites, so changes affect all of them – inform and confirm with the subsidiary. Subscription invoice is enabled per country at code level (ask RHQ). Item category to NERP for SEPCO is set at product launch (ask the subsidiary; CoE has no NERP visibility).

## Next steps
Get EA Direct Access.pptx and the Extended Warranty playbook; confirm the "AUTU" ticket name/process, whether EA configs are site or base-store level, and which countries use subscription invoices and two-step payment; get the recording of the delivery-mode session.
