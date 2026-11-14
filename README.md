# Omni-Channel Customer Analysis in Adobe Customer Journey Analytics

A hands-on project built in **Adobe Customer Journey Analytics (CJA) Analysis Workspace**, using Adobe's omni-channel retail demo dataset. I designed the segments, calculated metrics and visualizations myself, then used them to analyse how customers buy across web, app, call center and store.

> **Data note:** the data is Adobe's synthetic CJA demo dataset (retail, Nov 1–13, 2026). No real company or customer data is involved.

## View the live project in Adobe CJA

**https://analytics.adobe.com/?linkId=3b4c3879-ebab-4a02-91c2-c9d5595a9b6e&dpc=acc**

> ⚠️ **Sign-in required.** The live report sits inside Adobe Experience Cloud. To open it you need to sign in with an Adobe ID that has access to the Adobe organization where it was built. If you don't have access, the screenshots below show every panel of the report.

---

## What I built in CJA

| CJA feature | How I used it |
|---|---|
| **Segment builder** | 3 person-level customer segments, plus a reusable event-level "Web Order" segment |
| **Calculated metrics** | Revenue per person, orders per person, web orders, web revenue, AOV by channel, unattributed revenue |
| **Freeform tables** | Segment comparison, channel orders and revenue, marketing channel breakdown, Purchase ID audit |
| **Visualizations** | Bar charts, donuts, summary number, text panels |
| **Fallout** | Person-level checkout funnel (eventual path) compared across segments |
| **Journey canvas** | Checkout step 1 → step 2 → completion by channel (online, call center, store) |
| **Panel structure** | 5 panels, each with a fixed date range, a clear question and a written takeaway |

---

## The report, panel by panel

### Panel 1: Customer segments
Segment size and value, with revenue-per-person and orders-per-person charts built from calculated metrics.

<img width="3450" height="2810" alt="02-panel1-customer-segments" src="https://github.com/user-attachments/assets/619ce027-aadc-4ecf-a9e2-2017dbf24c27" />


**Segment validation.** I checked that the three segments add up exactly to total orders (117,021), so every buyer falls in exactly one group.

<img width="693" height="177" alt="03-segment-validation-table" src="https://github.com/user-attachments/assets/e708d05d-21eb-4517-9171-6235a588562d" />

### Panel 2: Channel value
Orders and revenue by sales channel (web, app, call center, store).

<img width="2968" height="2040" alt="10-panel2-channel-value" src="https://github.com/user-attachments/assets/ba0db93d-c07f-4616-92e6-ed553fd340f8" />


### Panel 3: Checkout to completion
A journey canvas from checkout to completion in each channel, plus a person-level fallout comparing segments.

<img width="3450" height="5060" alt="04-panel3-checkout-journey" src="https://github.com/user-attachments/assets/378241ae-aca9-4fd5-ab90-0ed7897ec37b" />

### Panel 4: Where the money is
Orders vs revenue by marketing channel, and average order value by sales channel for each day.

<img width="3450" height="3000" alt="05-panel4-marketing-channel-and-aov" src="https://github.com/user-attachments/assets/048818e2-02b4-4bfa-9b0e-eb3c45ca1438" />

<img width="3450" height="2770" alt="06-panel4-aov-tables-unattributed" src="https://github.com/user-attachments/assets/4462c761-dd76-4b30-9a62-c402f7fe4dd2" />

### Panel 5: Data notes
A Purchase ID audit and the data-quality caveats behind the numbers.

<img width="3450" height="1200" alt="07-panel5-data-notes" src="https://github.com/user-attachments/assets/497406bf-5fb6-473f-a6c5-8ee89ac6f524" />

---

## How I built it

### Segments (segment builder)

| Segment | Include (Person) | Exclude (Person) |
|---|---|---|
| Digital-only buyers | Online Orders exists | Call Center Orders exists OR POS Orders exists |
| Store/assisted-only buyers | Call Center Orders exists OR POS Orders exists | Online Orders exists |
| Multi-channel buyers | Online Orders exists AND (Call Center Orders exists OR POS Orders exists) | none |
| Web Order (event) | Event container: Interaction Channel = Website OR Mobile Web, AND Total Orders exists | none |

<img width="661" height="374" alt="08-segment-store-assisted-only" src="https://github.com/user-attachments/assets/9f0bef2b-b721-4a98-b201-3642076ee3ed" />

<img width="512" height="323" alt="09-segment-web-order-event" src="https://github.com/user-attachments/assets/973ba592-5778-4bae-aa5f-d132e0080bcb" />


### Calculated metrics

- **Revenue per person** = Total Revenue ÷ People
- **Orders per person** = Total Orders ÷ People
- **Web Orders** = Total Orders, filtered by the Web Order (event) segment
- **Web Revenue** = Online Revenue − In-App Revenue
- **AOV by channel** = channel revenue ÷ channel orders
- **Unattributed Revenue** = Total Revenue − (Online + Call Center + POS Revenue)

### What I learned along the way

- **Container level matters.** My first segments overlapped. `does not exist` rules and Event-level exclude containers check one event at a time, so customers who had bought in other channels weren't removed. Person-level **Exclude** containers fixed it.
- **Use one definition everywhere.** Mixing "Online Orders" in one segment with "Web Order (event)" in another left gaps. Building all three segments on the same two building blocks made the totals reconcile exactly.
- **Check the date range.** "This month" pulled in future-dated orders with $0 revenue, so every panel uses a fixed Nov 1–13 range.
- **Attribution needs a sanity check.** "Typed/Bookmarked" was credited with 64% of revenue from 4% of orders, which points to offline sales with no marketing touch.

---

## Key results

| Segment | Share of buyers | Share of revenue | Revenue per person | Orders per person |
|---|---|---|---|---|
| Store/assisted-only | 42% | 54% | $1,982 | 1.2 |
| Multi-channel | 23% | 38% | $2,473 | 2.8 |
| Digital-only | 35% | 8% | $372 | 1.4 |

- Multi-channel customers are worth **nearly 7x** as much as digital-only customers.
- Digital is **half of orders** but only **~15% of revenue**. Call center and store orders are worth 5–6x more.
- **~16,500 people** reached the last checkout step and never ordered.
- **~50% of orders** have no Purchase ID, and **~$3.3M (3%)** of revenue has no sales channel.

---

## Author

**Janani Shivram**, BI and data analytics consultant (Microsoft DP-600, PL-300 certified).
[LinkedIn](https://www.linkedin.com/in/janani-shivram-100/)
