# Citi Bike Trip Distance: January 2025 vs September 2025 (NYC)

## Overview
This project compares NYC Citi Bike trip distances in **January 2025** and **September 2025** to explore seasonal differences and understand whether changes are driven by:
1) **Rider mix** (more casual vs member riders), or  
2) **Behavioral shifts** (everyone riding farther).

## Data
- Source: NYC Citi Bike trip data (monthly tripdata CSVs).
- Months analyzed: **January 2025** and **September 2025**
- Sampling: Random samples were used for faster iteration.
- Key fields used:
  - `start_lat`, `start_lng`, `end_lat`, `end_lng`
  - `member_casual`
  - (optional) `started_at` / `ended_at` for time-based analysis

## Methodology

### 1 Cleaning
- Converted coordinate columns to numeric.
- Dropped rows with missing coordinates.
- Computed trip distance and removed **0-distance** trips (likely GPS/station artifacts).

### 2 Distance Calculation (Haversine)
Trip distance was computed from start/end coordinates using the Haversine formula.

### 3 Comparison Metrics
- Summary statistics (mean, median, quartiles, max)
- Distribution comparison (box plots with 5th–95th percentile whiskers)
- Total miles and **miles per 10,000 rides** (normalized for sample size)
- Breakdown by rider type (`member_casual`)

### 4 Decomposition: Mix vs Behavior
To explain why September distances are higher, the change in overall mean was decomposed into:
- **Composition effect**: effect of a larger share of casual riders
- **Within-group effect**: effect of longer rides among members/casual riders

Overall mean distance:
\[
\mu = p_{casual}\mu_{casual} + (1-p_{casual})\mu_{member}
\]

## Results (Key Findings)

### Overall Trip Distance Increase
- **Overall mean (Jan 2025):** 1.081 miles  
- **Overall mean (Sept 2025):** 1.338 miles  
- **Increase:** +0.257 miles (~24%)

### Normalized Total Mileage
- **Jan miles per 10k rides:** 10,809.91  
- **Sept miles per 10k rides:** 13,377.36  
- **Difference:** +2,567.45 miles per 10k rides (~23.7%)

### Rider Mix Shift (Casual Share)
- **Jan:** 9.19% casual
- **Sept:** 18.73% casual  
Casual share roughly **doubles** in September.

### Decomposition: What Drives the Increase?
Total mean increase: **+0.2567 miles**
- **Composition effect (more casual riders):** +0.0127 miles (~5%)
- **Within-group effect (rides longer):** +0.2441 miles (~95%)

**Interpretation:**  
September’s higher average distance is driven primarily by **longer rides within both rider types**, not mainly by the increased share of casual riders.

### Within-Group Mean Distances
- **Members:** 1.069 → 1.308 miles  
- **Casual:** 1.201 → 1.468 miles  

Both members and casual riders travel farther in September.

## Visualizations Included
- Box plot comparing Jan vs Sept trip distances (5th–95th percentile whiskers)
- Bar chart: mean distance by rider type (member vs casual)

## How to Run
1. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib
