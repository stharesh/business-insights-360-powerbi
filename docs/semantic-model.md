# Semantic Model

The Business Insights 360 semantic model brings actual sales, forecasts, costs, operating expenses, targets, and market-share data into a shared analytical structure. Its purpose is to let every report view use consistent dimensions, measures, and benchmarks.

## Model snapshot

The model contains:

| Model object | Count |
| --- | ---: |
| Tables | 29 |
| Columns | 127 |
| Measures | 65 |
| Relationships | 28 |

These totals include business-facing tables and supporting structures used by the Power BI model. They should not be interpreted as 29 independent business entities.

## Design objective

The model is designed to support five connected analytical experiences:

- Executive performance monitoring
- Finance and dynamic P&L analysis
- Customer, product, and market sales analysis
- Marketing and profitability analysis
- Forecast Accuracy and inventory-risk analysis

Shared dimensions allow users to move between these views while retaining a consistent understanding of date, customer, product, and market context.

## Logical architecture

```text
                          ┌──────────────────┐
                          │  Shared dimensions│
                          │                  │
                          │  Date            │
                          │  Customer        │
                          │  Product         │
                          │  Market          │
                          └────────┬─────────┘
                                   │
                 ┌─────────────────┼─────────────────┐
                 │                 │                 │
                 ▼                 ▼                 ▼
        ┌────────────────┐ ┌────────────────┐ ┌────────────────┐
        │ Actuals and    │ │ Cost and       │ │ Targets and    │
        │ forecasts      │ │ profitability  │ │ market share   │
        └────────┬───────┘ └────────┬───────┘ └────────┬───────┘
                 │                  │                  │
                 └──────────────────┼──────────────────┘
                                    ▼
                         ┌────────────────────┐
                         │ Measures and       │
                         │ reporting logic    │
                         └─────────┬──────────┘
                                   ▼
                    Executive · Finance · Sales
                    Marketing · Supply Chain
```

The diagram summarizes how shared dimensions, analytical facts, supporting inputs, and measures work together.

## 1. Shared dimensions

The central dimensions provide reusable filter context across functional areas.

| Table | Analytical role | Representative attributes |
| --- | --- | --- |
| `dim_date` | Supports time filtering and period comparison | Calendar and reporting-period context |
| `fiscal_year` | Supports fiscal-year selection and reporting | Fiscal reporting context |
| `dim_customer` | Enables customer and commercial-channel analysis | Customer, market, platform, and channel |
| `dim_product` | Enables product-hierarchy analysis | Division, segment, category, product, and variant |
| `dim_market` | Enables geographic and market analysis | Market, sub-zone, and region |

### Why shared dimensions matter

- The same product definition can be used in Finance, Sales, Marketing, and Supply Chain.
- Customer and market selections can filter both actuals and forecasts.
- Time comparisons can be reused by last-year and target benchmark logic.
- Cross-functional navigation does not require separate copies of the same business hierarchy.

## 2. Actuals and forecasting

### `fact_actual_estimates`

This is the principal analytical fact structure for sales and profitability reporting. It contains the main financial chain, including:

- Sales quantities and values
- Sales deductions
- Net Sales
- Product-related costs
- Gross Margin
- Operating-expense inputs
- Profitability results used by the report

It supports Executive, Finance, Sales, and Marketing analysis through the shared dimensions.

### `fact_forecast_monthly`

This table provides the forecast quantities used by supply-chain analysis. In combination with actual sales, it supports:

- Net forecast error
- Absolute forecast error
- Absolute error percentage
- Forecast Accuracy
- OOS and EI risk classification

Actuals and forecasts are analyzed through common date, customer, and product context.

## 3. Cost and profitability inputs

Several supporting tables provide inputs required to move from sales to profitability.

| Table | Role in the analytical model |
| --- | --- |
| `manufacturing_cost` | Supplies manufacturing-cost inputs used in product profitability |
| `freight_cost` | Supplies freight-related cost inputs |
| `post_invoice_deductions` | Supports deductions applied after invoicing |
| `Operational_expenses` | Supplies advertising, promotion, and other operating-expense inputs |

These inputs are brought into the appropriate dimensional context so the measure layer can calculate margin and profit consistently.

### Profitability chain

```text
Gross Sales
    ↓
Pre-invoice and post-invoice deductions
    ↓
Net Sales
    ↓
Manufacturing, freight, and related product costs
    ↓
Gross Margin
    ↓
Advertising, promotions, and other operating expenses
    ↓
Net Profit
```

The operational-expense measure uses a negative sign convention. Consequently, adding operational expense to Gross Margin is equivalent to subtracting the expense when calculating Net Profit.

## 4. Targets and competitive analysis

### `NsGmTarget`

This table supports plan-versus-actual comparison for the target measures represented in the model, including Net Sales and Gross Margin reporting.

### `marketshare`

This table supports competitive-position analysis by providing the inputs required for Market Share reporting.

Together, these tables extend the model beyond historical reporting. Users can compare internal performance with targets and evaluate external competitive position within the represented market data.

## 5. Helper, selector, and reporting tables

The model also contains supporting tables used to control the report experience. Their roles include:

- Selecting last year or target as the comparison basis
- Structuring the dynamic P&L rows
- Supporting display and navigation logic
- Providing measure selectors or report toggles
- Enabling consistent ordering and labeling

These tables may not represent source-system business entities. They exist to make the semantic layer more usable and to keep interactive logic out of individual visuals where practical.

Power BI-generated date structures are not emphasized in the portfolio narrative because they do not demonstrate the business modeling decisions as clearly as the shared dimensions and analytical facts.

## Relationship strategy

The model contains 28 relationships. At a logical level:

- Actuals and forecasts are analyzed through shared date, customer, and product dimensions.
- Market attributes provide geographic and commercial context where applicable.
- Cost tables connect through the dimensions relevant to their grain.
- Target and market-share tables connect through the dimensions required by their reporting context.
- Helper and selector tables support reporting behavior rather than transactional analysis.

This design keeps filter behavior consistent across functional views and allows shared measures to respond to the same customer, product, market, and time context.

## Measure layer

The 65-measure layer can be understood in four groups.

### Base measures

Base measures aggregate core quantities and financial values required by downstream calculations.

### Derived financial measures

These measures implement the reporting path from sales through margin and profit, including deductions, costs, Gross Margin, operational expenses, and Net Profit.

### Forecasting measures

These measures compare actual and forecast quantities, calculate error magnitude, derive Forecast Accuracy, and classify OOS or EI risk.

### Dynamic reporting measures

These measures respond to report selections, including:

- Dynamic P&L row selection
- Last-year versus target benchmarking
- Percentage and value reporting within a shared layout
- Context-sensitive results across report views

Selected formulas are documented in [Analytical Logic Patterns](dax-highlights.md).

## How the model supports each view

| Report view | Primary model components |
| --- | --- |
| Executive | Shared dimensions, actuals, targets, market share, and summary measures |
| Finance | Actuals, deductions, cost inputs, operating expenses, targets, and dynamic P&L logic |
| Sales | Customer, product, market, actuals, and benchmark measures |
| Marketing | Product hierarchy, geography, actuals, profitability, and benchmark measures |
| Supply Chain | Actuals, monthly forecasts, shared dimensions, Forecast Accuracy, and risk measures |

[Return to the project README](../README.md)
