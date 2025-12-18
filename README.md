# Meta Ads Analysis - Supps&
This project showcases how raw digital advertising data can be transformed into clear, actionable insights using Python, SQL, Power BI. It originated from a client proposal that didn’t move forward, so the concept was developed into a full portfolio demonstration of data-driven marketing intelligence based on a fictive supplement company.

## Project Goal
The customer faced significant challenges, including inefficient budget allocation, limited strategic focus on high-value customers, and difficulty identifying long-term performance trends. These issues were compounded by Meta’s fragmented and unintuitive platform, which forced internal analysts to rely on manual calculations and produce slow, inconsistent reports. This underscored the need for a unified, on-brand BI solution that could serve as a single source of truth.

After asking further clarifying questions to key stakeholders, the following primary research questions were identified that the BI solution should address:

- Which campaigns, ad sets, or ads generate the highest revenue and profit?
- Which ads are underperforming relative to spend?
- How do performance metrics evolve over time (daily, weekly, monthly)?
- Which countries, age groups, or genders respond best to specific campaigns?
- hat strategies can scale high-performing ads or reallocate budget effectively?

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
See file for the sql queries

The dataset contains 208,512 rows, covering 181 days, 4 campaigns, 12 ad sets, 36 ads, 4 countries, 4 age groups, and 2 genders, with perfectly balanced distribution across dimensions. All key metrics (Impressions, Clicks, Spend, Conversions, Revenue) are complete, and no zero-revenue-with-conversions cases were found. Minor rounding differences were observed in CTR and CPC, so these will be recalculated in dashboards.

Based on these findings, the ETL and data model decisions were:

- Created a star schema, separating dimensions (Campaign, Ad_Set, Ad, Date, Country, Age_Group, Gender) from the fact table.

- Fact table stores numeric metrics at the fine-grained level.

- This design ensures efficient queries and smooth reporting, especially given the large, categorical-heavy dataset.


## 3. Extract, Transform, Load (ETL)

## 4. Dashboard Design 
![Overview](/Pictures/1.%20Overview%20Page.png)
![Costs & ROI](/Pictures/2.%20Costs%20&%20ROI%20Page.png)
![Segmentation](/Pictures/3.%20Segmentation%20Page.png)
![Trends](/Pictures/4.%20Trends%20Page.png)


## Conclusions 

