# CoE Meeting Notes – Handover Day 4: RNPL (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487549964
Sub-pages not yet summarised in this file (personal notes): Ayu RNPL Config (2487648481), TungNS – RNPL (2487451986), Quynhltn – RNPL (2487845126), Trangdtt – RNPL promotion (2487517783).

Meeting: 28/10/2026, recording starts 17:35 (~58 min); combined session "OOW | RNPL". Group: Product. Chair and presenter Chong Haw Eong (SDSAP). Scope: RNPL / SR+ (Reserve Now, Pay Later): e-voucher SKUs, external serial vouchers, distribution and redemption promotion rules, ending a sale, common errors.

References: Confluence RHQ page *RNPL SR* (page 444930420), slide "SR+ setup" (V1.5), file "Voucher RNPL Generation – Formatting". Related: Day 3 Promotion Rule and Pre-order; Day 4 OOW.

## 1. Concept
**RNPL**, also **SR+ (Samsung Reservation Plus)**, is one of the region's most important promotions, used for **every flagship launch**. Before the campaign customers **buy an e-voucher** cheaply (e.g. USD 10); during the **campaign** it is **boosted** (e.g. USD 100) when redeemed; which products get the discount is up to the subsidiary. If the customer misses the campaign the voucher **keeps its original value** for a long time (2–3 years); voucher validity is always driven by the promotion.

## 2. RHQ-allowed SKUs, ban list, approval
- **No new RNPL SKU is created** – they exist on production: Flagship (S, Z) **Z-CODE-EVOUCHER** (FS); A-series **SMARTPHONE-EVOUCHER** (SP); **TABLET-EVOUCHER** (TB); **WEARABLES-EVOUCHER** (WR); **TV-EVOUCHER**; **MONITOR-EVOUCHER** (MO); **CE-EVOUCHER** (SAVINA only); **DA-EVOUCHER**; **AIRCON-EVOUCHER** (AC); Samsung Members EPP **Z-CODE-VOUCHER-EPP** (MB).
- KB: **RNPL is banned on the newest flagship models**; every RNPL setup needs **RHQ review/approval**. KB ban list: S26 series, Buds4 / Buds4 Pro, Z Fold / Z Flip (Chong: earlier flagships were still run; rules change over time). **Samsung Members EPP** is not true RNPL so not banned; Ops CoE must **extend the promotion each time**. SKUs not in the table need RHQ review first; even launch campaigns (A series, new TV) need approval on the ticket.

## 3. Three RNPL promotion rules (voucher, not coupon)
1. **Distribution**: customer buys the e-voucher SKU and pays → sends a **voucher code**.
2. **Redemption**: during the campaign the code gives the promised discount on a product list.
3. **After boost period**: a **long-validity** promotion so unredeemed customers can still use the voucher at its **original value** – a **local-law compliance** requirement; subsidiaries usually raise tickets to extend 2–3 years.
RNPL **must use vouchers, not coupons**: NERP needs **F5 posting** and does not recognise coupons. Chong: very easy to set up, very easy to break.

## 4. Creating the external serial voucher codes
- Create the code list in RHQ format and ingest it into Hybris, attached to a serial voucher.
- File **Voucher RNPL Generation – Formatting (xlsx)**: columns fixed prefix **SR**, **Country** (VN, MY…), **Type** (FS, SP, TB, WR, TV, MO, DA… per type reference), **Date, Month, Year** (start date, 2 digits as text), **Random**. Example `SR-VNFS-2702-259A-3K4D`.
- **The format must follow RHQ exactly**; do not accept subsidiary change requests. Generate the requested quantity (e.g. 5,000) and **check duplicates** with Excel Remove Duplicates (10,000 may have 1, 500,000 about 10); fix duplicates by editing the **last 4 characters**. Paste as values into another file to keep.

## 5. E-voucher SKU setup (product setup guideline)
- Name per RHQ table; **base code Z-RNPL** (same for all SR+ SKUs); **Max limit = 1**; **Product type NORMAL** (RNPL Z-codes have NERP sync/link); name/identifier via **supersync** (AEM, because there is a PD); category **DIGITAL_PRODUCT**; **RRP** per request (subsidiary updates NERP then sync).
- **Delivery mode `xx-rnpl-digital-delivery-mode-yy`** (xx = country, yy = SR+ SKU), e.g. `id-rnpl-digital-delivery-mode-Z-CODE-EVOUCHER`; Tech must add it to base store/website/multistore. Flags: Standalone, Skip Fulfilment, `ZoneDeliveryMode.digitalDeliveryMode` (false for TSE), `ZoneDeliveryMode.exclusive`.
- **Block Stock Import = TRUE**; **Max Order Quantity = 1**; **Block Price Import = TRUE** if not supersynced (usually supersynced). **No product references, trade-in, add-on, SC+**. **No promotion may discount an RNPL SKU**. Sync AEM and price; **no stock**.
- The e-voucher SKU need not match the redeemed product (redemption is by category/product in the promotion), but by standard TV campaign → TV-EVOUCHER, tablet → TABLET-EVOUCHER, and the **type in the code** (SRMYFS, SRMYTB…) must match, because a **Hybris job sends voucher sales figures to the subsidiaries** – wrong format → empty sales report.
- Status: **approved** and **purchasable**, with RHQ greenlight (first-time setup/test) before approving. The slide is an older version.
- **VN**: add **company code** (like SC+). **PH**: **tax class must be empty** for all RNPL vouchers. **TH**: product type NORMAL (almost all countries are NORMAL).

## 6. Voucher creation and upload
- Upload file: any Excel, **header row `externalSerialVoucherCode`**, then codes in the latest format. Name free (e.g. ExternalSerial_RNPL_PME4230).
- Find **Vouchers** → create **serial voucher** (3-character prefix, e.g. K1D). **External voucher upload**: Vouchers → External Serial Voucher → enter the prefix (K1D) and the file.
- **Check**: log in as **csadmin** → Vouchers → External Serial Voucher → find prefix → Administration → External Serial Voucher Codes: shows the mapping between external codes and system-generated serial codes.

## 7. Distribution promotion rule
- **Condition**: qualifying site; product final price threshold; **qualifying product = RNPL e-voucher SKU** (e.g. Z-CODE-EVOUCHER); **message from the subsidiary**, shown **at the top of the cart** – seeing it means the promotion triggered.
- **Action: Send External Vouchers to Customer**; **Number of External Serial Voucher = 1**; **Cooling-off period = 0** (sent when the cronjob runs, within hours).
- The **External Voucher** field in normal Backoffice often shows "No read access": **save, log out, log in as csadmin**, open the promotion, enter the voucher prefix, save, return to normal BO. Save before logging out.
- The **action message** goes into the customer's **email**; the condition message shows on the cart (can be the same or different).
- **Halt rule execution** + highest priority: blocks other promotions in the cart so nobody stacks discounts on the already cheap SKU; customers with other items must buy RNPL separately (regional rule in the RHQ guideline).

## 8. Real example (SAVINA) and selling conditions
- Ticket **FLC-20361 [SAVINA][B8Q8H8]_vn_MX_D2C_Voucher promotion_SR+_22 Jul–17 Aug2026**. Email has customer name, voucher code and the text from the rule message (content may change; needs RHQ approval).
- Chong's habit: **record in the ticket** all conditions, what is updated and what is pending (product info: SKU, name/image pending NERP sync, RRP pending price approval; promotion info: voucher code, external voucher code, quantity 5k, rule names). Name/image missing from NERP → CoE updates on Hybris. **RRP must wait for approval** – never open sales at an unapproved price; subsidiaries push, think first.
- PDP benefit max **2 lines**. If the rule **doesn't run** and customers buy: they pay but get **no voucher** → VOC. Workaround: Tech inserts the promotion into the order manually and re-runs the cronjob – avoid. **No refund** on RNPL e-vouchers (subsidiary policy), so verify beforehand: serial voucher, rule text, publish, cart test.
- Checkout: **digital product**, no fulfilment info; delivery mode shows digital. **Only instant payment** (card, QR…) – **no COD, no pay later** (voucher is sent right after order confirmation; a cancelled COD would have an issued voucher). Front end shows names like "Samsung Reservation+ Galaxy …", not "RNPL".

## 9. Ending the sale
- SAVINA reminders: (1) CoE side: **redemption promotion needs action type CASH_VOUCHER**; (2) SAVINA side: **AR clearing date in NERP follows the end date of the distribution promotion**, so set distribution end date = redemption end date and **hide the e-voucher on the web** after the last sale day (e.g. sell until 13 Aug, promotion until 17 Aug, hide from 14 Aug).
- **Most important**: archive the e-voucher SKU and set it unapproved (sales status archive, approval unapproved) **at the same time as the distribution promotion's end date, or one day earlier**.
- **Most common error**: promotion expires (e.g. 13 Aug 23:59:59) but the SKU is not archived → customers can still buy and receive **no voucher** → VOC; the subsidiary must issue extra vouchers, possibly outside PMI approval.
- SKU and voucher/promotion are separate entities. End the voucher early (archive early) but **never end the promotion early** – the cronjob needs time to deliver to late buyers. Set a reminder to archive.

## 10. Redemption promotion rule
- Starts when the real product is out (e.g. Fold/Flip 8 pre-order). Condition and discount set by the subsidiary, typically **distributed discount on target products** (100/200/300… is the "boost").
- Mandatory: a condition **container** (e.g. X) and the action **Add action type on target products** with target container X and **promotion action type = CASH_VOUCHER** – only for the **redemption** promotion (NERP accepts F5 posting only with vouchers).
- Applies to **all subsidiaries except ID and MY**, which don't send F5 posting to NERP because they don't sell directly (ID via 3PL **GDC**, MY sells to **SDS** for fulfilment).
- The redeem code is the external serial voucher mapped in step 6. For flagships redemption usually **coincides with the pre-order**; afterwards a promotion returns the voucher to its **original value** (see 3).
- Redemption can be BOGO or combined. Last SAVINA run had **3 redemption rules**: BOGO gift; main-phone discount (bigger in the first 72 h); partner-product/accessory extra discount of 500,000. Every rule needs **CASH_VOUCHER**. SAVINA often chases in chat: reply done with a **Backoffice screenshot**.

## 11. Running out of vouchers, replacements, security
- If 5,000 codes were uploaded and 5,001+ customers bought, the extra customers get **no voucher** (Hybris has a report). Fix: **top up the external serial voucher** and run the cronjob. When topping up, create a new file and **compare with the old one, no duplicates** – serial vouchers are **single-use** (first payment writes the voucher invalidation table); a duplicate gives the second customer "voucher already used".
- Replacement vouchers (per agreement with the subsidiary) are usually managed by **CS**; one code can be created and sent outside the system. Record it on the ticket.
- **Security**: send large coupon/serial voucher lists as an **encrypted email file to the ticket creator**, **never attached to the ticket or sent over chat**; VOC vouchers can be worth up to ~50% of a phone's price.
- Chong's closing: RNPL is important to every flagship; write a dedicated guideline, especially for **archiving the SKU on time**.

## Difficult points
Archive SKU on time; distribution promotion must trigger (cart message) or customers get nothing; CASH_VOUCHER on every redemption rule except ID/MY; csadmin needed for the External Voucher field; RHQ code format (type matches SKU) and duplicate checks; ban list and approval rules change over time – always check the latest KB.

## Next steps
Read the RNPL (SR+) KB and slide V1.5, get the formatting file; build an RNPL checklist (SKU Z-RNPL / DIGITAL_PRODUCT / max 1 / delivery mode / VN company code / PH empty tax; voucher + external serial upload; distribution rule with halt, cooling 0, message; redemption with CASH_VOUCHER; original-value rule; archive date); set an archive/hide reminder; ask Chong for csadmin accounts and the current ban list and RHQ approval process; agree on sending voucher lists via encrypted email.

Recording: Handover_Day4_or2_2026.10.28.mp4.
