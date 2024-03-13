# Creating-SQL-Temporary-Tables
Temporary tables in SQL provide a valuable tool for managing and manipulating data within a database session without the need for permanent storage. They serve various purposes such as data pre-processing, staging, and filtering subsets of data.


Creating SQL Temporary Tables
Type text or HTML
<!-- wp:paragraph -->
<p>Temporary tables in SQL provide a valuable tool for managing and manipulating data within a database session without the need for permanent storage. They serve various purposes such as data pre-processing, staging, and filtering subsets of data.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading" id="h-what-are-temporary-tables"><strong>What are Temporary Tables?</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>Temporary tables, as the name suggests, are temporary storage structures that exist only for the duration of a database session. They are automatically deleted when the session ends. Here's a quick recap of what you need to know about temporary tables:</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><!-- wp:list-item -->
<li><strong>Automatic Deletion</strong>: Temporary tables are automatically removed from the database when the session ends, making them suitable for short-term data manipulation tasks.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><strong>Data Pre-processing</strong>: They serve as a holding area for storing intermediate results during complex calculations, enhancing the efficiency of data processing.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><strong>Data Staging</strong>: Temporary tables can collect results from multiple queries, facilitating subsequent analysis or data merging operations.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><strong>Filtered Subset Storage</strong>: They can store filtered subsets of data, eliminating the need to repeatedly select and filter data for analysis, thereby streamlining data retrieval processes.</li>
<!-- /wp:list-item --></ol>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>Now, let's explore various methods to create temporary tables, focusing on techniques applicable to BigQuery.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>Temporary Table Creation in BigQuery</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>In BigQuery, temporary tables can be created using the <code>WITH</code> clause. The syntax for creating a temporary table with the <code>WITH</code> clause is as follows:</p>
<!-- /wp:paragraph -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>WITH
    new_table_data AS (
        SELECT *
        FROM Existing_table
        WHERE Tripduration &gt;= 60
    )</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Let's break down this query:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li>The statement begins with the <code>WITH</code> clause followed by the name of the new temporary table (<code>new_table_data</code> in this example).</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>The <code>AS</code> clause indicates that the subsequent query result will be stored in the temporary table.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>The subquery within the parentheses filters the data from an existing table (<code>Existing_table</code>).</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>Once executed, the filtered data will be stored in the temporary table <code>new_table_data</code>, allowing subsequent queries to be run on this filtered dataset.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p><strong>Creating a Temporary Table in BigQuery:</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Consider a scenario where we want to create a temporary table named <code>high_sales</code> containing sales records where the sales amount is greater than $1000:</p>
<!-- /wp:paragraph -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>WITH
    high_sales AS (
        SELECT *
        FROM Sales
        WHERE Amount &gt; 1000
    )</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>In this example, <code>Sales</code> is the existing table containing sales records, and <code>Amount</code> is the column representing sales amount.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>Temporary Table Creation in Other Databases</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>While the <code>WITH</code> clause is specific to BigQuery, other databases such as SQL Server and MySQL offer alternative methods for creating temporary tables. One common approach is using the <code>SELECT INTO</code> syntax:</p>
<!-- /wp:paragraph -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>SELECT *
INTO AfricaSales
FROM GlobalSales
WHERE Region = &quot;Africa&quot;</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>In this example, <code>GlobalSales</code> is the existing table containing global sales records, and we are selecting records for the African region and storing them in a temporary table named <code>AfricaSales</code>.</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>User-Managed Temporary Table Creation</strong></h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>In addition to database-managed temporary tables, users can create and manage temporary tables using the <code>CREATE TABLE</code> statement. After completing the analysis, users can drop these tables using the <code>DROP TABLE</code> clause.</p>
<!-- /wp:paragraph -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>CREATE TEMP TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
    ...
)</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p><strong>Creating a User-Managed Temporary Table</strong>:</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>Suppose we want to create a temporary table named <code>employee_data</code> to store employee information for analysis:</p>
<!-- /wp:paragraph -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>CREATE TEMP TABLE employee_data (
    employee_id INT,
    employee_name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10,2)
)</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Once the analysis is complete, the temporary table <code>employee_data</code> can be dropped using the following command:</p>
<!-- /wp:paragraph -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>DROP TABLE employee_data</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:heading -->
<h2 class="wp-block-heading">Practice these Examples for understanding the Temporary Tables</h2>
<!-- /wp:heading -->

<!-- wp:heading {"level":3} -->
<h3 class="wp-block-heading"><strong>Example 1: Creating Temporary Tables with the WITH Clause in BigQuery</strong></h3>
<!-- /wp:heading -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 1.1: Filtering and Storing Specific Data
WITH high_sales AS (
    SELECT *
    FROM Sales
    WHERE Amount &gt; 1000
)</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>WITH high_sales AS (</code>: This line starts the common table expression (CTE) named <code>high_sales</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>SELECT *</code>: It selects all columns from the <code>Sales</code> table.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>FROM Sales</code>: It specifies the source table as <code>Sales</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>WHERE Amount &gt; 1000)</code>: It filters the data, selecting only records where the amount is greater than $1000.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 1.2: Calculating Aggregated Metrics
WITH monthly_revenue AS (
    SELECT EXTRACT(MONTH FROM OrderDate) AS Month, SUM(Amount) AS TotalRevenue
    FROM Orders
    GROUP BY Month
)</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>WITH monthly_revenue AS (</code>: Begins a CTE named <code>monthly_revenue</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>SELECT EXTRACT(MONTH FROM OrderDate) AS Month</code>: Extracts the month from the <code>OrderDate</code> column and aliases it as <code>Month</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>SUM(Amount) AS TotalRevenue</code>: Calculates the total revenue.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>FROM Orders</code>: Specifies the source table as <code>Orders</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>GROUP BY Month)</code>: Groups the results by month.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3 class="wp-block-heading"><strong>Example 2: Creating Temporary Tables with SELECT INTO in SQL Server</strong></h3>
<!-- /wp:heading -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 2.1: Storing Data Based on Specific Conditions
SELECT *
INTO HighValueProducts
FROM Products
WHERE UnitPrice &gt; 100</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>SELECT *</code>: Selects all columns from the <code>Products</code> table.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>INTO HighValueProducts</code>: Creates a new table named <code>HighValueProducts</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>FROM Products</code>: Specifies the source table as <code>Products</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>WHERE UnitPrice &gt; 100</code>: Filters the data, selecting only records where the unit price is greater than $100.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 2.2: Copying Structure and Data from an Existing Table
SELECT *
INTO EmployeesBackup
FROM Employees</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>SELECT *</code>: Selects all columns from the <code>Employees</code> table.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>INTO EmployeesBackup</code>: Creates a new table named <code>EmployeesBackup</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>FROM Employees</code>: Specifies the source table as <code>Employees</code>.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3 class="wp-block-heading"><strong>Example 3: Creating User-Managed Temporary Tables in SQL Server</strong></h3>
<!-- /wp:heading -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 3.1: Defining Table Structure
CREATE TABLE #EmployeeData (
    EmployeeID INT,
    EmployeeName VARCHAR(50),
    Department VARCHAR(50),
    Salary DECIMAL(10,2)
)</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>CREATE TABLE #EmployeeData (</code>: Begins the creation of a temporary table named <code>#EmployeeData</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>EmployeeID INT, EmployeeName VARCHAR(50), Department VARCHAR(50), Salary DECIMAL(10,2)</code>: Specifies the columns and their data types.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 3.2: Populating Data into the Temporary Table
INSERT INTO #EmployeeData (EmployeeID, EmployeeName, Department, Salary)
VALUES (1, 'John Doe', 'IT', 60000.00),
       (2, 'Jane Smith', 'HR', 55000.00),
       (3, 'David Lee', 'Finance', 65000.00)</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>INSERT INTO #EmployeeData (EmployeeID, EmployeeName, Department, Salary)</code>: Specifies the columns to insert data into.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>VALUES</code>: Inserts multiple rows of data into the temporary table.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3 class="wp-block-heading"><strong>Example 4: Creating Temporary Tables in PostgreSQL</strong></h3>
<!-- /wp:heading -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 4.1: Storing Filtered Data
CREATE TEMP TABLE high_sales AS
SELECT *
FROM Sales
WHERE Amount &gt; 1000</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>CREATE TEMP TABLE high_sales AS</code>: Creates a temporary table named <code>high_sales</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>SELECT * FROM Sales WHERE Amount &gt; 1000</code>: Selects and filters records from the <code>Sales</code> table where the amount is greater than $1000.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 4.2: Creating a Temporary Table with Defined Structure
CREATE TEMP TABLE customer_info (
    customer_id INT,
    customer_name VARCHAR(100),
    email VARCHAR(255)
)</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>CREATE TEMP TABLE customer_info (</code>: Begins the creation of a temporary table named <code>customer_info</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>customer_id INT, customer_name VARCHAR(100), email VARCHAR(255)</code>: Specifies the columns and their data types.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3 class="wp-block-heading"><strong>Example 5: Creating Temporary Tables in MySQL</strong></h3>
<!-- /wp:heading -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 5.1: Storing Aggregated Data
CREATE TEMPORARY TABLE monthly_revenue
SELECT EXTRACT(MONTH FROM OrderDate) AS Month, SUM(Amount) AS TotalRevenue
FROM Orders
GROUP BY Month</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>CREATE TEMPORARY TABLE monthly_revenue</code>: Creates a temporary table named <code>monthly_revenue</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>SELECT EXTRACT(MONTH FROM OrderDate) AS Month, SUM(Amount) AS TotalRevenue FROM Orders GROUP BY Month</code>: Selects and aggregates revenue data by month from the <code>Orders</code> table.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:codemirror-blocks/code-block {"mode":"sql","mime":"text/x-sql"} -->
<div class="wp-block-codemirror-blocks-code-block code-block"><pre>-- Example 5.2: Copying Structure and Data from an Existing Table
CREATE TEMPORARY TABLE employee_backup
SELECT *
FROM Employees</pre></div>
<!-- /wp:codemirror-blocks/code-block -->

<!-- wp:paragraph -->
<p>Explanation:</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><!-- wp:list-item -->
<li><code>CREATE TEMPORARY TABLE employee_backup</code>: Creates a temporary table named <code>employee_backup</code>.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><code>SELECT * FROM Employees</code>: Selects all columns and data from the <code>Employees</code> table.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 class="wp-block-heading"><strong>Best Practices for Working with Temporary Tables</strong></h2>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><!-- wp:list-item -->
<li><strong>Global vs. Local Temporary Tables</strong>: Understand the distinction between global and local temporary tables. Local temporary tables are typically used for session-specific operations and are automatically deleted when the session ends.</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><strong>Dropping Temporary Tables After Use</strong>: It's good practice to drop temporary tables after use to release database resources and optimize performance, especially in scenarios involving heavy processing.</li>
<!-- /wp:list-item --></ol>
<!-- /wp:list -->

### Ref: <a href="http://www.deepdecide.com" target="_blank">deepdecide.com</a>
