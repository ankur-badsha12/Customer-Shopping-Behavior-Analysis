# End-to-End Retail Data Analytics Portfolio Project

This repository contains a professional, end-to-end data analytics project reflecting real-world corporate workflows [1]. It spans the complete data analytics life cycle: defining a business problem [1], executing data cleaning and feature engineering in Python [4, 7], performing advanced relational database analysis in PostgreSQL [15, 18], building an interactive Power BI KPI dashboard [4, 30], writing formal documentation [2, 41], and delivering stakeholder presentations [2, 42].

---

## 📌 Project Overview & Business Problem

A leading retail company aims to understand its customers' shopping behavior to improve sales, customer satisfaction, and long-term brand loyalty [3]. Over recent quarters, management has observed shifting purchase patterns across demographics, product categories, and sales channels [3].

The goal of this project is to analyze the customer behavior dataset and answer the core business question:
> **"How can the company leverage customer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?"** [3]

---

## 📂 Dataset Profile

Each row in the dataset represents an individual customer and details of their latest purchase [4]. The columns include:
*   **Customer ID:** Unique primary key identifying each customer [4, 5].
*   **Demographics:** Age and Gender [5].
*   **Product Information:** Item Purchased, Category, Size, Color, and Season [5].
*   **Transaction Details:** Purchase Amount (USD), Location, Shipping Type, and Payment Method [5].
*   **Promotions:** Discount Applied and Promo Code Used [5].
*   **Feedback & Engagement:** Review Rating, Subscription Status, Number of Previous Purchases, and Purchase Frequency [5].

---

## 🛠️ Step-by-Step Implementation

### Step 1: Data Cleaning & Feature Engineering (Python)
Using a Jupyter Notebook and **Pandas**, we clean and prepare the dataset to ensure a robust foundation for SQL and Power BI ingestion [4, 7]:
1.  **Imputing Missing Values:** The `review_rating` column contains 37 null values [8]. Rather than applying a broad median across the entire dataset (which introduces category bias), we impute missing ratings using the **median rating within each specific product category** (e.g., footwear missing ratings are filled with the footwear median) [8, 9, 10].
2.  **Standardising Column Names:** Converted mixed-case and spaced column names into **snake_case** (e.g., `customer_id`, `purchase_amount`) to maintain consistency and prevent syntax errors in SQL [10, 11].
3.  **Feature Engineering:**
    *   **Age Groups:** Created an `age_group` column dividing customers into four equal-sized distribution bins using `pd.qcut` (labels: *Young Adult, Adult, Middle-Aged, Senior*) [12].
    *   **Purchase Frequency Days:** Converted textual frequency values (weekly, fortnightly, monthly, quarterly) into numeric equivalents (e.g., 7 days, 14 days) via a custom mapping dictionary to facilitate numeric trend calculations [12, 13].
4.  **Redundancy Removal:** Dropped the `promo_code_used` column after validating that its values perfectly correlated with `discount_applied` (making one redundant) [14].

### Step 2: Advanced Data Analysis (SQL)
After cleaning, we connected the Jupyter Notebook to **PostgreSQL** using SQL Alchemy and `psycopg2` to write the data into a schema table named `customer` [15, 16]. We executed structured queries to extract deep business insights [18]:
*   **Revenue by Gender:** Analyzed total revenue split between male and female customers to tailor demographic campaigns [18, 19].
*   **High-Value Discount Buyers:** Located customers who received a discount but still spent more than the overall average purchase amount using SQL subqueries [19].
*   **Top-Rated Products:** Identified the top 5 products by highest average review rating (casting ratings to numeric values for rounding) to guide marketing spotlights [20, 21].
*   **Shipping & Spend Correlation:** Compared average spend between standard and express shipping to assess if express offerings correlate with higher-value transactions [21].
*   **Subscription Program Viability:** Analyzed the count, average spend, and total revenue of subscribed versus non-subscribed customers to measure subscription performance [22].
*   **Discount Dependency:** Calculated the percentage rate of discounted purchases for each product to find which items rely heavily on promotions to sell [23, 24].
*   **Customer Loyalty Segmentation:** Segmented customers into *New* (1 purchase), *Returning* (2-10 purchases), and *Loyal* (>10 purchases) categories using CTEs and CASE statements [25, 26].
*   **Top Products Per Category:** Ranked the top 3 items purchased within each category using the `ROW_NUMBER()` window function over category partitions [26, 27].
*   **Repeat Buyer Subscriptions:** Determined whether repeat buyers (customers with >5 previous purchases) are actively subscribing, highlighting gaps in subscription incentives [28, 29].
*   **Revenue by Age Group:** Calculated total spend across our engineered age demographics, indicating that young adults drive the most revenue [29].

### Step 3: Interactive Dashboard (Power BI)
We connected Power BI to PostgreSQL (`customer_behavior` database) [30] and built a fully interactive business dashboard:
*   **Dynamic Measures (DAX):** Formulated key metrics including `Number of Customers` (Count), `Average Purchase Amount` (Average formatted to USD), and `Average Review Rating` [31, 33].
*   **KPI Scorecard:** Designed a unified modern card visual showcasing high-level KPIs with styled rounded corners and brand-specific accent bars [31, 32].
*   **Visual Elements:**
    *   **Subscription Split:** Donut chart displaying the percentage of customers by subscription status [34, 35].
    *   **Category Performance:** Clustered column charts comparing sales volume vs. total revenue by product category [37].
    *   **Age Demographics:** Clustered bar charts breaking down revenue and sales count by age group [40].
*   **Interactivity Controls:** Added dynamic horizontal and vertical button slicers for *Subscription Status*, *Gender*, *Category*, and a list slicer for *Shipping Type* to allow real-time data drilling [38, 39, 41].

### Step 4: Reports & Presentation
*   **Documentation:** Prepared a formal project report detailing data transformations, database loading, query results, and strategic business recommendations [41, 42].
*   **Stakeholder Deck:** Imported the project report into Gamma AI to auto-generate a sleek, minimalist presentation slide deck tailored for managers and executive clients [42, 43].

---

## 📈 Key Insights & Business Recommendations

1.  **Demographic Focus:** Young adults generate the highest total revenue [29]. Marketing campaigns should emphasize channels and styles appealing to this segment [29].
2.  **Shipping Optimization:** Average transaction values are higher for express shipping than standard shipping [21, 22]. The business should heavily promote express delivery options or bundle free express shipping with higher cart thresholds [21, 22].
3.  **Subscription Opportunity:** While there is a substantial base of loyal repeat buyers, a significant portion of these high-value repeat buyers remain unsubscribed [28, 29]. Redesigning the subscription offer to include exclusive benefits can capture this latent group [28].

---

## 🚀 How to Run this Project

### Prerequisites
Ensure you have the following installed on your machine:
*   Python 3.12+ (Pandas, SQL Alchemy, `psycopg2`) [7, 15, 16]
*   PostgreSQL / PGAdmin (or MySQL / MS SQL Server) [15, 17]
*   Power BI Desktop [30]

### Running the Workflow
1.  **Run Jupyter Notebook:** Open the Python cleaning script, adjust the CSV file path, and execute to perform data transformation and load the cleaned dataset directly into your PostgreSQL database [7, 15, 16].
2.  **Execute SQL Queries:** Open the provided `.sql` file in PGAdmin and execute queries to analyze the `customer` table [17].
3.  **Open Power BI Dashboard:** Load the `.pbix` template, enter your local server credentials, and explore the interactive visuals [30, 41].

---

### Author :

Ankur Mishra

Presentated to - Novexa Technologies
