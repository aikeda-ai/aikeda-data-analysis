---
name: aikeda-data-analysis
description: Turn a dataset, workbook, database extract, or reference report into a repeatable end-to-end business analysis package with data-quality checks, metric definitions, multidimensional analysis, an adaptive interactive dashboard, and evidence-backed Feishu documents. Use when the user wants to reproduce the same analysis-and-delivery workflow on new data or a new business topic.
---

# Aikeda Data Analysis

Use this skill to produce a decision-ready analysis package from changing datasets or reference materials while preserving one consistent analytical and delivery standard.

Read [references/deliverable-contract.md](references/deliverable-contract.md) before starting. Apply only the sections relevant to the user's requested scope and destination.

## Operating principles

- Respect the requested stopping point. If the user asks only for a source dataset, quality check, chart, dashboard, or report, deliver that stage and do not continue automatically.
- Treat supplied reference files as guidance for business context, terminology, metric expectations, visual style, or document structure. Do not copy unsupported conclusions from them.
- Preserve source data. Perform cleaning and derived calculations in separate tables, queries, notebooks, or reproducible transformation steps.
- Establish data grain, date coverage, entity keys, filters, and snapshot boundary before calculating metrics.
- Separate observations, interpretation hypotheses, limitations, and recommended actions. Do not present temporal correlation as causation.
- Every important conclusion must be traceable to a metric, calculation, table, or chart. Visuals supplement the written evidence; they are not the only evidence.
- Keep output language, field labels, sheet names, report titles, and dashboard labels consistent with the user's chosen language.
- Use the user's requested publishing destination when available. Otherwise produce portable local files and provide clear paths.

## Inputs

Accept one or more of the following:

- Spreadsheet, CSV, Parquet, database extract, or connected data source.
- Reference report, metric dictionary, data dictionary, dashboard, or business brief.
- Business question, target audience, decision to support, reporting period, and desired dimensions.
- Output preferences such as spreadsheet, notebook, HTML dashboard, presentation, or Feishu document destination.

Infer routine details when the evidence is sufficient. Ask only when a missing choice would materially change the metric definition, analysis population, privacy treatment, or final destination.

If no dataset exists and the user explicitly requests demonstration data, create internally coherent data with realistic keys, dates, dimensions, events, and cross-table relationships. Record its provenance in the delivery notes. If the user asks to inspect the data before analysis, stop after generating and validating the data file.

## Workflow

### 1. Frame the analysis

Identify:

- The business process and primary decision.
- The reporting period and snapshot end date.
- The primary entities, events, and expected table grain.
- The target audience and level of detail.
- Required dimensions, filters, deliverable formats, and publishing destination.

Create a short analysis contract containing the question, population, period, dimensions, outputs, and known exclusions.

### 2. Profile and validate the data

Inventory every table or sheet, then check:

- Row and column counts, inferred types, date ranges, and key uniqueness.
- Missing values, exact and key-based duplicates, orphan relationships, invalid categories, impossible dates, and out-of-range values.
- Grain consistency across facts and dimensions.
- Records beyond the snapshot boundary and possible future-data leakage.
- Ratio anomalies that may reveal instrumentation or business-rule ambiguity.

Classify findings by severity and state whether each one blocks analysis, requires an adjustment, or only needs disclosure. Never silently repair ambiguous records.

### 3. Establish the metric contract

Before the main analysis, define every decision-relevant metric with:

- Business definition and formula.
- Numerator, denominator, unit, grain, and time window.
- Population, filters, cohort maturity rule, and null handling.
- Source table or system and refresh version.
- Known caveats and reconciliation rules.

For ratios, aggregate the numerator and denominator before dividing unless the business definition explicitly requires an average of ratios. Keep authoritative-source precedence explicit when systems disagree.

### 4. Perform the business analysis

Start with the overall trend and baseline, then drill down only where it helps explain the result. Typical dimensions include time, geography, product or plan, company size, acquisition channel, cohort, lifecycle stage, and customer segment.

For each important finding, use this sequence:

1. **Observation:** the measured result, with absolute values and rates where useful.
2. **Baseline or comparison:** prior period, long-term average, target, or relevant segment.
3. **Drill-down:** the dimensions that contribute most to the result, including counterexamples.
4. **Interpretation hypothesis:** a plausible explanation that remains clearly labeled as a hypothesis.
5. **Limitation:** data-quality, denominator, sample-size, comparability, or causal limits.
6. **Action condition:** what to test or monitor, who should act, and what success signal would justify the decision.

Do not force every available dimension into the report. Prefer the smallest set that materially explains the result.

### 5. Create editable visuals

Build charts from reusable data transformations or chart specifications rather than screenshots alone. Each chart must have a clear title, time period, unit, denominator where relevant, readable labels, and a written takeaway.

Inspect the rendered result. Fix overlapping text, indistinguishable colors, misleading scales, clipped labels, unreadable tables, and inappropriate chart types before delivery.

Export a clean image for report embedding while preserving the editable chart or chart specification as the source artifact.

### 6. Build the dashboard when requested

Create a reusable, polished data application rather than a collection of unrelated charts. Derive its information architecture from the business question, available metric families, decision workflow, dimensions, and actual findings. Do not reuse page names from a previous project unless the current data supports them.

By default, implement the dashboard as a componentized single-page data application, not as a static collection of precomputed charts. React with Vite is the recommended application shell for pages, reusable components, routing, shared filter state, and build output when the environment supports it, but it is not mandatory. Select ECharts, Recharts, or another mature chart library according to the data shape and required interactions. Using ECharts does not justify omitting shared state, filter-driven recalculation, page coordination, dynamic narrative, lineage access, interface states, or browser verification.

A static-hostable build is acceptable when it still behaves as the complete application described here. Unless the user explicitly requests a static presentation, a single HTML page containing precomputed charts, disconnected ECharts instances, or charts that do not share application state does not satisfy the dashboard deliverable.

The dashboard must contain:

- An overview page that communicates the current state, material changes, and the most decision-relevant KPIs.
- A small set of topic pages chosen from the current analysis. Group pages by the questions users need to answer, not by source-table names. A topic may concern demand, conversion, finance, retention, operations, supply, inventory, product behavior, service, risk, geography, portfolio, workforce, or another domain supported by the data.
- A data-quality and lineage page covering readiness, issues, metric definitions, table coverage, and authoritative sources.

Each analytical page should use only the regions it needs, selected from:

- Page purpose and dynamic narrative.
- Global filters and visible filter state.
- KPI or summary strip with comparisons and compact trends.
- Primary trend, distribution, relationship, flow, or composition view.
- Dimension drill-down and detailed table.
- Definitions, denominators, caveats, and source access.

Provide global filters only for dimensions that materially change the analysis. Recalculate totals, numerators, denominators, comparisons, and narrative text after filtering. Preserve page and filter state in the URL when the chosen implementation supports it.

Define and implement the relevant interface states instead of styling only the default state:

- Initial loading and skeleton state.
- Ready and unfiltered state.
- Filtered state with visible active filters and clear-all control.
- Hover, selected, isolated-series, sorted, and searched states where relevant.
- Empty-filter result and genuinely missing-data states, with different explanations.
- Data-quality warning and metric-unavailable states.
- Recoverable error state.
- Narrow-screen or horizontally scrollable state for dense tables and cohort-style matrices.
- Export state that produces a complete, uncropped image or data file.

Make chart definitions and data sources discoverable from the interface. Important charts should support precise tooltips, legend toggles, readable units, data inspection or copying, and clean image export. Tables should support the subset of sorting, search, pagination, sticky headers, and horizontal scrolling required by their size.

Use a consistent design system: restrained neutral background, one primary accent, semantic success/warning/risk colors, clear typography hierarchy, light card boundaries, consistent spacing, and stable number formats. Keep the same metric or segment color consistent across pages. Do not use decorative effects that obscure magnitude.

Preserve editable source code or chart specifications and produce a built HTML artifact. Start the dashboard when the environment permits, then inspect every page and relevant state in a real browser. Fix label overlap, indistinguishable colors, misleading scales, clipped content, identical in-cell bars for different values, unreadable heatmaps, broken filters, empty-state failures, export cropping, and console errors before completion.

### 7. Produce the reports

Unless the user requests a different structure, publish two separate Feishu documents:

1. **Data quality and metric definitions:** analysis readiness, issues and treatments, data grain and coverage, metric formulas, source lineage, refresh gates, and limitations.
2. **Business analysis:** management summary, headline metrics, evidence-backed drill-downs, hypotheses and limitations, prioritized actions, validation plans, and methodology.

Do not create Markdown analysis reports. Use a Feishu document connector, CLI, API, or authorized interface to create the final documents directly. If Feishu publishing is unavailable, report the missing capability as a blocker; do not silently substitute a Markdown file.

Insert the corresponding dashboard chart image near the conclusion it supports. Use local image uploads or another Feishu-supported image mechanism rather than fragile local file links. Every visual must also have a textual equivalent stating the relevant values and interpretation.

After creation, fetch or read each Feishu document back. Confirm that the title, section hierarchy, tables, images, captions, and final links exist in the published document. Creating a local draft or receiving an upload attempt is not completion.

### 8. Validate and hand off

Before declaring completion:

- Recalculate headline metrics independently or reconcile them to source totals.
- Confirm all quality treatments were applied consistently.
- Check that report values, dashboard values, and chart labels match.
- Verify every image, attachment, file path, and document link.
- Read each created Feishu document back and confirm that text, tables, captions, and images exist at the final destination.
- Provide a delivery manifest listing the source, transformations, editable artifacts, dashboard, reports, snapshot date, and unresolved limitations.

## Completion standard

The workflow is complete only when the requested artifacts are usable, internally consistent, traceable to source data, visually readable, and verified at their final destination. An attempted export or upload is not completion.
