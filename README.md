# Monday Coffee – Sales & Market Analysis Using PostgreSQL

## Project Overview

This project focuses on analyzing Monday Coffee's sales performance across different cities using PostgreSQL. The objective is to uncover meaningful business insights related to customer purchasing behavior, product performance, city-wise revenue, monthly sales growth, and market expansion opportunities.

By analyzing data from multiple relational tables, including **City, Customers, Products, and Sales**, this project aims to identify high-performing markets, understand customer preferences, evaluate business performance, and provide data-driven recommendations for expanding Monday Coffee's business.

The analysis follows a business-oriented approach, transforming raw transactional data into actionable insights that can support strategic decision-making.

## Business Objectives

- Estimate the potential coffee consumer population across different cities.
- Analyze total revenue generated from coffee sales.
- Identify the best-selling coffee products.
- Evaluate average sales per customer across cities.
- Understand customer distribution and purchasing behavior.
- Identify the top-performing products in each city.
- Compare average sales per customer with estimated city rental costs.
- Analyze monthly sales growth and revenue trends.
- Identify cities with the highest market potential for business expansion.
- Provide data-driven recommendations for selecting potential business locations.

## Tools & Technologies

| Technology | Purpose |
|---|---|
| PostgreSQL | Database management and analysis |
| SQL | Data querying and business analysis |
| pgAdmin 4 | Database exploration and query execution |
| Common Table Expressions (CTEs) | Organizing complex analytical queries |
| Window Functions | Ranking products and calculating monthly growth |
| Aggregate Functions | Revenue, customer, and sales calculations |

## Database Schema

The project uses four relational tables to perform comprehensive business analysis.

| Table | Description |
|---|---|
| city | Contains city information, population, estimated rent, and city ranking |
| customers | Contains customer details and their associated city IDs |
| products | Contains coffee product details and product IDs |
| sales | Contains transactional information, product IDs, customer IDs, sale dates, and total sales amounts |

### Table Relationships

The analysis combines these four tables using their respective primary and foreign key relationships.

- `city.city_id` → `customers.city_id`
- `customers.customer_id` → `sales.customer_id`
- `products.product_id` → `sales.product_id`

These relationships enable city-level, customer-level, and product-level sales analysis.

## Project Workflow

### Step 1: Database Exploration

Started by exploring the four available tables to understand the database structure and the information available for analysis.

**Activities performed:**

- Retrieved all records from the City table.
- Explored customer information.
- Examined available coffee products.
- Inspected sales transaction records.
- Understood relationships between tables.
- Identified relevant columns required for business analysis.

### Step 2: Business Analysis Using SQL

Developed SQL queries to solve practical business problems and extract meaningful insights from the dataset.

#### Business Questions & Analytical Approach

**1. Coffee Consumer Estimation by City**

**Business Question:** How many people in each city are estimated to consume coffee, assuming that 25% of the population consumes coffee?

**Approach:**
- Calculated 25% of the population for each city.
- Converted estimated consumer counts into millions.
- Ranked cities based on their estimated coffee consumer population.

**SQL Concepts:** Arithmetic operations, ROUND(), ORDER BY.

**2. Total Revenue from Coffee Sales**

**Business Question:** What is the total revenue generated from coffee sales across all cities during the last quarter of 2023?

**Approach:**
- Joined Sales, Customers, and City tables.
- Filtered transactions from October to December 2023.
- Calculated total revenue for each city.
- Ranked cities based on revenue generated.

**SQL Concepts:** INNER JOIN, SUM(), EXTRACT(), GROUP BY, ORDER BY.

**3. Sales Count for Each Product**

**Business Question:** How many units of each coffee product have been sold?

**Approach:**
- Joined Products and Sales tables.
- Used LEFT JOIN to retain products even when no sales transactions exist.
- Counted sales transactions for each product.
- Identified products with the highest transaction counts.

**SQL Concepts:** LEFT JOIN, COUNT(), GROUP BY.

**4. Average Sales Amount per Customer by City**

**Business Question:** What is the average sales amount per customer in each city?

**Approach:**
- Combined sales, customer, and city information.
- Calculated total revenue for each city.
- Counted unique customers.
- Divided total revenue by the number of unique customers.

**SQL Concepts:** INNER JOIN, SUM(), COUNT(DISTINCT), ROUND().

**5. City Population and Estimated Coffee Consumers**

**Business Question:** What are the total current customers and estimated coffee consumers in each city?

**Approach:**
- Created a CTE to calculate estimated coffee consumers.
- Created another CTE to calculate unique purchasing customers.
- Combined both datasets to compare estimated market size with the existing customer base.

**SQL Concepts:** CTEs, COUNT(DISTINCT), ROUND(), INNER JOIN.

**6. Top-Selling Products by City**

**Business Question:** What are the top three best-selling coffee products in each city based on sales volume?

**Approach:**
- Joined Sales, Products, Customers, and City tables.
- Counted product transactions for each city.
- Applied DENSE_RANK() to rank products within each city.
- Retrieved the top three products for every city.

**SQL Concepts:** Multiple JOINs, COUNT(), GROUP BY, DENSE_RANK(), PARTITION BY.

**7. Customer Segmentation by City**

**Business Question:** How many unique customers in each city have purchased coffee products?

**Approach:**
- Combined City, Customers, and Sales tables.
- Filtered transactions based on the available coffee product IDs.
- Counted distinct customers in each city.

**SQL Concepts:** LEFT JOIN, INNER JOIN, WHERE, IN, COUNT(DISTINCT).

**8. Average Sales vs. Rental Cost Analysis**

**Business Question:** How does average sales per customer compare with the estimated rental cost in each city?

**Approach:**
- Calculated total revenue and unique customers for each city.
- Determined average sales per customer.
- Retrieved estimated rental costs from the City table.
- Calculated average rental cost per existing customer.
- Compared sales performance with rental expenses to evaluate business opportunities.

**SQL Concepts:** CTEs, JOINs, SUM(), COUNT(DISTINCT), ROUND(), arithmetic operations.

**9. Monthly Sales Growth Analysis**

**Business Question:** What is the monthly sales growth or decline across different cities?

**Approach:**
- Extracted month and year from transaction dates.
- Calculated total monthly revenue for each city.
- Used the LAG() window function to retrieve the previous month's revenue.
- Calculated monthly sales growth percentages.
- Identified revenue growth and declining trends across cities.

**SQL Concepts:** CTEs, EXTRACT(), SUM(), LAG(), PARTITION BY, ORDER BY, ROUND().

**Sales Growth Formula:**

Monthly Growth (%) =

(Current Month Sales - Previous Month Sales) / Previous Month Sales × 100

**10. Market Potential Analysis**

**Business Question:** Which three cities offer the highest market potential for expanding Monday Coffee's business?

**Approach:**
- Calculated total revenue generated by each city.
- Identified the number of unique customers.
- Calculated average sales per customer.
- Retrieved estimated rental costs.
- Estimated coffee consumers based on 25% of the population.
- Calculated average rent per existing customer.
- Compared these business metrics to identify promising expansion locations.

**SQL Concepts:** Multiple CTEs, INNER JOIN, SUM(), COUNT(DISTINCT), ROUND(), arithmetic operations.

## SQL Concepts Applied

This project demonstrates practical implementation of the following PostgreSQL concepts:

- **Data Retrieval:** SELECT, DISTINCT
- **Joins:** INNER JOIN, LEFT JOIN
- **Aggregate Functions:** COUNT(), SUM(), AVG()
- **Grouping & Sorting:** GROUP BY, ORDER BY
- **Date & Time Functions:** EXTRACT()
- **Common Table Expressions:** WITH clause (CTEs)
- **Window Functions:** RANK(), DENSE_RANK(), LAG()
- **Window Partitioning:** PARTITION BY
- **Filtering:** WHERE, IN
- **Type Casting:** ::NUMERIC
- **Numeric Functions:** ROUND()
- **Business Calculations:** Revenue, average sales, market estimation, monthly growth percentages

## Key Business Insights & Recommendations

Based on the market potential analysis, the following three cities were identified as promising expansion opportunities.

### 1. Pune

**Business Highlights:**
- Generated the highest total revenue among the analyzed cities.
- Has a comparatively low average rental cost per existing customer.
- Demonstrates strong average sales per customer.

**Recommendation:**

Pune is a promising location for expansion due to its strong revenue performance, healthy customer spending, and comparatively lower rental cost per customer.

### 2. Delhi

**Business Highlights:**
- Has the highest estimated coffee consumer population at approximately 7.7 million.
- Has a substantial existing customer base of 68 customers.
- Average rent per customer is approximately 330, which remains below 500.

**Recommendation:**

Delhi offers significant market potential due to its large estimated coffee-consuming population and established customer base. Expansion could help capture a larger share of the available market.

### 3. Jaipur

**Business Highlights:**
- Has an existing customer base of approximately 69 customers.
- Average rent per customer is relatively low at approximately 156.
- Average sales per customer is approximately 11.6K.

**Recommendation:**

Jaipur presents an attractive expansion opportunity because of its relatively low rental cost per customer, strong existing customer base, and promising average sales performance.

### Overall Business Recommendation

Based on the analyzed metrics, Pune, Delhi, and Jaipur are promising candidates for Monday Coffee's expansion strategy.

- **Pune:** Prioritize revenue performance and customer spending.
- **Delhi:** Focus on capturing the large potential coffee consumer market.
- **Jaipur:** Explore cost-efficient expansion with a strong existing customer base.

These recommendations are based on the available sales, population, and rental data. Further evaluation of competition, operating costs, location suitability, and profitability would help validate the final expansion decisions.

## Key Performance Metrics Analyzed

| Business Metric | Analytical Purpose |
|---|---|
| Estimated Coffee Consumers | Measures potential market size |
| Total Revenue | Evaluates city-wise sales performance |
| Product Sales Count | Identifies popular products |
| Unique Customers | Measures customer reach |
| Average Sales per Customer | Evaluates customer spending |
| Estimated Rent per Customer | Compares rental cost with customer base |
| Monthly Sales Growth | Tracks revenue trends |
| Product Ranking by City | Identifies city-specific product preferences |
| Revenue by City | Identifies high-performing markets |

## Key Learnings

- Gained practical experience in analyzing relational databases using PostgreSQL.
- Improved understanding of multi-table joins and database relationships.
- Learned to translate business requirements into SQL queries.
- Applied CTEs to organize complex analytical queries.
- Used window functions to perform product ranking and monthly sales comparisons.
- Developed an understanding of customer segmentation and purchasing behavior.
- Performed revenue, sales growth, and market potential analysis.
- Learned how SQL-driven insights can support business expansion and strategic decisions.

## Project Structure

```text
Monday-Coffee-Sales-Analysis/
│
├── Monday_Coffee_SQL_Queries.sql
├── README.md
└── Dataset/
    ├── city.csv
    ├── customers.csv
    ├── products.csv
    └── sales.csv
```

*Update the filenames and folder structure according to the actual files in your GitHub repository.*

## How to Run This Project

**Prerequisites:**
- PostgreSQL
- pgAdmin 4
- Monday Coffee dataset

**Execution Steps:**

1. Clone the GitHub repository:

   ```bash
   git clone <your-github-repository-url>
   ```

2. Create a PostgreSQL database:

   ```sql
   CREATE DATABASE monday_coffee;
   ```

3. Connect to the newly created database using pgAdmin 4.

4. Import the four dataset files into PostgreSQL:
   - city
   - customers
   - products
   - sales

5. Verify the imported data:

   ```sql
   SELECT * FROM city;
   SELECT * FROM customers;
   SELECT * FROM products;
   SELECT * FROM sales;
   ```

6. Open `Monday_Coffee_SQL_Queries.sql`.

7. Execute the queries to explore the business questions and analyze the results.

## Conclusion

This project demonstrates how PostgreSQL can be used to transform raw transactional data into meaningful business insights.

By analyzing city demographics, customer purchasing behavior, product performance, revenue trends, and estimated rental costs, I developed a data-driven approach to identifying potential markets for Monday Coffee's business expansion.

The project strengthened my practical SQL skills and provided hands-on experience in solving real-world business problems through data analysis and analytical thinking.

---

**Author:** Dhanush Kumar

**Project:** Monday Coffee – Sales & Market Analysis

**Domain:** Data Analytics | Business Analysis

**Technologies:** PostgreSQL | SQL | pgAdmin 4
