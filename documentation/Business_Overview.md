# Business Overview

## 1. Executive Summary

**Samsung Supply Chain Analytics** is a Power BI business intelligence solution designed to provide a consolidated view of supply-chain performance across procurement, suppliers, manufacturing, inventory, logistics, customers, sales, and profitability.

The solution is structured around a multi-fact analytical model with shared dimensions. This allows decision-makers to move from an executive-level view into specific operational processes without treating each process as an isolated reporting problem.

The dashboard is designed to answer four core management questions:

1. **Are we buying efficiently?**
2. **Are we producing and holding inventory effectively?**
3. **Are we delivering reliably and at an acceptable logistics cost?**
4. **Are sales and customer activity generating profitable growth?**

> **Source of truth:** `Supply Cahin Analysis.pbix`. This document describes the implemented report and semantic model; it does not claim operational processes that are not represented in the PBIX.

---

## 2. Business Problem

Supply-chain performance is inherently cross-functional. Procurement decisions affect production availability; production affects inventory; inventory and facility capacity affect shipment execution; shipment performance affects customer service; and sales economics ultimately determine profitability.

A fragmented reporting approach can therefore create several analytical problems:

- Supplier performance is evaluated without connecting it to procurement cost and lead time.
- Inventory is viewed independently from production and facility capacity.
- Shipment volume is reviewed without sufficient visibility into delivery performance and logistics cost.
- Revenue is monitored without simultaneously considering cost, discounting, and profit.
- Different business processes may use different time perspectives.

The dashboard addresses these problems by bringing the major supply-chain processes into a single analytical model.

---

## 3. Analytical Scope

The report covers the following business domains.

| Domain | Primary analytical focus |
|---|---|
| Supplier & Procurement | Procurement quantity, procurement cost, supplier quality, supplier lead time |
| Manufacturing | Production volume, facility performance, product production |
| Inventory | Stock level, safety stock, reorder point, stock buffer |
| Shipment & Logistics | Shipment volume, delivery status, on-time delivery, lead time, logistics cost |
| Sales | Revenue, quantity sold, orders, discounts, cost |
| Customers | Customer and channel performance |
| Profitability | Profit, profit margin, product/customer profitability |
| Time | Trend analysis using the date dimension |

---

## 4. Business Process View

The analytical story follows the supply-chain lifecycle:

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

This is a **business-process view**, not the physical database relationship structure.

The Power BI model uses shared dimensions to analyze different fact processes consistently.

---

## 5. Management Questions

### Procurement & Suppliers

- Which suppliers contribute the largest procurement volume and cost?
- How does supplier lead time vary?
- How does supplier quality compare?
- Are procurement patterns concentrated among specific suppliers or products?

### Manufacturing

- Which facilities contribute the most production?
- Which products drive production volume?
- How does production activity change over time?
- Where should operational attention be focused?

### Inventory

- What is the current stock position?
- How does stock compare with safety-stock requirements?
- Which facilities or products have limited stock buffers?
- Where could inventory risk require further investigation?

### Logistics

- How many shipments are being processed?
- What proportion is delivered on time?
- What is the average lead time?
- Which facilities or shipment flows generate the highest logistics cost?
- What shipment statuses or delay reasons require attention?

### Sales & Customers

- Which products and categories generate revenue and profit?
- Which customers or channels contribute most to commercial performance?
- How does profitability vary by country?
- How much discounting is being applied?

---

## 6. Analytical Architecture

The semantic model follows a **Galaxy Schema / Constellation Schema** approach.

### Dimensions

```text
dim_customer
dim_supplier
dim_product
dim_date
dim_facility
```

### Facts

```text
fact_sales
fact_inventory
fact_production
fact_procurement
fact_shipment
```

Conceptually:

```text
                    dim_customer
                         │
                         │
dim_supplier ───────┐    │
                    │    │
dim_product ────────┼────┼────► Fact processes
                    │    │
dim_date ───────────┼────┤
                    │    │
dim_facility ───────┘    │
                         │
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
      Procurement     Production     Inventory
          │              │              │
          └──────────────┼──────────────┘
                         │
                      Shipment
                         │
                       Sales
```

The important design principle is that **facts are analyzed through conformed dimensions rather than by creating unnecessary fact-to-fact dependencies**.

---

## 7. Report Experience

The PBIX contains the following analytical pages:

1. **Intro**
2. **Overview**
3. **Supplier & Procurement**
4. **Inventory & Manufacturer**
5. **Shipment & Logistics**
6. **Sales & Customer**
7. **Sales & Customer 2**

The pages progressively move from broad performance monitoring toward more focused operational and commercial analysis.

---

## 8. Decision-Support Flow

A typical analytical workflow is:

```text
Executive Overview
       ↓
Identify performance deviation
       ↓
Select business process
       ↓
Segment by supplier / facility / product / customer / country
       ↓
Investigate operational driver
       ↓
Evaluate financial or service impact
       ↓
Define follow-up action
```

The dashboard is therefore intended to support **diagnosis**, not merely KPI display.

---

## 9. Technology

The implemented solution uses:

- **Power BI** — semantic modeling, interactive reporting, visualization
- **DAX** — business measures and analytical calculations
- **Figma** — dashboard visual/design preparation

No SQL, ETL pipeline, stored procedure, or enterprise data-warehouse implementation is claimed as part of this repository unless separately added and documented.

---

## 10. Senior Analytics Perspective

The core value of the project is not the number of visuals. It is the connection between:

```text
Business Process
      ↓
Data Model
      ↓
Metric Definition
      ↓
Visual Analysis
      ↓
Business Interpretation
```

A KPI is only useful when its definition, grain, filters, time context, and business meaning are understood.

This project therefore treats the Power BI semantic model as an analytical layer rather than simply a visualization layer.
