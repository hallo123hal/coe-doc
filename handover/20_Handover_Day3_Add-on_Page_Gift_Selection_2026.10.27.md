# CoE Meeting Notes – Handover Day 3: Add-on Page Gift Selection (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2486534408
Sub-page not summarised separately: TungNS – Add on page gift selection (2486829346).

Afternoon of 27/10/2026, Merchandising session (recording ~minutes 24–38, 14 min). Presenter Ong Hee Hui (Irene Ong, SDSAP); Q&A and checklist by Chong Haw Eong. References: KB – Product Reference – Bundle and Selection of Gift; KB – Add-on Page (Gift Selection). NZ is the example (AEM additional info for the add-on page has two kinds: selection of gift and the eVoucher page).

## What it is
On a watch PDP, Continue opens **Choose your gift**: a main title, a subtitle and a list of straps given free (FOC). Instead of one fixed gift, the customer picks the colour/model. Mostly used for **TVs** (choose a frame) and **watches** (choose a strap); some countries still use it, others give the FOC item directly.

## Step 1 – product reference
Product Cockpit → Product reference → download the child catalog template. Source code = main device SKU, reference type **SELECTION_OF_GIFT**, active = true, target code = gift SKU (one row per gift), plus validity (start/end).

## Step 2 – AEMAdditionalInfoTypeData of type Gift
Administration Cockpit → Types → AEMAdditionalInfoTypeData. Records can't be deleted, so **reuse an expired record** of type Gift (NZ has it). Gift selection needs **two** entries: main title ("Choose your gift") and subtitle ("Choose one of the products below") – case sensitive. Update unique key, start/end date, product codes (**main SKUs**, not child SKUs) and site, then **Enable This Type = True**. The page turns on at the start date and takes **15–30 minutes** to appear.

## How the three parts fit
Gift selection needs (1) **AEM additional info** (titles), (2) the **product reference** (gifts shown on the page) and (3) the **promotion rule** (gift enters the cart at 0, FOC). A gift that is out of stock or archived does not show.

## QA and go-live
- The add-on page can't be pre-QA'd; it can only be checked live (testing on staging is possible by pointing to the staging pre-QA environment).
- The setter must self-verify before sending to QA (otherwise it is returned) and is the first to check on go-live day; it may take a while to appear.
- Pre-go-live checklist: product reference correct, AEM additional info enabled, site correct, start/end dates correct. If the promotion isn't live the gift is charged; if the reference isn't linked the gift doesn't show. If everything is right and it still fails, suspect a technical issue.
- **Always set start and end dates** on SELECTION_OF_GIFT references: without a start date the gift page appears before the promotion begins and customers add a gift that isn't free (complaints); without an end date the page lingers after the promotion ends.

## Other notes
- AEM additional info is also used for BC add-on pages (MX flagships). A **disabled CTA** (greying out the lowest capacity on BC) used to exist but is no longer used – check before using.
- Review past setups on production: after expiry, prices and product references are removed; promotion rules and AEM additional info records remain (benefits to be rechecked).

## Next steps
Read the two KBs; build a gift selection go-live checklist; review old TV/watch setups; ask how to point to the staging pre-QA environment.
