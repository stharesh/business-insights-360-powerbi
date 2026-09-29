# Business Insights 360 — Power BI

An end-to-end business intelligence portfolio project designed to connect finance, sales, marketing, supply chain, forecasting, and executive decision-making in one Power BI experience.

> **Project status:** Phase 1 — repository foundation. The project is being published in reviewed phases; screenshots, detailed analytical logic, and supporting evidence will be added only after each phase is approved.

## Project overview

Business Insights 360 is structured as a cross-functional decision-support solution. It is intended to help business users move from an executive performance summary into focused investigation of profitability, customer and product contribution, market performance, forecast quality, and inventory risk.

The portfolio story is organized around five decision areas:

- **Executive:** Review company-wide performance and identify where deeper investigation is needed.
- **Finance:** Trace the path from Gross Sales to Net Profit and compare results with prior-year or target benchmarks.
- **Sales:** Evaluate customer, product, and market contribution across both revenue and profitability.
- **Marketing:** Identify segments, categories, divisions, and geographies producing profitable growth.
- **Supply Chain:** Assess forecast accuracy and distinguish potential Out-of-Stock (OOS) from Excess Inventory (EI) risk.

## Core KPI framework

The report uses a shared KPI framework so the same business definitions remain consistent across views.

| KPI | Decision use |
| --- | --- |
| Net Sales | Measure realized revenue after applicable deductions |
| Gross Margin | Evaluate profitability after product-related costs |
| Net Profit | Assess profitability after operating expenses |
| Forecast Accuracy | Measure the magnitude of forecast error |
| Market Share | Compare competitive position across markets and periods |

Detailed definitions and calculation context will be added in the documentation phase.

## Planned report views

| View | Primary analytical focus |
| --- | --- |
| Executive | Cross-functional performance, trends, and investigation priorities |
| Finance | P&L performance, profitability, and variance to benchmark |
| Sales | Customer, product, and market contribution |
| Marketing | Segment performance and profitable growth |
| Supply Chain | Forecast accuracy, net error, and inventory risk |

## Analytical capabilities

- Dynamic P&L reporting from Gross Sales through Net Profit
- Last-year and target benchmark switching
- Customer, product, market, and geography drill-downs
- Forecast error, Forecast Accuracy, OOS, and EI analysis
- Semantic modeling across actuals, forecasts, costs, targets, and market share
- Performance investigation using Power BI Performance Analyzer and DAX Studio

## Semantic model snapshot

The approved model inventory contains:

- **29 tables**
- **127 columns**
- **65 measures**
- **28 relationships**

The model is organized around shared date, customer, product, and market dimensions, with fact and input tables supporting actuals, forecasts, cost allocation, profitability, targets, and competitive analysis.

## Repository structure

```text
business-insights-360-powerbi/
├── README.md
├── .gitignore
├── assets/
│   ├── dashboards/
│   ├── model/
│   ├── navigation/
│   └── performance/
└── docs/
    ├── business-overview.md
    ├── dax-highlights.md
    ├── model-inventory.md
    ├── performance-optimization.md
    └── semantic-model.md
```

## Documentation map

- [Business overview](docs/business-overview.md) — business questions and decision areas
- [Semantic model](docs/semantic-model.md) — model design and logical table groups
- [DAX highlights](docs/dax-highlights.md) — selected analytical logic patterns
- [Performance optimization](docs/performance-optimization.md) — diagnostic workflow and evidence
- [Model inventory](docs/model-inventory.md) — detailed tables, columns, measures, and relationships

## Publication notes

- The Power BI `.pbix` file is intentionally excluded while data-sharing and attribution requirements are reviewed.
- This repository will not claim a quantified performance improvement unless a controlled before-and-after benchmark is documented.
- Attribution will be finalized before the related source materials or implementation details are published.
- No license has been added at this stage.

## Current phase

Phase 1 establishes the repository, its narrative foundation, and the approved documentation structure. Detailed documentation, validated screenshots, analytical logic, and performance evidence belong to later review phases.
