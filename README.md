# Meta Ads Analysis - Supps&
This project showcases how raw digital advertising data can be transformed into clear, actionable insights using Python, SQL, Power BI. It originated from a client proposal that didn’t move forward, so the concept was developed into a full portfolio demonstration of data-driven marketing intelligence based on a fictive supplement company.

## Project Goal
The customer faced significant challenges, including inefficient budget allocation, limited strategic focus on high-value customers, and difficulty identifying long-term performance trends. These issues were compounded by Meta’s fragmented and unintuitive platform, which forced internal analysts to rely on manual calculations and produce slow, inconsistent reports. This underscored the need for a unified, on-brand BI solution that could serve as a single source of truth.

After asking further clarifying questions to key stakeholders, the following primary research questions were identified that the BI solution should address:

- Q1: Which campaigns, ad sets, or ads generate the highest revenue and profit?
- Q2: Which ads are underperforming relative to spend?
- Q3 How do performance metrics evolve over time (daily, weekly, monthly)?
- Q4: Which countries, age groups, or genders respond best to specific campaigns?
- Q5: What strategies can scale high-performing ads or reallocate budget effectively?

## Solution Overview
The solution aimed to transform Meta’s fragmented analytics into a unified, intelligent BI ecosystem by integrating data feeds through a streamlined ETL process and structuring them into a robust, scalable data model, resulting in a Power BI dashboard—an on-brand, consolidated analytics platform that delivers real-time visibility, intuitive exploration, and a single source of truth, eliminates manual calculations and inconsistent reporting, and provides a solid foundation to address the key questions identified by stakeholders.

## Techstack 
- Chatgpt + Meta Ads Manager (Data Collection)
- SQL (ETL + Exploratory Analysis)
- Python (ETL + AI Report)
- Figma (UI/UX Design)
- PowerBI (Data model + Dashboarding)

## 1. Data Collection
Dummy data was created based on the structure of a Meta Ads Manager export for a fictitious supplement brand. This dataset mirrors the fields, formats, and relationships typically found in a real Meta export, ensuring realistic testing and development conditions. LINK

## 2. Exploratory Analysis
Since the data came from a single source (Meta Ads Manager) and thus is relatively well structured and consistent at its core, the exploratory analysis was fairly straightforward but still essential. Using a set of SQL queries, I assessed the data’s quality, structure, consistency, volume, and distribution. This stage focused on determining whether the data was useful and sufficient to answer the business questions, rather than on generating insights.

### Exploratory Analysis Conclusion
See file for all sql queries and outcomes

The dataset contains 208,512 rows, covering 181 days, 4 campaigns, 12 ad sets, 36 ads, 4 countries, 4 age groups, and 2 genders, with perfectly balanced distribution across dimensions. All key metrics (Impressions, Clicks, Spend, Conversions, Revenue) are complete, and no zero-revenue-with-conversions cases were found. Minor rounding differences were observed in CTR and CPC, so these will be recalculated in the ETL fase.

Based on these findings, the ETL and data model decisions were:

- Created a star schema, separating dimensions (Campaign, Ad_Set, Ad, Date, Country, Age_Group, Gender) from the fact table.

- Fact table stores numeric metrics at the fine-grained level.

- This design ensures efficient queries and smooth reporting, especially given the large, categorical-heavy dataset.


## 3. Extract, Transform, Load (ETL)

### Extraction & Initial Loading

Imported CSV data into a Pandas DataFrame and connected to a SQLite database.

Dataset contains 208,512 rows, balanced across campaigns, ad sets, ads, countries, age groups, and genders, with no missing key metrics.

Replaced any existing table in SQLite to avoid duplicates and ensure a clean starting point.

### Transformation

- Converted date and categorical columns to proper types.

- Calculated additional metrics for reporting:

1. Profit = Revenue − Spend

2. Conversion Rate = Conversions ÷ Clicks

3. ROAS = Revenue ÷ Spend
   
5. ROI = (Revenue − Spend) ÷ Spend

6. Extracted time features (Year, Month, Week, Day of Week) from the Date column.

### Modeling & Loading

Created a star schema:

- Dimension tables: Date, Campaign, Ad Set, Ad, Country, Age Group, Gender

- Fact table: contains numeric metrics and foreign keys to all dimensions

- Joined dimensions with the fact table at the fine-grained level (Date × Campaign × Ad_Set × Ad × Country × Age_Group × Gender).

- Exported all tables as CSVs for ETL pipeline use and dashboard ingestion.

This design ensures efficient querying and smooth reporting for a large, categorical-heavy dataset.

## 4. Dashboard Design 
### Page Architecture & Key Visuals

The dashboard follows a "Macro to Micro" logic, transitioning from high-level health to tactical details.

- Overview: Provides a high-level view of key profitability metrics and campaign-level performance. Designed for stakeholders who need quick, actionable insights to support decision-making without added complexity or the need for direct interaction with the dashboard.
  
- Costs & ROI: Provides insights into funnel performance and individual ad performance, and how they relate to each other. Allows users to further dissect results using campaign and month filters. Designed for users who want to analyze ad performance in more depth.

- Segmentation: Designed for users who want to go a step further by dissecting ad performance at a demographic level, allowing for better adjustment of ad targeting.

- Trends: Designed for users who want to dive further into performance by analyzing results across time horizons. Enables better timing decisions, momentum and duration analysis, and seasonality insights for ads.

### Design System: UX & Aesthetics

The design philosophy is built on clarity, brand alignment, and reduced cognitive load.

- Strategic Palette: I used a Sage Green and Neutral palette to reflect the "Supps&" brand identity. This "natural" aesthetic makes high-density data feel less overwhelming and more approachable.

- Modular Layout: Each visual is housed in a rounded "Card" with ample whitespace. This creates a clear hierarchy, allowing the user to process one insight at a time without "data fatigue."

- Intuitive Navigation: A consistent Sidebar and Filter placement (top-right) ensures a seamless user experience. Once the user learns Page 1, they can navigate the entire suite instinctively.

- KPI Prioritization: I used High-Contrast Typography for core metrics. The most critical numbers (Profit, ROAS) are the largest elements on the screen, ensuring "glanceability."

![Dashboard Overview](Dashboard%20Pictures/Dashboard%20Overview%201.png)
![Dashboard Costs & ROI](Dashboard%20Pictures/Dashboard%20Costs%20%26%20ROI%202.png)
![Dashboard Segmentation](Dashboard%20Pictures/Dashboard%20Segmentation%203.png)
![Dashboard Trends](Dashboard%20Pictures/Dashboard%20Trends%204.png)

## Conclusions 
The dashboard and ETL process provide a stable foundation for Supps& to engage in data-driven decision-making and offer stakeholders a clear, user-friendly way to interact with their data. At the start of the project, several key research questions were identified that were frequently raised and for which the dashboard needed to serve as a single source of truth. Below are the insights related to these questions:

### Overall Performance (Q1 & Q2)

Across Q1 and Q2, Supps & Ads demonstrates stable and sustained profitability. The ad budget is distributed relatively evenly across campaigns, indicating a diversified investment approach. However, when evaluating performance outcomes, results are clearly skewed in favor of the re-push campaigns. This confirms that the current strategy is working as intended.

Awareness-focused campaigns play a supporting role within the broader system by introducing and warming up new audiences. Re-push campaigns then retarget these users and successfully guide them toward a purchase decision. As such, lower ROAS on awareness campaigns should not be viewed as an issue when performance is assessed holistically rather than at the individual campaign level.

At the individual ad and asset level, performance is generally stable. A small number of ads and ad sets stand out as underperformers and should be reviewed more critically to determine whether optimization or replacement is needed.

The sales funnel itself is performing at a very high level. With a 6.61% click-through rate and a 5.28% conversion rate, performance significantly exceeds 2025 industry benchmarks for the health and wellness sector. This indicates that the ad creatives are highly engaging and that traffic is being directed to a landing page that converts with top-tier efficiency. Overall, the data reflects a well-structured funnel that effectively moves users from awareness to purchase.

### Overall Performance (Q3 & Q4)

The Netherlands is the primary profit-driving market for Supps&, followed by Germany and Belgium at roughly half that level, with Denmark contributing approximately half of those results. ROAS is consistent across markets, with higher profit in the Netherlands driven by greater conversion volume rather than efficiency differences.

Performance is evenly split between male and female audiences in both ROAS and customer volume. Results across age groups are similarly consistent, with the 25–34 segment performing slightly better, though differences remain marginal. Over time, ad performance has been relatively stable; however, a gradual increase in cost per acquisition and a slight decline in ROAS are visible. Spend and profit closely track each other, indicating that overall ad effectiveness remains consistent. Notably, January shows an anomaly in CTR and profit, suggesting increased audience receptiveness, potentially driven by New Year resolution behavior.

### Strategy Takeaways (Q5)

From these analyses, four main strategic takeaways and follow-up actions were identified:

#### 1. Scale Re-push Campaigns While Protecting Efficiency
Re-push campaigns are the primary profit drivers and validate the current funnel strategy. The most immediate upside lies in systematically increasing spend on these campaigns while closely monitoring marginal ROAS. Testing controlled budget increases and managing creative fatigue will help unlock additional profit without oversaturation or audience cannibalization.

#### 2. Counter Rising CPA Through Creative and Funnel Optimization

The gradual increase in CPA and slight decline in ROAS signal early efficiency pressure. Priority should be placed on refreshing high-performing creatives and testing new angles to sustain CTR, alongside targeted landing page and funnel optimizations to preserve conversion rates as media costs rise.

#### 3. Exploit Seasonal Momentum Identified in January

The January spike in CTR and profit presents a clear opportunity. Further research into messaging, offers, and creative themes used during this period can inform seasonally adjusted campaigns. Testing “resolution-driven” positioning outside January may help replicate this performance uplift throughout the year.

#### 4. Drive Volume Growth in Secondary Markets

With ROAS consistent across markets, higher profitability is driven by conversion volume rather than efficiency differences. Increasing spend and improving localization in Germany and Belgium represents a scalable growth opportunity, allowing Supps& to diversify revenue while maintaining current performance levels.


- Remy Dinh - Last Edit 22-12-2025.
- For more information, contact me on [LinkedIn](https://www.linkedin.com/in/remydinh23/)



