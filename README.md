# Bogotá 123 Emergency Line Response: Data Pipeline and Data Analyisis

## Project Overview
Data analysis and engineering analyzing 12 months of emergency calls through the 123 emergency  line in Bogotá (2025 - 2026) 

## Tech Stack
* **Data Warehous:e**: Google BigQuery
* **Data Modeling:** BigQuery SQL
* **Analytics and Visualization:** PowerBI

## Key Findings
### 1. Audit & Traceability
* **Critical Traceability Loss:** **Chapinero (60.28%)** and **La Candelaria (57.5%)** exhibited the highest rate of missing hospital reception.
* **Extreme Latency Bottlenecks:** A total of **2,422 incidents** (**2.03%** of all dispatch operations) experienced extreme delay anomalies exceeding the 6-hour threshold.
* **Timestamp Consistency:** **0 temporal anomalies** (negative numbers) detected across all records, confirming chronological integrity between dispatch and hospital arrival timestamps.

### 2. Operational Performance
* **Total Demand:** Processed **119,427 incidents** with an overall average latency of **128.21 minutes**.
* **Volume Distribution:** **Kennedy (16,096)**, **Engativá (10,961)**, and **Suba (10,916)** represent the top 3 highest volume districts in Bogotá.

### 3. Demographic & Vulnerable Population Assessment
* **Adulthood Prevalence (18-59):** Represented the primary demographic cohort requesting emergency services (**35.56%** of total calls).
* **Senior Cohort (60+):** Accounted for **22.06%** of incidents, registering the longest response times, with average latencies exceeding **210 minutes**.
* **Shift Period Share:** Incident distribution remained balanced across shifts: **Evening** (27.2%), **Morning** (26.8%), **Afternoon** (25.8%), and **Night** (20.2%).

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

## Dashboard Previews
### Page 1: Audit and Traceability
![Audit and Traceability](image1)
### Page 2: Operations
![Operations](image2)
### Page 3: Demographic and Shifts
![Demographic and Shifts](emergency_calls_bogota_25_26
/Demographic and Shifts.jpg)




