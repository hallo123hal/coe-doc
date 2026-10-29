# CoE Meeting Notes – Handover Day 4: VN SMS OTP and Notifications (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487353387
Sub-pages not yet summarised in this file (personal notes): Baopg – Note – VN SMS (2487747001), Ayu – NSP + SMS Messaging (2487451862), TungNS – VN SMS OTP/Notifications (2487714026), Quynhltn – VN SMS (2487648422), VN SMS Noti (2487714034), NgaVT – VM SMS/Notification (2487648438), NgaVT – Preferred warehouse priority (2488107091), Trangdtt – VN SMS OTP/Notifications (2487517223).

Meeting: 28/10/2026, three recordings: 15:34 (~11 min), 15:46 (~19 min), 16:09 (~13 min). Group: Content. Presenter Manikanta Vaddisetti (SDSAP), with Swalehat Ummus; Teams meeting organised and recorded by David Bui. Part 2 (warehouse priority) continues two **Day 3 items that were postponed on 27/10**: "priority warehouse by subs configs" (KB: SAVINA: Preferred warehouse priority) and "Warehouse setup by sub by subs". Related: Day 3 Delivery Mode and Service.

# Part 1 – VN order SMS notifications
Presented from Manikanta's Confluence page **VN SMS OTP/Notifications** (under 02-3: Tech Team). The title says OTP but the session covered **order notification SMS only**.

## 1.1 Five SMS pages
| SMS page | When sent |
| --- | --- |
| OrderPlacedSMS | Order placed successfully |
| OrderReadyForPickupSMS | O2O pickup order ready |
| ThankYouSMS | Order completed (step `sendThankYouMessage` in the order process), contains a survey link |
| OrderDispatchSMS | Order leaves the warehouse to the carrier |
| OrderCancelledSMS | Order cancelled (customer request or other) |

Templates are in Vietnamese without diacritics, with parameters like `%2$s` (order number) and links (bit.ly/samsungcschat, bit.ly/samsungonlinenps, hotline 1800-588889).

## 1.2 Switching on/off with Approval Status
Backoffice → **WCMS → Page** → advanced search by **ID** = SMS page name (e.g. OrderPlacedSMS). Results exist in **Toko VN Content Catalog: Staged** and **: Online** (also Toko th Content Catalog), Page Template = **SMS Page Template**. Open the page → Properties → **Approval Status**: **approved** = customer receives the SMS, **unapproved** = not sent. OrderPlacedSMS is currently **unapproved** because the **subsidiary asked to turn it off**. There is **no TokoConfig or other flag**.

## 1.3 Q&A
- The VN team could not see the other SMS pages on S2 – the SMS are currently off. Unsure staging has the config; KB data comes from **production** (Manikanta may add staging screenshots vs S4).
- Changing SMS content needs a **PC ticket** (every production change does).
- Edit in the **Staged content catalog** then **sync to Online**. The VN team asked to replace "staging" (they read it as S1–S4 environments); Manikanta edited the KB live to: "Approval Status >> to Unapproved/Approved (In **VN CONTENT staged catalog** & then sync it to Online)".

# Part 2 – Preferred warehouse by region for VN
## 2.1 Problem
A region has one default warehouse, e.g. **Hanoi (VN-HN)** → **WV05-S520**. If it is out of stock a Hanoi customer can't order. Subsidiary solution: when the main warehouse is empty, **look at neighbouring warehouses** in priority order.

## 2.2 TokoConfig and Site-Warehouse Ordered Mapping
- TokoConfig **`toko.pickup.combine.preferred.warehouse.enabled.vn`** – **VN only**; false disables the feature (KB SAVINA: Preferred warehouse priority).
- Backoffice → **Region** attribute **Site-Warehouse (Ordered) Mapping** (`siteToWarehouseMap`): a priority list of warehouses **per website** (EPP, SMB, EA…).
- Example VN-HN order: check stock in the first warehouse (**WV05-S520**, master), then **WV10-S520 MX_South**, then the last one. When the config is on and the site has a mapping, stock is computed **by this mapping, overriding** the warehouse on website / base store / region. KB: siteToWarehouseMap always has top priority if defined; a region may have several warehouses; with no region priority the general warehouse-level priority applies. Enhancement **VNME-15899 – Preferred warehouse setup priority**.
- Needs a **PC ticket**; the subsidiary supplies which website, region and warehouse order. Manikanta will add sample PC tickets to Confluence.
- Screen: Backoffice → Internationalization → Regions → **Thành phố Hà Nội [VN-HN]** → Administration → Site-Warehouse Ordered Mapping (~81 rows, one per site such as vn_ftel, vn_smbphucanh, vn_ea_swl_epp → WV05-S520 MX_D2C Master, WV10-S520 MX_South…). The right-hand "Site-Warehouse Mapping" box is empty. Each website can have a different order. Only Vietnam has this feature.

## 2.3 Q&A on who decides the order
- Left = site, right = that site's warehouse list. The KB North/South higher/lower example is only an example (master warehouse is in the North). Order comes from the **subsidiary via ticket**, not from the CoE; for VN no high/low priority is set on the warehouse itself.
- The subsidiary decided initially by **distance**, later adjusting for **stock and distance**.

## 2.4 Comparison with Warehouse.priority (Indonesia)
Indonesia **WC28 ID-MX-Jakarta**: Backoffice → Base Commerce → Warehouse → Administration → **Warehouse.priority = 5** (3–4 warehouses, each with its own value). In the session: **smallest number = highest priority**. **Warning:** the SAVINA KB says "the higher the number, the higher priority" – contradictory, to confirm (and the Leadtime session said larger = higher). VN warehouse **WV09-S552 CE_EXT EPP_North_10%** has an empty priority; **WV10-S520 MX_South** shows priority **1000**, unexplained. VN uses region mapping, ID uses warehouse priority.

## 2.5 Two ways to set warehouse priority
(1) **Region mapping** (VN only, needs the TokoConfig on); (2) **Warehouse.priority** on each warehouse (ID and other subsidiaries). If the TokoConfig is off VN falls back to warehouse order like Indonesia. SAVINA has ~15–20 warehouses, which can't be split by region with a general priority, so the region approach fits.

## 2.6 Subsidiary request file – COEC-31063
**COEC-31063 – Prefer WH for vn_corporate.xlsx** (sheet WH): columns Name, Country/Region, **ISO Code** (VN-50, VN-43…), **Site** (vn_corporate), **First / Second / Third line** (Regions.siteToWarehouseMap), **Value** (e.g. "vn_corporate> WV10-S520, WV05-S520, WV09-S551"). Examples: **VN-SG** → WV10-S520, WV05-S520, WV09-S551; **VN-HN** → WV05-S520, WV10-S520, WV09-S552. The subsidiary sends **all data** by region and site; the CoE raises **PC**, configures exactly as in the file, then checks 1–2 regions and may ask the subsidiary to confirm. Order in the mapping = priority (first highest). Only the warehouses applicable to that region are included. After PC approval, before setup, check **no duplicate and no existing config** for the same site.

## 2.7 Final Q&A
Stock check: first warehouse, then the next when empty – correct. Applies to **both MX and CE** (list includes MX, master and CE warehouses such as WV09-S552 CE_EXT EPP_North_10%).

## Difficult points
- SMS VN currently **unapproved** (subsidiary request); unclear whether staging S1–S4 has the SMS pages (KB from production).
- "OTP" in the title not covered.
- **Priority rule contradiction** (KB: larger = higher; session: smallest = highest, e.g. WC28 = 5; VN WV10-S520 = 1000, WV09-S552 empty) – confirm.
- Order is decided by the subsidiary; wrong order picks the wrong warehouse.
- Each region has many site rows (VN-HN ~81); manual updates are error-prone – check duplicates / existing config first.
- Relationship between the TokoConfig, Site-Warehouse Ordered Mapping, the empty Site-Warehouse Mapping and website/base store warehouses when config is missing is unclear.

## Next steps
Read the VN SMS KB (with the fixed wording), the SAVINA preferred warehouse KB and "VN warehouse setup" under 02-3: Tech Team; look for the SMS pages on staging; Manikanta to add sample PC tickets and subsidiary request tickets (e.g. COEC-31063); ask about the priority rule and the 1000 value; build a checklist (PC approved → check duplicates / existing config → update the ordered mapping per file → verify 1–2 regions → subsidiary confirms; TokoConfig `…enabled.vn` = true); ask whether VN has OTP SMS.

Recordings: Handover_Day4_vn1/vn2/vn3_2026.10.28.mp4.
