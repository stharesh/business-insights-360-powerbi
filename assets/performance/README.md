# Performance Evidence

Add the validated diagnostic captures using these exact filenames:

```text
performance-analyzer.png
dax-studio-query-analysis.png
```

## `performance-analyzer.png`

The capture should show the selected visual and its timing breakdown. The currently documented observation is approximately 2.69 seconds total and 1.25 seconds for the DAX query; verify the screenshot before publication.

## `dax-studio-query-analysis.png`

The capture should show the relevant DAX Studio investigation, such as Server Timings and the Physical or Logical Query Plan. It should support the diagnostic story without implying a measured improvement that has not been benchmarked.

If a before-and-after result is later published, capture both test states under comparable conditions and document the model version, filters, cache state, and number of runs.
