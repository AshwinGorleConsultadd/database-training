
# SQL Training - Database Fundamentals

Welcome to your SQL training journey! This guide offers a gentle introduction to core database concepts, focusing on relational databases, their structure, and design principles. Whether you're a curious beginner or brushing up your skills, this README will help you get a solid foundation.
#  1. Introduction to Databases



### a) History and Evolution of Databases
Pre-1960s: Data was managed manually or with simple file systems, lacking structure and control.

1960s(File based DB) : data was being stored in flat file system which laks in structure.

1960s–1970s (Hierarchical & Network): Early database models organized data in tree or graph structures but were rigid and complex.

1970s–2000s (Relational): The relational model introduced structured tables and SQL, becoming the standard for decades.

1980s–1990s (Object-Oriented): Object-oriented and object-relational databases aimed to integrate with programming objects but saw limited use.

2000s–Present (NoSQL): NoSQL databases emerged to handle big data and scale flexibly without fixed schemas.

Present (Cloud & Serverless): Modern databases are cloud-native, highly scalable, and support real-time, multi-model data access.

### b) Types of Databases: Relational vs. Non-relational
- **Relational Databases (SQL)**: Store data in structured tables with predefined schemas. Examples include PostgreSQL, MySQL, and Oracle. Ideal for transactions and structured data with relationships.
- **Non-relational Databases (NoSQL)**: Designed for flexibility and scalability. They store data in formats like key-value pairs, documents, or graphs. Examples include MongoDB, Redis, and Cassandra. Great for handling big data, unstructured content, and rapid development.

### c) Database Management Systems (DBMS) Overview
A DBMS is software that manages databases. It provides tools for data storage, retrieval, update, and administration. Key functions include query processing, security, backup, concurrency control, and data integrity. Popular DBMSs include MySQL, PostgreSQL, Microsoft SQL Serverand MongoDB.

### d) SQL vs. NoSQL Databases
- **SQL (Structured Query Language)** databases use fixed schemas and are optimized for complex queries and transactional consistency (ACID compliance).
- **NoSQL** databases offer more flexibility with dynamic schemas, allowing fast performance and easy scaling, especially for unstructured or distributed data systems. Each has its strengths depending on the application requirements.

# 2. Relational Database Fundamentals
Database design is the process of structuring a database to efficiently store, manage, and retrieve data. 

### a) Database Design Concepts
Database design is the process of structuring a database to efficiently store, manage, and retrieve data. It involves following 
- defining tables and relationships
- defining keys (primary, candidate, foreign and composite keys)
- Adding Constraints to ensure data integrity (NOT NULL, CHECK, UNIQUE)
- Normalization (1NF, 2NF, 3NF, BCNF etc)
- Denormalization (done in order to improve performance)
- Defining cardinality and participation constraints

### b) Entity-relationship Model
The ER model is a diagrammatic approach used to design and visualize a database's structure 
Key Components:

**Entities**: Real-world objects or concepts represented as rectangles (Ex: Student, Course).

- ***Strong Entity***: Exists independently (Ex: Student).
- ***Weak Entity:*** Depends on another entity (Ex: Instalments can not exists without Loan).

**Attributes:** Properties or details of entities shown as ovals (Ex: Name, Age).
Simple (Atomic): Cannot be divided (Ex: Age).
- ***Composite:*** Can be divided into smaller parts.
- ***Derived:*** Computed from other attributes (Ex: Age from DOB).
- ***Multivalued***: Can have multiple values.
- ***Primary Key Attribute :*** it is Unique identifier of an entity, underlined in the ER diagram.

**Relationships:** Associations between entities shown as diamonds.

- **Unary**: Relationship within the same entity.
- **Binary**: Between two entities (Ex: Student enrolls in Course).


**Cardinality:** Specifies the number of instances involved in relation:
- One-to-One (1:1): Each entity instance relates to one other.
- One-to-Many (1:N): One entity relates to many others.
- Many-to-Many (M:N): Many instances on both sides.

**Participation:**
- Total Participation: Entity must be involved in the relationship (double line).
- Partial Participation: Entity may or may not be involved (single line).
**Generalization, Specialization, Aggregation:**
- Generalization: Combining similar entities into a general one.
- Specialization: Breaking an entity into sub-entities.
- Aggregation: A relationship treated as an entity for higher abstraction.

# 3. Basic SQL Commands

**a) Data Definition Language (DDL)**
DDL commands are used to define and manage the structure of database objects like tables and schemas.

- CREATE:Creates a new table, database, or other object.
  CREATE TABLE students (id INT, name VARCHAR(50));

- ALTER: Modifies an existing database object ( add or remove columns).
  Ex: ALTER TABLE students ADD email VARCHAR(100);
- DROP: Deletes a table or database permanently. Ex:
  DROP TABLE students;

**b) Data Manipulation Language (DML)**
DML commands are used to manipulate data within tables.

- SELECT: Retrieves data from one or more tables.
  Ex: SELECT * FROM students;
- INSERT: Adds new records to a table.
  Ex: INSERT INTO students (id, name) VALUES (1, 'John');
- UPDATE: Modifies existing records in a table.
  Ex: UPDATE students SET name = 'Jane' WHERE id = 1;
- DELETE: Removes records from a table.
  Ex: DELETE FROM students WHERE id = 1;

 **c) Data Control Language (DCL)**
DCL commands manage permissions and access to database objects.

- GRANT: Gives a user access privileges.
  Ex: GRANT SELECT ON students TO user1;
- REVOKE: Removes access privileges from a user.
  Ex: REVOKE SELECT ON students FROM user1;

**d) Transaction Control Language (TCL)**
TCL commands manage transactions to ensure data integrity.

- BEGIN: Starts a new transaction.
- COMMIT: Saves all changes made in the current transaction.
- ROLLBACK: Undoes changes made in the current transaction.


# 4. Advanced SQL Queries


**a) Join** : Joins combine rows from two or more tables based on a common column.

- **Inner Join**: Returns only matching rows from both tables on which we are applying the join.  
  Ex: SELECT * FROM A INNER JOIN B ON A.id = B.id;

- **Left Outer Join**: Returns all rows from the left table, and matched rows from the right table.  
  Ex: SELECT * FROM A LEFT JOIN B ON A.id = B.id;

- **Right Outer Join**: Returns all rows from the right table, and matched rows from the left.  
  Ex: SELECT * FROM A RIGHT JOIN B ON A.id = B.id;

- **Full Outer Join**: Returns all rows from both tables, with NULLs where we are geting  no match.  
  Ex: SELECT * FROM A FULL OUTER JOIN B ON A.id = B.id;

- **Cross Join**: Returns the Cartesian product — all combinations of two tables.  
  Ex: SELECT * FROM A CROSS JOIN B

**b) Subqueries and Correlated Subqueries**  
Subqueries one quert nested inside another query.

- **Subquery**: Executes once and returns results to the main query.  
  Ex: SELECT name FROM students WHERE id IN (SELECT student_id FROM results WHERE mark > 80)

- **Correlated Subquery**: Executes for each row of the outer query, using values from it.  
  Ex: SELECT name, salary FROM employees e WHERE salary > ( SELECT AVG(salary) FROM employees )


**c) Set Operations**  
Set operations help us to combine results from multiple queries.

- **UNION**: Combines results and removes duplicates or the records exists in both table taken only ones.  
  Ex: SELECT name FROM A UNION SELECT name FROM B

- **INTERSECT**: Returns only rows common to both queries.  
  Ex: SELECT name FROM A INTERSECT SELECT name FROM B;

- **EXCEPT**: Returns rows from the first query not present in the second.  
  Ex: SELECT name FROM A EXCEPT SELECT name FROM B;

**d) Window Functions**  
Window functions perform calculations across a set of table rows related to the current row.

- **ROW_NUMBER()**: Assigns a unique number to each row.
- **RANK()**: Assigns a rank with possible gaps for ties.
- **DENSE_RANK()**: Assigns rank without gaps for ties.
- **NTILE(n)**: Divides result set into n roughly equal parts.
- **LAG()**: Returns value from the previous row.
- **LEAD()**: Returns value from the next row.

Ex:  
negative_samples AS (
    SELECT image_id, 0 AS weak_label
    FROM ranked_asc
    WHERE rn % 3 = 1
    LIMIT 10000
)
SELECT image_id, weak_label
FROM (
    SELECT * FROM positive_samples
    UNION ALL
    SELECT * FROM negative_samples
) AS combined
ORDER BY image_id;

**e) Common Table Expressions (CTEs)**  
CTEs helps us to simplify complex queries and improve readability of the query.

- **CTE**: it is a temporary result set used within the main query.  
  Ex:  
  WITH top_students AS (  
    SELECT name, mark FROM students WHERE mark > 90  
  )  
  SELECT * FROM top_students;

- **Recursive CTE**: Used to query hierarchical data like org charts , employee hierarchy and tree like structure.  
  Ex:  
  WITH RECURSIVE subordinates AS (

  SELECT id, name, manager_id
  FROM employees
  WHERE id = 1

  UNION ALL

  SELECT e.id, e.name, e.manager_id
  FROM employees e
  JOIN subordinates s ON e.manager_id = s.id
  )
  
  SELECT * FROM subordinates;



**f) Pivoting and Unpivoting Data**  
Transform data between rows and columns.

- **Pivoting**: Converts row data into columns — useful for summaries or reports or better visualization of the data.

Ex: we have this order table which represents item ordered int which months along with quantity 
| product | month | sales |
|---------|-------|-------|
| Pen     | Jan   | 100   |
| Pen     | Feb   | 120   |
| Pencil  | Jan   | 90    |
| Pencil  | Feb   | 95    |

Now this is the table ***after Pivoting*** which is giving us better understanding of how many quantity of product is sold in each month and can also compare two defferent product sale in each month.

| product | Jan | Feb |
|---------|-----|-----|
| Pen     | 100 | 120 |
| Pencil  | 90  | 95  |

**Pivote Query**

    SELECT
    product,
    SUM(CASE WHEN month = 'Jan' THEN sales ELSE 0 END) AS Jan,
    SUM(CASE WHEN month = 'Feb' THEN sales ELSE 0 END) AS Feb
    FROM sales_data
    GROUP BY product;


  

- **Unpivoting**: Converts columns back into rows. used to normalize wide tables, Exactly reverse of pivoting.  
**Un-Pivoting Query**

        SELECT 
        product,
        'Jan' AS month, 
        Jan AS sales
        FROM monthly_sales
        
        UNION ALL
        
        SELECT product,
        'Feb' AS month, 
        Feb AS sales 
        FROM monthly_sales;

  


#5. Database Design and Optimization

### a) Indexing
- **Clustered Index**

 - Physically orders the rows in the table based on the index key.
- There can be only one clustered index per table.
- The actual table data is stored in the same order as the clustered index.
- Faster for range queries and sorting on the indexed column.
- Ex. CREATE CLUSTERED INDEX idx_id ON users(id);

- **Non-Clustered Index**

- it creates a separate structure from the actual table data.
- Stores pointers (row references) to the data rows.
- we can have multiple non clustered indexes on a table.
- CREATE NONCLUSTERED INDEX idx_email ON users(email);

- **Covering Index**
- A non-clustered index that includes all columns a query needs, so the database doesn’t have to look up the main table.
- This makes reads faster because everything is already in the index.
- CREATE NONCLUSTERED INDEX idx_cover ON orders(order_id, customer_id, order_date);

### b) Key Query Optimization Techniques:
**i) Using Proper Indexes :** 
- we should make index on the cloumn frequently used in WHERE, GROUP BY and ORDER BY etc.
- The right index can reduce full table scans and make SELECT, JOIN, and WHERE much faster.


**ii) Avoid over SELECT** :  We should only select the needed columns

**iii) Filter Early :** Filtering data before join make query faster and efficient

**iv) Using JOIN Efficiently :**

- Should prefer INNER JOIN over OUTER JOIN if you don’t need unmatched - rows.
- Make sure JOINs using indexed keys.

**v) Limit the Result Set:** we should use LIMIT in order to avoiding over fetching of data than needed.

**vi) Using EXISTS Instead of IN**

**vii) Analyze and Use Execution Plans**

### c) Explain Plan
An Explain Plan shows how the database will execute a SQL query step by step.

- Which indexes are used?
- Which tables are scanned?
- How many rows are expected to be read?
- In what order will joins happen?
- Ex: EXPLAIN SELECT * FROM users WHERE email = 'abc@example.com';


### d) Partitioning and Sharding

| Feature            | Partitioning                                   | Sharding                                       |
|--------------------|------------------------------------------------|------------------------------------------------|
| Scope              | Within a single database                       | Across multiple databases or servers           |
| Purpose            | Improve query performance and manageability    | Enable scalability and handle huge data loads  |
| Data Location      | Same machine / DB instance                     | Different machines / DB instances              |
| Managed By         | Usually handled by the database engine         | You or your infrastructure team                |
| Use Case           | Moderate to large datasets                     | Very large, distributed systems                |


**What is Partitioning**? :Partitioning splits a large table into smaller parts called partitions, all within the same database.

#### Types of Partitioning:
- Range – Ex: based on a date column

        CREATE TABLE user_logs (
            id SERIAL PRIMARY KEY,
            user_id INT,
            action TEXT,
            log_date DATE
        ) PARTITION BY RANGE (log_date);

        CREATE TABLE user_logs_2023 PARTITION OF user_logs
        FOR VALUES FROM ('2023-01-01') TO ('2024-01-01');

- List – Ex: based on country code

            CREATE TABLE customers (
                customer_id SERIAL PRIMARY KEY,
                name TEXT,
                country_code TEXT
            ) PARTITION BY LIST (country_code);

            CREATE TABLE customers_us PARTITION OF customers
            FOR VALUES IN ('US');


- Hash – Ex: based on a hash of user_id


*Benefits:*
- Faster queries by scanning only relevant partitions
- Easier data management (Ex: dropping old partitions)
- All partitions still act like one logical table

**What is Sharding?** : Sharding splits data across multiple databases or servers. Each shard stores a portion of the data.

*Benefits:*
- Scales horizontally by adding more machines
- Spreads load and improves performance
- Ideal for extremely large datasets




**Partitioning and Sharding Strategies**

| Strategy               | Use When                                            |
|------------------------|-----------------------------------------------------|
| Range Partitioning     | Data splits naturally by time, price, or age        |
| List Partitioning      | Data splits by known values like country or type    |
| Hash Partitioning      | We want even distribution with no natural range    |
| Horizontal Sharding    | We split rows (Ex: by user ID) across databases  |
| Vertical Sharding      | We split columns into different databases          |


###e) Concurrency Control and Isolation Levels

**What is Concurrency Control?**  
Concurrency control ensures that multiple transactions can access the database simultaneously without conflicting or corrupting data.
It maintains:
- Correctness
- Performance
- Consistency

**What are Isolation Levels?**  
Isolation levels define how visible one transaction’s work is to others.

| Isolation Level    | Dirty Read | Non-Repeatable Read | Phantom Read |
|--------------------|------------|----------------------|--------------|
| Read Uncommitted   | ✅ Yes     | ✅ Yes               | ✅ Yes       |
| Read Committed     | ❌ No      | ✅ Yes               | ✅ Yes       |
| Repeatable Read    | ❌ No      | ❌ No                | ✅ Yes       |
| Serializable       | ❌ No      | ❌ No                | ❌ No        |

---

#### 1. **Read Uncommitted**
- Can read uncommitted (dirty) data from other transactions.
- Unsafe, rarely used.

#### 2. **Read Committed**
- Only sees committed data.
- Prevents dirty reads, but **non-repeatable reads** and **phantoms** are possible.
- Default in PostgreSQL and Oracle.

#### 3. **Repeatable Read**
- Data read once won’t change during the transaction.
- Prevents dirty and non-repeatable reads.
- **Phantom reads** can still occur.
- Default in MySQL (InnoDB).

#### 4. **Serializable**
- Strictest level.
- Transactions behave as if they ran one after another.
- Prevents all anomalies (dirty, non-repeatable, phantom).
- Slowest due to locking or blocking.

**Terminology Explained**

| Phenomenon         | Description                                                 |
|--------------------|-------------------------------------------------------------|
| Dirty Read         | Read data not yet committed by another transaction          |
| Non-repeatable Read| A row returns different values when read twice              |
| Phantom Read       | A query returns new rows when re-executed during transaction|



### f) Deadlocks and How to Handle Them

**What is a Deadlock?**  
A deadlock occurs when two or more transactions block each other by holding a lock the other needs. As a result, none of the transactions can proceed — they are stuck waiting for each other.

**Example Scenario:**
- Transaction A locks `Table 1` and wants `Table 2`
- Transaction B locks `Table 2` and wants `Table 1`
- Both wait forever → **Deadlock**



**How to Detect Deadlocks?**
- Most modern databases (PostgreSQL, MySQL, SQL Server) automatically detect deadlocks.
- When detected, one transaction is usually **aborted** so the other can continue.



**How to Handle or Prevent Deadlocks?**

- Always Access Tables in the Same Order

-  Keep Transactions Short and Fast

-  Use Lower Isolation Levels (when safe)

-  Add Explicit Lock Timeouts


