# KPI Catalog

## 1. KPI Governance

This document defines the principal KPIs used by the Samsung Supply Chain Analytics report.

Each KPI should be interpreted in the context of:

- Its fact-table grain
- Active report filters
- Selected date context
- Product, supplier, facility, customer, and geography dimensions
- Whether the metric is a volume, cost, service, or profitability measure

> **Important:** KPI values are intentionally not hard-coded in this documentation. Values displayed in Power BI are dynamic and depend on the current filter context.

---

# 2. Executive KPIs

## Total Revenue

**Business definition:** Total revenue generated from sales transactions within the current filter context.

**Primary source:** `fact_sales`

**Analytical use:** Measures commercial scale and provides the denominator for profitability ratios.

---

## Total Profit

**Business definition:** Total profit generated from sales transactions within the current filter context.

**Primary source:** `fact_sales`

**Analytical use:** Evaluates economic contribution after the modeled sales costs.

---

## Profit Margin

**Business definition:** Profit expressed relative to revenue.

**Conceptual formula:**

```text
Profit Margin % = Total Profit / Total Revenue
```

**Analytical use:** Allows profitability to be compared across products, customers, categories, countries, and periods without relying only on absolute profit.

**Interpretation caution:** A high margin does not necessarily mean high total profit; volume and revenue scale still matter.

---

## Total Cost

**Business definition:** Total modeled sales cost within the current filter context.

**Primary source:** `fact_sales`

**Analytical use:** Provides cost context for revenue and profit analysis.

---

# 3. Sales & Customer KPIs

## Total Quantity Sold

**Business definition:** Total quantity recorded as sold.

**Primary source:** `fact_sales`

**Analytical use:** Measures sales volume and supports volume-versus-value analysis.

---

## Total Orders

**Business definition:** Number of sales orders represented in the report's sales data.

**Primary source:** `fact_sales`

**Analytical use:** Provides order-volume context alongside revenue and quantity.

---

## Average Discount %

**Business definition:** Average discount percentage represented in the sales transactions under the current filter context.

**Analytical use:** Helps evaluate discounting behavior alongside revenue and profitability.

**Interpretation caution:** An average discount percentage should not automatically be interpreted as the weighted commercial discount unless the underlying measure explicitly uses a revenue/quantity-weighted calculation.

---

## Total Discount Amount

**Business definition:** Total modeled discount amount applied to sales.

**Analytical use:** Quantifies the commercial value of discounts and should be interpreted alongside revenue, volume, and margin.

---

# 4. Procurement KPIs

## Total Procurement Quantity

**Business definition:** Total quantity procured within the current filter context.

**Primary source:** `fact_procurement`

**Analytical use:** Measures purchasing volume across suppliers, products, and time.

---

## Total Procurement Cost

**Business definition:** Total procurement cost represented by procurement transactions.

**Primary source:** `fact_procurement`

**Analytical use:** Quantifies purchasing expenditure and supports supplier/product cost analysis.

---

## Average Lead Time

**Business definition:** Average lead time represented in the relevant process under the current filter context.

**Primary source:** Procurement and shipment analysis depending on the visual/measure.

**Analytical use:** Measures time performance and supports supplier or logistics diagnosis.

**Interpretation caution:** Procurement lead time and shipment/delivery lead time are different business concepts. They should not be combined unless the metric explicitly defines them as such.

---

## Average Quality

**Business definition:** Average supplier/product quality score represented in procurement data.

**Primary source:** `fact_procurement` and supplier attributes.

**Analytical use:** Supports supplier-quality comparison.

---

# 5. Production KPIs

## Total Quantity Produced

**Business definition:** Total production quantity recorded in the manufacturing fact table.

**Primary source:** `fact_production`

**Analytical use:** Measures manufacturing output by facility, product, and time.

---

## Defect Rate

**Business definition:** Proportion of defective production units relative to total production.

**Primary source:** `fact_production`

**Analytical use:** Provides a quality-performance perspective for manufacturing.

**Interpretation caution:** A defect rate should be considered together with production volume. A low rate on very small production volume may not represent the same operational significance as a similar rate at high volume.

---

# 6. Inventory KPIs

## Current Stock

**Business definition:** Stock level represented in the inventory data under the current filter context.

**Primary source:** `fact_inventory`

**Analytical use:** Measures inventory position.

---

## Safety Stock

**Business definition:** Target buffer stock level represented by the inventory model.

**Primary source:** `fact_inventory`

**Analytical use:** Provides a benchmark against which current stock can be evaluated.

---

## Reorder Point

**Business definition:** Stock threshold represented in the inventory model at which replenishment may be required.

**Primary source:** `fact_inventory`

**Analytical use:** Supports inventory replenishment analysis.

---

## Stock Buffer

**Business definition:** Difference between the current stock position and the relevant safety-stock level.

**Conceptual interpretation:**

```text
Stock Buffer = Stock Level - Safety Stock
```

A positive buffer indicates stock above safety stock; a negative buffer indicates stock below safety stock.

**Analytical use:** Identifies inventory positions requiring investigation.

---

## Stock vs Safety %

**Business definition:** Current stock expressed relative to safety stock.

**Conceptual formula:**

```text
Stock vs Safety % = Stock Level / Safety Stock
```

**Interpretation:**

- Below 100% → stock is below safety stock
- Around 100% → stock is approximately at safety stock
- Above 100% → stock exceeds safety stock

**Interpretation caution:** This is an inventory-position indicator, not a direct service-level probability.

---

## Stock Status

The report includes a `Stock Status` measure used to classify inventory positions.

The status should be interpreted as a **screening indicator** rather than a complete inventory-optimization decision. Further investigation may require demand, forecast, supplier lead time, and replenishment-cycle information.

---

# 7. Shipment & Logistics KPIs

## Total Shipments

**Business definition:** Number of shipment records represented in the shipment fact table.

**Primary source:** `fact_shipment`

**Analytical use:** Measures logistics activity.

---

## Delivered Shipments

**Business definition:** Shipment records classified as delivered under the report's shipment status logic.

**Primary source:** `fact_shipment`

**Analytical use:** Measures completed delivery activity.

---

## On-Time Delivery %

**Business definition:** Proportion of relevant shipments delivered on time according to the report's on-time delivery logic.

**Analytical use:** Measures logistics service performance.

**Interpretation caution:** The exact business definition of "on time" must be kept consistent with the implemented DAX logic and available delivery-date/status fields.

---

## Average Lead Time

**Business definition:** Average elapsed lead time for the relevant logistics/procurement process.

**Analytical use:** Supports service-level and operational-efficiency analysis.

**Important:** Lead time must always be interpreted with its process definition and date role.

---

## Total Logistics Cost

**Business definition:** Total shipping/logistics cost represented in shipment records.

**Primary source:** `fact_shipment`

**Analytical use:** Quantifies logistics expenditure and supports cost-per-volume investigations.

---

## Total Quantity Shipped

**Business definition:** Total quantity represented by shipment transactions.

**Primary source:** `fact_shipment`

**Analytical use:** Measures logistics volume.

---

## Total Quantity Delivered

**Business definition:** Quantity associated with delivered shipments under the report's delivery logic.

**Primary source:** `fact_shipment`

**Analytical use:** Provides delivered-volume context alongside shipment count and on-time performance.

---

# 8. KPI Interpretation Framework

A senior analytical review should avoid evaluating KPIs independently.

### Cost

```text
Procurement Cost
       +
Logistics Cost
       +
Sales Cost
```

should be considered in relation to:

```text
Revenue → Profit → Profit Margin
```

### Service

```text
Shipment Volume
       +
Delivered Shipments
       +
On-Time Delivery %
       +
Lead Time
```

should be considered together rather than treating delivery percentage as the only logistics KPI.

### Inventory

```text
Stock Level
       +
Safety Stock
       +
Reorder Point
       +
Stock Buffer
```

should be evaluated alongside production, procurement, and demand context.

### Supplier

```text
Procurement Volume
       +
Procurement Cost
       +
Lead Time
       +
Quality
```

should be considered together to avoid selecting suppliers based on a single metric.

---

# 9. KPI Design Principles

The report follows several important BI principles:

1. **Use measures for dynamic business calculations.**
2. **Keep KPI definitions consistent across pages.**
3. **Separate operational volume from financial value.**
4. **Use ratios with appropriate denominators.**
5. **Interpret absolute and relative metrics together.**
6. **Preserve date context when comparing periods.**
7. **Avoid treating correlation as causation.**
8. **Investigate KPI exceptions at the lowest useful business grain.**

---

# 10. Metric Quality Checklist

Before publishing or extending the report, validate:

- [ ] Numerator and denominator are defined.
- [ ] Fact-table grain is known.
- [ ] Date relationship is appropriate.
- [ ] Filters behave as intended.
- [ ] Zero/blank cases are handled.
- [ ] Percentages use appropriate formatting.
- [ ] Currency metrics use consistent currency assumptions.
- [ ] Counts do not unintentionally duplicate entities.
- [ ] KPI labels match the underlying DAX logic.
- [ ] Business definitions are documented independently from visual titles.
