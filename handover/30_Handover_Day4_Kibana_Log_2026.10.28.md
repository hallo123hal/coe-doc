# CoE Meeting Notes – Handover Day 4: Kibana Log (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487812222
Sub-pages not yet summarised in this file (personal notes): TungNS – Kibana (2487877907), Ayu – Kibana (2487288050), Quynhltn – Kibana Log (2487255284), Thanhvd Kibana (2487156950), NgaVT – Kibana log (2487451952).

Meeting: 28/10/2026, 16:00–16:30 scheduled, same session as NERP configs. Kibana starts at the end of the 16:28 recording (12:00–12:48) and continues in the 16:43 recording (~18 min). Group: Log. Presenter Mohammad Ashhar Mushtaq (SDSAP). Reference: KB – Kibana log (Samsung Confluence, page 444930875); the *Kibana Monitoring* page is the URL directory. Related: Day 3 Order Remediation, NERP Configs.

## 1. Accessing Kibana (SAP Cloud Logging)
- Log in with the ID you were given. The **Kibana Monitoring** page (Monitoring Grafana/Kibana/Dynatrace) is a table by **Cluster** (SMA, SMS, SMR, SMB, SMC…) and **ENV** (s1…s7, p1, p2), each row with an **Alternate Kibana URL** and a **CLS url**.
- Page header notes: if the page loads forever or the new Kibana doesn't work on VDI / office LAN, **raise a Proxy Request with SSL Bypass**; and **switch the filter to `logs-json-*`** right after login.
- Login screen is **SAP ID Service** (two-factor); pick the tenant (**Global**) and open **Discover**. The default index is OpenSearch – the first step is to **choose the `logs-json-*` index pattern**.

## 2. Filtering logs in Discover
- Default is the **last 15 minutes**. Add the **`logs.message`** field in the left pane to keep it readable (other fields: session, logger name, pod id…).
- Filter by site: **`logs.contextMap.siteUid: th`**; narrow the time to 5 minutes.
- Drop noise with the **minus (filter out value)** icon, e.g. **NOT `logs.message: DB_AUDIT`**.
- **`logs.level`** is INFO / WARN / ERROR; pick ERROR for errors only. Filters stack on the filter bar. Use on **STG or production**.
- Add **`logs.loggerName`** to see which **class** the logs come from; exclude one with the minus icon (e.g. NOT loggerName …SendReplacementConsignmentToWarehouseV2). The same works for thread / threadId.

## 3. Retention
Logs are kept about **3 weeks**. With *Last 30 days*, the earliest log of the filtered class was **2 Oct**, only ~**25–26 days**. Older issues need an **L2 ticket** to fetch logs from the **archive** (slow).

## 4. Tracing orders and carts
- **Order via threadId**: Backoffice → completed order → **process** (ConsignmentProcess) → pick a task, e.g. **sendConsignmentToExternalERP** → copy **ProcessTaskLog.threadId** → search it in Kibana (*Last 7 days*); toggle off old filters and remove noise (DB_AUDIT, session closed, session user changed). Result: **Sent request** (SOAP `MT_ESTORE_ORDER_CREATE_S`) and **Received response**. For an order **stuck at a step**: open the latest sub-process, take its threadId and trace what it ran.
- **Cart via cart id / customer id**: open the e-store, browser **Inspect → Network** to get the **cart id** (or customer id) and search it in Kibana (searching by user returned nothing in the demo; cart id worked). Combine with **AND**, values in **double quotes**, e.g. `"TH261028-88765776" AND "site"`. A "payment" search returned almost nothing because the **payment mode page is not released yet**.

## 5. KB – Kibana log: search tips and NERP tags
- **Kibana search code** table: `"xxxxxx" AND "yyyy"` (logs of xxxx with keyword yyyy), `"xxxxxx"` (order logs from cart level), `"xxxxxx" AND "<soap"` (order logs from ORDER_SPLIT, SO creation), `"xxxxxx" AND "OMS"` (BOPIS 2.0 / OMS), email, trade-in IDs, voucher-code, `"%GetDevicesNeeded%"` (SENZ equipment ID). **Double quotes** = exact phrase; `*` = wildcard.
- **NERP tags**: **`MT_ESTORE_ORDER_CREATE_S`** (request to NERP to create the SO), **`MT_ESTORE_ORDER_CREATE_R`** (NERP returns the SO number), `MT_ESTORE_ORDER_TRACKING_S/R`, `MT_ESTORE_RETURN_ORDER_S/R`, `MT_CREATED_PARKED_DOCU`. Example: `MT_ESTORE_ORDER_CREATE_S AND NOT "Received response"` over 15 min → only the order-create requests Hybris sent to NERP.
- Also searchable by order number, site, session id, thread id.
- Time range via Quick select; to **monitor continuously** (e.g. a running job) set **Refresh every 10 seconds → Start**.
- The BiPlus team had no further questions.

## Difficult points
- Retention ~25–26 days; older logs need an L2 ticket.
- Kibana needs a personal account and may need Proxy Request with SSL Bypass; check every BiPlus member has access.
- Many clusters/environments; mapping of cluster to site/subsidiary not explained.
- Searching by user/customer id failed in the demo; getting the cart id from the Network tab not shown in detail.
- NERP tag table lacks explanations for tracking / return / parked docu tags.

## Next steps
Check every Tech member's Kibana access (STG and production); ask SDSAP for the cluster ↔ site mapping and the L2 archive-log process; practise tracing an order by threadId and a cart by cart id on STG; ask for remarks on the tracking / return / parked docu tags in the KB.

Recordings: Handover_Day4_nk1_2026.10.28.mp4 (attached to the NERP Configs page) and Handover_Day4_nk2_2026.10.28.mp4.
