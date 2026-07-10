# 🛒 E-Commerce Orders — EDA, Analysis & Insights Pipeline

A three-stage, self-contained data analytics pipeline built on a synthetic e-commerce orders dataset. Each notebook can run independently end-to-end — no shared kernel state, no missing dependencies, no guesswork.

Author: Umair Ansari

---

## 📌 Overview

| | |
|---|---|
| 📦 Dataset | Synthetic e-commerce orders |
| 📅 Time span | Jan 2023 – Jun 2025 |
| 🔢 Rows | 1,200 orders (1,208 raw, before cleaning) |
| 📊 Features | 14 columns — pricing, discounts, shipping, delivery, ratings, status |
| 🧰 Stack | Python, pandas, numpy, matplotlib, seaborn |

---

## 📋 Task Summary

| Task | Notebook | Purpose | Output |
|---|---|---|---|
| 1 | Task1_EDA.ipynb | Load, clean, explore | ecommerce_orders_clean.csv |
| 2 | Task2_Analysis.ipynb | Correlation, outliers, segments | Charts + ranked tables |
| 3 | Task3_Insights.ipynb | Insights & recommendations | 5 data-driven findings |

---

## 🗂️ Project Structure

```
📁 DevelopersHub_Assigned_Task2
 ├── 📓 Task1_EDA.ipynb          → Load, clean, and explore the data
 ├── 📓 Task2_Analysis.ipynb     → Correlation, outliers, segment analysis
 ├── 📓 Task3_Insights.ipynb     → Data-driven insights & recommendations
 └── 📄 README.md
```

Pipeline flow:

```
 [ Raw Data ] → 🧹 Clean → 📊 Analyze → 💡 Insight → ✅ Recommend
     Task 1      Task 1      Task 2       Task 3       Task 3
```

Each notebook reloads the cleaned CSV on its own (and regenerates it from scratch if it's missing), so any notebook can be opened and run by itself.

---

## 🗃️ Dataset Schema

| Column | Type | Description |
|---|---|---|
| order_id | string | Unique order identifier |
| customer_id | int | Customer identifier |
| order_date | datetime | Date order was placed |
| product_category | categorical | Product category (8 types) |
| quantity | int | Units ordered |
| unit_price | float | Price per unit |
| discount_percent | int | Discount applied (%) |
| payment_method | categorical | Payment type (4 types) |
| shipping_cost | float | Shipping fee |
| delivery_days | int | Days to delivery |
| customer_rating | float | Rating (1–5) |
| order_status | categorical | Delivered / Cancelled / Returned / Pending |
| region | categorical | Customer region (5 zones) |
| total_amount | float | Final order value |

---

## 🧹 Task 1 — Exploratory Data Analysis

- ✅ Structure & data types (.info(), .describe())
- ✅ Missing value detection — 25 missing customer_rating values found (2.07%)
- ✅ Duplicate detection — 8 duplicate rows found (0.66%)
- ✅ Cleaned dataset saved for downstream use
- ✅ Univariate distributions + categorical breakdowns

Data quality summary:

| Check | Raw Data | After Cleaning |
|---|---|---|
| Total rows | 1,208 | 1,200 |
| Missing values | 25 (customer_rating) | 0 |
| Duplicate rows | 8 | 0 |
| Status | ⚠️ Issues found | ✅ Resolved |

Order status breakdown:

| Status | % of Orders | Visual |
|---|---|---|
| Delivered | 63.3% | ██████████████████████████████ |
| Cancelled | 15.9% | ████████ |
| Returned | 12.9% | ██████ |
| Pending | 7.9% | ████ |

⚠️ 28.8% of all orders never complete successfully — roughly 1 in every 3.

---

## 📊 Task 2 — Correlation & Relationship Analysis

Correlation with total_amount:

| Feature | Correlation (r) | Strength |
|---|---|---|
| unit_price | 0.74 | 🟢 Strong |
| quantity | 0.59 | 🟢 Moderate |
| customer_rating | 0.02 | ⚪ None |
| shipping_cost | 0.01 | ⚪ None |
| delivery_days | 0.01 | ⚪ None |
| discount_percent | -0.08 | 🔴 Negligible |

Revenue by category:

| Category | Revenue | Visual |
|---|---|---|
| Books | $36,656 | ██████████████████████████████ |
| Clothing | $35,662 | █████████████████████████████ |
| Electronics | $35,079 | █████████████████████████████ |
| Beauty | $34,402 | ████████████████████████████ |
| Grocery | $33,692 | ████████████████████████████ |
| Toys | $33,427 | ███████████████████████████ |
| Sports | $29,183 | ████████████████████████ |
| Home & Kitchen | $24,889 | ████████████████████ |

Outliers (1.5× IQR rule):

| Column | Outlier Count | % of Data |
|---|---|---|
| total_amount | 39 | 3.2% |
| unit_price | 25 | 2.1% |
| quantity | 0 | 0.0% |
| discount_percent | 0 | 0.0% |
| shipping_cost | 0 | 0.0% |
| delivery_days | 0 | 0.0% |
| customer_rating | 0 | 0.0% |

Cancel/return rate by payment method:

| Payment Method | Cancel/Return Rate |
|---|---|
| Credit Card | 32.2% |
| Cash on Delivery | 29.5% |
| Debit Card | 28.0% |
| Digital Wallet | 25.4% |

---

## 💡 Task 3 — Insights & Recommendations

| # | Insight | Finding |
|---|---|---|
| 1️⃣ | Fulfillment risk | 28.8% cancel/return rate |
| 2️⃣ | Revenue concentration | Books = 13.9% of total revenue |
| 3️⃣ | Value driver | Unit price outweighs quantity (r=0.74 vs 0.59) |
| 4️⃣ | Payment risk | Credit Card: 32.2% cancel/return vs 25.4% for Digital Wallet |
| 5️⃣ | High-value orders | 3.2% of orders are statistical outliers |

Recommendations:

| Priority | Recommendation | Based On |
|---|---|---|
| 1 | Investigate cancellations by payment method first | Insight 4 |
| 2 | Prioritize pricing strategy over upsell campaigns | Insight 3 |
| 3 | Model high-value orders separately | Insight 5 |
| 4 | Protect top revenue category (Books) with dedicated SLAs | Insight 2 |

---

## ▶️ How to Run

```bash
pip install pandas numpy matplotlib seaborn
jupyter notebook Task1_EDA.ipynb
```

Each notebook runs independently — open any one and run all cells top to bottom.

| Requirement | Version |
|---|---|
| Python | 3.10+ |
| pandas | 2.x |
| numpy | any recent |
| matplotlib | any recent |
| seaborn | any recent |

---

## ⚠️ Limitations

- Dataset is synthetic — relationships are realistic in shape, not sourced from real transactions
- Correlations capture linear relationships only
- Cancellation/return reasons aren't in the data — the pipeline shows where risk concentrates, not why

---

## 👤 Author

Umair Ansari
Data Analytics & Engineering Intern

---
