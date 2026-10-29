# CoE Meeting Notes – Handover Day 4: SC+ MX and CE on 3PD Platform (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487943181
Sub-pages not yet summarised in this file (personal notes): Baopg – Note – MX and CE on 3PD Platform (2487287950), Trangdtt – SC+ on 3D (2487877804), MinhVT – CE SC+ and 3PD setup (2487746947), Ngavt – CE SC+ and 3PD setup (2487419081), Quynhltn – SC+ on 3PD (2487845040), Trangnnt – SC+ on 3PD (2487353552), Ayu SC+ on 3PD (2488172605), TungNS – SC+ 3PD (2487451930), Thanhvd – SC+ 3PD (2488074312).

Meeting: 28/10/2026, end of the 13:47 recording (from 42:15) and the 14:40 recording (~18 min). Group: Product. Chair and presenter Chong Haw Eong (SDSAP). Scope: set up SC+ MX and CE for sale on 3PD platforms (Lazada, Shopee) in MY and SG. Setup of SC+ on Samsung.com / eStore / EPP is on 24_Handover_Day4_SC+_MX_and_CE.

References: KB – MY CE SC Special Setup for 3PD; [3PD][SMS] Selling SC+ on 3PD; KB – [SG] 3PD Physical MX SC+; tickets MYME-28150, MYME-28149, COEC-38151, SPIME-13745. Related: Day 3 3PD Ticket Handling and Middleware.

## 1. Why 3PD is completely different
- When a subsidiary raises a ticket to sell SC+ on 3PD, first **check the subsidiary has approval**, because the way of selling is different.
- On Samsung.com a customer buys the phone with SC+ (or standalone via IMEI) and SC+ is **activated automatically**. On Lazada/Shopee there is **no such journey** and marketplaces have **no external service SKU**, only normal SKUs.
- Customer buys on the marketplace, receives a code/info, then SC+ is activated; the subsidiary does **many manual steps** (send customer info, activate SC+). No enhancement yet – fully manual.
- Today: **MX SC+** sold on 3PD in **SG and MY**; **CE SC+** (extended warranty) only in **MY**; on Lazada and Shopee.

## 2. MX SC+ for 3PD
- SKUs are standardised for 3PD and separated from regular SC+: category **Insurance_3PD** (MY), base code **SMC-3PD**.
- **Product type = NORMAL** (regular SC+ is external service SKU). Warehouse = **MX warehouse** (MY: **WC11-S506**); block stock = true; available 9999; delivery mode **my-marketplace-delivery-standard**; TokoVariantProduct **gerpSchedType = CT**; tax class per subsidiary.
- **Approved and purchasable only in the 3PD catalog**; other catalogs stay check/unapproved (the base code SMC-3PD likewise active only for 3PD).
- These SKUs **are registered in NERP** (normal product type must be in NERP): marketplace order → Hybris → NERP. So **no separate RRP approval**: use **super sync price and stock** from NERP (Products Sync Selector Wizard → PRICE/STOCK results SUCCESS). No AEM (not sold on Hybris). **Do not change product codes** – use the subsidiary's exact SKU (e.g. MI-SCAS…). **No manufacturer AID** needed because activation on the SC+ portal is manual.
- Ticket example (MY, comment by Chong 16/09/2026): "3PD exclusive MX SC+ SKU": categories Insurance_3PD, base code SMC-3PD, product type NORMAL, warehouse MX, block stock TRUE, available 9999, delivery mode my-marketplace-delivery-standard, only 3PD catalogue approved & purchasable, gerpSchedType CT; "Pending confirmation on RRP before approve".
- Proposal: every new subsidiary uses the same standard so searching **SMC-3PD** identifies 3PD SKUs; category Insurance_3PD will be reported to RHQ for alignment.
- The Confluence page has a **Jira Comment Template** (Virtual/Physical SC+): 1 Upload file, 2 Base code setup, 3 Variant code setup (gerpSchedType CT, delivery mode, RRP, product status, tax class, sale unit pieces), 4 Stock (isBlockStock true, warehouse, available), 5 Note.

## 3. Choosing the right guideline; NGC; QA
This is the easiest place to go wrong: for 3PD follow the 3PD guideline, for Samsung.com another; first identify monthly / standalone / other. **NGC** exists only in SG and AU (reference only). **QA** can check product setup and orders in Hybris but **cannot see the 3PD platform side** without a real purchase – ask the subsidiary to help test orders. A ticket in QA review counts against our SLA; it can go on hold while waiting for the subsidiary.

## 4. CE SC+ on 3PD (MY)
Same approach: product type **normal**; check/unapproved in all catalogs, **approved & purchasable only in the 3PD catalog**; delivery mode **my-marketplace-delivery-standard** in every 3PD catalog. The page lists the MY P-codes dedicated to 3PD (P-QT…, P-RAC…, P-RE…, already set up) – they must **never be enabled** on B2C, EPP or SMB. Base code **GCIC-3PD**, category **Warranty_3PD** under supercategory external service (3); the base code identifies 3PD SKUs in reports. New countries (e.g. TH) reuse the same base code/category per their catalog (a country prefix like TH-/MY- is optional). Not a common setup – not every marketplace does it because the subsidiary must activate SC+ manually on the SC+ portal; always read the ticket requirements.

## 5. SG staging test ticket and item category YSNA
- **COEC-38151** "[SESP][3PD][Stg3] Change Item Category & Create Test Order": change the item category of **F-SC-WU2-L1** to **YSNA** and send a 3PD test order (Lazada/Shopee) to N-ERP with SM-L715FZSAXSP, ET-SNL71MDEGWW, F-SC-WU2-L1; goal: configure F-SC-WU2-L1 as a virtual item in N-ERP; after testing request the production change. Staging tests are possible only if the 3PD platform also has staging.
- Table on the page: **MX SC+ as virtual** (to NERP with ItemCate **YSNA**, not a physical item) and **MX SC+ as Physical Card** (ItemCate **YS02** or **YS10**). Flow: marketplace creates the order → LogicBroker splits the bundle → Hybris receives 2 normal SKUs → consignment to NERP → NERP creates SO, DO → **MX team activates SC+ manually**.
- Virtual F-code: SKU like F-CODE (base code F-SC), added to category "warranty", gerpSchedType changed to CT, product type NORMAL, RRP setup, delivery mode per subsidiary, approved & purchasable only in the 3PD catalog. Physical card: use the existing base code, no warranty category, gerpSchedType unchanged.
- Item category in ERP may differ per subsidiary; tested in SG only.

## 6. Q&A
- **Does the normal SKU need its own code?** No – marketplaces don't care; it interfaces with NERP, so use the subsidiary's code and the guideline.
- SC+ errors only show when **activation fails**, and then the order is cancelled (e.g. wrong price) – very bad, so check carefully before go-live. Marketplace-side promotion / activation cannot be tested; at least verify against the checklist.
- To see whether an order succeeded: Backoffice → Orders → **Admin** tab → **external service** → open it and read the **order XML / payload** sent to NERP.
- **Most 3PD tickets go to Tech – what does Merch do?** Merch does product setup, QA and go-live; Tech checks order flow and the XML payload when new orders arrive. All content of this session is Merch setup.

## Difficult points
- 3PD has no external service SKU; SC+ is a normal NERP-registered SKU and the subsidiary activates SC+ manually (no enhancement).
- Easy to mix up 3PD vs Samsung.com guidelines.
- Marketplace side cannot be tested; failures appear only on cancelled orders.
- ERP item category (YSNA virtual, YS02/YS10 physical) may vary per subsidiary; only SG tested.
- 3PD base code / category standard (Insurance_3PD, Warranty_3PD) set by SDSAP, must be aligned with RHQ.

## Next steps
Read the 3PD pages and tickets; use the Jira Comment Template for every 3PD SC+ ticket; check the subsidiary's 3PD approval and ask it to help test; agree Merch (setup) vs Tech (order flow / XML) split; ask Chong/RHQ to confirm 3PD base code/category for new countries (TH…).

Recordings: Handover_Day4_sc2_2026.10.28.mp4 (attached to the SC+ MX and CE page), Handover_Day4_sc3_2026.10.28.mp4.
