# 🏨 AtliQ Hotels Data Analysis — Python
![Python](https://img.shields.io/badge/Python-Data%20Analysis-3776FF)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Manipulation-9B59B6)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Analysis-00B8D9)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-FF1493)
![Jupyter Notebook](https://img.shields.io/badge/Jupyter%20Notebook-Development-FF8C00)
![CSV](https://img.shields.io/badge/CSV-Data%20Source-00C853)


An end-to-end **Data Analytics project using Python** to analyze hotel bookings, occupancy, revenue, customer ratings, and booking channels for **AtliQ Hotels**, a luxury and business hotel chain operating across major Indian cities.

The project focuses on identifying patterns behind the hotel's business performance and generating actionable insights from booking and occupancy data.

---

## 🔍 Project at a Glance

|   🏨 Domain   | 🏢 Industry | 📊 Booking Records | 📁 Source Files |
| :-----------: | :---------: | :----------------: | :-------------: |
| *Hospitality* |   *Hotels*  |       *134K+*      |     *6 CSVs*    |

| 🏙️ Cities | 🏨 Properties | 🛏️ Room Categories | 💰 Revenue Analyzed |
| :--------: | :-----------: | :-----------------: | :-----------------: |
|     *4*    |      *7*      |         *4*         |      *₹1.71B+*      |

| 📅 Analysis Period | 🧹 Data Preparation |           📈 Key Analysis Areas          | 💻 Primary Tool |
| :----------------: | :-----------------: | :--------------------------------------: | :-------------: |
|  *May – Aug 2022*  |   *Pandas + NumPy*  | *Occupancy, Revenue, Ratings & Bookings* |     *Python*    |


---

## 📌 Problem Statement

AtliQ Hotels is experiencing a **decline in business performance**. To understand the reasons behind this decline, booking and hotel data covering **May 2022 to July 2022** was provided, along with additional booking data for **August 2022**.

The objective of this analysis is to:

* Understand booking and revenue performance
* Analyze hotel occupancy across cities and room types
* Compare weekday and weekend occupancy
* Identify high- and low-performing properties
* Evaluate revenue contribution from different booking platforms
* Analyze customer ratings across cities
* Prepare the data for further business analysis

---

## 🎯 Project Objective

The analysis follows a simple business-focused approach:

**Data → Clean → Transform → Analyze → Identify Insights**

The main questions explored in the project include:

1. What is the average occupancy across different room categories?
2. Which cities have the highest occupancy?
3. Is occupancy better on weekdays or weekends?
4. How does occupancy vary across cities in June 2022?
5. How can the new August data be incorporated into the existing dataset?
6. Which cities generate the most realized revenue?
7. How does realized revenue change month by month?
8. Which hotel properties generate the most revenue?
9. Which cities have the highest average customer ratings?
10. Which booking platforms contribute the most realized revenue?

---

## 📂 Dataset & Data Sources

The project uses **5 primary CSV files**:

| File                           | Description                                                              |
| ------------------------------ | ------------------------------------------------------------------------ |
| `dim_date.csv`                 | Date, month, week number, and weekday/weekend information                |
| `dim_hotels.csv`               | Hotel/property details including property name, category, and city       |
| `dim_rooms.csv`                | Room category and room class mapping                                     |
| `fact_aggregated_bookings.csv` | Daily successful bookings and room capacity                              |
| `fact_bookings.csv`            | Booking-level information including booking status, ratings, and revenue |

An additional file was provided for August:

| File                  | Description                                 |
| --------------------- | ------------------------------------------- |
| `new_data_august.csv` | New aggregated booking data for August 2022 |

### Data Coverage

* **134,590 booking records** in the original bookings dataset
* **9,200 aggregated booking records** before cleaning
* **4 cities:** Mumbai, Delhi, Hyderabad, and Bangalore
* **3 months:** May, June, and July 2022
* Additional **August 2022** booking data
* **4 room categories:** RT1, RT2, RT3, and RT4
* **7 booking platforms**

---

## 🛠️ Tools & Technologies

| Tool / Library | Purpose                                                 |
| -------------- | ------------------------------------------------------- |
| 🐍 Python      | Data analysis and transformation                        |
| 🐼 Pandas      | Data loading, cleaning, grouping, merging, and analysis |
| 🔢 NumPy       | Numerical operations and array manipulation             |
| 📊 Matplotlib  | Data visualization                                      |

### Python Techniques Used

* DataFrame exploration
* Descriptive statistics
* Filtering and conditional analysis
* `groupby()` and aggregation
* Data merging and concatenation
* Missing-value handling
* Outlier detection
* Datetime conversion
* Feature creation
* Bar charts and pie charts

---

## 🧹 Data Cleaning & Preparation

The raw data contained several quality issues that were addressed before analysis.

### 1. Invalid Guest Counts

The `no_guests` column contained records with zero or negative guest counts.

These records were removed because they represented invalid booking information.

**Before cleaning:** 134,590 records
**After removing invalid guest counts:** 134,578 records

---

### 2. Revenue Outliers

Extreme values were identified in the `revenue_generated` column.

The project used the **mean + 3 × standard deviation** approach to determine an upper threshold.

Five unusually high values were identified and removed.

The `revenue_realized` column was also checked for unusually high values. The analysis found that the high values were associated with **RT4 / Presidential rooms**, so they were retained rather than incorrectly removing valid high-value bookings.

---

### 3. Missing Values

The booking dataset contained missing values primarily in:

* `ratings_given`

The aggregated booking dataset contained **2 missing values in `capacity`**.

These capacity values were filled using the mean capacity:

```python
df_agg_bookings['capacity'].fillna(
    df_agg_bookings['capacity'].mean(),
    inplace=True
)
```

---

### 4. Invalid Booking Capacity Records

Six records contained more successful bookings than the available capacity.

These records were removed because:

```text
successful_bookings > capacity
```

This reduced the aggregated bookings dataset from **9,200 to 9,194 records**.

---

## 🔄 Data Transformation

Several transformations were performed to make the data suitable for analysis.

### Occupancy Percentage

A new `Occupancy_pct` column was created using:

```python
Occupancy_pct = successful_bookings / capacity × 100
```

This provided a consistent measure for comparing hotel and room performance.

### Datetime Conversion

Date fields stored as text were converted into proper datetime format using Pandas.

This enabled analysis by:

* Month
* Date
* Week
* Weekday vs. weekend

### Dataset Integration

Multiple datasets were merged using common identifiers such as:

* `property_id`
* `room_category`
* `check_in_date`

The August dataset was also appended to the existing aggregated booking data.

After combining the existing data with August records, the final dataset contained **9,201 records**.

---

# 📊 Analysis & Key Insights

## 1. 🛏️ Occupancy by Room Class

Average occupancy across the four room classes was:

| Room Class   | Average Occupancy |
| ------------ | ----------------: |
| Presidential |        **59.28%** |
| Premium      |        **58.03%** |
| Elite        |        **58.01%** |
| Standard     |        **57.89%** |

The **Presidential room class** recorded the highest average occupancy, while **Standard rooms** had the lowest.

The difference between room classes was relatively small, with all four remaining close to the 58–59% range.

---

## 2. 📍 Occupancy by City

Average occupancy across the four cities:

| City      | Average Occupancy |
| --------- | ----------------: |
| Delhi     |        **61.51%** |
| Hyderabad |        **58.12%** |
| Mumbai    |        **57.91%** |
| Bangalore |        **56.33%** |

### Key Finding

**Delhi recorded the highest average occupancy at 61.51%**, while **Bangalore recorded the lowest at 56.33%**.

This highlights a noticeable difference in occupancy performance between cities.

---

## 3. 📅 Weekday vs. Weekend Occupancy

The analysis found a significant difference between weekday and weekend occupancy:

| Day Type | Average Occupancy |
| -------- | ----------------: |
| Weekday  |        **51.81%** |
| Weekend  |        **73.96%** |

### Key Finding

Weekend occupancy was substantially higher than weekday occupancy.

This indicates that AtliQ Hotels experiences considerably stronger demand during weekends compared with weekdays.

---

## 4. 🗓️ June 2022 Occupancy by City

During June 2022:

| City      | Average Occupancy |
| --------- | ----------------: |
| Delhi     |        **61.46%** |
| Mumbai    |        **57.79%** |
| Hyderabad |        **57.69%** |
| Bangalore |        **55.85%** |

### Key Finding

Delhi continued to lead occupancy performance in June, while Bangalore remained the lowest-performing city among the four.

---

## 5. 💰 Revenue by City

Total realized revenue during the analyzed booking period:

| City      | Revenue Realized |
| --------- | ---------------: |
| Mumbai    |  **668,569,251** |
| Bangalore |  **420,383,550** |
| Hyderabad |  **325,179,310** |
| Delhi     |  **294,404,488** |

### Key Finding

**Mumbai generated the highest realized revenue**, followed by Bangalore, Hyderabad, and Delhi.

An important observation is that **Delhi had the highest average occupancy but did not generate the highest total realized revenue**. This shows why occupancy and revenue need to be evaluated together rather than using occupancy alone as a measure of business performance.

---

## 6. 📈 Month-by-Month Revenue

Realized revenue by month:

| Month     | Revenue Realized |
| --------- | ---------------: |
| May 2022  |   **60,961,428** |
| June 2022 |   **52,903,014** |
| July 2022 |   **60,278,496** |

### Key Finding

Revenue decreased from May to June and then increased again in July.

* **May:** Highest revenue
* **June:** Lowest revenue
* **July:** Revenue recovered close to the May level

---

## 7. 🏨 Revenue by Hotel Property

| Hotel Property | Revenue Realized |
| -------------- | ---------------: |
| Atliq Exotica  |   **32,436,799** |
| Atliq Palace   |   **30,945,855** |
| Atliq City     |   **29,047,727** |
| Atliq Bay      |   **26,936,115** |
| Atliq Blu      |   **26,459,751** |
| Atliq Grands   |   **21,644,446** |
| Atliq Seasons  |    **6,672,245** |

### Key Finding

**Atliq Exotica generated the highest realized revenue**, while **Atliq Seasons generated the lowest** among the properties analyzed.

---

## 8. ⭐ Average Customer Rating by City

| City      | Average Rating |
| --------- | -------------: |
| Delhi     |       **3.79** |
| Hyderabad |       **3.65** |
| Mumbai    |       **3.63** |
| Bangalore |       **3.41** |

### Key Finding

Delhi recorded the highest average customer rating at **3.79**, while Bangalore had the lowest at **3.41**.

Bangalore therefore stands out as an area where both **occupancy and customer ratings** were comparatively lower.

---

## 9. 🌐 Revenue by Booking Platform

Realized revenue by booking platform:

| Booking Platform | Revenue Realized |
| ---------------- | ---------------: |
| Others           |   **72,310,965** |
| MakeYourTrip     |   **34,034,257** |
| Logtrip          |   **18,605,339** |
| Direct Online    |   **17,488,976** |
| Tripster         |   **11,959,078** |
| Journey          |   **10,757,858** |
| Direct Offline   |    **8,986,465** |

### Key Finding

The **Others** booking category generated the highest realized revenue, followed by **MakeYourTrip**.

The analysis also shows that third-party booking platforms contributed substantially to realized revenue compared with the direct offline channel.

---

# 💡 Business Recommendations

Based directly on the observed patterns, the following areas can be considered:

### 📅 Focus on Weekday Demand

Weekend occupancy was much higher than weekday occupancy. AtliQ Hotels could explore weekday-focused offers, corporate packages, or targeted promotions to improve weekday demand.

### 📍 Investigate Bangalore Performance

Bangalore recorded:

* The lowest average occupancy among the four cities
* The lowest average customer rating

This makes Bangalore an important city for further investigation into customer experience, pricing, demand, and hotel-level performance.

### 💰 Evaluate Revenue Alongside Occupancy

Delhi had the highest average occupancy but generated the lowest total city-level realized revenue among the four cities.

This suggests that occupancy alone should not be used to evaluate hotel performance. Revenue per occupied room, room pricing, and property mix should also be considered in future analysis.

### 🌐 Monitor Booking Channel Performance

The analysis shows strong revenue contribution from external booking platforms. AtliQ Hotels can evaluate the profitability and commission costs associated with these channels while continuing to monitor direct booking performance.

---

# 📊 Visualizations

The project uses **Matplotlib** to visually communicate the analysis, including:

* 📊 Booking platform distribution
* 🏨 Number of hotels by city
* 🛏️ Average occupancy by room class
* 📍 Average occupancy by city
* 📅 Weekday vs. weekend occupancy
* 🗓️ June occupancy by city
* 💰 Revenue by city
* 🏨 Revenue by hotel property
* ⭐ Average ratings by city
* 🌐 Revenue by booking platform

These visualizations help convert the numerical analysis into business-focused comparisons.

---

# 🎯 Project Outcome

This project demonstrates an end-to-end **Python-based data analysis workflow**:

**Problem Identification → Data Exploration → Data Cleaning → Data Transformation → Analysis → Visualization → Business Insights**

The analysis highlights differences in **occupancy, revenue, customer ratings, hotel performance, cities, and booking channels**, providing a structured view of AtliQ Hotels' business performance during the analyzed period.
