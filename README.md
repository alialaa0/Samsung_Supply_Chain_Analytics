# Samsung Supply Chain Analytics

A Power BI dashboard for analyzing Samsung's supply chain across **procurement, suppliers, manufacturing, inventory, logistics, sales, customers, and profitability**.

The project combines **Power BI, DAX, and Figma** to build an interactive analytical report from a multi-fact data model.

---

## Dashboard Preview

### 01 — Intro

![Intro](dashboard/screenshots/01_Intro.png)

### 02 — Supply Chain Overview

![Overview](dashboard/screenshots/02_Overview.png)

### 03 — Overview Filters

![Overview Filters](dashboard/screenshots/08_Overview_Filters.png)

### 04 — Supplier & Procurement

![Supplier & Procurement](dashboard/screenshots/03_Supplier_Procurement.png)

### 05 — Inventory & Manufacturing

![Inventory & Manufacturing](dashboard/screenshots/04_Inventory_Manufacturing.png)

### 06 — Shipment & Logistics

![Shipment & Logistics](dashboard/screenshots/05_Shipment_Logistics.png)

### 07 — Sales & Customer Insights

![Sales & Customer Insights](dashboard/screenshots/06_Sales_Customer_Insights.png)

### 08 — Sales Performance

![Sales Performance](dashboard/screenshots/07_Sales_Performance.png)

---

## Project Overview

The dashboard follows the main supply-chain flow:

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

The goal is to provide one place to monitor operational and financial performance and then drill into the areas behind the results.

---

## What I Analyzed

### Supplier & Procurement

* Procurement quantity
* Procurement cost
* Supplier lead time
* Supplier quality
* Supplier performance

### Inventory & Manufacturing

* Production quantity
* Stock level
* Safety stock
* Reorder point
* Stock buffer
* Production by facility and product

### Shipment & Logistics

* Total shipments
* Delivered shipments
* On-time delivery
* Lead time
* Logistics cost
* Shipment status
* Facility and carrier performance

### Sales & Customers

* Revenue
* Profit
* Cost
* Profit margin
* Quantity sold
* Orders
* Discounts
* Customer, country, channel, and product performance

---

## Data Model

The Power BI model uses a **Galaxy Schema / Constellation Schema** with shared dimensions and multiple fact tables.

### Dimensions

```text
dim_customer
dim_supplier
dim_product
dim_date
dim_facility
```

### Facts

```text
fact_sales
fact_inventory
fact_production
fact_procurement
fact_shipment
```

The shared dimensions allow the different business processes to be analyzed consistently.

---

## DAX & KPIs

The report uses reusable DAX measures for the main business KPIs, including:

```text
Total Revenue
Total Profit
Profit Margin
Total Cost
Total Quantity Sold
Total Orders
Procurement Quantity
Procurement Cost
Average Lead Time
Production Quantity
Current Stock
Safety Stock
Stock Buffer
Stock vs Safety %
Total Shipments
Delivered Shipments
On-Time Delivery %
Logistics Cost
Quantity Shipped
```

DAX documentation is available in:

[`PowerBI/DAX/Measures.md`](PowerBI/DAX/Measures.md)

---

## Tools

| Tool         | Purpose                                   |
| ------------ | ----------------------------------------- |
| **Power BI** | Data modeling, DAX, dashboard development |
| **DAX**      | KPI and analytical calculations           |
| **Figma**    | Dashboard design and visual layout        |

---

## Repository Structure

```text
Samsung_Supply_Chain_Analytics/
│
├── dashboard/
│   └── screenshots/
│       ├── 01_Intro.png
│       ├── 02_Overview.png
│       ├── 03_Supplier_Procurement.png
│       ├── 04_Inventory_Manufacturing.png
│       ├── 05_Shipment_Logistics.png
│       ├── 06_Sales_Customer_Insights.png
│       ├── 07_Sales_Performance.png
│       └── 08_Overview_Filters.png
│
├── PowerBI/
│   └── DAX/
│       └── Measures.md
│
├── Data_Model/
│   ├── Data_Model.md
│   └── Relationships.md
│
└── Documentation/
    ├── Business_Overview.md
    ├── KPIs.md
    └── Insights.md
```

---

## Documentation

* [Business Overview](Documentation/Business_Overview.md)
* [KPIs](Documentation/KPIs.md)
* [Insights](Documentation/Insights.md)
* [Data Model](Data_Model/Data_Model.md)
* [Relationships](Data_Model/Relationships.md)
* [DAX Measures](PowerBI/DAX/Measures.md)

---

## Project Focus

This project focuses on turning supply-chain data into a **clear, interactive business analysis** by combining data modeling, DAX measures, KPI design, and dashboard storytelling.

**Built with Power BI • DAX • Figma**
