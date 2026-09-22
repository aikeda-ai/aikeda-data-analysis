# Deliverable Contract

Use this reference to decide what to create and how to verify it. Deliver only the items within the user's requested scope.

## 1. Analysis contract

Record:

| Field | Required content |
|---|---|
| Business question | The decision or uncertainty the analysis should address |
| Audience | People who will read or act on the result |
| Population | Included entities, accounts, users, orders, or events |
| Reporting period | Start, end, and snapshot boundary |
| Primary grain | One row represents what |
| Dimensions | Time, region, segment, product, channel, cohort, or other relevant cuts |
| Deliverables | Data file, notebook, charts, dashboard, Feishu documents, or other requested artifacts |
| Exclusions | Known out-of-scope populations or unavailable evidence |

## 2. Data-quality report

Minimum sections:

1. Readiness conclusion: usable, usable with conditions, or blocked.
2. Table inventory: table name, grain, key, rows, columns, date coverage, and refresh version.
3. Finding register: identifier, severity, category, issue, count and rate, affected metrics, treatment, and owner or next check.
4. Relationship tests: orphan keys and duplicate fact grains.
5. Snapshot tests: future records and mismatched reporting windows.
6. Analysis gates: checks that must pass before the next refresh is published.

Severity guidance:

- **Blocking:** changes the population or invalidates a headline metric and cannot be resolved safely.
- **High:** likely changes a decision-relevant conclusion.
- **Medium:** affects a segment, supporting metric, or limited set of rows.
- **Low:** small coverage gap with a documented calculation rule.
- **Passed:** checked and no issue found.

Do not use the raw count alone to assign severity. Consider business impact, direction of bias, affected population, and whether the issue can be isolated.

## 3. Metric dictionary

Each metric row should include:

| Field | Meaning |
|---|---|
| Metric name | Stable business-facing label |
| Business definition | What the metric represents |
| Formula | Reproducible calculation |
| Numerator | Count or amount above the line |
| Denominator | Eligible population below the line |
| Unit | Currency, count, percentage, hours, or another unit |
| Grain | Account-month, event, order, user-day, or another grain |
| Time window | Calendar month, rolling window, maturity window, or point-in-time |
| Filters | Status, eligibility, exclusion, and null handling |
| Dimensions | Valid segmentation fields |
| Source | Authoritative table or system |
| Caveats | Comparability, coverage, anomaly, or causal limitations |
| Version | Effective date and revision status |

For cohort metrics, state the cohort-entry event, maturity rule, observation window, and denominator explicitly.

## 4. Feishu business analysis document

Recommended order:

1. Decision-oriented title with subject and time point.
2. Management summary with three to six evidence-backed conclusions.
3. Headline KPI baseline.
4. Trend and change decomposition.
5. Revenue, volume, or outcome structure.
6. Funnel, retention, lifecycle, or cohort analysis as relevant.
7. Product, operational, service, risk, or quality drivers as relevant.
8. Prioritized actions with validation conditions.
9. Method, metric definitions, source version, and limitations.

Every major section should answer:

- What happened?
- Compared with what?
- Which dimensions explain the result?
- What evidence contradicts or limits the simple story?
- What can be concluded now?
- What still requires testing?
- What action is justified, and under what condition?

Avoid causal verbs such as “caused,” “drove,” or “resulted in” unless the evidence supports causal identification. Use “coincided with,” “is consistent with,” or “supports the hypothesis” for descriptive evidence.

Publish the report as a Feishu document, not as a Markdown file. Use native headings, callouts, tables, lists, images, captions, and links so the document remains readable without a local workspace. Upload images into Feishu; do not embed local filesystem paths as the final image source.

## 5. Charts

For every chart:

- Preserve an editable source or reusable chart specification.
- State the metric, unit, population, time period, and source.
- Use consistent colors for the same metric or segment across the package.
- Keep labels legible at report width; abbreviate large values consistently.
- Show the denominator or base when a percentage may be misleading.
- Do not use decorative effects that obscure magnitude.
- For heatmaps, ensure color contrast distinguishes values and labels do not overlap.
- For tables with in-cell bars or sparklines, ensure the encoded values vary visibly or use plain numbers instead.
- Export a clean PNG or equivalent image after visual inspection.

## 6. Dashboard

### 6.1 Derive the page map

Do not begin from a fixed list of industry-specific pages. Build the page map from:

- The decisions the audience needs to make.
- The available metric families and valid dimensions.
- The natural sequence from overall result to contributing factors.
- The three to six findings that require explanation.
- The amount of information that can fit without turning a page into a chart gallery.

Always include an overview and a quality/lineage page. Add only the topic pages supported by the current data. Name each page after the question or business subject it answers. Avoid source-table names and do not carry over page names from another analysis by default.

Before implementation, create a compact page blueprint containing:

| Page | Decision question | KPIs | Primary evidence | Drill-down dimensions | Filters | Required states |
|---|---|---|---|---|---|---|
| Overview | What is the current state and material change? | Current values and comparisons | Primary trend and structure | Main contributors | Global dimensions | Loading, ready, filtered, empty |
| Dynamic topic page | What explains a specific result? | Topic-specific | Best-matched chart or table | Only explanatory dimensions | Relevant subset | Selection, sorting, no-result |
| Quality and lineage | Can the result be trusted and reproduced? | Readiness and issue counts | Finding register and table profile | Source and metric | Usually no business filter | Warning, passed, unavailable |

The rows above describe roles, not mandatory page titles.

### 6.2 Page regions

Select the regions that support each page's question:

1. **Application header:** dashboard title, snapshot date, refresh status, and global actions.
2. **Page navigation:** short, stable, and ordered according to the analytical story.
3. **Global filter bar:** active filters, clear-all, and appropriate defaults.
4. **Context header:** the question answered by the page and a short dynamic summary.
5. **KPI strip:** current value, comparison, direction, and compact trend when useful.
6. **Primary evidence area:** the strongest trend, distribution, composition, relationship, flow, matrix, map, or table.
7. **Drill-down area:** segments, contributors, exceptions, and detailed rows.
8. **Interpretation and caveat area:** observation, comparison, limitation, and next test.
9. **Definitions and source access:** formula, denominator, timestamp, and authoritative source.

Do not include every region on every page. A page is complete when it answers its decision question clearly, not when it contains a fixed number of cards.

### 6.3 KPI and narrative behavior

Each KPI card should include the current value and enough context to interpret it: a prior-period difference, target difference, baseline, rank, or sparkline. Do not show a change percentage when no valid comparison exists.

Dynamic narrative text must update with the filters. It should state the strongest observable result, the relevant comparison, the leading contributor, and an important limitation. Do not leave an all-data conclusion visible after the user filters to a segment.

### 6.4 Filters and state

- Use only dimensions that change multiple components or support a real decision.
- Recalculate both numerator and denominator under filters.
- Display active filters and provide clear-all.
- Keep incompatible controls disabled or explain why they do not apply.
- Preserve page and filter state in the URL when practical.
- Distinguish a valid zero from no records, unavailable fields, and an immature cohort.
- Provide separate states for loading, ready, filtered, selected, empty-result, missing-data, warning, recoverable error, and export.
- For dense tables or matrices, use responsive width, horizontal scrolling, sticky headers, or a condensed narrow-screen layout.

### 6.5 Chart and table interaction

Important charts should support the relevant subset of:

- Precise tooltips with formatted values and denominator or base.
- Legend toggling and series isolation.
- Selection, highlighting, or cross-filtering when it improves investigation.
- Metric definition and source access.
- Data inspection or copying.
- Clean PNG export without clipped legends, titles, or labels.

Tables should support the relevant subset of sorting, search, pagination, sticky headers, copy, and horizontal scrolling. In-cell bars and sparklines must encode real differences; if the variation is not legible, use formatted numbers instead.

### 6.6 Visual system

- Use a restrained neutral surface with one primary accent and semantic success, warning, and risk colors.
- Maintain clear title, section, card, label, and annotation hierarchy.
- Use consistent spacing, card radius, borders, and number formatting.
- Keep a metric or segment color stable across pages.
- Prefer readable two-dimensional charts to decorative 3D, heavy gradients, or effects that obscure magnitude.
- Limit simultaneous series; use filtering, small multiples, or ranking when categories are numerous.
- Make heatmap values and color steps distinguishable, prevent label overlap, and expose the sample base.
- Ensure color is not the only carrier of meaning.

### 6.7 Implementation and deliverables

The default implementation is a componentized single-page data application with shared runtime state. React with Vite is the preferred application shell when available because it provides a clear component, routing, state-management, and build structure; an equivalent component framework is acceptable. This recommendation does not require one chart library. Choose ECharts for interaction-rich, high-density, heatmap, large-series, or specialized visualization needs; choose Recharts or another mature library when it better fits the component model and chart requirements.

The chart engine is only the rendering layer. Regardless of library, the application must retain shared filters, filter-driven metric recalculation, coordinated page state, dynamic narrative, definitions and lineage, loading and exception states, export behavior, and browser verification. Do not accept “ECharts supports interaction” as evidence that those application behaviors exist; test them directly.

A build that can be hosted as static files is valid if it runs as the full application. Unless the user explicitly asks for a static presentation, the following are not sufficient:

- One HTML file containing only precomputed charts and fixed narrative.
- Multiple chart instances that do not share filter or selection state.
- Filters that hide marks visually without recalculating KPI numerators and denominators.
- Chart screenshots or exported images presented as the dashboard itself.
- An ECharts option collection without page architecture, application state, data lineage, or verified user flows.

Preserve componentized source code, reusable data transformations, and editable chart specifications. Produce a built HTML artifact with local or bundled dependencies rather than fragile external resources. Provide a clear start command and, when possible, launch a local service and return a clickable URL.

The dashboard delivery should identify:

- Source-code folder.
- Built HTML entry point.
- Data preparation layer.
- Page and filter map.
- Chart specification or editable configuration.
- Exported evidence-image folder.
- Runtime URL and start command.

### 6.8 Browser verification

Open the built dashboard in a real browser and inspect:

- Every page used in the analysis.
- Default, filtered, clear-all, single-segment, empty-result, and missing-data states.
- Relevant hover, legend, selection, search, sorting, scrolling, and export behavior.
- Desktop and narrow-width layout for dense content.
- Label overlap, clipped content, indistinguishable colors, misleading scales, number formats, and percentage denominators.
- Agreement between card values, chart tooltips, exported images, source totals, and Feishu document text.
- Browser console errors that affect use.

Fix observed defects and repeat the affected checks. Source code that has not been rendered and visually inspected does not satisfy this contract.

## 7. Feishu document publishing and image placement

Place a dashboard image immediately after the paragraph containing the conclusion it supports. Add a caption that names the dashboard view and metric. Follow the image with a textual equivalent if the precise values are not already in the preceding paragraph.

Do not insert a screenshot merely because it exists. Use it only when it improves verification or comprehension.

Create two separate Feishu documents unless the user requests a different grouping:

1. Data quality and metric definitions.
2. Business analysis with evidence-backed drill-downs.

Do not create Markdown analysis reports. If the environment cannot publish to Feishu, state that the report deliverable is blocked and identify the missing connector, authorization, or capability. Do not present a local Markdown draft as the completed report.

Upload evidence images to Feishu using a supported local-image or media-upload mechanism. After creation, fetch or read each document back and verify its title, sections, tables, images, captions, and link. Broken local image references are a failed delivery.

## 8. Output manifest

At handoff, list:

| Artifact | What to identify |
|---|---|
| Source data | File, connection, sheet or table names, and snapshot date |
| Transformation | Notebook, query, script, or calculation layer |
| Quality report | Feishu document link |
| Metric dictionary | Location and version |
| Editable visuals | Workbook, chart specification, or dashboard source |
| Dashboard | Local file, hosted URL, and filters |
| Business report | Feishu document link |
| Evidence images | Folder or embedded report locations |
| Open issues | Unresolved quality or interpretation limits |

## 9. Final verification checklist

- Headline metrics reconcile to source totals.
- Percentage denominators and cohort maturity are documented.
- Date boundaries and currency units are consistent.
- Segment totals reconcile to the overall total, allowing for documented exclusions.
- Quality issues have explicit treatments and are reflected in every artifact.
- Charts are readable and their images match the latest dashboard state.
- Unless explicitly requested otherwise, the dashboard is a componentized application rather than a disconnected static chart collection.
- Both Feishu documents have been read back after creation, including image and table presence.
- No Markdown analysis report was created as a final deliverable.
- All paths and links open successfully.
- Temporary workspaces are cleaned without removing source data or final deliverables.
