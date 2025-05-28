
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

## 2. Relational Database Fundamentals
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

## 3. Basic SQL Commands

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


## 4. Advanced SQL Queries


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


### Step-by-Step Query Explaination

- **Step 1** : Creating *"ranked_desc"* table which orders the images in desending order of their quality score hence we will use it for taking positive samples.
- **Step 2** : Creating *"ranked_asce"* table which orders the images in ascending order of their quality score hence we will use it for taking negative samples.
- **Step 3** : creating *"positive_samples"* table from *"ranked_desc"*  which is taking each thired record starting from 1
- **Step 4** :creating *"negative_samples"* table from *"ranked_asce"*  which is taking each thired record starting from 1
- **Step 5** :simple combining the results of both *"positive_samples"* and *"nagative_samples"* table
  
