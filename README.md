# Citi Bike NYC — Trip Data Analysis

Exploratory analysis of NYC Citi Bike trips across **January 2025** and **September 2025**,
covering ~150k trips combined. The project spans distance modeling, temporal demand patterns,
station-level analysis, and user-type segmentation.

---

## Tools & Stack

| Tool | Purpose |
|------|---------|
| Python 3 | Core analysis |
| pandas / numpy | Data loading, cleaning, feature engineering |
| matplotlib / seaborn | Visualizations |
| SQLite (`sqlite3`) | Relational query layer |
| Haversine formula | Trip distance estimation from GPS coordinates |

---

## Project Structure

```
citibike/
├── citibike.py                  # Full analysis script (Parts 1–4)
├── citibike.db                  # SQLite database (generated on run)
├── findings_report.md           # Stakeholder-facing findings report
├── peak_hours.png               # Trips by hour of day
├── top_stations.png             # Top 10 busiest start stations
├── trip_duration_dist.png       # Duration distribution by rider type
├── distance_by_rider_type.png   # Mean distance: Jan vs Sept by rider type
├── jan2025_tripdata_sample_75k.csv
└── sept2025_tripdata_sample_75k.csv
```

---

## How to Run

```bash
pip install pandas numpy matplotlib seaborn
python citibike.py
```

Running the script produces all outputs: the SQLite database, four PNG charts, and
`findings_report.md` — all populated with numbers from the actual dataset.

---

## Part 1 — Distance Analysis (Jan vs Sept)

Computes straight-line trip distance using the **Haversine formula** from start/end GPS coordinates.

**Key results:**
- Mean trip distance: **1.08 miles** (Jan) → **1.34 miles** (Sept) — a ~24% increase
- This increase is driven almost entirely by **within-group behavior** (everyone rides farther),
  not by the mix shifting toward more casual riders
  - Composition effect: +0.013 miles (~5%)
  - Within-group effect: +0.244 miles (~95%)

---

## Part 2 — SQLite Database Layer

The combined dataset is loaded into `citibike.db` and queried with four SQL analyses:

| Query | Finding |
|-------|---------|
| Trips by hour | Evening commute (5 PM) is the single busiest hour with 13,591 trips |
| Top 10 stations | W 21 St & 6 Ave leads with 607 trip starts |
| Weekday vs weekend | Weekdays: 3.2× the volume; weekends: longer avg trips |
| Duration by user type | Casual riders average 15.7 min; members average 10.3 min |

---

## Part 3 — Visualizations

All charts are saved as PNG files at 150 DPI.

**[peak_hours.png](peak_hours.png)** — Bar chart of trips by hour. The top 3 busiest hours
(4 PM, 5 PM, 6 PM) are highlighted in red. The evening commute spike is clearly dominant.

**[top_stations.png](top_stations.png)** — Horizontal bar of the 10 highest-volume start stations
across both months. Stations in Chelsea/Midtown West account for most of the top 10.

**[trip_duration_dist.png](trip_duration_dist.png)** — Overlapping histograms of trip duration
(capped at 60 min) for members vs casual riders. Members cluster tightly under 15 min;
casual riders have a much wider, longer-tailed distribution.

---

## Part 4 — Key Findings

Full findings with context and operational recommendations are in
[findings_report.md](findings_report.md).

Summary:
1. **5 PM is peak hour** — 13,591 trips; bimodal commute pattern visible across both months
2. **Top stations are highly concentrated** — W 21 St & 6 Ave, W 31 St & 7 Ave, and
   Lafayette St & E 8 St lead in departure volume
3. **Weekdays drive volume, weekends drive duration** — 3.2× more trips on weekdays;
   weekend trips average ~1 min longer
4. **Casual riders are a summer conversion opportunity** — casual share doubles from ~9%
   (Jan) to ~19% (Sept); casual riders take 1.5× longer trips than members

---

## Data

- **Source:** [Citi Bike System Data](https://citibikenyc.com/system-data) (public)
- **Samples:** 75,000-row random samples from January 2025 and September 2025 full monthly files
- **Cleaning:** Missing coordinates dropped; zero-distance trips removed; trips with duration
  outside 0–240 min excluded
