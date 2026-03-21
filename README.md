# PrismAnalytics
<div align="center">

<img src="https://img.shields.io/badge/version-1.0.0-F72585?style=for-the-badge&labelColor=1A1035" />
<img src="https://img.shields.io/badge/zero_dependencies-pure_HTML-7C83FD?style=for-the-badge&labelColor=1A1035" />
<img src="https://img.shields.io/badge/Chart.js-4.4.0-FF6B6B?style=for-the-badge&labelColor=1A1035" />
<img src="https://img.shields.io/badge/license-MIT-6BCB77?style=for-the-badge&labelColor=1A1035" />

<br /><br />

```
██████╗ ██████╗ ██╗███████╗███╗   ███╗
██╔══██╗██╔══██╗██║██╔════╝████╗ ████║
██████╔╝██████╔╝██║███████╗██╔████╔██║
██╔═══╝ ██╔══██╗██║╚════██║██║╚██╔╝██║
██║     ██║  ██║██║███████║██║ ╚═╝ ██║
╚═╝     ╚═╝  ╚═╝╚═╝╚══════╝╚═╝     ╚═╝
   A N A L Y T I C S
```

### **User Intelligence Dashboard**
*Volume & Growth · Activity Heatmap · Retention & Churn · Funnel Analysis*

<br />

[**→ Live Demo**](#) · [**→ Documentation**](#-documentation) · [**→ Quick Start**](#-quick-start) · [**→ Schema**](#-csv-schema)

<br />

</div>

---

## ✨ What is Prism Analytics?

**Prism Analytics** is a fully self-contained, single-file HTML dashboard that takes user event data from your company database (or a CSV upload) and surfaces four core intelligence modules — rendered in a vibrant, gradient-rich interface with zero build steps.

- 🗂 **One file** — `pulsedb_vibrant.html`. No npm, no webpack, no server.
- 🔌 **DB-ready** — configure PostgreSQL, MySQL, MongoDB, BigQuery, Snowflake or SQLite via the built-in connection panel.
- 📂 **CSV upload** — drag & drop any events CSV and all charts re-render instantly.
- 🎨 **Bold design** — vibrant gradient theme, Cabinet Grotesk + Fira Code typography, animated mesh background.
- 📊 **50K demo records** — pre-loaded synthetic data so you can explore every module before connecting real data.

---

## 📸 Screenshots

| Overview | Activity Heatmap |
|----------|-----------------|
| KPI cards + volume trend + geo | Day × Hour event heatmap |

| Retention Matrix | Funnel Analysis |
|-----------------|-----------------|
| 8-cohort × 8-week color matrix | Stage drop-off with device breakdown |

---

## ⚡ Quick Start

### Option A — Open in browser (zero setup)
```bash
# Just open the file
open pulsedb_vibrant.html
```
50,000 synthetic events load instantly. Explore every module with demo data.

### Option B — Upload your CSV
1. Click **⬆ Upload CSV** in the top bar
2. Drop a `.csv` file matching the [schema below](#-csv-schema)
3. All charts re-render immediately

### Option C — Connect your database
1. Click **🔌 Connect DB** in the top bar (or the sidebar status pill)
2. Select your DB type, enter credentials + a SELECT query
3. Hit **Test Connection**, then **Save & Connect**
4. The sidebar dot turns 🟢 green

> **Note:** The connection panel stores credentials in-session only. For production use, add a thin backend proxy that executes the query and returns JSON rows, then call `loadRows(data)` in the JS.

---

## 📊 Analytics Modules

### 📈 Volume & Growth
| Chart | Description |
|-------|-------------|
| KPI Cards | Unique Users, Sessions, Avg Duration, Page Views with Δ% |
| Volume Trend | DAU / New / Returning users over 7D · 30D · 90D |
| Traffic Sources | Acquisition mix doughnut (Organic, Paid, Social, Email, Direct, Referral) |
| Device Breakdown | Desktop vs Mobile vs Tablet session split |
| Top Locations | Geographic distribution horizontal bar |

### 🔥 Activity Heatmap
| Chart | Description |
|-------|-------------|
| Heatmap Grid | 7 days × 24 hours event frequency, blue→pink intensity gradient |
| Sessions/Day | Daily bar chart with 7-day rolling average overlay |
| Top Actions | Ranked horizontal bar of most-performed in-app events |

### 🔄 Retention & Churn
| Chart | Description |
|-------|-------------|
| Cohort Matrix | 8 monthly cohorts × 8 weeks, color-coded retention % |
| KPI Cards | Day-1 / Day-7 / Day-30 retention rates + monthly churn |
| Churn Trend | Monthly churn rate line chart over 8 months |
| Lifecycle | Active / At-risk / Churned breakdown doughnut |

### 🎯 Funnel Analysis
| Chart | Description |
|-------|-------------|
| Conversion Funnel | Visit → Signup → Add to Cart → Purchase with gradient bars |
| Funnel by Device | Desktop / Mobile / Tablet conversion rate comparison |
| Drop-off Analysis | Ranked leakage points horizontal bar |

### 🔬 Segments
Pie chart + behavior radar + comparison table across **New · Returning · Power · At-Risk · Churned** segments.

### 👥 User Records
Searchable per-user table — filter by ID, location, segment, or source. Derived live from raw event data.

---

## 📄 CSV Schema

Only `user_id`, `date`, and `action` are required. All other columns fall back to safe defaults.

| Column | Type | Description | Required |
|--------|------|-------------|----------|
| `user_id` | string | Unique identifier per user | ✅ |
| `date` | `YYYY-MM-DD` | Date of activity | ✅ |
| `action` | string | `page_view`, `click`, `purchase`, `signup`… | ✅ |
| `device` | string | `Desktop` / `Mobile` / `Tablet` | — |
| `location` | string | City or region name | — |
| `source` | string | `Organic`, `Paid`, `Social`, `Email`, `Direct`… | — |
| `session_duration` | integer | Session length in seconds | — |
| `page_views` | integer | Pages viewed per session | — |
| `segment` | string | `new` / `returning` / `power` / `at_risk` / `churned` | — |
| `hour` | integer | Hour of day (0–23) | — |

**Sample rows:**
```csv
user_id,date,action,device,location,source,session_duration,page_views,segment,hour
U00142,2026-03-01,page_view,Mobile,Mumbai,Organic,320,4,returning,9
U00891,2026-03-01,add_to_cart,Desktop,Bengaluru,Email,610,7,power,14
U00023,2026-03-02,purchase,Mobile,Delhi,Paid Ads,445,5,new,11
```

---

## 🗓️ Date Range Filter

Use the **7D · 30D · 90D** buttons in the sidebar bottom. Switching range re-filters the in-memory dataset and re-renders every active chart.

| Range | Best for |
|-------|----------|
| `7D` | Spotting short-term spikes or anomalies |
| `30D` | Default — balanced view for monthly reporting |
| `90D` | Cohort retention and funnel trend analysis |

---

## 🔌 Supported Databases

| Database | Default Port | Notes |
|----------|-------------|-------|
| PostgreSQL | 5432 | Recommended |
| MySQL | 3306 | |
| MongoDB | 27017 | |
| Google BigQuery | — | Project + dataset |
| Snowflake | — | Account + warehouse |
| SQLite | — | File path or in-browser WASM |

**Example query** (adapt column names to your schema):
```sql
SELECT
  user_id,
  DATE(created_at)        AS date,
  event_type              AS action,
  device,
  city                    AS location,
  utm_source              AS source,
  session_seconds         AS session_duration,
  pages_viewed            AS page_views,
  user_segment            AS segment,
  HOUR(created_at)        AS hour
FROM   user_events
WHERE  created_at >= NOW() - INTERVAL '30 DAY'
LIMIT  100000;
```

---

## 🛠️ Tech Stack

| Library | Version | Purpose |
|---------|---------|---------|
| [Chart.js](https://www.chartjs.org/) | 4.4.0 | All charts — line, bar, doughnut, radar, pie |
| [PapaParse](https://www.papaparse.com/) | 5.4.1 | CSV parsing |
| Cabinet Grotesk | Google Fonts | Display typography |
| Fira Code | Google Fonts | Monospace — IDs, KPIs, code |
| Vanilla JS | ES2020 | All interactivity — no framework |

Both Chart.js and PapaParse are loaded from CDN. **No npm install needed.**

---

## 🎨 Customisation

All design tokens live in `:root {}` at the top of the file:

```css
:root {
  --pink:    #F72585;   /* Primary accent — nav active, headings   */
  --indigo:  #7C83FD;   /* Secondary — borders, chips              */
  --coral:   #FF6B6B;   /* KPI card 1, funnel bars                 */
  --lime:    #6BCB77;   /* Success states, lifecycle               */
  --sky:     #4FC3F7;   /* Device chart, heatmap cool end          */
  --yellow:  #FFD93D;   /* Warning, at-risk segment                */
  --ink:     #1A1035;   /* Primary text + sidebar background       */
  --off:     #F9F7FF;   /* Main canvas background                  */
}
```

**Adding a new chart:**
1. Add `<canvas id="cMyChart">` inside any `.card` in the HTML
2. Call `mk("cMyChart", { type, data, options })` in the relevant render function
3. Use the `PAL[]` color array to stay on-palette
4. Use the `GS` object for consistent axis tick + gridline styles

---

## ⚠️ Known Limitations

- **No real backend** — DB credentials are in-session only; actual queries need a backend proxy
- **Large datasets** — 500K+ rows may cause slowness; pre-aggregate server-side for best performance
- **Retention cohorts** — derived from the `date` column; ensure your data covers the full selected range
- **CSV encoding** — file must be UTF-8
- **Best at ≥ 1024px** — sidebar may collapse on smaller viewports

---

## 🚀 Roadmap

- [ ] Real-time WebSocket sync from live DB streams
- [ ] PDF / PNG chart export per module
- [ ] Per-user drill-down timeline on row click
- [ ] Threshold-based anomaly alerts on KPI cards
- [ ] Dark mode toggle
- [ ] Multi-workspace URL-param switching

---

## 📁 File Structure

```
pulsedb_vibrant.html     ← The entire app (HTML + CSS + JS)
README.md                ← This file
```

That's it. One file.

---

## 📜 License

MIT — free to use, modify, and distribute.

---

<div align="center">

**Open `pulsedb_vibrant.html` in any browser to get started.**

Made with ♥ by the Prism Analytics team

</div>
