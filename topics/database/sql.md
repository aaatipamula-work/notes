# SQL

## Overview 

[SQL](https://en.wikipedia.org/wiki/SQL) or Structured Query Language a language used to communicate with [relational database management systems](https://en.wikipedia.org/wiki/Relational_database_management_system) (RDBMS). Like the name suggests it is particularly good at handling structured data. In addition to querying data, SQL also supports modifying data, and modifying the structure of RDBMSes. It is fairly easy to follow once the syntax is learnt.

## Resources 

I would suggest going through the following lessons to get a decent understanding of SQL and its use:

- [Khan Academy](https://www.khanacademy.org/computing/computer-programming/sql) 
  - [SQL Basics](https://www.khanacademy.org/computing/computer-programming/sql#sql-basics)
  - [More Advanced SQL Queries](https://www.khanacademy.org/computing/computer-programming/sql#more-advanced-sql-queries)
  - [Relational Queries](https://www.khanacademy.org/computing/computer-programming/sql#modifying-databases-with-sql)
- [W3 Schools Tutorials](https://www.w3schools.com/sql/default.asp)
  - This has an extensive list of pretty much every SQL feature you might use.
  - *It is mostly useful when you just want a short document that goes over a feature or topic*.

## Reference

- [W3 Schools Reference](https://www.w3schools.com/sql/sql_ref_keywords.asp)
  - Great for checking if you're using something correctly.
  - Has a pretty extensive list of everything you might ever use in SQL.

## Concepts 

### Normalization

**Coming Soon**

### View

A [View](https://en.wikipedia.org/wiki/View_(SQL)) is akin to a "virtual table" in an RDBMS. Instead of creating an entirely new table to store to disk a Views are usually defined to do one of the following: 

- Only expose a smaller subset of data out of an entire table
- Join and [de-normalize](#normalization) a set of tables
- Virtually partitioning a table into different subsections

Views are much lighter to store as the only data stored is the definition of the view. They also don't have to be updated any time a related table is updated. 

Views can be created with the following syntax:

```sql
CREATE VIEW my_view AS
SELECT col1, col3, col5 ...
FROM my_table
WHERE col3 > 10
```

Any querying conditionals, aggregates etc. can be added to create the needed view.

## Syntax

**Coming Soon**

## Databases

### MSSQL (Microsoft SQL Server)

[MSSQL](https://en.wikipedia.org/wiki/Microsoft_SQL_Server) or Microsoft SQL Server.

*MSSQL* uses a superset of SQL called [T-SQL](https://www.simplilearn.com/tutorials/sql-tutorial/transact-sql) or Transact SQL.

Being a superset of SQL it functions similarly at its core and anything you've already learned about SQL should apply. The only statement I've found that does not work is the `LIMIT` statement.

> I suggest downloading [SSMS](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16) or SQL Server Management Studio to interact with databases.
