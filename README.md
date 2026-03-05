# Campaign Status Dashboard — FullSpeed Automotive

A single-file, client-side analytics dashboard for visualizing campaign workflow data exported from Monday.com. Designed for marketing leadership to analyze time-in-status, identify bottlenecks, and detect rework loops across creative campaigns.

---

## Features

- **Dataset Library** — Upload and save multiple Monday.com CSV exports; switch between them from a landing page. Datasets are persisted in `localStorage`.
- **KPI Overview** — At-a-glance cards for total items analyzed, average time in top status, rework rate, and more. Each KPI is clickable and opens a drilldown panel.
- **Status Time Analysis** — Horizontal bar charts showing average hours per workflow status, sortable by total time or item count.
- **Bottleneck Detection** — Automatically surfaces the statuses accumulating the most total time, with per-item drilldowns.
- **Rework Detection** — Identifies items that re-entered a previously held status (revision loops), with a dedicated banner and transition history per item.
- **Group & Month Breakdowns** — Charts segmented by creative group (e.g. Creative Queue, Creative Production, Sandbox) and by month.
- **Status Transition Map** — Visualizes how often items move between specific statuses.
- **Items Table** — Filterable and sortable table of all campaign items, with inline sparkbars showing per-status time distribution. Clicking any row opens a detail panel.
- **Filter Bar** — Filter the entire dashboard by group, month, and status using pill controls and a searchable multi-select dropdown.

---

## Usage

This is a zero-dependency, zero-build HTML application. No server, no package manager, no compilation step.

1. Open `index.html` in any modern browser.
2. Export an Activity Log from Monday.com:
   - Open your board → **Activity Log** → **Export** → **CSV**
3. Upload the CSV via the landing page or the header upload zone.
4. Optionally save the dataset to the library for quick access later.

---

## CSV Format

The dashboard expects a Monday.com Activity Log CSV. Required columns:

| Column | Description |
|---|---|
| `Pulse Name` | Campaign / item name |
| `Previous Value` | Status before the change |
| `Value` | Status after the change |
| `Changed at` | ISO 8601 timestamp of the status change |

The parser derives time-in-status by computing durations between consecutive status transitions per item. Items are grouped by board and bucketed by month based on activity timestamps.

---

## Tech Stack

| Concern | Implementation |
|---|---|
| Runtime | Vanilla JS (ES2020), no framework |
| Charts | [Chart.js 4.4.0](https://www.chartjs.org/) via CDN |
| Fonts | Inter / Inter Tight via Google Fonts |
| Persistence | Browser `localStorage` (dataset library) |
| Build | None — single `.html` file |

---

## File Structure

```
index.html   # Entire application: HTML, CSS, and JS in one file
```

---

## Browser Support

Any modern browser (Chrome, Firefox, Safari, Edge). Internet Explorer is not supported. An active internet connection is required on first load for Chart.js and Google Fonts; after that, cached assets allow offline use.

---

## Limitations

- All data processing runs client-side; large CSVs (10k+ rows) may cause noticeable parse times.
- Dataset library relies on `localStorage` and is browser/device-specific — exports are not available.
- No authentication or multi-user support.
