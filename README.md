# ecommerce-analytics-project
# 📦 E-Commerce Business Intelligence Platform

> **Project Type:** Data Analytics | End-to-End Pipeline  
> **Domain:** E-Commerce / Retail  
> **Assigned By:** Senior Data Analytics Manager  
> **Sprint Duration:** 3 Weeks  
> **Status:** 🟡 In Progress

---

## 📌 Project Overview

This project delivers a full-scale business intelligence solution for a multi-channel e-commerce company operating across **Amazon India**, **International Markets**, and multiple retail platforms (Ajio, Flipkart, Myntra, Snapdeal, Paytm, Limeroad).

The goal is to ingest raw, messy sales data from 6 different sources, clean and transform it into a reliable data layer, and surface **actionable business insights** through SQL analysis and an interactive Power BI dashboard — enabling data-driven decisions across sales, inventory, pricing, and operations.

---

## 🎯 Business Objectives

- Identify top-performing states, categories, and SKUs by revenue
- Measure and reduce Amazon order cancellation rates
- Compare profit margins across all retail platforms
- Analyse international vs domestic revenue split
- Track inventory health — flag low-stock, high-demand SKUs
- Monitor monthly expense vs revenue trends (IIGF)

---

## 🗂️ Dataset Description

| File | Source | Rows | Key Columns |
|---|---|---|---|
| `Amazon_Sale_Report.csv` | Amazon Seller Central | ~1,28,975 | Order ID, Date, Status, Category, Amount, ship-state |
| `International_sale_Report.csv` | International Orders | ~37,432 | DATE, CUSTOMER, SKU, PCS, RATE, GROSS AMT |
| `Sale_Report.csv` | Internal Inventory | ~9,271 | SKU Code, Design No., Stock, Category, Size, Color |
| `May-2022.csv` | MRP Pricing Sheet | ~1,330 | SKU, Category, TP, MRP, Platform-wise MRP |
| `P__L_March_2021.csv` | Profit & Loss Sheet | ~1,330 | SKU, TP 1, TP 2, Platform-wise MRP |
| `Expense_IIGF.csv` | Expense Tracker | ~17 | Received Amount, Expense, Particulars |

---

## 🔴 Known Data Quality Issues (Pre-Cleaning)

The raw datasets contain the following problems that must be resolved before analysis:

| Issue | Description | Affected Files |
|---|---|---|
| **Missing Values** | ~5% nulls in key columns (Order ID, Amount, Status) | All files |
| **Duplicate Rows** | ~3% duplicate records from system exports | All files |
| **Inconsistent Date Formats** | Mix of `MM-DD-YY` and `MM/DD/YY` | Amazon, International |
| **Case Inconsistency** | `MUMBAI` vs `mumbai` vs `Mumbai` | City, Category, Status |
| **Whitespace Corruption** | Leading/trailing spaces in text fields | All files |
| **Dtype Corruption** | `'N/A'` string injected in numeric columns | All files |
| **Negative Outliers** | Negative values in Amount, Qty, Stock, Rate | Amazon, International, Sale Report |

---

## 🛠️ Tech Stack

| Phase | Tool | Purpose |
|---|---|---|
| Version Control | Git + GitHub | Code tracking, collaboration |
| Data Profiling | Python — `ydata-profiling` | Auto quality report before cleaning |
| Data Cleaning | Python — `Pandas` in Jupyter Notebook | Fix nulls, duplicates, dtypes, formats |
| Data Storage | MySQL / PostgreSQL | Structured querying of cleaned data |
| EDA | Python — `Matplotlib`, `Seaborn` | Statistical exploration and charts |
| Dashboard | Power BI / Tableau / Looker Studio | Interactive business dashboard |
| Reporting | PowerPoint + PDF | Final presentation to stakeholders |

---

## 📁 Project Structure

```
ecommerce-analytics-project/
│
├── data/
│   ├── raw/                        ← Original dirty CSV files (do not modify)
│   │   ├── Amazon_Sale_Report_DIRTY.csv
│   │   ├── International_sale_Report_DIRTY.csv
│   │   ├── Sale_Report_DIRTY.csv
│   │   ├── May-2022_DIRTY.csv
│   │   ├── P__L_March_2021_DIRTY.csv
│   │   └── Expense_IIGF_DIRTY.csv
│   └── cleaned/                    ← Output after cleaning pipeline
│
├── notebooks/
│   ├── 01_data_profiling.ipynb     ← ydata-profiling reports
│   ├── 02_data_cleaning.ipynb      ← Full cleaning pipeline
│   ├── 03_eda_amazon.ipynb         ← Amazon sales EDA
│   ├── 04_eda_international.ipynb  ← International sales EDA
│   └── 05_margin_analysis.ipynb    ← P&L and platform margin EDA
│
├── scripts/
│   ├── clean_amazon.py             ← Reusable cleaning script
│   ├── clean_international.py
│   └── load_to_db.py               ← Load cleaned data into MySQL
│
├── sql/
│   ├── schema.sql                  ← Table creation scripts
│   ├── revenue_analysis.sql        ← Business queries
│   └── cancellation_analysis.sql
│
├── reports/
│   ├── amazon_profile.html         ← Data quality profile report
│   ├── dashboard.pbix              ← Power BI dashboard file
│   └── final_presentation.pdf      ← Manager-ready slide deck
│
└── README.md
```

---

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/ecommerce-analytics-project.git
cd ecommerce-analytics-project
```

### 2. Install Dependencies
```bash
pip install pandas numpy matplotlib seaborn ydata-profiling jupyter sqlalchemy pymysql
```

### 3. Run Data Profiling
```bash
jupyter notebook notebooks/01_data_profiling.ipynb
```

### 4. Run Cleaning Pipeline
```bash
jupyter notebook notebooks/02_data_cleaning.ipynb
# OR run as a script:
python scripts/clean_amazon.py
```

### 5. Load into Database
```bash
python scripts/load_to_db.py
```

### 6. Open Dashboard
Open `reports/dashboard.pbix` in Power BI Desktop and refresh the data source to `data/cleaned/`.

---

## 📊 Key Business Questions Answered

**Sales Performance**
- Which are the top 10 states by revenue on Amazon India?
- What is the month-over-month sales growth trend?
- Which product categories drive the most orders vs most revenue?

**Cancellation Analysis**
- What is the overall cancellation rate across all orders?
- Which states/categories have the highest cancellation rates?
- What is the revenue lost due to cancellations?

**Margin & Pricing Analysis**
- Which retail platform (Amazon, Flipkart, Myntra, Ajio etc.) offers the best margin?
- What is the TP-to-MRP ratio per category?
- Which SKUs are being sold below cost price?

**Inventory Intelligence**
- Which SKUs are critically low in stock but have high sales velocity?
- Which sizes or colors are overstocked?

**International Revenue**
- What percentage of total revenue comes from international orders?
- Who are the top international customers by gross amount?

---

## 📅 Project Timeline

```
Week 1  ──► Git Setup → Data Profiling → Data Cleaning (all 6 files)
Week 2  ──► EDA → SQL Queries → Business Questions Answered
Week 3  ──► Power BI Dashboard → Final Presentation → Manager Review
```

---

## 📈 Dashboard Sections (Power BI)

| Section | Visual Type | Metric |
|---|---|---|
| Overview KPIs | Cards | Total Revenue, Orders, Cancellation Rate |
| Revenue by State | Horizontal Bar Chart | Top 10 States |
| Monthly Trend | Line Chart | Revenue & Orders over time |
| Category Breakdown | Donut Chart | Revenue share by category |
| Platform Margin | Clustered Bar | TP vs MRP across platforms |
| International Map | Filled Map | Revenue by customer geography |
| Inventory Risk | Table | Low stock + high demand SKUs |

---

## 👥 Team & Roles

| Role | Responsibility |
|---|---|
| Data Analyst (You) | Cleaning, EDA, SQL, Dashboard |
| Data Engineering Lead | Database setup, pipeline review |
| Business Analyst | Requirement gathering, insight validation |
| Analytics Manager | Final review and stakeholder presentation |

---

## 📝 Deliverables Checklist

- [ ] Data quality profiling report (HTML)
- [ ] Cleaned datasets in `data/cleaned/`
- [ ] Jupyter notebooks with documented cleaning steps
- [ ] SQL schema + business query files
- [ ] Power BI dashboard (`.pbix`)
- [ ] Final presentation deck (10 slides, PDF)
- [ ] README updated with findings summary

---

## ⚠️ Important Notes

- **Never modify files in `data/raw/`** — these are the original source files preserved for audit trail
- All cleaning steps must be **documented in notebooks** with comments explaining each decision
- Any assumption made during cleaning (e.g. imputation strategy) must be logged in the notebook markdown
- Cleaned data must pass a **validation check script** before being loaded to the database

---



---

*This project follows the company's standard Data Analytics delivery framework. All data is for internal business use only.*
