# Marketplace Merchandising & Order Funnel Health (Analytics Case Study)

## Overview
This project analyzes a marketplace catalog and order lifecycle data to answer two operational questions:
1) What products/categories/vendors are driving demand and revenue signals?
2) Where does the order funnel leak (cart → checkout → approval → repayment → completion), and what should we fix first?

The output is a corporate-style deliverable set:
- Analytics-ready SQL marts
- Executive dashboard (Metabase)
- Insights memo with prioritized recommendations

## Business Questions
- Which categories/brands/vendors contribute most to demand and revenue signals?
- Which products have high views but low carting (merchandising opportunity)?
- What are the largest funnel drop-offs (checkout, approval, repayment, completion)?
- Which segments have high cancellation/denial/refund rates?
- Where do we see inventory risk (high demand with low/negative inventory)?
- Are there margin anomalies (negative/zero margins) requiring data or pricing review?

## Datasets
- `product_catalog.csv`
  - Product attributes + vendor/category hierarchy
  - Price/cost/margin + inventory
  - Demand/revenue signals (30/90 days), views, carted users
- `user_order_history.csv`
  - Order line items with lifecycle timestamps:
    carted, checkout, approved/denied, repayment, canceled/refunded, completed

> Note: Order line items do not include price at purchase time; revenue from orders is not directly observable.
> We use catalog-level revenue fields and/or price proxies where explicitly stated.

## Tech Stack
- Postgres (Docker) as local warehouse
- dbt for transformations + documentation + tests
- Metabase for dashboards
- Python for ingestion, QA checks, and ad-hoc analysis

## Project Outputs
- `/models` (dbt): staging + marts
- `/dashboards`: screenshots and dashboard spec
- `/reports`: insights memo (PDF/Markdown)
- `/docs`: data dictionary + metric definitions + architecture diagram

## Repo Structure
- `data/` (optional): local-only data folder (not committed)
- `ingest/`: python scripts to load CSVs into Postgres
- `dbt/`: dbt project (models, tests, docs)
- `reports/`: insights memo + visuals
- `docs/`: diagrams, KPI definitions, data dictionary

## How to Run (local)
1. `docker compose up -d` (Postgres + Metabase)
2. `python ingest/load_data.py`
3. `cd dbt && dbt build`
4. Open Metabase and view the dashboard

## KPI Definitions (initial)
- Funnel stages (order-level):
  - Carted → Checkout → Approved (or Denied) → In Repayment → Completed
  - Exceptions: Canceled, Refunded
- Core metrics:
  - Checkout rate, approval rate, repayment start rate, completion rate
  - Denial/cancel/refund rates
  - Cycle times between stages (e.g., checkout→approved)

## License / Data Note
User identifiers are anonymized. Publish only aggregated outputs; do not publish raw datasets.
