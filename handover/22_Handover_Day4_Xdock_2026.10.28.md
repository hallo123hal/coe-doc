# CoE Meeting Notes – Handover Day 4: Xdock (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487975946
Sub-pages not yet summarised in this file: Trangdtt – Postcode2xdock (2487582755), MinhVT – Xdock (2487255139), Baopg – Note – RDD (2487943225), TungNS – Xdock (2487419030), Trangnnt – RDD (2487419153), Thanhvd – PostCodexDoc (2487353611).

Meeting: there was no separate session. Swalehat Ummus (SDSAP, PIC) presented Xdock inside the Leadtime master session on the morning of 28/10/2026 (recording starts 10:17; Xdock at 10:08–13:40, Q&A 19:30–25:40). Group: Fulfillment. Full detail and screenshots are on the Leadtime Master page (see 21_Handover_Day4_Leadtime_Master). No KB page is listed for this topic in the schedule.

## Main content
- **PostCode2XDock** (Backoffice → Types → PostCode2XDock): each postal code is assigned one warehouse and one **cross dock ID**. The cross dock ID links a **LeadTime** record to the postal code and warehouse, which is used to compute lead time and RDD.
- Record fields: Postal Code, Cross Dock, Country, Ship To, Warehouse, Address. VN example: postal code 00213 → cross dock VN-01_WV07-S551, warehouse WV07-S551.
- Upload file (per KB): country, postalCode (optional), postalCodeStart, postalCodeEnd (optional), warehouse, crossDock. Sample **TH xDock Master_20240402.xlsx**; name pattern `(country_code) xDock Master_(date).xlsx`.
- Upload path: Types → PostCode2XDock → **PostCode2XDock File Upload** → Upload File; the system creates an import cronjob (`postCode2XDockImport_delta_…`).
- Data is **provided by the subsidiaries** (worked out with their logistics team); the CoE only uploads. Mainly **TH and VN** use it. SG has no postal code mapping (a single record SG_000000_999999).
- With several warehouses Hybris picks by **Warehouse.Priority** (larger number = higher priority, per the KB example WC03 = 100 beats WC11-S501 = 50) and falls back to the next warehouse when out of stock.

## Q&A
- **VN team:** postal codes already map to warehouse and delivery mode, so what does Xdock add? **Ummus:** hard to explain; the cross dock ID is the key joining LeadTime and PostCode2XDock.
- **VN team:** is the highest priority the larger or smaller number? **Ummus:** after an unclear answer, settled on larger = higher.
- Every change on production needs a **PC ticket**. Ummus will add a reference PC ticket (VN batch) to the handover inventory. This request type is very rare.

## Open issues
- Business meaning of Xdock and the cross dock ID naming rule are not explained.
- Scope per subsidiary inconsistent: KB says TH, PH, SG, NZ; the session said mainly TH and VN.
- The priority rule must be checked on real data (the VN SMS session that afternoon said smaller = higher).
- VN team has no access to the PC project.

## Next steps
Read the references before the session and practise on staging. The "Questions from the team (unanswered)" table on the page is empty.
