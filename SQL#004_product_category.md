# SQL #004
## Power Users
Site: [[DataLemur](https://datalemur.com/)]\
Difficulty per Site: Medium

## Problem
A Microsoft Azure Supercloud customer is defined as a customer who has purchased at least one product from every product category listed in the products table. \
Write a query that identifies the customer IDs of these Supercloud customers.[[Full Description](https://datalemur.com/questions/supercloud-customer)]

## ✅ Submitted Solution
This solution is functionally correct and achieves the goal of counting users per message. 

```
WITH cust_categories AS (
  SELECT 
    cust.customer_id, 
    COUNT(DISTINCT prd.product_category) as count_categories
  FROM customer_contracts cust 
  INNER JOIN products prd 
    ON cust.product_id=prd.product_id
  GROUP BY cust.customer_id)

SELECT customer_id
FROM cust_categories
WHERE count_categories = (
  SELECT COUNT(DISTINCT product_category) FROM products
);
```
## 🚀 Advanced Solution
Removes unnecessary CTE unless reused elsewhere.
Uses HAVING instead of filtering a grouped subquery — cleaner and avoids subquery nesting.

```
SELECT 
  cust.customer_id
FROM 
  customer_contracts AS cust
JOIN 
  products AS prd
  ON cust.product_id = prd.product_id
GROUP BY 
  cust.customer_id
HAVING 
  COUNT(DISTINCT prd.product_category) = (
    SELECT COUNT(DISTINCT product_category) FROM products
  );

```
