# DAX Measures

Main DAX measures used in the Samsung Supply Chain Analytics project.

## Sales

```DAX
total_revenue =
SUM(fact_sales[gross_revenue])
```

```DAX
total_profit =
SUM(fact_sales[profit])
```

```DAX
profit_margin =
DIVIDE(
    [total_profit],
    [total_revenue],
    0
)
```

```DAX
total_cost =
SUM(fact_sales[total_cost])
```

```DAX
total_quantity_sold =
SUM(fact_sales[quantity_sold])
```

```DAX
total_orders =
DISTINCTCOUNT(fact_sales[order_number])
```

```DAX
avg_discount_pct =
AVERAGE(fact_sales[discount])
```

## Procurement

```DAX
total_quantity_procuremnt =
SUM(fact_procurement[order_quantity])
```

```DAX
total_procurement_cost =
SUM(fact_procurement[total_cost])
```

```DAX
avg_lead_time =
AVERAGE(fact_procurement[lead_time_days])
```

```DAX
avg_quality =
AVERAGE(fact_procurement[quality_score])
```

## Production

```DAX
total_quantity_produce =
SUM(fact_production[quantity_produced])
```

```DAX
defect_rate =
DIVIDE(
    SUM(fact_production[defective_units]),
    SUM(fact_production[quantity_produced]),
    0
)
```

## Inventory

```DAX
Current Stock =
SUM(fact_inventory[stock_level])
```

```DAX
Safety Stock =
SUM(fact_inventory[safety_stock_level])
```

```DAX
Reorder Point =
SUM(fact_inventory[reorder_point])
```

```DAX
Stock Buffer =
[Current Stock] - [Safety Stock]
```

```DAX
Stock vs Safety % =
DIVIDE(
    [Current Stock],
    [Safety Stock],
    0
)
```

```DAX
Stock Status =
SWITCH(
    TRUE(),
    [Current Stock] < [Safety Stock], "Below Safety Stock",
    [Current Stock] < [Reorder Point], "Below Reorder Point",
    "Healthy"
)
```

## Shipment & Logistics

```DAX
total_shipments =
COUNTROWS(fact_shipment)
```

```DAX
delivered_shipments =
CALCULATE(
    [total_shipments],
    fact_shipment[status] = "Delivered"
)
```

```DAX
total_logistic_cost =
SUM(fact_shipment[shipping_cost])
```

```DAX
total_quantity_shipped =
SUM(fact_shipment[quantity])
```

```DAX
total_quantity_delivered =
CALCULATE(
    [total_quantity_shipped],
    fact_shipment[status] = "Delivered"
)
```

```DAX
on_time_delivery_pct =
DIVIDE(
    [delivered_shipments],
    [total_shipments],
    0
)
```

## Date Analysis

The model uses `dim_date` as the common date dimension for time-based analysis.

For an inactive date relationship:

```DAX
Example Measure =
CALCULATE(
    [Total Measure],
    USERELATIONSHIP(
        dim_date[date_key],
        fact_shipment[delivery_date_key]
    )
)
```

## Measure Principles

The measures are built around reusable calculations:

```text
Fact Data
   ↓
Base Measure
   ↓
KPI
   ↓
Dashboard Visual
```

The main analytical areas are:

```text
Sales
Procurement
Production
Inventory
Shipment
Profitability
```

> The measure names above were verified from the PBIX report. Where the original DAX expression was not readable from the PBIX metadata, the formulas shown are documented implementations rather than claims that they are byte-for-byte identical to the original PBIX expressions.
