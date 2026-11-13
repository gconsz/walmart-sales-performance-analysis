# Walmart Store Sales & Operational Performance Analysis

**SQL | Google BigQuery | Tableau | Data Analytics**

## Project Overview

This project analyzes historical weekly sales data from 45 Walmart stores to evaluate sales performance, identify seasonal trends, compare holiday and non-holiday demand, and measure differences in store-level sales variability.

I used Google BigQuery and SQL to validate, clean, transform, and analyze the dataset. I then developed a Tableau dashboard with five analytical visualizations and three key performance indicators (KPIs).

The goal was to translate historical retail sales data into actionable insights that could support inventory planning, workforce scheduling, and operational decision-making.

**Analysis period:** February 5, 2010 – October 26, 2012

**Dataset:** 6,435 store-week records, covering 45 stores and 143 weeks

**Dataset source:** [Walmart Dataset — Kaggle](https://www.kaggle.com/datasets/yasserh/walmart-dataset)

*This is an independent educational project using a community-published historical dataset, not an official Walmart business analysis.*

---

## Business Objective

**Main Business Question:**

How can Walmart use historical sales data to identify store performance trends, seasonal demand patterns, and opportunities to improve operational planning?

Five questions guided the analysis:

1. Which stores generated the highest cumulative sales?
2. How did total weekly sales change over time?
3. Were average sales higher during holiday weeks?
4. Which months showed the strongest seasonal sales performance?
5. Which stores experienced the greatest and least sales variability?

---

## Tools and Technologies

| Tool | Application |
|---|---|
| Google BigQuery | Data storage, validation, transformation, and analysis |
| SQL | Data cleaning, aggregation, business questions, and KPI calculations |
| Tableau | Interactive sales performance dashboard |
| GitHub | Project documentation, SQL scripts, and supporting files |

**SQL techniques:** `COUNT`, `COUNTIF`, `GROUP BY`, `SUM`, `AVG`, `STDDEV_SAMP`, `SAFE_DIVIDE`, `SAFE_CAST`, conditional logic, Common Table Expressions, date functions, and analytical views.

---

## Dataset Description

The original dataset contains eight columns:

| Column | Description |
|---|---|
| Store | Store identification number |
| Date | Weekly reporting date |
| Weekly_Sales | Weekly store sales |
| Holiday_Flag | Whether the week is classified as a holiday week |
| Temperature | Regional temperature |
| Fuel_Price | Regional fuel price |
| CPI | Consumer Price Index |
| Unemployment | Regional unemployment rate |

Each record represents one store's sales for a particular reporting week.

The primary focus was sales performance. Economic and environmental variables were retained but were not included in the five core business analyses.

---

## Data Cleaning and Preparation

The original dataset was imported into Google BigQuery as `walmart_raw`.

The cleaning process included:

1. **Missing-value checks:** No NULL values were identified in the original eight columns.
2. **Duplicate detection:** No duplicate combinations of Store and Date were found.
3. **Numerical validation:** Checked for invalid or unusual numerical values, including negative sales and invalid economic measures. No invalid values requiring removal were identified.
4. **Date standardization:** Converted reporting dates into a consistent date format.
5. **Holiday flag standardization:** Standardized holiday indicators for categorical comparisons.
6. **Field standardization:** Renamed fields to consistent, descriptive names.
7. **Date feature creation:** Created `sales_year`, `sales_month`, and `month_start` to support time-based analysis.

A cleaned analytical view named `walmart_clean` was created in BigQuery, preserving the original source records.

The transformed dataset was used for SQL analysis and Tableau visualization.

**Data quality outcome:** The final analytical dataset retained 6,435 records, 45 stores, and 143 weekly reporting dates.

---

## Key Performance Indicators

The following KPIs were calculated from the cleaned dataset.

| KPI | Result |
|---|---:|
| Total Sales | $6,737,218,987.11 |
| Average Weekly Sales per Store | $1,046,964.88 |
| Total Stores | 45 |
| Total Reporting Weeks | 143 |
| Total Store-Week Records | 6,435 |
| Average Combined Weekly Sales | $47,113,419.49 |

The total sales figures reconcile across the weekly, monthly, and holiday SQL analysis outputs.

---

## Business Question 1 — Store Performance

**Which Walmart stores generated the highest total sales between February 2010 and October 2012?**

### SQL Analysis

Store sales were aggregated using `SUM(weekly_sales)` and `AVG(weekly_sales)`, grouped by store identifier, and ranked by cumulative sales.

### Results

| Rank | Store | Total Sales | Avg. Weekly Sales |
|---|---|---:|---:|
| 1 | 20 | $301.40M | $2.11M |
| 2 | 4 | $299.54M | $2.09M |
| 3 | 14 | $289.00M | $2.02M |
| 4 | 13 | $286.52M | $2.00M |
| 5 | 2 | $275.38M | $1.93M |

All five stores reported data for 143 weeks.

### Key Findings

- **Store 20 generated the highest cumulative sales:** $301,397,792.46.
- Store 4 ranked second, with $299,543,953.38.
- Store 14 ranked third, with $288,999,911.34.
- The ten highest-selling stores accounted for approximately **39.05% of the dataset's total sales**.

### Business Insight

Store 20 was the highest-performing location by cumulative sales during the observation period. Stores 4 and 14 followed closely, indicating substantial sales volumes across multiple locations.

Because the leading stores all reported the same number of weeks, their cumulative sales are directly comparable within this dataset.

### Business Recommendation

Walmart could examine demand patterns at high-volume stores to improve inventory allocation and workforce scheduling.

Further investigation into store size, geographic location, customer characteristics, and operational practices would help explain why certain stores generated higher sales.

---

## Business Question 2 — Weekly Sales Trends

**How did Walmart's total weekly sales change over time, and which weeks experienced the highest and lowest sales?**

### SQL Analysis

Weekly sales were aggregated across the 45 stores using `SUM(weekly_sales)` and grouped by reporting date.

### Results

| Metric | Week Date | Total Sales |
|---|---|---:|
| Highest weekly sales | December 24, 2010 | $80,931,415.60 |
| Second-highest weekly sales | December 23, 2011 | $76,998,241.31 |
| Lowest weekly sales | January 28, 2011 | $39,599,852.99 |
| Second-lowest weekly sales | January 27, 2012 | $39,834,974.67 |

**Average combined weekly sales:** $47,113,419.49.

All 45 stores reported sales for every week included in the analysis.

### Key Findings

- The highest sales week occurred on **December 24, 2010**, generating approximately $80.93 million.
- A similar peak occurred on December 23, 2011, generating approximately $77.00 million.
- The two lowest weeks occurred in late January of 2011 and 2012.
- These results reveal pronounced late-year increases followed by lower sales in January.

### Business Insight

The recurring increases in November and December suggest that sales demand follows seasonal patterns.

The substantial decline after the late-December peaks indicates that operational demand may change significantly between the holiday shopping season and the beginning of the following year.

These observations describe seasonal patterns, not their confirmed causes.

### Business Recommendation

Walmart could use historical weekly demand to adjust seasonal inventory levels, staffing schedules, and distribution planning.

Sales forecasts should account for recurring late-year peaks and subsequent declines to reduce the risk of inventory shortages or excess stock.

---

## Business Question 3 — Holiday Sales Performance

**Do Walmart stores generate higher average weekly sales during holiday weeks compared with non-holiday weeks?**

### SQL Analysis

The cleaned holiday indicator was used to divide store-week records into holiday and non-holiday categories.

Average weekly store sales were calculated using `AVG(weekly_sales)`.

### Results

| Metric | Holiday | Non-Holiday |
|---|---:|---:|
| Store-Week Records | 450 | 5,985 |
| Average Weekly Store Sales | $1,122,887.89 | $1,041,256.38 |
| Total Sales | $505.30M | $6.23B |

### Key Findings

Holiday-week average sales exceeded non-holiday averages by **$81,631.51 per store-week**.

This represents an approximately **7.84% higher average weekly sales value** during holiday weeks.

There were 10 holiday reporting weeks and 133 non-holiday reporting weeks in the dataset.

### Business Insight

Holiday-designated weeks were associated with stronger average store sales.

Although non-holiday weeks generated greater cumulative sales because they represented far more reporting periods, the average store-week comparison provides a more meaningful measure of relative performance.

The difference is observational and does not prove that holiday designation directly caused higher sales.

### Business Recommendation

Retail operations teams could consider historical holiday-week demand when planning inventory availability, staffing requirements, and replenishment schedules.

More detailed analysis by store and individual holiday would help determine whether the overall pattern is consistent across locations.

---

## Business Question 4 — Monthly Sales Seasonality

**Which months experienced the highest average weekly sales, and were there recurring seasonal patterns across 2010, 2011, and 2012?**

### SQL Analysis

Weekly records were grouped by year and month, calculating cumulative monthly sales and average sales per store-week.

Average sales were used to account for differences in the number of reporting weeks per month.

### Results

| Month | Avg. Sales per Store-Week | Total Monthly Sales |
|---|---:|---:|
| December 2010 | $1,283,380.15 | $288.76M |
| December 2011 | $1,280,347.12 | $288.08M |
| November 2011 | $1,167,568.64 | $210.16M |
| November 2010 | $1,126,963.17 | $202.85M |

For comparison:

| Month | Avg. Sales per Store-Week |
|---|---:|
| January 2011 | $909,466.48 |
| January 2012 | $938,302.62 |

### Key Findings

- **December 2010 had the highest monthly average store-week sales:** approximately $1.283 million.
- December 2011 followed closely at approximately $1.280 million.
- November also showed elevated averages in both 2010 and 2011.
- January had substantially lower average sales in both 2011 and 2012.

### Business Insight

The monthly results support the seasonal pattern observed in the weekly sales analysis.

Higher average sales in November and December, followed by lower values in January, suggest recurring differences in demand throughout the retail calendar.

The dataset does not include January 2010 or November–December 2012, limiting comparisons across complete calendar years.

### Business Recommendation

Walmart could develop monthly seasonal planning benchmarks to anticipate inventory and staffing needs.

Operations teams could compare store-specific demand patterns against these broader monthly averages to identify locations requiring additional seasonal resources.

---

## Business Question 5 — Store Sales Variability

**Which Walmart stores experienced the greatest fluctuations in weekly sales, and which maintained the most consistent sales performance?**

### SQL Analysis

Sales variability was measured using the coefficient of variation (CV).

**CV (%) = Standard Deviation of Weekly Sales ÷ Average Weekly Sales × 100**

This measure allows comparisons across stores with different average sales volumes.

### Highest Sales Variability

| Store | Coefficient of Variation |
|---|---:|
| 35 | 22.97% |
| 7 | 19.73% |
| 15 | 19.34% |
| 29 | 18.37% |
| 23 | 17.97% |

### Lowest Sales Variability

| Store | Coefficient of Variation |
|---|---:|
| 37 | 4.21% |
| 30 | 5.20% |
| 43 | 6.41% |

### Key Findings

- **Store 35 experienced the highest relative sales variability**, with a coefficient of variation of 22.97%.
- Stores 7 and 15 followed at 19.73% and 19.34%, respectively.
- Store 37 had the lowest coefficient of variation at 4.21%, indicating the most consistent weekly sales relative to its average.
- Store 30 was the second-most consistent, at 5.20%.

### Business Insight

The variability analysis reveals meaningful differences in sales stability across locations.

Stores with higher coefficients of variation experienced larger relative fluctuations, while stores with lower values maintained more consistent weekly performance.

Variability alone does not indicate poor operational performance. It may reflect seasonal demand, market characteristics, or store-specific conditions.

### Business Recommendation

Walmart could prioritize more detailed demand forecasting and flexible replenishment strategies for stores with greater sales fluctuations.

Stores exhibiting consistent demand may be better suited to stable inventory and staffing schedules, subject to additional operational analysis.

---

## Tableau Sales Performance Dashboard

A Tableau dashboard was developed to communicate findings through interactive visualizations.

### Dashboard Components

**KPI Cards**
- Total Sales
- Average Weekly Sales per Store
- Total Stores

**Visualizations**
1. Top 10 Walmart Stores by Total Sales
2. Walmart Weekly Sales Trend
3. Holiday vs. Non-Holiday Average Weekly Sales
4. Walmart Monthly Sales Seasonality Heatmap
5. Walmart Store Sales Variability

### Dashboard Design

The dashboard uses a consistent blue color scheme, contrasting categorical colors, readable sales labels, and a sequential heatmap palette.

Currency values are abbreviated where appropriate, and sales variability is displayed as percentages.

**Dashboard screenshot:** Add the uploaded dashboard image to the `images/` folder and embed it here.

**Interactive Tableau Dashboard:** Add Tableau Public URL here after publication.

---

## Summary of Key Findings

| Analysis | Result |
|---|---|
| Total Sales | $6.74 billion |
| Highest-Selling Store | Store 20 — $301.40 million |
| Highest Sales Week | December 24, 2010 — $80.93 million |
| Lowest Sales Week | January 28, 2011 — $39.60 million |
| Holiday Sales Difference | +7.84% average per store-week |
| Strongest Month | December 2010 — $1.283 million average per store-week |
| Most Variable Store | Store 35 — 22.97% CV |
| Most Consistent Store | Store 37 — 4.21% CV |

## Overall Business Recommendations

The analysis identified differences in store performance, recurring seasonal demand patterns, higher average sales during holiday-designated weeks, and varying levels of store-level sales stability.

Based on these findings, retail operations teams could:

1. **Improve seasonal inventory forecasting** by incorporating recurring late-year sales patterns.
2. **Adjust staffing and replenishment planning** around periods of increased demand.
3. **Examine high-volume stores** to better understand their operational requirements and performance drivers.
4. **Develop store-specific forecasting approaches** for locations with greater sales variability.
5. **Monitor sales performance through dashboards** that support regular operational reviews.

These are proposed operational applications, not measured results of implemented changes.

---

## Project Limitations

- The data is historical, covering February 2010 through October 2012.
- The public dataset has not been independently authenticated as official Walmart financial reporting.
- The first and final calendar years are incomplete.
- Store-level geographic and operational information is limited.
- Holiday and seasonal sales differences represent associations rather than causal effects.
- The economic indicators included in the dataset were not examined through multivariate or causal modeling.
- No operational interventions were implemented or evaluated.

These limitations should be considered before applying the findings to real-world decisions.

---

## Future Improvements

Potential extensions include:

- Examining relationships between sales and fuel prices, CPI, unemployment, and temperature
- Developing store-specific weekly sales forecasts
- Investigating individual holiday periods
- Comparing high-performing and high-variability stores in greater detail
- Building automated sales reporting workflows

---

## Repository Contents

- `sql/` — BigQuery cleaning and business analysis queries
- `images/` — SQL result screenshots and dashboard images
- `tableau/` — Tableau dashboard resources
- `business_questions.md` — Business questions and supporting analysis, if included in the repository
- `README.md` — Project methodology, findings, and recommendations

### Project Links

**GitHub Repository:** [Walmart Sales Performance Analysis](https://github.com/gconsz/walmart-sales-performance-analysis)

**Dataset Source:** [Kaggle Walmart Dataset](https://www.kaggle.com/datasets/yasserh/walmart-dataset)

**Interactive Dashboard:** Add Tableau Public link after publication.

---

## Skills Demonstrated

**Data Cleaning:** Missing-value checks, duplicate detection, data validation, date conversion, and transformations.

**SQL Analysis:** Aggregation, conditional logic, date functions, standard deviation, coefficient of variation, and business question development.

**Data Visualization:** Tableau dashboard development, KPI reporting, bar charts, time-series analysis, and heatmaps.

**Business Analytics:** Sales performance evaluation, seasonal analysis, store comparisons, operational recommendations, and communication of findings.

---

## Author

**GitHub:** [gconsz](https://github.com/gconsz)

**Portfolio:** [Extern Portfolio](https://extern.com/portfolios/graeme-cyrell)

**Project:** Walmart Store Sales & Operational Performance Analysis
