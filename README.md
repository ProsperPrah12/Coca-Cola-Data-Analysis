# Coca-Cola-Data-Analysis
This project analyzes Coca-Cola sales data using cleaned data, SQL for advanced statistical analysis, and Tableau for visualization. It explores sales trends, promotion impact, customer segmentation, and forecasting, turning raw data into actionable insights for business decisions.

### Project Overview

- This project delivers an advanced analysis of Coca-Cola sales data using SQL and Tableau. Since the dataset is already cleaned, the focus is on leveraging SQL for statistical analysis to uncover    sales patterns, seasonal trends, and product performance across regions. Tableau is then used to create interactive dashboards that visualize key insights, highlight correlations, and forecast      future demand. The objective is to transform structured sales data into actionable business intelligence that supports decisions in marketing, pricing, and inventory optimization.

### Data Source 

- The dataset used in this project is a cleaned Coca-Cola sales dataset provided in CSV format. It contains detailed records of sales transactions, including product names, quantities, sales          amounts, shipment details, salespeople, and regional information.

### Tools Used

1. Microsoft Excel – for preliminary data inspection and validation. [Download Here](https://config.office.com/deploymentsettings)
2. SQL – for advanced querying, aggregation, and statistical analysis. [Download Here](https://learn.microsoft.com/en-us/ssms/)
3. Tableau – for creating interactive dashboards and visualizations to communicate insights. [Download Here](https://www.tableau.com/community/public)

### Exploratory Data Analysis (EDA)

- Analyzed sales distribution across countries and product categories.
- Identified top-5 performing Beverage Brand and states by total sales.
- Examined seasonal trends to detect peak demand months.
- Compared brand-level contributions to overall revenue.
- Reviewed outliers and fluctuations for potential business insights.

### Data Analysis

- Analyzed sales distribution across countries and product categories.
  ```sql
    SELECT 
    [State],
    [Beverage Brand] AS ProductCategory,
    SUM(TRY_CAST(REPLACE(REPLACE([Price per Unit], '$',''), ',', '') AS DECIMAL(18,2))) AS Total_Sales,
    SUM(TRY_CAST(REPLACE([Units Sold], ',', '') AS INT)) AS Total_Units

    FROM [dbo].[CocaCola]
    
    WHERE ISNUMERIC(REPLACE([Units Sold], ',', '')) = 1
    GROUP BY [State], [Beverage Brand]
    ORDER BY [State], Total_Sales DESC;
  ```
- Identified top-5 performing Beverage Brand and states by total sales.
  ```sql
    SELECT TOP 5
    [State], [Beverage Brand],
    SUM(TRY_CAST(REPLACE(REPLACE([Units Sold], '$',''), ',', '') AS DECIMAL(18,2))) AS Total_Sales
    FROM [dbo].[CocaCola]
    GROUP BY [Beverage Brand],[State]
    ORDER BY Total_Sales DESC;
  ```
- Examined seasonal trends to detect peak demand months.
  ```sql
    SELECT 
    DATENAME(MONTH, [Date]) AS Month,
    SUM(TRY_CAST(REPLACE(REPLACE([Units Sold], '$',''), ',', '') AS DECIMAL(18,2))) AS Total_Sales
    FROM [dbo].[CocaCola]
        
    WHERE TRY_CAST([Date] AS DATE) IS NOT NULL
    GROUP BY DATENAME(MONTH, [Date]), MONTH([Date])
    ORDER BY MONTH([Date]) ASC;
  ```
- Compared brand-level contributions to overall revenue.
  ```sql
    SELECT 
    [Beverage Brand],
    SUM(TRY_CAST(REPLACE(REPLACE([Units Sold], '$',''), ',', '') AS DECIMAL(18,2))) AS Total_Sales,
    AVG(TRY_CAST(REPLACE(REPLACE([Units Sold], '$',''), ',', '') AS DECIMAL(18,2))) AS Avg_Sales
    FROM [dbo].[CocaCola]
    GROUP BY [Beverage Brand]
    ORDER BY Total_Sales DESC;
  ```
