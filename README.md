# Samsung Supply Chain Analytics

An end-to-end business intelligence project for analyzing Samsung's supply chain across **procurement, suppliers, manufacturing, inventory, logistics, sales, customers, and profitability**.

The project combines **data modeling, DAX, dashboard design, and business analysis** to build an interactive analytical solution from a multi-fact data model.

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

The objective is to provide a single view of operational and financial performance while allowing deeper analysis by supplier, facility, product, customer, country, and channel.

---

## Analysis Areas

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
* Facility and carrier analysis

### Sales & Customers

* Revenue
* Profit
* Cost
* Profit margin
* Quantity sold
* Orders
* Discounts
* Customer, country, channel, and product analysis

---

## Data Model

The analytical model uses a **Galaxy Schema / Constellation Schema** with shared dimensions and multiple fact tables.

### Dimensions

```text
dim_customer
dim_supplier
dim_product
dim_date
dim_facility
```

### Fact Tables

```text
fact_sales
fact_inventory
fact_production
fact_procurement
fact_shipment
```

Shared dimensions allow the different business processes to be analyzed consistently across the project.

---

## DAX & KPIs

The project uses reusable DAX measures for the main business KPIs:

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
Reorder Point
Stock Buffer
Stock vs Safety %

Total Shipments
Delivered Shipments
On-Time Delivery %
Logistics Cost
Quantity Shipped
```

Detailed documentation:

[`PowerBI/DAX/Measures.md`](PowerBI/DAX/Measures.md)

---

## Tools

| Tool            | Purpose                                       |
| --------------- | --------------------------------------------- |
| 📊 **Power BI** | Data modeling, DAX, and dashboard development |
| 🧮 **DAX**      | KPI and analytical calculations               |
| 🎨 **Figma**    | Dashboard design and visual layout            |

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

| Document                                                | Description                        |
| ------------------------------------------------------- | ---------------------------------- |
| [Business Overview](Documentation/Business_Overview.md) | Project scope and business context |
| [KPIs](Documentation/KPIs.md)                           | KPI definitions and usage          |
| [Insights](Documentation/Insights.md)                   | Dashboard analysis                 |
| [Data Model](Data_Model/Data_Model.md)                  | Model structure                    |
| [Relationships](Data_Model/Relationships.md)            | Table relationships                |
| [DAX Measures](PowerBI/DAX/Measures.md)                 | Main DAX measures                  |

---

## Project Focus

The project focuses on combining:

**Data Modeling → DAX → KPI Design → Visualization → Business Analysis**

The goal is to turn supply-chain data into a clear and interactive analytical solution that supports both high-level monitoring and detailed analysis.
