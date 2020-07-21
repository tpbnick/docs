# SQL Basics

SQL (Structured Query Language) is a language designed to allow both technical and non-technical users query, manipulate, and transform data from a relational database. And due to its simplicity, SQL databases provide safe and scalable storage for millions of websites and mobile applications.  

Often times, in order for us to build the most function website we can, we depend on a **database** to store information.  Databases often are set up as tables with information in columns and rows (e.g. Excel Spreadsheets & Google Sheets).  

**Quick Links**  

* [SQL Cheat Sheets](https://www.sqltutorial.org/sql-cheat-sheet/)  

* [Free SQL Course](https://sqlbolt.com)  

* [SQL for Dummies (PDF)](https://nicklyss.com/wp-content/uploads/2020/07/SQL-for-Dummies-A.-Taylor.pdf)  

For the following examples we will be using sqlite3, which is a SQL command line program, on the [CS50 IDE](https://ide.cs50.io/).  We will also be using the following [.csv file](https://nicklyss.com/wp-content/uploads/2020/07/Movies.csv) which contains a database with data about some of Pixar's classic movies.  Let's import this into the IDE.  First drag and drop the file into the left side of the IDE, preferably a folder.  Next, let's run the following commands:
```
sqlite3 movies.db
```
This creates a new database called `'movies'`.  
```
.mode csv
```
This changes mode of the program to be able to read .csv files.
```
.import "Movies.csv" movies
```
This imports the Movies.csv file into a table called "movies".  We should now be able to see and interact with the data inside our database.  

## `SELECT` Queries 101
To retrieve data from a SQL database, we need to write `SELECT` statements, which are often colloquially refered to as *queries*.  A query itself is just a statement which declares what data we are looking for, where to find it in the database, and optionally, how to transform it before it is returned.  

We can think of a table in SQL as a type of entity (i.e. dogs) and each row in that table as a specific *instance* of that type (i.e. pug, beagle, border collie, etc.).  This means that the columns would then represent the common properties shared by all instances of that entity (i.e. color of fur, length of tail, etc.).  

And given a table of data, the most basic query we could write would be one that selects for a couple columns (properties) of the table with all the rows (instances),  
```sql
SELECT column, another_column, ...
FROM mytable;
```
The result of this query will be a two-dimensional set of rows and columns, effectively a copy of the table, but only with the columns that we requested.  

If we want to retrieve all the columns of data from a table, we can then use the asterisk (`*`) shorthand in place of listing all the column names individually.  
```sql
SELECT *
from mytable;
```
This query, in particular, is really useful because it's a simple way to inspect a table by dumping all the data at once.  

Now, lets begin using the .csv file from above for some exercises:

1. Find the `title` of each film:
```sql
SELECT title FROM movies;
```  
2. Find the `director` of each film:
```sql
SELECT director FROM movies;
```
3. Find the `title` and `director` of each film:
```sql
SELECT title, director FROM movies;
```
4. Find the `title` and `year` of each film:
```sql
SELECT title, year FROM movies;
```
5. Find **all** information about each film:
```sql
SELECT * FROM movies;
```

## Queries with Constraints
Now we know how to select for specific columns of data from a table, but if you had a table with a hundred million rows of data, reading through all the rows would be inefficient and perhaps even impossible.  

In order to filter certain results from being returned, we need to use a `WHERE` clause in the query.  The clause is applied to each row of data by checking specific column values to determine whether it should be included in the results or not.

```sql
SELECT column, another_column, ...
FROM mytable
WHERE condition
	AND/OR another_condition
	AND/OR ...;
```
More complex clauses can be constructed by joining numerous `AND` or `OR` logical keywords (i.e. num_wheels >= 4 AND doors <= 2).  Below are some useful operators that you can use for numerical data (i.e. integer or floating point):

| Operator                | Condition                                            | SQL Example                   |
|-------------------------|------------------------------------------------------|-------------------------------|
| =, !=, <, <=, >, >=     | Standard numerical operators                         | col_name != 4                 |
| BETWEEN ... AND ...     | Number is within a range of two values (inclusive)   | col_name BETWEEN 1.5 AND 10.5 |
| NOT BETWEEN ... AND ... | Number is not within range of two values (inclusive) | col_name NOT BETWEEN 1 AND 10 |
| IN (...)                | Number exists in a list                              | col_name IN (2, 4, 6)         |
| NOT IN (...)            | Number does not exist in a list                      | col_name NOT IN (1, 3, 5)     |

In addition to making the results more manageable to understand, writing clauses to constrain the set of rows returned also allows the query to run faster due to the reduction in unnecessary data being returned.  

??? tip "SQL Syntax"	
	As you may have noticed by now, SQL doesn't *require* you to write the keywords all capitalized, but as convention, it helps people distinguish SQL keywords from column and table names, and makes the query code easier to read.  

Now let's do some exercises using the same .csv from above:

1. Find the movie with a row `id` of `6`:
```sql
SELECT id, title FROM movies WHERE id = 6;
```
2. Find the movies released in the `year`s between 2000 and 2010:
```sql
SELECT title, year FROM movies WHERE year BETWEEN 2000 AND 2010;
```
3. Find the movies **not** released in the `year`s between 2000 and 2010:
```sql
SELECT title, year FROM movies WHERE year NOT BETWEEN 2000 AND 2010;
```
4. Find the first 5 Pizar movies and their release `year`:
```sql
SELECT title, year FROM movies WHERE year <= 2003;
```