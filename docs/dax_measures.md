# DAX Measures · Medidas DAX

All measures live in the `_Measures` table, organized in display folders.
*Todas las medidas están en la tabla `_Measures`, organizadas en carpetas.*

**Validated values** come from the full dataset and were cross-checked against Power Query and Google Sheets.
*Los **valores validados** se obtuvieron con todos los datos y se comprobaron contra Power Query y Google Sheets.*

---

## 📁 Sales · Ventas

| Measure | DAX | Description (EN / ES) | Validated value |
|---|---|---|---|
| **Sales** | `CALCULATE( SUM(order_items[price]), orders[is_sale] = TRUE() )` | Product sales from valid orders (not canceled or unavailable) / Ventas de productos de pedidos válidos | R$ 13,494,400.74 |
| **Sales M** | `DIVIDE( [Sales], 1000000 )` | Display measure in millions (format `R$ #,0.0"M"`) / Medida de presentación en millones | R$ 13.5M |
| **Sales K** | `DIVIDE( [Sales], 1000 )` | Display measure in thousands (format `R$ #,0"K"`) / Medida de presentación en miles | — |
| **Orders** | `CALCULATE( DISTINCTCOUNT(order_items[order_id]), orders[is_sale] = TRUE() )` | Unique valid orders (counted from order_items so category filters work) / Pedidos válidos únicos | 98,199 |
| **Items** | `CALCULATE( COUNTROWS(order_items), orders[is_sale] = TRUE() )` | Items sold / Artículos vendidos | — |
| **Avg Ticket** | `DIVIDE( [Sales], [Orders] )` | Average order value / Ticket promedio | R$ 137.42 |
| **Items per Order** | `DIVIDE( [Items], [Orders] )` | Average basket size / Artículos por pedido | 1.14 |
| **Avg Item Price** | `DIVIDE( [Sales], [Items] )` | Average price per item / Precio promedio por artículo | R$ 120.38 |
| **Sales LY** | `CALCULATE( [Sales], SAMEPERIODLASTYEAR(Calendar[Date]) )` | Sales in the same period last year / Ventas del mismo periodo del año anterior | — |
| **YoY %** | `DIVIDE( [Sales] - [Sales LY], [Sales LY] )` | Year-over-year growth (only meaningful for comparable periods) / Crecimiento anual (solo con periodos comparables) | — |
| **Growth Jan-Aug** | see below / ver abajo | Like-for-like growth, Jan–Aug 2018 vs. 2017 / Crecimiento comparable | 138.3% |

```dax
Growth Jan-Aug =
VAR Sales2018 =
    CALCULATE( [Sales], DATESBETWEEN(Calendar[Date], DATE(2018,1,1), DATE(2018,8,31)) )
VAR Sales2017 =
    CALCULATE( [Sales], DATESBETWEEN(Calendar[Date], DATE(2017,1,1), DATE(2017,8,31)) )
RETURN
    DIVIDE( Sales2018 - Sales2017, Sales2017 )
```
> **Why?** The generic `YoY %` compared 8 months of 2018 against 12 months of 2017 when a year was selected. This measure always compares equivalent periods.
> ***¿Por qué?** El `YoY %` genérico comparaba 8 meses de 2018 contra 12 meses de 2017. Esta medida siempre compara periodos equivalentes.*

---

## 📁 Delivery · Entregas

| Measure | DAX | Description (EN / ES) | Validated value |
|---|---|---|---|
| **Delivered Orders** | `COUNT(orders[delivery_days])` | Orders delivered with a delivery date (COUNT ignores blanks) / Pedidos entregados con fecha | 96,470 |
| **Late Orders** | `CALCULATE( COUNTROWS(orders), orders[delivery_status] = "Late" )` | Delivered after the estimated date / Entregados después de la fecha estimada | 6,534 |
| **% Late** | `DIVIDE( [Late Orders], [Delivered Orders] )` | Share of late deliveries (base = delivered orders) / % de entregas tardías | 6.8% |
| **Avg Delivery Days** | `AVERAGE(orders[delivery_days])` | Mean days from purchase to delivery / Días promedio | 12.1 |
| **Median Delivery Days** | `MEDIAN(orders[delivery_days])` | Median, robust to outliers (max = 209 days) / Mediana, robusta a atípicos | 10 |

---

## 📁 Reviews · Reseñas

| Measure | DAX | Description (EN / ES) | Validated value |
|---|---|---|---|
| **Avg Review Score** | `AVERAGE(order_reviews[review_score])` | Average rating (1–5); reviews pre-aggregated to one per order / Calificación promedio; reseñas agrupadas a una por pedido | 4.09 |

---

## 📁 Customers · Clientes

| Measure | DAX | Description (EN / ES) | Validated value |
|---|---|---|---|
| **Unique Customers** | `DISTINCTCOUNT(customers[customer_unique_id])` | Real people (`customer_id` is created per order) / Personas reales | 96,096 |
| **Repeat Customers** | see below / ver abajo | Customers with more than one order / Clientes con más de un pedido | 2,997 |
| **Repeat Rate** | `DIVIDE( [Repeat Customers], [Unique Customers] )` | Repeat purchase rate / Tasa de recompra | 3.1% |
| **% Customers** | see below / ver abajo | Share of all customers, ignoring the state filter / % del total de clientes | SP 41.9% |

```dax
Repeat Customers =
COUNTROWS(
    FILTER(
        VALUES(customers[customer_unique_id]),
        CALCULATE( COUNTROWS(customers) ) > 1
    )
)
```

```dax
% Customers =
DIVIDE(
    [Unique Customers],
    CALCULATE( [Unique Customers], REMOVEFILTERS(customers[customer_state]) )
)
```
> **Why?** "Show value as % of grand total" divided by the visible top 10 states only (46.4% for SP). `REMOVEFILTERS` makes the denominator the national total (41.9%).
> ***¿Por qué?** "Mostrar valor como % del total general" dividía solo entre los 10 estados visibles (46.4% para SP). `REMOVEFILTERS` hace que el denominador sea el total nacional (41.9%).*

---

## 📅 Calendar table · Tabla calendario

```dax
Calendar =
ADDCOLUMNS(
    CALENDAR(DATE(2016, 1, 1), DATE(2018, 12, 31)),
    "Year", YEAR([Date]),
    "Quarter", "Q" & QUARTER([Date]),
    "Month Number", MONTH([Date]),
    "Month", FORMAT([Date], "mmm"),
    "Year-Month", FORMAT([Date], "yyyy-mm")
)
```
Plus / más: `Month EN = FORMAT(Calendar[Date], "mmm", "en-US")`. 1,096 rows, marked as date table, related 1:* to `orders[purchase_date]`.
