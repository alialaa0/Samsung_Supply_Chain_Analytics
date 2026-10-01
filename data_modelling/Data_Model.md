# Data Model

## Overview

The project uses a **Galaxy Schema / Constellation Schema** because the model contains multiple fact tables that share common dimensions.

The model is designed to analyze different supply-chain processes while keeping the dimensions reusable across the report.

```text
                    dim_customer
                         │
                    ┌────┴────┐
                    │         │
dim_supplier ───────┤         │
                    │         │
dim_product ────────┤  FACTS  │
                    │         │
dim_date ───────────┤         │
                    │         │
dim_facility ───────┘         │
                              │
             ┌────────────────┼────────────────┐
             │        │       │       │        │
             ▼        ▼       ▼       ▼        ▼
          Sales   Inventory Production Procurement Shipment
```

---

## Dimension Tables

### `dim_customer`

Contains customer information used for customer and sales analysis.

Main attributes include:

```text
customer_id
customer_name
country
channel_type
customer_size
annual_volume
```

---

### `dim_supplier`

Contains supplier information used for procurement analysis.

Main attributes include:

```text
supplier_id
supplier_name
country
city
tier
specialty
average_quality_score
```

---

### `dim_product`

Contains product information shared across the different business processes.

Main attributes include:

```text
product_id
product_name
category
product_line
color
specification
unit_cost
unit_price
weight
```

---

### `dim_date`

The common calendar dimension used for time-based analysis.

Main attributes include:

```text
date_key
date
day
day_name
day_of_week
month
month_name
quarter
year
weekend_indicator
```

---

### `dim_facility`

Contains facility information used across manufacturing, inventory, and shipment analysis.

Main attributes include:

```text
facility_id
facility_name
facility_type
country
city
specialization
annual_capacity
```

---

# Fact Tables

## `fact_sales`

Contains sales transaction data.

Main fields include:

```text
sales_id
order_number
customer_id
product_id
date_key
quantity_sold
unit_price
gross_revenue
discount
total_cost
profit
profit_margin
```

Used for:

* Revenue
* Profit
* Cost
* Quantity sold
* Orders
* Discounts
* Profitability analysis

---

## `fact_inventory`

Contains inventory positions by facility and product.

Main fields include:

```text
inventory_id
date_key
facility_id
product_id
stock_level
safety_stock_level
reorder_point
```

Used for:

* Current stock
* Safety stock
* Reorder point
* Stock buffer
* Inventory status

---

## `fact_production`

Contains production information.

Main fields include:

```text
production_id
batch_number
date_key
facility_id
product_id
quantity_produced
defective_units
defect_rate
```

Used for:

* Production volume
* Facility production
* Product production
* Defect analysis

---

## `fact_procurement`

Contains procurement transactions.

Main fields include:

```text
procurement_id
purchase_order_number
supplier_id
product_id
order_date_key
delivery_date_key
order_quantity
unit_cost
total_cost
lead_time_days
quality_score
```

Used for:

* Procurement quantity
* Procurement cost
* Supplier analysis
* Lead-time analysis
* Quality analysis

---

## `fact_shipment`

Contains shipment and delivery information.

Main fields include:

```text
shipment_id
customer_id
product_id
facility_id
ship_date_key
delivery_date_key
quantity
shipping_cost
status
carrier
delay_reason
tracking_number
```

Used for:

* Shipment volume
* Delivered shipments
* On-time delivery
* Logistics cost
* Lead-time analysis
* Shipment status

---

# Model Design

The main design principle is to keep the fact tables focused on their individual business processes while using shared dimensions for analysis.

```text
             Shared Dimensions
                    │
        ┌───────────┼───────────┐
        │           │           │
        ▼           ▼           ▼
      Sales     Inventory    Production
        │           │           │
        └───────────┼───────────┘
                    │
              Procurement
                    │
                 Shipment
```

The facts are not modeled as a chain of fact-to-fact relationships.

Instead, shared dimensions provide the common analytical context.

---

# Grain

The grain of each fact table is defined by its business transaction or recorded operational event.

| Fact               | Analytical grain                                  |
| ------------------ | ------------------------------------------------- |
| `fact_sales`       | Sales transaction                                 |
| `fact_inventory`   | Inventory position by date, facility, and product |
| `fact_production`  | Production batch/event                            |
| `fact_procurement` | Procurement transaction                           |
| `fact_shipment`    | Shipment transaction                              |

Understanding the grain is important when creating measures because aggregations should match the level of detail stored in each fact.

---

# Date Analysis

`dim_date` is used as the common calendar dimension.

Some processes contain more than one date, such as shipment date and delivery date or procurement order date and delivery date.

This allows the report to analyze the same business process from different date perspectives.

For an inactive date relationship, DAX can activate the required relationship using:

```DAX
CALCULATE(
    [Measure],
    USERELATIONSHIP(
        dim_date[date_key],
        fact_table[secondary_date_key]
    )
)
```

---

# Summary

The model provides a common analytical structure for:

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

The business flow above describes the analytical story of the project, while the Power BI model uses shared dimensions to connect the different fact processes.
