![alt text](<../Screenshots/PhpMyAdmin_logo (1).png>)

# Lab: MySQL User Access Control and Data Encryption

**Estimated time:** 35 minutes

---

## Learning Objectives

After completing this lab you'll be able to manage MySQL user accounts, control database access, and implement data encryption. You'll also be able to demonstrate the skills needed to use phpMyAdmin and MySQL CLI to perform these tasks.

| Objective | Description |
|:----------|:------------|
| **User Account Management** | Create and manage MySQL user accounts with appropriate privileges |
| **Access Control** | Control access to MySQL databases and their objects at database and table levels |
| **Data Encryption** | Secure sensitive data using AES encryption and decryption |

---

## Concepts Covered

### MySQL User Privilege Levels

| Level | Scope | Description |
|:------|:------|:------------|
| **Global** | All databases | Applies to all databases on the MySQL server |
| **Database** | Specific database | Applies to all objects within a specific database |
| **Table** | Specific table | Applies to specific tables within a database |
| **Column** | Specific column | Applies to specific columns within a table |

### Common MySQL Privileges

| Privilege | Description |
|:----------|:------------|
| **ALL PRIVILEGES** | Grants all available privileges |
| **SELECT** | Allows reading data from tables |
| **INSERT** | Allows adding new rows to tables |
| **UPDATE** | Allows modifying existing data |
| **DELETE** | Allows removing rows from tables |
| **CREATE** | Allows creating new databases and tables |
| **DROP** | Allows deleting databases and tables |

### AES Encryption in MySQL

| Function | Purpose |
|:---------|:--------|
| `AES_ENCRYPT()` | Encrypts data using AES algorithm |
| `AES_DECRYPT()` | Decrypts data encrypted with AES_ENCRYPT() |
| `SHA2()` | Hashes a passphrase using SHA-2 family (224, 256, 384, 512 bits) |

---

## Tools Needed

- **phpMyAdmin** - Web-based GUI tool for managing MySQL databases
- **MySQL CLI** - Command-line interface for executing SQL commands
- **MySQL Database** - world database (sample database)

---

## Exercise 1: Create a MySQL User Account

In this exercise, you will learn how to create a user account and grant appropriate privileges.

### Step 1: Access phpMyAdmin

1. Navigate to your phpMyAdmin installation
2. Log in with administrator credentials

![phpMyAdmin home screen]

![alt text](<../Screenshots/phpMyAdmin home screen_.png>)

### Step 2: Navigate to User Accounts

1. Go to **Home** > **User accounts** tab
2. Click **Add user account**

![User accounts tab]

![alt text](<../Screenshots/User accounts tab.png>)

### Step 3: Create New User

Fill in the following information:

| Field | Value |
|-------|-------|
| **User name** | db_owner |
| **Host name** | localhost |
| **Password** | [Create a strong password] |
| **Re-type** | [Same password] |

![alt text](<../Screenshots/Fill the Login Information.png>)

### Step 4: Grant Database Privileges

1. Under **Database for user account**, select **Create database with same name and grant all privileges**
2. This automatically creates a database named `db_owner` and grants all privileges on it

![alt text](<../Screenshots/Grant Database Privileges.png>)

### Step 5: Grant Global Privileges (Optional)

Select the following global privileges if needed:

| Privilege | Purpose |
|:----------|:--------|
| **SELECT** | Read data from any database |
| **INSERT** | Add data to any database |
| **UPDATE** | Modify data in any database |
| **DELETE** | Remove data from any database |

### Step 6: Complete User Creation

1. Click **Go** at the bottom of the page
2. Verify that the user appears in the User accounts list

![User created successfully]

![alt text](<../Screenshots/User created successfully.png>)

![alt text](<../Screenshots/User created successfully_executed.png>)

### Step 7: Verify User Creation

You should see a confirmation message:
```

You have successfully created a user account with appropriate privileges.

```

---

## Exercise 2: Control Access to MySQL Databases and Their Objects

In this exercise, you will learn how to control access to MySQL databases and their objects by modifying user privileges.

### Scenario

You will modify privileges of the user `db_owner` so that this user cannot update any columns except the `Population` column of the `city` table in the `world` database.

### Step 1: Access User Privileges

1. Go to **Home** > **User accounts** tab
2. Click **Edit privileges** next to the `db_owner` user

![Edit privileges option]

### Step 2: Select Database

1. Under the **Database** sub-tab
2. Select the `world` database from the list
3. Click **Go**

![Select world database]

### Step 3: Grant Database-Specific Privileges

1. Under **Database-specific privileges**
2. Click **Check all** to select all privileges
3. Click **Go** at the bottom

![Database-specific privileges]

### Step 4: Switch to Table-Specific Privileges

1. Switch to the **Table** sub-tab
2. Select the table `city` from the drop-down menu
3. Click **Go**

![Select city table]

### Step 5: Configure Table-Specific Privileges

Under **Table-specific privileges**, configure access to columns of the `city` table as shown:

| Command | Grant | Restrict To |
|:--------|:------|:------------|
| **SELECT** | ✓ | All columns |
| **INSERT** | ✓ | All columns |
| **UPDATE** | ✓ | Only Population column |
| **DELETE** | ✓ | All columns |

**To restrict UPDATE to only the Population column:**

1. Find the **UPDATE** row in the privilege table
2. Select **Population** from the column dropdown
3. Ensure other columns are not selected

![Table-specific privileges configuration]

### Step 6: Save Changes

1. Click **Go** at the bottom of the page
2. The configuration will restrict `db_owner` from updating all columns except the `Population` column

---

## Exercise 3: Secure Data Using Encryption

In this exercise, you will learn how to secure your data by adding an extra layer of security using data encryption.

### Important Note

There may be certain parts of your database containing sensitive information which should not be stored in plain text. This is where encryption comes in.

### Encryption Overview

You will implement encryption and decryption of a column in the `world` database using the official **AES (Advanced Encryption Standard)** algorithm.

| AES Characteristic | Description |
|:-------------------|:------------|
| **Type** | Symmetric encryption (same key encrypts and decrypts) |
| **Default key length** | 128 bits |
| **Alternate key lengths** | 196 or 256 bits |
| **Trade-off** | Key length vs performance and security |

### Step 1: Open MySQL CLI

1. Click the **MySQL CLI** button from the MySQL service session tab

![MySQL CLI button]

### Step 2: Hash the Passphrase

First, you will need to hash your passphrase with a specific hash length using a hash function from the SHA-2 family.

**Important:** It is good practice to hash the passphrase you use, since storing the passphrase in plaintext is a significant security vulnerability.

**Command:**
```sql
SET @key_str = SHA2('My secret passphrase', 512);
```

**Explanation:**

- `My secret passphrase` - Your chosen passphrase (replace with your own)
- `512` - Hash length (can be 224, 256, 384, or 512)

![Hash passphrase command]

### Step 3: Connect to the Database

```sql
USE world;
```

### Step 4: View the Current Table

Take a quick look at the `countrylanguage` table:

```sql
SELECT * FROM countrylanguage LIMIT 5;
```

**Note:** For demonstration purposes, suppose that the last column in the table, labeled `Percentage`, contains sensitive data, such as a citizen's passport number. Storing such sensitive data in plain text is an enormous security concern.

![countrylanguage table before encryption]

### Step 5: Modify Column Data Type

To encrypt the `Percentage` column, first convert the data in the column into binary byte strings of length 255:

```sql
ALTER TABLE countrylanguage 
MODIFY COLUMN Percentage varbinary(255);
```

![Modify column data type]

### Step 6: Encrypt the Column

Use the AES encryption standard and your hashed passphrase to encrypt the column:

```sql
UPDATE countrylanguage 
SET Percentage = AES_ENCRYPT(Percentage, @key_str);
```

**Important:** This operation cannot be undone without the key. Make sure to store your passphrase securely!

![Encrypt column command]

### Step 7: Verify Encryption

Check if the column was successfully encrypted:

```sql
SELECT * FROM countrylanguage LIMIT 5;
```

**Expected Result:** The data in the `Percentage` column is now encrypted and completely illegible.

![Encrypted data shown as binary]

### Step 8: Decrypt the Data

The sensitive data is now encrypted and secured from prying eyes. However, you still need a way to access the encrypted data when needed.

To decrypt, use the `AES_DECRYPT` command with the same key:

```sql
SELECT CAST(AES_DECRYPT(Percentage, @key_str) AS CHAR(255)) 
FROM countrylanguage;
```

**Note:** Since AES is symmetric, the same key is used for both encryption and decryption.

![Decrypted data output]

---

## Practice Exercise: Control Access to MySQL Databases and Their Objects

### Scenario

You will modify privileges of the user `db_owner` (created in Exercise 1) such that this user cannot **INSERT**, **UPDATE**, or **DELETE** any column of the `country` table in the `world` database.

<details>
<summary>💡 Hint</summary>

1. Navigate to User accounts > Edit privileges for db_owner
2. Select the world database
3. Go to Table sub-tab
4. Select the `country` table
5. Under Table-specific privileges, uncheck INSERT, UPDATE, and DELETE
6. Keep SELECT checked (read-only access)
7. Click Go to save changes

</details>

<details>
<summary>✅ Solution</summary>

**Step-by-step instructions:**

1. Go to **Home** > **User accounts** tab
2. Click **Edit privileges** for the `db_owner` user
3. Under **Database** sub-tab, select the `world` database
4. Click **Go**
5. Switch to the **Table** sub-tab
6. Select the table `country` from the drop-down menu
7. Click **Go**
8. Under **Table-specific privileges**:
   - Uncheck **INSERT**
   - Uncheck **UPDATE**
   - Uncheck **DELETE**
   - Keep **SELECT** checked
9. Click **Go** to save changes

**Verification:**
The user `db_owner` can now only read data from the `country` table (SELECT) but cannot insert, update, or delete any rows.

</details>

---

## Lab Completion Checklist

| Task                                                | Completed |
| :-------------------------------------------------- | :-------- |
| **User Account Management**                   |           |
| Accessed phpMyAdmin                                 | ☐        |
| Navigated to User accounts tab                      | ☐        |
| Created new user account (db_owner)                 | ☐        |
| Granted appropriate privileges                      | ☐        |
| Verified user creation                              | ☐        |
| **Access Control**                            |           |
| Edited user privileges                              | ☐        |
| Selected world database                             | ☐        |
| Granted database-specific privileges                | ☐        |
| Configured table-specific privileges for city table | ☐        |
| Restricted UPDATE to only Population column         | ☐        |
| **Data Encryption**                           |           |
| Opened MySQL CLI                                    | ☐        |
| Hashed passphrase with SHA2                         | ☐        |
| Connected to world database                         | ☐        |
| Viewed countrylanguage table                        | ☐        |
| Modified column to varbinary(255)                   | ☐        |
| Encrypted Percentage column with AES_ENCRYPT        | ☐        |
| Verified encryption worked                          | ☐        |
| Decrypted data with AES_DECRYPT                     | ☐        |
| **Practice Exercise**                         |           |
| Modified db_owner privileges for country table      | ☐        |
| Restricted INSERT, UPDATE, DELETE                   | ☐        |

---

## Screenshot Checklist

| Screenshot        | File Name                       | Description                                          |
| :---------------- | :------------------------------ | :--------------------------------------------------- |
| User Creation     | `MySQL_User_Creation.png`     | New user account creation screen                     |
| Table Privileges  | `MySQL_Table_Privileges.png`  | Table-specific privileges configuration              |
| Encryption Before | `MySQL_Encryption_Before.png` | countrylanguage table before encryption              |
| Encryption After  | `MySQL_Encryption_After.png`  | countrylanguage table after encryption (binary data) |
| Decryption        | `MySQL_Decryption.png`        | Decrypted data output                                |

---

## Troubleshooting Tips

| Issue                                 | Solution                                                                |
| :------------------------------------ | :---------------------------------------------------------------------- |
| **Cannot edit user privileges** | Ensure you are logged in as a MySQL administrator (root user)           |
| **Encryption returns NULL**     | Verify the column was properly converted to varbinary before encryption |
| **Decryption returns NULL**     | Ensure you are using the exact same passphrase and hash length          |
| **Permission denied**           | Check that the user has appropriate privileges for the database/table   |
| **AES functions not available** | Verify MySQL version supports encryption functions (5.6+)               |

---

## Common MySQL Commands Summary

| Command                                           | Purpose                                   |
| :------------------------------------------------ | :---------------------------------------- |
| `SET @var = value`                              | Assign a value to a user-defined variable |
| `SHA2('string', length)`                        | Hash a string using SHA-2 algorithm       |
| `USE database;`                                 | Select a database to work with            |
| `SELECT * FROM table;`                          | Retrieve all rows from a table            |
| `ALTER TABLE table MODIFY COLUMN col datatype;` | Change a column's data type               |
| `UPDATE table SET col = value;`                 | Update data in a table                    |
| `AES_ENCRYPT(data, key)`                        | Encrypt data using AES                    |
| `AES_DECRYPT(data, key)`                        | Decrypt AES-encrypted data                |
| `CAST(value AS datatype)`                       | Convert a value to a specified data type  |

---

## Key Takeaways

| Concept                             | Description                                                                     |
| :---------------------------------- | :------------------------------------------------------------------------------ |
| **Least Privilege Principle** | Grant users only the privileges they need to perform their job functions        |
| **Privilege Levels**          | MySQL supports global, database, table, and column-level privileges             |
| **Symmetric Encryption**      | AES uses the same key for encryption and decryption                             |
| **Key Security**              | Never store encryption keys or passphrases in plaintext; hash them instead      |
| **Data Type Conversion**      | Encrypted data must be stored in binary-compatible data types (varbinary, blob) |
| **SHA-2 Hashing**             | Provides 224, 256, 384, or 512-bit hash outputs for passphrase security         |

---

## Summary

In this hands-on lab, you have:

| Activity                                                       | Completed |
| :------------------------------------------------------------- | :-------- |
| Created a MySQL user account with appropriate privileges       | ✓        |
| Granted database-specific and table-specific privileges        | ✓        |
| Restricted UPDATE access to a specific column only             | ✓        |
| Hashed a passphrase using SHA-2 for key security               | ✓        |
| Encrypted a sensitive data column using AES_ENCRYPT            | ✓        |
| Verified encryption by viewing binary data                     | ✓        |
| Decrypted data using AES_DECRYPT with the same key             | ✓        |
| Modified user privileges for INSERT, UPDATE, DELETE operations | ✓        |

---

## Congratulations!

You have successfully completed the **MySQL User Access Control and Data Encryption** lab. You now know how to:

- Create and manage MySQL user accounts using phpMyAdmin
- Grant database-specific and table-specific privileges
- Restrict access at the column level
- Implement AES encryption to secure sensitive data
- Hash passphrases using SHA-2 for key security
- Encrypt and decrypt data using symmetric encryption

These skills are essential for database administration, securing sensitive information, and implementing the principle of least privilege in production database environments.

---


*Last updated: January 2026*


