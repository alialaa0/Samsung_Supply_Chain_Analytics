# 📊 Data Model

## Overview

The Power BI semantic model follows a **Galaxy Schema (Constellation Schema)**.

The model contains multiple fact tables that share common dimension tables. This structure supports analysis across different supply chain business processes while maintaining consistent dimensions.

---

## 🧩 Dimension Tables

### `dim_customer`

Contains customer-related information:

- Customer ID
- Customer Name
- Country
- Channel Type
- Customer Size
- Annual Volume

### `dim_supplier`

Contains supplier-related information:

- Supplier ID
- Supplier Name
- Country
- City
- Tier
- Specialty
- Average Quality Score

### `dim_product`

Contains product-related information:

- Product ID
- Product Name
- Category
- Product Line
- Color
- Specification
- Unit Cost
- Unit Price
- Weight

### `dim_date`

Provides the calendar structure used for time-based analysis.

Includes:

- Date
- Date Key
- Day
- Day Name
- Day of Week
- Month
- Month Name
- Quarter
- Year
- Weekend Indicator

### `dim_facility`

Contains facility-related information:

- Facility ID
- Facility Name
- Facility Type
- Country
- City
- Specialization
- Annual Capacity

---

## 📦 Fact Tables

### `fact_sales`

Stores sales transactions:

- Sales ID
- Order Number
- Customer ID
- Product ID
- Date Key
- Quantity Sold
- Unit Price
- Gross Revenue
- Discount
- Total Cost
- Profit
- Profit Margin

### `fact_inventory`

Stores inventory information:

- Inventory ID
- Date Key
- Facility ID
- Product ID
- Stock Level
- Safety Stock Level
- Reorder Point

### `fact_production`

Stores production records:

- Production ID
- Batch Number
- Date Key
- Facility ID
- Product ID
- Quantity Produced
- Defective Units
- Defect Rate

### `fact_procurement`

Stores procurement transactions:

- Procurement ID
- Purchase Order Number
- Supplier ID
- Product ID
- Order Date Key
- Delivery Date Key
- Order Quantity
- Unit Cost
- Total Cost
- Lead Time Days
- Quality Score

### `fact_shipment`

Stores shipment and logistics information:

- Shipment ID
- Customer ID
- Product ID
- Facility ID
- Ship Date Key
- Delivery Date Key
- Quantity
- Shipping Cost
- Status
- Carrier
- Delay Reason
- Tracking Number

---

## 🏗️ Schema Structure

The model follows a **Galaxy / Constellation Schema**, where multiple fact tables share common dimensions.

```text
                         ┌──────────────┐
                         │   dim_date   │
                         └──────┬───────┘
                                │
       ┌────────────────────────┼────────────────────────┐
       │                        │                        │
┌──────▼───────┐         ┌──────▼───────┐         ┌──────▼───────┐
│ dim_customer │         │ dim_product  │         │ dim_supplier │
└──────┬───────┘         └──────┬───────┘         └──────┬───────┘
       │                        │                        │
       └────────────────────────┼────────────────────────┘
                                │
                     ┌──────────▼──────────┐
                     │    Fact Tables     │
                     └──────────┬──────────┘
                                │
          ┌─────────────────────┼─────────────────────┐
          │          │          │          │          │
          ▼          ▼          ▼          ▼          ▼
       Sales     Inventory  Production Procurement Shipment
          │          │          │          │          │
          └──────────┴──────────┼──────────┴──────────┘
                                │
                       ┌────────▼────────┐
                       │  dim_facility   │
                       └─────────────────┘
```

---

## 🔗 Relationship Design

The model primarily uses:

- **One-to-many (1:*) relationships**
- Dimension-to-fact relationships
- **Single-direction filtering**

General relationship pattern:

```text
Dimension
    1
    │
    ▼
Fact
    *
```

Example:

```text
dim_product[product_id]
          1
          │
          ▼
fact_sales[product_id]
          *
```

This allows product attributes to filter the related sales records.

---

## 📅 Multiple Date Roles

Some fact tables contain multiple date keys because different dates represent different business events.

For example, `fact_shipment` contains:

```text
ship_date_key
delivery_date_key
```

The model connects both fields to the Date dimension:

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

The inactive relationship can be activated inside a DAX measure using `USERELATIONSHIP()`.

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

This allows the same Date dimension to support different business date perspectives.

---

## 🎯 Why This Model?

The Galaxy Schema allows multiple supply chain processes to be analyzed using shared dimensions.

The main analytical areas are:

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
Customer / Sales
```

Shared dimensions such as **Date, Product, Facility, Customer, and Supplier** allow users to filter and analyze different business processes consistently across the Power BI report.

---

## 📌 Model Summary

| Type | Table |
|---|---|
| Dimension | `dim_customer` |
| Dimension | `dim_supplier` |
| Dimension | `dim_product` |
| Dimension | `dim_date` |
| Dimension | `dim_facility` |
| Fact | `fact_sales` |
| Fact | `fact_inventory` |
| Fact | `fact_production` |
| Fact | `fact_procurement` |
| Fact | `fact_shipment` |

**Dimensions:** 5  
**Fact Tables:** 5  
**Relationships:** 18
