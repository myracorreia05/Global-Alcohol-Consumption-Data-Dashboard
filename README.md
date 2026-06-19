# PROOF — Global Alcohol Consumption Dashboard

**An interactive data journalism project exploring alcohol consumption patterns across 193 countries**


![PROOF Dashboard Preview]
</div>

---

## What Is This?

PROOF is a single-file, zero-dependency interactive data dashboard built to explore a deceptively rich dataset: **what does every country on Earth drink, and how much?**

It started as a portfolio project. It became a genuine investigation into how culture, religion, colonialism, and geography shape human habit at a global scale.

The findings are surprising. Belarus consumes nearly **3× the global average** of pure alcohol. Namibia leads the world in beer — a direct legacy of German colonial breweries from the 1800s. Haiti drinks almost exclusively spirits. 13 countries report zero consumption entirely. Europe out-drinks Asia by a factor of **3.7×**, not because of wealth (Singapore and Japan are affluent) — but because of culture.

This project visualises all of it.

---

## Live Demo

🔗 **[myracorreia05.github.io/Global-Alcohol-Consumption-Data-Dashboard](https://myracorreia05.github.io/Global-Alcohol-Consumption-Data-Dashboard/)** 

---

## Key Findings from the Data

| Finding | Detail |
|---|---|
| 🥇 Heaviest overall | **Belarus** — 14.4L pure alcohol / person / year |
| 🥈 2nd heaviest | **Lithuania** — 12.9L |
| 🍺 Beer champion | **Namibia** — 376 servings / year |
| 🥃 Spirits champion | **Grenada** — 438 servings / year |
| 🍷 Wine champion | **France** — 370 servings / year |
| 🌍 Global average | **4.7L** pure alcohol per person per year |
| 🚫 Zero consumption | **13 countries** — all majority-Muslim nations |
| 📊 Beer dominance | **101 of 180** drinking nations choose beer as primary beverage (56%) |
| 🌐 Biggest regional gap | Europe (8.7L avg) vs. Asia (2.0L avg) — **3.7× difference** |

### Regional Averages

| Region | Countries | Avg Total (L) | Avg Beer | Avg Spirits | Avg Wine |
|---|---|---|---|---|---|
| Europe | 46 | 8.7 | 195 | 137 | 141 |
| Americas | 36 | 6.1 | 151 | 151 | 39 |
| Oceania | 15 | 3.2 | 96 | 45 | 33 |
| Africa | 52 | 3.1 | 63 | 17 | 17 |
| Asia | 43 | 2.0 | 32 | 55 | 8 |

---

## Visualisations

The project includes **7 distinct chart types**, all built from scratch:

| Visualisation | Technology | What It Shows |
|---|---|---|
| **Choropleth World Map** | D3.js + TopoJSON | All 193 countries colour-coded by consumption metric — switchable between total alcohol, beer, spirits, and wine |
| **Force-Collision Bubble Chart** | D3.js force simulation | One circle per country, area ∝ total consumption, colour = dominant drink, physics-packed layout |
| **Scatter Plot** | D3.js | Beer vs. spirits for all 193 countries — with average crosshair lines, labelled outliers, and tooltip hover |
| **Distribution Histogram** | D3.js | Full distribution of consumption across all nations, colour-binned by intensity |
| **Stacked Bar Chart** | Vanilla JS | Top 12 nations with beer/spirits/wine composition breakdown |
| **Ranked Bar Charts** | Vanilla JS | Top 10–15 by beer, spirits, wine, and total alcohol |
| **Colour-coded Heatmap** | Vanilla JS | Top 20 nations compared across all 4 metrics with 6-level intensity scale |

Plus a fully interactive data table — **sortable by any column, searchable by country name, filterable by continent, paginated**.

---

## Country Spotlight Highlights

Nine countries get in-depth portrait cards because the numbers alone don't tell the full story:

**Namibia** — 376 beer, 3 spirits, 1 wine. An almost total beer monoculture. German colonial breweries established in the late 1800s never left, and their influence on local consumption is measurable over a century later.

**Haiti** — 326 spirits, 1 beer, 1 wine. The most extreme beverage monoculture in the dataset. Clairin, a raw unaged sugarcane spirit, constitutes almost all alcohol consumed in the country.

**Grenada** — 438 spirit servings per year, the highest of any nation on Earth. Rum production on the island shapes local consumption patterns in a way few places rival.

**France** — 370 wine servings, 151 spirits, 127 beer. The only high-volume drinker with genuine balance across all three categories.

**Nigeria** — 9.1L total but only 42 beer servings. The dataset likely undercounts locally-brewed sorghum beer and palm wine, which are not always captured in WHO serving data.

**South Korea** — 9.8L/year, the highest in Asia (excluding Russia). Extraordinary for a region that averages 2.0L. Soju and beer culture are deeply embedded.

---

## Technical Build

### Stack
- **D3.js v7** — choropleth map, bubble chart, scatter plot, histogram, axes
- **TopoJSON** — world topology for the choropleth
- **Vanilla JavaScript (ES6+)** — all interactivity, filtering, sorting, state management
- **HTML5 / CSS3** — layout, animations, custom design system
- **Google Fonts CDN** — Cormorant Garamond + JetBrains Mono

### What I deliberately avoided
No React. No Vue. No Chart.js. No npm. No build step. No webpack.

Every chart, animation, and interaction is written by hand. This was an intentional choice: using a charting library abstracts away the parts that are worth understanding — scale functions, projection systems, force simulations, DOM manipulation, event delegation. Writing it from scratch forces genuine understanding.

### Architecture
The entire project is **one HTML file** (`drinks_deep.html`). All 193 country records are embedded as a JavaScript constant. All CSS is in a `<style>` block. All logic is in a `<script>` block. Open the file in a browser — it works. No server required.

### Key implementation details
- **World map**: Uses `d3.geoNaturalEarth1()` projection with a name-normalisation dictionary to match country names between WHO data and TopoJSON topology (e.g. `"czechia"` → `"Czech Republic"`)
- **Bubble chart**: `d3.forceSimulation()` with `forceCollide`, `forceX`, and `forceY` — 300 ticks computed synchronously before render to avoid animation jank
- **Colour scales**: `d3.scaleLinear()` with custom 3-stop colour ramps per metric
- **Scroll animations**: `IntersectionObserver` with staggered `transition-delay` for cascade reveal
- **Scroll progress bar**: `window.scrollY / (scrollHeight - innerHeight)` mapped to a fixed `<div>` width

---

## Dataset


| Column | Type | Description |
|---|---|---|
| `country` | string | Country name |
| `beer_servings` | integer | Beer servings per person per year |
| `spirit_servings` | integer | Spirit servings per person per year |
| `wine_servings` | integer | Wine servings per person per year |
| `total_litres_of_pure_alcohol` | float | Litres of pure alcohol per person per year |

**Records:** 193 countries  
**Nulls:** None — 13 countries legitimately report 0 across all categories  
**Coverage:** Circa 2010–2014 (WHO reporting window)

---

## Skills Demonstrated

This project was built to demonstrate practical skills across the analytics-to-engineering stack:

- **Data analysis** — statistical exploration, outlier identification, regional segmentation, correlation analysis
- **Data visualisation** — 7 chart types built from first principles using D3.js
- **Data storytelling** — translating raw numbers into narrative insights (the Namibia colonial brewing finding, the Haiti clairin monoculture, etc.)
- **Frontend engineering** — state management, event delegation, DOM manipulation, CSS animations, responsive layout
- **UX/UI design** — custom design system, dark editorial aesthetic, scroll-based reveal, interactive tooltips
- **Geospatial visualisation** — choropleth mapping with TopoJSON, country name normalisation across datasets

---

## About the Author

**Myra Correia** — MS in Business Analytics, Syracuse University (Whitman School of Management, 2026) · GPA 3.85

BBA + LLB, University of Mumbai · Former Business Analyst at Limeneal Solutions, where I built 10+ Power BI / Tableau dashboards and automated 300+ hours of manual reporting.

I build data projects at the intersection of analytics, storytelling, and engineering.


