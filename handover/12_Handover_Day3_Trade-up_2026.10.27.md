# CoE Meeting Notes – Handover Day 3: Trade-up (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2485748231
Afternoon of 27/10/2026, Merchandising session (recording ~minutes 74–84, 9 min). Chair Chong Haw Eong; presenter Pindo (SDSAP; schedule lists Jenardi Alvindo Girsang as PIC). Reference: Manual + Bulk Upload CE Trade-up (Revamp). Trade-in is for MX, **trade-up is for CE**.

## Manual setup
1. Product Cockpit → find the main SKU → **Trade-in configuration**.
2. In the popup pick the category and brand of eligible old devices (e.g. LG, Sony); the open SKU is the main SKU receiving the trade-up.
3. Next → enter discount amount, start date, end date.
4. Click **Save mapping** first, then Finish.

## Bulk upload
- Menu **MSA Uploads** → choose the country (e.g. NZ) → yellow upload button.
- File columns: main SKU, store, device ID (must be the device ID, not a name like "Sony"), additional discount (on top of the normal trade-up), start date, end date, action (default).
- **Dates are GMT** – convert accordingly (unlike overtrade, which uses local time).
- Verify either way in **Variant Trade-in Mapping** by entering the main SKU or ID.

## Customer journey
PDP lets the customer choose trade-up and pick the old device brand in a popup; the cart offers the same popup; the payment page order summary shows the trade-up discount.

## Two discounts (Chong Haw Eong)
A **base discount** is set in MSA (the subsidiary works with MSA) and an **additional discount** is set by CoE via Hybris upload. The customer sees one lump total; check the cart to see the Hybris part. One device ID per row (100 devices = 100 rows).

## Indonesia
Each scheme change involves 10,000–12,000 rows, too many to upload by hand, so the **MSA team uploads**. Order: do the trade-in mapping (old devices ↔ main SKU) first, then upload pricing.

## Next steps
Read the Revamp page; remember GMT dates; coordinate with MSA for Indonesia.
