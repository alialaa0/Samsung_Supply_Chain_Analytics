# Relationships

## Overview

The Power BI model uses dimension-to-fact relationships to connect the different supply-chain processes.

The main relationship pattern is:

```text
Dimension
    1
    │
    │
    ▼
Fact
    *
```

The dimensions provide the filtering context while the fact tables contain the business-process data.

---

# Relationship Structure

## Customer Relationships

`dim_customer` is used to analyze customer-related activity.

```text
dim_customer
     1
     │
     ├──────────► fact_sales
     │
     └──────────► fact_shipment
```

This allows sales and shipment activity to be analyzed by customer.

---

## Supplier Relationships

`dim_supplier` connects supplier information to procurement activity.

```text
dim_supplier
     1
     │
     └──────────► fact_procurement
```

This allows procurement quantity, cost, lead time, and quality to be analyzed by supplier.

---

## Product Relationships

`dim_product` is a shared dimension across the main supply-chain processes.

```text
dim_product
     1
     │
     ├──────────► fact_sales
     ├──────────► fact_inventory
     ├──────────► fact_production
     ├──────────► fact_procurement
     └──────────► fact_shipment
```

This is important because the same product can be analyzed across procurement, production, inventory, shipment, and sales.

---

## Facility Relationships

`dim_facility` is used across operational processes.

```text
dim_facility
     1
     │
     ├──────────► fact_inventory
     ├──────────► fact_production
     └──────────► fact_shipment
```

This allows facility-level analysis across inventory, manufacturing, and logistics.

---

## Date Relationships

`dim_date` is the common date dimension.

```text
dim_date
    1
    │
    ├──────────► fact_sales
    ├──────────► fact_inventory
    ├──────────► fact_production
    ├──────────► fact_procurement
    └──────────► fact_shipment
```

The date dimension provides consistent filtering for time-based analysis.

---

# Multiple Date Roles

Some fact tables contain more than one date key.

For example, shipment data contains:

```text
ship_date_key
delivery_date_key
```

The two dates represent different business events.

Conceptually:

```text
dim_date[date_key]
       │
       ├── Ship Date
       │
       └── Delivery Date
```

The active relationship is used for the normal date analysis, while another date relationship can be activated when the analysis requires it.

Example:

```DAX
Delivered Analysis =
CALCULATE(
    [Total Measure],
    USERELATIONSHIP(
        dim_date[date_key],
        fact_shipment[delivery_date_key]
    )
)
```

The same approach can be used for other fact tables that contain multiple date roles.

---

# Filtering Direction

The model follows the standard dimensional-model pattern:

```text
Dimension
    ↓
Fact
```

The dimension provides the filter context for the related fact table.

For example:

```text
dim_product[category]
        ↓
fact_sales
```

Selecting a product category therefore filters the related sales records.

The same principle applies to supplier, customer, facility, and date analysis.

---

# Fact-to-Fact Relationships

The model does not require direct relationships between the fact tables.

For example:

```text
fact_sales  X  fact_inventory
fact_sales  X  fact_shipment
fact_sales  X  fact_procurement
```

Instead, shared dimensions provide the analytical connection.

Example:

```text
                 dim_product
                /     |      \
               /      |       \
              ▼       ▼        ▼
        fact_sales  fact_inventory  fact_production
```

This keeps the model easier to filter and reduces unnecessary many-to-many relationship problems.

---

# Relationship Design

The relationship design follows these principles:

1. Dimensions provide the analytical context.
2. Fact tables store business-process events or measurements.
3. Shared dimensions are reused across processes.
4. Fact tables are not directly chained together.
5. Date roles are handled through the date dimension.
6. Different date roles can be used through inactive relationships and `USERELATIONSHIP()` when required.

---

# Analytical Impact

The relationships allow the dashboard to move from a high-level KPI into the dimensions behind the result.

For example:

```text
Total Revenue
      ↓
Product
      ↓
Category
      ↓
Customer
      ↓
Country
      ↓
Channel
```

Similarly:

```text
Total Procurement Cost
      ↓
Supplier
      ↓
Product
      ↓
Country
```

And:

```text
Total Shipments
      ↓
Facility
      ↓
Product
      ↓
Customer
      ↓
Shipment Status
```

This relationship structure is what allows the report to work as an interactive analytical model rather than a collection of independent charts.

---

# Summary

The model is based on a shared-dimension approach:

```text
                    dim_customer
                         │
dim_supplier ───────┐    │
                    │    │
dim_product ────────┤    │
                    │    │
dim_date ───────────┤    │
                    │    │
dim_facility ───────┘    │
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
      Procurement    Production      Inventory
          │              │              │
          └──────────────┼──────────────┘
                         │
                      Shipment
                         │
                        Sales
```

The result is a reusable Power BI model where procurement, production, inventory, shipment, customer, and sales analysis can be performed through common dimensions.
