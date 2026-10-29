PIZZERIA TRENDS
Pizza Sales Analysis | Power BI
================================

An interactive Power BI dashboard exploring pizza sales, order trends,
product preferences, and menu pricing using the Pizza Place Sales dataset
for 2015.

PROJECT SNAPSHOT
----------------
Orders placed          21,350
Pizza units sold       49,574
Pizza types            32
Calculated revenue     $817,860.05
Menu price range       $9.75-$35.95

DASHBOARD FEATURES
------------------
- KPIs: pizzas sold, orders placed, and pizza types
- Orders by date, month, and time of day
- Top 10 bestsellers and pizza size/category comparisons
- Pizza name, ingredients, size, and price details
- Filters for size, category, and custom Veg/Non-veg classification
- Cheapest and most expensive pizza variants

DATA MODEL
----------
orders.order_id        -> order_details.order_id
pizzas.pizza_id        -> order_details.pizza_id
pizza_types.pizza_type_id -> pizzas.pizza_type_id

These are active one-to-many relationships in the Power BI model.

TOOLS & SKILLS
--------------
Power BI Desktop | Power Query | DAX | Data Modeling | Dashboard Design

KEY DAX MEASURES
----------------
Pizzas Sold =
SUM ( 'order_details'[quantity] )

Orders Placed =
DISTINCTCOUNT ( 'orders'[order_id] )

Total Revenue =
SUMX (
    'order_details',
    'order_details'[quantity] * RELATED ( 'pizzas'[price] )
)

Pizza Types =
DISTINCTCOUNT ( 'pizza_types'[pizza_type_id] )

Cheapest Pizza = MIN ( 'pizzas'[price] )
Most Expensive Pizza = MAX ( 'pizzas'[price] )

KEY INSIGHTS
------------
- The Classic Deluxe Pizza led sales by quantity with 2,453 units.
- The Classic category generated the highest category revenue: $220,053.10.
- 12 PM was the busiest order hour, with 2,520 orders.

These results describe the 2015 sample dataset. Report filters may change
values shown in visuals.

DATASET
-------
Source: Maven Analytics - Pizza Place Sales
https://mavenanalytics.io/data-playground/pizza-place-sales

Files: orders.csv, order_details.csv, pizzas.csv, pizza_types.csv
Period: January-December 2015

Note: Veg/Non-veg is a custom classification based on ingredient keywords,
not a source field, and should be checked for edge cases. Revenue is
quantity multiplied by listed price; taxes, discounts, refunds, and costs
are not included.

HOW TO OPEN
-----------
1. Download the dataset from the source link.
2. Open the .pbix report in Power BI Desktop.
3. If needed, update CSV paths in Transform data > Data source settings.
4. Refresh the data and explore the dashboard with the slicers.

AUTHOR
------
Ansh Sharma | GitHub: https://github.com/anshanalytics
