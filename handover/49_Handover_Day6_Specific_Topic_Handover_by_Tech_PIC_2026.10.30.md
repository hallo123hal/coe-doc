# CoE Meeting Notes – Handover Day 6: Specific Topic Handover by Tech PIC (2026.10.30)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2491351079
Sub-pages (member notes): TungNS – specific handover by Tech (2491416619), MinhVT – Tech specific topics (2491416646).

Status: the main page was last seen as a pre-created template (**NOT HELD YET**, modified 30/10/2026): planned 09:30–11:00 on 30/10/2026, Teams + meeting room, group Config. Presenters per schedule (SDSAP): Manikanta Vaddisetti, Aldwin John Gavino, Mohammad Ashhar Mushtaq, Swalehat Ummus, Shamni Krishnan, Tan Soon Kit Amos. BiPlus: all CoE members. Note creator: Quý Trần Đức. Recording, main content, Q&A and the unanswered-questions table are placeholders; no reference document is linked in the schedule.

Related topics: Day 4 Kibana Log (30_), Day 4 All Scripting (31_), Day 4 NERP Configs by Subs by Site (29_).

## Content recorded by team members (not an official minute)

**TungNS's note – items that Tech handles**
- Rule of thumb: when a task requires searching under **Types** (Administration Cockpit), **Tech handles it**.
- **Singpass** (SG): user authentication, applied for Trade-in. The *singpass personal detail* field stores the information received from Singpass, **encrypted**; site-specific configuration.
- **SESP – Tradein TIPLUS**.
- **Bin Lock feature for credit card payment** (AU): any modification requires a **PC ticket → Tech**.
- **PostalCodeWarehouse mapping**: the sub provides an Excel → run **ImpEx** → Tech → **PC ticket**. Maps a postal code to a warehouse to decide which warehouse is preferred for that area; otherwise selection falls back to product type / site.
- **AU Warehouse – SMA**: configured through **tokoConfig**.
- **Voucher/coupon config**: **voucher.apply.limit** = maximum number of vouchers a customer can apply at once.
- **Subs request to update multistore access code**: **SAVINA only** (many warehouses → many multistores; each month they ask to update/remove access from a multistore site). Related: *SMS and SMA – User Multistore Link*. Typically customers successfully link their work email to their account → check which account each multistore links to and until when. If the company email is empty (not provided) the next login errors "already linked" → raise a **PC ticket** to delete that record so the customer can re-link. The error usually occurs when a customer tries to link the company email with a multistore and the system says it is already linked although the earlier link failed (still empty).

**MinhVT's note**
- **Parcel Locker** – AU only.

## Next steps
Re-check this page after the session for the official recording and minutes; read the related Day 4 pages and practise on staging.
