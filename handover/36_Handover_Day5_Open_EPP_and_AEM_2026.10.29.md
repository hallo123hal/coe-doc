# CoE Meeting Notes – Handover Day 5: Open EPP and AEM (2026.10.29)

Source: https://biplus.atlassian.net/wiki/spaces/SamsungCoETech/pages/2489516092
Sub-pages (personal notes of team members, not summarised in detail): TungNS – EPP and AEM (2489385034), MinhVT – Open EPP and AEM (2489417801, empty), Thanhvd (2489745411), Trangdtt (2489320201), Ayu (2489516180), Baopg (2489745420), Ngavt (2489778193), Trangnnt (2489548943), Quynhltn (2489352306).

Meeting: HELD on 29/10/2026, recording starts 10:05 (about 9 minutes). Group: Multistore. Presenter: Irene Ong (Teams display name, Samsung). BiPlus: all CoE members (Merch, Tech, QA) in the meeting room and on Teams. Note creator: Quý Trần Đức. Reference KB (Samsung Confluence, space SEAORHQ): *Open EPP: Hybris + EPP AEM Config* (page 687342722). Related topic: Day 5 Bulk Order Site Config and Bulk Order Upload (see 39_Handover_Day5_Bulk_Order).

## Main content

### 1. Normal EPP vs Open EPP on the frontend (00:00 – 01:53)
- KB example: PH site **ph_homecredit** (Home Credit); reference ticket **PME-13178** "[SEPCO] EPP: WEBSITE: CREATION: HOMECREDIT".
- **Normal EPP** (e.g. /ph/multistore/edu_uno/): has a **login page**; after login a **profile icon** (Log-In / Sign-Up) appears; at checkout the customer's saved information is pre-filled (KB: **enable SA during checkout flow**).
- **Open EPP** (e.g. /ph/multistore/ph_homecredit/): **no login page**, goes straight to the **homepage**; **no Log-In / Sign-Up icon**.
- In Open EPP the login only appears at checkout, page **guestlogin/checkout**: **Continue as a member** (Samsung Express Checkout button, Sign up) or **Continue as guest** (enter email, then Guest checkout). KB calls this **disable SA during checkout flow**.
- The Q&A confirmed: the **only difference** between Normal EPP and Open EPP is the **login page**.

### 2. Hybris configuration: Multistore and Website (01:53 – 02:37)
- **Multistore → Configurations tab** (Config Properties): **Is SSO Disabled = True** and **Is allow Guest Access = True**.
  - Per KB: to **enable** SA (Samsung Account) in checkout, Is SSO Disabled = False; to **disable** SA in checkout, Is SSO Disabled = True (Open EPP uses True).
- **Multistore → Administration tab**: **TokoMultiStore.prePurchaseGuestAllowed = False**.
- **Website → Administration tab**: **CMSSite.disableCheckoutSSO = True**.
- KB screenshots are the real ph_homecredit multistore and website configuration.

### 3. EPP 2.0 (AEM) configuration: Store Mgmt (02:37 – 03:30)
- In **EPP 2.0** (Adobe Experience Manager): **EPP (ver.2) → Store Mgmt** → find the store → open **Store Information** → **Sign In/Sign UP Display = No** → **Save & Apply**.
- KB remark: sign in/up must not be turned on on the AEM side even if SSO disable is FALSE, because it is not supported.
- KB also lists **Store Type → Open EPP**; the ph_homecredit screenshot shows Store Type = Open EPP, Store URL /ph/multistore/ph_homecredit, Display = Yes, Product Auto Publish = Yes, Sign In/Sign UP Display = No.
- Irene: the topic is short, these are all the steps.

## Q&A
- **VN team:** what system is the EPP 2.0 / AEM screen, the team has never seen it? **Irene:** it is **EPP 2.0**, a **different system from Hybris**; access must be **requested from RHQ**, like backoffice access.
- Live walk-through: login via **WMC** (Samsung AD SSO, SingleID verification) → **Adobe Experience Manager** → **EPP (ver.2) → Store Mgmt**: filter by **Site**, list of Store ID / Store Name; click a Store ID to open the **Store Information** popup (demo used an AU store). To change: find **Sign In/Sign UP Display**, select **No**, **Save & Apply**.
- **VN team:** in AEM only this one property is changed? **Irene:** yes.
- **VN team:** is Open EPP only for Philippines (KB cites a PH ticket)? **Irene:** it can apply to **other subs**, depending on alignment with RHQ; CoE executes only with **RHQ approval**. The KB is only a reference.

## Difficult points and open issues
- **EPP 2.0 (AEM) is a separate system**; the VN team has no access yet (WMC / Samsung AD SSO). RHQ access process and lead time unclear.
- Guest flags look opposite: **Is allow Guest Access = True** but **TokoMultiStore.prePurchaseGuestAllowed = False**; the meaning of each was not explained.
- KB says Sign In/Sign UP Display must stay off in AEM even when SSO disable = FALSE; unclear when an Open EPP would use SSO disable = FALSE.
- Unclear whether **Store Type = Open EPP** is set at store creation or must be changed by CoE.
- Only example is PH (ph_homecredit).

## TungNS personal note (summary)
Normal EPP has a login page; Open EPP goes directly to the homepage. Config: SSO disable = true, CMSSite.disableCheckoutSSO = true; in EPP 2.0 (AEM) request access from RHQ, then Sign in / Sign up = No. The two types differ only by the login page and the sign-up UI.

## Next steps
- Request **EPP 2.0 (AEM, Store Mgmt)** and WMC access from RHQ for Merch/Tech members.
- Read the KB and compare with the real **ph_homecredit** multistore/website configuration in backoffice.
- Ask the SDSAP PIC: meaning of Is allow Guest Access vs prePurchaseGuestAllowed; who sets Store Type Open EPP in AEM; whether Shop Sync is needed after Save & Apply.
- Set up Open EPP for a sub only when the ticket has **RHQ approval**.
