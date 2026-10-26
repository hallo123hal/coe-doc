# Not_listed - services BiPlus needs that are NOT in the SDSAP inventory (Tùng = PIC)

Source: sheet *6 SDSAP handover review*, **Part C. Not in the inventory: what BiPlus needs SDSAP to add**. Filter: column *BiPlus PIC* = Tung. BIPLUS INTERNAL - do not send to Samsung, RHQ or SDSAP.

Two of the 23 Part C items have Tung as PIC. Neither has its own call slot: both are *asked inside an existing SDSAP topic* in **Room B (Tech)**.

| Part C # | Item | Service Pack(s) | Where it is asked | Time |
|---|---|---|---|---|
| 7 | Invoice and e-invoice generation and correction | TEC-ORD-07 (Tier 1 #14, Sprint 3, Must) | inside topic 56 *FI Posting* | Thu 29 Oct 11:20, Room B |
| 8 | Order cancellation and return | TEC-ORD-02 (Tier 1 #21) and TEC-ORD-03 (Tier 1 #23), Sprint 4, Must | inside topic 22 *Order processes E2E* | Tue 27 Oct 10:30, Room B |

| Day | Time | File |
|---|---|---|
| Day 1, Tue 27 Oct | 10:30 Room B | [TEC-ORD-02_order-cancellation.md](TEC-ORD-02_order-cancellation.md), [TEC-ORD-03_order-return.md](TEC-ORD-03_order-return.md) |
| Day 3, Thu 29 Oct | 11:20 Room B | [TEC-ORD-07_invoice-and-e-invoice.md](TEC-ORD-07_invoice-and-e-invoice.md) |

**Check this:** the sheet's *Tier 1* tab lists TEC-ORD-02/03/07 with owner **Minh, Quý** (Tech), while Part C names **Tung** as PIC (the team table has Nguyen Son Tung as Tech Sub-Lead). I treated Part C's PIC as authoritative because it is what you asked for. The other Part C items belong to other people (Ayu, Minh, Thuy Trang, Quy, Thanh, Xuan, Quoc, Thao).

These three are **Tech** services (COEC tickets, Level 1/2 engineers, production changes under a PC ticket), unlike the Merchandising services in the day folders.
