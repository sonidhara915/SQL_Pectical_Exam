# SQL_Pectical_Exam
# 🛒 E-Commerce Database Management System

An optimized, production-ready relational database schema designed for modern e-commerce platforms. This project contains structural setups, sample transactional datasets, data cleansing procedures, and advanced analytics queries (including window functions and conditional workflows) to manage customers, catalog segments, and order fulfillment.

---

## 🏗️ Database Architecture & Schema

The ecosystem operates on a highly normalized relational model featuring 7 interconnected tables with enforced referential integrity and cascading deletes.

### 📊 Entity-Relationship Overview

```
 [Categories] ──< [Products] ──< [OrderItems] >── [Orders] >── [Customers]
                                                    │     │
                                                    │     └─── [Shipping]
                                                    └─── [Payments]
```

### 🗂️ Data Dictionary

| Table Name | Primary Key | Foreign Key(s) | Key Responsibility |
| :--- | :--- | :--- | :--- |
| **`customers`** | `customer_id` | *None* | Stores registered user profiles, contact details, and location. |
| **`categories`** | `category_id` | *None* | Defines product classification segments for catalog indexing. |
| **`products`** | `product_id` | `category_id` | Tracks individual items, unit pricing, and real-time inventory. |
| **`orders`** | `order_id` | `customer_id` | Captures order placement dates, global status, and financial subtotals. |
| **`orderitems`** | `order_item_id` | `order_id`, `product_id` | Granular line-item breakdown linking orders to quantities. |
| **`payments`** | `payment_id` | `order_id` | Logs transaction processing methods, timestamps, and settlement status. |
| **`shipping`** | `shipping_id` | `order_id` | Tracks fulfillment logistics, dispatch dates, and final deliveries. |

---

## 📈 Analytics & Advanced Query Intelligence

The architecture includes a comprehensive library of optimized queries categorized by operation type:

### 🔍 1. Filter, Search & Grouping Controls
* **Temporal Audits:** Automatically isolates historical cancelled transactions and filters rolling monthly transactional volumes.
* **Inventory Control:** Lists active products with positive stock levels to prevent catalog overselling.
* **Volume Analysis:** Evaluates total order aggregates grouped by individual buyer accounts.

### 🤝 2. Relational Joins & Data Extraction
* **Cross-Status Integrity Validation:** Cross-references pending order pipelines against confirmed payment records.
* **Fulfillment Pipeline Exceptions:** Identifies orders lacking shipping assignments via strategic outer joins.
* **Dormant Account Isolation:** Spots registered profiles with zero historical transactions for retargeting campaigns.

### 📊 3. Revenue Metrics & Business Intelligence
* **Categorical Performance:** Computes localized revenue totals aggregated across product categories.
* **Macro Revenue Logs:** Aggregates gross platform turnover excluding cancelled pipeline revenue.
* **Fulfillment Logistics Audits:** Analyzes actual delivery timelines using interval-based day counters.

### 💎 4. Advanced Window Functions & Logic Engines
* **VIP Customer Stratification:** Computes exact customer value ranks using dense transaction totals (`RANK() OVER`).
* **Financial Run-Rates:** Tracks dynamic month-over-month cumulative revenue trajectories.
* **Dynamic Segmentation Rules:** Employs `CASE WHEN` logic blocks to classify products into popularity tiers (e.g., Best Seller, Popular) and segment users into loyalty statuses (Gold, Silver, Bronze).

---

## 🧹 Data Quality & Maintenance Rules

To guarantee platform data consistency, automated standardization scripts handle the following operational workflows:
* **Enforced Casing:** Transforms product records into standardized uppercase titles.
* **String Sanitization:** Trims unnecessary whitespaces across customer text fields.
* **Null Value Handling:** Fallbacks missing contact details to uniform standard strings.
