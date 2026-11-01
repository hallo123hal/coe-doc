# CoE Meeting Notes – Handover Day 6: SMB and SMB Promotion (2026.10.30)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2491842590
Sub-pages (personal notes, not summarised in detail): Thanhvd – SMB (2491744659), Ayu – SMB & SMB Promotion (2492006699), TungNS – SMB (2491318700), Quynhltn – SMB (2491842933), Trangnnt – SMB (2491646450).

Meeting: HELD on 30/10/2026, recording starts 14:39 (about 16 minutes). Group: Multistore. Presenters: Jenardi Alvindo Girsang (SDSAP, "Pindo" on Teams) for the KB and backoffice; another SDSAP member (name unclear) added the SMB rule part from about 11:00. BiPlus: all CoE members. Reference: **KB – SG SMB Promo Setup for Prescribed Goods and Non-Prescribed Goods** (Samsung SEAORHQ; copy in BiPlus Knowledge Base page 2478081371; reference ticket SPHME-13535 "SESP – MX – EPP – SMB Promo for Q3"). Related: Day 5 All Promotions (47_), Coupon Display (38_), Price Row (44_), Discount Row (45_).

## Main content

### 1. Prescribed vs non-prescribed goods (00:30 – 02:00)
- SG SMB promotions are set up for 2 SKU types: **Prescribed Goods** and **Non-Prescribed Goods**.
- Where: Backoffice → **WCMS → Website** → site **sgsme** (Toko SG SME, default promotion group **sgsmePromotionGroup**) → **Administration** tab → **Eligible VAT Products**. SKUs in the list = **prescribed goods** (the cart **excludes GST**); SKUs not listed = **non-prescribed goods**.
- **Prescribed goods**: tax relief when purchased **above 10,000 SGD**. **Non-prescribed goods**: no tax relief, no threshold.

### 2. Promotion action and price/discount row precaution (02:00 – 04:34)
- **Prescribed goods**: the GST exclusion is deducted from the RRP, so a target fixed price gives a wrong result → use **only Percentage Discount on Products** (KB example: 40% off).
- **Non-prescribed goods**: **Target Fixed Price on Products** is fine; the RRP in Hybris shows as is.
- Precautions (KB): (1) with Percentage Discount on Products ensure **no Price Row or Discount Row** exists for the SKU on the **SG SMB catalog**; (2) the final price in the brief is **tax inclusive**; (3) tax is excluded only when the **prescribed goods total** exceeds 10k SGD (not the cart total).
- Check: product (catalog **Toko SG SME Product Catalog : Online**) → **Prices** tab → Prices and Discounts. In the example the discount row belongs to **sg_memberCustomerDiscountGroup** (member site), not SMB, so no impact.
- Rule name examples: **SG_SMB_WEB_SP_12AUG26_31AUG26_DISCOUNT_AUSPECIAL-SPHME13535-FLIP8-256GB** (prescribed) and **…-FOLD8U-1TB** (non-prescribed).

### 3. Cart display and KB FAQ (04:34 – 07:30)
- Prescribed **below 10k**: GST not excluded. **Above 10k**: GST is excluded automatically and the cart shows **"exclude GST"** under the RRP. Non-prescribed above 10k: no such text.
- **FAQ**: which SKUs are prescribed? The **SESP PIC** states it in the brief/ticket; otherwise ask. Tax exclusion not shown? Check the SKU's tax relief per KB **[SG] VAT REVERSAL – GST 0%**, else tell the SESP PIC. Special price running in the same period as the rule? **SESP PIC decides**; **never remove** a price row, discount row or special price without the sub's consent on the ticket. The Merch/QA workflow is unchanged (Merch sets up and sends screenshots, QA checks).

### 4. Q&A (07:30 – 11:00)
- Information comes from the **promotion brief** (price, SKU, discount…); the site already has the prescribed/non-prescribed setup, so the work is mainly the promotion.
- Promotions are done by **Merch**; adding SKUs to **Eligible VAT Products** on website sgsme is also done by **Merch** when the sub sends new SKUs.

### 5. Sample SMB rule: Authorized SMB Customer (11:00 – 16:30)
- SMB orders are usually **bulk and high value** → follow the guideline exactly.
- The SMB site (samsung.com/<country>/business) allows **only registered partners/SMB customers approved by the sub**. Every SMB promotion rule must have **Authorized SMB Customer** as its **first condition**.
- Sample rule **Voucher Applied [SG_SMB_WEB_SP_12AUG26_31AUG26_DISCOUNT_AUSPECIAL-SPHME13535-FLIP8-256GB/INACTIVE/v4]**, Conditions & Actions: Authorized SMB Customer → **Qualifying sites** (sgsme; likewise vnsme, mysme) → Qualifying products → Product price threshold → Coupon code (AUSPECIAL). Action: **Percentage discount on products** (40%).
- The action is always **percentage discount on products** (needed for the tax exclusion above 10,000); there must be **no special price** running, otherwise ask the sub to remove it.
- Another common SMB promotion: **buy more save more** (quantity-based, e.g. 10 or 20 units); the **Authorized SMB Customer** condition is mandatory regardless.
- The next session announced: **third party trade-in vendors and payment vendors**.

## Difficult points and open issues
- Prescribed goods: only Percentage Discount on Products; a target fixed price or a price row / discount row / special price on the SMB catalog breaks the GST deduction.
- The 10k SGD threshold is on the prescribed total, not the cart; test below and above.
- Don't remove running price rows or special prices on your own.
- Missing Authorized SMB Customer as the first condition risks applying the promotion to the wrong customers.
- Prescribed SKUs come from the SESP PIC brief; the tax relief setup in KB [SG] VAT REVERSAL – GST 0% was not presented.

## Next steps
- Merch: read both KBs; on staging inspect website sgsme → Administration → Eligible VAT Products and the sample rule (Conditions & Actions).
- QA: prepare test cases for a prescribed cart below/above 10k SGD ("exclude GST" text) and a non-prescribed cart.
- Ask the SDSAP PIC for the list of live SMB sites (sgsme, vnsme, mysme…) and a sample buy-more-save-more SMB rule.
