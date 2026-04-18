![alt text](../Screenshots/datasette-logo.png)


# Lab: COUNT, DISTINCT, and LIMIT — Querying the San Francisco Film Locations Database

**Estimated time:** 35 minutes

---

## Learning Objectives

After completing this lab you'll be able to use three essential SQL expressions to query and analyze data. You'll also be able to demonstrate the skills needed to use an open-source data exploration tool, Datasette, to perform these tasks.

| Objective | Description |
|:----------|:------------|
| **COUNT** | Retrieve the number of rows that match a query criteria |
| **DISTINCT** | Remove duplicate values from a result set and return only unique values |
| **LIMIT** | Restrict the number of rows retrieved from a table |

---

## Tools Needed

**Datasette**, a no-charge open-source multi-tool for exploring and publishing data, accessible through your web browser.

**Database:** San Francisco Film Locations dataset (Public Domain Dedication and License)

---

## Exploring the Database

Before you begin your SQL query lab tasks, let's explore the SanFranciscoFilmLocations database.

### Step 1: Run the Initial Query

1. If the first statement listed below is not already in the Datasette textbox, copy the code below by clicking on the copy button and then paste it into the textbox of the Datasette tool using `Ctrl+V` or right-click and choose **Paste**

```sql
SELECT * FROM FilmLocations;
```

2. Click **Submit Query**

3. Scroll down the table and explore all the columns and rows of the `FilmLocations` table to get an overall idea of the data

### Column Attribute Descriptions

| Column | Description |
|:-------|:------------|
| **Title** | Titles of the films |
| **ReleaseYear** | Time of public release of the films |
| **Locations** | Locations of San Francisco where the films were shot |
| **FunFacts** | Funny facts about the filming locations |
| **ProductionCompany** | Companies who produced the films |
| **Distributor** | Companies who distributed the films |
| **Director** | People who directed the films |
| **Writer** | People who wrote the films |
| **Actor1** | Person 1 who acted in the films |
| **Actor2** | Person 2 who acted in the films |
| **Actor3** | Person 3 who acted in the films |

![FilmLocations table preview]

![alt text](<../../Simple SELECT Statements/Screenshots/FilmLocations table preview.png>)

---

## Exercise 1: COUNT

In this exercise, you will use the `COUNT` aggregate function to retrieve the number of rows that match specific query criteria.

### Step 1: Count All Rows in the Table

**Problem:** Retrieve the number of rows from the "FilmLocations" table.

**Solution:**
```sql
SELECT COUNT(*) FROM FilmLocations;
```

1. Copy the solution code above
2. Paste it into the Datasette textbox
3. Click **Submit Query**

**Expected Output:**
```
COUNT(*)
--------
[total number of rows in the table]
```

![COUNT all rows result]

![alt text](<../Screenshots/Count with WHERE Clause.png>)

![alt text](<../Screenshots/COUNT all rows result.gif>)

### Step 2: Count with WHERE Clause

**Problem:** Retrieve the number of locations of the films which are written by James Cameron.

**Solution:**
```sql
SELECT COUNT(Locations) FROM FilmLocations WHERE Writer="James Cameron";
```

1. Copy the solution code above
2. Paste it into the Datasette textbox
3. Click **Submit Query**

**Expected Output:**
```
COUNT(Locations)
----------------
[number of locations for James Cameron films]
```

![COUNT with WHERE clause result]

![alt text](<../Screenshots/Count with WHERE Clause.jpg>)

![alt text](<../Screenshots/COUNT with WHERE clause result.gif>)

### Step 3: Practice Exercises on COUNT

Now, let's practice creating and running some COUNT related queries.

---

#### Problem 3.1

**Problem:** Retrieve the number of locations of the films which are directed by Woody Allen.

<details>
<summary>💡 Hint</summary>

Use the `COUNT()` function with a `WHERE` clause filtering on the `Director` column.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT COUNT(Locations) FROM FilmLocations WHERE Director="Woody Allen";
```
</details>

<details>
<summary>📤 Output</summary>

```
COUNT(Locations)
----------------
[number of locations for Woody Allen films]
```
</details>

![alt text](<../Screenshots/Retrieve the number of locations of the films which are directed by Woody Allen.png>)

![alt text](<../Screenshots/Solution 3.1.gif>)

---

#### Problem 3.2

**Problem:** Retrieve the number of films shot at Russian Hill.

<details>
<summary>💡 Hint</summary>

Use `COUNT(*)` with a `WHERE` clause filtering on the `Locations` column.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT COUNT(*) FROM FilmLocations WHERE Locations="Russian Hill";
```
</details>

<details>
<summary>📤 Output</summary>

```
COUNT(*)
--------
[number of films shot at Russian Hill]
```
</details>

![alt text](<../Screenshots/Retrieve the number of films shot at Russian Hill.png>)


![alt text](<../Screenshots/Solution 3.2.gif>)

---

#### Problem 3.3

**Problem:** Retrieve the number of rows having a release year older than 1950 from the "FilmLocations" table.

<details>
<summary>💡 Hint</summary>

Use `COUNT(*)` with a `WHERE` clause using the `<` operator on the `ReleaseYear` column.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT COUNT(*) FROM FilmLocations WHERE ReleaseYear < 1950;
```
</details>

<details>
<summary>📤 Output</summary>

```
COUNT(*)
--------
[number of films released before 1950]
```
</details>


![alt text](<../Screenshots/Retrieve the number of rows having a release year older than 1950 from the (FilmLocations) table.png>)

![alt text](<../Screenshots/Solution 3.3.gif>)

---

### Step 4: Take Screenshot

1. Take a screenshot showing one of your COUNT queries and its result
2. Save the file as `SQL_COUNT_Query.png`

---

## Exercise 2: DISTINCT

In this exercise, you will use `DISTINCT` to remove duplicate values from result sets and return only unique values.

### Step 1: Retrieve Unique Film Titles

**Problem:** Retrieve the name of all films without any repeated titles.

**Solution:**
```sql
SELECT DISTINCT Title FROM FilmLocations;
```

1. Copy the solution code above
2. Paste it into the Datasette textbox
3. Click **Submit Query**

**Expected Output:**
```
Title
-----
[unique film titles, no duplicates]
```

![DISTINCT titles result]

![alt text](<../Screenshots/DISTINCT titles result.png>)


![alt text](<../Screenshots/DISTINCT titles result.gif>)


### Step 2: COUNT DISTINCT with WHERE Clause

**Problem:** Retrieve the number of release years of the films distinctly, produced by Warner Bros. Pictures.

**Solution:**
```sql
SELECT COUNT(DISTINCT ReleaseYear) FROM FilmLocations WHERE ProductionCompany="Warner Bros. Pictures";
```

1. Copy the solution code above
2. Paste it into the Datasette textbox
3. Click **Submit Query**

**Expected Output:**
```
COUNT(DISTINCT ReleaseYear)
---------------------------
[number of distinct release years for Warner Bros films]
```

![COUNT DISTINCT result]

### Step 3: Practice Exercises on DISTINCT

Now, let's practice creating and running some DISTINCT related queries.

---

#### Problem 3.1

**Problem:** Retrieve the name of all unique films released in the 21st century and onwards, along with their release years.

<details>
<summary>💡 Hint</summary>

Use `SELECT DISTINCT` with the `Title` and `ReleaseYear` columns, and a `WHERE` clause for `ReleaseYear >= 2000`.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT DISTINCT Title, ReleaseYear FROM FilmLocations WHERE ReleaseYear >= 2000;
```
</details>

<details>
<summary>📤 Output</summary>

```
Title                    | ReleaseYear
-------------------------|------------
[unique film titles]     | [year]
```
</details>

---

#### Problem 3.2

**Problem:** Retrieve the names of all the directors and their distinct films shot at City Hall.

<details>
<summary>💡 Hint</summary>

Use `SELECT DISTINCT` with `Director` and `Title`, and filter `Locations = "City Hall"`.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT DISTINCT Director, Title FROM FilmLocations WHERE Locations="City Hall";
```
</details>

<details>
<summary>📤 Output</summary>

```
Director     | Title
-------------|-------------------
[director]   | [film title]
```
</details>

---

#### Problem 3.3

**Problem:** Retrieve the number of distributors distinctly who distributed films acted by Clint Eastwood as 1st actor.

<details>
<summary>💡 Hint</summary>

Use `COUNT(DISTINCT Distributor)` with a `WHERE` clause filtering `Actor1 = "Clint Eastwood"`.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT COUNT(DISTINCT Distributor) FROM FilmLocations WHERE Actor1="Clint Eastwood";
```
</details>

<details>
<summary>📤 Output</summary>

```
COUNT(DISTINCT Distributor)
---------------------------
[number of distinct distributors]
```
</details>

---

### Step 4: Take Screenshot

1. Take a screenshot showing one of your DISTINCT queries and its result
2. Save the file as `SQL_DISTINCT_Query.png`

---

## Exercise 3: LIMIT

In this exercise, you will use `LIMIT` to restrict the number of rows retrieved from a table.

### Step 1: Retrieve First 25 Rows

**Problem:** Retrieve the first 25 rows from the "FilmLocations" table.

**Solution:**
```sql
SELECT * FROM FilmLocations LIMIT 25;
```

1. Copy the solution code above
2. Paste it into the Datasette textbox
3. Click **Submit Query**

**Expected Output:**
```
[First 25 rows of the table]
```

![LIMIT 25 result]

### Step 2: LIMIT with OFFSET

**Problem:** Retrieve the first 15 rows from the "FilmLocations" table starting from row 11.

**Solution:**
```sql
SELECT * FROM FilmLocations LIMIT 15 OFFSET 10;
```

1. Copy the solution code above
2. Paste it into the Datasette textbox
3. Click **Submit Query**

**Expected Output:**
```
[Rows 11 through 25 of the table]
```

![LIMIT with OFFSET result]

### Step 3: Practice Exercises on LIMIT

Now, let's practice creating and running some LIMIT related queries.

---

#### Problem 3.1

**Problem:** Retrieve the name of first 50 films distinctly.

<details>
<summary>💡 Hint</summary>

Use `SELECT DISTINCT Title` with `LIMIT 50`.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT DISTINCT Title FROM FilmLocations LIMIT 50;
```
</details>

<details>
<summary>📤 Output</summary>

```
Title
-----
[first 50 unique film titles]
```
</details>

---

#### Problem 3.2

**Problem:** Retrieve first 10 film names distinctly released in 2015.

<details>
<summary>💡 Hint</summary>

Use `SELECT DISTINCT Title` with `WHERE ReleaseYear = 2015` and `LIMIT 10`.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT DISTINCT Title FROM FilmLocations WHERE ReleaseYear = 2015 LIMIT 10;
```
</details>

<details>
<summary>📤 Output</summary>

```
Title
-----
[first 10 unique film titles from 2015]
```
</details>

---

#### Problem 3.3

**Problem:** Retrieve the next 3 film names distinctly after first 5 films released in 2015.

<details>
<summary>💡 Hint</summary>

Use `SELECT DISTINCT Title` with `WHERE ReleaseYear = 2015`, `LIMIT 3`, and `OFFSET 5`.
</details>

<details>
<summary>✅ Solution</summary>

```sql
SELECT DISTINCT Title FROM FilmLocations WHERE ReleaseYear = 2015 LIMIT 3 OFFSET 5;
```
</details>

<details>
<summary>📤 Output</summary>

```
Title
-----
[films 6-8 from the 2015 results]
```
</details>

---

### Step 4: Take Screenshot

1. Take a screenshot showing one of your LIMIT queries and its result
2. Save the file as `SQL_LIMIT_Query.png`

---

## Lab Completion Checklist

| Task | Completed |
|:-----|:----------|
| Explored the FilmLocations table with `SELECT *` | ☐ |
| Used `COUNT(*)` to count all rows | ☐ |
| Used `COUNT()` with WHERE clause | ☐ |
| Solved COUNT practice exercises (3 problems) | ☐ |
| Used `DISTINCT` to remove duplicate titles | ☐ |
| Used `COUNT(DISTINCT)` with WHERE clause | ☐ |
| Solved DISTINCT practice exercises (3 problems) | ☐ |
| Used `LIMIT` to retrieve first 25 rows | ☐ |
| Used `LIMIT` with `OFFSET` | ☐ |
| Solved LIMIT practice exercises (3 problems) | ☐ |
| Took screenshot of COUNT query | ☐ |
| Took screenshot of DISTINCT query | ☐ |
| Took screenshot of LIMIT query | ☐ |

---

## Screenshot Checklist

| Screenshot | File Name | Description |
|:-----------|:----------|:------------|
| COUNT Query | `SQL_COUNT_Query.png` | COUNT query with result showing row count |
| DISTINCT Query | `SQL_DISTINCT_Query.png` | DISTINCT query showing unique values |
| LIMIT Query | `SQL_LIMIT_Query.png` | LIMIT query showing restricted rows |

---

## Troubleshooting Tips

| Issue | Solution |
|:------|:---------|
| **Query returns no results** | Check for typos in column names or string values (SQL is case-sensitive for string comparisons) |
| **COUNT returns unexpected number** | Remember `COUNT(*)` counts all rows; `COUNT(column)` counts non-null values only |
| **DISTINCT not removing duplicates** | Ensure you're using `SELECT DISTINCT` not just `SELECT` |
| **LIMIT not working** | Some SQL dialects use `LIMIT` while others use `TOP` or `ROWNUM` — Datasette uses `LIMIT` |
| **String comparison fails** | Use double quotes for string literals in Datasette: `WHERE Writer="James Cameron"` |

---

## Common SQL Filters and Operators

| Operator/Function | Purpose | Example |
|:------------------|:--------|:--------|
| `COUNT(*)` | Count all rows | `SELECT COUNT(*) FROM table` |
| `COUNT(column)` | Count non-null values | `SELECT COUNT(Locations) FROM table` |
| `COUNT(DISTINCT column)` | Count unique values | `SELECT COUNT(DISTINCT Title) FROM table` |
| `DISTINCT` | Remove duplicates | `SELECT DISTINCT Title FROM table` |
| `LIMIT n` | Return first n rows | `SELECT * FROM table LIMIT 10` |
| `OFFSET n` | Skip first n rows | `SELECT * FROM table LIMIT 10 OFFSET 5` |
| `WHERE` | Filter rows | `WHERE ReleaseYear > 2000` |
| `=` | Equality | `WHERE Director="Woody Allen"` |
| `<` | Less than | `WHERE ReleaseYear < 1950` |
| `>` | Greater than | `WHERE ReleaseYear > 2010` |
| `AND` | Combine conditions | `WHERE Year > 2000 AND Year < 2010` |

---

## Key Takeaways

| Concept | Description |
|:--------|:------------|
| **COUNT(*)** | Returns the total number of rows in a table or result set |
| **COUNT(column)** | Returns the number of non-null values in a specific column |
| **COUNT(DISTINCT column)** | Returns the number of unique values in a column |
| **DISTINCT** | Removes duplicate rows from the result set |
| **LIMIT** | Restricts the number of rows returned by a query |
| **OFFSET** | Skips a specified number of rows before starting to return results |
| **WHERE clause** | Filters rows before applying COUNT, DISTINCT, or LIMIT |

---

## Summary

In this hands-on lab, you have:

| Activity | Completed |
|:---------|:----------|
| Explored the FilmLocations database using Datasette | ✓ |
| Used `COUNT(*)` to count all rows in a table | ✓ |
| Used `COUNT(column)` with WHERE clause to filter results | ✓ |
| Solved COUNT practice exercises | ✓ |
| Used `DISTINCT` to remove duplicate values from result sets | ✓ |
| Used `COUNT(DISTINCT column)` to count unique values | ✓ |
| Solved DISTINCT practice exercises | ✓ |
| Used `LIMIT` to restrict number of rows retrieved | ✓ |
| Used `LIMIT` with `OFFSET` to skip rows | ✓ |
| Solved LIMIT practice exercises | ✓ |
| Took screenshots of each query type for documentation | ✓ |

---

## Congratulations!

You have successfully completed the **COUNT, DISTINCT, and LIMIT — Querying the San Francisco Film Locations Database** lab. You now know how to:

- Use `COUNT()` to retrieve the number of rows matching query criteria
- Use `DISTINCT` to eliminate duplicate values from result sets
- Use `LIMIT` with and without `OFFSET` to restrict the number of rows retrieved
- Combine these expressions with `WHERE` clauses for precise data filtering
- Write SQL queries to analyze and summarize database content

These skills are essential for data analysis, database reporting, and working with large datasets where you need to understand data distribution, identify unique values, and paginate results.



---

*Last updated: April 2026*
