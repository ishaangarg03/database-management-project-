Here’s an improved version of your **Database Management Guide** with better structure, enhanced readability, and additional details for clarity.

---

# **Database Management Guide**

This guide outlines how to set up and manage a database for your project. It covers creating tables, inserting data, deleting records, and utilizing SQL queries efficiently. The database schema includes tables for users, categories, products, orders, and order items. Follow these steps to streamline your database operations.

## **Table of Contents**

- [Creating Tables](#creating-tables)
- [Understanding Primary Keys](#primary-keys)
- [Inserting Data (INSERT)](#adding-data-insert)
- [Deleting Data (DELETE)](#deleting-data-delete)
- [Executing SQL Queries](#using-the-queries)
- [Important Considerations](#important-notes)
- [Technologies Used](#technologies-used)

## **Creating Tables**

To initiate your database, create the necessary tables. Each table is defined with a unique primary key to maintain data integrity and establish clear relationships between different entities.

```sql
-- Create the 'users' table
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255) NOT NULL UNIQUE,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    first_name VARCHAR(255),
    last_name VARCHAR(255),
    address TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create the 'categories' table
CREATE TABLE categories (
    category_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(255) NOT NULL UNIQUE,
    description TEXT
);

-- Create the 'products' table
CREATE TABLE products (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(255) NOT NULL,
    description TEXT,
    price DECIMAL(10, 2) NOT NULL,
    image_url VARCHAR(255),
    category_id INT,
    stock_quantity INT DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES categories(category_id)
);

-- Create the 'orders' table
CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    total_amount DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);

-- Create the 'order_items' table
CREATE TABLE order_items (
    order_item_id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT NOT NULL,
    price_per_unit DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
```

---

## **Understanding Primary Keys**

Each table contains a **primary key**, which uniquely identifies each record, ensuring data consistency and proper relationships across tables.

| **Table**      | **Primary Key**    |
|----------------|--------------------|
| `users`        | `user_id`          |
| `categories`   | `category_id`       |
| `products`     | `product_id`        |
| `orders`       | `order_id`          |
| `order_items`  | `order_item_id`     |

---

## **Inserting Data (INSERT)**

To populate your tables with data, use **INSERT** statements. Here are some examples:

```sql
-- Add a new user:
INSERT INTO users (username, email, password, first_name, last_name, address) 
VALUES ('testuser', 'testuser@example.com', 'securepassword', 'Test', 'User', '123 Test St');

-- Add a new category:
INSERT INTO categories (category_name, description) 
VALUES ('New Category', 'Description of the new category');

-- Add a new product:
INSERT INTO products (product_name, description, price, image_url, category_id, stock_quantity) 
VALUES ('Awesome Product', 'This product is awesome!', 29.99, 'https://example.com/image.jpg', 1, 10);
-- Note: Replace 1 with the actual category_id of an existing category.

-- Add a new order:
INSERT INTO orders (user_id, total_amount) 
VALUES (1, 79.99); 
-- Replace 1 with the actual user_id of an existing user.

-- Add order items:
INSERT INTO order_items (order_id, product_id, quantity, price_per_unit) 
VALUES (1, 2, 2, 19.99), (1, 3, 1, 39.99);
-- Replace 1 with the actual order_id, and 2, 3 with actual product_id values.
```

---

## **Deleting Data (DELETE)**

**Caution:** When deleting data, always use the **WHERE** clause to prevent accidental loss of data. Double-check foreign key relationships before proceeding.

```sql
-- Delete a user:
DELETE FROM users WHERE user_id = 2;

-- Delete a category:
DELETE FROM categories WHERE category_id = 3;

-- Delete a product:
DELETE FROM products WHERE product_id = 1;

-- Delete an order:
DELETE FROM orders WHERE order_id = 1;

-- Delete order items associated with an order:
DELETE FROM order_items WHERE order_id = 1;
```

---

## **Executing SQL Queries**

1. **Connect to your database**: Use tools like MySQL Workbench, phpMyAdmin, or any SQL client to connect to your database.
2. **Open a query editor**: Access the query editor in your chosen database client.
3. **Paste and execute**: Copy the SQL queries from this guide (after updating placeholder values) and execute them to create tables or manipulate data.

---

## **Important Considerations**

- **Replace placeholders**: Always substitute example values (e.g., `category_id`, `user_id`, `product_id`) with actual values from your database.
- **Foreign Key Constraints**: When deleting records, ensure you remove dependent records first to avoid foreign key constraint violations.
- **Backup your data**: Before running any **DELETE** operations, make sure you have a full backup of your database.

---

## **Technologies Used**

- **SQL**: Structured Query Language (SQL) for managing and interacting with databases.
- **SQL Dialect**: The examples provided are compatible with SQL-based database systems such as **MySQL** and **MariaDB**.

---

This guide helps you manage your database with a focus on ensuring data integrity, simplifying operations, and handling data efficiently.
