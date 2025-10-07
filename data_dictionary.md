# 📘 Data Dictionary — Online Store Database

This **Data Dictionary** describes the structure of the **Online_Store** database, detailing each table, its columns, data types, and purpose.  
The database consists of **three main tables** — `customers`, `products`, and `orders` — with defined relationships that ensure referential integrity and support business operations.

---

## 🧍‍♂️ Table 1: `customers`

Stores essential customer information used for transactions and communication.

| Column Name | Data Type | Constraints | Description |
|--------------|------------|--------------|--------------|
| `customer_id` | SERIAL | PRIMARY KEY | Unique identifier for each customer |
| `name` | TEXT | NOT NULL | Full name of the customer |
| `email` | TEXT | UNIQUE, NOT NULL | Customer email address (used for login/communication) |
| `phone` | TEXT | NULL | Customer contact phone number |
| `created_at` | TIMESTAMP | DEFAULT NOW() | Timestamp when the customer was added |

**Purpose:**  
Holds unique customer data. Serves as the parent table for orders placed in the system.  

**Relationships:**  
Referenced by `orders.customer_id` (One-to-Many relationship).

---

## 📦 Table 2: `products`

Contains product catalog information including pricing and stock quantity.

| Column Name | Data Type | Constraints | Description |
|--------------|------------|--------------|--------------|
| `product_id` | SERIAL | PRIMARY KEY | Unique identifier for each product |
| `name` | TEXT | NOT NULL | Product name |
| `category` | TEXT | NOT NULL | Product category (e.g., Electronics, Furniture, Appliances) |
| `price` | DECIMAL(10,2) | NOT NULL | Price per unit of the product |
| `stock_quantity` | INT | NOT NULL | Current quantity in stock |

**Purpose:**  
Stores all available products in the online store. Used to manage stock levels and pricing.  

**Relationships:**  
Referenced by `orders.product_id` (One-to-Many relationship).

---

## 🧾 Table 3: `orders`

Links customers to the products they purchase. Each record represents a single order transaction.

| Column Name | Data Type | Constraints | Description |
|--------------|------------|--------------|--------------|
| `order_id` | SERIAL | PRIMARY KEY | Unique identifier for each order |
| `customer_id` | INT | FOREIGN KEY → customers(customer_id) | ID of the customer placing the order |
| `product_id` | INT | FOREIGN KEY → products(product_id) | ID of the product purchased |
| `order_date` | TIMESTAMP | DEFAULT NOW() | Date and time when the order was made |
| `quantity` | INT | NOT NULL, CHECK (quantity > 0) | Number of items ordered |
| `total_price` | DECIMAL(10,2) | NOT NULL | Total cost of the order (product price × quantity) |

**Purpose:**  
Acts as a linking table that records transactions and connects customers to purchased products.  

**Relationships:**  
- `customer_id` → references `customers(customer_id)`  
- `product_id` → references `products(product_id)`  
(Both form **foreign key** relationships.)

---

## 🧠 Relationships Summary

| Relationship | Type | Description |
|---------------|------|--------------|
| `customers` → `orders` | One-to-Many | A customer can have multiple orders |
| `products` → `orders` | One-to-Many | A product can appear in multiple orders |
| `orders` | Junction | Connects customers and products |

---

