# Performance Analysis and Optimization

This document explains how report performance is measured, investigated, and retested in Business Insights 360, from visual-level timing through DAX query-plan analysis.

## Objective

The performance workflow answers five practical questions:

1. Which visual is contributing most to page-render time?
2. How much time is associated with its DAX query?
3. What does the query plan reveal about execution?
4. Which model, measure, or visual change should be tested?
5. Did the same controlled test produce a measurable improvement?

## Performance baseline

Power BI Performance Analyzer was used to profile a selected table visual. The available capture records approximately:

| Measurement | Observed time |
| --- | ---: |
| Total visual duration | 2.69 seconds |
| DAX query duration | 1.25 seconds |

The remaining duration was distributed across visual display and other Power BI processing. The timing breakdown identifies the selected table visual as a focused optimization target.

## Diagnostic workflow

```text
Measure the report page
          ↓
Identify the expensive visual
          ↓
Copy the generated DAX query
          ↓
Inspect execution in DAX Studio
          ↓
Form and implement one optimization hypothesis
          ↓
Repeat the same controlled test
          ↓
Compare results and document the outcome
```

## Step 1 — Profile the page in Power BI

Power BI Performance Analyzer is the first diagnostic layer because it measures performance at the visual level.

### Procedure

1. Open the report page being tested.
2. Start recording in Performance Analyzer.
3. Refresh the visuals under the intended filter context.
4. Compare total duration and DAX query duration across visuals.
5. Select the visual that warrants deeper investigation.

### What this establishes

- Whether the delay is concentrated in one visual or distributed across the page.
- How much of the visual duration is associated with DAX execution.
- Whether visual rendering and other processing also require attention.

Performance Analyzer identifies **where to investigate**. It does not, by itself, explain why the generated query is expensive.

## Step 2 — Extract the generated query

The DAX query generated for the selected visual is copied from Performance Analyzer. This preserves the visual's actual fields, measures, filters, grouping, and sort behavior.

Using the generated query is preferable to testing an unrelated handwritten query because it keeps the investigation tied to the real report experience.

The following context should be recorded alongside the query:

- Report page and visual name
- Active slicers and filters
- Selected benchmark state
- Power BI Desktop version
- Test timestamp
- Whether the cache was cold or warm

## Step 3 — Investigate in DAX Studio

The copied query is evaluated in DAX Studio using three complementary views.

### Server Timings

Server Timings helps distinguish work performed by the Storage Engine from work performed by the Formula Engine. It can reveal whether the query is dominated by data retrieval or by measure evaluation and intermediate calculations.

### Physical Query Plan

The Physical Query Plan shows the operations used to execute the query. It is useful for identifying expensive scans, materialized intermediate results, repeated work, and operations that deserve closer inspection.

### Logical Query Plan

The Logical Query Plan describes the analytical operations requested before physical execution. Reviewing it helps connect the visual's requested groupings and measures to the resulting execution strategy.

Together, these views connect the report visual to the analytical and physical work performed by the engine.

## Step 4 — Identify optimization opportunities

The query plan guides targeted checks across the measure, model, and visual design:

- Repeated or unnecessarily complex measure evaluation
- Iterators operating over a larger table than required
- Filter context that can be simplified
- Relationships that create unexpected propagation or ambiguity
- High-cardinality columns used in a visual
- Excessive grouping or too many displayed rows
- Calculations performed at query time that could be modeled more efficiently
- Visual design that requests more detail than the decision requires

Each change is isolated so its impact can be measured during retesting.

## Step 5 — Retest under controlled conditions

A meaningful comparison requires the test conditions to remain consistent.

| Control | Why it matters |
| --- | --- |
| Same report page and visual | Prevents comparing different workloads |
| Same slicers and filters | Preserves the same filter context |
| Same data and model version | Avoids volume or schema differences |
| Same cache condition | Prevents cold-cache and warm-cache distortion |
| Multiple test runs | Reduces the influence of one-off variation |
| Median or representative duration | Avoids selecting only the best result |

The optimized version is measured again in Performance Analyzer, with the generated query checked in DAX Studio when deeper analysis is useful.

## Performance engineering capabilities

This workflow demonstrates the ability to move beyond report construction into performance engineering:

- Measure performance at the visual level.
- Connect the visual to its generated DAX query.
- Inspect execution behavior in DAX Studio.
- Target model, measure, or visual changes based on the query plan.
- Retest consistently under controlled conditions.

[Return to the project README](../README.md)
