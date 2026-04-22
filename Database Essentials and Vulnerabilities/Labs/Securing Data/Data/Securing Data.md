
![alt text](<../Screenshots/PhpMyAdmin_logo (1).png>)

# Lab: Securing Data — Encryption, Hashing, Masking, and Access Control

**Estimated time:** 45 minutes

---

## Introduction

In today's digital landscape, data security is paramount, particularly in databases that store sensitive information. This lab, "Securing Data," aims to equip participants with practical skills in safeguarding data using a variety of techniques.

Participants will explore methods such as:
- **Encryption** for protecting data at rest and in transit
- **Hashing** for secure password storage
- **Data masking** for obscuring sensitive information
- **Tokenization** for replacing sensitive data with non-sensitive equivalents
- **Permission restrictions** for enforcing role-based access controls

By the end of this lab, participants will have a comprehensive understanding of how to apply these security measures within MySQL, thereby enhancing their ability to protect data against unauthorized access and breaches.

---

## Learning Objectives

| Objective | Description |
|:----------|:------------|
| **Implement Data Encryption** | Use MySQL's encryption functions to secure sensitive data both at rest and during transmission |
| **Apply Secure Data Handling** | Gain hands-on experience in hashing passwords, masking data, and tokenizing sensitive information |
| **Establish Role-Based Access Controls** | Configure permissions and roles within MySQL to manage and restrict access to sensitive data |

---

## Concepts Covered

### Security Techniques Overview

| Technique | Purpose | MySQL Functions |
|:----------|:--------|:----------------|
| **Encryption** | Protect data confidentiality (reversible) | `AES_ENCRYPT()`, `AES_DECRYPT()` |
| **Hashing** | Secure password storage (irreversible) | `SHA2()`, `MD5()`, `SHA1()` |
| **Data Masking** | Obscure sensitive data for non-production use | `CONCAT()`, `SUBSTRING()`, `INSERT()` |
| **Tokenization** | Replace sensitive data with non-sensitive tokens | Custom implementation |
| **Access Control** | Restrict data access based on user roles | `GRANT`, `REVOKE`, `CREATE ROLE` |

---

## Database Creation

In order to perform all the activities mentioned in this lab, you need to specify a database.

### Step 1: Ensure a Database Exists

Make sure you have a database created. If not, create one with the following command:

```sql
CREATE DATABASE my_database;
```

![alt text](<../Screenshots/Ensure a Database Exists.png>)

![alt text](<../Screenshots/Ensure a Database Exists_executed.png>)

### Step 2: Select the Database

Use the `USE` command to select the database you want to work with:

```sql
USE my_database;
```

![alt text](<../Screenshots/Select the Database.png>)

---

## Exercise 1: Encryption — Protecting Data at Rest

In this exercise, you will implement encryption for data at rest using MySQL's built-in encryption functions.

### Activity: Implement Encryption for Data at Rest

**Technique:** Data encryption at rest using AES (Advanced Encryption Standard)

### Step 1: Create the Encrypted Data Table

```sql
CREATE TABLE sensitive_data (
    id INT AUTO_INCREMENT PRIMARY KEY,
    encrypted_data VARBINARY(255)
);
```

![alt text](<../Screenshots/Create the Encrypted Data Table.png>)

![alt text](<../Screenshots/Create the Encrypted Data Table_executed.png>)

**Explanation:** This creates a table named `sensitive_data` with an `id` column and an `encrypted_data` column to store encrypted information. The `VARBINARY` data type is used because encrypted data is binary.

### Step 2: Insert Encrypted Data

```sql
INSERT INTO sensitive_data (encrypted_data)
VALUES (AES_ENCRYPT('Sensitive Data', 'encryption_key'));
```

![alt text](<../Screenshots/Insert Encrypted Data.png>)

![alt text](<../Screenshots/Insert Encrypted Data_executed.png>)



**Explanation:** The `AES_ENCRYPT` function encrypts the data 'Sensitive Data' using the key 'encryption_key'. The result is stored as binary data.

### Step 3: Retrieve and Decrypt Data

```sql
SELECT id, AES_DECRYPT(encrypted_data, 'encryption_key') AS decrypted_data
FROM sensitive_data;
```
![alt text](<../Screenshots/Retrieve and Decrypt Data.png>)


**Explanation:** To decrypt, `AES_DECRYPT` is used with the same encryption key to convert the binary data back to its original plaintext form.

### Step 4: Using a Hashed Encryption Key (More Secure)

For better security, use a hashed key instead of a plaintext key:

```sql
-- Create a hashed key variable
SET @key_str = SHA2('MyStrongPassphrase', 512);

-- Insert with hashed key
INSERT INTO sensitive_data (encrypted_data)
VALUES (AES_ENCRYPT('Sensitive Data', @key_str));

-- Retrieve with hashed key
SELECT id, AES_DECRYPT(encrypted_data, @key_str) AS decrypted_data
FROM sensitive_data;
```

![alt text](<../Screenshots/Using a Hashed Encryption Key (More Secure).png>)

![alt text](<../Screenshots/Using a Hashed Encryption Key (More Secure)_executed.png>)

---

## Exercise 2: Hashing — Secure Password Storage

In this exercise, you will apply hashing for secure password storage using MySQL hash functions.

### Activity: Implement Hashing for Passwords

**Technique:** Use MySQL hash functions to store passwords securely (irreversible)

### Step 1: Create the Users Table

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE,
    password_hash VARBINARY(255)
);
```

![alt text](<../Screenshots/Create the Users Table.png>)

![alt text](<../Screenshots/Create the Users Table_executed.png>)


**Explanation:** This creates a table named `users` with `id`, `username`, and `password_hash` columns to store user information and hashed passwords.

### Step 2: Insert a Hashed Password

```sql
INSERT INTO users (username, password_hash)
VALUES ('user1', SHA2('password123', 256));
```

![alt text](<../Screenshots/Insert a Hashed Password.png>)

**Explanation:** The `SHA2` function hashes the password 'password123' using the SHA-256 algorithm (256-bit output). The hashed password is stored in the `password_hash` column.

### Step 3: Verify a Hashed Password (Login Validation)

```sql
SELECT username
FROM users
WHERE username = 'user1' AND password_hash = SHA2('password123', 256);
```

![alt text](<../Screenshots/Verify a Hashed Password (Login Validation).png>)

**Explanation:** To verify, the same hashing function is applied to the input password. If the hashes match, the credentials are valid.

### Step 4: Adding Salt for Additional Security

```sql
-- Create table with salt column
CREATE TABLE users_secure (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE,
    password_hash VARBINARY(255),
    salt VARBINARY(32)
);

-- Insert with random salt
SET @salt = RANDOM_BYTES(16);
INSERT INTO users_secure (username, password_hash, salt)
VALUES ('user1', SHA2(CONCAT('password123', @salt), 256), @salt);

-- Verify with salt
SELECT username
FROM users_secure
WHERE username = 'user1' 
  AND password_hash = SHA2(CONCAT('password123', salt), 256);
```

![alt text](<../Screenshots/Adding Salt for Additional Security.png>)

![alt text](<../Screenshots/Adding Salt for Additional Security_executed.png>)

---

## Exercise 3: Data Masking — Obscuring Sensitive Information

In this exercise, you will implement data masking techniques to protect sensitive data in non-production environments.

### Activity: Mask Sensitive Data

**Technique:** Use MySQL string functions to mask sensitive data

### Step 1: Create the Employees Table

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    ssn VARCHAR(11),
    phone VARCHAR(15),
    email VARCHAR(100),
    credit_card VARCHAR(19)
);
```

![alt text](<../Screenshots/Create the Employees Table.png>)

![alt text](<../Screenshots/Create the Employees Table_executed.png>)

### Step 2: Insert Sample Data

```sql
INSERT INTO employees (ssn, phone, email, credit_card) VALUES
('123-45-6789', '555-123-4567', 'john.doe@example.com', '4111-1111-1111-1111'),
('987-65-4321', '555-987-6543', 'jane.smith@example.com', '5500-0000-0000-0004');
```

![alt text](<../Screenshots/Insert Sample Data.png>)

### Step 3: Mask SSN (Social Security Number)

```sql
SELECT 
    CONCAT('XXX-XX-', SUBSTRING(ssn, 8)) AS masked_ssn
FROM employees;
```

**Explanation:** The `CONCAT` and `SUBSTRING` functions are used to mask the SSN by showing only the last 4 digits.

**Output:**

```
masked_ssn
-----------
XXX-XX-6789
XXX-XX-4321
```

![alt text](<../Screenshots/Mask SSN (Social Security Number).png>)

### Step 4: Mask Phone Numbers

```sql
SELECT 
    CONCAT('XXX-XXX-', SUBSTRING(phone, 9)) AS masked_phone
FROM employees;
```

**Output:**

```
masked_phone
------------
XXX-XXX-4567
XXX-XXX-6543
```

![alt text](<../Screenshots/Mask Phone Numbers.png>)

### Step 5: Mask Email Addresses

```sql
SELECT 
    CONCAT(LEFT(email, 1), '***@', SUBSTRING_INDEX(email, '@', -1)) AS masked_email
FROM employees;
```

**Output:**

```
masked_email
------------
j***@example.com
j***@example.com
```

![alt text](<../Screenshots/Mask Email Addresses.png>)

### Step 6: Mask Credit Card Numbers

```sql
SELECT 
    CONCAT('XXXX-XXXX-XXXX-', RIGHT(credit_card, 4)) AS masked_card
FROM employees;
```

**Output:**

```
masked_card
-----------------
XXXX-XXXX-XXXX-1111
XXXX-XXXX-XXXX-0004
```

![alt text](<../Screenshots/Mask Credit Card Numbers.png>)

---

## Exercise 4: Tokenization — Replacing Sensitive Data

In this exercise, you will implement tokenization to replace sensitive data with non-sensitive equivalents.

### Activity: Implement Tokenization

**Technique:** Replace sensitive data with randomly generated tokens

### Step 1: Create Token Mapping Table

```sql
CREATE TABLE token_mapping (
    token_id INT AUTO_INCREMENT PRIMARY KEY,
    original_value TEXT,
    token VARCHAR(50) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

![alt text](<../Screenshots/Create Token Mapping Table.png>)

![alt text](<../Screenshots/Create Token Mapping Table_executed.png>)


### Step 2: Create Function to Generate Token

```sql
-- Generate a random token
SET @token = MD5(RAND());
```

![alt text](<../Screenshots/Create Function to Generate Token.png>)

### Step 3: Insert and Tokenize Data

```sql
-- Original sensitive data
SET @original_ssn = '123-45-6789';
SET @token = MD5(CONCAT(@original_ssn, RAND(), NOW()));

-- Store mapping
INSERT INTO token_mapping (original_value, token) 
VALUES (@original_ssn, @token);

-- Store only the token in application table
CREATE TABLE customer_data (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_name VARCHAR(100),
    ssn_token VARCHAR(50)
);

INSERT INTO customer_data (customer_name, ssn_token)
VALUES ('John Doe', @token);
```

![alt text](<../Screenshots/Insert and Tokenize Data.png>)

### Step 4: Retrieve Original Data (Authorized Only)

```sql
-- Join to get original data (restrict to authorized users)
SELECT cd.customer_name, tm.original_value AS ssn
FROM customer_data cd
JOIN token_mapping tm ON cd.ssn_token = tm.token;
```

![alt text](<../Screenshots/Retrieve Original Data (Authorized Only).png>)

---

## Exercise 5: Role-Based Access Control (RBAC)

In this exercise, you will establish role-based access controls by configuring permissions and roles within MySQL.

### Activity: Implement Role-Based Access Control

**Technique:** Use MySQL `GRANT`, `REVOKE`, and `CREATE ROLE` statements

### Step 1: Create Roles

```sql
-- Create application roles
CREATE ROLE 'app_admin';
CREATE ROLE 'app_manager';
CREATE ROLE 'app_user';
CREATE ROLE 'app_viewer';
```

![alt text](<../Screenshots/Create Roles.png>)


### Step 2: Grant Privileges to Roles

```sql
-- Admin role: full access
GRANT ALL PRIVILEGES ON my_database.* TO 'app_admin';

-- Manager role: read and write on most tables
GRANT SELECT, INSERT, UPDATE ON my_database.employees TO 'app_manager';
GRANT SELECT, INSERT, UPDATE ON my_database.users TO 'app_manager';

-- User role: read-only on employees, full on own data
GRANT SELECT ON my_database.employees TO 'app_user';
GRANT SELECT, INSERT, UPDATE ON my_database.users TO 'app_user';

-- Viewer role: read-only on non-sensitive data
GRANT SELECT (id, username) ON my_database.users TO 'app_viewer';
```

![alt text](<../Screenshots/Grant Privileges to Roles.png>)


### Step 3: Create Users and Assign Roles

```sql
-- Create users
CREATE USER 'alice'@'localhost' IDENTIFIED BY 'StrongPass123!';
CREATE USER 'bob'@'localhost' IDENTIFIED BY 'SecurePass456!';
CREATE USER 'charlie'@'localhost' IDENTIFIED BY 'ViewOnly789!';

-- Assign roles
GRANT 'app_admin' TO 'alice'@'localhost';
GRANT 'app_user' TO 'bob'@'localhost';
GRANT 'app_viewer' TO 'charlie'@'localhost';

-- Set default roles
SET DEFAULT ROLE 'app_admin' TO 'alice'@'localhost';
SET DEFAULT ROLE 'app_user' TO 'bob'@'localhost';
SET DEFAULT ROLE 'app_viewer' TO 'charlie'@'localhost';
```

![alt text](<../Screenshots/Create Users and Assign Roles.png>)


### Step 4: Verify Role Assignments

```sql
-- Show grants for a user
SHOW GRANTS FOR 'alice'@'localhost';

-- Show roles assigned to a user
SELECT * FROM mysql.default_roles WHERE USER = 'alice';
```

![alt text](<../Screenshots/Verify Role Assignments.png>)

### Step 5: Create Views for Column-Level Security

```sql
-- Create a view that excludes sensitive columns
CREATE VIEW employees_public AS
SELECT id, 
       CONCAT('XXX-XX-', SUBSTRING(ssn, 8)) AS masked_ssn,
       CONCAT('XXX-XXX-', SUBSTRING(phone, 9)) AS masked_phone,
       email
FROM employees;

-- Grant access to the view instead of the base table
GRANT SELECT ON my_database.employees_public TO 'app_viewer';
```

![alt text](<../Screenshots/Create Views for Column-Level Security.png>)

---

## Practice Exercises

### Exercise 1: Implement Encryption

**Scenario:** Create a table to store customer credit card information securely using encryption.

<details>
<summary>✅ Solution</summary>

```sql
CREATE TABLE customer_cards (
    card_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_name VARCHAR(100),
    encrypted_card VARBINARY(255),
    encrypted_expiry VARBINARY(255)
);

SET @key = SHA2('CustomerDataKey2024', 256);

INSERT INTO customer_cards (customer_name, encrypted_card, encrypted_expiry)
VALUES ('John Smith', 
        AES_ENCRYPT('4111-1111-1111-1111', @key),
        AES_ENCRYPT('12/28', @key));

SELECT customer_name, 
       AES_DECRYPT(encrypted_card, @key) AS card_number,
       AES_DECRYPT(encrypted_expiry, @key) AS expiry
FROM customer_cards;
```

</details>

![alt text](<../Screenshots/Implement Encryption.png>)

---

### Exercise 2: Implement Password Hashing with Salt

**Scenario:** Create a user authentication system with salted password hashes.

<details>
<summary>✅ Solution</summary>

```sql
CREATE TABLE auth_users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE,
    password_hash VARBINARY(255),
    salt VARBINARY(32),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Register a new user
SET @username = 'john_doe';
SET @password = 'MySecurePassword';
SET @salt = RANDOM_BYTES(16);
SET @hash = SHA2(CONCAT(@password, @salt), 256);

INSERT INTO auth_users (username, password_hash, salt)
VALUES (@username, @hash, @salt);

-- Login verification
SELECT user_id 
FROM auth_users 
WHERE username = 'john_doe' 
  AND password_hash = SHA2(CONCAT('MySecurePassword', salt), 256);
```

</details>

![alt text](<../Screenshots/Implement Password Hashing with Salt.png>)

---

### Exercise 3: Create Role-Based Access

**Scenario:** Create a role for data analysts who need read-only access to employee data but should not see salary information.

<details>
<summary>✅ Solution</summary>

```sql
-- Create role
CREATE ROLE IF NOT EXISTS 'data_analyst';

-- Create safe view
CREATE OR REPLACE VIEW my_database.employee_analyst AS
SELECT 
    id,
    email
FROM my_database.employees;

-- Grant access ONLY to the view
GRANT SELECT ON my_database.employee_analyst TO 'data_analyst';

-- Create user and assign role
CREATE USER IF NOT EXISTS 'analyst1'@'localhost' IDENTIFIED BY 'AnalystPass123';
GRANT 'data_analyst' TO 'analyst1'@'localhost';
SET DEFAULT ROLE 'data_analyst' TO 'analyst1'@'localhost';
```

</details>

![alt text](<../Screenshots/Create Role-Based Access.png>)

---

## Lab Completion Checklist

| Task                                      | Completed |
| :---------------------------------------- | :-------- |
| **Database Setup**                  |           |
| Created my_database                       | ☐        |
| Selected the database with USE            | ☐        |
| **Encryption**                      |           |
| Created sensitive_data table              | ☐        |
| Inserted encrypted data with AES_ENCRYPT  | ☐        |
| Retrieved decrypted data with AES_DECRYPT | ☐        |
| **Hashing**                         |           |
| Created users table                       | ☐        |
| Inserted hashed passwords with SHA2       | ☐        |
| Verified passwords with hash comparison   | ☐        |
| Implemented salt for additional security  | ☐        |
| **Data Masking**                    |           |
| Created employees table                   | ☐        |
| Masked SSN numbers                        | ☐        |
| Masked phone numbers                      | ☐        |
| Masked email addresses                    | ☐        |
| Masked credit card numbers                | ☐        |
| **Tokenization**                    |           |
| Created token_mapping table               | ☐        |
| Generated tokens for sensitive data       | ☐        |
| Stored tokens instead of original data    | ☐        |
| **Access Control**                  |           |
| Created application roles                 | ☐        |
| Granted privileges to roles               | ☐        |
| Created users and assigned roles          | ☐        |
| Created views for column-level security   | ☐        |

---

## Screenshot Checklist

| Screenshot     | File Name                     | Description                           |
| :------------- | :---------------------------- | :------------------------------------ |
| Encryption     | `Security_Encryption.png`   | AES_ENCRYPT and AES_DECRYPT results   |
| Hashing        | `Security_Hashing.png`      | SHA2 hashed passwords                 |
| Masking        | `Security_Masking.png`      | Masked SSN, phone, email, credit card |
| Tokenization   | `Security_Tokenization.png` | Token mapping table                   |
| Access Control | `Security_RBAC.png`         | Role grants and user assignments      |

---

## Summary Table of Security Techniques

| Technique                | MySQL Function                        | Use Case                          | Reversible?        |
| :----------------------- | :------------------------------------ | :-------------------------------- | :----------------- |
| **Encryption**     | `AES_ENCRYPT()` / `AES_DECRYPT()` | Protecting sensitive data at rest | Yes                |
| **Hashing**        | `SHA2()`, `MD5()`                 | Password storage                  | No                 |
| **Masking**        | `CONCAT()`, `SUBSTRING()`         | Non-production data obfuscation   | Partial            |
| **Tokenization**   | Custom (MD5, RAND)                    | Payment card data, PII            | Yes (with mapping) |
| **Access Control** | `GRANT`, `REVOKE`                 | User permission management        | N/A                |

---

## Key Takeaways

| Concept                    | Key Point                                                                          |
| :------------------------- | :--------------------------------------------------------------------------------- |
| **Encryption**       | Use AES_ENCRYPT/AES_DECRYPT for reversible data protection; always use strong keys |
| **Hashing**          | Never store plaintext passwords; use SHA-256 or stronger with unique salts         |
| **Data Masking**     | Protect sensitive data in non-production environments; use string functions        |
| **Tokenization**     | Replace sensitive data with tokens; store mapping separately                       |
| **Least Privilege**  | Grant only necessary permissions; use roles for easier management                  |
| **Defense in Depth** | Combine multiple techniques for comprehensive data protection                      |

---

## Congratulations!

You have successfully completed the **Securing Data** lab. You now understand how to:

- Implement data encryption using MySQL's AES functions
- Apply hashing for secure password storage with salt
- Mask sensitive data for non-production environments
- Implement tokenization to replace sensitive data
- Establish role-based access controls with MySQL roles and privileges

These skills are essential for protecting sensitive data in database systems and ensuring compliance with data security regulations like GDPR, HIPAA, and PCI-DSS.

---



*Last updated: January 2026*


