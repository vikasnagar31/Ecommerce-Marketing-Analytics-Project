# Ecommerce-Marketing-Analytics-Project
An In-depth analysis of E-comm marketplace's data. This project focuses on providing data-driven insights into customer &amp; seller behavior, product performance, &amp; channel effectiveness to analyze overall business performance. Key analyses include EDA, customer &amp; seller segmentation, cross-selling analysis, payment behavior, &amp; customer satisfaction.

## Project Overview

This project presents a comprehensive analysis of business performance for a leading online marketplace in India. The primary objective is to leverage data to measure, manage, and analyze various aspects of the business, including customer behavior, seller performance, product trends, and channel effectiveness. The analysis covers a dataset spanning from September 2016 to October 2018, providing actionable insights to drive strategic business decisions. This repository serves as a showcase of my analytical skills in data cleaning, exploratory data analysis, customer segmentation, and deriving meaningful business intelligence.

## Business Context

The client is a prominent online marketplace in India seeking to partner with Analytixlabs to gain a deeper understanding of their business performance. As an analyst on this project, the goal is to provide data-driven insights by analyzing customer and seller behaviors, product performance, and channel effectiveness. This analysis is crucial for identifying areas of improvement, optimizing marketing strategies, and enhancing overall profitability.

## Data Overview

The dataset for this project consists of multiple interconnected tables, providing a holistic view of the marketplace's operations.

*   **Customers:** Contains information about the customers.
*   **Sellers:** Includes details about the sellers on the platform.
*   **Products:** Contains product-specific information.
*   **Orders:** Holds information about orders, including status and dates.
*   **Order_Items:** Provides details at the order item level.
*   **Order_Payments:** Contains information regarding order payments.
*   **Order_Review_Ratings:** Stores customer ratings for orders.
*   **Geo-Location:** Includes location details for shipping and customer addresses.

## Business Objectives

This analysis aims to address several key business questions. The following is a sample of the objectives explored:

1.  **Perform Detailed Exploratory Analysis:**
    *   Calculate high-level metrics such as Total Revenue, Total Quantity, Total Products, Total Categories, Total Sellers, Total Locations, Total Channels, and Total Payment Methods.
    *   Track the acquisition of new customers on a monthly basis.
    *   Analyze month-on-month customer retention.
    *   Understand the revenue contribution from new versus existing customers over time.
    *   Identify trends and seasonality in sales and quantity by various dimensions like category, location, time, channel, and payment method.
    *   Determine popular products and categories by month, seller, state.
    *   List the top 10 most expensive products.

2.  **Perform Customer/Seller Segmentation:**
    *   Group customers and sellers based on the revenue they generate to identify high-value segments.

3.  **Cross-Selling Analysis:**
    *   Identify the top 10 combinations of products that are frequently purchased together in a single transaction.

4.  **Payment Behavior Analysis:**
    *   Understand the preferred payment methods of customers.
    *   Identify the most frequently used payment channels.

5.  **Customer Satisfaction Analysis:**
    *   Determine the top 10 highest and lowest-rated product categories.
    *   Identify the top 10 highest and lowest-rated products.
    *   Calculate the average customer rating by location, seller, product, category, and month.

## Methodology

The project was executed following a structured analytical approach:

1.  **Data Cleaning and Preparation:** The initial phase involved a thorough cleaning of the provided dataset. This included handling missing values, correcting data types, and ensuring data consistency across all tables to prepare it for analysis.

2.  **Exploratory Data Analysis (EDA):** A deep dive into the data to uncover initial patterns, anomalies, and relationships. This involved calculating key business metrics and visualizing trends over time and across different segments.

3.  **Customer and Seller Segmentation:** Utilized RFM (Recency, Frequency, Monetary) analysis principles to segment customers and sellers based on their revenue contribution. This helps in tailoring marketing and seller management strategies.

4.  **Market Basket Analysis:** Implemented association rule mining (Apriori algorithm) to identify products that are frequently bought together, providing insights for cross-selling and product bundling strategies.

5.  **Behavioral Analysis:** Analyzed payment preferences and customer satisfaction ratings to understand user behavior and identify areas for improving the customer experience.
6.  etc...

## Tools and Libraries Used

*   **Programming Language:** Python
*   **Libraries:**
    *   **Pandas:** For data manipulation and analysis.
    *   **NumPy:** For numerical operations.
    *   **Matplotlib & Seaborn:** For data visualization.
    *   **Scikit-learn:** For machine learning algorithms (e.g., for segmentation).
 
## Project Structure
├── data/
│ ├── Customers.csv
│ ├── Sellers.csv
│ ├── Products.csv
│ ├── Orders.csv
│ ├── Order_Items.csv
│ ├── Order_Payments.csv
│ ├── Order_Review_Ratings.csv
│ └── Geo-Location.csv
├── notebooks/
│ └── E-Commerce_Analysis.ipynb
└── README.md
 
## How to Use This Repository

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/E-Commerce-Marketing-Analytics.git
    ```
2.  **Install the required libraries:**
    ```bash
    pip install pandas numpy matplotlib seaborn scikit-learn  
    ```
3.  **Explore the Jupyter Notebook:** The `notebooks/E-Commerce_Analysis.ipynb` file contains the complete step-by-step analysis  

## Contact

Feel free to reach out with any questions or feedback!

*   **Name:** Vikas Nagar
*   **LinkedIn:**  https://linkedin.com/in/vikas31
*   **GitHub:**  https://github.com/vikasnagar31
*   **Email:** nagarvikas2003@gmail.com
