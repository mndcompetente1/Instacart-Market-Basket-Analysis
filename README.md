# 🛒 Instacart Market Basket Analysis

An interactive **Power BI** report that explores grocery order behavior on Instacart: what customers buy, when they buy it, how big their baskets are, and which products are bought together (using association-rule machine learning).

![Homepage]
<img width="1522" height="880" alt="page_01_homepage" src="https://github.com/user-attachments/assets/437a47b0-06f4-4dac-b46a-447c33bfefaa" />

> **Course / Task:** IT0105 – Finals
> **File:** `Finals_IT0105.pbix`
> **Tools:** Microsoft Power BI Desktop, plus association-rule mining for the ML pages

---

## 📌 Table of Contents
1. [Business Problem](#-business-problem)
2. [Objectives](#-objectives)
3. [Dataset & Data Model](#-dataset--data-model)
4. [Dashboard Walkthrough](#-dashboard-walkthrough)
5. [Machine Learning: Association Rules](#-machine-learning-association-rules)
6. [Key Findings](#-key-findings)
7. [Recommendations](#-recommendations)
8. [How to Open the Project](#-how-to-open-the-project)
9. [Skills Demonstrated](#-skills-demonstrated)

---

## 🎯 Business Problem

Instacart is a U.S.-based grocery delivery and retail media company, founded in 2012, that connects customers with local stores for same-day delivery or pickup. It operates across the United States and Canada, serving millions of households and partnering with thousands of retailers.

With thousands of products across multiple departments, **how can we identify which items drive the most orders and customer engagement?**

![Background]<img width="1522" height="880" alt="page_02_background" src="https://github.com/user-attachments/assets/025fc3f3-cca5-4619-a0e9-ee084dc19e6f" />


## ✅ Objectives

- Identify **top-selling products per department**.
- Understand **customer purchasing behavior** (e.g., staples vs. impulse buys).
- Provide actionable insights for **inventory management and marketing strategies**.
- Build a **dashboard** that allows stakeholders to explore product performance interactively.

![Objectives]("C:\Users\Mico\Downloads\page_03_objectives.png)

---

## 🗃️ Dataset & Data Model

The data follows the Instacart relational schema: orders, order line items, products, aisles, and departments.

![Entity Relationship Diagram](downloads/erd_schema.png)

**Dataset at a glance**

| Total Orders | Unique Customers | Unique Products | Unique Departments |
|:---:|:---:|:---:|:---:|
| ~4K | ~4K | ~50K | 21 |

**Tables in the Power BI model**

| Table | Purpose |
|---|---|
| `RawData` | Base order-level data (order, product, aisle, department, day/hour) |
| `OrdersProductsFull` | Orders joined with product and department details |
| `products` | Product catalog |
| `departments` | Department lookup |
| `BasketSizes` | Basket size per order, with `basket_size` and `basket_size_bucket` (1–5, 6–10, 11+) |
| `TemporalOrders` | Order timing (day of week, hour of day) |
| `Top3ProductsByDept` | Top 3 products per department by order count, with a rank |
| `DepartmentPairs` | Department co-occurrence pairs |

**Custom measures:** *Sum of Orders*, *Unique Customers*, *Unique Products*, *Unique Departments*, and *% Orders per Dept*.

![Data Set and Data Model]("C:\Users\Mico\Downloads\page_04_data_model.png)

---

## 📊 Dashboard Walkthrough

The report has 11 pages with a custom green theme, a home button on every page, and navigation buttons that link all sections.

**Interactivity:** slicers for *Department*, *Basket Size Bucket*, and *Day of Week*, a *Rank* slicer for top products, and reset buttons on each page.

### 1️⃣ Main Dashboard
A summary view with orders by day of week, basket size distribution, and department share of orders by basket size.

![Dashboard]("C:\Users\Mico\Downloads\page_05_dashboard.png)

### 2️⃣ Basket Analysis
Shows how many items customers put in a basket and how the department mix changes as baskets get larger.

![Basket Analysis]("C:\Users\Mico\Downloads\page_06_basket_analysis.png)

### 3️⃣ Department Segmentation
Ranks departments by orders, shows the top products inside each one, and compares department share across basket sizes.

![Department Segmentation]("C:\Users\Mico\Downloads\page_07_department_segmentation.png)

### 4️⃣ Temporal Patterns
Looks at when customers order: by day of week, by hour of day, and which departments dominate at each hour.

![Temporal Patterns]("C:\Users\Mico\Downloads\page_08_temporal_patterns.png)

---

## 🤖 Machine Learning: Association Rules

To go beyond descriptive charts, I used **market-basket association rule mining** (support and lift) to find products that are frequently bought together. A **lift above 1** means the items appear together more often than chance would suggest.

![Machine Learning]("C:\Users\Mico\Downloads\page_09_machine_learning.png)

### Overall and by Basket Size

| High Support + High Lift | Small vs. Large Baskets |
|---|---|
| ![Overall](images/ml_high_support_lift.jpg) | ![Basket size](images/ml_basket_size_rules.jpg) |

- **Overall:** Organic bananas ↔ Organic Hass avocados is the strongest pair (lift ≈ 2.6).
- **Small baskets:** bananas ↔ avocados (lift ≈ 4.4).
- **Large baskets:** lemon ↔ avocado, zucchini ↔ baby spinach, bananas → raspberries.

### By Department

![Departmental Rules]("C:\Users\Mico\Downloads\page_10_departmental_rules.png)

| Produce | Beverages | Frozen |
|---|---|---|
| ![Produce](images/ml_rules_produce.jpg) | ![Beverages](images/ml_rules_beverages.jpg) | ![Frozen](images/ml_rules_frozen.jpg) |

- **Produce:** bananas ↔ raspberries and bananas ↔ avocados are the strongest pairs.
- **Beverages:** sparkling water flavors are bought together (lift up to ≈ 6).
- **Frozen:** strawberries ↔ frozen wild blueberries (lift ≈ 7).

---

## 🔍 Key Findings

![Findings and Recommendations]("C:\Users\Mico\Downloads\page_11_conclusion.png)

1. **Basket size distribution:** most baskets hold **5–15 items**, with a sharp drop after 20+. Small baskets (1–5) are common, but large baskets (11+) still make up a significant share.
2. **Basket size vs. department mix:**
   - Small baskets lean toward snacks, personal care, and quick-need items.
   - Medium baskets (6–10) mix pantry staples and produce.
   - Large baskets (11+) are dominated by produce and snacks, which points to planned, full-stock shopping trips.
3. **Department share of orders:** Produce consistently drives the highest order counts, Dairy & Eggs and Beverages are strong secondary contributors, and smaller departments (personal care, pets, alcohol) appear mostly in small baskets.
4. **Temporal patterns:**
   - **Day of week:** orders peak on Day 1 and are lowest on Day 4.
   - **Hour of day:** orders peak from mid-morning to early afternoon.
   - **Department by time:** Produce and snacks dominate during peak hours.

## 💡 Recommendations

| Area | Action |
|---|---|
| **Basket-size targeting** | Promote snack + beverage bundles for small baskets to encourage upsizing; reinforce produce + pantry combos for large baskets. |
| **Cross-selling & personalization** | Deploy "Frequently Bought Together" suggestions from the ML rules (e.g., bananas → raspberries, sparkling water flavors); highlight frozen fruit pairings for health-focused customers. |
| **Dairy & Eggs** | Create curated bundles (milk + bread, eggs + bacon) and place dairy next to pantry staples to raise basket penetration. |
| **Time-based promotions** | Push fresh produce and snack offers during peak hours (10 AM–3 PM) and run weekly "Day 1" campaigns. |
| **Department strategy** | Keep produce as the anchor department, use beverages and dairy as secondary drivers, and elevate smaller departments in small-basket campaigns. |

---

## ▶️ How to Open the Project

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free, Windows).
2. Download or clone this repository.
3. Open `Finals_IT0105.pbix`.
4. Start from the **Homepage** and use the navigation buttons and slicers to explore.

> The report uses the **Icon Map Pro** custom visual, which is bundled inside the file.

---

## 🧰 Skills Demonstrated

- **Data modeling:** relational schema, table relationships, and derived tables (basket sizes, top-3 products, department pairs)
- **DAX:** custom measures for orders, unique counts, and percentage-of-department share
- **Data visualization & UX design:** themed multi-page report with navigation buttons, slicers, and a consistent layout
- **Exploratory analysis:** basket size, department mix, and temporal patterns
- **Machine learning:** association rule mining (support and lift) for cross-selling insights
- **Business storytelling:** turning findings into concrete marketing and inventory recommendations

---

## 👤 Author

**Matthew Nicolai D. Competente**
