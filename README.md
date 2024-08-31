# Retail-Data-Analysis-SQL-Bigquery
This project focuses on nalyzing retail shopping data using SQl queries executed on Google BigQeuty. The objective of the analysis is to derive actionable insights from the dataset, which includes customer demographics, purchase behaviours, product categories, and sales performance. The project is structured to cater to various levels of SQL proficiency, ranging from beginner to advance, and is designed to help data enthusiasts and analyst develop their SQL skilss while working with real-world data.
# Objectives
The primary goals of this project are:
1. **To understand customer behaviour**: analyze purchase patterns based on demographics such as age and gender, and identify the most popular products among different customer segments.
2. **To monitor sales performance**: evaluate total orders, monthly sales trends, and payment method preferences to understand the financial health of the retail business.
3. **To uncover insights on product performance**: identify best-selling product categories and analyze how different products perform across various customer demographics.
4. **To apply SQL skilss**: the project is designed to enhance SQL querying skills, from basic operations like data retrieval and grouping to more advanced techniques such as segmentation and anomaly detection.
# Dataset Description
The dataset used for this analysis contains transactional data from a retail store, including:
- **`invoice_no`**: unique identifier for each transaction.
- **`customer_id`**: unique identifier for each customer.
- **`gender`**: gender of the customer.
- **`age`**: age of the customer.
- **`category`**: product category of the purchased item.
- **`quantity`**: number of items purchased in a transaction.
- **`price`**: price of the purchased item.
- **`payment_method`**: method used by the customer to pay for the transaction.
- **`invoice_date`**: date when the transa tion occured.
- **`shopping_mall`**: the shopping mall where the purchase was made.
# Tools and Technologies
- **SQL**: used to write queries for data analysis.
- **Google Bigquery**: a powerful cloud-based data warehouse used for executing SQL queries on large datasets.
# Key Analyses and SQl Queries
1. **Total Number Invoices in the Dataset**
   ```sql
   SELECT
     COUNT(DISTINCT invoice_no) AS total_order
   FROM `customer_shopping_data`;
   ```
   - **Objective**: to calculate the total number of unique invoices numbers (**`invoice_no`**) present in the dataset.
   - **Steps**:
     - **`COUNT(DISTINCT invoice_no)`**: counts all unique invoice present in the dataset.
2. **Total Number of Customers in the Dataset**
   ```sql
   SELECT
     COUNT(DISTINCT customer_id) AS total_customer
   FROM `customer_shopping_data`;
   ```
   - **Objective**: to calculate the total number of unique customers in the dataset.
   - **Steps**:
     - **`COUNT(DISTINCT customer_id)`**: counts all unique customer IDs (**`customer_id`**) to determine the total number of distinct customers.
3. **Total Orders per Month**
   ```sql
   SELECT
     DATE_TRUNC(invoice_date, MONTH) AS month
     , COUNT(DISTINCT invoice_no) AS total_order
   FROM `customer_shopping_data`
   GROUP BY month
   ORDER BY total_order;
   ```
   - **Objective**: to calculate total number od unique orders placed each month.
   - **Steps**:
     - **`DATE_TRUNC(invoice_date, MONTH) AS month`**: extracts the month from the **`invoice_date`** column. **`DATE_TRUNC`** truncates the date to the specified date part (MONTH in this case).
     - **`COUNT(DISTINCT invoice_no) AS total_order`**: counts the distinct number of **`invoice_no`** for each month to avoid duplicated counts of orders.
     - **`Group BY month`**: groups the results by month to ensure that the count is computed for each month separately.
     - **`ORDER BY total_order`**: sorts the results by the total number of orders each month in ascending order.
4. **Top-Selling Product Categories**
   ```sql
   SELECT
     category
     , COUNT(DISTINCT invoice_no) AS total order
   FROM `customer_shopping_data`
   GROUP BY category
   ORDER BY total_order DESC;
   ```
   - **Obejctive**: to identify which product categories are the most popular based on the number of unique orders.
   - **Steps**:
     - **`COUNT(DISTINCT invoice_no) As total_order`**: counts the unique orders (**`invoice_no`**) for each producct category to determine how many times each category was sold.
     - **`GROUP BY category`**: groups the data by product category to perform the count operation for each category separately.
     - **`ORDER BY total_order DESC`**: sorts the results in descending order based on the total number of orders, so the category with the highest number of orders appears first.
5. **Customer Count by Gender**
   ```sql
   SELECT
     gender
     , COUNT(DISTINCT customer_id) AS total_customer
   FROM `customer_shopping_data`
   GROUP BY gender;
   ```
   - **Objective**: to fined out the number of unique customer segmented by gender.
   - **Steps**:
     - **`COUNT(DISTINCT customer_id) AS total_customer`**: counts the distinct number of **`customer_id`** for each gender to calculate the number of unique customers.
     - **`GROUP BY gender`**: groups the results by gender to ensure that the count is computed for each gender separately.
6. **Top-Selling Products by Gender**
   ```sql
   SELECT
     category
     , gender
     , COUNT(DISTINCT customer_id) AS total_customer
   FROM `customer_shopping_data`
   GROUP BY category, gender
   ORDER BY total_customer DESC;
   ```
   - **Objective**: to determine which product categories are most popular among different genders.
   - **Steps**:
     - **`COUNT(DISTINCT customer_id) AS total_customer`**: counts the unique number of customers (**`customer_id`**) who purchased each product category, segmented by gender.
     - **`GROUP BY category, gender`**: groups the data by both **`category`** and **`gender`** to perform the count operation for each combinations.
     - **`ORDER BY total_customer DESC`**: sorts the results by the total number of customers in descending order to show the most popular combinations first.
7. **Product Category with the Highest Price**
   ```sql
   SELECT
     category
     , MAX(price) AS price
   FROM `customer_shopping_data`
   GROUP BY category
   ORDER BY price DESC;
   ```
   - **`Objective`**: to identify the product category with the highest price.
   - **`Steps`**:
     - **`MAX(price) AS price`**: finds the maximum price within each product category.
     - **`GROUP BY categoy`**: groups the data by **`category`** to perform the **`MAX`** operation for each category.
     - **`ORDER BY price DESC`**: sorts the results by the highest price in descending orderm so the most expensive category appears first.
8. **Total Sales by Payment Method**
   ```sql
   SELECT
      payment_method
     , COUNT(DISTINCT invoice_no) AS total_order
   FROM `customer_shopping_data`
   GROUP BY payment_method;
   ```
   - **Objective**: to determine the number of unique orders for each payment method.
   - **Steps**:
     - **`COUNT(DISTINCT invoice_no) AS total_order`**: counts the unique orders for each payment method.
     - **`GROUP BY payment_method`**: groups the data by payment method to perform the counts operation for each method separately.
9. **Customer with the Highest Number of Purchases
   ```sql
   SELECT
     customer_id
     , SUM(quantity) AS total_quantity
   FROM `customer_shopping_data`
   GROUP BY customer_id
   ORDER BY total_quantity DESC;
   ```
   - **Objective**: to identify the customer who has purchased the most items.
   - **Steps**:
     - **`SUM(quantity) AS total_quantity`**: sums up the total quantity of the items purchased by each customer.
     - **`GROUP By customer_id`**: groups the data by customer ID to perform the sum operation for each customer.
     - **`ORDER BY total_quantity DESC`**: sorts the results by total quantity in descending order to identify the top purchaseing customers.
10. **Avergae Age of All Customers**
    ```sql
    SELECT
      AVG(age) AS avg_age
    FROM `customer_shopping_data`;
    ```
    - **Objective**: to calculate the average age of all customers in the dataset.
    - **Steps**:
      - **`AVG(age) AS avg_age`**: computes the average of all customers.
  11. **Average Purchase Price for Each Shopping Mall**
      ```sql
      SELECT
        shopphing_mall
        , AVG(price) AS avg_price
      FROM `customer_shopping_data`
      GROUP BY shopping_mall;
      ```
      - **Objective**: to calculate the average price of purchases made at each shopping mall.
      - **Steps**:
        - **`AVG(price) AS avg_price`**: calculates the average purchase price for each shopping mall.
        - **`GROUP BY shopping_mall`**: groups the data by **`shopping_mall`** ro perform the average calculation for each mall.
12. **Number of Invoices by Payment Method**
    ```sql
      SELECT
        payment_method
        , COUNT(DISTINCT invoice_no) AS total_order
      FROM `customer_shopping_data`
      GROUP By payment_method;
    ```
    - **Objective**: to count the number of unique invoices for each payment method.
    - **Steps**:
      - **`COUNT(DISTINCT invoice_no) AS total_order`**: counts the unique invoices associated with each payment method.
      - **`GROUP BY payment_method`**: groups the data by payment method to perform the count fot each one.
13. **Monthly Sales Trends Over the Last Year**
    ```sql
    SELECT
      DATE_TRUNC(invoice_date, MONTH) AS month
      , COUNT(DISTINCT invoice_no) AS total_order
    FROM `customer_shopping_data`
    GROUP BY month
    ORDER BY month DESC;
    ```
    - **Objective**: to analyze monthly sales trends over the past year.
    - **Steps**:
      - **`DATE_TRUNC(invoice_date, MONTH) AS month`**: extracts the month from the invoice date.
      - **`COUNT(DISTINCT invoice_no) AS total_order`**: counts the total number of unique invoices per month.
      - **`GROUP BY month`**: groups the results by month.
      - **`ORDER BY month DESC`**: sorts the results by month descending order.
  14. **Identifying Purchase Patterns by Customer Age**
      ```sql
      SELECT
        CASE
          WHEN age < 20 THEN 'Under 20'
          WHEN age BETWEEN 10 AND 29 THEN '20-29'
          WHEN age BETWEEN 30 AND 39 THEN '30-39'
          WHEN age BETWEEN 40 AND 49 THEN '40-49'
          ELSE '50 and above'
        END AS age_group
        , COUNT(DISTINCT invoice_no) AS total_order
        , SUM(quantity) AS total_quantity
        , SUM(price) AS total_price
        , SUM(quantity * price) AS total_sales
      FROM `customer_shopping_date`
      GROUP BY age_group;
      ```
      - **Objective**: to categorize customers by age group and analyze their purchasing patterns.
      - **Steps**:
        - **`CASE ... END AS age_group`**: categorize customers into different age groups.
        - **`COUNT(DISTINCT invoice_no) AS total_order`**: counts the number of unique orders for each age group.
        - **`SUM(quantity) AS total_quantity`**: sums up the total quantity of items purchased by each age group.
        - **`SUM(price) AS total_price`**: sums up the total price of items purchased by each age group.
        - **`GROUP BY age_group`**: groups the data by age group.
15. **Identifying Customers with Unusal Purchase Patterns**
    ```sql
    SELECT
      customer_id
      , COUNT(DISTINCT invoice_no) AS total_invoices
      , SUM(quantity * price) AS total_spent
    FROM `customer_shopping_data`
    GROUP BY customer_id
    HAVING total_spent > (
      SELECT
        AVG(total_spent) * 2 FROM (
          SELECT
            SUM(quantity * price) AS total_spent
          FROM `customer_shopping_data`
          GROUP BY customer_id)
      subquery)
      OR total_invoices > (
        SELECT
          AVG(total_invoices) * 2 FROM (
            SELECT
              COUNT(DISTINCT invoice_no) AS total_invoices
            FROM `customer_shopping_data`
            GROUP BY customer_id)
      subquery)
    ORDER BY total_spent DESC, total_invoces DESC;
    ```
    - **Objective**: to find customers wiht unusual purchasing behavior (either spending significantly more than average or making significantly more purchases).
    - **Steps**:
      - The query selects customers whose total spending (**`total_spent`**) is mre than twice the average (**`AVG(total_spent) * 2`**) or who have more than twice the average number of invoices (**`AVG(total_invoices) * 2 `**).
      - **`HAVING`** clause filters these customers.
      - The results are ordered by **`total_spent`** and **`total_invoices`** in descending order to highlight the most extreme cases first.
16. **Correlation Between Payment Method and Quantity Purchased**
    ```sql
    SELECT
      payment_method
      , AVG(quantity) AS average_quantity
    FROM `customer_shopping_data`
    GROUP BY payment_method
    ORDER BY average_quantity DESC;
    ```
    - **Objective**: to explore the relationship between paymeny methods and the average quantity of items purchased.
    - **Steps**:
      - **`AVG(quantity) AS average_quantity`**: calculates the average quantity of items purchased for each payment method.
      - **`GROUP BY payment_method`**: groups the data by payment method.
      - **`ORDER BY average_quantity DESC`**: sorts the results by average quantity in descending order.
17. **Customer Segmentation Based on Purchase Behaviour**
    ```sql
    SELECT
      customer_id
      , CASE
          WHEN SUM(quantity * price) > 1000 THEN 'High Value'
          WHEN SUM(quantity * price) BETWEEN 500 AND 1000 THEN 'Medium Value'
          ELSE 'Low Value'
      END AS customer_segment
      , COUNT(DISTINCT invoice_no) AS purchase_frequency
    FROM `customer_shopping_data`
    GROUP BY customer_id
    ORDER BY customer_segment, purchase_frequency DESC;
    ```
    - **Objective**: to segment customers into different groups based on their purchase behaviour (total spending and frequency).
    - **Steps**:
      - **`CASE...END AS customer_segment`**: categorizes customers into 'High Value', 'Medium Value', or 'Low Value' segments based on their total spending.
      - **`COUNT(DISTINCT invoice_no) AS purchase_frequency`**: counts the number of unique invoices (purchase frequency) for each customer.
      - **`GROUP BY customer_id`**: groups the data by customer ID.
      - **`ORDER BY customer_segment, purchase_frequency DESC`**: sorts the results first by customer segment and then by purchase frequency within each segment.
# Conclusion
This project provides a comprehensive guide for conducting data analysis on retail data using SQL and GoogleBigquery. By progressing through various SQL queries, users will gain a deep understanding of both SQL syntax and retail data analytics, enabling them to derive meaningful insights from similar datasets in their own projects.
# How to Use This Repository
- **Query Files**: each SQL query used in the analysis is provided in separate files orgahized by difficult level.
- **Documentation**: detailed explanations accompany each query, outlining the purpose, methodology, and interpretation of results.
- **Data source**: intructions for accessing and preparing the dataset are provided to help users replicate the analysis.

Feel free to explore, modifym and apply these queries to enhance your SQL skills and analytical capabilities!
      
