# BeanScore: Coffee Quality & Sensory Analysis Dashboard
 
## 🔷 Project Overview
This project focuses on analyzing **Arabica coffee quality data** from the Coffee Quality Institute (CQI) to uncover insights related to **sensory attributes, processing methods, regional differences, defects, and altitude influence**.

An **interactive Power BI dashboard** was developed using a structured **star schema model** and DAX measures to enable dynamic filtering, drill-down analysis, and actionable insights for growers, roasters, and buyers.

---

## 🔷 Dataset Information 
* **Source:** Coffee Quality Institute (CQI)
* **Total Records:** ~1,300 samples
* **Columns:** 30+

### Key Features:
* **Sensory Attributes** → Aroma, Flavor, Acidity, Body, Balance, Aftertaste, Sweetness, Clean Cup, Uniformity, Overall
* **Defects** → Category One, Category Two, Quakers
* **Production Info** → Processing Method, Variety, Bag Weight, Moisture %
* **Geography** → Country, Region, Altitude
* **Target Metric** → Total Cup Points (sum of 10 sensory attributes)

---

## 🔷 Data Preparation

### ✔ Data Wrangling
* Checked for null values and cleaned missing entries
* Normalized sensory scores (scale 0–10)
* Structured dataset for star schema modeling

### ✔ Feature Engineering
* **Altitude Band** → 0–1000m, 1000–1500m, 1500–2000m, 2000m+
* **Defect Category Labels** → Category One vs Category Two
* **Year Buckets** → Harvest Year grouped for temporal trends

---

## 🔷 Data Modeling (Star Schema)

### ⭐ Fact Table: `df_arabica_clean`
Contains:
* ID, Lot Number, Country, Region, Processing Method, Variety
* Sensory attributes (10), Total Cup Points
* Category One defects, Category Two defects, Total Defects
* Number of Bags, Weight of Bag (Kg), Altitude, Harvest Year

### Dimension Tables:
* **Dim_Region** → Country, Region, Avg Altitude (Hierarchy: Country > Region)
* **Dim_Processing_Method** → Processing Method
* **Dim_Variety** → Variety
* **Dim_Date** → Harvest Year, Grading Date

---

## 🔷 Key Metrics (DAX)
* **Avg Cup Score** = `AVERAGE([Total Cup Points])`
* **Top Region Score** = `MAXX(SUMMARIZE(Region, [AvgCupScore]), [AvgCupScore])`
* **Top Region Name** = `MAXX(SUMMARIZE('df_arabica_clean', 'df_arabica_clean'[Region], "RegionAvg", [Avg Cup Score]), IF([RegionAvg] = [TopRegionScore], 'df_arabica_clean'[Region]))`

### Screenshot/Demos:
* Example:  ![Dashboard Preview](https://github.com/Amol9805/BeanScore-Quality-Index-and-Sensory-analysis-Dashboard/blob/main/Data%20Modelling.png)
---

# Dashboard Pages & Visualizations

---

## 🟣 1. Sensory Attribute Analysis
Focuses on identifying sensory drivers of cup quality.

### Visuals Used:
* **Bar Chart** → Avg score per attribute
* **Radar Chart** → Sensory profiles by processing method
* **Table** → Attribute averages vs Total Cup Points
* **KPI Card** → Highest scoring attribute

### Insights:
* Aroma & Flavor are strongest predictors of quality
* Uniformity, Clean Cup, and Sweetness are consistently maxed


### Screenshot/Demos:
* Example:  ![Dashboard Preview](https://github.com/Amol9805/BeanScore-Quality-Index-and-Sensory-analysis-Dashboard/blob/main/Sensory%20Analysis.png)
---

## 🟠 2. Processing Method Analysis
Compares methods and their impact on quality.

### Visuals Used:
* **Bar Chart** → Avg Cup Score by Method
* **Scatter Plot** → Defects vs Cup Score by Method
* **Donut Chart** → Defect share by Method
* **Combo Chart** → Cup Score vs Defects

### Insights:
* Anaerobic methods yield high scores but risk defects
* Washed/Wet is stable but not always top-scoring


### Screenshot/Demos:
* Example:  ![Dashboard Preview](https://github.com/Amol9805/BeanScore-Quality-Index-and-Sensory-analysis-Dashboard/blob/main/ProcessingMethod.png)
---

## 🟢 3. Regional Differences
Highlights geography and altitude influence.

### Visuals Used:
* **Map** → Avg Cup Score by Country
* **Drill-down Bar Chart** → Country > Region vs Avg Cup Score
* **Combo Chart** → Region vs Avg Cup Score + Avg Altitude
* **KPI Card** → Top scoring region

### Insights:
* Ethiopia, Tanzania, and Guatemala consistently lead
* Altitude positively correlates with cup score

### Screenshot/Demos:
* Example:  ![Dashboard Preview](https://github.com/Amol9805/BeanScore-Quality-Index-and-Sensory-analysis-Dashboard/blob/main/Regional%20Analysis.png)
---

## 🟡 4. Defects vs Quality
Analyzes how defects reduce scores.

### Visuals Used:
* **Scatter Plot** → Total Defects vs Avg Cup Score
* **Bar Chart** → Avg Cup Score by Defect Category
* **Heatmap** → Method × Defect Level vs Avg Cup Score
* **KPI Card** → Lowest scoring method due to defects

### Insights:
* Category One defects are the most damaging
* Semi-Lavado and Pulped Natural methods are most vulnerable


### Screenshot/Demos:
* Example:  ![Dashboard Preview](https://github.com/Amol9805/BeanScore-Quality-Index-and-Sensory-analysis-Dashboard/blob/main/Variety%20and%20Defect%20Analysis.png)
---

## 🎯 Overall Project Insights
1. **Quality Drivers:** Aroma, Flavor, and Acidity are the strongest sensory predictors.
2. **Processing Trade‑offs:** Innovative methods (Anaerobic, Honey) can yield high scores but increase defect risk.
3. **Regional Strengths:** Ethiopia, Tanzania, and Guatemala are consistently strong; Mexico’s Zongolica region is a hidden gem.
4. **Defect Impact:** Category One defects are the most damaging; reducing them yields immediate score improvements.
5. **Temporal Trends:** Quality fluctuates by harvest year — external factors like climate and processing practices matter.
6. **Variety Profiles:** Gesha and Bourbon lead; hybrids need defect management.
7. **Altitude Effect:** Higher altitudes consistently correlate with better cup scores.

---

## 🚀 Recommendations
* **Growers:** Focus on reducing Category One defects; experiment with fermentation to enhance aroma/flavor.
* **Roasters/Buyers:** Prioritize high‑altitude regions and heirloom varieties; monitor harvest year trends.
* **CQI/Industry:** Expand training on defect reduction and processing innovation; invest in altitude‑specific best practices.

---

## 🔷 Interactivity Features
* **Slicers:** Country, Region, Processing Method, Variety, Harvest Year
* **ToolTips:** Interactive Overall information
* **Drill‑Down:** Country → Region hierarchy

---
## 🔷 Tools & Technologies
* **Power BI** → Dashboard & Visualization
* **DAX** → Measures & Calculations
* **Power Query** → Data Wrangling
* **CQI Dataset** → Coffee Quality Institute

---

## 🔷 Conclusion
This project demonstrates how Power BI can transform raw coffee quality data into meaningful insights through data modeling, visualization, and interactivity. The dashboard enables stakeholders to monitor quality drivers, understand regional strengths, and optimize processing strategies.

---

## 🔷 Future Enhancements
* Predictive modeling (regression/ML) to forecast cup scores
* Soil and genetic factor integration
