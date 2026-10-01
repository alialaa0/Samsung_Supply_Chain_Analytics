# 🔗 Data Model Relationships

## Overview

The Power BI model contains **18 relationships** connecting the five dimension tables with the five fact tables.

The relationships primarily follow:

- **One-to-many (1:*)** cardinality
- **Dimension → Fact** filtering direction
- **Single-direction** filter propagation

General pattern:

```text
Dimension
    1
    │
    ▼
Fact
    *
```

---

# 📊 Relationship Map

## 1. Inventory

### Date

```text
dim_date[date_key]
       1
       │
       ▼
fact_inventory[date_key]
       *
```

### Facility

```text
dim_facility[facility_id]
       1
       │
       ▼
fact_inventory[facility_id]
       *
```

### Product

```text
dim_product[product_id]
       1
       │
       ▼
fact_inventory[product_id]
       *
```

---

## 2. Procurement

### Delivery Date

```text
dim_date[date_key]
       1
       │
       ▼
fact_procurement[delivery_date_key]
       *
```

### Order Date

```text
dim_date[date_key]
       1
       │
       ▼
fact_procurement[order_date_key]
       *
```

### Product

```text
dim_product[product_id]
       1
       │
       ▼
fact_procurement[product_id]
       *
```

### Supplier

```text
dim_supplier[supplier_id]
       1
       │
       ▼
fact_procurement[supplier_id]
       *
```

---

## 3. Production

### Date

```text
dim_date[date_key]
       1
       │
       ▼
fact_production[date_key]
       *
```

### Facility

```text
dim_facility[facility_id]
       1
       │
       ▼
fact_production[facility_id]
       *
```

### Product

```text
dim_product[product_id]
       1
       │
       ▼
fact_production[product_id]
       *
```

---

## 4. Sales

### Customer

```text
dim_customer[customer_id]
       1
       │
       ▼
fact_sales[customer_id]
       *
```

### Date

```text
dim_date[date_key]
       1
       │
       ▼
fact_sales[date_key]
       *
```

### Product

```text
dim_product[product_id]
       1
       │
       ▼
fact_sales[product_id]
       *
```

---

## 5. Shipment

### Customer

```text
dim_customer[customer_id]
       1
       │
       ▼
fact_shipment[customer_id]
       *
```

### Delivery Date

```text
dim_date[date_key]
       1
       │
       ▼
fact_shipment[delivery_date_key]
       *
```

This relationship is **inactive** and is used when analysis needs to be based on the delivery date.

### Facility

```text
dim_facility[facility_id]
       1
       │
       ▼
fact_shipment[facility_id]
       *
```

### Product

```text
dim_product[product_id]
       1
       │
       ▼
fact_shipment[product_id]
       *
```

### Ship Date

```text
dim_date[date_key]
       1
       │
       ▼
fact_shipment[ship_date_key]
       *
```

---

# 📅 Date Relationships

The Date dimension plays an important role because several fact tables contain date keys.

Some fact tables contain multiple dates representing different business events.

For `fact_shipment`:

```text
                    dim_date
                       │
             ┌─────────┴─────────┐
             │                   │
          Active              Inactive
             │                   │
             ▼                   ▼
     ship_date_key       delivery_date_key
             │                   │
             └──── fact_shipment ┘
```

The active relationship allows normal filtering using the shipment date.

The inactive relationship can be activated inside a measure when analysis needs to be based on the delivery date.

Example:

```DAX
Delivered Shipments =
CALCULATE(
    [Total Shipments],
    USERELATIONSHIP(
        dim_date[date_key],
        fact_shipment[delivery_date_key]
    )
)
```

---

# 🧭 Relationship Summary

| # | Dimension | Fact | Key |
|---:|---|---|---|
| 1 | `dim_date` | `fact_inventory` | `date_key` |
| 2 | `dim_facility` | `fact_inventory` | `facility_id` |
| 3 | `dim_product` | `fact_inventory` | `product_id` |
| 4 | `dim_date` | `fact_procurement` | `delivery_date_key` |
| 5 | `dim_date` | `fact_procurement` | `order_date_key` |
| 6 | `dim_product` | `fact_procurement` | `product_id` |
| 7 | `dim_supplier` | `fact_procurement` | `supplier_id` |
| 8 | `dim_date` | `fact_production` | `date_key` |
| 9 | `dim_facility` | `fact_production` | `facility_id` |
| 10 | `dim_product` | `fact_production` | `product_id` |
| 11 | `dim_customer` | `fact_sales` | `customer_id` |
| 12 | `dim_date` | `fact_sales` | `date_key` |
| 13 | `dim_product` | `fact_sales` | `product_id` |
| 14 | `dim_customer` | `fact_shipment` | `customer_id` |
| 15 | `dim_date` | `fact_shipment` | `delivery_date_key` |
| 16 | `dim_facility` | `fact_shipment` | `facility_id` |
| 17 | `dim_product` | `fact_shipment` | `product_id` |
| 18 | `dim_date` | `fact_shipment` | `ship_date_key` |

---

# 🧠 Modeling Principles

The model follows these principles:

1. **Dimensions filter facts**
2. Fact tables are not directly connected to each other
3. Relationships use business keys appropriate to each process
4. One-to-many relationships are used between dimensions and facts
5. Single-direction filtering is used to reduce ambiguity
6. Multiple date roles are handled using active/inactive relationships
7. `USERELATIONSHIP()` is used when an inactive date relationship is required for a specific measure

---

## 📌 Relationship Count

**Total Relationships:** 18

**Dimensions:** 5

**Fact Tables:** 5

**Primary Relationship Pattern:**

```text
Dimension (1)
      ↓
Fact (*)
```
