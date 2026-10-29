# CoE Meeting Notes – Handover Day 4: NERP Configs by Subs by Site (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487648266
Sub-pages not yet summarised in this file (personal notes): TungNS – NERP by subs by site (2487648496), Baopg – Note – NERP Config (2487255270), Quynhltn – NERP Configs (2487288031), NgaVT – NERP (2487681224).

Meeting: 28/10/2026, 16:00–16:30 scheduled; this topic is in the 16:28 recording (~13 min, 00:00–12:00); the end of the recording moves on to Kibana Log (see 30_Handover_Day4_Kibana_Log). Group: Fulfillment. Presenter Mohammad Ashhar Mushtaq (SDSAP). No KB page listed in the schedule. Related: Day 3 Order Remediation, Kibana Log, All Scripting.

## 1. Where the NERP config lives
Ashhar understands "subs" in the topic name as **base store**. Two configs: **GERP Config** (order data sent to NERP) and **GERP FI Config** (financial data). Path: Backoffice → **Base Commerce → Base Store** → store (e.g. **Toko MY Store**) → **Administration** tab → fields **Gerp Config** (GERPConfigModel) and **Gerp Fi Config** (GERPFiConfigModel); the screen shows `BaseStore.fulfilmentSource = NERP`. It can be overridden at site level (section 6).

## 2. GERPConfigModel – main fields
Open from the base store or via Types (GERPConfigModel). Values (company code, distribution channel, partner number, sales organization, ship-to partner number…) are **all provided by the subsidiary**. Changes can be made manually in Backoffice or by impex but **need PIC approval**. Toko MY Store example: **Distribution channel = 30**, **Division = 00**, **document type sales order = YS10**; other fields: deliveryModeErpConfig, domainPartnerMap, disablePOType, disablePricesPerDivision.

## 3. ErpItemTypeDetail – SKU-level NERP config
Item type **ErpItemTypeDetail** holds per-**SKU** config, e.g. Samsung Care **pack codes** (SKUs starting with P). Example: ErpProductType **P-GT-LCXOS2PW**, Warehouse **WC11-S506**, ErpItemTypeValue **MAIN_PRODUCT**, OrderType **YS10**, Item Categories **YNS1**, Scheduled Categories **CT**. Values come from the subsidiary; create records only when requested (values differ, structure is the same).

## 4. PH: one config shared by several sites; delivery mode map
- **ph_ERP_Config_B2C** is attached to base store Toko PH Store and base sites **Toko PH Estore** and **Compensation**. A new site that should reuse a config only needs to be **added to the Base site field**, but usually the subsidiary asks for a **separate config** (section 6).
- **GERPConfig.deliveryModeErpConfig** maps each **delivery mode** to an NERP code, e.g. `ph-delivery-small-ce → 7003`, the `ph_2.0-2.5-HP-…` modes → `7009` (51 entries for B2C). New mode → new map entry.

## 5. GERP FI Config
Separate financial config, also per site; codes come from the subsidiary. Also has a delivery-mode map and a **Payment provider payment id map** (payment mode → ID). TH example (`th_2243821_fi`): **kbank → 2247458**, kbankInstallment → 2247458, **atome → 4197425**, zeroAccountNumber → 4162946, tradeinHKONTAccountNumber → 12010101; Profit center = AZ.

## 6. Creating config for a new site with the clone script (example ph_gaming)
- On a request to create NERP config / NERP FI config for a new site: **ask the subsidiary which site to reference**, then clone that site's config.
- Example ticket **PC-47711 "[SEPCO] Create NERP FI & NERP Config for new site ph_gaming"** (verification COEC-34799; request said "ERP Configs: same as **ext_uno**").
- Groovy script: FlexibleSearch for CMSSite uid IN ('ph_gaming','ext_uno'); **source = ext_uno**, **target = ph_gaming**; `modelService.clone` copies the source config and attaches it to the target site. **Two identical scripts**: one for **GERPFiConfigModel**, one for **GERPConfigModel**. If the new site differs, add set statements. The script is also in KB **Cloning of ERP & ERPFi Configs** (see 31_Handover_Day4_All_Scripting).

## 7. A site with its own config: Shop for Business and the domain partner map
- Site **Shop for Business (phsme)**: the **site** Administration tab has **Erp Config = ph_ERP_Config_SMB** and **Erp Fi Config = ph_ERP_FI_Config_SMB**, different from the base store. ph_ERP_Config_SMB: company code **C5B3**; deliveryModeErpConfig holds only that site's modes (ph-delivery-standard-ac, ph-delivery-standard-vd, ph-delivery-small-ce → 7003).
- **GERPConfig.domainPartnerMap** **splits orders by the customer's email domain**: e.g. a customer registered with **homecredit.ph** → partner ID **5961417**; 30 entries on screen (partner.samsung.com, stellarbrandz.com, landers.ph, jw.org…). The same map exists in the site's **FI config**.

## 8. Requests to add / change domain partner map entries
Subsidiaries sometimes ask to **add a domain**: they send domain name and ID, the team adds the line and Saves. When a company **changes its domain**: remove the old line, add the new one. Ashhar searched Jira for sample tickets (COEC-28349 "[SME] EPP Corporate Domain list", COEC-24432 "MY – [EPP] Add domain filter…") and promised to **paste the ticket link**.

## Difficult points
- Meaning of "subs": base store, but config can also sit on the site (Shop for Business); site → base store precedence needs confirming.
- All NERP values come from the subsidiary; every change needs PIC approval.
- The clone script copies everything; differences must be added by hand (easy to miss).
- Domain partner map edited by hand per request; sample ticket not yet pasted.
- Unclear when ErpItemTypeDetail is needed beyond Samsung Care pack codes.

## Next steps
Get the sample domain-map ticket from Ashhar; read PC-47711 / COEC-34799 and try the clone script on staging; confirm the PIC approval flow for GERP config changes (manual vs impex, who approves); list base stores/sites with their own config (e.g. ph_ERP_Config_SMB).

Recording: Handover_Day4_nk1_2026.10.28.mp4 (attached to the Confluence page).
