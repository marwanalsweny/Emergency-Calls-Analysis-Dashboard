# 🚨 Incident Tracking & Spatial Analytics Dashboard

An interactive and comprehensive **Power BI** incident management and spatial intelligence dashboard, developed to track, visualize, and analyze safety, operational, or traffic incidents across geographic locations and timeframes.

---

## 📌 Project Overview

This project provides public safety officials, operations teams, and decision-makers with real-time situational awareness and historical incident trends. By combining geospatial mapping, incident severity scoring, and temporal tracking, the dashboard enables proactive risk mitigation and resource allocation.

---

## 📑 Dashboard Architecture & Pages

The dashboard is structured into targeted analytical modules[cite: 2]:

1. **Home / Executive Summary (`Home Page`):**[cite: 2]
   * High-level KPI metrics: Total Incidents, Open vs. Resolved Cases, Average Resolution Time, and Severity Breakdown.
   * High-level temporal trends and status distribution.

2. **Geospatial & Location Analysis (`Location Page`):**[cite: 2]
   * Map-based spatial distribution of reported incidents across regions, districts, and checkpoints.
   * Incident frequency and severity categorization by location.

3. **Density & Hotspot Analysis (`Heatmap Page`):**[cite: 2]
   * Visual density heatmap highlighting critical risk zones and high-incident clusters.
   * Time-of-day and day-of-week pattern recognition for targeted intervention.

4. **Detailed Log & Timeline (`Recent Incident Page`):**[cite: 2]
   * Granular log of recent incidents with dynamic filtering by status, priority, and category.
   * Case-level drill-through for operational investigations.

---

## 🛠️ Tools & Technical Workflow

* **Microsoft Power BI Desktop:** Visual hierarchy design, navigation buttons, and responsive cross-filtering[cite: 2].
* **Power Query (ETL):** Data cleansing, type transformation, datetime standardization, and geographic coordinate validation.
* **Data Modeling:** Star Schema design linking incident fact tables with Date, Location, and Category dimensions[cite: 2].
* **DAX (Data Analysis Expressions):** Custom business metrics, dynamic ranking, and time intelligence.

---

## 💡 Key DAX Measures

dax
// Total Incidents Count
Total Incidents = COUNTROWS('Incidents')

// Open Incidents
Open Incidents = 
CALCULATE(
    COUNTROWS('Incidents'),
    'Incidents'[Status] = "Open"
)

// Critical Incidents Rate
Critical Incident Rate = 
DIVIDE(
    CALCULATE(COUNTROWS('Incidents'), 'Incidents'[Severity] = "Critical"),
    [Total Incidents],
    0
)

// Incidents Month-over-Month Growth
Incidents MoM Growth = 
VAR CurrentMonth = [Total Incidents]

Author
Marwan Hamdy Alsweny - Data Analyst & BI Developer
VAR PriorMonth = CALCULATE([Total Incidents], DATEADD('Date'[Date], -1, MONTH))
RETURN
DIVIDE(CurrentMonth - PriorMonth, PriorMonth, 0)
