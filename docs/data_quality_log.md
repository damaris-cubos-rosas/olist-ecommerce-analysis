# Data-Quality Log · Bitácora de calidad de datos

Every issue found during profiling and cleaning, with the decision taken.
*Cada problema encontrado durante el perfilado y la limpieza, con la decisión tomada.*

| # | Table | Finding (EN) | Hallazgo (ES) | Count | Decision / Decisión |
|---|---|---|---|---|---|
| 1 | orders | Orders without delivery date | Pedidos sin fecha de entrega | 2,965 | Kept; delivery times use only delivered orders with a date / Se conservan; los tiempos usan solo entregados con fecha |
| 2 | orders | "delivered" orders without delivery date | Pedidos "delivered" sin fecha de entrega | 8 | Excluded from delivery-time metrics / Excluidos de los tiempos de entrega |
| 3 | orders | Incomplete months (2016, Sep–Oct 2018); Nov 2016 missing | Meses incompletos (2016, sep–oct 2018); falta nov 2016 | — | Trend: Jan 2017–Aug 2018; growth: Jan–Aug vs. Jan–Aug / Tendencia ene 2017–ago 2018; crecimiento ene–ago |
| 4 | orders | "canceled" orders with a delivery date | Pedidos "canceled" con fecha de entrega | 6 | Treated as canceled / Tratados como cancelados |
| 5 | all | No cost data | Sin datos de costos | — | No margin analysis; stated as a limitation / Sin análisis de margen; se declara como limitación |
| 6 | customers | `customer_id` is created per order, not per person | `customer_id` se crea por pedido, no por persona | — | Repeat analysis uses `customer_unique_id` / La recompra usa `customer_unique_id` |
| 7 | reviews | Duplicate `review_id`; orders with several reviews | `review_id` duplicado; pedidos con varias reseñas | 99,224 → 98,673 | Grouped to one average score per order / Agrupado a una calificación promedio por pedido |
| 8 | order_items | Orders without items | Pedidos sin artículos | 775 | Sales calculated from order_items / Ventas calculadas desde order_items |
| 9 | payments | Order without payment record | Pedido sin registro de pago | 1 | Documented / Documentado |
| 10 | category_translation | Header row not promoted | Encabezado no promovido | — | Fixed (Use first row as headers) / Corregido |
| 11 | products | Products without category | Productos sin categoría | 610 | Labeled "Uncategorized" / Etiquetados "Uncategorized" |
| 12 | products | 2 categories missing from the translation table | 2 categorías sin traducción | 2 | Translated manually (Gaming Pc, Portable Kitchen Appliances) / Traducidas manualmente |
| 13 | orders | Delivery-time outliers (max 209 days) | Valores atípicos en días de entrega (máx. 209) | 4,117 > 30 days | Kept; median reported alongside mean; delivery ranges created / Se conservan; se reporta mediana y promedio; rangos de entrega |
| 14 | category_translation | Typos in the source file ("Costruction", "Fashio") | Errores ortográficos en el archivo original | 3 categories | Corrected; still 74 categories / Corregidos; siguen siendo 74 categorías |
| 15 | orders | Statuses with tiny samples: approved (2), created (5) | Estados con muestras mínimas | 7 | Excluded from comparisons / Excluidos de las comparaciones |
| 16 | customers | Roraima (RR) has only 45 customers | Roraima (RR) tiene solo 45 clientes | 45 | Shown with customer count in tooltip / Se muestra con el número de clientes en el tooltip |

**Key validation checks · Validaciones clave**
- Order status counts sum to the total (99,441). / La suma por estado cuadra con el total.
- Primary keys verified (Distinct = Unique = Row count) for orders, customers, products, sellers. / Llaves primarias verificadas.
- Row counts preserved after every merge (products: 32,951). / Filas conservadas tras cada combinación.
- Power BI measures match Google Sheets (valid sales R$ 13,494,400.74; Jan–Aug 2017 R$ 3,080,850.81; Jan–Aug 2018 R$ 7,341,037.41). / Las medidas de Power BI cuadran con Google Sheets.
