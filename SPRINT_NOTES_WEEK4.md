# Sprint Notes — Week 4

## Team

- Odetunde Olumide Temitope — Data Scientist
- Kukoyi Zainab Omotola — Data Analyst
- Nyong Asuabiat — Data Analyst

**Scrum Master this week:** _(to be filled in by the team)_

**Sprint scope:** Product Performance Analysis, ABC / Pareto Classification, Fast-Moving Product Identification, Slow-Moving & Dead Stock Identification, Product Demand Trend Analysis, Inventory Turnover Analysis

## What was completed

- Built `Week4_Product_Analytics.ipynb`, run end to end, producing seven result tables and six charts.
- Product performance for all 30 products and 15 categories: units, order lines, revenue, cost, gross profit, margin and revenue share.
- ABC / Pareto classification: 10 A, 7 B and 13 C products (A = 81.5% of revenue).
- Velocity classes (Fast/Medium/Slow) ranked by order lines, with units sold as a cross-check.
- Dead-stock screen at 90 days: 0 products.
- Demand trend per product with a significance test; seasonality index by calendar month.
- Inventory turnover, days of cover and years of supply by product and by branch.

## Decisions made

- Sales figures use Delivered orders only, revenue ex-GST, from `sales_transactions.csv`. The stock ledger is not used for demand because its OUT movements miss about 9% of delivered units.
- Velocity is ranked by **order lines** (picking frequency), not units sold. Units sold changes the class of 8 of 30 products, so the basis is stated wherever classes appear.
- A product is called Growing or Declining only if its trend is beyond ±2% a year and statistically significant (p < 0.05). Otherwise it is Stable.
- Turnover and years of supply use the last 12 months of delivered units, not all history.

## Findings

- Revenue is concentrated: two products make up 36% and four categories make up 89%.
- Movement is almost uniform across products (Fast vs Slow differ by about 3%), and no product is dead stock.
- Demand is stable; 29 of 30 products show no significant trend.
- Stock is about 97 years of supply, so overstock is the main issue to take into Week 5.

## Open items

- All 180 stock positions carry the Week 3 `scale_mismatch_flag`. Stock-based results need confirming against a physical count.
## Next steps

Week 5: Stock Health Assessment, Overstock & Understock Detection and Inventory Aging Analysis, building on the turnover results here.
