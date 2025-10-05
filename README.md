# 📦 Online Store Database — Week 2 Documentation

## ✅ Project Overview

This project implements a simple **Online Store database** using **Supabase (PostgreSQL)**.  

The name of the schema is **Online_Store**.

The schema contains **3 main tables** with **sample data** and a **foreign key relationship**:  

- **customers** - Stores customer information.  
- **products** - Stores product details.  
- **orders** - Tracks purchases (linked to customers & products).  

The **orders** table acts as a joining table linking the `customers` and `products` tables. It contains foreign keys referencing both.

---

## 🎯 Project Purpose

The **Online Store Database** project was developed to demonstrate key database design and management concepts using **Supabase (PostgreSQL)**.  
Its main purpose is to model how an e-commerce platform manages **customers**, **products**, and **orders** in a structured, efficient, and relational way.

The database provides a foundation for:
- Storing and retrieving customer information securely.  
- Managing product listings, prices, and inventory levels.  
- Recording customer orders and linking them to purchased products.  
- Supporting business analytics such as total sales per product or per customer.  

This project showcases practical database design principles including **normalization**, **foreign key constraints**, and **referential integrity** while preparing the groundwork for future expansion into a full-stack e-commerce application.

---
## 🧩 Schema Overview

The **Online_Store** schema is designed to represent the core structure of a basic e-commerce system.  
It includes **three interrelated tables**; `customers`, `products`, and `orders`, each serving a distinct role in maintaining data consistency and enabling relational queries.

---

## 💡 Example Queries

Below are sample SQL queries tested in **Supabase SQL Editor** to demonstrate how the `Online_Store` database works.

---

### 🧍‍♂️ **1. List All Customers**

Retrieves all customer records from the `customers` table.

```sql
SELECT * FROM customers;
```
📘 This query displays all registered customers along with their contact details and registration date.

---

### 📦 **2. View Available Products**
Displays the list of all products and their current stock levels.

``` sql

SELECT name, category, price, stock_quantity
FROM products
ORDER BY category, name;
```
📘 This is useful for viewing the store’s catalog and inventory overview.

---

### 🧾 **3. View All Orders with Customer and Product Details**

The query fetches all orders joined with customer and product information.

```sql
SELECT 
    o.order_id,
    c.name AS customer_name,
    p.name AS product_name,
    o.quantity,
    o.total_price,
    o.order_date
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN products p ON o.product_id = p.product_id
ORDER BY o.order_date DESC;
```
📘 Displays complete transaction details with relational links.
---
### 💰 **4. Calculate Total Sales per Product**

The query shows how much revenue each product has generated based on all orders.

```sql

SELECT 
    p.name AS product_name,
    SUM(o.total_price) AS total_sales
FROM orders o
JOIN products p ON o.product_id = p.product_id
GROUP BY p.name
ORDER BY total_sales DESC;
```
📘 This helps in identifying top-performing products by total sales value.
--
### 👑 **5. Find the Top Customer by Total Spending**

This Determines which customer has spent the most money on orders.

``` sql

SELECT 
    c.name AS customer_name,
    SUM(o.total_price) AS total_spent
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
GROUP BY c.name
ORDER BY total_spent DESC
LIMIT 1;
```
