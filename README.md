# udemy-data-engineering-basics
My notes I took from this course - https://www.udemy.com/course/basic-data-engineering-for-beginner-using-google-cloud-python

---
# Introduction to Data Engineering
## What is Data Engineering?
- Data Engineering:
  - All engineering & Operational tasks required to make data available for end-user (business user).
  - Data available for analytics, building data modelm reporting, etc.
- Hierarchy of Needs (Bottom of the Pyramid to top):
  - Collect: Instrumentation, logging, sensors, external data, user generated content
  - Move/Store: Reliable data flow, infrastructure, pipelines, ETL (extract-transform-load), structured & unstructured data storage.
  - Explore/transform: Cleaning, anomaly detection, preparation.
  - Aggregate/label: Analytics, metrics, segments, aggregates, features, training data.
  - Learn/Optimize: A/B Testing, experimentation, simple ML algorithms.
  - Learn/Optimize: AI, deep learning.
- Role & Responsibilities:
  - Machine Learning/AI engineer: Machine learning, AI algorithm
  - Data scientist/ data analyst: Reporting, analytics, data visualization
  - Data Engineer: Data storage & Processing (extract, transform, load)
  - Software Engineer: Transactional system
- Data Engineering Activities:
  - Ingest data from source(s)
  - Build & maintain data warehouse/data lake
  - Build & maintain data pipeline
  - Schedule & automate script/pipelines
  - Create specific tables for further analytics use case
  - Data migration to cloud
  - Debug data quiality issues
## Data Engineering Example:
- Sample Case:
  - Naturamics: marketplace for vegetables, fruits & other farm products
  - Build a product recommender
  - Based on historical data
- Solution:
  - Naturamics Data Scintists/data analysts and Machine Learning/AI engineers require training data for analytics/modelling/ML.
  - For this they need data from the Product table (views, avg rating, purchases per product) and User table (top products viewed & Purchased per user).
  - The historical data is generated in Naturamics model applicaiton in websites (developed by Software engineers) which consists of Browsing history, Purchase history and Product ratings.
  - Those data sources are recorded from user interaction to Naturamics market place and written by Software Engineers.
  - Data Engineer is at the center. They coordinate with software engineer to know tha data source, and with data scientist or ML engineer, to know what kind of data required to achieve the goal, which in this case is product and user table. 
  - Create and populate data for product and user tbale is data engineer responsibility.
  - Data Engineer only read existing data written by Software Engineer.
  - The data engineer task, is to move data, or to be exact,
    - extract data from source.
    - transform it using some aggregate function, like summing or averaging numeric values
    - then load it into another data store 
    - and logical format that more appropriately for achieveing the goal
  - This process is commonly known as ETL, extract-transform-load.
  - Data engineer can use SQL scripts, or code and framework, and flow or scheduling tools that are specifically designed to handle ETL tasks.
  - In this example, data engineer aggregate the data source into something like below:
    - Browser history is aggregated into *Product view per user* and *Total view per product*.
    - Purchase history is aggregated into *Product purchased per user* and *Total purchase per product*.
    - Product ratings is aggregated into *Average rating per product*.
  - Then these afregated data then, in this example, further transformed to achieve product and user table, required to train product recommender.
    - *Product view per user* and *Total purchase per product* are transformed into User table.
    - *Total view per product*, *Product purchased per user* and *Average rating per product* are transformed into Product table.
  - This is data engineer's task to create, and populate those tables. 
## What is Data Modelling?
- Data Model
  - Data abstraction/blueprint
    - Data fields
    - Relationships among data
  - Analogy: For the analogy, before we build a house, we must have some kind of blueprint. The blueprint containing the rooms and how the room connect each other. This blueprint in data field, is what we called as data model.
  - Final state: logical structure for database (Data model sometimes also referred as database model, the final state of data model is logical structure used for database.)
- Data Modelling:
  - Purpose: Data Modelling is the process to create data model, where we organize data into database system to ensure that your data is persisted and easily usable by users on organization.
  - Data should be persisted & easily usable.
  - Support business decisions
    - Market decision
    - Product (application) development
    - Risk assessment
- Data Modelling Steps:
  - Gather goals (What data outcome that business needs?)
  - Gather possible data sources (The data team need to make sure data availability, and completeness.)
  - Conceptual data modelling (mapping the concept of possible data, relationship, that we have, or will have.)
- Data Modelling Importance:
  - How our data is organized for our applications is extremely critical.
  - Organized data determines later data use (Without good data model, queries that could have been straightforward and simple might become complicated and slow.)
  - Data modelling should begin before writing application code, business logic, or analytical models
  - Data modelling might not a single step, but more an iterative process.
  - And data modelling most of the times rely on many people (This means, everyone involved on data analysis and usage should take parts during modelling.)
---
# Database
## What is Database?
- Database
  - Collection of related data.
  - How they are organized.
  - Analogy for big database: Think of database software as something like excel spreadsheet, but can contains millions, or billions of data, where each data can related to other data.
  - Analogy for big database: On the other hand, there might be very small database, like if you use a fitness tracker watch, the device also has database inside of it.
  - Database is everywhere: Most applications right now will somehow related to database, whether that is a simple text file, or dedicated database software.
- Database is Important
  - Important or most business.
  - Sample case: e-commerce
    - thousands of customers hit the website, and sell or buy items.
    - We need to know the exact transaction : who is the seller, who is the buyer, products, price, logistic, etc.
  - Sample case: healthcare research
    - company need to improve drugs effectiveness for a disease.
    - The researchers will need to find data from existing medicine, and previous research, like the chemical substance, effect on disease, exact measurement, et cetera.
    - Such data might be very large and detail.
  - Even system that look simple will need database.
    - For example, a fitness tracker watch will have internal database on the device, even if its very simple.
    - It stores your movement, heartbeat, or track GPS when you run.
    - Then later you can synchronize database from device, into your phone, which eventually send data into much larger database in cloud.
## Relational Database
- Relational Database
  - Digital database based on relational data model.
  - Collection of tables and their relationships.
    - Relational database model organizes data into one or more tables of columns and rows, with a unique value identifying each row.
    - Table is also called as relation.
    - Columns of the table are called attributes or fields.
    - Rows are also called records or tuples.
    - Generally each table represents one entity.
      - For example, we have table countries.
        - Each row represent one instance of that type of entity, such as "India" or "Japan", a single country.
        - Each column represents specific value attached to that instance, such as name, currency or national language.
    - A good table will have unique value for each row, in the previous example, something like country_id can be unique for each row, and no duplicate.
      - Such key is also knwon as primary key.
    - Table can have relationship to other table.
      - For example, each row of table cities can be related to table countries.
      - Each country can have multiple cities, or multiple rows in table cities.
        - For example, India has city Delhi and Kolkata. While Japan jas city Tokyo and Osaka.
      - So, the relationship between te countrues table and the cities table is "One to Many".
      - One country can have many cities.
      - To connect country with city, each row in cities has reference to owning country through column country_id.
      - This country_id in table cities is called as foreign key.
  - RDBMS: Relational Database Management System
  - Invented by Edgar Codd (IBM) in late 60s-early 70s.
  - Widely used even today.
- RDBMS Sample:
  - Open Source:
    - PostgreSQL
    - MySQL
  - Enterprise work:
    - Oracle
    - SQL Server
  - Lightweight simple task:
    - SQLite
- SQL
  - Language to interact with RDBMS
  - SQL: Structured Query Language
  - Mostly same syntax across RDBMS product
  - Minor difference (dialect)
  - Further categories: DDL, DML, DCL, TCL
- SQL Categories:
  - DDL: Data Definition Language
    - SQL that used to define or modify table structures. That is creating, dropping table, or modifying column definition. Also truncating table (deleting all rows on table), add comment to column definition, or rename column.
    ```
    CREATE
    DROP
    ALTER
    TRUNCATE
    COMMENT
    RENAME
    ```
  - DML: Data Manipulation Language
    - SQL statements to read data, insert new data to table, update existing data, delete particular data, or merge new data into existing data.
    ```
    SELECT
    INSERT
    UPDATE
    DELETE
    MERGE
    ...
    ```
  - DCL: Data Control Language
    - It is related with defining permission for accessing data. This can be grant permission or revoke permission for certain user, to certain tables.
    ```
    GRANT
    REVOKE
    ```
  - TCL: Transaction Control Language
    - is related with defining permission for accessing data. This can be grant permission or revoke permission for certain user, to certain tables. TCL or transaction control language is category to control transaction within database. Transaction is set of tasks that grouped into a single execution unit. Each transaction begins with a specific task and ends when all the tasks in the group successfully complete. If any of the tasks fail, the transaction fails. Therefore, a transaction has only two results: success or failed.
    ```
    COMMIT
    ROLLBACK
    SAVEPOINT
    ```
- Relational Database Benefits:
  - Widely ued, easier to learn.
  - Suitable for "small" volume.
  - Data schema is highly structured.
  - Relation between two tables (or more) [Ability to combining more than one table based on common key to get detailed information. This is something that unique to relational databases and makes it very powerful.]
  - Support aggregation & analytics [Aggregations is calculating single value from multiple inputs, like summing numbers, averaging, get maximum or minimum value, etc. This capability also includes grouping rows by multiple criterias.]
  - SQL query is flexible.
  - Multiple indexes.
  - Support ACID transactions for data integrity.
- When to Use Relational Database
  - All (most) benefits matches data characteristics.
  - Relational database machine
    - Typically centralized, on one machine
    - Better performance requires scaling up hardware (CPU, memory)
      - Vertical Scaling
- Database Index
  - The database index looks like a book index.
  - We have additional place on the database, which consists of the index.
  - In the database index, we have table and the column, used for the index.
  - Hence, if we find data by the indexed column, we can find the data fast.
  - Index is very helpful when your data is large.
  - Thousands of data rows might not need significant time to search, but hundred thousands, or millions of rows, without indexing, will be very slow search.
  - Each indexes are related to specific table and consist of one or more keys.
  - A table can have more than one index built from it.
  - The keys are basically based on table columns.
- Index & primary Key
  - Primary key is a unique value for each record, used to identify that particular record.
  - Primary key is always an index.
  - If Primary keys are sequential numbers with no particular business meaning, then they are called surrogate key.
  - If Primary keys have a business meaning to them (attributes to the entity), then they are called natural key.
  - So either we use surrogate or natural primary key, we automatically have one index for our table.
  - Just for information, we can have table without primary key at all, although it is generally a bad practice and should not be done.
- Be Wise on Index
  - Index speeds up search/find (read)
  - Book example
    - Insert, update, delete term need index maintenance
  - Database index
    - Speed up SELECT
    - Slowing down INSERT, UPDATE, DELETE
      - So, other than read operations, other operations are slowed down because of index maintenance.
      - So, be wise when using index.
    - Only index columns that are frequently read.
- ACID Data Integrity
  - Transaction
    - Set of tasks as single execution unit.
    - Success when all tasks in set were success.
    - Failed if one of task in set was failed.
    - So, there can be only two results in transaction, success or failed.
    - Grouping tasks into transaction, will gurantee data integrity and consistency.
  - Transaction Example
    - Payment Transaction
      - There will be four steps for this transaction:
        - Deduct money from our bank account.
        - Transfer money to merchant
        - Create ledger entry (debit)
        - Create ledger entry (credit)
      - Transaction is success only when all 4 tasks were a success.
      - Transaction is failed if one of the task was failed.
        - Take example,
          - when the 3rd task : debit ledger entry is failed. In this case, we must cancel money transfer, and return the amount into our bank account. Or in other words, we cancel the 2nd and 1st task.
          - On the other hand, since the 3rd task already failed, we must make sure that the 4th task,creating credit ledger entry, is never executed for this transaction.
        - All previous tasks must be cancelled (rollback) and unprocessed tasks must not be executed. 
        - If we do not rollback previous tasks, or still execute any individual task, it will break our data integrity.
        - This means, we will have unbalanced data.
    - In order to maintain transaction integrity, there are four properties that must be followed
      - They are ACID properties: atomicity, consistency, isolation, and durability.
  - ACID Properties
    - Atomicity: all changes to data are performed as if they are single operation.
      - That is, all the changes are performed, or none of them are.
      - The payment transaction example refers to only Atomicity. 
    - Consistency: data is consistent when transaction starts and when it ends.
      - In the payment example, the consistency ensures that the total value of funds in both the accounts is the same at the start and end of each transaction.
      - If we have 2000 in our bank account, and merchant has 5000 to their bank account, which sums is 7000.
      - Then we trigger payment transaction of 400, then at the end of transaction, the sum must still be 7000, although now we have 1600 in our bank account, and merchant has 5400.
    - Isolation: each transaction proceeds independently and securely.
      - Transaction x will not affect transaction y, or the other way around.
      - Whether transaction x is success or failed, its result will not impact transaction y.
      - In database, where we process rows, the database will has row locking mechanism, where certain row is locked by transaction x, and transaction y cannot process that particular row, while transaction x still acquire the row lock.
      - When transaction x has finished, the row lock will be released, and transaction y can process that row.
    - Durability: in successful transaction, data changes are saved into database, even in the event of a system failure.
      - For example, soon after a transaction succeed, the electricity is suddenly down.
      - Then this property must make sure that data modified by transaction, is saved in database.
      - So when electricity is back to normal, we have the same exact data in database, that previously modified by transaction.
## When Not To Use Relational Database?
- When Not To Use