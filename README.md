# VoltGrid Energy – Enterprise EV Charging Network Performance Intelligence Platform

## Industry

**Electric Vehicle Charging / Energy / Mobility**

## Project Overview

The **VoltGrid Energy – Enterprise EV Charging Network Performance Intelligence Platform** is a data analytics and business intelligence project designed to analyze the operational, financial, customer, energy, and sustainability performance of an EV charging network.

The project uses **MySQL and SQL** for database creation, data validation, cleaning, transformation, and analysis, and **Microsoft Power BI** for interactive dashboards and business intelligence reporting.

The solution analyzes charging sessions, charging stations, charger types, vehicles, customers, revenue, queue time, maintenance, energy consumption, renewable energy usage, carbon savings, and station performance to identify operational bottlenecks, revenue opportunities, customer experience issues, and sustainability improvements.

> **Data scope:** City, Latitude, and Longitude are intentionally excluded from the dashboard analysis. **State** is used as the geographic/business dimension.

### Business Areas Covered

- Charging session and demand performance
- Charging station operations
- Charger-type performance
- Revenue and financial performance
- Customer experience
- Queue and waiting-time analysis
- Maintenance and uptime
- Energy consumption
- Renewable energy contribution
- Carbon savings
- Station performance and risk

## Project Objectives

- Build a structured relational database for EV charging operations.
- Organize charging-session, station, charger, vehicle, customer, revenue, and sustainability data.
- Analyze charging volume, energy delivered, revenue, and revenue efficiency.
- Measure station uptime, queue time, maintenance, and operational performance.
- Analyze charger type, vehicle type, membership, and payment behavior.
- Evaluate customer ratings and waiting-time patterns.
- Monitor renewable energy contribution and carbon savings.
- Identify underperforming stations and operational risk areas.
- Build interactive Power BI dashboards for management reporting.
- Generate actionable business recommendations.

## Tools & Technologies

| Tool / Technology | Purpose |
| --- | --- |
| **MySQL** | Database creation and data storage |
| **SQL** | Data validation, querying, cleaning, and analysis |
| **Microsoft Power BI** | Interactive dashboard development |
| **DAX** | KPI and calculated measure creation |
| **Power Query** | Data transformation and preparation |
| **CSV** | Dataset source |
| **GitHub** | Version control and documentation |

## Dataset Description

The project uses an **EV Charging Network Enterprise Dataset** containing approximately **200,000 charging-session records**.

### Geographic Fields Excluded

The following fields are intentionally not used in the dashboard:

```text
City
Latitude
Longitude
```

The geographic/business dimension used for analysis is:

```text
State
```

### Main Data Categories

| Category | Examples |
| --- | --- |
| **Session** | Session ID, session start, session end, duration |
| **Station** | Station ID, station name, state, uptime, maintenance |
| **Charging** | Charger type, charger power, fast charging, energy delivered |
| **Vehicle** | Vehicle type, battery capacity, battery levels, battery health |
| **Revenue** | Electricity price, session cost, revenue |
| **Customer** | Queue time, customer rating, membership, payment method |
| **Sustainability** | Renewable energy %, carbon saved |
| **Operations** | Peak hour, traffic, holiday, day of week, month |

## Database Design

The database follows a relational **Star Schema** with the charging-session table acting as the central fact table.

### Fact Table

- `Fact_Charging_Session`

### Dimension Tables

- `Dim_Station`
- `Dim_Charger`
- `Dim_Vehicle`
- `Dim_Date`

### Logical Relationships

```text
                  ┌───────────────┐
                  │   Dim_Date    │
                  └───────┬───────┘
                          │
                          │
┌───────────────┐   ┌─────▼──────────────────┐   ┌───────────────┐
│ Dim_Station   │───│ Fact_Charging_Session  │───│ Dim_Charger   │
└───────────────┘   └─────┬──────────────────┘   └───────────────┘
                          │
                    ┌─────▼────────┐
                    │ Dim_Vehicle  │
                    └──────────────┘
```

## SQL Analysis

SQL was used to create the database, create tables, import data, validate records, clean the dataset, and support business analysis.

### Database Creation

```sql
CREATE DATABASE EV_Charging_Analytics;
USE EV_Charging_Analytics;
```

### SQL Analysis Areas

- Charging session volume
- Revenue analysis
- Energy analysis
- Station performance
- Charger performance
- Queue-time analysis
- Maintenance analysis
- Customer rating analysis
- Peak-hour analysis
- Renewable energy analysis
- Carbon savings
- Data validation
- Station risk analysis

### Data Validation

Typical validation checks include:

```sql
-- Row count
SELECT COUNT(*) 
FROM Fact_Charging_Session;

-- Duplicate sessions
SELECT Session_ID, COUNT(*)
FROM Fact_Charging_Session
GROUP BY Session_ID
HAVING COUNT(*) > 1;

-- NULL validation
SELECT COUNT(*)
FROM Fact_Charging_Session
WHERE Session_ID IS NULL;

-- Negative-value validation
SELECT COUNT(*)
FROM Fact_Charging_Session
WHERE Energy_Delivered_kWh < 0
   OR Revenue_USD < 0;
```

## Power BI Dashboard

Four interactive Power BI dashboards were developed.

### Dashboard 1 — Executive Overview

- Total Sessions
- Total Stations
- Total Energy Delivered
- Total Revenue
- Average Revenue per Session
- Average Queue Time
- Average Customer Rating
- Monthly Revenue Trend
- Sessions vs Energy Trend
- Revenue by State
- Revenue by Charger Type
- Sessions by Vehicle Type
- Revenue by Membership Type

### Dashboard 2 — Charging Operations & Station Performance

- Total Stations
- Average Station Uptime
- Average Queue Time
- Maintenance Sessions
- Fast Charging %
- Top Stations by Charging Sessions
- Station Uptime vs Queue Time
- Station Performance Matrix
- Maintenance Impact
- Peak-Hour Sessions

### Dashboard 3 — Revenue & Customer Analytics

- Total Revenue
- Average Revenue per Session
- Average Session Cost
- Revenue per kWh
- Average Customer Rating
- Monthly Revenue Trend
- Revenue by Charger Type
- Revenue by Membership Type
- Revenue by Vehicle Type
- Payment Method Distribution
- Queue Time vs Customer Rating

### Dashboard 4 — Sustainability & Network Risk

- Total Energy Delivered
- Average Energy per Session
- Renewable Energy %
- Total Carbon Saved
- Average Battery Health
- Energy Delivered by Charger Type
- Monthly Energy Trend
- Renewable Energy Contribution
- Carbon Saved by State
- Station Performance Score
- Station Risk Matrix

## Key KPIs

| KPI | Business Purpose |
| --- | --- |
| **Total Sessions** | Measures charging demand |
| **Total Stations** | Measures network size |
| **Total Energy Delivered** | Measures energy consumption |
| **Total Revenue** | Measures financial performance |
| **Average Revenue / Session** | Measures revenue efficiency |
| **Average Queue Time** | Measures customer waiting time |
| **Average Customer Rating** | Measures customer satisfaction |
| **Average Station Uptime** | Measures operational reliability |
| **Fast Charging %** | Measures fast-charging adoption |
| **Revenue / kWh** | Measures charging revenue efficiency |
| **Renewable Energy %** | Measures sustainability |
| **Total Carbon Saved** | Measures environmental impact |
| **Average Battery Health** | Measures vehicle/battery condition |
| **Station Performance Score** | Measures overall station performance |
| **Station Risk** | Identifies stations requiring attention |

## Key DAX Measures

### Total Sessions

```DAX
Total Sessions =
DISTINCTCOUNT(
    Fact_Charging_Session[Session_ID]
)
```

### Total Revenue

```DAX
Total Revenue =
SUM(
    Fact_Charging_Session[Revenue_USD]
)
```

### Total Energy Delivered

```DAX
Total Energy Delivered =
SUM(
    Fact_Charging_Session[Energy_Delivered_kWh]
)
```

### Average Revenue per Session

```DAX
Average Revenue per Session =
DIVIDE(
    [Total Revenue],
    [Total Sessions],
    0
)
```

### Average Queue Time

```DAX
Average Queue Time =
AVERAGE(
    Fact_Charging_Session[Queue_Time_Min]
)
```

### Average Customer Rating

```DAX
Average Customer Rating =
AVERAGE(
    Fact_Charging_Session[Customer_Rating]
)
```

### Average Station Uptime

```DAX
Average Station Uptime =
AVERAGE(
    Fact_Charging_Session[Station_Uptime_Percentage]
)
```

### Fast Charging %

```DAX
Fast Charging % =
DIVIDE(
    CALCULATE(
        [Total Sessions],
        Fact_Charging_Session[Fast_Charging_Flag] = 1
    ),
    [Total Sessions],
    0
)
```

### Revenue per kWh

```DAX
Revenue per kWh =
DIVIDE(
    [Total Revenue],
    [Total Energy Delivered],
    0
)
```

### Total Carbon Saved

```DAX
Total Carbon Saved =
SUM(
    Fact_Charging_Session[Carbon_Saved_kg]
)
```

### Average Renewable Energy %

```DAX
Average Renewable Energy % =
AVERAGE(
    Fact_Charging_Session[Renewable_Energy_Percentage]
)
```

## Key Business Questions

### Revenue

- Which state generates the highest revenue?
- Which charger type generates the most revenue?
- Which membership type generates the highest revenue?
- How is revenue changing over time?
- Which charger types provide the best revenue efficiency?

### Operations

- Which stations have the highest charging activity?
- Which stations have the longest queues?
- Which stations have low uptime?
- How does maintenance affect queue time?
- When is charging demand highest?
- Which stations require operational attention?

### Customer

- Which vehicle types use the network most?
- Which membership type generates the most revenue?
- Which payment methods are most popular?
- Does queue time affect customer ratings?

### Energy & Sustainability

- Which charger type delivers the most energy?
- What is the average energy delivered per session?
- What percentage of energy is renewable?
- How much carbon is saved?
- Which states contribute the most carbon savings?

### Risk

- Which stations have high queues and low uptime?
- Which stations have low customer ratings?
- Which stations have weak overall performance?
- Where should management prioritize operational improvements?

## Key Insights

1. **Revenue Performance:** Revenue analysis provides visibility into the financial contribution of states, charger types, vehicle types, and membership segments.
2. **Charging Demand:** Session trends identify periods of high and low network demand.
3. **Station Efficiency:** Uptime and queue-time analysis helps identify operational bottlenecks.
4. **Customer Experience:** Queue time and customer-rating analysis helps evaluate service quality.
5. **Charger Performance:** Charger-type analysis helps identify charging technologies with strong demand and revenue.
6. **Maintenance Impact:** Maintenance analysis helps understand operational effects on charging availability and customer waiting.
7. **Energy Management:** Energy-delivered analysis supports charging-capacity and energy planning.
8. **Sustainability:** Renewable-energy and carbon-saving metrics provide visibility into environmental performance.
9. **Station Risk:** Station-level performance scoring helps prioritize stations requiring operational review.
10. **Business Optimization:** Combining operational, financial, customer, and sustainability metrics supports data-driven network planning.

## Project Workflow

```text
Raw Dataset
     ↓
Data Inspection
     ↓
Data Cleaning & Validation
     ↓
MySQL Database Creation
     ↓
Table Creation
     ↓
SQL Data Validation
     ↓
SQL Analysis
     ↓
Power BI Data Connection
     ↓
Power Query Transformation
     ↓
DAX Measures & KPIs
     ↓
Dashboard Development
     ↓
Business Insights
     ↓
Recommendations
```

## Repository Structure

```text
VoltGrid-EV-Charging-Network-Analytics/
│
├── README.md
│
├── sql/
│   └── ev_charging_network_analytics.sql
│
├── powerbi/
│   └── EV_Charging_Network_Dashboard.pbix
│
├── data/
│   └── README.md
│
├── screenshots/
│   ├── Executive_Overview.png
│   ├── Charging_Operations.png
│   ├── Revenue_Customer.png
│   └── Sustainability_Risk.png
│
└── docs/
    └── ER_Diagram.png
```

## Dashboard Screenshots

The project contains four Power BI dashboard pages:

1. **Executive Overview**
2. **Charging Operations & Station Performance**
3. **Revenue & Customer Analytics**
4. **Sustainability & Network Risk**

## How to Run the Project

### 1. Clone the Repository

```bash
git clone <your-github-repository-url>
cd VoltGrid-EV-Charging-Network-Analytics
```

### 2. Create the MySQL Database

Open **MySQL Workbench** and execute:

```sql
CREATE DATABASE EV_Charging_Analytics;
USE EV_Charging_Analytics;
```

### 3. Run the SQL Script

Run the SQL script from:

```text
sql/ev_charging_network_analytics.sql
```

### 4. Load the Dataset

Import the EV charging dataset into the MySQL staging/fact structure.

> City, Latitude, and Longitude are intentionally excluded from the dashboard analysis.

### 5. Validate the Database

```sql
SHOW TABLES;
```

Verify row counts, NULL values, duplicates, invalid values, and date ranges.

### 6. Open Power BI

Open:

```text
powerbi/EV_Charging_Network_Dashboard.pbix
```

### 7. Configure the Data Source

Connect Power BI to the MySQL database and update the required server/database connection details.

### 8. Refresh the Dataset

Click **Refresh** in Power BI.

### 9. Explore the Dashboards

```text
Executive Overview
        ↓
Charging Operations & Station Performance
        ↓
Revenue & Customer Analytics
        ↓
Sustainability & Network Risk
```

## Dashboard Theme

The dashboard uses a modern EV technology theme.

| Element | HEX |
| --- | --- |
| Background | `#0B1220` |
| Card Background | `#111C2E` |
| Primary Accent | `#22C55E` |
| Secondary Accent | `#06B6D4` |
| Warning | `#F59E0B` |
| Critical | `#EF4444` |
| Main Text | `#F8FAFC` |
| Secondary Text | `#94A3B8` |

## Recommendations

- Increase charging capacity at high-demand stations.
- Investigate stations with long queue times.
- Improve maintenance at low-uptime stations.
- Optimize charger allocation based on demand.
- Monitor customer ratings to improve service quality.
- Use revenue-per-kWh analysis to evaluate charger economics.
- Increase renewable-energy usage where feasible.
- Prioritize low-performing stations for operational review.
- Use peak-hour analysis for capacity planning.
- Monitor station risk regularly through the Power BI dashboard.

## Future Enhancements

- Real-time charging-session monitoring
- EV charging demand forecasting
- Machine-learning-based station demand prediction
- Queue-time prediction
- Predictive maintenance
- Dynamic charger allocation
- Customer churn prediction
- Automated station-risk alerts
- Automated Power BI refresh
- EV charging API integration
- Advanced revenue and profitability analysis

## Author

### **Nithyanandhan K (AF05258492)**

**Project:** VoltGrid Energy – Enterprise EV Charging Network Performance Intelligence Platform

**Industry:** Electric Vehicle Charging / Energy / Mobility

**Technologies:** MySQL | SQL | Power BI | DAX | Power Query | Python | GitHub

**Project Focus:** Data Analytics | Business Intelligence | Operations Analytics | Revenue Analytics | Customer Analytics | Sustainability Analytics

## License

This project is created for **educational, portfolio, and data analytics demonstration purposes**.
