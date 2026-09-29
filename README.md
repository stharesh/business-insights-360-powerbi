# Business Insights 360 — Power BI

An end-to-end business intelligence portfolio project designed to connect finance, sales, marketing, supply chain, forecasting, and executive decision-making in one Power BI experience.

> **Project status:** Review candidate — all documentation phases are consolidated. Visual evidence, field-level metadata, and attribution remain explicit final-review gates.

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

Detailed definitions and calculation context are available in the supporting documentation.

## Report views

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

## Evidence status

| Evidence | Status | Review location |
| --- | --- | --- |
| Business decision framework | Documented | [Business overview](docs/business-overview.md) |
| Selected DAX patterns | Documented with confirmed expressions | [Analytical logic patterns](docs/dax-highlights.md) |
| Performance workflow | Documented with observed timings | [Performance analysis](docs/performance-optimization.md) |
| Logical semantic model | Documented | [Semantic model](docs/semantic-model.md) |
| Field-level model inventory | Partially validated; direct export required | [Model inventory](docs/model-inventory.md) |
| Dashboard screenshots | Pending validated captures | [Evidence manifest](assets/README.md) |
| Model and diagnostic screenshots | Pending validated captures | [Evidence manifest](assets/README.md) |
| Attribution and sharing rights | Pending confirmation | [Final review checklist](docs/final-review-checklist.md) |

## Skills demonstrated

- Translating cross-functional business questions into an analytical reporting structure
- Financial modeling from Gross Sales through Net Profit
- DAX design for dynamic P&L reporting and benchmark switching
- Forecast Accuracy and directional inventory-risk analysis
- Semantic modeling across actuals, forecasts, costs, targets, and market share
- Report-performance investigation using Power BI Performance Analyzer and DAX Studio
- Evidence-aware technical documentation that separates observations from unverified claims

## Repository structure

```text
business-insights-360-powerbi/
├── README.md
├── .gitignore
├── assets/
│   ├── README.md
│   ├── dashboards/README.md
│   ├── model/README.md
│   ├── navigation/README.md
│   └── performance/README.md
└── docs/
    ├── business-overview.md
    ├── dax-highlights.md
    ├── final-review-checklist.md
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
- [Evidence manifest](assets/README.md) — required screenshots and capture standards
- [Final review checklist](docs/final-review-checklist.md) — evidence, metadata, attribution, and publication gates

## Publication notes

- The Power BI `.pbix` file is intentionally excluded while data-sharing and attribution requirements are reviewed.
- Dashboard, model, navigation, and diagnostic screenshots are not included until validated captures are available.
- This repository will not claim a quantified performance improvement unless a controlled before-and-after benchmark is documented.
- The original source of the Business Insights 360 / AtliQ case study must be confirmed before attribution is finalized.
- No license has been added at this stage.

## Review status

The documentation phases are consolidated into this review candidate. Before final submission, complete the remaining evidence, metadata, attribution, and sharing-rights checks in the [final review checklist](docs/final-review-checklist.md). Missing evidence is labeled directly rather than replaced with mockups or inferred technical details.
