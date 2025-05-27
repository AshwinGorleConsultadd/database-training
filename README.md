
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

## 2 Relational Database Fundamentals
Database design is the process of structuring a database to efficiently store, manage, and retrieve data. 

## a) Database Design Concepts
Database design is the process of structuring a database to efficiently store, manage, and retrieve data. It involves following 
- defining tables and relationships
- defining keys (primary, candidate, foreign and composite keys)
- Adding Constraints to ensure data integrity (NOT NULL, CHECK, UNIQUE)
- Normalization (1NF, 2NF, 3NF, BCNF etc)
- Denormalization (done in order to improve performance)
- Defining cardinality and participation constraints

## b) Entity-relationship Model
The ER model is a diagrammatic approach used to design and visualize a database's structure 
Key Components:

**Entities**: Real-world objects or concepts represented as rectangles (e.g., Student, Course).
***Strong Entity***: Exists independently (e.g., Student).
***Weak Entity:*** Depends on another entity (e.g., Payment with no unique ID without Student).

**Attributes:** Properties or details of entities shown as ovals (e.g., Name, Age).
Simple (Atomic): Cannot be divided (e.g., Age).
***Composite:*** Can be divided into smaller parts.
***Derived:*** Computed from other attributes (e.g., Age from DOB).
***Multivalued***: Can have multiple values.
***Primary Key (Key Attribute):*** it is Unique identifier of an entity, underlined in the ER diagram.

**Relationships:** Associations between entities shown as diamonds.

- Unary: Relationship within the same entity.
- Binary: Between two entities (e.g., Student enrolls in Course).


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

## 3 Basic SQL Commands

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

