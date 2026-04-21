![alt text](<../Screenshots/PhpMyAdmin_logo (1).png>)

# Lab: Basic Database Operations — Create, Populate, and Query a Database

**Estimated time:** 45 minutes

---

## Learning Objectives

After completing this lab you'll be able to use phpMyAdmin with MySQL to perform basic database operations. You'll also be able to demonstrate the skills needed to create, populate, and query a database using SQL commands.

| Objective                      | Description                                                       |
| :----------------------------- | :---------------------------------------------------------------- |
| **Create and populate**  | Create a database and table, then import data to populate it      |
| **Execute SQL commands** | Perform basic database operations using Structured Query Language |
| **Retrieve data**        | Use simple SELECT statements to retrieve data from tables         |
| **Filter data**          | Learn how to filter data output using WHERE statements            |
| **Add and remove data**  | Use INSERT and DELETE statements to modify table data             |
| **Remove tables**        | Use DROP statements to remove tables from a database              |

---

## Concepts Covered

### Basic SQL Commands

| Command                   | Purpose                           | Syntax Example                                                    |
| :------------------------ | :-------------------------------- | :---------------------------------------------------------------- |
| **CREATE DATABASE** | Creates a new database            | `CREATE DATABASE database_name;`                                |
| **CREATE TABLE**    | Creates a new table               | `CREATE TABLE table_name (column1 datatype, column2 datatype);` |
| **SELECT**          | Retrieves data from tables        | `SELECT column1, column2 FROM table_name;`                      |
| **WHERE**           | Filters data based on conditions  | `SELECT * FROM table_name WHERE condition;`                     |
| **INSERT**          | Adds new rows to a table          | `INSERT INTO table_name VALUES (value1, value2);`               |
| **DELETE**          | Removes rows from a table         | `DELETE FROM table_name WHERE condition;`                       |
| **DROP TABLE**      | Removes a table from the database | `DROP TABLE table_name;`                                        |

---

## Tools Needed

**MySQL** - A free, open source relational database system that offers:

- Command line interface (MySQL CLI)
- Third-party web interface (phpMyAdmin)

**SN Labs Cloud IDE** - A virtual lab environment used in this course that includes MySQL as a service.

### Two Components of the SN Labs Cloud IDE

| Component                   | Location             | Purpose                                              |
| :-------------------------- | :------------------- | :--------------------------------------------------- |
| **Instructions**      | Left side of screen  | Steps to follow to complete the lab                  |
| **Tools & Terminals** | Right side of screen | Menus, terminals, and tools to execute lab exercises |

---

## Dataset Used in this Lab

The dataset used in this lab is a single **Open Document Spreadsheet file (.ods)** that contains:

| Attribute          | Value                                                      |
| :----------------- | :--------------------------------------------------------- |
| **Rows**     | 10 rows                                                    |
| **Columns**  | 6 columns                                                  |
| **Content**  | Fictitious customer demographics and insurance policy data |
| **Filename** | `Insurance-info.ods`                                     |

### Dataset Columns

| Column               | Description                         |
| :------------------- | :---------------------------------- |
| **CustomerID** | Unique identifier for each customer |
| **FirstName**  | Customer's first name               |
| **LastName**   | Customer's last name                |
| **Age**        | Customer's age                      |
| **PolicyType** | Type of insurance policy            |
| **Premium**    | Annual premium amount               |

---

## Exercise 1: Create a Database and Table

In this exercise, you will create a new database and table to store the insurance information.

### Step 1: Access phpMyAdmin

1. Navigate to the **phpMyAdmin** interface in the SN Labs Cloud IDE
2. Log in with your credentials (if required)

![phpMyAdmin home screen]


![alt text](<../Screenshots/phpMyAdmin home screen.png>)

### Step 2: Create a New Database

1. Click on the **New** button in the left sidebar
2. Enter the database name: `insurance_db`
3. Select **utf8mb4_general_ci** as the collation
4. Click **Create**

```sql
CREATE DATABASE insurance_db;
```

**Expected Output:**

```
Database created successfully.
```

![Create database]

![alt text](<../Screenshots/Create database.png>)

### Step 3: Select the Database

Click on the `insurance_db` database in the left sidebar to select it.

**Alternative method using SQL:**

```sql
USE insurance_db;
```

### Step 4: Create the Customers Table

Create a table named `customers` with the following structure:

```sql
CREATE TABLE customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Age INT,
    PolicyType VARCHAR(50),
    Premium DECIMAL(10, 2)
);
```

**Column Descriptions:**

| Column               | Data Type       | Description                              |
| :------------------- | :-------------- | :--------------------------------------- |
| **CustomerID** | INT PRIMARY KEY | Unique identifier, cannot be NULL        |
| **FirstName**  | VARCHAR(50)     | Customer's first name (max 50 chars)     |
| **LastName**   | VARCHAR(50)     | Customer's last name (max 50 chars)      |
| **Age**        | INT             | Customer's age in years                  |
| **PolicyType** | VARCHAR(50)     | Type of insurance policy                 |
| **Premium**    | DECIMAL(10,2)   | Annual premium amount (2 decimal places) |

![alt text](<../Screenshots/Create the Customers Table.png>)

![alt text](<../Screenshots/Create the Customers Table_executed.png>)

### Step 5: Verify Table Creation

```sql
SHOW TABLES;
```

**Expected Output:**

```
Tables_in_insurance_db
---------------------
customers
```

![alt text](<../Screenshots/Show tables.png>)

---

## Exercise 2: Populate the Table with Data

In this exercise, you will insert data into the `customers` table using INSERT statements.

### Step 1: Insert Individual Rows

Insert each customer record one at a time:

```sql
INSERT INTO customers (CustomerID, FirstName, LastName, Age, PolicyType, Premium)
VALUES (1, 'John', 'Smith', 35, 'Auto', 1200.00);
```

```sql
INSERT INTO customers (CustomerID, FirstName, LastName, Age, PolicyType, Premium)
VALUES (2, 'Sarah', 'Johnson', 42, 'Home', 1800.00);
```

```sql
INSERT INTO customers (CustomerID, FirstName, LastName, Age, PolicyType, Premium)
VALUES (3, 'Michael', 'Brown', 28, 'Life', 950.00);
```

```sql
INSERT INTO customers (CustomerID, FirstName, LastName, Age, PolicyType, Premium)
VALUES (4, 'Emily', 'Davis', 55, 'Health', 3200.00);
```

```sql
INSERT INTO customers (CustomerID, FirstName, LastName, Age, PolicyType, Premium)
VALUES (5, 'David', 'Wilson', 31, 'Auto', 1150.00);
```

![alt text](<../Screenshots/Insert Individual Rows.png>)

![alt text](<../Screenshots/Insert Individual Rows_executed.png>)

### Step 2: Insert Multiple Rows at Once

```sql
INSERT INTO customers (CustomerID, FirstName, LastName, Age, PolicyType, Premium)
VALUES 
    (6, 'Lisa', 'Martinez', 47, 'Home', 1950.00),
    (7, 'James', 'Anderson', 39, 'Life', 1100.00),
    (8, 'Patricia', 'Thomas', 62, 'Health', 4500.00),
    (9, 'Robert', 'Jackson', 44, 'Auto', 1300.00),
    (10, 'Maria', 'White', 29, 'Life', 875.00);
```

![alt text](<../Screenshots/Insert Multiple Rows at Once.png>)

![alt text](<../Screenshots/Insert Multiple Rows at Once_executed.png>)

### Step 3: Verify Data Insertion

```sql
SELECT * FROM customers;
```

**Expected Output:**

```
CustomerID | FirstName | LastName  | Age | PolicyType | Premium
-----------|-----------|-----------|-----|------------|--------
1          | John      | Smith     | 35  | Auto       | 1200.00
2          | Sarah     | Johnson   | 42  | Home       | 1800.00
3          | Michael   | Brown     | 28  | Life       | 950.00
4          | Emily     | Davis     | 55  | Health     | 3200.00
5          | David     | Wilson    | 31  | Auto       | 1150.00
6          | Lisa      | Martinez  | 47  | Home       | 1950.00
7          | James     | Anderson  | 39  | Life       | 1100.00
8          | Patricia  | Thomas    | 62  | Health     | 4500.00
9          | Robert    | Jackson   | 44  | Auto       | 1300.00
10         | Maria     | White     | 29  | Life       | 875.00
```

---

## Exercise 3: Retrieve Data Using SELECT Statements

In this exercise, you will use SELECT statements to retrieve data from the customers table.

### Step 1: Select All Columns

```sql
SELECT * FROM customers;
```

### Step 2: Select Specific Columns

```sql
SELECT FirstName, LastName, Premium FROM customers;
```

**Expected Output:**

```
FirstName | LastName  | Premium
----------|-----------|--------
John      | Smith     | 1200.00
Sarah     | Johnson   | 1800.00
Michael   | Brown     | 950.00
Emily     | Davis     | 3200.00
David     | Wilson    | 1150.00
Lisa      | Martinez  | 1950.00
James     | Anderson  | 1100.00
Patricia  | Thomas    | 4500.00
Robert    | Jackson   | 1300.00
Maria     | White     | 875.00
```

### Step 3: Use WHERE to Filter Data

**Problem:** Retrieve all customers with Auto insurance.

```sql
SELECT * FROM customers WHERE PolicyType = 'Auto';
```

**Expected Output:**

```
CustomerID | FirstName | LastName | Age | PolicyType | Premium
-----------|-----------|----------|-----|------------|--------
1          | John      | Smith    | 35  | Auto       | 1200.00
5          | David     | Wilson   | 31  | Auto       | 1150.00
9          | Robert    | Jackson  | 44  | Auto       | 1300.00
```

### Step 4: Use Comparison Operators

**Problem:** Retrieve customers with premium greater than $1500.

```sql
SELECT FirstName, LastName, Premium 
FROM customers 
WHERE Premium > 1500;
```

**Expected Output:**

```
FirstName | LastName  | Premium
----------|-----------|--------
Sarah     | Johnson   | 1800.00
Emily     | Davis     | 3200.00
Lisa      | Martinez  | 1950.00
Patricia  | Thomas    | 4500.00
```

### Step 5: Use Multiple Conditions with AND

**Problem:** Retrieve customers under 40 years old with Life insurance.

```sql
SELECT * FROM customers 
WHERE Age < 40 AND PolicyType = 'Life';
```

**Expected Output:**

```
CustomerID | FirstName | LastName | Age | PolicyType | Premium
-----------|-----------|----------|-----|------------|--------
3          | Michael   | Brown    | 28  | Life       | 950.00
10         | Maria     | White    | 29  | Life       | 875.00
```

### Step 6: Use Multiple Conditions with OR

**Problem:** Retrieve customers with Home or Health insurance.

```sql
SELECT FirstName, LastName, PolicyType 
FROM customers 
WHERE PolicyType = 'Home' OR PolicyType = 'Health';
```

**Expected Output:**

```
FirstName | LastName  | PolicyType
----------|-----------|-----------
Sarah     | Johnson   | Home
Emily     | Davis     | Health
Lisa      | Martinez  | Home
Patricia  | Thomas    | Health
```

---

## Exercise 4: Add and Remove Data Using INSERT and DELETE

In this exercise, you will use INSERT to add new rows and DELETE to remove rows from the table.

### Step 1: Insert a New Row

**Problem:** Add a new customer with the following information:

- CustomerID: 11
- FirstName: Charles
- LastName: Lee
- Age: 52
- PolicyType: Auto
- Premium: 1400.00

```sql
INSERT INTO customers (CustomerID, FirstName, LastName, Age, PolicyType, Premium)
VALUES (11, 'Charles', 'Lee', 52, 'Auto', 1400.00);
```

### Step 2: Verify the Insert

```sql
SELECT * FROM customers WHERE CustomerID = 11;
```

### Step 3: Delete a Specific Row

**Problem:** Delete the customer with CustomerID = 11.

```sql
DELETE FROM customers WHERE CustomerID = 11;
```

### Step 4: Verify the Delete

```sql
SELECT * FROM customers WHERE CustomerID = 11;
```

**Expected Output:**

```
(empty result set)
```

### Step 5: Delete Rows Based on Conditions

**Problem:** Delete all customers with Health insurance.

```sql
DELETE FROM customers WHERE PolicyType = 'Health';
```

### Step 6: Verify the Delete

```sql
SELECT * FROM customers WHERE PolicyType = 'Health';
```

**Expected Output:**

```
(empty result set)
```

---

## Exercise 5: Remove a Table Using DROP

In this exercise, you will use the DROP TABLE statement to remove a table from the database.

### Step 1: Drop the Customers Table

**Warning:** This action is irreversible and will delete all data in the table.

```sql
DROP TABLE customers;
```

### Step 2: Verify the Table is Removed

```sql
SHOW TABLES;
```

**Expected Output:**

```
Tables_in_insurance_db
---------------------
(empty set)
```

---

## Practice Exercises

### Problem 1: Create and Populate a New Table

**Scenario:** Create a new table called `claims` with the following structure:

| Column      | Data Type       | Description                              |
| ----------- | --------------- | ---------------------------------------- |
| ClaimID     | INT PRIMARY KEY | Unique claim identifier                  |
| CustomerID  | INT             | Foreign key to customers table           |
| ClaimDate   | DATE            | Date of claim                            |
| ClaimAmount | DECIMAL(10,2)   | Amount claimed                           |
| Status      | VARCHAR(20)     | Claim status (Pending, Approved, Denied) |

<details>
<summary>✅ Solution</summary>

```sql
CREATE TABLE claims (
    ClaimID INT PRIMARY KEY,
    CustomerID INT,
    ClaimDate DATE,
    ClaimAmount DECIMAL(10,2),
    Status VARCHAR(20)
);

INSERT INTO claims VALUES 
(1, 1, '2024-01-15', 2500.00, 'Approved'),
(2, 3, '2024-02-20', 1800.00, 'Pending'),
(3, 5, '2024-03-10', 3200.00, 'Approved');
```

</details>

---

### Problem 2: Filter Data with WHERE

**Scenario:** Retrieve all customers with premium between $1000 and $2000.

<details>
<summary>✅ Solution</summary>

```sql
SELECT * FROM customers 
WHERE Premium BETWEEN 1000 AND 2000;
```

</details>

---

### Problem 3: Delete with Conditions

**Scenario:** Delete all customers over 60 years old.

<details>
<summary>✅ Solution</summary>

```sql
DELETE FROM customers WHERE Age > 60;
```

</details>

---

## Lab Completion Checklist

| Task                                        | Completed |
| :------------------------------------------ | :-------- |
| **Database Setup**                    |           |
| Created insurance_db database               | ☐        |
| Selected the database                       | ☐        |
| Created customers table with proper columns | ☐        |
| Verified table creation                     | ☐        |
| **Data Population**                   |           |
| Inserted individual rows (1-5)              | ☐        |
| Inserted multiple rows at once (6-10)       | ☐        |
| Verified data insertion with SELECT         | ☐        |
| **Data Retrieval**                    |           |
| Selected all columns with SELECT *          | ☐        |
| Selected specific columns                   | ☐        |
| Used WHERE to filter by PolicyType          | ☐        |
| Used comparison operators (>, <)            | ☐        |
| Used AND operator for multiple conditions   | ☐        |
| Used OR operator for multiple conditions    | ☐        |
| **Data Modification**                 |           |
| Inserted a new row with INSERT              | ☐        |
| Deleted a specific row with WHERE           | ☐        |
| Deleted rows based on conditions            | ☐        |
| **Table Removal**                     |           |
| Dropped the customers table with DROP TABLE | ☐        |
| Verified table was removed                  | ☐        |

---

## Screenshot Checklist

| Screenshot        | File Name                  | Description                        |
| :---------------- | :------------------------- | :--------------------------------- |
| Database Creation | `DB_Create_Database.png` | Database created successfully      |
| Table Creation    | `DB_Create_Table.png`    | Customers table structure          |
| Data Insertion    | `DB_Insert_Data.png`     | INSERT statements and verification |
| SELECT Query      | `DB_Select_Query.png`    | SELECT with WHERE clause results   |
| DELETE Operation  | `DB_Delete_Query.png`    | DELETE statement results           |
| DROP Table        | `DB_Drop_Table.png`      | Table dropped confirmation         |

---

## Troubleshooting Tips

| Issue                                  | Solution                                                         |
| :------------------------------------- | :--------------------------------------------------------------- |
| **Database already exists**      | Use `DROP DATABASE IF EXISTS insurance_db` before creating     |
| **Table already exists**         | Use `DROP TABLE IF EXISTS customers` before creating           |
| **Foreign key constraint fails** | Delete child records before deleting parent records              |
| **Syntax error**                 | Check for missing commas, quotes, or parentheses                 |
| **Data type mismatch**           | Ensure inserted values match column data types                   |
| **DELETE without WHERE**         | Always include WHERE clause unless you intend to delete all rows |

---

## Common SQL Commands Summary

| Command             | Purpose             | Example                                                   |
| :------------------ | :------------------ | :-------------------------------------------------------- |
| `CREATE DATABASE` | Create new database | `CREATE DATABASE db_name;`                              |
| `CREATE TABLE`    | Create new table    | `CREATE TABLE table_name (col1 INT, col2 VARCHAR(50));` |
| `INSERT INTO`     | Add rows to table   | `INSERT INTO table_name VALUES (1, 'value');`           |
| `SELECT`          | Retrieve data       | `SELECT * FROM table_name;`                             |
| `WHERE`           | Filter results      | `SELECT * FROM table_name WHERE condition;`             |
| `DELETE FROM`     | Remove rows         | `DELETE FROM table_name WHERE condition;`               |
| `DROP TABLE`      | Remove table        | `DROP TABLE table_name;`                                |
| `SHOW TABLES`     | List all tables     | `SHOW TABLES;`                                          |

---

## Key Takeaways

| Concept                   | Description                                         |
| :------------------------ | :-------------------------------------------------- |
| **CREATE DATABASE** | Creates a new database container for tables         |
| **CREATE TABLE**    | Defines table structure with columns and data types |
| **INSERT**          | Adds new rows of data to a table                    |
| **SELECT**          | Retrieves data; use WHERE to filter results         |
| **DELETE**          | Removes rows; always use WHERE to avoid data loss   |
| **DROP TABLE**      | Completely removes a table and all its data         |
| **Primary Key**     | Uniquely identifies each row in a table             |
| **VARCHAR**         | Variable-length string data type                    |
| **DECIMAL**         | Exact numeric data type for currency                |

---

## Summary

In this hands-on lab, you have:

| Activity                                                          | Completed |
| :---------------------------------------------------------------- | :-------- |
| Created a database using phpMyAdmin                               | ✓        |
| Created a table with appropriate data types                       | ✓        |
| Inserted data using individual and multiple-row INSERT statements | ✓        |
| Retrieved data using SELECT statements                            | ✓        |
| Filtered data using WHERE with comparison operators               | ✓        |
| Used AND and OR operators for complex conditions                  | ✓        |
| Added new rows with INSERT                                        | ✓        |
| Removed rows with DELETE and WHERE                                | ✓        |
| Removed a table using DROP TABLE                                  | ✓        |

---

## Congratulations

You have successfully completed the **Basic Database Operations** lab. You now know how to:

- Create and populate databases and tables using phpMyAdmin
- Execute SQL commands to perform basic database operations
- Retrieve data from tables using SELECT statements
- Filter data output using WHERE statements with various operators
- Add and remove data from tables using INSERT and DELETE statements
- Remove tables using DROP statements

These skills are fundamental to working with relational databases and form the foundation for more advanced database operations.

---

*Last updated: January 2026*
