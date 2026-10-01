# NYC 311 Service Requests — Cleaning & Exploratory Analysis

Python/pandas coursework — Baruch College (CIS 2300). **By Nicholas Osani.**

## The data

10,000 NYC 311 service requests from the NYC Open Data portal (Socrata API,
dataset `erm2-nwe9`), saved as `311_service_requests.csv`. Raw municipal data:
47 columns, inconsistent types, duplicates, and thousands of still-open cases.

## What I did

1. **Ingest** — pulled 10,000 rows via the Socrata API with pagination.
2. **Cleaning** — removed exact duplicates, inspected missing values, dropped
   rows missing key fields, dropped unneeded columns (47 → 28), parsed date
   strings to datetimes, and engineered `days_to_close` from
   `closed_date - created_date`. Still-open cases (no `closed_date`) were
   excluded from duration analysis — resolution time can't be measured on
   unresolved cases.
3. **Analysis** — categorical summaries: complaint mix, agency workload, and
   borough/temporal patterns.

## Key findings

- **10,000 raw rows → 6,031** after cleaning (4 duplicates; ~3,965 open cases).
- **Noise dominates**: `Noise - Residential` is the top complaint (2,062 of
  6,031), followed by `Illegal Parking` (1,476) and `Blocked Driveway` (551) —
  50 distinct complaint types.
- **NYPD carries 89%** of the cleaned caseload (5,360 complaints).
- **Brooklyn leads** boroughs (1,645); Staten Island has 135.

## Run it

```bash
pip install pandas jupyter
jupyter notebook 311-service-requests.ipynb
```

## Files

- `311-service-requests.ipynb` — full pipeline, executed end to end
- `311_service_requests.csv` — the 10,000-row raw pull
