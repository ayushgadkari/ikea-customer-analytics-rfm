# 📦 IKEA Gifting: Customer Analytics and RFM Segmentation

*An end-to-end data analytics portfolio project built **completely from scratch for learning purposes** to demonstrate practical expertise in SQL, Python, and Power BI.*

---

⚠️ Disclaimer & Acknowledgements

Educational & Skill Demonstration Purpose: This repository contains an end-to-end data analytics project built locally from scratch to practice, demonstrate, and showcase my hands-on capabilities across SQL, Python (pandas), and Power BI.

Project Concept & Inspiration: The original project idea and business framework were inspired by an online tutorial series by Mansi Goel (YouTube: Mansi G.). I independently executed the technical implementation from scratch to validate my skills.

Custom Adaptations & Differences: Please note that this project is not an exact copy of the original tutorial. It includes custom modifications, small logic tweaks, and tailored visual enhancements developed during my own analysis and problem-solving process.

Fictional Brand: IKEA Gifting is a fictional brand used solely for design, storytelling, and educational portfolio purposes. It is not affiliated with, endorsed by, or representative of the real IKEA corporation. All metrics are derived from the public, anonymized UCI Online Retail II dataset.

---

## 💡 About This Project & Learning Objectives

This project was built from scratch as a **hands-on learning initiative** to master the complete data analytics lifecycle—from defining business requirements to engineering data and presenting executive intelligence.

By executing this end-to-end workflow, I gained practical experience connecting multiple data tools into a single pipeline rather than studying them in isolation:
* **Writing a Business Requirements Document** before touching any data to ensure technical work answers actual business questions.
* **Handling Real Data Quality Issues** — tackling mixed date formats, invalid row types, duplicate transactions, and missing customer identifiers in SQL Server.
* **RFM Analysis & Segmentation** — engineering custom metrics in Python to quantify customer worth and group them into actionable tiers (Champions, Loyal, At Risk, Lost, etc.).
* **Executive Data Visualization** — designing interactive, structured reporting views in Power BI Desktop.

---

## 🎯 Business Problem & Purpose

The objective of this project was to simulate a real-world customer analytics engagement for a fictional e-commerce retailer (**IKEA Gifting**). The primary goal was to identify high-value customer segments and detect early churn risks to enable targeted retention strategies.

### Key Questions Answered

* **Customer Value:** Who are our most valuable customers, and what proportion of overall revenue do they drive?
* **Churn Identification:** Which customer segments are showing signs of inactivity and are at risk of churning?
* **Geographic & Temporal Trends:** How do customer value and retention rates vary across regions and over time (months, quarters, years)?
* **Actionable Strategy:** What concrete marketing and retention steps should be tailored for each specific RFM segment?

---

## 🔑 Key Analytics Findings

* **80/20 Revenue Concentration:** The **Champions** segment represents roughly **22%** of the total customer base but contributes close to **68% of total revenue**.
* **High Churn Risk:** Overall customer churn sits at **50.86%** (using a 90-day inactivity threshold), indicating that retention strategies are a critical business driver.
* **Seasonality:** Strong Q4 spikes in revenue align with the seasonal and gifting nature of the product catalog.

---

## 🛠️ Tools & Technologies Learned

Through building this project from scratch, I gained hands-on technical skills across three core analytics tools:

| Tool | Focus & Application |
| :--- | :--- |
| **SQL Server / SSMS** | Data ingestion, data type formatting, window functions for duplicate removal, and large-scale exploratory querying on 1M+ rows. |
| **Python (pandas, Jupyter)** | Data transformation, calculating Recency, Frequency, and Monetary (RFM) metrics, quantile scoring, and customer churn logic. |
| **Power BI Desktop & DAX** | Dimensional modeling, custom DAX metrics, interactive UX design (page navigation, bookmark toggles, conditional formatting gradients). |

---

## 🔄 Project Workflow & Repository Structure

```text
ikea-customer-analytics-rfm/
│
├── 01_sql/
│   └── data_cleaning.sql          # SQL scripts for data cleaning and mixed date fixes
│
├── 02_python/
│   └── rfm_segmentation.ipynb     # Jupyter Notebook for RFM calculation and scoring
│
├── 03_powerbi/
│   └── dashboard_preview.png      # Screenshots or links for the Power BI dashboard
│
├── data/
│   └── README.md                  # Instructions to access the raw UCI dataset
│
└── README.md                      # Complete project documentation
```

---

## 📱 Dashboard Overview (Power BI)

* **Page 1 — Home Page:** Project introduction, navigation structure, and an interactive metrics glossary defining Recency, Frequency, Monetary, and Churned %.
* **Page 2 — Executive Overview:** High-level KPIs (total customers, revenue, churn %, average customer value) with time-series and geographic breakdown views.
* **Page 3 — RFM Analysis Deep Dive:** Detailed segment performance matrix showing customer distribution, average R/F/M scores with conditional color gradients, and revenue concentration.

---

## 💻 Code Highlights

### SQL: Converting Mixed Date Formats
```sql
SELECT
    Invoice, StockCode, Description, Quantity,
    COALESCE(
        TRY_CONVERT(datetime2, InvoiceDate, 120),
        TRY_CONVERT(datetime2, InvoiceDate, 105)
    ) AS InvoiceDate,
    TRY_CONVERT(decimal(10,2), Price) AS Price,
    Customer_ID, Country
INTO dbo.RetailCombined
FROM dbo.[Year 2009-2010];
```

### Python: Quantile-based RFM Scoring
```python
# Quantile scoring for Recency, Frequency, and Monetary value
rfm['R_Score'] = pd.qcut(rfm['Recency'], 5, labels=[5, 4, 3, 2, 1]).astype(int)
rfm['F_Score'] = pd.qcut(rfm['Frequency'].rank(method='first'), 5, labels=[1, 2, 3, 4, 5]).astype(int)
rfm['M_Score'] = pd.qcut(rfm['Monetary'], 5, labels=[1, 2, 3, 4, 5]).astype(int)
```

---

## 🚀 How to Reproduce This Project

1. Clone this repository to your local computer.
2. Download the **Online Retail II** dataset from the UCI Machine Learning Repository.
3. Execute the SQL scripts in `01_sql/` to generate the clean database table.
4. Run the Jupyter Notebook in `02_python/` to calculate customer RFM scores and generate the output file.
5. Explore the Power BI report structure or view the screenshots in `03_powerbi/`.
