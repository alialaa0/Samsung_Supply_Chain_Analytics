# Business Insights

## 1. Purpose

This document translates the dashboard from a collection of visuals into an analytical framework for decision-making.

The goal is not to list isolated observations. A senior analytics interpretation should connect:

```text
Metric
  ↓
Pattern
  ↓
Potential driver
  ↓
Business impact
  ↓
Validation required
  ↓
Decision / action
```

> **Evidence standard:** This document is based on the implemented PBIX report structure and KPI set. It deliberately avoids inventing numeric findings that cannot be verified from a live execution of the model. Dashboard users should validate the current values and filters before treating an observation as a measured business fact.

---

# 2. Executive Insight Framework

The report is designed around five connected performance areas:

```text
Supplier & Procurement
          ↓
Manufacturing & Inventory
          ↓
Shipment & Logistics
          ↓
Customers & Sales
          ↓
Profitability
```

The key analytical principle is that an operational KPI should be connected to its downstream commercial or financial impact where possible.

For example:

```text
Supplier Lead Time
       ↓
Inventory Position
       ↓
Shipment Reliability
       ↓
Customer Experience
       ↓
Commercial Performance
```

This is more useful than reviewing each dashboard page independently.

---

# 3. Supplier & Procurement Insights

## 3.1 Supplier performance should be evaluated multidimensionally

The report provides supplier-level analysis across:

- Procurement quantity
- Procurement cost
- Average lead time
- Quality

A supplier with high procurement volume should therefore not be assessed on cost alone.

A robust supplier review asks:

```text
High Volume?
    +
Competitive Cost?
    +
Acceptable Lead Time?
    +
Acceptable Quality?
```

### Analytical implication

Supplier concentration may create operational dependency even when the supplier performs well on an individual KPI.

**Follow-up analysis:** calculate supplier concentration by procurement cost and quantity, then compare the concentration against lead-time and quality performance.

---

## 3.2 Lead time requires operational context

A long average lead time may indicate a procurement constraint, but the dashboard alone should not be used to conclude the root cause.

Potential validation dimensions include:

- Supplier
- Product
- Facility
- Country
- Order period
- Procurement quantity

The correct analytical sequence is:

```text
Identify high lead time
        ↓
Segment by supplier/product
        ↓
Check whether the pattern persists
        ↓
Compare with quality and cost
        ↓
Investigate operational cause
```

---

# 4. Manufacturing Insights

## 4.1 Production concentration matters

The manufacturing page provides production analysis by facility and product.

A useful question is not simply:

> Which facility produces the most?

The more useful question is:

> **Which facilities or products carry the greatest operational dependency?**

High production concentration can create a potential single-point-of-failure risk if capacity, inventory, or logistics constraints affect the same facility.

**Follow-up analysis:** compare production volume with facility annual capacity and shipment activity.

---

## 4.2 Production volume should be evaluated with quality

Production output alone is incomplete.

The model contains production-quality information including defective units and defect rate.

The analytical relationship is:

```text
Production Volume
        +
Defect Rate
        ↓
Effective Output Quality
```

A high-volume facility with an elevated defect rate can require more attention than a low-volume facility with the same rate.

---

# 5. Inventory Insights

## 5.1 Safety stock is a reference point, not a performance target by itself

The report exposes:

- Stock Level
- Safety Stock
- Reorder Point
- Stock Buffer
- Stock Status
- Stock vs Safety %

This enables inventory positions to be classified relative to operational thresholds.

### Key diagnostic

```text
Stock < Safety Stock
        ↓
Potential inventory risk
        ↓
Check:
Procurement lead time
Production availability
Demand / sales volume
Shipment requirements
```

However, stock below safety stock is **not automatically evidence of a stockout or service failure**.

The dashboard should be used to identify positions for investigation.

---

## 5.2 Excess inventory requires a different question

Stock above safety stock is not automatically inefficient.

The analytical test should consider:

```text
Stock Level
    +
Demand / Sales Volume
    +
Reorder Point
    +
Lead Time
    +
Production / Procurement Pattern
```

A large stock buffer may be intentional when supply uncertainty or lead time is high.

Therefore:

> **Inventory optimization requires balancing availability risk against holding exposure.**

The current dashboard provides the inventory-position layer; a complete optimization model would require additional demand/forecast and inventory-cost inputs.

---

# 6. Shipment & Logistics Insights

## 6.1 Delivery performance should be read with lead time

The logistics page provides:

- Total Shipments
- Delivered Shipments
- On-Time Delivery %
- Average Lead Time
- Logistics Cost
- Shipment status
- Facility-level analysis

On-time delivery is therefore only one part of logistics performance.

A more robust view is:

```text
Shipment Volume
        +
Delivery Completion
        +
On-Time %
        +
Lead Time
        +
Logistics Cost
```

---

## 6.2 High logistics cost should be normalized

A facility with high total logistics cost may simply process more shipments.

Therefore:

```text
Total Logistics Cost
```

should not be interpreted as inefficiency without considering:

```text
Shipment Volume
or
Quantity Shipped
```

A useful follow-up KPI would be:

```text
Logistics Cost per Shipment
```

and, where the business definition supports it:

```text
Logistics Cost per Unit Shipped
```

These ratios would make facility comparisons more economically meaningful.

---

## 6.3 Delays should be investigated by reason

The shipment model includes a delay-reason attribute.

This creates an opportunity to move from:

```text
"What percentage was late?"
```

to:

```text
"Why were shipments late?"
```

That distinction matters because a KPI describes the outcome while a delay-reason analysis can identify an operational intervention point.

---

# 7. Sales & Customer Insights

## 7.1 Revenue and profit answer different questions

The sales pages provide revenue, cost, profit, quantity, orders, and discount-related measures.

A product or customer with high revenue is not automatically the most profitable.

The correct analytical comparison is:

```text
Revenue
   +
Cost
   ↓
Profit
   ↓
Profit Margin
```

This allows the business to distinguish scale from economic contribution.

---

## 7.2 Discounting should be connected to profitability

The report includes:

- Average Discount %
- Total Discount Amount
- Revenue
- Profit
- Profit Margin

This allows discounting to be analyzed as a commercial lever rather than an isolated percentage.

A useful diagnostic is:

```text
Higher Discount
      ↓
Revenue response?
      ↓
Quantity response?
      ↓
Profit impact?
      ↓
Margin impact?
```

The dashboard should not be used to claim that discounts caused a profit change unless the underlying analysis controls for other factors.

---

## 7.3 Customer and channel analysis

Customer-level and channel-level views can reveal concentration and performance differences.

Useful follow-up questions include:

- Which customers contribute the most revenue?
- Which customers contribute the most profit?
- Are high-revenue customers also high-margin customers?
- Does performance vary by channel?
- Does country-level performance hide customer-level differences?

---

# 8. Cross-Functional Insights

## 8.1 The strongest analysis connects operational and commercial metrics

The report's model enables cross-dimensional analysis.

For example:

```text
Supplier
   ↓
Product
   ↓
Facility
   ↓
Shipment
   ↓
Customer
   ↓
Sales
```

This makes it possible to investigate whether operational performance is associated with commercial outcomes.

However, association should not be presented as causation without a controlled analysis.

---

## 8.2 Identify trade-offs, not just winners

A senior BI review should explicitly search for trade-offs.

Examples:

| Trade-off | Analytical question |
|---|---|
| Cost vs Quality | Are lower procurement costs associated with lower quality scores? |
| Inventory vs Service | Do higher stock buffers correspond to better delivery performance? |
| Production vs Quality | Are high-output facilities also maintaining acceptable defect rates? |
| Discount vs Margin | Does higher discounting coincide with weaker profitability? |
| Logistics Cost vs Service | Are higher logistics costs associated with better delivery performance? |
| Supplier Concentration vs Risk | Is procurement concentrated among a small number of suppliers? |

These are **hypotheses for investigation**, not conclusions by themselves.

---

# 9. Recommended Executive Review

A management review can use the following sequence:

### Step 1 — Start with financial performance

Review:

- Revenue
- Profit
- Profit Margin
- Cost

### Step 2 — Identify operational pressure

Review:

- Procurement cost
- Lead time
- Production
- Inventory position
- Shipment performance

### Step 3 — Segment the problem

Break the metric down by:

- Supplier
- Facility
- Product
- Customer
- Country
- Channel
- Time

### Step 4 — Validate the driver

Use the relevant operational dimension rather than assuming causation.

### Step 5 — Quantify business impact

Connect the operational issue to:

- Cost
- Revenue
- Profit
- Service level
- Inventory exposure

---

# 10. Analytical Gaps & Recommended Extensions

The current dashboard provides a strong descriptive BI layer. The following extensions would move the solution toward deeper decision support.

## 10.1 Supplier concentration

Add:

```text
Supplier Procurement Share %
Top-N Supplier Share %
```

Purpose: quantify dependency.

---

## 10.2 Logistics efficiency

Add:

```text
Logistics Cost / Shipment
Logistics Cost / Unit
```

Purpose: normalize logistics expenditure.

---

## 10.3 Inventory efficiency

If additional inputs become available:

```text
Inventory Turnover
Days Inventory Outstanding
Stockout Rate
Excess Inventory Value
```

Purpose: evaluate inventory efficiency beyond stock thresholds.

---

## 10.4 Manufacturing capacity utilization

The facility dimension includes annual capacity.

A future metric could compare:

```text
Production / Available Capacity
```

Purpose: identify under-utilized or capacity-constrained facilities.

---

## 10.5 Customer profitability

Extend customer analysis with:

```text
Revenue by Customer
Profit by Customer
Margin by Customer
Order Frequency
Average Order Value
```

Purpose: distinguish customer scale from customer economics.

---

# 11. Insight Quality Standard

Every published insight should pass this test:

```text
Is the observation directly supported by the data?
        ↓
Is the comparison like-for-like?
        ↓
Is the denominator appropriate?
        ↓
Could another factor explain the pattern?
        ↓
Is causation being claimed without evidence?
        ↓
Can the business act on the finding?
```

If the answer fails any of these checks, the statement should be reframed as a **hypothesis** rather than a conclusion.

---

# 12. Final Analytical Position

The dashboard should be treated as a **decision-support layer** over the supply-chain model.

Its strongest analytical capability is the ability to connect:

```text
Procurement
    ↓
Manufacturing
    ↓
Inventory
    ↓
Logistics
    ↓
Customers
    ↓
Sales
    ↓
Profitability
```

The next level of maturity is not adding more charts. It is adding **validated ratios, root-cause analysis, scenario analysis, and clearly defined decision thresholds** where the underlying data supports them.
