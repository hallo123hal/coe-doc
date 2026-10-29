# CoE Meeting Notes – Handover Day 4: PH SMS / Viber OTP and Notifications (2026.10.28)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2487353414
Sub-pages not yet summarised in this file (personal notes): TungNS – NPS messaging (2487550089), Baopg – Note – NPS Messaging (2487648331), Quynhltn – NPS messaging (2488074248), Trangnnt – NPS messaging (2488172574).

Meeting: 28/10/2026, recording starts 10:56 (~7 min; originally scheduled 15:30–16:00, held earlier). Group: Content. Presenter Shamni Krishnan (SDSAP); the Teams meeting was organised by David Bui. No KB page in the schedule; Shamni presented her own Confluence page **KB – [PH] NPS Messaging (Infobip)**. The topic is short and **applies only to the Philippines**. The title says "OTP" but **OTP was not covered** – only order notification / NPS messages.

## 1. Two messages sent to the customer
**Order ready for pickup**
- Customer orders with pick up in store; the order goes **SHIPPED** (2nd GI in NERP). When the status changes to **READY FOR PICKUP**, Hybris sends a signal to **Infobip** to send the template. Only **O2O pickup** orders; sent **once** per order.
- Sent only in the **8AM–8PM** window using Infobip's messaging window (the API is called in real time, Infobip schedules sending).
- Viber uses the Infobip API **SMS failover** (if Viber fails, an SMS is sent).
- Viber text: "Hello [Customer Name]. Your Order [PHxxxxx-xxxxxxxx] is now READY FOR PICKUP in [SES Branch]. Please collect your order within 14 days to avoid cancellation." SMS is the same without the store name.

**Order complete (NPS survey)**
- Home delivery or pick up in store, order completed with billing. When the status changes to **COMPLETED**, Hybris signals Infobip to send the completion template. Same rules: once per order, 8AM–8PM, Viber with SMS failover.
- Contains an **NPS survey link** by order number (survey3.medallia.com … `oid={order.id}`) shortened with Infobip's **URL shortening**. The Viber message has a **button** with the survey URL and an **800x800 image** provided by **SEPCO**. SMS: "We hope you are enjoying your new Samsung product. Complete our survey to get a voucher for your next order: [URL]".

## 2. Tech side – the single TokoConfig
The project is live and integrated; no issues received since go-live from the tech side. The only config: **Types → TokoConfig → `toko.viber.push.notification.enabled.ph`**, currently **true** (set **false** to disable). If there is an issue, contact the **subsidiary**, who checks with Infobip.

## 3. Q&A
- **Do we need to do anything on Infobip?** No; integration is done unless there is a technical issue. There was **one case** of a customer not receiving a message – escalated to the subsidiary to check with Infobip. **The CoE has no Infobip contact** and works through the subsidiary.
- If the integration breaks: check **source code** and config first, then **raise a ticket to L2**, and work with the subsidiary in parallel. Usual task is only **enabling/disabling the TokoConfig** on request; to see Infobip logs contact the subsidiary.
- **PH only?** Yes.
- **Ticket to change the config?** Shamni pointed to her Confluence page (already added to the Handover Inventory); **no specific ticket named**. Links: KB – [PH] NPS Messaging (Infobip) and Infobip's API doc [Send Viber messages](https://www.infobip.com/docs/api/channels/viber/viber-business-messages/send-viber-messages) (POST /viber/2/messages, "Text message with SMS failover" example).

## Difficult points
- No direct Infobip contact; log/delivery checks go through the subsidiary.
- No specific troubleshooting guide (only one case so far); must read source code and raise L2.
- "OTP" in the title not presented.
- Unknown whether a sample PC ticket exists for toggling the TokoConfig.
- Image and survey link come from SEPCO; process for changing template content unclear.

## Next steps
Read the KB and Infobip API doc; check the TokoConfig on production (currently true) and note how to toggle; find in source code the flow that signals READY FOR PICKUP / COMPLETED to Infobip; ask Shamni about OTP for PH, a sample enable/disable ticket, the ticket of the missed-message case, the PH subsidiary Infobip contact, and where templates are managed (Infobip or Hybris).

Recording: Handover_Day4_ph_2026.10.28.mp4.
