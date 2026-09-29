# Model Inventory

This inventory records the semantic-model objects that were confirmed during the Business Insights 360 review. It distinguishes exact names from logical descriptions so that missing metadata is not reconstructed or guessed.

## Coverage summary

| Model object | Confirmed total | Documented here |
| --- | ---: | --- |
| Tables | 29 | Confirmed named business tables plus supporting-table categories |
| Columns | 127 | Confirmed business attributes and calculation inputs; exact field export pending |
| Measures | 65 | Confirmed analytical measures and measure families; full expression export pending |
| Relationships | 28 | Confirmed logical relationship paths; exact properties pending |

## Inventory confidence levels

| Level | Meaning |
| --- | --- |
| Confirmed name | The object name appeared in the approved model review |
| Confirmed role | The object's analytical purpose was verified, but every field was not exported |
| Pending metadata | Exact name, expression, grain, key, or relationship property requires direct model export |

## Confirmed named tables

### Shared dimensions

| Table | Confirmed role | Confirmed representative attributes |
| --- | --- | --- |
| `dim_date` | Shared time context | Calendar and reporting-period attributes |
| `fiscal_year` | Fiscal reporting context | Fiscal-year selection and grouping |
| `dim_customer` | Customer and commercial hierarchy | Market, platform, and channel |
| `dim_product` | Product hierarchy | Division, segment, category, product, and variant |
| `dim_market` | Geographic hierarchy | Market, sub-zone, and region |

### Actuals and forecasting

| Table | Confirmed role | Confirmed analytical content |
| --- | --- | --- |
| `fact_actual_estimates` | Main sales and profitability fact structure | Sales, deductions, costs, Gross Margin, and operating-expense inputs |
| `fact_forecast_monthly` | Monthly forecast fact | Forecast quantities used with actual sales for error and accuracy analysis |

### Cost and profitability inputs

| Table | Confirmed role |
| --- | --- |
| `manufacturing_cost` | Manufacturing-cost input by its applicable product and time context |
| `freight_cost` | Freight-cost input by its applicable reporting context |
| `post_invoice_deductions` | Post-invoice deduction input |
| `Operational_expenses` | Advertising, promotion, and other operating-expense input |

### Targets and competitive analysis

| Table | Confirmed role |
| --- | --- |
| `NsGmTarget` | Target inputs supporting Net Sales and Gross Margin comparisons |
| `marketshare` | Inputs supporting competitive Market Share analysis |

## Supporting table categories

The 29-table total also includes model-support structures. Their exact names will be listed only after direct metadata validation.

| Category | Model role | Publication treatment |
| --- | --- | --- |
| Benchmark selectors | Switch comparison context between last year and target | Document the behavior; validate exact table and field names |
| P&L structure | Provide financial-statement rows, order, and display logic | Document with the dynamic P&L measure |
| Toggle and parameter tables | Control interactive report behavior | Include only selectors that add analytical value |
| Navigation or display helpers | Support labels, ordering, or navigation | Keep separate from source-system business entities |
| Power BI-generated date structures | Support automatic date behavior where present | Record in the technical export but de-emphasize in the portfolio story |

The gap between the 13 confirmed named tables above and the 29-table model total is intentionally not filled with inferred names.

## Confirmed measure inventory

### Profitability measures

| Measure | Confirmed logic or role |
| --- | --- |
| `[GM $]` | Gross Margin value used in profitability reporting |
| `[Ads & Promotions]` | Advertising and promotion expense input |
| `[Other Operational Expense]` | Other operating-expense input |
| `[Operational Expense $]` | Adds the two operating-expense components and multiplies the result by `-1` |
| `[Net Profit]` | Adds the negative Operational Expense value to Gross Margin |

Confirmed expressions:

```DAX
Operational Expense $ =
([Ads & Promotions] + [Other Operational Expense]) * -1

Net Profit =
[GM $] + [Operational Expense $]
```

### Forecasting measures

| Measure | Confirmed logic or role |
| --- | --- |
| `[Forecast quantity]` | Forecast quantity denominator used by error analysis |
| `[ABS Error]` | Absolute magnitude of the forecast error |
| `[ABS Error %]` | Absolute error divided by Forecast quantity |
| `[Forecast Accuracy %]` | One minus ABS Error % when the error percentage is not blank |
| `[Net error]` | Directional forecast error used by risk classification |
| `[Risk]` | Returns `OOS` for negative Net error and `EI` for positive Net error |

Confirmed expressions:

```DAX
ABS Error % =
DIVIDE([ABS Error], [Forecast quantity], 0)

Forecast Accuracy % =
IF(
    [ABS Error %] <> BLANK(),
    1 - [ABS Error %],
    BLANK()
)

Risk =
IF(
    [Net error] < 0,
    "OOS",
    IF([Net error] > 0, "EI", BLANK())
)
```

### Confirmed measure families

The approved review also confirmed the following analytical families, although the complete production expressions are not reproduced without a direct model export:

- Gross Sales and deduction measures
- Net Sales and Net Sales percentage or variance measures
- Gross Margin and Gross Margin %
- Net Profit and Net Profit %
- Market Share
- Last-year comparison measures
- Target comparison measures
- Dynamic P&L reporting through `SWITCH(TRUE())`
- Benchmark-switching logic used by Net Sales, Gross Margin %, Net Profit %, and P&L reporting

## Confirmed logical relationships

The model contains 28 relationships. The confirmed analytical paths are:

| From | To | Analytical purpose |
| --- | --- | --- |
| Date context | Actuals | Analyze realized performance over time |
| Date context | Forecasts | Analyze forecast quantities over time |
| Customer | Actuals | Analyze sales and profitability by customer and commercial hierarchy |
| Customer | Forecasts | Analyze forecast performance by customer |
| Product | Actuals | Analyze sales and profitability by product hierarchy |
| Product | Forecasts | Analyze forecast performance by product |
| Market context | Relevant facts | Analyze geography and market performance |
| Cost inputs | Relevant dimensions or facts | Apply manufacturing, freight, and deduction inputs at their modeled grain |
| Target inputs | Relevant dimensions | Compare actual results with plan |
| Market-share inputs | Relevant dimensions | Analyze competitive position in the represented market context |

The following relationship properties remain pending direct export:

- Exact key columns
- Cardinality
- Cross-filter direction
- Active or inactive state
- Referential-integrity assumptions
- Any many-to-many or bridge-table implementation

## Business-area mapping

| Business area | Dimensions | Facts and inputs | Measure families |
| --- | --- | --- | --- |
| Executive | Date, customer, product, market | Actuals, targets, market share | KPI summaries and benchmarks |
| Finance | Date, customer, product, market | Actuals, deductions, manufacturing cost, freight cost, operating expenses, targets | P&L, margin, profit, and variance |
| Sales | Date, customer, product, market | Actuals and targets | Net Sales, contribution, margin, and benchmark measures |
| Marketing | Date, product, market | Actuals, targets, market share | Segment profitability and competitive measures |
| Supply Chain | Date, customer, product | Actuals and forecasts | Error, accuracy, OOS, and EI measures |

## Metadata required for the final field-level export

To convert this reviewed inventory into a complete technical appendix, export or capture the following directly from Power BI, Tabular Editor, DAX Studio, or another model metadata tool:

1. All table names and hidden states
2. All columns, data types, source columns, and formatting
3. All measures, DAX expressions, formats, home tables, and display folders
4. All relationships, keys, cardinalities, directions, and active states
5. Table and column descriptions
6. Calculation groups, field parameters, or role-playing date structures if present
7. Row-level security roles if present

## Validation checklist

- [ ] Reconcile the 29-table total with a direct metadata export.
- [ ] Reconcile the 127-column total with the exported field list.
- [ ] Reconcile the 65-measure total with the exported measure list.
- [ ] Reconcile the 28 relationships with the relationship diagram or metadata export.
- [ ] Confirm exact casing for every object name.
- [ ] Confirm fact-table grain before publishing field-level descriptions.
- [ ] Confirm all DAX expressions against the production model.
- [ ] Remove Power BI-generated objects from the recruiter-facing summary where they add no portfolio value.
- [ ] Check that no confidential connection strings or source credentials are included.

## Evidence boundary

This inventory is complete for the model facts available in the approved review. It is not represented as a full metadata export. Unknown object names and relationship properties are explicitly left pending rather than inferred.

[Return to the project README](../README.md)
