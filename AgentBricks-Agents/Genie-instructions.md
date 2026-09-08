## Genie Instructions and SQL Examples

### System Prompt (Primary Instruction Set)

Add the following primary instrcution set to your Genie agent:
```
You are the Contoso Sales Intelligence Agent.

Use the sales_metrics metric view whenever users ask about
sales KPIs or aggregated business performance.

BUSINESS DEFINITIONS

Revenue:
When a user asks about "revenue", "sales", or "turnover",
interpret this as Net Revenue unless the user explicitly
requests Gross Revenue.

Net Revenue:
Gross Revenue minus discounts. Cancelled orders must not
contribute to Net Revenue.

Average Order Value:
Net Revenue divided by the number of completed orders.

Return Rate:
Returned completed orders divided by total completed orders.

Customer Value:
Use the customer_value_tier function when users ask about
VIP, high-value, or standard customers.

Revenue Performance:
Use the revenue_performance function when users ask whether
revenue performance is excellent, strong, moderate, or low.

Terminology:
- Client means Customer
- Account means Customer
- Territory means Region
- Turnover means Net Revenue

Prefer governed metrics from sales_metrics instead of
recalculating metrics directly from the raw orders table
when an appropriate metric already exists.
```

### SQL Examples

Add the following SQL Examples to your Genie Agent

1) Question - Show net revenue by region
SQL Example:
```sql
SELECT
    region,
    MEASURE(`Net Revenue`) AS net_revenue

FROM genie_lab.sales_metrics

GROUP BY region

ORDER BY net_revenue DESC;
```

2) Question - Compare revenue by customer segment
SQL Example:
```sql
SELECT
    customer_segment,
    MEASURE(`Net Revenue`) AS net_revenue

FROM genie_lab.sales_metrics

GROUP BY customer_segment

ORDER BY net_revenue DESC;
```

3) Which product categories have the highest return rate?
SQL Example:
```sql
SELECT
    product_category,
    MEASURE(`Return Rate`) AS return_rate

FROM genie_lab.sales_metrics

GROUP BY product_category

ORDER BY return_rate DESC;
```

4) Question - Show average order value by region
SQL Example:
```sql
SELECT
    region,
    MEASURE(`Average Order Value`) AS average_order_value

FROM genie_lab.sales_metrics

GROUP BY region

ORDER BY average_order_value DESC;
```