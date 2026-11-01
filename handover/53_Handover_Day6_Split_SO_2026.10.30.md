# CoE Meeting Notes – Handover Day 6: Split SO (2026.10.30)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2491514911
Sub-pages (personal notes, not summarised in detail): NgaVT (2491711845), Ayu (2491253092), Baopg (2491973937), TungNS (2491777305, draft), MinhVT (2491711853), Quynhltn (2491679133), Trangnnt (2491580933).

Meeting: HELD on 30/10/2026, recording starts 13:43 (about 31 minutes; presentation about 06:27–25:50, the first ~6 and last ~5 minutes are waiting). Group: Config. Presenter: Swalehat Ummus (SDSAP); the scheduled PIC Tai Sheau Yann did not present. BiPlus: all CoE members. Reference (Samsung Confluence SEAORHQ): **CS-1141 Split Consignment Based on RDD | Tied FOC inside 1 Consignment with its Main Product | PH Version** (page 556990824). Related: Day 3 Order Remediation (07_), Day 3 Delivery Mode and Service (09_), Day 4 Xdock (22_), Day 3 Promotion Rule and Pre-order (05_).

## Main content

### 1. Overview and configuration (06:27 – 08:30)
- **Split SO** is a **very new** function, enabled for **3 countries: ID, PH, TH**. The order is **split into consignments by RDD** (requested delivery date) and delivered in RDD priority order.
- KB CS-1141 (main ticket CS-1141 "Hybris Split SO function") has Test data, Setup | Configurations (TokoconfigProperty, Base store, Category, CMS Site level) and Results.
- **SKU level**: Administration tab flag **TokoVariantProduct.splitDelivery = true**; only flagged SKUs are split.
- **TokoconfigProperty** (per country):
  - **toko.cart.level.split.in.checkout.version.<country> = 2** (split version 2; exists for every country).
  - **toko.split.based.on.first.delivery.date.enabled.<country> = TRUE** – the on/off switch (true = split by RDD works).
  - **toko.enable.splitby.requestdeliverydate.<country> = TRUE** ("Outside Guidance", FLC-19306 "Split Consignment with Different RDD is not working").
  - **toko.same.foc.for.multiple.main.sku.split.disabled.<country> = TRUE** (FOC scenario).
- **Base store**: **BaseStore.enableFOCSplitCombineFeature = false** ("since FOC is not split"). **Category**: category type "MERCH", **Category.MerchCategoryType = IM**. **CMS Site**: **CMSSite.enableSplitDeliveryFeature = true**.
- **Promotion rule** (Administration tab): **PromotionSourceRule.splitFOC**: **False = tied** (FOC stays in the main product's consignment), **True = split**. Content parts (Split Combine content box, MX Delivery Banner) cannot be applied (FLC-19309).
- It works only when **all** levels are enabled.

### 2. ID example: enabling split after the pre-order period (PC-51739) (08:22 – 12:23)
- ID initially did **not** have the function during pre-order; later the sub wanted it, **changed RDDs** and split consignments by RDD. Reference ticket **PC-51739**.
- The sub provides a **list of orders and SKUs** (each SKU with its RDD); impex files **epp_rdd_update.txt** / **Estore_rdd_update.txt** (attached to the ticket) update the RDD per order entry.
- Order entry → **Requested time** tab holds the **Requested Delivery Date** (chosen on the front end). The function relies mostly on the **Named Delivery Date**: line items are grouped by date, nearest first.
- Example: 2 SKUs with different RDDs (3 Sep and around 13 Aug) → **2 consignments** (Order → **Consignments** tab: <order> and <order>_1), both sent to **NERP**.
- Purpose: **paid items ship quickly**, without waiting for the pre-order ship date.

### 3. Mandatory toggles, FOC flag and PC-51739 procedure (12:23 – 14:35)
- Toggles in section 1 are **mandatory**. For Merch, with an **FOC** promotion set the splitFOC flag correctly.
- PC-51739 steps (orders/consignments already existed): **Action 1** impex RDD (UPDATE OrderEntry: requestedDeliveryDate, namedDeliveryDate); **Action 2** allow consignment deletion – Tokoconfig **tier.two.restricted.types.to.delete**, remove "consignment" from its value; **Action 3** remove consignments and re-push (run in **COE-nonPII-Email-oneOffScriptJob**), script **PC-51739_removeConsignment.txt**.
- Consignments (and orders) **cannot be deleted by default**.
- Tech: Tokoconfigs already enabled. Merch: category must be **MERCH** with **MerchCategoryType = IM**. Which SKUs are eligible is **decided by the sub**.

### 4. Q&A
- **Must all config levels be combined?** Yes, base store, site, category and SKU, all of them. Demo: Backoffice → **WCMS → Website** → Toko ID Estore → Administration: **CMSSite.enableSplitDeliveryFeature = True**.
- Backoffice → **System → Types**: **toko.cart.level.split.in.checkout.version.*** exists for all 7 countries (value 2) but that does not mean it is active; **toko.split.based.on.first.delivery.date.enabled.*** is **true only for ID, PH, TH**. Each sub decides when to use it. "2" is the version number.
- **Why PC-51739?** The function was off when orders were placed in pre-order; the sub later wanted RDD-based shipping and sent the SKU list. Because consignments already existed, **the order cannot be sent to NERP again** (sales order already exists there; a resend is a duplicate NERP rejects). So **NERP must close the SO**; then the order is updated with the new RDD. **Requested Delivery Date** and **Named Delivery Date** are both considered when sending to NERP.
- **Only for pre-order?** Yes, it was built for pre-order: if several products were grouped in one consignment, paid items would be delayed to the pre-order ship date.
- **Same RDD?** Not split: an order with 3 SKUs where the first two share an RDD puts both in the first consignment.
- PC-51739 was added to Confluence; the script that removes consignments and re-triggers the NERP send is in the ticket.
- Schedule change announced mid-session: next come **Samsung Rewards** and the **SEAO cronjob** (AJ), then the normal flow (see 51_ and 56_).

## Difficult points and open issues
- Works only when every level is set (country Tokoconfig, base store, CMS site, MERCH/IM category, SKU splitDelivery, promotion splitFOC); one missing level = no split and hard to debug.
- Enabling after consignments exist: NERP closes the SO, change tier.two.restricted.types.to.delete, impex RDD, run the one-off script; wrong order risks duplicate orders in NERP.
- How the system chooses between Requested and Named Delivery Date when grouping was not explained in detail.
- Content parts not applicable (FLC-19309); FOC flags are spread across several places and their mapping to tied/split FOC is not fully clear.

## Next steps
- Read KB CS-1141 and ticket PC-51739 (RDD impex, Tokoconfig, PC-51739_removeConsignment.txt).
- On staging check all levels for ID/PH/TH and try an order with 2 SKUs on different RDDs to see 2 consignments.
- Merch: check splitFOC on promotion rules with FOC.
- Ask the SDSAP PIC: process with NERP to close the SO when re-splitting; Named vs Requested Delivery Date logic.
