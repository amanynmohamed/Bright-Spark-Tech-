# Bookstore Database Project - README

## Project Overview

In this project, our goal is to create a relational database for a bookstore using MySQL. The database will store information about books, authors, customers, orders, shipping, and more. The project is split into different tasks, with each team member taking responsibility for specific parts of the project. Below are the steps and responsibilities for each member.

---

## Project Tasks Breakdown

### Step 1: Database Creation
*Amany Nabil* will be responsible for creating the database. This includes setting up the MySQL database for the bookstore, defining the necessary tables, and ensuring that the database structure meets the project requirements.

### Step 2: Table Creation
*Amany Nabil* will also handle the creation of the tables within the MySQL database. This includes defining the schema and data types for each table according to the project’s requirements.

### Step 3: ERD Design (Entity Relationship Diagram)
*Neo Mokoele* will create the Entity Relationship Diagram (ERD) using Draw.io. The ERD will visually represent the relationships between all the tables in the database, ensuring clarity and alignment with the MySQL design.

### Step 4: Relationship Verification
*Neo Mokoele* will verify the relationships between the tables, making sure that the connections in the ERD are accurate and reflect the actual relationships in the MySQL schema.

### Step 5: SQL Queries
*Nomakha Dlomo* will write the SQL queries needed to manipulate and populate the data in the tables. This will include inserting sample data and ensuring that queries return the correct results.

### Step 6: GitHub Upload
*Amany Nabil* will upload the completed project files (including the MySQL scripts, ERD, and SQL queries) to GitHub. This will ensure the project is accessible and can be easily shared with others.

---

## Expected Outcomes

By the end of this project, we will have:

- A fully functional MySQL database to manage the bookstore's data.
- An accurate ERD representing the relationships between all tables.
- A set of SQL queries that populate and manipulate the data effectively.
- The entire project uploaded to GitHub for easy access and sharing.

---

## Tools and Technologies Used

- *MySQL*: For creating and managing the database.
- *Draw.io*: For designing the ERD.
- *GitHub*: For storing and sharing the project files.


-- Country Table
CREATE TABLE country (
    country_id INT PRIMARY KEY,
    country_name VARCHAR(100)
);

-- Address Table
CREATE TABLE address (
    address_id INT PRIMARY KEY,
    street VARCHAR(255),
    city VARCHAR(100),
    postal_code VARCHAR(20),
    country_id INT,
    FOREIGN KEY (country_id) REFERENCES country(country_id)
);

-- Customer Table
CREATE TABLE customer (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    email VARCHAR(100),
    phone_number VARCHAR(20)
);

-- Address Status Table
CREATE TABLE address_status (
    address_status_id INT PRIMARY KEY,
    status_description VARCHAR(100)
);

-- Customer Address Table (Many-to-many: Customer - Address)
CREATE TABLE customer_address (
    customer_address_id INT PRIMARY KEY,
    customer_id INT,
    address_id INT,
    address_status_id INT,
    FOREIGN KEY (customer_id) REFERENCES customer(customer_id),
    FOREIGN KEY (address_id) REFERENCES address(address_id),
    FOREIGN KEY (address_status_id) REFERENCES address_status(address_status_id)
);

-- Author Table
CREATE TABLE author (
    author_id INT PRIMARY KEY,
    author_name VARCHAR(100)
);

-- Publisher Table
CREATE TABLE publisher (
    publisher_id INT PRIMARY KEY,
    publisher_name VARCHAR(100)
);

-- Book Language Table
CREATE TABLE book_language (
    language_id INT PRIMARY KEY,
    language_name VARCHAR(50)
);

-- Book Table
CREATE TABLE book (
    book_id INT PRIMARY KEY,
    title VARCHAR(255),
    publisher_id INT,
    language_id INT,
    FOREIGN KEY (publisher_id) REFERENCES publisher(publisher_id),
    FOREIGN KEY (language_id) REFERENCES book_language(language_id)
);

-- Book Author Table (Many-to-many: Book - Author)
CREATE TABLE book_author (
    book_author_id INT PRIMARY KEY,
    book_id INT,
    author_id INT,
    FOREIGN KEY (book_id) REFERENCES book(book_id),
    FOREIGN KEY (author_id) REFERENCES author(author_id)
);

-- Order Status Table
CREATE TABLE order_status (
    order_status_id INT PRIMARY KEY,
    status_description VARCHAR(100)
);

-- Shipping Method Table
CREATE TABLE shipping_method (
    shipping_method_id INT PRIMARY KEY,
    method_name VARCHAR(100)
);

-- Customer Order Table
CREATE TABLE cust_order (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_status_id INT,
    shipping_method_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customer(customer_id),
    FOREIGN KEY (order_status_id) REFERENCES order_status(order_status_id),
    FOREIGN KEY (shipping_method_id) REFERENCES shipping_method(shipping_method_id)
);

-- Order Line Table (Many-to-many: Orders - Books)
CREATE TABLE order_line (
    order_line_id INT PRIMARY KEY,
    order_id INT,
    book_id INT,
    quantity INT,
    price DECIMAL(10, 2),
    FOREIGN KEY (order_id) REFERENCES cust_order(order_id),
    FOREIGN KEY (book_id) REFERENCES book(book_id)
);

-- Order History Table
CREATE TABLE order_history (
    history_id INT PRIMARY KEY,
    order_id INT,
    status_id INT,
    changed_on DATETIME,
    FOREIGN KEY (order_id) REFERENCES cust_order(order_id),
    FOREIGN KEY (status_id) REFERENCES order_status(order_status_id)
);
