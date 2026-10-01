# DAX Measures

## 1. Source and Verification Standard

This document is based on the uploaded Power BI file:

```text
Supply Cahin Analysis.pbix
```

The PBIX report metadata was inspected directly from the `.pbix` package.

### What is verified

The report layer contains references to the following measures. These are **actual measure names used by the report visuals**, including their model/table qualification.

### What is intentionally not guessed

The readable `Report/Layout` section exposes measure references, but the measure expression definitions are stored in the compressed `DataModel` stream.

The `DataModel` in this PBIX is stored using **XPress9 compression**. Therefore, the exact DAX expression text cannot be responsibly reproduced from the accessible report metadata alone.

> **No DAX formula below has been inferred from the measure name.**
>
> This is intentional. A measure called `total_revenue` does not prove whether the underlying expression is `SUM(...)`, `CALCULATE(SUM(...))`, `SUMX(...)`, or something else.

For that reason, this document separates **verified measure metadata** from **DAX source that still requires model-level extraction**.

---

# 2. Verified Measure Inventory

The following measures were found as measure references in the PBIX report layer.

| # | Measure | Table | Verified from PBIX |
|---:|---|---|---|
| 1 | `total_revenue` | `fact_sales` | Yes |
| 2 | `total_profit` | `fact_sales` | Yes |
| 3 | `profit_margin` | `fact_sales` | Yes |
| 4 | `avg_discount_pct` | `fact_sales` | Yes |
| 5 | `total_shipments` | `fact_shipment` | Yes |
| 6 | `delivered_shipments` | `fact_shipment` | Yes |
| 7 | `on_time_delivery_pct` | `fact_shipment` | Yes |
| 8 | `avg_lead_time` | `fact_procurement` | Yes |
| 9 | `total_logistic_cost` | `fact_shipment` | Yes |
| 10 | `total_quantity_shipped` | `fact_shipment` | Yes |
| 11 | `total_quantity_procuremnt` | `fact_procurement` | Yes |
| 12 | `total_quantity_produce` | `fact_production` | Yes |
| 13 | `Safety Stock` | `fact_inventory` | Yes |
| 14 | `Stock Buffer` | `fact_inventory` | Yes |
| 15 | `Stock Status` | `fact_inventory` | Yes |
| 16 | `Stock vs Safety %` | `fact_inventory` | Yes |

These are the measure references actually consumed by the report visuals.

---

# 3. Sales Measures

## 3.1 `fact_sales[total_revenue]`

**Status:** Verified measure reference.

**Used by:** Sales / executive report visuals.

**Purpose indicated by report usage:** Revenue analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

The measure name alone is insufficient evidence to determine the exact DAX implementation.

---

## 3.2 `fact_sales[total_profit]`

**Status:** Verified measure reference.

**Used by:** Sales and profitability visuals.

**Purpose indicated by report usage:** Profit analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

---

## 3.3 `fact_sales[profit_margin]`

**Status:** Verified measure reference.

**Used by:** KPI cards and profitability analysis.

**Purpose indicated by report usage:** Profit-margin analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

> Do not replace this with a guessed `DIVIDE([total_profit], [total_revenue])` expression unless the actual model definition is inspected.

---

## 3.4 `fact_sales[avg_discount_pct]`

**Status:** Verified measure reference.

**Used by:** Sales & Customer 2 report page.

**Purpose indicated by report usage:** Average discount percentage analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

---

# 4. Procurement Measures

## 4.1 `fact_procurement[avg_lead_time]`

**Status:** Verified measure reference.

**Used by:** Supplier & Procurement analysis.

**Purpose indicated by report usage:** Procurement lead-time analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

---

## 4.2 `fact_procurement[total_quantity_procuremnt]`

**Status:** Verified measure reference.

**Note:** The spelling `procuremnt` is preserved exactly as it appears in the PBIX model reference.

**Used by:** Supplier & Procurement visuals.

**Purpose indicated by report usage:** Procurement quantity analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

> The repository documentation should preserve the actual model name rather than silently renaming the measure.

---

# 5. Production Measures

## 5.1 `fact_production[total_quantity_produce]`

**Status:** Verified measure reference.

**Used by:** Inventory & Manufacturer analysis.

**Purpose indicated by report usage:** Production-volume analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

---

# 6. Inventory Measures

## 6.1 `fact_inventory[Safety Stock]`

**Status:** Verified measure reference.

**Used by:** Inventory visuals and facility-level tables.

**Purpose indicated by report usage:** Safety-stock analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

---

## 6.2 `fact_inventory[Stock Buffer]`

**Status:** Verified measure reference.

**Used by:** Inventory visual tooltips and facility-level analysis.

**Purpose indicated by report usage:** Stock-buffer analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

> Do not assume the expression is `Stock Level - Safety Stock` without inspecting the actual measure definition.

---

## 6.3 `fact_inventory[Stock Status]`

**Status:** Verified measure reference.

**Used by:** Facility-level inventory table.

**Purpose indicated by report usage:** Inventory-status classification.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

> The classification thresholds cannot be safely inferred from the measure name.

---

## 6.4 `fact_inventory[Stock vs Safety %]`

**Status:** Verified measure reference.

**Used by:** Inventory visual tooltips and facility-level analysis.

**Purpose indicated by report usage:** Comparison between stock and safety-stock positions.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

> Do not assume a specific numerator, denominator, or handling of zero/blank safety stock without extracting the actual DAX.

---

# 7. Shipment & Logistics Measures

## 7.1 `fact_shipment[total_shipments]`

**Status:** Verified measure reference.

**Used by:** Shipment & Logistics KPI visuals.

**Purpose indicated by report usage:** Total shipment activity.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

---

## 7.2 `fact_shipment[delivered_shipments]`

**Status:** Verified measure reference.

**Used by:** Shipment & Logistics KPI and analysis visuals.

**Purpose indicated by report usage:** Delivered-shipment analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

---

## 7.3 `fact_shipment[on_time_delivery_pct]`

**Status:** Verified measure reference.

**Used by:** Shipment & Logistics KPI visuals.

**Purpose indicated by report usage:** On-time delivery performance.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

> The exact definition of "on time" must come from the DAX expression. It should not be reconstructed from the measure name.

---

## 7.4 `fact_shipment[total_logistic_cost]`

**Status:** Verified measure reference.

**Used by:** Shipment & Logistics analysis.

**Purpose indicated by report usage:** Logistics-cost analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

---

## 7.5 `fact_shipment[total_quantity_shipped]`

**Status:** Verified measure reference.

**Used by:** Shipment & Logistics analysis.

**Purpose indicated by report usage:** Shipped-quantity analysis.

**Exact DAX:**

```text
Not extracted from the accessible report metadata.
```

---

# 8. Measures vs Raw Column Aggregations

An important distinction was found in the PBIX report metadata.

Several visuals use **direct column aggregations** rather than custom measures.

Examples include:

```text
Sum(fact_inventory.stock_level)
Sum(fact_inventory.safety_stock_level)
Sum(fact_inventory.reorder_point)
Sum(fact_sales.discount_amount)
Sum(fact_sales.total_cost)
Sum(fact_sales.quantity_sold)
Sum(fact_sales.unit_price)
Sum(fact_procurement.total_cost)
```

There are also direct column references such as:

```text
dim_customer.channel_type
dim_customer.country
dim_customer.customer_name
dim_facility.facility_name
dim_product.category
dim_product.product_name
dim_supplier.supplier_name
dim_supplier.tier
```

These should **not** be documented as DAX measures merely because Power BI aggregates them inside a visual.

---

# 9. Verified Report-Level Evidence

The PBIX report metadata shows these measures being used in report visuals.

### Sales

```text
fact_sales.total_revenue
fact_sales.total_profit
fact_sales.profit_margin
fact_sales.avg_discount_pct
```

### Procurement

```text
fact_procurement.avg_lead_time
fact_procurement.total_quantity_procuremnt
```

### Production

```text
fact_production.total_quantity_produce
```

### Inventory

```text
fact_inventory.Safety Stock
fact_inventory.Stock Buffer
fact_inventory.Stock Status
fact_inventory.Stock vs Safety %
```

### Shipment

```text
fact_shipment.total_shipments
fact_shipment.delivered_shipments
fact_shipment.on_time_delivery_pct
fact_shipment.total_logistic_cost
fact_shipment.total_quantity_shipped
```

---

# 10. Why Exact DAX Is Not Included Yet

The PBIX is a ZIP-based container, but its semantic model is stored in the `DataModel` file.

The model begins with the following XPress9 compression marker:

```text
This backup was created using XPress9 compression.
```

The report's `Report/Layout` is readable and provides the measure references used by visuals.

However, the actual DAX expression definitions reside in the compressed semantic-model metadata.

Therefore:

```text
Report/Layout
    ↓
Measure names / references
    ✓ Extracted

DataModel
    ↓
Actual measure expressions
    ⚠ Requires model-level XPress9 decoding
```

This is why the exact formulas are deliberately not reconstructed here.

---

# 11. Required Next Step for Complete DAX Documentation

To produce a definitive version containing:

```DAX
total_revenue =
    <actual expression>

total_profit =
    <actual expression>

profit_margin =
    <actual expression>
```

the model itself must be exported/read in a format that exposes the semantic-model metadata.

Recommended options:

### Option A — Power BI Project format

Save/export the report as a **PBIP** project.

This is the preferred repository-friendly approach because model metadata can be version-controlled as text.

### Option B — Tabular Editor / DAX Studio

Connect to the model and export the measures with their expressions.

### Option C — PBIT / DataModelSchema

Export a template/model schema that exposes the semantic model metadata.

Once the model-level metadata is available, this document can be upgraded to contain the **exact DAX source for every measure**.

---

# 12. Repository Quality Rule

Do not commit guessed DAX.

A professional analytics repository should follow:

```text
Actual DAX
    ↓
Document exact expression
    ↓
Explain business purpose
    ↓
Explain filter context
    ↓
Explain edge cases
```

and never:

```text
Measure name
    ↓
Guess formula
    ↓
Present guess as implementation
```

The current file therefore represents the **verified measure inventory** from the PBIX without introducing unsupported DAX.
