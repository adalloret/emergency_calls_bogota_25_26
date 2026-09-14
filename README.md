# Bogotá 123 Emergency Line Response: Data Pipeline and Data Analyisis

## Project Overview
Data analysis and engineering analyzing 12 months of emergency calls through the 123 emergency  line in Bogotá (August 2025 - July 2026) 

## Tech Stack
* **Data Warehous:e**: Google BigQuery
* **Data Modeling:** BigQuery SQL
* **Analytics and Visualization:** PowerBI

## Key Findings
### 1. Operational Traceability and Loss of Control (`is_missing_reception`)
* **Global Loss Rate:** 51.05% of dispatched emergency calls lacked an official hospital reception timestamp.
* **Top Critical Localities (Statistically Filtered)**: To eliminate low-volumne sampling bias, local districts were dynamically filtered using a 25th percentile volume treshold ($P:{25}\ge 3,245$ incidents). Among representative high-volume urban localitues, **Barrios Unidos** and **Usaquén** registered the highest rates of missing hospital reception traceability (**56.21%** and **55.99%** respectively), representing over 6630 unminored patiend handovers combined.

### 2. Emergency Latency Analysis (`latency_minutes`)
* **Average Response Time:** The overall average response time from ambulanec dispatch to hospital reception was **194.0 minutes** (median: **189.0 minutes**)
* **Extreme Latencies (>6 Hours):** **2,422 incidents** (**2.03%** of all recorded emergency dispatch operations experienced extreme delay anomalies exceeding the 6-hour threshold
* **Shift Period Impact:** Response times spiked during the **morning** shift, reaching an average latency of **205.8 minutes** (median: **200.0 minutes**), compared to **180.5 minutes** (median: **171.0 minutes**) during the **night** shift.

### 3. Demographic and Vulnerable Population Assesment
* **Adulthood Prevalence (18-59):** Represented the single largest demographic cohort requesting emergency medical services, accounting for **35.56%** of total annual incidents.
* **Senior Population (60+):** Represented **22.06%** of total emergency incidents, exhibiting the highest average latencies in **Usme** (**227.6 minutes** on average).

--- 

## Data model and Pipeline Architecutre
### Unified Staging View (`vw_incidencia_historica`)
The core analytics layer unifies 12 monthly CSV tables using a `COALESCE` pattern to handle varying schema headers, column names, and type conversions while sntardizing all field names to English standards: 
* `incident_id` : Stantardize emergency ID
* `dispatch_timestamp` / `reception_timestamp`: Audit timestamps
* `locality`: Cleaned and mapped to Bogotá's 20 officil districts and outsied of Bogotá
* `age_group`: Categorized demographic cohorts (`early_childhood`, `childhood`, `adolescence`, `adulthood`, `senior`).
* `shift_period`: Time window (`morning`, `afternoon`, `evening`, `night`)
* `is_missing_reception`, `is_extreme_latency_6h`, `is_time_inconsisstency`: Automated flags

--- 




