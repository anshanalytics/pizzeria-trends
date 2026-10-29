PIZZERIA TRENDS — PIZZA SALES ANALYSIS | POWER BI
=================================================

An interactive Power BI sales dashboard built to explore pizza sales performance, order timing, product preferences, and menu pricing. The report uses a dark burgundy visual theme and turns one year of transaction data into business-friendly KPIs and comparisons.

PROJECT TYPE: Data Analytics / Business Intelligence
TOOLS: Power BI Desktop, Power Query, DAX, Data Modeling
DATASET PERIOD: January–December 2015

1. PROJECT OVERVIEW
-------------------
The goal is to understand how a fictional pizza restaurant performed during 2015. The dashboard reviews order volume over time, compares pizza sizes and categories, identifies bestsellers, and examines menu prices.

Interactive slicers: Pizza Size, Pizza Category, and a custom Veg/Non-veg classification.

2. BUSINESS QUESTIONS
---------------------
- How many orders were placed and how many pizzas were sold?
- How does order activity change by date, month, and time of day?
- Which pizza types sell the most by quantity?
- How do pizza variants compare by size and category?
- What are the minimum and maximum listed pizza prices?
- How does the product mix change when users filter by size, category, or Veg/Non-veg classification?

3. DASHBOARD FEATURES
---------------------
- KPI cards: Pizzas Made, Orders Placed, Types of Pizza
- Price cards: Cheapest Pizza and Most Expensive Pizza
- Pizza details table: pizza name, ingredients, price, and size
- Orders by Date, Orders by Month, and Orders by Time
- Pizza Available by Size and Pizza by Category
- Bestsellers: Top 10 pizza types by quantity sold
- Pizza by Category and Size: stacked comparison across sizes
- Slicers: Pizza Size, Pizza Category, and custom Veg/Non-veg filter

4. DATASET
----------
Source: Maven Analytics — Pizza Place Sales
https://mavenanalytics.io/data-playground/pizza-place-sales

The dataset contains a year of fictional pizza restaurant transactions in four CSV tables:

Table: orders
Rows: 21,350
Fields: order_id, date, time
Purpose: One row per order with date and time.

Table: order_details
Rows: 48,620
Fields: order_details_id, order_id, pizza_id, quantity
Purpose: Pizza line items and quantities within orders.

Table: pizzas
Rows: 96
Fields: pizza_id, pizza_type_id, size, price
Purpose: Pizza size and price variants.

Table: pizza_types
Rows: 32
Fields: pizza_type_id, name, category, ingredients
Purpose: Pizza names, categories, and ingredients.

DATASET SNAPSHOT
- 21,350 distinct orders
- 49,574 pizza units sold
- 48,620 order-detail rows
- 32 distinct pizza types
- 96 pizza size/price variants
- $817,860.05 calculated revenue (quantity × listed unit price)
- $9.75–$35.95 listed price range across variants

5. DATA MODEL
-------------
Create these active one-to-many (1:*) relationships with Single cross-filter direction:

orders[order_id]          -> order_details[order_id]
pizzas[pizza_id]          -> order_details[pizza_id]
pizza_types[pizza_type_id] -> pizzas[pizza_type_id]

This allows dates and times to filter order details, while pizza size, price, name, category, and ingredients flow through related pizza tables.

6. KEY DAX MEASURES
-------------------
Total Pizzas Sold =
SUM ( 'order_details'[quantity] )

Total Orders =
DISTINCTCOUNT ( 'orders'[order_id] )

Total Revenue =
SUMX (
    'order_details',
    'order_details'[quantity] * RELATED ( 'pizzas'[price] )
)

Total Pizza Types =
DISTINCTCOUNT ( 'pizza_types'[pizza_type_id] )

Cheapest Pizza Price =
MIN ( 'pizzas'[price] )

Most Expensive Pizza Price =
MAX ( 'pizzas'[price] )

Average Order Value =
DIVIDE ( [Total Revenue], [Total Orders], 0 )

MONTH COLUMNS
Month Name = FORMAT ( 'orders'[date], "MMM" )
Month Number = MONTH ( 'orders'[date] )

After creating the columns, select orders[Month Name] and choose Column tools > Sort by column > Month Number.

TOP 10 BESTSELLERS
Use pizza_types[name] as the category and [Total Pizzas Sold] as the value. Apply a visual-level Top N filter: Top 10, By value = [Total Pizzas Sold].

7. HIGHLIGHTS FROM THE DATA
---------------------------
Calculated from the CSV files before report-level slicers are applied:
- 49,574 pizzas were sold across 21,350 distinct orders.
- The Classic Deluxe Pizza was the top individual pizza type by quantity, with 2,453 units sold.
- The Classic category generated the highest revenue among the four categories: $220,053.10.
- 12 PM was the busiest order hour, with 2,520 orders.
- Listed pizza variant prices ranged from $9.75 to $35.95.

These are dataset-level observations, not claims about a real restaurant. Visual values can change with slicers and report filters.

8. HOW TO OPEN THE PROJECT
--------------------------
1. Download or clone the repository.
2. Download the CSV files from the dataset source if they are not included in the repository.
3. Open the .pbix file in Power BI Desktop.
4. If Power BI cannot find the CSV files, go to Transform data > Data source settings and update the source paths.
5. Select Refresh to reload the data.
6. Use the slicers to explore the report.

9. SUGGESTED REPOSITORY STRUCTURE
---------------------------------
pizzeria-trends-power-bi/
  README.md
  Pizzeria-Trends.pbix
  assets/
    dashboard-screenshot.png
  data/                      (optional)
    orders.csv
    order_details.csv
    pizzas.csv
    pizza_types.csv

Update the example PBIX filename to the actual filename you upload. Once the dashboard is final, add a screenshot at assets/dashboard-screenshot.png.

10. SKILLS DEMONSTRATED
-----------------------
- Power BI dashboard design and visual formatting
- Data modeling and relationship management
- DAX measures and calculated columns
- Data aggregation and KPI definition
- Date sorting and time-based trend analysis
- Top N filtering and category comparisons
- Interactive slicers
- Communicating business insights through visual analytics

11. LIMITATIONS AND NOTES
------------------------
- The data represents a fictional restaurant and covers 2015 only.
- No customer ID is provided, so the report measures orders, not unique customers.
- The original data has no dedicated Veg/Non-veg field. A custom ingredient-keyword classification is an approximation and should be reviewed.
- Revenue is quantity multiplied by listed unit price; tax, discounts, refunds, and operating costs are not included.
- Counting pizza variants by size is not the same as counting units sold; use quantity for units sold.

AUTHOR
------
Ansh Sharma
GitHub: https://github.com/anshanalytics

Built as a portfolio project to practice data modeling, DAX, and business-focused dashboard design in Power BI.
