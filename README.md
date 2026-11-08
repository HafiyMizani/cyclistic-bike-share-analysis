# Cyclistic Bike-Share: Data-Driven Conversion Strategy
### Google Data Analytics Professional Certificate Capstone Project

---

## 📌 Project Overview
This repository contains an end-to-end data analytics case study analyzing historical trip records from Cyclistic, a fictional bike-share company based in Chicago. The core objective is to analyze behavioral differences between annual members and casual riders, providing actionable business recommendations to maximize annual membership conversion.

* **Tools Used:** SQL (Google BigQuery), Tableau, GitHub
* **Methodology:** 6-Phase Data Analysis Process (Ask, Prepare, Process, Analyze, Share, Act)

---

## Phase 1: Ask (Business Task & Scope Definition)

### 1. Business Background
Cyclistic operates a fleet of over 5,800 geotracked bicycles across 690+ stations in Chicago. The existing pricing model offers single-ride passes, full-day passes (classified as **Casual Riders**), and annual subscriptions (classified as **Cyclistic Members**).

Financial analysts concluded that **annual members generate significantly higher profit margins than casual riders**. Marketing Director Lily Moreno decided to focus growth initiatives on converting existing casual users—who already know and trust the service—into high-value annual members rather than solely acquiring all-new leads.

### 2. Business Task
> Analyze Cyclistic's historical bike trip data to identify behavioral patterns distinguishing casual riders from annual members, and develop data-backed marketing strategies to drive annual membership conversion.

### 3. Key Stakeholders
* **Lily Moreno (Director of Marketing):** Leading future digital campaigns and membership initiatives.
* **Cyclistic Executive Team:** Decision-makers approving marketing budget allocation and commercial strategies based on rigorous analytical evidence.
* **Cyclistic Marketing Analytics Team:** Core team responsible for data extraction, hygiene, and baseline performance metrics.

### 4. Guiding Business Questions
1. **How do annual members and casual riders use Cyclistic bikes differently?** *(Primary project scope)*
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

### 5. Hypotheses & Core Analysis Dimensions
| Dimension | Key Metrics | Initial Hypothesis |
| :--- | :--- | :--- |
| **Weekly Cadence** | Total ride counts by day of week | Members ride primarily during weekdays (Mon–Fri), whereas casual users peak heavily on weekends (Sat–Sun). |
| **Trip Duration** | Average and median ride length (minutes) | Casual riders record longer durations per trip (recreational), while members record shorter, consistent commute trips. |
| **Hourly Distribution** | 24-hour trip frequency | Member usage peaks around commuter hours (7–9 AM, 5–7 PM), while casual usage steadily grows through midday and afternoon. |
| **Asset Preference** | Bike type breakdown (classic vs. electric) | Casual riders lean towards electric bikes for leisurely, non-routine outings. |

---

## Phase 2: Prepare (Data Sourcing & Integrity)

- **Data Source:** Cyclistic historical bike trip records (12 consecutive months of public data provided by Motivate International Inc.).
- **Data Volume:** 6,006,904 raw ride records across Chicago.
- **Data Integrity (ROCCC):**
  - **Reliable & Original:** Authentic automated municipal bike-docking transaction logs.
  - **Comprehensive:** Complete timestamp, coordinate, bike type, and user classification attributes.
  - **Current & Cited:** Licensed publicly under the City of Chicago bike-share data license agreement.
  - **Privacy:** Data is strictly anonymized; no Personally Identifiable Information (PII) such as credit cards or member IDs is present.

---

## Phase 3: Process (Data Cleaning & SQL Transformations)

All data ingestion, cleansing, and aggregations were executed in **Google BigQuery**:
1. **Consolidation:** Merged 12 separate monthly tables using `UNION ALL` into a staging environment.
2. **Quality Control & Cleansing:**
   - Excluded invalid records with missing station identifiers or coordinates for location-based analysis.
   - Filtered out negative ride durations (`ended_at < started_at`) and administrative test/dock check records (`ride_length < 1 minute` or `> 1,440 minutes`).
3. **Feature Engineering:**
   - Derived `ride_length_minutes` using `TIMESTAMP_DIFF(ended_at, started_at, SECOND) / 60.0`.
   - Extracted temporal variables: `day_of_week`, `hour_of_day`, and `month`.
   - Aggregated findings into compact datasets for Tableau visualization.

---

## Phase 4: Analyze (Exploratory Data Analysis & Findings)

| Metric / Dimension | Annual Members | Casual Riders |
| :--- | :--- | :--- |
| **Total Trips Volume** | **3,896,783** (64.9%) | **2,110,121** (35.1%) |
| **Average Ride Duration** | **11.9 minutes** (Utility commute) | **17.6 – 20.5 minutes** (Leisure exploration) |
| **Peak Commute Hours** | Bimodal spikes at **8:00 AM** and **5:00 PM** | Gradual afternoon curve peaking **12:00 PM – 5:00 PM** |
| **Peak Days of Week** | Tuesday – Thursday (Workdays) | Saturday & Sunday (Weekends) |
| **Seasonality Trend** | Consistent year-round; moderate winter dip | Highly weather-dependent; summer surge (Jun–Aug) |
| **Top Start Stations** | Transit stations, offices (Canal St, Clinton St) | Lakefront, parks (Navy Pier, Millennium Park) |

---

## Phase 5: Share (Tableau Dashboard)

An interactive multi-metric dashboard was designed in Tableau Public to present the behavioral dichotomy between both customer segments.

🔗 **Live Interactive Dashboard:** [View on Tableau Public](https://public.tableau.com/views/CyclisticBike-ShareCaseStudyUserBehaviorAnalysis_17941103228910/CyclisticBike-ShareAnnualMembersvsCasualRidersAnalysis?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

### Dashboard Highlights:
- **Volume & Trip Length Comparison:** Demonstrates member dominance in ride count alongside casual dominance in trip duration.
- **Hourly & Weekly Curves:** Visualizes the commuter dual-peak curve versus the leisure afternoon/weekend curve.
- **Geographic Station Map:** Displays clear spatial separation: casual riders clustered tightly along the Lake Michigan shoreline, whereas annual members are distributed across commercial and residential transit routes.

---

## Phase 6: Act (Executive Business Recommendations)

1. **Seasonal & Weekend Membership Tier:**
   - *Insight:* Casual riders concentrate heavily on weekends and summer months, avoiding standard annual commitments.
   - *Recommendation:* Introduce a **"Summer Pass"** (June–August) and a **"Weekend Warrior Pass"** with an option to credit pass costs toward a full annual membership.
2. **Geo-Targeted Station Marketing:**
   - *Insight:* Top casual origin points are concentrated at recreational hotspots (Navy Pier, Millennium Park, Lake Shore Dr).
   - *Recommendation:* Deploy QR-code kiosks at these lakefront stations offering immediate on-app signup discounts, paired with geofenced mobile push notifications upon docking.
3. **Ride Duration Value Proposition:**
   - *Insight:* Casual riders average 17–20+ minutes per trip compared to 12 minutes for members.
   - *Recommendation:* Market membership benefits emphasizing extended ride caps (e.g., "First 45 minutes free per ride for members vs. 30 minutes for single passes") to show tangible savings for long leisure trips.
