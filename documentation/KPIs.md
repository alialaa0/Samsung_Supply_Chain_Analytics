# KPIs

This file documents the main KPIs used in my Samsung Supply Chain Analytics dashboard.

The KPI values are dynamic in Power BI and change according to the selected filters, dimensions, and date context.

---

## Sales & Profitability

### Total Revenue

**Source:** `fact_sales`

Measures the total revenue represented in the sales data.

I use this KPI as the main measure of sales value and as the base for profitability analysis.

---

### Total Profit

**Source:** `fact_sales`

Measures the total profit represented in the sales data.

I use it together with revenue and cost to understand the financial result of sales activity.

---

### Profit Margin

**Source:** `fact_sales`

Measures profitability relative to revenue.

```text
Profit Margin = Profit / Revenue
```

The exact DAX implementation is maintained in the Power BI model.

This KPI is useful when comparing products, customers, categories, countries, or other segments where total profit alone may not be enough.

---

### Total Cost

**Source:** `fact_sales`

Measures the total sales cost represented in the model.

I use it with revenue and profit to understand the financial performance of sales.

---

### Total Quantity Sold

**Source:** `fact_sales`

Measures the quantity sold.

It provides the volume perspective alongside revenue and profit.

---

### Total Orders

**Source:** `fact_sales`

Measures the order activity represented in the sales data.

I use it with quantity and revenue to understand sales volume and order performance.

---

### Average Discount %

**Source:** `fact_sales`

Measures the average discount percentage used in the sales data.

I use this KPI to review discounting together with revenue, profit, and margin.

---

### Total Discount Amount

**Source:** `fact_sales`

Measures the total discount amount represented in sales transactions.

This gives the value perspective of discounting rather than only the percentage.

---

## Procurement

### Total Procurement Quantity

**Source:** `fact_procurement`

Measures the total quantity procured.

I use it to compare procurement activity across suppliers, products, and time.

---

### Total Procurement Cost

**Source:** `fact_procurement`

Measures the procurement cost represented in the model.

This is used to analyze purchasing expenditure across suppliers and products.

---

### Average Lead Time

**Source:** `fact_procurement`

Measures the average procurement lead time represented in the model.

I use this KPI mainly in the Supplier & Procurement analysis to compare supplier performance.

---

### Average Quality

**Source:** `fact_procurement`

Represents the average quality information available in the procurement data.

It is used together with procurement quantity, cost, and lead time when reviewing suppliers.

---

## Manufacturing

### Total Quantity Produced

**Source:** `fact_production`

Measures total production quantity.

I use it to compare production activity across facilities, products, and time.

---

### Defect Rate

**Source:** `fact_production`

Represents the defect rate available in the production data.

It provides a quality perspective alongside production quantity.

---

## Inventory

### Safety Stock

**Source:** `fact_inventory`

Represents the safety-stock level in the inventory data.

I use it as a reference point when reviewing current stock.

---

### Reorder Point

**Source:** `fact_inventory`

Represents the reorder point available in the inventory model.

It provides another inventory threshold for analysis.

---

### Stock Buffer

**Source:** `fact_inventory`

Measures the stock-buffer position used in the dashboard.

I use it to understand the difference between the current stock position and the relevant inventory reference level.

---

### Stock vs Safety %

**Source:** `fact_inventory`

Compares the stock position with safety stock.

This KPI helps identify inventory positions that are above or below the safety-stock reference.

---

### Stock Status

**Source:** `fact_inventory`

Provides the inventory status used in the dashboard.

I use this classification in the inventory analysis to make the stock position easier to review at facility level.

---

## Shipment & Logistics

### Total Shipments

**Source:** `fact_shipment`

Measures the total shipment records represented in the model.

---

### Delivered Shipments

**Source:** `fact_shipment`

Measures shipments classified as delivered in the shipment data.

---

### On-Time Delivery %

**Source:** `fact_shipment`

Measures the on-time delivery performance represented in the dashboard.

I use it as the main service-performance KPI in the Shipment & Logistics page.

---

### Total Logistics Cost

**Source:** `fact_shipment`

Measures the logistics cost represented in shipment transactions.

I use it to compare logistics expenditure across facilities and other available dimensions.

---

### Total Quantity Shipped

**Source:** `fact_shipment`

Measures the quantity represented by shipment transactions.

It provides the shipment-volume perspective alongside shipment count and logistics cost.

---

## KPI Usage

I do not use the KPIs independently.

For example:

```text
Revenue
   +
Cost
   +
Profit
   +
Profit Margin
```

gives a better view of sales performance than revenue alone.

For logistics:

```text
Shipments
   +
Delivered Shipments
   +
On-Time Delivery %
   +
Lead Time
   +
Logistics Cost
```

provides a broader view of delivery performance.

For inventory:

```text
Stock
   +
Safety Stock
   +
Reorder Point
   +
Stock Buffer
```

helps me review the inventory position using the thresholds available in the model.
