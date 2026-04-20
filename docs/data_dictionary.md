# Data Dictionary — US Flight Delays 2015

## Dataset Overview

| Property | Value |
|----------|-------|
| **Sector** | Aviation / Transportation |
| **Source** | Bureau of Transportation Statistics (BTS) |
| **Time Period** | January 2015 — December 2015 |
| **Total Records** | ~5,819,079 flights |
| **Format** | CSV |

---

## Source Files

### 1. `airlines.csv` (14 rows × 2 columns)

| Column | Type | Description |
|--------|------|-------------|
| IATA_CODE | string | 2-letter airline identifier (e.g., AA, UA, DL) |
| AIRLINE | string | Full airline name (e.g., "American Airlines Inc.") |

### 2. `airports.csv` (322 rows × 7 columns)

| Column | Type | Description |
|--------|------|-------------|
| IATA_CODE | string | 3-letter airport identifier (e.g., ATL, LAX, ORD) |
| AIRPORT | string | Full airport name |
| CITY | string | City where the airport is located |
| STATE | string | 2-letter US state code |
| COUNTRY | string | Country code (USA) |
| LATITUDE | float | Geographic latitude |
| LONGITUDE | float | Geographic longitude |

### 3. `flights.csv` (~5.8M rows × 31 columns)

| Column | Type | Description | Notes |
|--------|------|-------------|-------|
| YEAR | int | Year of flight (2015) | |
| MONTH | int | Month (1-12) | |
| DAY | int | Day of month (1-31) | |
| DAY_OF_WEEK | int | Day of week (1=Mon, 7=Sun) | |
| AIRLINE | string | 2-letter airline IATA code | FK to airlines.csv |
| FLIGHT_NUMBER | int | Flight number | |
| TAIL_NUMBER | string | Aircraft tail registration number | Has missing values |
| ORIGIN_AIRPORT | string | Departure airport IATA code | FK to airports.csv |
| DESTINATION_AIRPORT | string | Arrival airport IATA code | FK to airports.csv |
| SCHEDULED_DEPARTURE | int | Scheduled departure time (HHMM format) | e.g., 1430 = 2:30 PM |
| DEPARTURE_TIME | float | Actual departure time (HHMM format) | NaN if cancelled |
| DEPARTURE_DELAY | float | Departure delay in minutes (negative = early) | NaN if cancelled |
| TAXI_OUT | float | Minutes from gate to wheels-off | NaN if cancelled |
| WHEELS_OFF | float | Take-off time (HHMM format) | NaN if cancelled |
| SCHEDULED_TIME | float | Scheduled flight duration (minutes) | |
| ELAPSED_TIME | float | Actual flight duration (minutes) | NaN if cancelled |
| AIR_TIME | float | Time in the air (minutes) | NaN if cancelled |
| DISTANCE | int | Distance between airports (miles) | |
| WHEELS_ON | float | Landing time (HHMM format) | NaN if cancelled |
| TAXI_IN | float | Minutes from landing to gate | NaN if cancelled |
| SCHEDULED_ARRIVAL | int | Scheduled arrival time (HHMM format) | |
| ARRIVAL_TIME | float | Actual arrival time (HHMM format) | NaN if cancelled |
| ARRIVAL_DELAY | float | Arrival delay in minutes (negative = early) | NaN if cancelled |
| DIVERTED | int | 1 = flight was diverted, 0 = not | |
| CANCELLED | int | 1 = flight was cancelled, 0 = not | |
| CANCELLATION_REASON | string | A=Airline, B=Weather, C=NAS, D=Security | NaN if not cancelled |
| AIR_SYSTEM_DELAY | float | Delay due to air system (NAS) in minutes | NaN → 0 if no delay |
| SECURITY_DELAY | float | Delay due to security in minutes | NaN → 0 if no delay |
| AIRLINE_DELAY | float | Delay due to airline/carrier in minutes | NaN → 0 if no delay |
| LATE_AIRCRAFT_DELAY | float | Delay due to late arriving aircraft in minutes | NaN → 0 if no delay |
| WEATHER_DELAY | float | Delay due to weather in minutes | NaN → 0 if no delay |

---

## Engineered Columns (Added During Cleaning)

| Column | Type | Description |
|--------|------|-------------|
| DATE | datetime | Proper date column (YYYY-MM-DD) |
| SCHEDULED_DEPARTURE_TIME | string | Scheduled departure in HH:MM format |
| SCHEDULED_ARRIVAL_TIME | string | Scheduled arrival in HH:MM format |
| MONTH_NAME | string | Full month name (e.g., "January") |
| DAY_NAME | string | Full day name (e.g., "Monday") |
| QUARTER | string | Quarter (Q1, Q2, Q3, Q4) |
| DEP_HOUR | int | Departure hour (0-23) |
| TIME_OF_DAY | string | Morning / Afternoon / Evening / Night |
| CANCELLATION_REASON_DESC | string | Human-readable cancellation reason |
| IS_EXTREME_DEP_DELAY | int | 1 if departure delay > 180 min |
| IS_EXTREME_ARR_DELAY | int | 1 if arrival delay > 180 min |
| DEPARTURE_DELAY_CAPPED | float | Departure delay winsorized at 99.5th percentile |
| ARRIVAL_DELAY_CAPPED | float | Arrival delay winsorized at 99.5th percentile |
| DELAY_CATEGORY | string | On Time / Minor / Moderate / Significant / Severe / Cancelled |
| IS_DELAYED | int | 1 if arrival delay > 15 min (industry standard) |
| TOTAL_DELAY_BREAKDOWN | float | Sum of all 5 delay cause columns |
| PRIMARY_DELAY_CAUSE | string | Dominant delay cause for each flight |
| DISTANCE_CATEGORY | string | Short-haul / Medium-haul / Long-haul |
| ROUTE | string | "ORIGIN → DESTINATION" concatenation |
| AIRLINE_NAME | string | Full airline name (merged from airlines.csv) |
| ORIGIN_AIRPORT_NAME | string | Full origin airport name (merged) |
| ORIGIN_CITY | string | Origin city name (merged) |
| ORIGIN_STATE | string | Origin state code (merged) |
| ORIGIN_LAT | float | Origin airport latitude (merged) |
| ORIGIN_LONG | float | Origin airport longitude (merged) |
| DEST_AIRPORT_NAME | string | Full destination airport name (merged) |
| DEST_CITY | string | Destination city name (merged) |
| DEST_STATE | string | Destination state code (merged) |
| DEST_LAT | float | Destination airport latitude (merged) |
| DEST_LONG | float | Destination airport longitude (merged) |

---

## KPI Definitions

| KPI | Formula | Business Meaning |
|-----|---------|------------------|
| **On-Time Rate** | % of flights with ARRIVAL_DELAY ≤ 15 min | Industry-standard punctuality measure |
| **Delay Rate** | % of flights with ARRIVAL_DELAY > 15 min | Inverse of on-time rate |
| **Cancellation Rate** | CANCELLED flights / Total flights × 100 | Operational reliability metric |
| **Avg Departure Delay** | Mean of DEPARTURE_DELAY (non-cancelled) | Ground operations efficiency |
| **Avg Arrival Delay** | Mean of ARRIVAL_DELAY (non-cancelled) | End-to-end delay measure |
| **Primary Delay Cause** | Highest value among 5 delay columns | Root cause analysis |

---

## Data Limitations

- Dataset covers only **US domestic flights** in 2015
- No airline financial data (revenue, fuel cost) is included
- Weather data is limited to delay attribution — no raw meteorological data
- Some airport codes in flights may not map to airports.csv (non-IATA codes)
- Delay cause columns only populated when total delay > 15 min
