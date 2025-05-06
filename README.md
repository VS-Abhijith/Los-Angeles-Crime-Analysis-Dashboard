# Los Angeles Crime Analysis Dashboard (2020-2024)

## Overview

This project presents a comprehensive analysis of crime in Los Angeles from January 1, 2020, to December 31, 2024. Built using Tableau, the dashboard reveals crime patterns by time, geography, type, and victim demographics. The dataset is sourced from [data.gov](https://catalog.data.gov/dataset/crime-data-from-2020-to-present), which hosts open records from the Los Angeles Police Department (LAPD).

**🔗 Dashboard Link:** [Tableau Public - Los Angeles Crime Dashboard](https://public.tableau.com/views/LosAngelesCrimeDashboard_17465076259260/LosAngelesCrimeDashboard)

**👤 LinkedIn:** [www.linkedin.com/in/vsabhijith](https://www.linkedin.com/in/vsabhijith)

---

## 🔧 Data Cleaning Process

The dataset initially contained formatting issues, inconsistencies, and missing values. Here's a detailed breakdown of how the data was standardized:

### ✅ Validated Columns

* `**, **`\*\*, **`**, **`**, **`**, **`**, **`**, **`**, **`**, **`**, **`**, **`**, **`**, **`**, \*\*`**, **` — ensured no nulls present.

### 📅 Date and Time Cleaning

* **Date format issues** were addressed using a Python script: mixed formats like `07-07-2020 00:00`, `03/27/2020 12:00:00 AM` were standardized.
* Power Query and native tools failed to fully transform inconsistent date formats, so Python was used.
* ✅ Script: [Date Cleaning Python Colab](https://colab.research.google.com/drive/1pELmkqLBWpPzAmLZoDU2nRfezNExsZi_?usp=sharing)

### 🕒 Time Transformation

* `TIME OCC` values such as `2130` or `0600` were transformed to `21:30`, `06:00` format using Power Query:

```powerquery
Time.FromText(Text.Start(Text.PadStart(Text.From([TIME OCC]), 4, "0"), 2) & ":" & Text.End(Text.PadStart(Text.From([TIME OCC]), 4, "0"), 2))
```

### 🧹 Text Cleanup

* Trimmed all text columns
* Made column headers friendly for visualization tools

### 🕳️ Missing Data Treatment

| Column           | Action Taken                                       |
| ---------------- | -------------------------------------------------- |
| `Vict Age`       | -1 (missing ages; binned under `-5` → Unknown Age) |
| `Vict Sex`       | "Not Available"                                    |
| `Vict Descent`   | "Not Available"                                    |
| `Premis Desc`    | "Not Available"                                    |
| `Premis Cd`      | -1                                                 |
| `Weapon Used Cd` | -1                                                 |
| `Weapon Desc`    | "Not Applicable"                                   |
| `Crm Cd 2/3/4`   | -1                                                 |
| `Cross Street`   | "Not Available"                                    |

Converted cleaned Excel to CSV using pandas:

```python
import pandas as pd

excel_path = "Cleaned_Crime_Data_Standardized.xlsx"
csv_path = "Cleaned_Crime_Data_Standardized.csv"

df = pd.read_excel(excel_path)
df.to_csv(csv_path, index=False)
```

### ❗ Note on Data Quality

* Crime entries from future dates in 2025 were observed; filtered out using a Tableau filter.

---

## 📊 Dashboard Features

### 1. **Top KPIs**

* **Total Crimes:** 1,004,901
* **Average Crimes per Day:** 537.4
* **Crime Rate per 1000 People:** 264.4
* **Crime Clearance Rate:** 8.97%

### 2. **Temporal Analysis**

* **Hourly Distribution:** Crimes peak between 12 PM and 6 PM
* **Weekday Reporting:** Highest on Friday, lowest on Sunday
* **Monthly Trend:** Noticeable drop during pandemic, seasonal surges in summer

### 3. **Geospatial Insights**

* **Crime Cluster Zones:** Central LA, Hollywood, and South LA are hotspots
* **Area-wise Arrest Rate:** Highest in 77th Street and Central Areas

### 4. **Victim Demographics**

* **Victim Age Distribution:** Majority fall between 18–30; `-1` indicates unknown age
* **Victim Gender:** Males represent \~58.6%, Females \~39.8%, Others & Unknown \~1.6%
* **Victim Descent:** Hispanic and White together make up nearly 50%

### 5. **Crime Characteristics**

* **Top Crime Types:** Vehicle theft, Battery (Simple), and Burglary
* **Weapon Usage:** Majority marked as "Not Applicable" — sign of non-violent or data gaps
* **Crime vs Premises:** Streets and dwellings dominate as crime locations
* **Crime vs Time:** Assault and battery dominate evenings

### 6. **Donut Charts & Trends**

* **Part I vs Part II Crimes:** 59.97% Part I (more serious offenses)
* **Arrests vs Non-Arrests:** Only 8.97% led to arrests

### 7. **Outlier Dates**

* **Highest Crime Days:** February 2, 2023 — 929 reports
* **Lowest Crime Days:** December 31, 2024 — 38 reports

---

## 🧠 Insight Opportunities

* **Missing values are features, not bugs:** Consider analyzing why weapon data is missing — perhaps in low-threat scenarios.
* **Part II Crimes lead to fewer arrests:** Target intervention there.
* **Temporal hotspots:** Strategies can be tailored to weekends, and 12 PM–6 PM windows.

---

## 📁 Files

* Tableau Workbook: `Los Angeles Crime Dashboard.twbx`
* PNG Snapshot: `Los Angeles Crime Dashboard.png`
* Cleaned Data CSV: `Cleaned_Crime_Data_Standardized.csv`

---

## 📌 About the Dataset

> This dataset reflects incidents of crime in the City of Los Angeles dating back to 2020. This data is transcribed from original crime reports that are typed on paper and therefore there may be some inaccuracies within the data. Some location fields with missing data are noted as (0°, 0°). Address fields are only provided to the nearest hundred block in order to maintain privacy.

---

## 🚀 Future Scope

* Predictive modeling to forecast crimes by location and time
* Integration with population density, income, or housing data
* Automated alerts for crime pattern shifts

---

## 📎 Citation

**Data Source:** [data.gov - Crime Data from 2020 to Present](https://catalog.data.gov/dataset/crime-data-from-2020-to-present)

---

Feel free to connect with me on [LinkedIn](https://www.linkedin.com/in/vsabhijith) or fork the repo to extend this work!
