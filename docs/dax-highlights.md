# Analytical Logic Patterns

This document highlights the DAX patterns that carry the most analytical value in Business Insights 360. The focus is not on basic aggregation measures; it is on logic that changes how users interpret profitability, forecasting, risk, and benchmarks.

## 1. Dynamic P&L reporting

The financial statement uses a dynamic `SWITCH(TRUE())` pattern so one reporting measure can return the appropriate result for the selected P&L row. The logic supports the reporting path from Gross Sales through Net Profit and Net Profit %.

This pattern separates the presentation structure from the underlying calculations:

```text
Selected P&L row
        ↓
Dynamic reporting measure
        ↓
Relevant financial measure
        ↓
Gross Sales → Net Sales → Gross Margin → Net Profit
```

### Why it matters

- Maintains a consistent P&L layout without creating a separate visual for every metric.
- Allows currency values and percentage metrics to coexist in the same reporting structure.
- Makes benchmark logic reusable across the financial statement.
- Reduces repeated visual-level configuration and keeps business logic inside the semantic model.

## 2. Expense sign convention and Net Profit

These measures must be interpreted together:

```DAX
Operational Expense $ =
([Ads & Promotions] + [Other Operational Expense]) * -1

Net Profit =
[GM $] + [Operational Expense $]
```

Operational expenses are deliberately stored as a negative reporting value. Adding the `Operational Expense $` measure to Gross Margin is therefore mathematically equivalent to subtracting operating expenses from Gross Margin.

For example:

```text
Gross Margin             100
Operational Expense      -30
Net Profit                70
```

### Why it matters

Showing the sign convention beside the Net Profit formula prevents readers from incorrectly concluding that expenses are being added to profit. It also keeps expense presentation consistent within the P&L.

## 3. Forecast Accuracy

Forecast Accuracy is derived from the absolute forecast error:

```DAX
ABS Error % =
DIVIDE([ABS Error], [Forecast quantity], 0)

Forecast Accuracy % =
IF(
    [ABS Error %] <> BLANK(),
    1 - [ABS Error %],
    BLANK()
)
```

`ABS Error %` expresses the magnitude of the miss relative to forecast quantity. `Forecast Accuracy %` then converts that error ratio into an accuracy measure.

The `DIVIDE` function provides controlled zero-denominator handling, while the outer `IF` avoids returning a displayed accuracy when the error percentage is blank.

### Interpretation

- A smaller absolute error percentage produces higher Forecast Accuracy.
- Accuracy measures the **magnitude** of the forecast miss.
- Accuracy alone does not indicate whether demand was under-forecast or over-forecast.

That directional interpretation is handled separately by the risk classification.

## 4. Out-of-Stock and Excess Inventory risk

```DAX
Risk =
IF(
    [Net error] < 0,
    "OOS",
    IF([Net error] > 0, "EI", BLANK())
)
```

The measure classifies the direction of the forecast miss:

| Net error | Classification | Business interpretation |
| --- | --- | --- |
| Less than zero | OOS | Potential Out-of-Stock exposure |
| Greater than zero | EI | Potential Excess Inventory exposure |
| Equal to zero or blank | Blank | No directional risk classification |

Forecast Accuracy and Risk answer different questions:

- **Forecast Accuracy:** How large was the miss?
- **Risk:** In which direction did the miss occur?

Keeping these concepts separate gives supply-chain users both a performance metric and an operational signal.

## 5. Dynamic benchmarking

The model allows users to switch the comparison basis between last year and target. The same benchmark choice is applied consistently across:

- Net Sales
- Gross Margin %
- Net Profit %
- P&L reporting

This design is more useful than hard-coding separate comparison visuals because the user can keep the same analytical context while changing the business question:

| Benchmark | Question answered |
| --- | --- |
| Last year | How has performance changed over time? |
| Target | How is actual performance tracking against the plan? |

## Pattern summary

| Pattern | Analytical value |
| --- | --- |
| Dynamic P&L | Maps a reporting row to the correct financial result |
| Expense sign convention | Preserves financial statement presentation and correct Net Profit arithmetic |
| Forecast Accuracy | Quantifies the magnitude of forecast error |
| OOS/EI risk | Identifies the direction and likely operational consequence of forecast error |
| Dynamic benchmarking | Reuses one comparison framework for last-year and target analysis |

## Design principles

- Centralize reusable business logic in measures instead of individual visuals.
- Keep financial sign conventions explicit and consistent throughout the P&L.
- Separate forecast-error magnitude from operational-risk direction.
- Apply a shared benchmark context across Net Sales, Gross Margin, Net Profit, and P&L reporting.
- Preserve filter context so the same measures work across executive and functional views.

[Return to the project README](../README.md)
