# Business Overview

## Project Overview

I built this Power BI project to analyze a Samsung supply chain from procurement and suppliers through production, inventory, shipments, customers, sales, and profitability.

The main idea of the project is to bring these areas into one report so I can look at the supply chain from both an operational and business perspective.

The report is organized into:

- Supply Chain Overview
- Supplier & Procurement
- Inventory & Manufacturing
- Shipment & Logistics
- Sales & Customer
- Sales Performance & Profitability

The dashboard was designed in Figma and implemented in Power BI using DAX measures and an analytical data model.

---

## Business Problem

Supply-chain performance is not controlled by one department. Supplier performance can affect procurement and production, production affects inventory, inventory and facility operations affect shipments, and the final result appears in customer and sales performance.

Because of this, I wanted the dashboard to answer questions such as:

- How much are we procuring and from which suppliers?
- How are suppliers performing in terms of lead time and quality?
- How much are we producing across facilities and products?
- What is the current inventory position compared with safety stock and reorder points?
- How many shipments are being processed and delivered?
- How is on-time delivery performing?
- What are the logistics costs?
- Which products, customers, countries, and channels contribute to sales and profit?
- How do discounts, costs, revenue, and profit relate to each other?

---

## Analytical Scope

### Supplier & Procurement

The procurement analysis looks at:

- Supplier
- Procurement quantity
- Procurement cost
- Lead time
- Quality
- Product
- Supplier tier
- Supplier location

This page helps me compare suppliers using more than one metric instead of looking only at procurement cost.

### Manufacturing

The manufacturing analysis focuses on:

- Production quantity
- Facility
- Product
- Production trends
- Manufacturing performance

### Inventory

The inventory analysis includes:

- Stock level
- Safety stock
- Reorder point
- Stock buffer
- Stock status
- Stock compared with safety stock

This gives a view of where inventory is positioned relative to the thresholds available in the model.

### Shipment & Logistics

The logistics analysis covers:

- Total shipments
- Delivered shipments
- On-time delivery
- Lead time
- Logistics cost
- Quantity shipped
- Shipment status
- Facility
- Carrier
- Delay reason

### Sales & Customers

The sales analysis covers:

- Revenue
- Profit
- Cost
- Quantity sold
- Orders
- Discounts
- Profit margin
- Customer
- Country
- Channel
- Product and category

---

## Data Model

I used a **Galaxy Schema / Constellation Schema** because the project contains several business processes that share common dimensions.

### Dimensions

```text
dim_customer
dim_supplier
dim_product
dim_date
dim_facility
```

### Fact tables

```text
fact_sales
fact_inventory
fact_production
fact_procurement
fact_shipment
```

The shared dimensions allow the same business entities to be used across different fact tables.

For example, `dim_product` can be used to analyze sales, inventory, production, procurement, and shipments.

The `dim_date` table provides a common time dimension for the model.

---

## Business Process

The business flow represented by the project can be viewed as:

```text
Supplier
   ↓
Procurement
   ↓
Production
   ↓
Inventory
   ↓
Shipment
   ↓
Customer
   ↓
Sales
   ↓
Profitability
```

This is the business flow of the analysis. It is separate from the physical relationships in the Power BI model.

---

## Dashboard Pages

### 01 — Intro

Project landing page and introduction.

### 02 — Supply Chain Overview

The main overview of supply-chain performance, including financial, operational, inventory, and logistics indicators.

### 03 — Supplier & Procurement

Analysis of procurement activity and supplier performance.

### 04 — Inventory & Manufacturing

Analysis of production and inventory position across facilities and products.

### 05 — Shipment & Logistics

Analysis of shipment activity, delivery performance, lead time, and logistics cost.

### 06 — Sales & Customer

Analysis of revenue, profit, cost, sales volume, customers, channels, and countries.

### 07 — Sales Performance & Profitability

More detailed analysis of sales, discounts, products, customers, and profitability.

---

## Tools Used

- **Power BI** — data modeling, DAX, visuals, filters, and dashboard development
- **DAX** — analytical measures and KPI calculations
- **Figma** — dashboard design and visual layout

---

## Project Goal

The goal of the project is not only to create charts. I wanted to build a dashboard where the data model, KPIs, and visuals work together.

The overall flow is:

```text
Data Model
    ↓
DAX Measures
    ↓
KPIs
    ↓
Interactive Dashboard
    ↓
Business Analysis
```

This approach makes the report easier to use for both high-level monitoring and detailed analysis.
