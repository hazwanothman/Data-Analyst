# 📊 MSR Daily Sales Report — Power BI

An end-to-end retail sales reporting solution built in **Power BI**, covering daily, monthly, and yearly performance across physical outlets, consignment, online, pop-up, and wholesale channels in **Malaysia (MY)** and **Singapore (SG)**.

The report gives management and outlet teams one place to track sales against target, compare periods, spot under-performing outlets early, and project month-end results.

---

## 🧰 Tech Stack

| Layer | Tools |
|---|---|
| Data sources | Shopify, MLS, Business Central 365 (BC365), LoyaltyLion, Footfall, Facebook Ads, Google Ads |
| Ingestion | Fivetran, Syncwith, custom API (VM) |
| Storage / warehouse | Google BigQuery, Google Sheets |
| Modelling & reporting | Power BI (Power Query, DAX, star-schema data model) |
| Documentation | draw.io |

---

## 🏗️ Data Architecture

```mermaid
flowchart LR
    subgraph Sources
        FB[FB Ads]
        GA[Google Ads]
        SH[Shopify]
        LL[LoyaltyLion]
        TR[Transfers - Shopify]
        FF[Footfall]
        MLS[MLS]
        BC[BC365]
    end

    subgraph Ingestion
        SW[Syncwith]
        FT[Fivetran]
        API[API - VM]
    end

    GS[Google Sheets]
    BQ[(Google BigQuery<br/>Data Warehouse)]
    OUT[API - VM outbound]
    PBI[Power BI]

    FB --> SW
    GA --> SW
    SW --> GS
    GS --> BQ
    SH --> FT --> BQ
    LL --> API
    TR --> API
    FF --> API
    API --> BQ
    MLS --> BQ

    BQ --> OUT
    OUT --> SUB[Sales submission]
    OUT --> CL[BQ clone]

    BQ --> PBI
    GS --> PBI
    BC --> PBI

    PBI --> DSR[DSR: Day-to-day / Monthly / Yearly]
    PBI --> P2[PBI 2.0: Finance / Management / Marketing / Operations / Merchandising]
```

The full diagram is in [`data_flow_diagram.drawio`](data_flow_diagram.drawio) and can be opened at [app.diagrams.net](https://app.diagrams.net).

---

## 🗂️ Data Model

![Data Model](https://github.com/user-attachments/assets/ab5034cf-84f5-43c1-951f-20d89ca67bcc)

---

## 📄 Report Pages

### 1. Day-to-Day Analysis — MY (Shopify)

Daily and month-to-date view of sales performance, filterable by outlet, date, financial year / quarter / month, and custom date range.

**Key features**
- **Headline KPIs:** MTD sales, last-year MTD, % change, yesterday's sales, and the MVP outlet of the month
- **Performance cards:** Total Sales, Monthly Target (with % achieved), Total Orders, Total Quantity, AOV, and AvSP
- **Top 5 and Bottom 5 outlets** by sales
- **Sales by channel:** Outlet, Consignment, Online, Pop-up, Wholesale (SG)
- **Last 3 weeks sales by day** to show day-of-week patterns
- **Current month vs. last MTD vs. last year MTD**
- **Online sales by marketplace:** Brand.com, Shopee, Lazada, Zalora, TikTok, Amazon
- **Outlet target table** with achievement % and remaining balance to target
- **Extrapolated sales** by outlet and in total against the monthly target
- **Compare Sales:** any two date ranges side by side, with difference, % target, and GP%

![Day-to-Day Analysis 1](https://github.com/user-attachments/assets/1276e892-f800-4fab-94c4-396c01d14335)
![Day-to-Day Analysis 2](https://github.com/user-attachments/assets/1942bc98-bbfe-4466-abf8-11c614a766c4)

### 2. Monthly Analysis — MY (BC365)

Month-level performance sourced from Business Central 365.

![Monthly Analysis 1](https://github.com/user-attachments/assets/cf4a59bb-7357-4319-bec7-12a92f4ade45)
![Monthly Analysis 2](https://github.com/user-attachments/assets/790a8653-31e1-4b22-ac3d-4747c76d04b9)
![Monthly Analysis 3](https://github.com/user-attachments/assets/76a33cf2-4f83-47ed-a18f-2888c8cbc589)

### 3. Yearly Analysis — MY (BC365)

Year-over-year trends and long-term performance.

![Yearly Analysis 1](https://github.com/user-attachments/assets/c68bb556-de25-4a7c-b1b3-b3b1c4864793)
![Yearly Analysis 2](https://github.com/user-attachments/assets/d45c828c-c0dd-4a46-a0c3-3f33c0c9c765)
![Yearly Analysis 3](https://github.com/user-attachments/assets/3b9170ad-c5f7-42d6-98c1-3e7ba56fdfd3)

### 4. Additional pages
- **Festive Analysis:** performance during festive seasons
- **Forecast:** projected sales

---

## 📐 Key Measures

| Measure | Definition |
|---|---|
| Total Sales | Net sales for the selected period |
| MTD Sales | Month-to-date sales |
| Δ Sales % | (MTD Sales − Last Year MTD) ÷ Last Year MTD |
| AOV (Average Order Value) | Total Sales ÷ Total Orders |
| AvSP (Average Selling Price) | Total Sales ÷ Total Quantity |
| Target Achievement % | Total Sales ÷ Monthly Target |
| Target Balance | Total Sales − Monthly Target |
| Extrapolated Sales | Projected month-end sales based on performance to date |
| GP% | (Sales − Cost) ÷ Sales, with cost sourced from MLS |

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `MSR @ Daily Sales Report.pbix` | Power BI report file |
| `data_flow_diagram.drawio` | Data pipeline and architecture diagram |
| `README.md` | Project documentation |

---

## ▶️ How to Use

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (Windows).
2. Clone or download this repository.
3. Open `MSR @ Daily Sales Report.pbix`.
4. Use the slicers (Outlet, Date, FY/Quarter/Month, Date Range) to explore the data.

> **Note:** Live data connections (BigQuery, BC365, Google Sheets) require credentials and will not refresh outside the original environment. The report opens with the last cached data.

---

## 👤 Author

**Hazwan Othman**
Data Analyst · Power BI · SQL · BigQuery

[GitHub](https://github.com/hazwanothman)
