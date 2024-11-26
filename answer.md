# SQL Challenge:

## Question

Suppose you have a database with three tables: "users", "orders", and "products". The "users" table contains columns id, name, and email. The "orders" table contains columns id, user_id, product_id, quantity, and created_at. The "products" table contains columns id, name, price, and category.

Write a single SQL query that returns a list of all users who have made at least 3 orders in the "Electronics" category and have spent more than $1000 on those orders, sorted by the total amount they have spent in descending order. The output should include the user's name, email, and the total amount they have spent on "Electronics" orders.

## Answer

```sql
SELECT users.name, users.email, SUM(products.price * orders.quantity) AS amount_spent FROM users
JOIN orders ON users.id = orders.user_id
JOIN products ON products.id = orders.product_id
WHERE products.category = 'Electronics'
GROUP BY users.name, users.email
HAVING COUNT(orders.user_id) >= 3 AND SUM(products.price * orders.quantity) > 1000
ORDER BY amount_spent DESC
```