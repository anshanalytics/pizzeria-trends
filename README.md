# 🍕 PIZZERIA TRENDS | Pizza Sales Analysis in Power BI

An interactive Power BI dashboard exploring pizza sales, order trends, product preferences, and menu pricing using the Pizza Place Sales dataset for 2015.

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Measures-blue)
![Dataset](https://img.shields.io/badge/Dataset-Maven%20Analytics-green)

---

## 📊 Dashboard Preview

<p align="center">
  <img src="PIZZERIA%20TRENDS.png" alt="Pizzeria Trends Power BI Dashboard" width="100%">
</p>

> The full interactive version is available in the `PIZZERIA TRENDS.pbit` template. Open it in Power BI Desktop to use the slicers and filters.

---

## 📌 Project Snapshot

| Metric | Value |
|---|---|
| Orders placed | 21,350 |
| Pizza units sold | 49,574 |
| Pizza types | 32 |
| Calculated revenue | $817,860.05 |
| Menu price range | $9.75 - $35.95 |

---

## ✨ Dashboard Features

- KPIs: pizzas sold, orders placed, and pizza types
- Orders by date, month, and time of day
- Top 10 bestsellers and pizza size/category comparisons
- Pizza name, ingredients, size, and price details
- Filters for size, category, and custom Veg/Non-veg classification
- Cheapest and most expensive pizza variants

---

## 🗂️ Data Model

```text
orders.order_id            -> order_details.order_id
pizzas.pizza_id            -> order_details.pizza_id
pizza_types.pizza_type_id  -> pizzas.pizza_type_id
```

These are active one-to-many relationships in the Power BI model.

---

## 🛠️ Tools & Skills

Power BI Desktop | Power Query | DAX | Data Modeling | Dashboard Design

---

## 🧮 Key DAX Measures

```DAX
Pizzas Sold = SUM ( 'order_details'[quantity] )

Orders Placed = DISTINCTCOUNT ( 'orders'[order_id] )

Total Revenue =
SUMX (
    'order_details',
    'order_details'[quantity] * RELATED ( 'pizzas'[price] )
)

Pizza Types = DISTINCTCOUNT ( 'pizza_types'[pizza_type_id] )

Cheapest Pizza = MIN ( 'pizzas'[price] )

Most Expensive Pizza = MAX ( 'pizzas'[price] )
```

---

## 💡 Key Insights

- The **Classic Deluxe Pizza** led sales by quantity with **2,453 units**.
- The **Classic** category generated the highest category revenue: **$220,053.10**.
- **12 PM** was the busiest order hour, with **2,520 orders**.

> These results describe the 2015 sample dataset. Report filters may change values shown in visuals.

---

## 📁 Dataset

- **Source:** [Maven Analytics - Pizza Place Sales](https://mavenanalytics.io/data-playground/pizza-place-sales)
- **Files:** `orders.csv`, `order_details.csv`, `pizzas.csv`, `pizza_types.csv`
- **Period:** January - December 2015

**Note:** Veg/Non-veg is a custom classification based on ingredient keywords, not a source field, and should be checked for edge cases. Revenue is quantity multiplied by listed price; taxes, discounts, refunds, and costs are not included.

---

## 🚀 How to Open

1. Download the dataset from the source link above.
2. Open `PIZZERIA TRENDS.pbit` in Power BI Desktop.
3. If needed, update the CSV paths in **Transform data > Data source settings**.
4. Refresh the data and explore the dashboard with the slicers.

---

## 📁 Repository Structure

```text
pizzeria-trends/
├── PIZZERIA TRENDS.pbit   # Power BI template
├── PIZZERIA TRENDS.png    # Dashboard screenshot
└── README.md
```

---

## 👤 Author

**Ansh Sharma** | GitHub: [@anshanalytics](https://github.com/anshanalytics)
