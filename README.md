# 📊 UPI Transaction Analysis — End-to-End Data Analytics Project

<p align="center">
  <img src="https://img.shields.io/badge/SQL-MySQL-blue?style=for-the-badge&logo=mysql&logoColor=white"/>
  <img src="https://img.shields.io/badge/Excel-Pivot%20Tables%20%26%20Charts-green?style=for-the-badge&logo=microsoftexcel&logoColor=white"/>
  <img src="https://img.shields.io/badge/Power%20BI-DAX%20Dashboard-yellow?style=for-the-badge&logo=powerbi&logoColor=white"/>
  <img src="https://img.shields.io/badge/Dataset-250%2C000%20rows-orange?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge"/>
</p>

---

## 🧾 Project Overview

This is a **complete end-to-end data analytics project** on **2,50,000 UPI (Unified Payments Interface) transactions** recorded across India from **January to October 2024**.

The project covers the full analyst pipeline:
> **Raw CSV → SQL Database → Excel Analysis → Power BI Dashboard**

The goal is to uncover payment patterns, identify failure causes, detect fraud risks, and build an interactive business intelligence dashboard — all using three industry-standard tools.

---

## 🗂️ Repository Structure

```
UPI-Transaction-Analysis/
├── README.md
├── dataset/
│   └── upi_transactions_2024.csv        ← 2,50,000 rows | 17 columns
├── sql/
│   └── UPI_SQL_Queries.sql              ← 17 queries (Basic + Advanced) + View
├── excel/
│   └── upi_analysis.xlsx                ← Cleaned data + Pivot Tables + Dashboard
├── powerbi/
│   └── upi_analysis.pbix                ← 3-page interactive Power BI report
└── report/
    └── UPI_Project_Report.docx          ← Full project report (8 sections)
```

---

## 📦 Dataset Description

| Property | Details |
|---|---|
| **Rows** | 2,50,000 transactions |
| **Columns** | 17 features |
| **Date Range** | January 2024 – October 2024 |
| **Total Value** | ₹32.79 Crore |
| **Source** | Synthetic UPI transaction dataset |

### Columns

| Column | Description |
|---|---|
| `transaction_id` | Unique ID for each transaction |
| `timestamp` | Date and time of the transaction |
| `transaction_type` | P2P, P2M, Bill Payment, Recharge |
| `merchant_category` | Shopping, Grocery, Fuel, Food, Utilities, etc. |
| `amount (INR)` | Transaction value in Indian Rupees |
| `transaction_status` | SUCCESS or FAILED |
| `sender_age_group` | 18-25, 26-35, 36-45, 46-55, 56+ |
| `sender_state` | State of the sender (10 states) |
| `sender_bank` | Bank used by sender (8 banks) |
| `receiver_bank` | Bank used by receiver |
| `device_type` | Android, iOS, Web |
| `network_type` | 3G, 4G, 5G, WiFi |
| `fraud_flag` | 1 = Fraud, 0 = Normal |
| `hour_of_day` | Hour of transaction (0–23) |
| `day_of_week` | Monday – Sunday |
| `is_weekend` | 1 = Weekend, 0 = Weekday |

---

## 🛠️ Tools & Technologies

| Tool | Version | Purpose |
|---|---|---|
| **MySQL** | 8.0+ | Database creation, querying, CTEs, Window Functions |
| **Microsoft Excel** | 2019/365 | Data cleaning, SUMIFS, Pivot Tables, Dashboard |
| **Power BI Desktop** | Latest | Power Query ETL, DAX Measures, Interactive Dashboard |

---

## 📁 Phase 1 — SQL Analysis

**File:** `sql/UPI_SQL_Queries.sql`

### Basic Queries (Q1–Q8)
| Query | Description |
|---|---|
| Q1 | Total transaction count |
| Q2 | Amount summary — total, avg, min, max |
| Q3 | Transactions by type (P2P / P2M / Bill / Recharge) |
| Q4 | Success vs Failed rate with percentage |
| Q5 | Top 5 merchant categories by total spending |
| Q6 | State-wise transaction volume |
| Q7 | Device type breakdown (Android / iOS / Web) |
| Q8 | Transactions by day of week |

### Advanced Queries (Q9–Q17)
| Query | SQL Concept | Description |
|---|---|---|
| Q9 | **CTE** | Monthly transaction trend (Jan–Oct 2024) |
| Q10 | **RANK() Window Function** | Bank ranking by transaction volume |
| Q11 | **CASE WHEN** | Failure rate by network type |
| Q12 | **CASE WHEN** | Amount bucket classification |
| Q13 | **RANK()** | Peak hour analysis |
| Q14 | **GROUP BY** | Weekend vs weekday spending |
| Q15 | **GROUP BY** | Age group spending behaviour |
| Q16 | **Self JOIN** | Bank-to-bank transfer flow |
| Q17 | **Multi-condition CASE** | Fraud risk detection & scoring |

### Bonus
- `CREATE VIEW fraud_risk_summary` — reusable fraud view, directly connectable to Power BI

---

## 📁 Phase 2 — Excel Analysis

**File:** `excel/upi_analysis.xlsx`

### Sheets
| Sheet | Contents |
|---|---|
| `Raw Data` | Original imported CSV data |
| `Cleaned Data` | Fixed timestamps, added Amount Bucket column |
| `Analysis` | SUMIFS, COUNTIFS, AVERAGEIFS formulas + 4 Pivot Tables |
| `Dashboard` | Combined charts with 4 connected slicers |

### Pivot Tables
- **PT1:** Monthly transaction volume by type
- **PT2:** Merchant category vs average amount
- **PT3:** State-wise success rate
- **PT4:** Bank-wise performance summary

### Key Formulas Used
```excel
=SUMIFS(amount, sender_bank, "SBI")              → Bank-wise revenue
=COUNTIFS(status, "FAILED", network, "3G")       → Network failure count
=AVERAGEIFS(amount, is_weekend, 1)               → Weekend avg spend
=XLOOKUP(state, state_list, region_list)         → State to region mapping
```

---

## 📁 Phase 3 — Power BI Dashboard

**File:** `powerbi/upi_analysis.pbix`

### DAX Measures
```dax
Total Revenue       = SUM(upi_transactions[amount])
Success Rate %      = DIVIDE(COUNTIF(status=SUCCESS), COUNTROWS())
Failure Rate %      = DIVIDE(COUNTIF(status=FAILED), COUNTROWS())
Avg Transaction Val = AVERAGE(upi_transactions[amount])
Fraud Count         = CALCULATE(COUNTROWS(), fraud_flag = 1)
Fraud Rate %        = DIVIDE([Fraud Count], [Transaction Count])
Weekend Txn %       = DIVIDE(COUNTIF(is_weekend=1), COUNTROWS())
```

### Report Pages
| Page | Visuals |
|---|---|
| **1. Executive Summary** | KPI cards, monthly trend line, transaction type donut, top categories bar |
| **2. Bank & State Analysis** | Map visual, bank performance bar, bank-to-bank matrix, device by state |
| **3. Fraud & Risk Intelligence** | Fraud KPIs, failure by network, risk scatter plot, top suspicious transactions |

### Interactivity Features
- ✅ **5 Slicers** — Month, Transaction Type, Bank, Device, Network
- ✅ **Drill-through** — Click any state → view its individual transactions
- ✅ **Bookmarks** — "Show Fraud Only" toggle button
- ✅ **Custom Tooltips** — Additional KPIs on chart hover
- ✅ **Cross-filtering** — All visuals respond to each other

---

## 🔍 Key Findings

| # | Finding | Detail |
|---|---|---|
| 1 | **High Success Rate** | 95.05% of all 2,50,000 transactions succeeded |
| 2 | **P2P Dominates** | P2P = 44.9% of all transactions (1,12,445 txns) |
| 3 | **SBI #1 Bank** | SBI handles 62,693 transactions — 25.1% market share |
| 4 | **3G Has Highest Failure** | 3G failure rate = 5.22% vs 4.86% on 5G/WiFi |
| 5 | **Top State: Maharashtra** | 37,427 transactions — 14.97% of total volume |
| 6 | **Top Spenders: Age 26–35** | ₹11.60 Crore spent — highest of all age groups |
| 7 | **Android Dominates** | 75.1% of transactions happen on Android devices |
| 8 | **480 Fraud Cases** | 0.19% fraud rate — highest risk on 3G after 10PM |

---

## 📊 Dashboard Preview

> *(Add screenshots of your Power BI dashboard pages here)*

| Executive Summary | Bank & State Analysis | Fraud & Risk |
|---|---|---|
| ![Page 1](screenshots/powerbi_page1.png) | ![Page 2](screenshots/powerbi_page2.png) | ![Page 3](screenshots/powerbi_page3.png) |

> *(Also add screenshots of SQL query results and Excel dashboard)*

---

## 🚀 How to Run This Project

### SQL
1. Install [MySQL Workbench](https://www.mysql.com/products/workbench/)
2. Create a new schema (database)
3. Import `dataset/upi_transactions_2024.csv` using **Table Data Import Wizard**
4. Open `sql/UPI_SQL_Queries.sql` and run queries one by one

### Excel
1. Open `excel/upi_analysis.xlsx` in Microsoft Excel 2019 or Office 365
2. Navigate to the **Dashboard** sheet
3. Use the slicers to filter by bank, transaction type, or device

### Power BI
1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
2. Open `powerbi/upi_analysis.pbix`
3. If prompted, update the data source path to your local CSV location
4. Explore the 3 report pages using slicers and drill-through

---

## 📈 Project Highlights

```
✔  2,50,000 rows analysed across 3 tools
✔  17 SQL queries — Basic + Advanced (CTEs, Window Functions, Views)
✔  4 Pivot Tables with connected slicers in Excel
✔  8 DAX measures in Power BI
✔  3-page interactive Power BI report
✔  Fraud risk scoring using multi-condition SQL logic
✔  Bank-to-bank flow analysis (unique insight)
✔  Full project report (8 sections, 14 pages)
```

---

## 🧠 Skills Demonstrated

`SQL` `MySQL` `CTEs` `Window Functions` `Data Cleaning` `Excel` `Pivot Tables`
`SUMIFS` `XLOOKUP` `Power BI` `Power Query` `DAX` `Data Visualisation`
`Fraud Detection` `Exploratory Data Analysis` `Business Intelligence` `Storytelling with Data`

---

## 👤 About Me

**Anurag**
Aspiring Data Analyst | SQL • Excel • Power BI

📧 [your email here]
🔗 [LinkedIn profile link here]
🐙 [GitHub profile link here]

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">
  ⭐ If you found this project useful, please give it a star!
</p>
