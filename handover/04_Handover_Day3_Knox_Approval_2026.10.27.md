# CoE Meeting Notes – Handover Day 3: Knox Approval (2026.10.27)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2485223528
Sub-pages not yet summarised in this file: Trangdtt – Knox Approval (2486599717), Ayu – Knox Approval (2486829127), Thanhvd – Knox Approval (2486829201), TungNS – Knox Approval (2486763669).

Meeting: handover day 3, morning of 27/10/2026, in the office and on Teams. Presenter Chong Haw Eong (SDSAP); BiPlus CoE VN team in the room and on Teams (~23 people). The Loom recording covers only the first 31 minutes (audio could not be transcribed; content comes from screen share and Teams captions from 20:50).

## Day 3 agenda (27/10 and 28/10)
Parallel sessions in several rooms. 27/10: Benefit / Add-on page with AEM info / Category Structure (Ong Hee Hui); Pre-order and RTF override (Chong Haw Eong, Saidatul Humairah Binti Abdul Razak); Auto MBO (Shamni Krishnan, Saidatul); Knox Approval (Chong Haw Eong); Overtrade NZ (Ong Hee Hui); Trade-up bulk upload (Jenardi Alvindo Girsang); Trade-in T-base code for AU/ID/MY/NZ/PH/SG/TH/VN (Lee Chia Yee, Tai Sheau Yann); 3PD E2E, issues, cronjobs, middleware (Quan Nguyen); priority warehouse (Manikanta Vaddisetti); delivery mode/service config (Mohammad Ashhar Mushtaq); order process E2E / Order Remediation (Aldwin John Gavino); direct EA access and GCIC updates for ID (Tan Soon Kit Amos). 28/10: Leadtime master and Xdock, SC+ Grading (TH), SC+ MX/CE, SC+ on 3PD and OOW. All day 1–2 items on page 02-18 Handover Inventory are COMPLETED.

## Knox approval for Special Price (KB – Special Price Knox Approval)
- Every special price and discount change on Hybris needs Knox approval before it takes effect. Toko configs: `knox.discount.promotion.approval.disabled.<StoreID>` = false (promotion) and `knox.price.approval.disabled.<StoreID>` = false (price). Cronjobs every 45 min: `knoxPromotionStatusJob` (KNOXPENDINGAPPROVAL → KNOXAPPROVED) and `knoxPriceApplyingJob` (KNOXAPPROVED → COMPLETED).
- Steps: (1) upload the special price template in Backoffice (pop-up "Price Information Change Detected"); special price rows and discount rows follow the same process, MX and CE SKUs can share one approval; (2) in Admin Cockpit open **PriceInfoChange**, rows are VALID; (3) select SKUs and submit; (4) fill the **Request for Price Information Change Approval** form: Approval Title, Comment (ticket number), Business PIC (per subsidiary), Approval Process (path predefined by MX/VD/DA), use Export Excel to check, then OK; (5) Knox approval is created along the path, which follows the subsidiary org chart and gets longer with deeper discount (Hybris uses the highest discount in the submission).
- Submitting by discount row does not allow the same SKU with different validity periods (error "Please check duplicated PriceInfoChange…"); price rows do.
- After submit: VALID → KNOXPENDINGAPPROVAL → KNOXAPPROVED → COMPLETED, then the row appears in the staged catalog. Editing a price manually in staged catalog creates a new PriceInfoChange row → new Knox approval.
- Demo (VN data): SKU RT38CG6584B1SV, 9,891,000 VND, 32.62% discount, special, 23/10–30/11/2026. VN approval paths: `PRICE_SAVINA_MX_DIVISIONCONFIG`, `PRICE_SAVINA_VD (TV)`, `PRICE_SAVINA_VD (EB)`, `PRICE_SAVINA_HA`, `PRICE_SAVINA_AC`; each lists requester, consent, approval and notification.
- Knox Portal: the Promotion Approval mailbox receives "[Official][Approved]…" emails with the Draft → Consent → Approved → Notification history and a DiscountContent.xlsx attachment. Example: IDME-11575 SmartThings Lifestyle Campaign RAC x MX.
- Backoffice configuration lives under Marketing → Knox Approval (KnoxAccount, KnoxApprovalConfig, KnoxApprovalDivisionConfig, KnoxApprovalPath, KnoxApprovalLine).

## Q&A on price approval
- Agree with each subsidiary on a long-term Business PIC.
- SLA for tickets waiting on Knox: Jira has no dedicated status (workflow is shared by all countries), so by agreement with RHQ the ticket goes **ON HOLD** (the wait is the subsidiary's SLA) but stays under the CoE handler's name; update Jira every 2–3 days; waits of 2–3 weeks (even cancellations) are normal; only the submitter can see the approval step; after approval the price goes live and QA checks.
- Two files: the subsidiary's upload file (check catalog and fields) and the system-generated discount content file to cross-check.
- "All config changes need a PC ticket – but in this case never": taken to mean the configs that disable Knox approval are never changed; to confirm with Chong.

## Knox approval for Promotion Rules (KB – Promotion Rule Knox Approval)
- Config `knox.discount.promotion.approval.disabled.<StoreID>` = false; cronjobs `knoxPromotionStatusJob` and `knoxPromotionPublishingJob` (KNOXAPPROVED → PUBLISHED) every 45 min.
- Steps: in Admin Cockpit → Marketing → Promotion Rules fill the Approval section (Title, Description, Business PIC) and save; click **Publish rule**, which opens "Request for Discount Promotion Approval" with auto-filled type and details.
- Demo (SG): rule `SG_B2C_CRP_CE_01JAN26_31DEC26_DISCOUNT_11921-SL6-SL7-RRPPRC-5`, type D102 (direct price discount, SKU, immediate, fixed rate), 5% on Samsung Care+ Core SKUs with voucher SL6/SL7; Approval section holds the ticket number (e.g. SPHME-12934). The recording ends here; the continuation is on the "Promotion Rule and Pre-order" page.

## Next steps
Read the two KB pages and the Knox Approval child pages (Configs, FAQ, Overtrade, Testing); agree Business PIC per subsidiary; apply the ON HOLD workaround; confirm the "never change config" statement; obtain the full recording of 27/10.
