# 📦 Inventory Replenishment, Stock-Out Risk & Order Fulfillment Analysis (SQL)

## 📌 Project Overview

This project analyzes a relational e-commerce order and inventory database using **MySQL** to solve core **Supply Chain, Inventory Control, and Order Fulfillment** challenges.  
The primary objective was to track real-time SKU stock levels post-fulfillment, identify critical stock-out risks, evaluate bulk ordering behavior, and uncover regional/seasonal demand spikes to support data-driven replenishment planning.

---

## 🗄️ Relational Schema & Supply Chain Data Model

The database consists of three interconnected operational tables linking **Customer Demand**, **Order Fulfillment**, and **Warehouse Inventory**:

- **`Books` (SKU & Inventory Master):** Catalog details including SKU/Book ID, Author/Supplier, Category/Genre, Unit Price, and Available Warehouse Stock.
- **`Customers` (Destination & Distribution Master):** Registered customer records with City and Country attributes for regional logistics mapping.
- **`Orders` (Fulfillment Transactions):** Transactional order logs capturing Order Date, Fulfilled Quantity, and Total Order Value.

### Entity Relationship Flow
```text
Customers (Destination) ──► Orders (Fulfillment) ──► Books (SKU Inventory)
```

![Table_Structure](screenshots/table_structure.pdf)

---

## 🛠️ Tools & SQL Techniques Applied

- **Database Engine:** MySQL Workbench
- **Core SQL Operations:** Multi-table `INNER JOIN`s, Conditional Filtering (`WHERE`, `HAVING`), Aggregations (`SUM`, `COUNT`, `AVG`)
- **Advanced Analytics:** Subqueries, Common Table Expressions (CTEs), and Window Functions (`SUM() OVER`) for cumulative demand and real-time stock balance tracking

---

## 🎯 Supply Chain & Operations Problems Solved

### 🔹 Inventory Control & Replenishment Risk
- **Total Warehouse Stock Valuation & Count:** Calculated total available inventory across 500 unique SKUs.
- **Stock-Out & Critical Threshold Detection:** Identified SKUs hitting minimum stock thresholds requiring immediate procurement replenishment.
- **Real-Time Post-Fulfillment Stock Calculation:** Built dynamic SQL queries subtracting cumulative `Orders[Quantity]` from `Books[Stock]` to determine live net inventory balances.

### 🔹 Demand Planning & Order Velocity
- **Seasonal Demand Surge Analysis:** Isolated order volume spikes during peak periods (November 2023) to guide safety stock adjustments.
- **Bulk Order & Multi-Unit Fulfillment:** Flagged multi-quantity orders (`Quantity > 1`) to assess warehouse picking/packing volume vs. single-unit shipments.
- **Category-Level Velocity:** Measured unit turnover across product categories (Fantasy, Science Fiction, Biography) to support ABC inventory prioritization.

### 🔹 Regional Distribution & High-Value Order Mapping
- **Cross-Border & Regional Demand Hubs:** Mapped order frequency and revenue concentration across international markets (Canada, Nicaragua, Denmark) and high-value urban hubs (East Craigfort, Schroederton).
- **Repeat Order & Customer Retention Tracking:** Identified repeat buyers (`2+ orders`) to forecast recurring baseline demand.

---

## 📊 Key Operational & Inventory Metrics

| Supply Chain KPI | Finding / Metric |
| :--- | :--- |
| **Total Orders Fulfilled** | 500 transactional orders |
| **Active SKU Catalog Size** | 500 unique titles/SKUs |
| **Highest Unit Value SKU** | *$49.98* ("Proactive system-worthy orchestration") |
| **Peak Demand Period** | November 2023 (significant seasonal order surge) |
| **Top International Demand Markets** | Nicaragua, Denmark, and Canada |
| **Order Profile** | Majority of orders involve multi-unit quantities (`> 1 unit`) |

---

## 🔍 Key Supply Chain Insights

### 1. Inventory & Replenishment Risks
- **Critical Stock Depletion:** Multiple high-velocity SKUs have fallen to minimum stock levels, creating immediate lost-sales exposure if reorder points are not triggered.
- **Real-Time Inventory Visibility:** Subtracting fulfilled quantities from initial stock exposed discrepancies between catalog listings and actual available-to-promise (ATP) inventory.

### 2. Demand & Category Velocity
- **High-Turnover Categories:** *Fantasy* leads in multi-unit order frequency, requiring higher safety stock buffers, whereas *Science Fiction* demonstrates steady baseline velocity.
- **High-Value Low-Volume SKUs:** *Biography* and premium *Fantasy* titles drive disproportionate revenue per unit despite lower unit movement—ideal candidates for strict **ABC inventory classification**.

### 3. Regional Logistics & Fulfillment Patterns
- **Concentrated High-Value Shipments:** Orders exceeding $30 cluster heavily in specific cities (*East Craigfort*, *Schroederton*) and international markets (*Canada*, *Nicaragua*, *Denmark*), indicating opportunities for regional carrier optimization and bulk shipping consolidation.

---

## 📸 Query Execution & Output Previews

### Total Fulfilled Order Revenue
![Total Revenue](screenshots/total_revenue.png)

### Category-Wise Unit Demand Velocity
![Genre Wise Sales Performance](screenshots/genre_wise_sales_performance.png)

### Recurring Demand (Repeat Customers with 2+ Orders)
![Customer Loyality](screenshots/customer_loyality.png)

### Critical Low-Stock SKUs (Reorder Alert)
![Lowest Stock](screenshots/lowest_stock.png)

---

## 💡 Actionable Supply Chain Recommendations

1. **Automate Reorder Point (ROP) Alerts:** Implement automated procurement triggers when live post-fulfillment stock drops below safety stock thresholds for fast-moving *Fantasy* and *Sci-Fi* SKUs.
2. **Seasonal Safety Stock Buffering:** Increase inventory buffers by 20–25% ahead of Q4 (November) to absorb recurring seasonal demand spikes without stock-outs.
3. **Regional Shipping Consolidation:** Negotiate dedicated 3PL/courier rates for high-frequency international corridors (Canada, Nicaragua, Denmark) and high-value urban clusters to reduce per-shipment freight costs.
4. **SKU Bundling for Slow-Moving Stock:** Bundle lower-velocity titles with high-demand genres to accelerate inventory turnover and reduce warehouse holding costs.

---

## 📂 Repository Structure

- `analysis_queries.sql` — Complete SQL script containing inventory tracking, stock-out detection, and demand analysis queries.
- `screenshots/` — Query output screenshots and database schema diagram.