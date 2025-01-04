# Virgin Megastore – Financial Analysis Report

### Dashboard Link 
https://app.powerbi.com/groups/me/reports/dec7ca5d-e86f-40c4-9aea-5a5165f5e345/9c96d7158d96bc706011?experience=power-bi

## Problem Statement

This dashboard helps the finance and strategy teams at Virgin Megastore gain insights into the overall financial performance of the business. It highlights the key performance indicators (KPIs)—such as Sales, Orders, Profit, Profit Margin, and Discount—across various segments (e.g., Channel Partners, Enterprise, Government), products, and geographies (countries). By identifying areas where profit margins are lower or discounts are higher, decision-makers can focus on optimizing pricing, promotions, and operational efficiencies to drive profitability.

From the data, we can see that despite a significant improvement in orders and revenue compared to the previous year, there is a slight dip in overall profit margin. Additionally, certain segments (like Enterprise) may need extra attention to improve margin, while others (like Channel Partners) are performing exceedingly well.  

---

## Steps Followed

1. Step 1: Data Loading  
   - Load data into Power BI Desktop, dataset is a csv file. 

2. Step 2: Data Cleaning & Profiling 
   - Opened Power Query Editor.  
   - Under the "View tab", used Column distribution, Column quality, and Column profile to identify any nulls, errors, or outliers.  
   - Confirmed that key columns such as Sales Amount, Orders, and Discount had valid values and minimal errors.  

3. Step 3: Data Transformation  
   - Performed necessary transformations such as removing unnecessary columns, renaming fields for clarity, and merging or appending queries if required.  
   - Ensured consistent data types (e.g., numeric for sales, dates for time-series, text for categories).  

4. Step 4: Calculated Columns & Measures  
   - Calculated Columns: Created new columns to categorize or group data (e.g., Segment, Country groups, etc.) if not already in the data.  
   - Measures:  
     - "Total Sales" = SUM([Sales])  
     - "Total Orders" = COUNT([Order ID]) or SUM([Orders]) (depending on the data)  
     - "Profit Margin" = DIVIDE([Profit], [Sales])  
     - "Discount Amount" = SUM([Discount])  
     - Additional DAX measures for YoY change, percentage differences, etc.

5. Step 5: Report Design & Visuals  
   - Applied a "theme" under the "View" tab in Power BI to maintain consistent branding (Virgin Megastore colors: navy blue, orange, etc.).  
   - "Card Visuals" for displaying overall KPIs (Sales, Orders, Profit, Profit Margin, Discount) and their YoY changes.  
   - "Bar Charts" and "Column Charts" to show:  
     - 'Orders by Country' 
     - 'Profit Margin by Country'  
     - 'Profit Margin by Segment'  
     - 'Sales Amount by Year and Month'  
   - 'Doughnut/Pie Chart' to show discount distribution across Low, Medium, and High discount bands.  
   - 'Stacked Bar/Column Chart' for analyzing product-level performance (e.g., Top 3 products by Sales).  

6. Step 6: Filtering & Slicers  
   - Added slicers for filters such as 'Product Category', 'Country', 'Segment, and 'Time Period (Year/Month)'.  
   - This allows interactive exploration, so users can drill down into specific segments or products and see the associated KPIs.  

7. Step 7: Publishing the Report  
   - Published the report to Power BI Service using the 'Publish' button in Power BI Desktop.  
   - Created a 'Dashboard' in Power BI Service with pinned visuals to give a high-level overview.  
   - Shared the dashboard with stakeholders and assigned appropriate access levels.

---
## Measures
-Calculates the total amount of discounts offered
Discount offered = SUM(financials[Discounts]) 

-Calculates the total amount of discounts offered during the same period last year (LY).
Discount Offered LY = CALCULATE([Discount offered],DATEADD('Date Table'[Date],-1,YEAR))

-Counts the total number of units sold.
Orders = SUM(financials[Units Sold])

-Counts the total units sold during the same period last year.
Orders LY = CALCULATE([Orders],DATEADD('Date Table'[Date],-1,YEAR))

-Aggregates total profit from all transactions.
Profit = SUM(financials[Profit])

-Calculates total profit for the same period last year
Profit LY = CALCULATE([Profit],DATEADD('Date Table'[Date],-1,YEAR))

-Determines the ratio of profit to total sales amount.
Profit margin = DIVIDE([Profit],[Sales Amount]) 

-Determines last year’s profit margin for the same time period.
Profit Margin LY = CALCULATE([Profit margin],DATEADD('Date Table'[Date],-1,YEAR))

-Sums the net sales from the financials dataset.
Sales Amount = SUM(financials[Net Sales])

-Shows total sales for the same period last year
Sales Amount LY = CALCULATE([Sales Amount],DATEADD('Date Table'[Date],-1,YEAR))

-Retrieves the sales value for the top three products, based on the selected filters.
Top 3 products by sales = CALCULATE([Sales Amount], TOPN(3,ALLSELECTED(financials[Product]),[Sales Amount],DESC),VALUES(financials[Product]))

-Used as a flag to indicate if the “Top 3 products by sales” measure contains a valid (non-blank) value.
Top highlight = IF(ISBLANK([Top 3 products by sales]),0,1)

-Generates a basic date table with Month Number, Month Name, and Year columns, using the built-in CALENDARAUTO() function.
Date Table = 
 
 ADDCOLUMNS(CALENDARAUTO(),
 "Month No",MONTH([Date]),
 "Month Name",FORMAT([Date],"MMMM"),
 "Year",YEAR([Date])
 )

## Snapshot of the Dashboard

![BIReport](https://github.com/user-attachments/assets/51eca006-1a65-4972-90dc-22376305df91)

---

## Key Insights & Findings

1. Year-over-Year (YoY) Growth  
   - 'Sales': \~92M (current), up from \~26M last year (+249.46%).  
   - 'Orders': \~861K (current), up from \~264K last year (+225.36%).  
   - 'Profit': \~13M (current), up from \~3.9M last year (+235.58%).  

2. Profit Margin Changes 
   - Current profit margin is 14.1%, slightly lower compared to 14.7% last year (-3.97%).  
   - While sales and profit have grown significantly, the margin reduction may indicate increased costs or higher discounts.

3. Discount Trends  
   - Total discount of \~7.06M, up from \~2.15M last year (+229.04%).  
   - Most discounts are in the “High” band (57.8%), suggesting a need to evaluate promotional strategies to ensure they do not erode profitability.

4. Geographical Performance  
   - Top countries by orders: Canada (247K), France (241K), United States (233K), Mexico (203K), and Germany (201K).  
   - Profit margin is highest in Germany (15.7%), closely followed by France (15.5%), while the United States is lower at 12%.  

5. Segment & Product Analysis 
   - Channel Partners' segment has the highest profit margin (\~73%), indicating effective collaboration or pricing strategy.  
   - 'Enterprise' segment margin is negative (-3.13%), likely requiring cost optimization or reevaluation of B2B pricing.  
   - Top three products by sales are *Paseo* (33K), *VTT* (20.5K), and *Velo* (18.25K).

6. Monthly & Yearly Sales 
   - Sales trends show spikes in certain months, suggesting potential seasonal promotions or events that drive revenue.  
   - Monitoring monthly fluctuations can help plan inventory and marketing campaigns more effectively.

---

## Recommendations

1. Margin Improvement  
   - Investigate why overall margins have fallen, despite higher total profit. This could be due to 'increased promotional discounts' or 'rising operational costs'.  
   - Reassess the “High” discount band strategy to protect profit margins.

2. Cost Optimization in the Enterprise Segment  
   - With a negative profit margin, Enterprise accounts may need renegotiated contracts, improved cost efficiencies, or refined product bundles to restore profitability.

3. Geographic Expansion & Diversification  
   - Continue focusing on high-performing countries like Germany and France, but develop action plans for the United States and Mexico to improve their margins.

4. Product Portfolio Strategy  
   - Align marketing and inventory for top-selling products (Paseo, VTT, Velo) to maximize revenue.  
   - Evaluate whether underperforming products can be repositioned or phased out.

5. Ongoing Monitoring  
   - Update and review this dashboard periodically (e.g., monthly or quarterly) to track progress on discount optimization, segment profitability, and overall margin improvement.

---

## Conclusion

This 'Virgin Megastore Financial Analysis Report' centralizes key metrics, helping stakeholders quickly identify areas of strong performance as well as opportunities for improvement. By taking action based on these insights—optimizing discounts, reevaluating unprofitable customer segments, and improving underperforming geographies—the company can continue its strong sales growth while also safeguarding overall profitability.

> Note: The calculations and insights in this dashboard can change dynamically based on the filters applied (e.g., time period, product categories, countries). Continual updates to the data source ensure the report remains relevant for decision-making.

