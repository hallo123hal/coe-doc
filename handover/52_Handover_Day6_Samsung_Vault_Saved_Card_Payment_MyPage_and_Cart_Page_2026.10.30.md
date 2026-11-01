# CoE Meeting Notes – Handover Day 6: Samsung Vault – Saved Card Payment, MyPage and Cart Page (2026.10.30)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2491744322
Sub-pages (personal notes, not summarised in detail): Thanhvd – Payment Vault (2491416846), Baopg (2491744564), NgaVT (2491220252), Ayu (2491220260), Quynhltn (2491974089), Trangnnt (2492006753).

Meeting: HELD on 30/10/2026, recording starts 13:33 (about 7 minutes, **starts mid-presentation**, so the opening of the topic is missing). Group: Config. Teams meeting organised/recorded by David Bui. Presenter: Swalehat Ummus (SDSAP, PIC per schedule). BiPlus: all CoE members. Related: Day 4 RNPL (28_), Day 6 All Third Party Integrations Trade-in and Payment Vendors (see 57_).

## Main content

### 1. Configuration (00:00 – 01:16)
- KB page **Samsung Vault (Saved card payment)** (Confluence → 10 – Knowledge Base). Purpose: let customers **add/edit credit-card information on MyPage** and save the card to their account. Original ticket: **[SG] HGE-6095 – (Vault) To Save Credit Card on My page**.
- **Payment provider parameter**: Backoffice → Payment Modes → the country's card payment mode (e.g. **Credit/Debit Card [sg-adyenCcMORPaymentMode]**) → Payment Provider Parameters → add **enableSaveCcOnMyPage = true**.
- **Two TokoConfigs** (Backoffice → Types → TokoConfigProperty): **add.paymentinfo.from.external.system.$siteUid = true** and **toko.vault.storeid.country.mapping.$siteUid** = country store code (SG: **SGP**).
- Enabled only for **SG** and **NZ**. Backoffice shows add.paymentinfo.from.external.system.sg / .nz = true and toko.vault.storeid.country.mapping.sg = SGP, .nz = NZL.

### 2. Customer UI and Backoffice data (01:16 – 03:30)
- Frontend: My Page → **Profile Setting** → **Payment** → **+ Add** opens **Add New Card**: Credit Card Number, Name, Expiration, CVV, Terms & Conditions / Privacy Policy consent, **Set this Primary**. The card is validated and saved to the account.
- No card: "You did not add any payment methods yet". With a card: a **Credit Card** box (masked number, expiry, Primary flag) and a **delete** button. KB screenshots come from SG staging (stg3), regular and business site.
- Backoffice: Customers → customer → **Payments** tab → **Payment Methods** (Payment Method Details). A saved card is flagged **true** and some values are stored in the payment provider parameters (not shown; the demo account had no saved card).
- Since go-live **no tickets** have been received for this feature (not even to turn it off).

### 3. Q&A (03:30 – 05:00)
- **VN team:** only Singapore? **Ummus:** **Singapore and New Zealand**; no other country.
- **toko.vault.storeid.country.mapping**: SG = **SGP**; NZ spoken as "NZP" but the screen shows **NZL**. Values are **fixed and must not be changed**.
- Purely configuration; at go-live probably enabled by someone on the RHQ side (unclear).
- Nothing was shown specifically about the **cart page** despite the title.
- The VN team took a minute of internal discussion, then moved to the next topic (the next slot used a different Teams link).

## Difficult points and open issues
- Recording starts mid-way; any Vault overview at the beginning is missing.
- Setup has 3 parts (enableSaveCcOnMyPage on the card mode, add.paymentinfo.from.external.system.$siteUid, toko.vault.storeid.country.mapping.$siteUid); store ids (SGP, NZL) must not be changed. NZ spoken "NZP" vs screen "NZL" – use NZL.
- Saved-card data on Backoffice (true flag, stored parameters) not shown; card tokenisation on the Adyen/Vault side unclear.
- No tickets since go-live → no incident experience; the cart page part was not presented.

## Next steps
- Read the KB Samsung Vault (Saved card payment) and ticket HGE-6095.
- On SG/NZ staging check the 3 settings, add/delete a test card in My Page → Profile Setting → Payment, then check Customers → Payments in Backoffice.
- Ask Swalehat Ummus: summary of the unrecorded opening, the cart page part (saved card at checkout?), where cards are stored (Hybris or Adyen/Vault), which fields are stored in the provider parameters, and how to handle card-saving errors.
