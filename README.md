# 🛍️ Shopify Sales Analysis — Power BI Dashboard

An end-to-end Business Intelligence project that analyses Shopify transaction data to uncover insights into **revenue performance, customer purchasing behaviour, and customer retention**, presented through an interactive Power BI dashboard.

**Author:** Santanu Pathak

---

## 📌 Project Overview

This project analyses a Shopify sales export in Power BI to help store stakeholders understand where revenue comes from, how customers behave, and how well the business retains them. The goal is a single interactive dashboard that lets a non-technical store owner explore the data and walk away with clear, actionable insights.

**Tool used:** Power BI Desktop
**Core skills:** Power Query (ETL), Data Modeling (Star Schema), DAX Measures, Data Visualization

---

## 🎯 Business Objective

Design an interactive dashboard that helps stakeholders (store owners, marketing, and operations teams) spot patterns in revenue generation, customer retention, and engagement — enabling data-driven decisions on merchandising, marketing spend, and customer re-engagement.

**Key business questions answered:**
1. How much revenue is the store generating, and which products drive it?
2. What is the average order value, and how does it vary by customer type?
3. What share of revenue comes from new vs. returning customers?
4. What is the repeat purchase (retention) rate, and how healthy is it?
5. Which regions, payment gateways, and days of the week drive the most orders?

---

## 📊 Key Performance Indicators (KPIs)

| KPI | Value |
|---|---|
| Total Revenue | **$4.60M** |
| Total Orders | **7,431** |
| Total Customers | **4,431** |
| Average Order Value (AOV) | **$618.89** |
| Repeat Purchase Rate | **46.02%** |
| Total Tax Collected | **$418.09K** |

---

## 🗂️ Project Structure

```
Shopify-Sales-Analysis/
│
├── data/                       # Raw and cleaned Shopify export (orders, customers, products)
├── ShopifySalesAnalysis.pbix   # Main Power BI report file
├── docs/
│   ├── Shopify_Sales_Analysis_Report.docx   # Full written project report
│   └── Shopify_Sales_Analysis.pptx          # Presentation deck
├── screenshots/                # Exported dashboard page images
└── README.md                   # This file
```

---

## 🧱 Data Model

The report uses a **star schema**:

- **Fact table:** `Orders` (order ID, customer ID, order date, product, quantity, price, gateway, tax)
- **Dimension tables:** `Customers`, `Products`, `Date` (marked as an official Date table for time intelligence)

This structure keeps relationships simple (one-to-many from dimensions to the fact table) and makes DAX time-intelligence functions (e.g. `TOTALYTD`, `DATEADD`) work correctly.

---

## 🧮 Core DAX Measures

```DAX
Total Revenue = SUM(Orders[Total Price])

Total Orders = DISTINCTCOUNT(Orders[Order ID])

Total Customers = DISTINCTCOUNT(Orders[Customer ID])

Average Order Value = DIVIDE([Total Revenue], [Total Orders])

Repeat Purchase Rate =
DIVIDE(
    CALCULATE(DISTINCTCOUNT(Orders[Customer ID]), Orders[Order Rank] > 1),
    [Total Customers]
)

Revenue - New Customers =
CALCULATE([Total Revenue], Orders[Customer Type] = "New")

Revenue - Returning Customers =
CALCULATE([Total Revenue], Orders[Customer Type] = "Returning")
```

---

## 📈 Dashboard Pages

1. **Sales Analysis** — headline KPIs, revenue by product type, new vs. returning revenue split, billing province map, order type by payment gateway, order quantity by customer type.
2. **Customer Analysis** — customer counts, order frequency distribution, top customers by spend.
3. **Product Performance** — revenue and order volume by product category, top vs. underperforming products.
4. **Retention & Cohort Analysis** — repeat purchase rate, cohort retention by first-purchase month, gap between first and second purchase.
5. **Geographic Analysis** — revenue and orders by billing province/region.

---

## 🔍 Key Insights

- **Running Shoes, Tennis Shoes, and Walking Shoes** are the top three revenue drivers, together contributing roughly **71% of total revenue**.
- **Returning customers generate 40.44% of revenue** despite being a smaller share of the customer base — showing strong customer value once acquired.
- A **46.02% repeat purchase rate** indicates close to half of all customers return for a second order, a solid retention baseline with room to grow.
- **Shopify Payments** is by far the dominant payment gateway, followed by PayPal.
- Low-revenue categories (Clogs, Boy's, Water Shoes) may be candidates for bundling, discontinuation, or a merchandising review.

---

## ✅ Recommendations

1. **Double down on top categories** (Running/Tennis/Walking Shoes) with targeted marketing and inventory investment.
2. **Launch a win-back campaign** aimed at first-time buyers to lift the repeat purchase rate above 46%.
3. **Review long-tail products** (Clogs, Boy's, Water Shoes) for bundling or promotional pricing to reduce dead stock.
4. **Optimize checkout for Shopify Payments and PayPal**, since together they cover the vast majority of transactions.
5. **Use the cohort view** to time re-engagement emails around the typical gap between a customer's first and second purchase.

---

## 🚀 How to Use

1. Open `ShopifySalesAnalysis.pbix` in **Power BI Desktop**.
2. Refresh the data source if connected to a live Shopify export.
3. Use the **slicers** (Billing Address Province, Product Type, Order Type) to filter the report.
4. Click on any chart to **cross-filter** the rest of the dashboard.

---

## 📄 License

This project is for educational purposes as part of a Business Intelligence / Power BI coursework assignment.

---

**Prepared by:** Santanu Pathak
