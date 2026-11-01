# CoE Meeting Notes – Handover Day 5: Discount Row (2026.10.29)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2489155618
Sub-pages (personal notes, not summarised in detail): TungNS (2489680150), Thanhvd (2489090486), Ngavt (2489024854), Baopg (2489123360), Quynhltn (2489876545), Ayu (2489942098), Trangdtt (2491908116), Trangnnt (2491711967).

Meeting: HELD on 29/10/2026, recording starts 14:56 (about 17 minutes). Group: Price. Chair/presenter: Ong Hee Hui (Irene Ong, SDSAP, PIC). BiPlus: all CoE members. Deck: **Discount Row logic (1).pptx** (7 slides: Discount Row Priority, System Logic, Overwriting existing discount row). No KB page listed. Related: 44_Handover_Day5_Price_Row (which already covered part of discount row vs special price).

## Main content

### 1. Where the Discount Row sits (01:46 – 03:30)
- Right **below the Price Row**: **Product Cockpit → Products → open a SKU → Prices tab**: block **Prices** (price rows) then block **Discounts** (discount rows).
- Example SKU **LS32FM700UEXXY** (NZ estore product catalog : Staged). Discounts columns: Product, Valid From, Valid To, **Customer Discount Group** (nz_memberCustomerDiscountGroup, ph_…, sg_…, th_…, vn_…).

### 2. System logic – date-prioritised discount (03:30 – 06:30)
- **Eligible discount**: End Date **≥ TODAY** and Start Date **≤ TODAY**. If several rows are eligible, the system picks the row whose **start date is closest to TODAY**. Validity is computed on **date and time**.
- **Scenario 1** (SKU-A, cmsSite vn,ea): 10% 01/12–31/12 and 20% 10/12–12/12/2024. On 08/12 → **10%**; on 12/12 → **20%**.
- **Scenario 2**: 10% (01/12 00:00:00 – 31/12) and 13% (01/12 00:01:00 – 10/12). On 08/12 → **10%**. Remark: with the **same start date and time** the system takes the **row updated into the system first** (top row).
- **Scenario 3**: 15% (01/12–31/12), 20% (10/12–12/12), 15% (20/12–25/12). 08/12 → 15%; 12/12 → 20%; 19/12 → 15% (first row; from 20/12 the third row has the closer start).
- In short: same SKU → the eligible row with the **start date closest to now**; the percentage is irrelevant.

### 3. Q&A on the selection logic (06:30 – 13:25)
- Same start and end → system takes the row put in **first** (**oldest record**), so remove the unwanted one.
- "Closest" = current date closest to the discount **start date**. Swapped rows (first 20%, second 10%) on 12/12 → **10%** (closer start date), regardless of percentage.
- Uploading a new discount does **not** auto-expire or ignore the old row.
- The VN team suggested the order may follow the **PK** (record created first). A participant asked the team to collect deep technical questions and ask later.

### 4. Overwriting an existing discount row (13:25 – 15:30)
Slide "To amend existing discount row":
1. Adjust **one by one for all sites in BO**.
2. **Bulk upload** with the **same start date/time and end date/time** to overwrite the existing discount.
3. Upload a new set of discounts with a **start date closer to today**.
4. **Raise a ticket to the tech team** to delete the existing discount, then re-upload.
- Same SKU with different discount but the same start date/time: overwrite as above or have tech delete the old row.
- Every change (including discount rows) goes through price **Knox approval**. In practice CoE **uploads on behalf of the subsidiary**: sub fills the template, CoE checks it, uploads, sends for approval, then **syncs Staged → Online**. The logic is learned so CoE can **guide subs** to fix their templates.

### 5. Discount row priority (15:30 – 16:50)
- When all sites' discount rows have the **same priority**, a site with **no "Customer Discount Group"** (normally **B2C**) takes precedence and applies to **all sites sharing the catalog**, even if other sites set different discounts. To get different values, adjust the **priority**.
- **Lower number = higher priority** (0–10); **default = 1**; **EA sites changed to 0** so B2C and EA can differ.
- Where: **Administration Cockpit → Price Settings → Discounts**, find the identifier (e.g. **vn_ea_swlDiscountModel** priority 0; vn_ea_swl_studentDiscountModel and vn_ea_swl_loyaltyDiscountModel priority 1), edit **Priority** under Properties.
- Irene: CoE does **not touch** priority in daily work. Session ended 16:50 with no further questions.

## Difficult points and open issues
- Discount rows **do not auto-expire**; identical start date/time → oldest record wins, so overwrite or have tech delete.
- Scenario 2 shows start times 1 minute apart while the remark says "same start date and time" and the result is 10%; unclear whether comparison is to the second/minute or by day.
- "First record" order (PK / creation time?) not technically confirmed.
- B2C (no discount group) can override sites sharing a catalog; EA is priority 0; the full list of discount models and priorities per site is unclear.
- Deleting a discount row needs tech; all changes go through Knox approval and Staged → Online sync.

## Next steps
- Ask PIC Ong Hee Hui for **Discount Row logic (1).pptx** and the discount row bulk upload template.
- Collect technical questions (order with same start date/time, second vs minute comparison, PK handling) for SDSAP.
- Tech: confirm the deletion process (ticket to tech) and the discount models/priorities per site.
- Merch: prepare guidance for subs on overlapping discounts (overwrite with the same start/end date-time).
