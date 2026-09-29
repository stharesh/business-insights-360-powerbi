# Business Overview

Business Insights 360 is a cross-functional Power BI solution designed to help decision-makers move from a company-level performance signal to the financial, commercial, or operational driver behind it.

This document describes the decisions supported by the report. It deliberately avoids presenting unverified business outcomes or invented recommendations before the dashboard evidence is published.

## Business objective

Finance, sales, marketing, and supply-chain teams often evaluate performance through different measures and reporting views. That separation can make it difficult to answer a broader question:

> What changed, where did it change, and which business function should investigate next?

Business Insights 360 addresses that problem through a shared KPI framework and connected functional views. Users can begin with an executive summary, identify an area requiring attention, and continue into the relevant analysis without changing the underlying business definitions.

## Intended users

| User group | Primary need |
| --- | --- |
| Executive leadership | Understand overall performance and prioritize deeper investigation |
| Finance | Trace revenue, deductions, costs, margins, and operating expenses through the P&L |
| Sales | Compare customer, product, and market contribution across revenue and profitability |
| Marketing | Identify segments and geographies producing profitable or unprofitable growth |
| Supply chain | Evaluate forecast quality and distinguish potential stock-out from excess-inventory risk |
| Analytics teams | Maintain consistent measures, benchmarks, and filter behavior across report views |

## Shared KPI framework

The report uses a common set of KPIs so users do not encounter conflicting definitions when moving between functional views.

| KPI | Business meaning | Typical decision use |
| --- | --- | --- |
| Net Sales | Revenue remaining after applicable sales deductions | Evaluate realized commercial performance |
| Gross Margin | Profitability remaining after product-related costs | Compare the quality of revenue across products, customers, and markets |
| Net Profit | Gross Margin after operating expenses | Assess the final profitability contribution represented in the model |
| Forecast Accuracy | One minus the absolute forecast-error percentage | Measure the magnitude of the forecast miss |
| Market Share | The company's share of the represented market | Compare competitive position across markets and periods |

Detailed calculation logic is documented in [Analytical Logic Patterns](dax-highlights.md). The model inventory will provide the complete measure definitions in a later phase.

## Executive view

The Executive view is the starting point for cross-functional investigation.

### Questions supported

- How are the principal financial and operational KPIs performing together?
- Which business area shows the strongest signal for further investigation?
- Is performance better understood through a prior-year or target comparison?
- Which market, customer, product, or business function should be examined next?

### Decision role

The view is intended to prioritize attention rather than replace the detailed functional analysis. A signal identified here should lead the user into Finance, Sales, Marketing, or Supply Chain with the same reporting context.

## Finance view

The Finance view explains how revenue progresses through the profitability chain.

### Questions supported

- Where is Gross Sales reduced through pre-invoice and post-invoice deductions?
- How do product-related costs affect Gross Margin?
- How do advertising, promotions, and other operating expenses affect Net Profit?
- How does the selected result compare with last year or target?
- Which market, customer, or product contributes to a favorable or unfavorable variance?

### Investigation path

```text
Gross Sales
    ↓
Sales deductions
    ↓
Net Sales
    ↓
Product-related costs
    ↓
Gross Margin
    ↓
Operating expenses
    ↓
Net Profit
```

The dynamic P&L measure keeps this reporting path in a consistent statement structure. Operational expenses are represented as negative values, so adding the expense measure to Gross Margin produces Net Profit.

## Sales view

The Sales view evaluates how customers, products, and markets contribute to commercial performance.

### Questions supported

- Which customers and products contribute most to Net Sales?
- Which markets combine strong sales with strong Gross Margin?
- Where does revenue contribution differ from profitability contribution?
- Which customer or product concentration deserves further investigation?
- How does performance compare with the selected benchmark?

### Decision role

The purpose is not only to rank entities by sales. It is to identify whether high-volume business also produces healthy margin and to surface cases where commercial scale and profitability tell different stories.

## Marketing view

The Marketing view evaluates performance through product hierarchy and geography.

### Questions supported

- Which divisions, segments, and categories generate profitable growth?
- Where is Net Sales strong but Gross Margin or Net Profit weaker?
- How does performance vary across regions, sub-zones, and markets?
- Which parts of the portfolio require a closer pricing, promotion, or mix investigation?
- How do actual results compare with last year or target?

### Decision role

The view helps distinguish growth in revenue from growth in profitable contribution. It supports portfolio and market investigation while leaving causal conclusions to evidence from the relevant product, pricing, and campaign context.

## Supply Chain view

The Supply Chain view connects forecast performance with potential inventory consequences.

### Questions supported

- How closely does forecast demand match actual sales?
- Where are the largest absolute forecast errors occurring?
- Which customer, product, or market combinations have weaker Forecast Accuracy?
- Does the direction of net error indicate potential Out-of-Stock or Excess Inventory exposure?
- Where should planning teams investigate the forecast assumptions further?

### Accuracy versus risk

These concepts are intentionally separated:

- **Forecast Accuracy** describes the magnitude of the forecast miss.
- **Risk classification** describes its direction: negative net error maps to OOS and positive net error maps to EI.

This distinction prevents a single accuracy percentage from hiding the operational consequence of the error.

## Dynamic analysis and benchmarking

The report uses a consistent benchmark selector rather than separate visuals for every comparison.

| Benchmark | Business question |
| --- | --- |
| Last year | How has performance changed over time? |
| Target | How is actual performance tracking against the plan? |

The selection is designed to apply to Net Sales, Gross Margin %, Net Profit %, and P&L reporting. This lets users change the comparison question while preserving the surrounding report context.

## Cross-functional investigation flow

```text
Executive signal
       ↓
Select KPI and benchmark
       ↓
Identify market, customer, product, or period
       ↓
Open the relevant functional view
       ↓
Trace the financial or operational driver
       ↓
Record the question requiring business follow-up
```

An example investigation might begin with a Net Sales variance in the Executive view, continue into Sales to identify the contributing customers and products, move to Finance to assess margin quality, and use Supply Chain to check whether forecast error may have affected availability. This is an analytical path, not a claim that one factor caused another.

## What the report supports—and what it does not

### Supported

- Consistent cross-functional KPI analysis
- Drill-down by shared business dimensions
- Prior-year and target comparisons
- Profitability-chain investigation
- Forecast-error magnitude and direction analysis
- Structured identification of follow-up questions

### Not claimed without further evidence

- Causal conclusions from dashboard correlations alone
- A quantified revenue, margin, or inventory improvement
- A measured performance gain without controlled before-and-after testing
- Complete data lineage before the source and model inventory is reviewed

## Current evidence boundary

This phase documents the decision framework supported by the approved report design. Dashboard screenshots and detailed business findings will be added only when they can be validated against the report. The Power BI file remains excluded while data-sharing and attribution requirements are reviewed.

[Return to the project README](../README.md)
