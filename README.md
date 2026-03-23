# 🛒 E-Commerce Marketing Analytics — End-to-End Project
---

## 📌 Project Overview

This project delivers a full-scale marketing analytics solution for one of India's leading e-commerce marketplaces. I Acting as a data analyst, the goal was to clean multi-table transactional data and extract actionable insights across customers, sellers, products, payments, and geographies — The project covers the full data pipeline: starting from raw, messy transactional data across 8 tables, cleaning it thoroughly, and then analysing it to answer real business questions.

![Alt text](https://www.softwaresuggest.com/blog/wp-content/uploads/2023/10/eCommerce-Analytics-Challenges-Opportunities-and-Best-Practices.jpg)

The insights cover who the customers are, what they buy, when they buy, how they pay, how satisfied they are, and which products are often bought together.
The final output gives the business a data-driven foundation to make smarter decisions around marketing, inventory, seller management, and customer retention.

---

## 📂 Dataset Overview

| Table | Description | Records |
|---|---|---|
| `CUSTOMERS.csv` | Customer demographics & location | 99,441 |
| `ORDERS.csv` | Order lifecycle & status | 99,441 |
| `ORDER_ITEMS.csv` | Product-level order details | 112,650 |
| `ORDER_PAYMENTS.csv` | Payment transactions | 103,886 |
| `ORDER_REVIEW_RATINGS.csv` | Customer review scores | 100,000 |
| `PRODUCTS.csv` | Product catalogue & dimensions | 32,951 |
| `SELLERS.csv` | Seller profiles | 3,095 |
| `GEO_LOCATION.csv` | Zip-code level geo coordinates | 19,015 |

---

##  Data Cleaning & Pre-processing

The raw data required several cleaning steps before analysis:

- **Type Conversion** — Parsed all date/timestamp columns (`order_purchase_timestamp`, `order_approved_at`, `shipping_limit_date`, `review_creation_date`) to proper `datetime` objects.
- **Column Renaming** — Fixed typos in the `products` table (`product_name_lenght` → `product_name_length`, `product_description_lenght` → `product_description_length`).
- **Missing Value Handling** — Dropped rows with nulls in `orders`, `products`, and `sellers` tables. Filled `product_category_name` nulls with `'unknown'` in analytical joins.
- **Duplicate Review Handling** — Identified reviews with duplicate `review_id` linked to different orders (data integrity issue) — kept the first. For orders with multiple review updates, kept the **latest** review to reflect the most genuine customer sentiment.
- **Out-of-Scope Records** — Removed `order_items` with `shipping_limit_date` beyond 2018 (outside project scope).
- **Zero-Weight Products** — Removed products with `product_weight_g = 0` as physically unrealistic.
- **Payment Normalisation** — Replaced `'not_defined'` payment type with `'Unknown'`.
- **Missing IDs** — Identified 628 product IDs in `order_items` with no matching product record, and 57 seller IDs with no seller registration (handled gracefully via join strategy).

---

## 📊 Analysis & Key Findings

### 1️⃣ High-Level Business Metrics

| Metric | Value |
|---|---|
| **Total Revenue (incl. freight)** | ₹ 16,008,872 |
| **Total Revenue (product price only)** | ₹ 13,591,298 |
| **Total Items Sold** | 1,12,646 |
| **Total Unique Products** | 32,323 |
| **Total Product Categories** | 71 |
| **Total Active Sellers** | 3,038 |
| **Total States Covered** | 20 |
| **Total Cities** | 3,809 |
| **Total Zip Code Areas** | 19,015 |
| **Payment Methods Available** | 5 |
| **Orders Delivered** | 96,455 |
| **Orders Cancelled** | 6 |

>  **Insight:** Extremely low cancellation rate (< 0.01%) indicates strong order fulfilment reliability.

---

### 1b. New Customer Acquisition (Monthly)

Monthly new customer acquisition was tracked by identifying each `customer_unique_id`'s first-ever purchase month. This revealed growth trends and seasonal spikes across the 2016–2018 period.

---

### 1c. Customer Retention (Month-on-Month)

Cohort-style retention analysis tracked which customers returned in subsequent months after their first purchase, providing month-on-month retention rates.

>  **Insight:** The majority of customers are one-time buyers — a common pattern in e-commerce — highlighting the need for loyalty and re-engagement programs.

---

### 1d. Revenue from New vs. Existing Customers

Revenue was split by customer type (new vs. returning) per month, showing the contribution of acquired vs. retained customers to overall revenue growth.

---

### 1e. Trends & Seasonality

- **Monthly/Weekly Trends:** Clear upward growth trajectory from late 2016 through mid-2018, with a peak around Q4 2017 (festive season).
- **Day-of-Week Trends:** Weekdays consistently outperform weekends in both order volume and revenue.
- **Hourly Trends:** Peak ordering hours fall during the afternoon and evening, suggesting a working-hours and post-work shopping pattern.
- **Top Category by State (Sample — Andhra Pradesh):**
  - Bed, Bath & Table — 6,976 units
  - Health & Beauty — 5,880 units
  - Sports & Leisure — 5,185 units
  - Furniture & Décor — 5,117 units
  - Computers & Accessories — 4,730 units

---

### 1f & 1g. Popular Products & Categories

- Products were ranked by units sold across **month**, **seller**, **state**, and **category** dimensions.
- Categories were ranked by units sold across **state** and **month** dimensions.
- In the early months (Sep–Oct 2016), **Health & Beauty** and **Furniture & Décor** dominated. By 2018, **Bed, Bath & Table** emerged as a consistent leader across states.

---

### 1h. Top 10 Most Expensive Products

Products were deduplicated by `product_id` using median price to avoid fluctuations, then ranked. These high-ticket items predominantly belong to premium electronics and furniture categories.

---

### 2️⃣ Customer & Seller Segmentation

#### Customer Segmentation (by Revenue Generated)

Customers were grouped into revenue bands using `pd.cut` on total spend:

| Segment | Revenue Range |
|---|---|
| Low Value | ₹ 0 – 1,000 |
| Mid Value | ₹ 1,000 – 5,000 |
| High Value | ₹ 5,000+ |

>  **Insight:** A large proportion of customers fall in the low-value segment — opportunity for upselling through recommendations and bundling.

#### Seller Segmentation (Decile Analysis)

Sellers were divided into **10 deciles** based on total revenue generated (using `pd.qcut`), from Decile 1 (lowest performing) to Decile 10 (top performers).

>  **Insight:** The top decile of sellers accounts for a disproportionately large share of total revenue — classic Pareto distribution. Nurturing top-decile sellers is critical.

---

### 3️⃣ Cross-Selling — Market Basket Analysis

Using combinatorics on multi-item orders, the **top 10 product pairs** and **top 10 product triplets** most frequently purchased together were identified.

- Multi-item orders were isolated by filtering `order_id`s with more than one item.
- All 2-item and 3-item combinations per order were enumerated using `itertools.combinations`.
- Frequency counted using `collections.Counter`.

>  **Insight:** Cross-sell bundles can be surfaced as "Frequently Bought Together" recommendations on the product pages to increase average order value.

---

### 4️⃣ Payment Behaviour

| Payment Method | Characteristic |
|---|---|
| **Credit Card** | Most used; drives the highest total revenue |
| **UPI** | Widely used; predominantly for smaller transactions |
| **Debit Card** | Rarely used |
| **Voucher** | Used for discounts and repeat purchases |
| **Unknown** | Small volume; likely system/legacy entries |

>  **Insight:** Credit card dominance signals an opportunity to offer EMI-based offers to drive higher-ticket purchases. UPI's prevalence suggests targeting mobile-first, younger demographics with UPI-exclusive deals.

---

### 5️⃣ Customer Satisfaction — Ratings Analysis

#### Top & Bottom Rated Categories (Weighted Rating)
- Weighted ratings (adjusted for review volume) were computed per category to avoid bias from sparse ratings.
- Top 10 highest-rated and lowest-rated categories were identified.

#### Top & Bottom Rated Products
- Products ranked by average rating (minimum review threshold applied for reliability).
- Top performers consistently had **5.0 average ratings** with 12–15+ reviews.

#### Average Ratings by Dimension

| Dimension | Analysis Performed |
|---|---|
| **Location** | Average rating by state and city |
| **Seller** | Top 10 highest-rated and lowest-rated sellers |
| **Product** | Ranked by avg rating × review count |
| **Category** | Simple and weighted average |
| **Month** | Trend of average rating over time |

>  **Insight:** Monthly rating trends help identify if service quality degraded during high-volume periods (e.g., festive season), which is actionable for logistics and customer support planning.

---

## 🗂️ Project Structure
```
├── E-Commerce_Analytics_End_to_end_Project.ipynb   # Main analysis notebook
├── Final_Capstone_Project_-_Marketing_Analytics.pdf # Project documentation
├── CUSTOMERS.csv
├── ORDERS.csv
├── ORDER_ITEMS.csv
├── ORDER_PAYMENTS.csv
├── ORDER_REVIEW_RATINGS.csv
├── PRODUCTS.csv
├── SELLERS.csv
├── GEO_LOCATION.csv
└── README.md
```

---

##  How to Run

1. **Clone the repository:**
```bash
   git clone https://github.com/vikasnagar31/your-repo-name.git
   cd your-repo-name
```

2. **Install dependencies:**
```bash
   pip install pandas numpy matplotlib seaborn
```

3. **Launch the notebook:**
```bash
   jupyter notebook E-Commerce_Analytics_End_to_end_Project.ipynb
```

4. **Run all cells sequentially** from top to bottom — later cells depend on earlier transformations.

---

##  Dependencies

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, transformation |
| `numpy` | Numerical operations |
| `matplotlib` | Data visualisation |
| `seaborn` | Statistical plots |
| `itertools` | Combination generation for market basket analysis |
| `collections` | Frequency counting for cross-sell pairs/triplets |

---

##  Business Recommendations Summary

1. **Retention Programs** — Most customers buy only once. Implement personalised re-engagement campaigns (email/push) targeting lapsed buyers.
2. **Seller Development** — Bottom-decile sellers need support (training, logistics) to improve output and reduce churn.
3. **Cross-Sell Bundles** — Use identified product pairs/triplets to build "Frequently Bought Together" features and bundle discounts.
4. **Credit Card EMI Offers** — Credit card is the top payment channel; partner with banks for zero-cost EMI to drive higher-value purchases.
5. **Category Focus** — Bed, Bath & Table, Health & Beauty, and Sports & Leisure are consistently top categories across states — prioritise inventory and promotions here.
6. **Peak Hour Marketing** — Afternoon/evening is peak ordering time; schedule campaigns and flash sales during these hours.
7. **Festive Season Prep** — Q4 shows consistent demand spikes; plan logistics and seller inventory well in advance.
8. **Rating Monitoring** — Track low-rated sellers and categories proactively; poor ratings in high-volume categories directly impact repeat purchases.

---

## 👤 Author

**Vikas Nagar**  
[LinkedIn](https://www.linkedin.com/in/vikas31/) · 
