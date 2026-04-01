# Citi Bike NYC — Operations Findings Report
*Prepared by: Data Analysis Team | Dataset: January 2025 & September 2025 trip samples (146,986 trips)*

---

## Executive Summary

This report summarizes key patterns in Citi Bike ridership drawn from a combined sample of
**146,986 trips** across January and September 2025. The analysis covers peak demand hours,
high-volume stations, weekday vs. weekend usage, and differences between member and casual riders.
Findings are intended to support scheduling, infrastructure, and outreach decisions.

---

## Key Finding 1 — Peak Demand Concentrates in the Evening Commute Window

Ridership follows a clear bimodal pattern: a morning rise and a stronger evening peak.

- The **single busiest hour is 5:00 PM**, with **13,591 trips**.
- The next two busiest hours are **6:00 PM** and **4:00 PM**.
- Overnight hours (midnight–6 AM) are the quietest period across both months.

**Recommendation:** Prioritize rebalancing operations and staffing during the 5:00 PM–6:00 PM window.
Consider dynamic incentive pricing or pre-positioned bikes at high-demand stations before peak hours.

---

## Key Finding 2 — A Small Number of Stations Drive Disproportionate Volume

The top 10 start stations account for a significant share of all departures.

- **#1 busiest station:** W 21 St & 6 Ave (607 trip starts across both months)
- The top 10 stations (out of hundreds citywide) concentrate departures at transit hubs,
  waterfront areas, and high foot-traffic intersections.

**Recommendation:** Ensure these high-volume stations are prioritized in real-time inventory
monitoring. Frequent shortages at these nodes have an outsized impact on rider satisfaction.

---

## Key Finding 3 — Weekdays Drive Volume; Weekends Drive Longer Rides

| Day Type | Total Trips | Avg Duration |
|----------|-------------|--------------|
| Weekday  | 112,186     | 10.8 min |
| Weekend  | 34,800     | 11.8 min |

- Weekdays generate **3.2× the trip volume** of weekends, consistent with commuter use.
- Weekend riders take longer trips on average (11.8 min vs. 10.8 min), suggesting
  more recreational use.

**Recommendation:** Operations staffing and bike availability targets should differ by day type.
Weekend rebalancing can focus on longer-duration hotspots (parks, waterfronts); weekday operations
should prioritize throughput at transit-adjacent stations.

---

## Key Finding 4 — Casual Riders Take Longer Trips; Members Ride More Frequently

| Rider Type | Trips | Avg Duration | Avg Distance |
|------------|-------|--------------|--------------|
| Member     | 126,507  | 10.3 min | 1.181 mi |
| Casual     | 20,479   | 15.7 min | 1.379 mi |

- **Members** make up the majority of trips and ride shorter, more purposeful routes —
  consistent with daily commute patterns.
- **Casual riders** take trips that are **1.5× longer** on average and cover more
  distance per trip, suggesting tourism or leisure use.
- Both months contribute roughly equal sample sizes (~73k trips each), but September's rider
  composition shifts dramatically: casual riders grow from **~9% in January to ~19% in September**,
  reflecting seasonal tourism and recreational demand.

**Recommendation:** Casual rider growth in summer creates conversion opportunities.
Targeted membership promotions in August–September (when casual share peaks) could improve
annual revenue. Consider in-app prompts after a rider's 3rd casual trip.

---

## Visualizations

| File | Description |
|------|-------------|
| [peak_hours.png](peak_hours.png) | Trips by hour of day — top-3 hours highlighted |
| [top_stations.png](top_stations.png) | Horizontal bar chart of top 10 start stations |
| [trip_duration_dist.png](trip_duration_dist.png) | Duration distribution by rider type (≤60 min) |
| [distance_by_rider_type.png](distance_by_rider_type.png) | Mean Haversine distance: Jan vs Sept by rider type |

---

## Data Notes

- **Source:** NYC Citi Bike monthly trip data (publicly available)
- **Months:** January 2025 (75k-row sample), September 2025 (75k-row sample)
- **Cleaning applied:** Rows missing coordinates dropped; zero-distance trips removed
  (likely GPS/docking artifacts); trips with duration ≤ 0 or ≥ 240 min excluded
- **Distance method:** Haversine formula from start/end GPS coordinates
- All figures reflect the cleaned sample and may not represent full-month totals exactly
