# 📦 Online Store Database — Week 1 Deliverables

## ✅ Overview

This project implements a simple **Online Store database** using **Supabase (PostgreSQL)**. 

The name of the schema is **Online_Store**

The schema contains **3 main tables** with **sample data** and a **foreign key relationship**:  

- **customers** → Stores customer information.  
- **products** → Stores product details.  
- **orders** → Tracks purchases (linked to customers & products).
  
The **orders** table acts as a joining table linking customers and products tables. It has both foreign keys from costomers and products tables

---
## ✅ Steps in Supabase

### Step 1 - Created a Project Called Online_Store

<img width="1600" height="860" alt="image" src="https://github.com/user-attachments/assets/32ba9d26-abbf-44a6-ae4a-32a7f5f9c0ea" />

---

### Step 2 - Created three tables
<img width="1600" height="600" alt="image" src="https://github.com/user-attachments/assets/a5b8b238-ff26-4a80-aa52-a807f3debfe2" />

### Step 3 - Inserted at least 5 rows per table.
<img width="1600" height="600" alt="image" src="https://github.com/user-attachments/assets/ca0b7e4c-243b-4698-b5c4-16dd6081d389" />

### Step 4 - Test queries in Supabase SQL editor.

*`List all customers`*

<img width="1600" height="600" alt="image" src="https://github.com/user-attachments/assets/a7671f23-f617-43e6-a618-79f25d8c8da1" />

*`List all Products`*

<img width="1600" height="600" alt="image" src="https://github.com/user-attachments/assets/1b73b530-1017-422a-b915-6624b4a0e37f" />

*`List all orders`*

<img width="1600" height="600" alt="image" src="https://github.com/user-attachments/assets/36bb052d-afec-49a8-b062-3b94e483e965" />


## 🗂 Database Schema (`Online_Store.sql`)

### ``Creating Tables``

#### `TABLE: customers`

```sql
CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE NOT NULL,
    phone TEXT,
    created_at TIMESTAMP DEFAULT NOW()
);
```
---
#### `TABLE: products`
```sql
CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    category TEXT NOT NULL,
    price DECIMAL(10,2) NOT NULL,
    stock_quantity INT NOT NULL
);
```
---
#### `TABLE: orders`
``` sql
CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(customer_id) ON DELETE CASCADE,
    product_id INT REFERENCES products(product_id),
    order_date TIMESTAMP DEFAULT NOW(),
    quantity INT NOT NULL CHECK (quantity > 0),
    total_price DECIMAL(10,2) NOT NULL
);
```
---
### `Inserting Sample Data`

#### customers table
```sql
INSERT INTO customers (name, email, phone) VALUES
('Godwin Waswa', 'waswa@gmail.com', '0177788772'),
('Alice Wanyonyi', 'wanyony@gmail.com', '0112382342'),
('Charles Kinyua', 'kcharles@gmail.com', '0712344455'),
('Diana Bett', 'diana@gmail.com', '0231234832'),
('Blessings Onyango', 'onyango@yahoo.com', '0823462710'),
('Charles Omondi', 'omondi@gmail.com', '03212334432');
```
---
#### products table
```sql
INSERT INTO products (name, category, price, stock_quantity) VALUES
('Laptop', 'Electronics', 89566.00, 5),
('Smartphone', 'Electronics', 34000.50, 20),
('Office Chair', 'Furniture', 13000.00, 65),
('Coffee Maker', 'Appliances', 5000.00, 30),
('Headphones', 'Accessories', 8000.00, 52),
('Television', 'Electronics', 50000.00, 52);
```
---

#### orders table
```sql
INSERT INTO orders (customer_id, product_id, quantity) VALUES
(1, 1, 1),
(2, 2, 2),
(3, 3, 1),
(4, 4, 3),
(5, 5, 2);
