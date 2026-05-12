# Coffee Shop Sales – Excel Data Modeling

**Transform flat file into relational star schema using Power Query & Power Pivot**

---

## 📌 Project Overview

This project demonstrates **proper data modeling techniques in Excel** – not just formulas and pivot tables.

**The Challenge:** Raw data came as a single flat Excel file with transactions, products, and store information all in one sheet.

**What I Did:**
- Separated flat file into **fact and dimension tables** (star schema)
- Removed duplicates from dimension tables for **data integrity**
- Created **relationships** using Power Pivot data model
- Built calculated fields (**Revenue = Quantity × Price**)
- Created **date dimension** with weekday/month names using Excel formulas (`=TEXT()`, `=MONTH()`, `=WEEKDAY()`)
- Loaded everything into **data model** (not Excel sheets) – handling 1M+ rows

**Tools Used:** Excel, Power Query, Power Pivot, DAX

---

## 💡 Trivia: Why Segment Flat Files into Fact & Dimension Tables?

Most Excel users keep everything in **one flat file**. But this causes problems:

| Problem | Example |
|---------|---------|
| **Duplicate data** | Product name repeats 10,000 times (once per transaction) |
| **Data inconsistency** | "Coffee" vs "coffee" vs "Cofee" – same product, different spellings |
| **Wasted storage** | 50 columns × 1M rows = massive file size |
| **Slow performance** | VLOOKUP scans thousands of rows every time |
| **Hard to maintain** | Update a product name? You must update 10,000 rows |

**When you segment into Fact & Dimension Tables:**

| Benefit | What It Means |
|---------|----------------|
| **One source of truth** | Product name stored once in dim_product – update once, everywhere |
| **Smaller file size** | No duplicate data – only keys in fact table |
| **Faster calculations** | Relationships are optimized; no VLOOKUP needed |
| **Cleaner structure** | Business logic separate from transaction data |
| **Scalable** | Fact table can grow to millions; dimensions stay small |
| **Professional approach** | Same method used in Power BI, SQL Server, and data warehouses |

**Think of it like this:**
- **Flat file** = One giant closet with everything thrown in
- **Star schema** = Organized room: clothes rack (dim_product), shoe rack (dim_store), calendar (dim_date), and log book (fact_sales)

> *"Data modeling is not just for databases. Excel's Power Pivot can handle star schemas too – and it will change how you work with large datasets forever."*

---

## 🎯 Why This Approach is Better

| Traditional Excel | This Approach |
|------------------|----------------|
| VLOOKUP across sheets | **Relationships** in data model |
| Duplicate data everywhere | **One copy per dimension** |
| Slow with 100K+ rows | **Handles 1M+ rows** |
| Formulas break if columns move | **Measures are stable** |
| Cannot build proper dashboards | **Power Pivot dashboards** |

---

## 📊 Data Model Structure (Star Schema)

┌─────────────┐
│ dim_date │
│ - Date │
│ - Month │
│ - Weekday │
└──────┬──────┘
│
┌─────────────┐ ┌─────▼─────┐ ┌─────────────┐
│ dim_product │◄────►│ fact_sales │◄────►│ dim_store │
│ - product_id│ │ - trans_id │ │ - store_id │
│ - category │ │ - quantity │ │ - location │
│ - type │ │ - unit_price│ └─────────────┘
│ - detail │ │ - Revenue │
└─────────────┘ │ - date │
└────────────┘


**Relationships:**
- `fact_sales[product_id]` → `dim_product[product_id]`
- `fact_sales[store_id]` → `dim_store[store_id]`
- `fact_sales[transaction_date]` → `dim_date[Date]`

---

## 🔧 Step-by-Step Process

### Step 1: Load Raw Data into Power Query
Imported flat Excel file containing all transaction data.

### Step 2: Create Dimension Tables

**dim_product** – One row per unique product
- Extracted product columns, removed duplicates on `product_id`

**dim_store** – One row per unique store
- Extracted store columns, removed duplicates on `store_id`

**dim_date** – Date attributes for time analysis
- Created using Excel formulas:
  - `=TEXT(date,"mmm")` → Month name (Jan, Feb, Mar)
  - `=TEXT(date,"ddd")` → Weekday name (Sun, Mon, Tue)
  - `=MONTH(date)` → Month number
  - `=DAY(date)` → Day number
  - `=WEEKDAY(date)` → Weekday number

### Step 3: Create Fact Table

**fact_sales** – Transaction-level data
- Kept transaction columns: `transaction_id`, `date`, `time`, `quantity`, `unit_price`, `store_id`, `product_id`
- **Added calculated Revenue column:** `= quantity × unit_price`

### Step 4: Load to Data Model (Not Excel Sheets)
Used "Only Create Connection" → "Add to Data Model". Bypasses Excel's 1M row limit.

### Step 5: Create Relationships
Connected fact tables to dimension tables using Power Pivot's Diagram View.

### Step 6: Build Dashboard
Insert PivotTables and PivotCharts connected to the data model. No VLOOKUP needed.

---

## 📊 Sample Dashboard Insights

| Visual | Insight |
|--------|---------|
| Revenue by Month | Sales grew from $26K (Jan) to $54K (Jun) |
| Transactions by Day | Weekends (Sat/Sun) have highest volume |
| Transactions by Hour | Peak hours: 8-10 AM and 3-5 PM |
| Top Products | Barista Espresso ($31K), Gourmet Coffee ($23K) |

---

## 🛠️ Skills Demonstrated

| Skill | How |
|-------|-----|
| **Data Modeling** | Star schema (fact & dimension tables) |
| **Power Query** | ETL, data cleaning, transformation |
| **Power Pivot** | Relationships, data model |
| **Excel Formulas** | `TEXT()`, `MONTH()`, `WEEKDAY()`, `DAY()` |
| **Calculated Fields** | Revenue = Quantity × Price |
| **Scalable Design** | Data model handles 1M+ rows |

---

## 🚀 How to Use This File

1. Download `Coffee Shop Dashboard.xlsx`
2. Open in Excel
3. Go to **Power Pivot** → **Manage** to see the data model
4. Go to **Diagram View** to see table relationships

**Requirements:** Excel 2016 or later (Power Pivot included in Professional Plus)

---

## 📅 Project Date

May 2026

## 🔗 Connect with Me

- **LinkedIn:** [linkedin.com/in/reginaldhigoy](https://www.linkedin.com/in/reginaldhigoy/)
- **GitHub:** [github.com/reginaldhigoy](https://github.com/reginaldhigoy)
- **Email:** reginaldhigoy.dev@gmail.com

---

*This project demonstrates data modeling skills – not business insights.*
