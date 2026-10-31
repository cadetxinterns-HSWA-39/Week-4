# CadetX — Heavy Supplier, Inventory & Warehouse Analytics

## Week 4 submission: Product Performance, ABC Classification, Movement, Demand Trend & Turnover

Phase 2 (Core Product, Inventory & Warehouse Analytics), sprint 1 of 3.

## Team

- Odetunde Olumide Temitope — Data Scientist
- Kukoyi Zainab Omotola — Data Analyst
- Nyong Asuabiat — Data Analyst

## What's in this folder

```
week-04/
├── Week4_Product_Analytics.ipynb      (full analysis, run end to end, outputs included)
├── README.md
├── SPRINT_NOTES_WEEK4.md
└── outputs/
    ├── product_performance_full.csv   (one row per product, every metric below)
    ├── category_performance.csv
    ├── abc_classification.csv
    ├── velocity_and_dead_stock.csv
    ├── demand_trend.csv
    ├── turnover_by_product.csv
    ├── turnover_by_branch.csv
    └── charts/ (6 PNG charts)
```

To re-run the notebook, point `DATA_DIR` at a folder holding `sales_transactions.csv` and `inventory_position.csv` (both in the Week 2 folder).

## Ground rules

- Sales = **Delivered** orders only: 117,656 order lines, with 12,746 cancelled lines excluded.
- Revenue = `line_total`, **excluding GST**. Cost = `quantity × unit_cost`.
- Demand comes from `sales_transactions.csv`, not the stock ledger, because the ledger's OUT movements miss about 9% of delivered units (Week 3 validation).
- Period: 2019-01-01 to 2024-12-31. 30 products, 6 branches.

## Results

**Headline:** 1,234,939 units, ₹2,295.9 cr revenue (ex-GST), ₹495.0 cr gross profit, **21.56% gross margin**.

### 1. Product performance
- Two products carry over a third of revenue: Engine Block EB-600 (₹485.7 cr, 21.2%) and Transmission Assembly TA-800 (₹338.8 cr, 14.8%).
- Four categories make up 89% of revenue: Engine (33.0%), Hydraulic (28.4%), Transmission (14.8%), Undercarriage (13.1%).
- Revenue and margin pull in opposite directions: A-class products earn 17–25% margin, while the lowest-revenue products earn 26–46%.

### 2. ABC / Pareto classification
| Class | Products | Share of revenue | Share of units |
|---|---|---|---|
| A (first 80%) | 10 | 81.5% | 33.5% |
| B (next 15%) | 7 | 14.1% | 23.1% |
| C (last 5%) | 13 | 4.4% | 43.4% |

The 13 C-class products are 43% of units but only 4.4% of revenue, so they take up a lot of handling for little revenue.

### 3. Fast-moving products
Ranked by **order lines** (picking frequency) into thirds: 10 Fast, 10 Medium, 10 Slow. Fast products have only **3.4% more order lines** than Slow ones (3.5% more units), and the busiest product has just 5.6% more lines than the quietest. Movement is almost uniform across the range, so the Fast/Slow split is a ranking, not a real gap. Ranking by units sold instead gives the same class for 22 of 30 products.

### 4. Slow-moving and dead stock
**0 dead-stock products.** Every product sold within the last day of the data, and the weakest product still sold 1,304 units in the last 90 days. The Slow list is relative only; none of those products has stopped selling.

### 5. Demand trend
Network units are flat-to-slightly-down (207,925 in 2019, 199,858 in 2024). One product out of 30 shows a statistically significant trend (Brake Pad BP-40, −2.3% a year), which is about what chance alone would produce, so the other 29 are **Stable**. Single-year swings per product reach −15.6% to +13.4% (2024 vs 2023); these are noise, not trends. Seasonality is mild, with July and August about 7% above an average month.

### 6. Inventory turnover
- Network turnover is **0.0103 a year**, i.e. about **97 years of supply** on a last-12-months basis (199,029 units sold against 19.3 million units in stock).
- Product range: 85 to 108 years of supply.
- By branch: Chennai 81 years, Kolkata 85, Ahmedabad 100, Delhi 103, Pune 106, Hyderabad 116.

## Caveats

- All 180 stock positions carry the `scale_mismatch_flag` raised in Week 3 (`current_stock` is far above `max_stock`). Turnover and years of supply are therefore **as recorded** and need confirming against a physical count before anyone acts on them.
- Velocity classes depend on the chosen basis (order lines here). Units sold gives a different split for 8 of 30 products.
- Revenue here is ex-GST. `product_features.csv` (Week 3) holds GST-inclusive revenue, which is about 27% higher.
