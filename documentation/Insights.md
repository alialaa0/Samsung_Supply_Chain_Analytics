# Insights

This section summarizes the main analytical areas I focused on when building and reviewing the dashboard.

I use the dashboard to move from a high-level KPI to the supplier, facility, product, customer, or other dimension behind the result.

---

## 1. Supplier & Procurement

The Supplier & Procurement page brings together procurement quantity, procurement cost, lead time, and quality.

The main point of this analysis is that supplier performance should not be viewed using procurement cost alone.

For example, when reviewing a supplier I look at:

```text
Procurement Quantity
        +
Procurement Cost
        +
Lead Time
        +
Quality
```

This makes it possible to compare supplier activity from both a cost and operational perspective.

I also use product and supplier dimensions to move from the overall procurement result into individual suppliers and products.

---

## 2. Manufacturing

The Manufacturing analysis focuses on production quantity across facilities and products.

The main questions I use here are:

- Which facilities are contributing to production?
- Which products represent the largest production activity?
- How does production change over time?
- How does production quality relate to production volume?

The model also contains defective-unit and defect-rate information, so production volume can be reviewed together with the available quality information.

---

## 3. Inventory

The Inventory page compares the stock position with the inventory thresholds available in the model.

The main indicators are:

```text
Stock Level
Safety Stock
Reorder Point
Stock Buffer
Stock Status
Stock vs Safety %
```

This allows me to identify inventory positions that need further attention.

I use the facility and product dimensions to move from the overall inventory position to a more detailed view.

I do not treat a stock position by itself as proof of a stockout or excess inventory. The dashboard provides the inventory measures available in the model; the business interpretation still depends on the surrounding demand and supply context.

---

## 4. Shipment & Logistics

The logistics page focuses on shipment volume and delivery performance.

The main indicators are:

- Total shipments
- Delivered shipments
- On-time delivery %
- Average lead time
- Logistics cost
- Quantity shipped
- Shipment status

I use these measures together because shipment volume alone does not explain delivery performance.

The dashboard also contains facility, carrier, and delay-related information, which can be used to investigate the shipment results at a more detailed level.

---

## 5. Sales & Customer

The Sales & Customer pages combine revenue, profit, cost, quantity, orders, discounts, and margin.

The main analysis is:

```text
Revenue
   ↓
Cost
   ↓
Profit
   ↓
Profit Margin
```

This helps separate sales volume from financial performance.

I also use customer, country, channel, product, and category dimensions to understand where sales and profit are coming from.

---

## 6. Discount & Profitability

The dashboard includes both:

- Average Discount %
- Total Discount Amount

along with revenue, cost, profit, and profit margin.

This allows discounting to be reviewed together with profitability rather than as a standalone KPI.

The analysis can be used to identify segments where discounting and profitability should be reviewed together.

---

## 7. Cross-Functional Analysis

One of the main strengths of the model is that the same dimensions can be used across different business processes.

For example, `dim_product` connects the analysis of:

```text
Procurement
Production
Inventory
Shipment
Sales
```

This makes it possible to follow a product across several parts of the supply chain.

Similarly, the facility dimension can be used to compare production, inventory, and shipment activity.

---

## 8. How I Use the Dashboard

My analysis follows a simple process:

```text
1. Start with the overview
        ↓
2. Identify the KPI or area I want to investigate
        ↓
3. Filter by supplier / facility / product / customer
        ↓
4. Compare the related KPIs
        ↓
5. Move to the detailed page
        ↓
6. Use the result to understand the business context
```

This keeps the dashboard focused on analysis rather than only displaying numbers.

---

## 9. Key Analytical Takeaways

The dashboard brings together three different views of the supply chain:

### Operational

```text
Procurement
Production
Inventory
Shipments
Lead Time
```

### Commercial

```text
Customers
Orders
Quantity
Revenue
Discounts
```

### Financial

```text
Cost
Profit
Profit Margin
Logistics Cost
Procurement Cost
```

Looking at these areas together gives a more complete view of supply-chain performance than reviewing each process separately.

---

## 10. What the Dashboard Helps Me Answer

At the end of the analysis, the dashboard helps answer:

- Where is procurement activity concentrated?
- How are suppliers performing?
- Which facilities and products drive production?
- Where is stock positioned relative to safety stock and reorder points?
- How is shipment and delivery performance changing?
- Where are logistics costs coming from?
- Which customers, countries, channels, and products contribute to sales?
- How do revenue, cost, profit, and margin compare across the available dimensions?

These questions are the main reason I structured the report around the full supply-chain flow rather than creating separate disconnected dashboards.
