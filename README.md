# Infographic Dashboard
## Project Description
This project showcases an infographic-style dashboard built in Power BI to provide a comprehensive mid-year performance review of Kraken Koffee’s new Florida sales region. The dashboard integrates analytical storytelling with creative visuals to highlight key performance metrics such as total sales ($698K), transactions (149K), average order value ($4.69), and store-level performance trends across Orlando, Tampa, and Miami.

By blending traditional BI analytics with an infographic layout, this dashboard presents data in a visually engaging and easily digestible format, making insights more accessible to business users and executives.

![image alt](https://github.com/gouravjain77/Infographic_Dashboard/blob/main/full.png?raw=true)

## Key Highlights
- Data Visualization Tool: Power BI

- Design Tool for Layout & Background: Microsoft PowerPoint

- Data Sources: Simulated retail sales data for multiple store locations in Florida

- Core Visuals Used: KPI cards, bar charts, clustered columns, line charts, heatmaps, and custom visuals for infographic storytelling

## Key Insights Displayed:

- Comparative store performance (Orlando vs. Tampa vs. Miami)

- Top-performing products and time-based sales patterns

- Customer behaviour trends and day-wise revenue distribution

- Year-end sales forecasts based on mid-year performance

## Importance of Infographic Dashboards:
Infographic dashboards transform conventional analytical reports into visually immersive data stories. Instead of relying solely on tables and charts, they use design elements, icons, and colour-coded visuals to help viewers grasp key insights at a glance.
This approach enhances executive communication, improves data-driven storytelling, and increases stakeholder engagement by making analytics both informative and aesthetically appealing.

## Design Approach:
The background and thematic layout of this dashboard were created in PowerPoint to establish a branded and visually cohesive structure. The background was then imported into Power BI, where dynamic visuals were overlaid on top to create an interactive infographic experience that combines design flexibility with analytical power.

## Sections Of Dashboard
### Overview
The header section introduces the Kraken Koffee 2023 Half-Time Review Dashboard, summarising the report's purpose: to evaluate mid-year sales performance across the brand’s Florida locations. It presents key metrics, such as total sales, transactions, average order value, and store count, providing viewers with an instant snapshot of business performance.

![image alt](https://github.com/gouravjain77/Infographic_Dashboard/blob/c2284a045cc07d50d38952535fed18a500ab2987/1.png)

### Key Insights
This section highlights major observations and trends, such as which products and store locations are driving revenue growth. It provides quick, actionable insights supported by visuals like bar charts and KPI cards, allowing decision-makers to identify top-performing products and understand regional performance differences.

![image alt](https://github.com/gouravjain77/Infographic_Dashboard/blob/45dbb34ddc67b9a24b8a10a85df00eed870a3b08/2.png)

### Sales Trends
The trend analysis visuals show sales distribution across different months and times of day, helping stakeholders identify peak revenue periods. The combination of bar charts and heat maps allows for a deeper understanding of customer behaviour and store efficiency patterns.

![image alt](https://github.com/gouravjain77/Infographic_Dashboard/blob/d29c5c1c41087d5880c6eea048ceece1aa25eb0d/3.png)

### Forecast
This section projects future sales performance using Power BI’s forecasting capabilities. It enables the business to anticipate year-end results and plan marketing or operational strategies accordingly.

![image alt](https://github.com/gouravjain77/Infographic_Dashboard/blob/d29c5c1c41087d5880c6eea048ceece1aa25eb0d/4.png)

## Measures Created
### Core Measures
- Average Order Size = AVERAGE(Kraken_Koffee_Fact[Total Sales])
- Most Popular Seller = 
CALCULATE(
    MIN(Product_Dim[product_detail]),
    FILTER(Product_Dim,[Product Transactions Ranking]=1)
)
- Product Sales Ranking = 
RANKX(ALLSELECTED(Product_Dim),[Total Sales],,DESC,Dense)
- Product Transactions Ranking = 
RANKX(ALLSELECTED(Product_Dim),[Total Transactions],,DESC,Dense)
- Top Earner = 
CALCULATE(
    MIN(Product_Dim[product_detail]),
    FILTER(Product_Dim,[Product Sales Ranking]=1)
)
- Total Products = COUNT(Product_Dim[product_id])
- Total Sales = 
SUM(Kraken_Koffee_Fact[Total Sales])
- Total Stores = DISTINCTCOUNT(Store_Dim[store_id])
- Total Transactions = COUNT(Kraken_Koffee_Fact[transaction_id])
### Nested Measures
- Total Transactions = COUNT(Kraken_Koffee_Fact[transaction_id])
- Max AOS Marker = 
SWITCH(TRUE(),
    [Average Order Size]=[Max Avg Order Size (Hour)],[Average Order Size],
    BLANK())
- Max Avg Order Size (Hour) = 
MAXX(ALLSELECTED(Kraken_Koffee_Fact[Hour]),[Average Order Size])
- Product Category Rank = CALCULATE(RANKX(ALL('Product_Dim'[product_type]),[Total Sales],,DESC,Dense),ALL(Product_Dim[product_category]))
### Formatting And Text
- Bar Chart Label(Product Category) = 
FORMAT([Total Sales]/1000,"$###,##0K") & " (" & FORMAT([% Of Sales],"###,##0.0%") & ")"
- MAX AOS Marker Label = 
"Max Order Size: " & FORMAT([Max AOS Marker],"$###,##0.00")
- Top 10 Product Type Highlight = 
IF([Product Category Rank] <= 10, "#EFB251", "#00958C")

## Benefits

- Quick Insights: The infographic layout allows stakeholders to grasp key business metrics at a glance without navigating multiple pages.

- Enhanced Storytelling: Combines visuals, narratives, and data in a single view, making performance insights more engaging and easier to communicate.

- Data-Driven Decisions: Provides clear visibility into product performance, store trends, and forecasted outcomes, enabling more strategic planning.

- Interactive Exploration: Users can interact with visuals to drill down into specific stores, time frames, or products for deeper insights.

- Visually Appealing Design: The PowerPoint-designed background adds aesthetic value, improving stakeholder engagement and presentation quality.

## Conclusion
The Kraken Koffee 2023 Half-Time Review Dashboard serves as a perfect example of how data visualisation and design can work together to simplify complex information. By integrating Power BI’s analytical power with infographic-style storytelling, this dashboard not only delivers valuable business insights but also enhances user experience. It stands as a visually compelling and decision-support tool that bridges the gap between data analysis and executive storytelling.
