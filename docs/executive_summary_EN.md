# Olist · Sales, Delivery & Customer Analysis (2016–2018)

**Author:** Dámaris Cubos Rosas · **Tools:** LibreOffice Calc · Google Sheets · Power BI (Power Query + DAX)
**Data:** Brazilian E-Commerce Public Dataset by Olist (Kaggle) · 99,441 orders · Sep 2016 – Oct 2018 · figures in Brazilian reais (R$)

---

## 🎯 Key message

> **Olist is growing fast (sales up 2.4x in one year), but that growth relies on new customers: only 3.1% buy again, and when a delivery is late the rating drops from 4.29 to 2.27 stars. Keeping delivery promises and driving repeat purchases are the two levers with the greatest potential.**

---

## 1. Context

Olist is a Brazilian **marketplace**: it connects independent sellers with online shoppers and manages logistics. It holds no inventory of its own.

The analysis was framed as a **simulated business case**: answering the four questions an e-commerce management team would ask about its operation. I defined the questions at the start of the project, based on the available data:

1. How are sales evolving, and is there seasonality?
2. Which categories generate the most revenue?
3. Who are the customers, where are they, and how many come back?
4. How do late deliveries affect customer satisfaction?

---

## 2. Key findings

### 📈 Sales and seasonality
- **Total sales: R$ 13.5M** across 98,199 valid orders, with an average ticket of **R$ 137.42**.
- **Sales grew 2.4x:** R$ 3.08M (Jan–Aug 2017) → R$ 7.34M (Jan–Aug 2018), **+138%** comparing the same months.
- **Peak in November 2017: R$ 1.0M, +52% vs. October**, coinciding with Black Friday. *There is only one complete November in the data, so seasonality cannot be confirmed yet.*
- Cancellations account for only **0.7%** of sales: not a material issue.

### 🏷️ Categories
- **10 of 74 categories drive 58.8% of sales.** Health & Beauty leads (9.3%).
- Health & Beauty leads on **price**, not volume: R$ 130 per item vs. R$ 93 for Bed, Bath & Table, the category with the most orders.

### 👥 Customers
- **96,096 unique customers**, of whom **only 3.1% purchased more than once.**
- **1.14 items per order:** nearly 9 in 10 orders contain a single product.
- **São Paulo holds 41.9% of customers.** Northern states wait up to **3.5x longer** for their orders (Roraima 29 days vs. São Paulo 8.3).

### 🚚 Delivery and satisfaction (key finding)
- Average delivery time of **12.1 days** (median 10). **6.8% of orders arrive late.**
- **Ratings depend on keeping the promise:**

| Order outcome | Average rating |
|---|---|
| Delivered on time | ⭐ 4.29 |
| Delivered late | ⭐ 2.27 |
| Not delivered | ⭐ 1.75 |

- Ratings decline step by step with waiting time and **collapse after 30 days** (2.18 ⭐).
- Orders **stuck in "processing"** get the worst rating (**1.27 ⭐**), even lower than canceled orders (1.80 ⭐).
- **Customers in distant states rate almost the same as those in São Paulo**, even though they wait longer. This suggests that **what frustrates customers is not waiting, but a broken delivery promise.**

---

## 3. Recommendations

| # | Recommendation | Why (evidence) | KPI and target (12 months) | Estimated impact* |
|---|---|---|---|---|
| 1 | **🚚 Keep the delivery promise.** Recalibrate estimated delivery dates (especially for distant states) and trigger alerts for at-risk orders or orders stuck in "processing". | Late = 2.27 ⭐ vs. on time = 4.29 ⭐; "processing" = 1.27 ⭐. | % Late deliveries: **6.8% → < 5%** | ≈ 1,700 fewer orders with a negative experience |
| 2 | **🔁 Repeat-purchase program.** Personalized campaigns for past buyers based on the category they purchased, backed by on-time deliveries. | Of 96,096 customers, 93,099 bought only once. | Repeat customer rate: **3.1% → 5%** | ≈ 1,800 more returning customers → **≈ R$ 250K** (one extra order each) |
| 3 | **🛒 Cross-selling.** Recommend complementary products in the cart and on product pages ("frequently bought together"). | 1.14 items per order. | Items per order: **1.14 → 1.25** | Ticket +R$ 13 (+9.6%) → **≈ R$ 1.3M** on historical volume |
| 4 | **🏷️ Prioritize leading categories.** Focus marketing and seller acquisition on the top 10 categories; evaluate the other 64 categories (41% of sales) separately before making decisions about them. | 10 of 74 categories = 58.8% of sales. | Top-10 category sales: **+15%** | **≈ R$ 1.2M** additional |
| 5 | **🛍️ Prepare for Black Friday.** Early campaigns and offers, plus reinforced logistics capacity to avoid delays at the peak. Measure results to confirm seasonality. | Nov 2017: +52% vs. October. | Nov vs. Oct growth: **+52% → +70%** | **≈ R$ 120K** additional in the peak month |

\* *Rough estimates based on the dataset's historical baseline (Sep 2016 – Aug 2018), in product sales (excluding freight). They size opportunities; they are not forecasts.*

---

## 4. Assumptions and limitations

- **Sale** = order not canceled and not marked unavailable (committed sale). No return data is available.
- **No cost data**, so margin and profitability are not analyzed.
- **Growth** is measured only on comparable months (Jan–Aug); 2016 and Sep–Oct 2018 are incomplete.
- **Reviews:** when an order had several, their average was used.
- **Delivery days:** outliers (up to 209 days) were kept; the median is reported alongside the mean.
- **Small samples:** order statuses "approved" (2 orders) and "created" (5) were excluded from comparisons, because with so few cases a single review shifts the average dramatically and the result is not reliable. Roraima (45 customers) is shown, with its customer count visible so it can be read with caution.
- **Correlation is not causation:** the link between delays and ratings is strong, but other factors (seller, product, communication) may play a role.
- **Data cleaning:** 16 data-quality findings were documented (missing dates, duplicate reviews, untranslated or misspelled categories, etc.), each with its decision.

---

## 5. Suggested next steps

1. Analyze **sellers**: do a few of them concentrate the delays?
2. Measure **estimated-date accuracy** by state: where is Olist over-promising?
3. **Segment customers (RFM)** to target repeat-purchase campaigns.
4. Analyze **freight and payment methods** (installments) and their relationship with ticket size.
