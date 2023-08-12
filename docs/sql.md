# SQL Basics

SQL (Structured Query Language) is a language designed to allow both technical and non-technical users query, manipulate, and transform data from a relational database. And due to its simplicity, SQL databases provide safe and scalable storage for millions of websites and mobile applications.  

Often times, in order for us to build the most function website we can, we depend on a **database** to store information.  Databases often are set up as tables with information in columns and rows (e.g. Excel Spreadsheets & Google Sheets).  

**Quick Links**  

* [SQL Cheat Sheets](https://www.sqltutorial.org/sql-cheat-sheet/)  

* [Free SQL Course](https://sqlbolt.com)  

* [SQL for Dummies (PDF)](https://cdn.nickplatt.dev/files/Docs/SQL-for-Dummies-A.-Taylor.pdf)  

* [Additional SQL Reference Material](https://www.w3schools.com/sql/)  

For the following examples we will be using sqlite3, which is a SQL command line program, on the [CS50 IDE](https://ide.cs50.io/).  We will also be using the following [.csv file](https://cdn.nickplatt.dev/files/Docs/Movies.csv) which contains a database with data about some of Pixar's classic movies.  Let's import this into the IDE.  First drag and drop the file into the left side of the IDE, preferably a folder.  Next, let's run the following commands:
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

| Operator                | Condition                                            | SQL Example                           |
|-------------------------|------------------------------------------------------|---------------------------------------|
| =, !=, <, <=, >, >=     | Standard numerical operators                         | col_name **!**= 4                     |
| BETWEEN ... AND ...     | Number is within a range of two values (inclusive)   | col_name **BETWEEN** 1.5 **AND** 10.5 |
| NOT BETWEEN ... AND ... | Number is not within range of two values (inclusive) | col_name **NOT BETWEEN** 1 AND 10     |
| IN (...)                | Number exists in a list                              | col_name **IN** (2, 4, 6)             |
| NOT IN (...)            | Number does not exist in a list                      | col_name **NOT IN** (1, 3, 5)         |

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

When Writing `WHERE` clauses with columns containing text data, SQL supports a number of useful operators to do things like case-insensitive string comparison and wildcard pattern matching.  Below are a few common text-data specific operators:  

| Operator     | Condition                                                                                             | SQL Example                                                            |
|--------------|-------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| =            | Case sensitive exact string comparison (**notice the single equals**)                                 | col_name **=** "abc"                                                  |
| != or <>     | Case sensitive exact string inequality comparison                                                     | col_name **!=** "abcd"                                                 |
| LIKE         | Case insensitive exact string comparison                                                              | col_name **LIKE** "ABC"                                                |
| NOT LIKE     | Case insensitive exact string inequality comparison                                                   | col_name **NOT LIKE** "ABCD"                                           |
| %            | Used anywhere in a string to match a sequence of zero or more characters (only with LIKE or NOT LIKE) | col_name **LIKE** "%AT%" (matches "AT", "ATTIC", "CAT" or even "BATS") |
| _            | Used anywhere in a string to match a single character (only with LIKE or NOT LIKE)                    | col_name **LIKE** "AN_" (matches "AND" but not "AN")                   |
| IN (...)     | String exists in a list                                                                               | col_name **IN** ("A", "B", "C")                                        |
| NOT IN (...) | String does not exist in a list                                                                       | col_name **NOT IN** ("D", "E", "F")                                    |  

??? tip "String Quotes"
	All strings must be quoted so that the query parser can distinguish words in the string from SQL keywords.  

We should not that while most database implementations are quite efficient when using these operators, full-text search is best left to dedicated libraries like [Apache Lucene](http://lucene.apache.org/) or [Sphinx](http://sphinxsearch.com/).  These libraries are designed specifically to do full text search, and as a result are more efficient and can support a wider variety of search features including internationalization and advanced queries.  

Now let's test these operators using the same .csv from above:

1. Find all the Toy Story movies:
```sql
SELECT title, director FROM movies WHERE title LIKE "Toy Story%";
```
2. Find all the movies directed by John Lasseter:
```sql
SELECT title, director FROM movies WHERE director LIKE "John Lasseter";
```
3. Find all the movies (and director) not directed by John Lasseter:
```sql
SELECT title, director FROM movies WHERE director NOT LIKE "John Lasseter";
```
4. Find all the WALL-* movies:
```sql
SELECT title FROM movies WHERE title LIKE "WALL-_";
```

## Filtering and Sorting Query Results
Even though the data in a database may be unique, the results of any particular query may not be - take our Movies table for example, many different movies can be released the same year.  In such cases, SQL provides a convenient way to discard rows that have a duplicate column value by using the **`DISTINCT`** keyword.  
```sql
SELECT DISTINCT column, another_column, ...
FROM mytable
WHERE condition(s);
```
Since the **`DISTINCT`** keyword will blindly remove duplicate values, we will learn in a future lesson how to discard duplicated based on specific columns using grouping and the **`GROUP BY`** cluase.  

### Ordering Results
Unlike our neatly ordered table in the last few lessons, most data in real databases are added in no particular column order.  As a result, it can be difficult to read through and understand the results of a query as the size of a table increases to thousands or even millions of rows.  

To help with this, SQL provides a way to sort your results by a given column in ascending or descending order using the **`ORDER BY`** clause:
```sql
SELECT column, another_column, ...
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC;
```
When an **`ORDER BY`** clause is specified, each row is sorted alpha-numerically based on the specified column's value.  In some databases, you can also specify a collation to better sort data containing international text.  

### Limiting Results to a Subset
Another clause which is commonly used with the **`ORDER BY`** clause are the **`LIMIT`** and **`OFFSET`** clauses, which are a useful optimization to indicate to the database the subset of the results you care about.  

The **`LIMIT`** will reduce the number of rows to return, and the optional **`OFFSET`** will specify where to begin counting the number rows from:
```sql
SELECT column, another_column, ...
FROM mytable
WHERE condition(s)
ORDER BY column ASC/DESC
LIMIT num_limit OFFSET num_offset;
```
If you think about websites like Reddit or Pinterest, the front page is a list of links sorted by popularity and time, and each subsequent page can be represented by sets of links at different offsets in the database.  Using these clauses, the database can then execute queries faster and more efficiently by processing and returning only the requested content.  

??? tip "Order of Execution"
	**`LIMIT`** and **`OFFSET`** are applied relative to the other parts of a query, generally done last after other clauses have been aplied.  

Now let's do some exercises using the previous .csv used above:

1. List all directors of Pixar movies (alphabetically), without duplicates:
```sql
SELECT DISTINCT director FROM movies ORDER BY director ASC;
```
2. List the last four Pixar movies released (ordered from most recent to last):
```sql
SELECT title FROM movies ORDER BY year DESC LIMIT 4;
```
3. List the first 5 Pixar movies sorted alphabetically:
```sql
SELECT title FROM movies ORDER BY title ASC LIMIT 5;
```
4. List the next 5 Pixar movies sorted alphabetically:
```sql
SELECT title FROM movies ORDER BY title ASC LIMIT 5 OFFSET 5;
```

## Review Exercises
Let's take a new [.csv file](https://cdn.nickplatt.dev/files/Docs/Cities.csv) containing a few of the most populous cities in North America and do some review exercises from what has been learned above:

1. List all the Canadian cities and their populations:
```sql
SELECT city, population FROM north_american_cities WHERE country = "Canada";
```
2. Order all the cities in the United States by their latitude from north to south:
```sql
SELECT city, latitude FROM north_american_cities WHERE country = "United States" ORDER BY latitude DESC;
```
3. List all the cities west of Chicago, ordered from west to east:
```sql
SELECT city, longitude FROM north_american_cities WHERE longitude < -87.629798 ORDER BY longitude ASC;
```
4. List the two largest cities in Mexico (by population):
```sql
SELECT city, population FROM north_american_cities WHERE country = "Mexico" ORDER BY population DESC LIMIT 2;
```
5. List the third and fourth largest cities (by population) in the United States and their population:
```sql
SELECT city, population FROM north_american_cities WHERE country = "United States" ORDER BY population DESC LIMIT 2 OFFSET 2; 
```