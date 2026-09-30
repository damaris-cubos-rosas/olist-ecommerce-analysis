# Olist · Análisis de ventas, entregas y clientes (2016–2018)

**Autora:** Dámaris Cubos Rosas · **Herramientas:** LibreOffice Calc · Google Sheets · Power BI (Power Query + DAX)
**Datos:** Brazilian E-Commerce Public Dataset by Olist (Kaggle) · 99,441 pedidos · sep 2016 – oct 2018 · cifras en reales brasileños (R$)

---

## 🎯 Mensaje principal

> **Olist está creciendo rápido (ventas ×2.4 en un año), pero ese crecimiento depende de clientes nuevos: solo 3.1% vuelve a comprar, y cuando una entrega llega tarde la calificación cae de 4.29 a 2.27 estrellas. Cumplir la fecha prometida y trabajar la recompra son las dos palancas con mayor potencial.**

---

## 1. Contexto

Olist es un **marketplace** brasileño: conecta a vendedores independientes con compradores en línea y gestiona la logística. No tiene inventario propio.

El análisis se planteó como un **caso de negocio simulado**: responder las cuatro preguntas que la gerencia de un e-commerce haría sobre su operación. Las preguntas las definí yo al inicio del proyecto, a partir de los datos disponibles:

1. ¿Cómo evolucionan las ventas y hay estacionalidad?
2. ¿Qué categorías generan más ingresos?
3. ¿Quiénes son los clientes, dónde están y cuántos vuelven a comprar?
4. ¿Cómo afectan las entregas tardías a la satisfacción del cliente?

---

## 2. Hallazgos principales

### 📈 Ventas y estacionalidad
- **Ventas totales: R$ 13.5M** en 98,199 pedidos válidos, con un ticket promedio de **R$ 137.42**.
- **Las ventas se multiplicaron ×2.4:** R$ 3.08M (ene–ago 2017) → R$ 7.34M (ene–ago 2018), **+138%** comparando los mismos meses.
- **Pico en noviembre de 2017: R$ 1.0M, +52% vs. octubre**, coincidente con Black Friday. *Solo existe un noviembre completo en los datos, así que la estacionalidad aún no puede confirmarse.*
- Las cancelaciones representan solo **0.7%** de las ventas: no son un problema relevante.

### 🏷️ Categorías
- **10 de 74 categorías generan el 58.8% de las ventas.** La líder es Health & Beauty (9.3%).
- Health & Beauty lidera por **precio**, no por volumen: R$ 130 por artículo contra R$ 93 de Bed, Bath & Table, que es la categoría con más pedidos.

### 👥 Clientes
- **96,096 clientes únicos**, de los cuales **solo 3.1% compró más de una vez.**
- **1.14 artículos por pedido:** casi 9 de cada 10 pedidos llevan un solo producto.
- **São Paulo concentra el 41.9% de los clientes.** Los estados del norte esperan hasta **3.5 veces más** su pedido (Roraima 29 días vs. São Paulo 8.3).

### 🚚 Entregas y satisfacción (hallazgo principal)
- Entrega promedio de **12.1 días** (mediana de 10). **6.8% de los pedidos llega tarde.**
- **La calificación depende de cumplir la promesa:**

| Situación del pedido | Calificación promedio |
|---|---|
| Entregado a tiempo | ⭐ 4.29 |
| Entregado tarde | ⭐ 2.27 |
| No entregado | ⭐ 1.75 |

- La calificación cae en escalera según los días de espera y **se desploma después de 30 días** (2.18 ⭐).
- Los pedidos **atorados en "processing"** reciben la peor calificación (**1.27 ⭐**), incluso peor que los cancelados (1.80 ⭐).
- **Los clientes de estados lejanos califican casi igual que los de São Paulo**, aunque esperen más. Esto sugiere que **lo que molesta no es esperar, sino que no se cumpla la fecha prometida.**

---

## 3. Recomendaciones

| # | Recomendación | Por qué (dato) | KPI y meta (12 meses) | Impacto estimado* |
|---|---|---|---|---|
| 1 | **🚚 Cumplir la fecha prometida.** Recalibrar la fecha estimada de entrega (sobre todo en estados lejanos) y activar alertas para pedidos en riesgo o atorados en "processing". | Tarde = 2.27 ⭐ vs. a tiempo = 4.29 ⭐; "processing" = 1.27 ⭐. | % Entregas tardías: **6.8% → < 5%** | ≈ 1,700 pedidos menos con una experiencia negativa |
| 2 | **🔁 Programa de recompra.** Campañas personalizadas para quienes ya compraron, según la categoría que adquirieron, apoyadas en entregas puntuales. | De 96,096 clientes, 93,099 compraron una sola vez. | Tasa de recompra: **3.1% → 5%** | ≈ 1,800 clientes recurrentes más → **≈ R$ 250K** (un pedido adicional cada uno) |
| 3 | **🛒 Venta cruzada.** Recomendar productos complementarios en el carrito y en la página del producto ("frecuentemente comprados juntos"). | 1.14 artículos por pedido. | Artículos por pedido: **1.14 → 1.25** | Ticket +R$ 13 (+9.6%) → **≈ R$ 1.3M** sobre el volumen histórico |
| 4 | **🏷️ Priorizar las categorías líderes.** Concentrar marketing y la atracción de vendedores en las 10 categorías principales; evaluar por separado las otras 64 categorías (41% de las ventas) antes de tomar decisiones sobre ellas. | 10 de 74 categorías = 58.8% de las ventas. | Ventas del top 10: **+15%** | **≈ R$ 1.2M** adicionales |
| 5 | **🛍️ Preparar Black Friday.** Campañas y ofertas anticipadas, junto con capacidad logística reforzada para no generar retrasos en el pico. Medir el resultado para confirmar la estacionalidad. | Nov 2017: +52% vs. octubre. | Crecimiento nov vs. oct: **+52% → +70%** | **≈ R$ 120K** adicionales en el mes pico |

\* *Estimaciones aproximadas sobre la base histórica del dataset (sep 2016 – ago 2018), en ventas de productos (sin flete). Sirven para dimensionar oportunidades, no como pronóstico.*

---

## 4. Supuestos y limitaciones

- **Venta** = pedido no cancelado ni marcado como no disponible (venta comprometida). No hay datos de devoluciones.
- **No hay datos de costos**, por lo que no se analiza margen ni rentabilidad.
- **Crecimiento** medido solo con meses comparables (ene–ago); 2016 y sep–oct 2018 están incompletos.
- **Reseñas:** cuando un pedido tenía varias, se usó el promedio.
- **Días de entrega:** se conservaron los valores atípicos (hasta 209 días) y se reporta mediana además del promedio.
- **Muestras pequeñas:** los estados de pedido "approved" (2 pedidos) y "created" (5) se excluyeron de las comparaciones, porque con tan pocos casos una sola reseña cambia mucho el promedio y el resultado no es confiable. Roraima (45 clientes) se muestra, pero con su número de clientes visible para leerlo con cautela.
- **Correlación no es causalidad:** la relación entre retrasos y calificación es fuerte, pero puede haber otros factores (vendedor, producto, comunicación).
- **Limpieza de datos:** se documentaron 16 hallazgos de calidad (fechas faltantes, reseñas duplicadas, categorías sin traducción o con errores ortográficos, etc.), cada uno con su decisión.

---

## 5. Próximos pasos sugeridos

1. Analizar a los **vendedores**: ¿unos pocos concentran los retrasos?
2. Medir la **precisión de la fecha estimada** por estado: ¿en cuáles se promete de más?
3. **Segmentar clientes (RFM)** para dirigir las campañas de recompra.
4. Analizar **flete y métodos de pago** (parcialidades) y su relación con el ticket.
