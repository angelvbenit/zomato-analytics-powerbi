# Zomato Global Restaurant Analytics | Power BI Dashboard

![Power BI](https://img.shields.io/badge/Power_BI-Data_Visualization-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data_Analysis_Expressions-0078D4?style=for-the-badge)
![PowerQuery](https://img.shields.io/badge/Power_Query-ETL-404040?style=for-the-badge)

A high-performance, dark-themed Power BI dashboard analyzing global restaurant data from Zomato. This project focuses on end-to-end data engineering—from ETL and currency normalization to advanced time intelligence and interactive storytelling.

## Dashboard Preview

| **Page 1: Executive Overview** | **Page 2: Deep Dive Analysis** |
| :--- | :--- |
| ![Page 1](https://github.com/angelvbenit/zomato-analytics-powerbi/blob/main/PAGE1.png?raw=true) | ![Page 2](https://github.com/angelvbenit/zomato-analytics-powerbi/blob/main/PAGE2.png?raw=true) |

---

## Key Features

* **Currency Normalization:** Automated conversion of local restaurant costs (15+ currencies) into a unified **USD Metric** for global benchmarking.
* **Two-Page Interactive Navigation:** User-friendly interface utilizing **Button Navigation** to toggle between high-level KPIs and granular data.
* **Advanced Time Intelligence:** Custom Calendar table supporting standard and **Financial Year** (April-March) reporting.
* **Aesthetic UI:** "Insanely cool" dark-mode design with Zomato-brand accent coloring (#CB202D) and glowing area charts for modern visual appeal.
* **Price Segmentation:** Dynamic grouping of restaurants into Price Buckets (Cheap Eats, Mid-Range, Expensive, Luxury).

---

## Data Engineering & ETL (Power Query)

The project follows a rigorous data preparation process to ensure accuracy:

1.  **Data Loading:** Imported three core datasets: `Main`, `Country`, and `Currency`.
2.  **Date Reconstruction:** Combined separate Year, Month, and Day columns using custom M-code: 
    * `#date([Year Opening], [Month Opening], [Day Opening])`
3.  **Relational Merging:** Performed a Left Outer Join between the `Main` table and `Currency` table to pull in exchange rates.
4.  **Calculated Columns:** Created `Cost in USD` by multiplying `Average_Cost_for_two` with the `USD Rate`.
5.  **Clean-up:** Removed null values from dimensional tables and standardized data types (Rating to Decimal, Cost to Whole Number).

---

## Data Modeling

* **Schema:** Star Schema.
* **Primary Table:** `Main` (Fact table containing restaurant transactions).
* **Dimensions:** * `Country` linked via `CountryCode` (Many-to-One).
    * `Calendar` linked via `OpeningDate` (Many-to-One).
* **Cardinality:** Enforced strict Many-to-One (*:1) relationships with single cross-filter direction for optimal performance.

---

## Advanced DAX Measures

The following key measures were developed to power the visuals:

* **Core Metrics:**
    * `Total Restaurants = DISTINCTCOUNT('Main'[RestaurantID])`
    * `Average Rating = AVERAGE('Main'[Rating])`
    * `Countries Covered = DISTINCTCOUNT('Country'[Countryname])`
* **Engagement Analysis:**
    * `Table Booking Count = CALCULATE([Total Restaurants], 'Main'[Has_Table_booking] = "Yes")`
    * `% Table Booking = DIVIDE([Table Booking Count], [Total Restaurants], 0)`
* **Custom Grouping:**
    * `Price_Buckets = SWITCH(TRUE(), [Cost in USD] <= 10, "Cheap Eats", [Cost in USD] <= 30, "Mid-Range", ...)`

---

## Dashboard Breakdown

### **Page 1: Executive Overview**
* **KPI Header:** 6 high-impact cards highlighting global reach (Cuisines, Cities, Countries, and Costs).
* **Global Footprint:** A dark-style map showing restaurant density by country.
* **Growth Trend:** An area chart showing restaurant openings over time with a red "neon" glow effect.
* **Cuisine Mix:** A TreeMap identifying the top 10 most popular cuisines.

### **Page 2: Deep Dive Analysis**
* **Price Bucket Analysis:** A breakdown of how restaurants are distributed across cost segments.
* **Rating Distribution:** A column chart displaying volume across various rating scores.
* **Popularity Ranking:** A horizontal bar chart identifying the Top 10 Restaurants by total user votes.
* **Slicer Controls:** Dynamic filtering by Country, Year, and Price Bucket.

---

## Repository Structure

* `Power BI Dashboard.pbix`: The source Power BI file.
* `PAGE1.png` / `PAGE2.png`: Screenshots of the dashboard pages.
* `Datasets/`: Source CSV/Excel files used for the analysis.

---

## Setup Instructions
1.  Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
2.  Clone this repository to your local machine.
3.  Open the `Power BI Dashboard.pbix` file.
4.  If prompted, update the data source paths to point to the files in the `/Datasets` folder.

---

**Developed by:** [Angel Benit Veronica]  
**Objective:** Created as a portfolio project to demonstrate expertise in Power BI, DAX, and Data Storytelling.
