# 📊 CRM Sales Opportunities Analysis Power BI Dashboard

## Project Overview
This project involves the end-to-end development of a Business Intelligence dashboard to analyze a global CRM Sales Opportunities dataset. The goal was to transform raw data into actionable insights, enabling stakeholders to track key performance indicators (KPIs), monitor sales trends, identify top-performing products and accounts, and analyze the sales pipeline health.

Key questions addressed by this dashboard:
1.  What is the total Revenue and Total Pipeline value?
2.  Are we seeing growth or decline in sales? (Quarter-over-Quarter analysis)
3.  Which products have the highest win rates?
4.  How concentrated is our revenue among top clients?
5.  What is the average sales cycle duration?
6.  How many deals are currently in each stage of the pipeline?

---

## 🛠️ Technologies Used
*   Power BI Desktop: Data transformation, DAX modeling, and visualization.
*   Power Query (M): Data cleaning and ETL (Extract, Transform, Load) processes.
*   DAX: Calculated measures and columns for advanced analytics.
*   GitHub: Version control and project documentation.

---

## 📂 Project Files & Links (Original Dataset)
*((https://github.com/Joseph-Chibueze-Portfolio/crm-sales-opportunities-analysis/blob/main/accounts.csv)*
*(https://github.com/Joseph-Chibueze-Portfolio/crm-sales-opportunities-analysis/blob/main/products.csv))*
*(https://github.com/Joseph-Chibueze-Portfolio/crm-sales-opportunities-analysis/blob/main/sales_pipeline.csv)*
*(https://github.com/Joseph-Chibueze-Portfolio/crm-sales-opportunities-analysis/blob/main/sales_teams.csv)*

*   🖼️ Dashboard Screenshot: [View Dashboard Image] [https://github.com/Joseph-Chibueze-Portfolio/crm-sales-opportunities-analysis/blob/main/CRM%20SALES%20OPPORTUNITIES%20DASHBOARD.png]
*   📋 Power BI Report File (.pbix): [Download PBIX File] [https://github.com/Joseph-Chibueze-Portfolio/crm-sales-opportunities-analysis/blob/main/CRM%20SALES%20OPPORTUNITIES.pbix]

---

## ⚙️ Data Preparation & Transformation (ETL)
Before visualization, the raw data from four disparate tables required significant cleaning and shaping in Power Query to enable accurate analysis.

### 1. Data Cleaning Highlights
*   ACCOUNTS Table: Replaced null values in the **Subsidiary of** column with 'Parent' for clarity. Applied proper casing (Capitalize Each Word), trim, and clean to all text columns.
PRODUCT Table:e:** Performed standard cleaning operations: removing duplicates, trimming whitespace, and cleaning data types.
SALES PIPELINE Table (Fact Table):):** This was the most critical cleaning step. Deals marked as **deal_stage** = "Engaging" had blank **close_date** and **close_value**. To ensure accurate reporting, these blanks were replaced with "Prospect". This prevents unclosed opportunities from skewing "Closed Won" revenue totals or Win Rate caSALES TEAMS Table:S TEAMS Table:** Promoted the first row to headers to establish correcsales_agent(**sales_agent**, **manager**, **regional_office**).

### 2. Data Modeling (Star Schema)
AStar Schemaa robust **Star Schema** data model was built. This is the foundation of the entire report, ensuring accurate filtering andFact Table:ce.

Sales Pipeline* The **Sales Pipeline** table sits at the center, containing the transactional sales data (measures like close_value, pipeline_value, dates, and IDs).
* Accountsn Producthe **Accounts**, **Product**, and **Sales Teams** tables were connected as dimensioRelationships:ct table.
*   **Relationships:** One-to-Many (1:*) relationships were established based on common keys (e.g., linking Accounts[Account] to Sales Pipeline[account]).

### 3. Date Table Creation
To enable complex Time Intelligence functions (QoQ growth, YTD totals), a dedicated Date Table was created using DAX because the existing data ranges (1979-2017) were inDAX Formula:en tables.

*   **DAX Formula:** 
   
    DateTable = CALENDAR(DATE(1979, 1, 1), DATE(2017, 12, 31))
    
*   Columns were added for YeMonther, and Month.
*   The **Month** cMonth Numberured to sort by **Month Number** to ensure chronological (not alphabetical) sorting on charts.
*   An active relatDateTable[Date]shed between **DateTable[Date]** and **Sales Pipeline[close_date]**.

---

## 🧮 Key DAX Measures & Calculations

Below are the core DAX measures developed to power the analytics and KPIs.
