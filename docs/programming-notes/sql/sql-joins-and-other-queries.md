# SQL `Joins` and Other Query Types

## Multi-Table queries with `JOIN`s

Up to now, we've been working with a single table, but entity data in the real
world is often broken down into pieces and stored across multiple orthogonal
tables using a process known as _normalization_.

### Database Normalization

Tables that share information about a single entity need to have a _primary key_
that identifies that entity _uniquely_ across the database. One common primary
key type is an auto-incrementing integer (because they are space efficient), but
it can also be a string, hashed value, so long as it is unique.

Using the **`JOIN`** clause in a query, we can combine row data across two
separate tables using this unique key. The first of the joins that we will
introduce is the **`INNER JOIN`**.

```sql
SELECT column, another_table_column, ...
FROM mytable
INNER JOIN another_table
	ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, ... ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

The **`INNER JOIN`** is a process that matches rows from the first table and the
second table which have the same key (as defined by the **`ON`** constraint) to
create a result row with the combined columns from both tables. After the tables
are joined, the other clauses we learned previously are then applied.

??? tip "`JOIN` vs. `INNER JOIN`"

    You may see queries where the `INNER JOIN` is
    written simply as a `JOIN`. These two are equivalent, but we will continue to
    refer to these joins as inner-joins because they make the query easier to read
    once you start using other types of joins.

Let's do some exercises where we look at multiple tables. We will use the
[Movies.csv](https://cdn.nickplatt.dev/Docs/Movies.csv) file from previous
examples and a new [Boxoffice.csv](https://cdn.nickplatt.dev/Docs/Boxoffice.csv)
file with additional movie information.

1. Find the domestic and international sales for each movie:

```sql
SELECT title, domestic_sales, international_sales
FROM movies
	JOIN boxoffice
		ON movies.id = boxoffice.movie_id;
```

2. Show the sales numbers for each movie that did better internationally rather
   than domestically:

```sql
SELECT title, domestic_sales, international_sales
FROM movies
	JOIN boxoffice
		ON movies.id = boxoffice.movie_id
WHERE international_sales > domestic_sales;
```

3. List all the movies by their ratings in descending order:

```sql
SELECT title, rating
FROM movies
	JOIN boxoffice
		on movies.id = boxoffice.movie_id
ORDER BY rating DESC;
```

### Outer Joins

Depending on how you want to analyze the data, the `INNER JOIN` might not be
sufficient because the resulting table only contains data that belongs in both
of the tables.

If the two tables have asymmetric data, which can easily happen when data is
entered in different stages, then we would have to use a `LEFT JOIN`,
`RIGHT JOIN`, or `FULL JOIN` instead to ensure that the data you need is not
left out of the results.

```sql
SELECT column, another_column, ...
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table
	ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, ... ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

Like the `INNER JOIN` these three new joins have to specify which column to join
the data on.

When joining table A to table B, a `LEFT JOIN` simply includes rows from A
regardless of whether a matching row is found in B. the `RIGHT JOIN` is the
same, but reversed, keeping rows in B regardless of whether a match is found in
A. Finally, a `FULL JOIN` simply means that rows from both tables are kept,
regardless of whether a matching row exists in the other table.

When using any of these new joins, you will likely have to write additional
logic to deal with `NULL`s in the result and constraints.

??? tip "JOINS"

    You might see queries with these joins written as
    `LEFT OUTER JOIN`, `RIGHT OUTER JOIN`, or `FULL OUTER JOIN`, but the `OUTER`
    keyword is really kept for SQL-92 compatibility and these queries are simply
    equivalent to `LEFT JOIN`, `RIGHT JOIN`, and `FULL JOIN` respectively.

For the following exercises we will be using new tables. We will use a table
which stores fictional data about
[**Employees**](https://cdn.nickplatt.dev/Docs/Employees.csv) in the film studio
and their assigned office
[**Buildings**](https://cdn.nickplatt.dev/Docs/Buildings.csv). Some of the
buildings are new, so they don't have any employees in them yet, but we need to
find some information about them regardless.

1. Find the list of all buildings that have employees:

```sql
SELECT DISTINCT building FROM employees;
```

2. Find the list of all buildings and their capacity:

```sql
SELECT building_name, capacity FROM buildings;
```

3. List all buildings and the distinct employee roles in each building
   (including empty buildings):

```sql
SELECT DISTINCT building_name, role
FROM buildings
	LEFT JOIN employees
		on building_name = building;
```

### A short note on `NULL`s

It's always good to reduce the possibility of `NULL` values in databases because
they require special attention when constructing queries, constraints (certain
functions behave differently with null values) and when processing the results.

An alternative to `NULL` values in your database is to have **data-type
appropriate default values**, like 0 for numerical data, empty strings for text
data, etc. But if your database needs to store incomplete data, then `NULL`
values can be appropriate if the default values will skew later analysics (for
example, when taking averages of numerical data).

Sometimes, it's also not possible to avoid `NULL` values, as we saw in the last
lesson when outer-joining two tables with asymmetric data. In these cases, you
can test a column for `NULL` values in a `WHERE` clause by using either the
`IS NULL` or `IS NOT NULL` constraint.

```sql
SELECT column, another_column, ...
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
AND/OR ...;
```

For the following exercises, we will be using the same
[**Employees**](https://cdn.nickplatt.dev/Docs/Employees.csv) and
[**Buildings**](https://cdn.nickplatt.dev/Docs/Buildings.csv) tables from the
last exercises.

1. Find the name and role of all employees who have not been assigned to a
   building:

```sql
SELECT name, role
FROM employees
WHERE building IS NULL;
```

2. Find the names of the buildings that hold no employees:

```sql
SELECT DISTINCT building_name
FROM buildings
	LEFT JOIN employees
		ON building_name = building
WHERE role IS NULL;
```

### Queries with Expressions

In addition to querying and referencing raw column data with SQL, you can also
use _expressions_ to write more complex logic on column calues in a query. These
expressions can use mathematical and string functions along with basic
arithmetic to transform values when the query is executed, as shown in this
physics example:

```sql
SELECT particle_speed / 2.0 AS half_particle_speed
FROM physics_data
WHERE ABS(particle_position) * 10.0 > 500;
```

Each database has its own supported set of mathematical, string, and date
functions that can be used in a query, which you can find in their own
respective docs.

The use of expressions can save time and extra post-processing of the result
data, but can also make the query harder to read, so we recommend that when
expressions are used in the `SELECT` part of the query, that they are also given
a descriptive _alias_ using the `AS` keyword.

```sql
SELECT col_expression AS expr_description, ...
FROM mytable;
```

In addition to expressions, regular columns and even tables can also have
aliases to make them easier to reference in the output and as a part of
simplifying more complex queries.

```sql
SELECT column AS better_column_name, ...
FROM a_long_widgets_table_name AS mywidgets
INNER JOIN widget_sales
	ON mywidgets.id = widgets_sales.widget_id;
```

We are now going to use expressions to transform the `BoxOffice` data into
something easier to understand for the tasks below. We will use the
[Movies.csv](https://cdn.nickplatt.dev/Docs/Movies.csv) and
[Boxoffice.csv](https://cdn.nickplatt.dev/Docs/Boxoffice.csv) files for the
following exercise:

1. List all movies and their combines sales in millions of dollars:

```sql
SELECT title, (domestic_sales + international_sales) / 1000000 AS gross_sales_millions
FROM movies
	JOIN boxoffice
	ON movies.id = boxoffice.movie_id;
```

2. List all movies and their ratings in percent:

```sql
SELECT title, rating * 10 AS rating_percent
FROM movies
	JOIN boxoffice
		ON movies.id = boxoffice.movie_id;
```

3. List all movies that we released on even number years

```sql
SELECT title, year
FROM movies
WHERE year % 2 = 0;
```

??? tip "Odd Vs. Even"

    Remember that to determine if a SQL value is even or odd,
    we use the module operator (`%`), which returns the remainder after division of
    its operands. Since the remainder of an even number divided by 2 is always 0,
    and the remainder of an odd number divided by 2 is always 1 - this makes modulo
    an easy way to find even/odd numbers.

### Queries with Aggregates

In addition to the simple expressions from above, SQL also supports the use of
aggregate expressions (or functions) that allow you to summarize information
about a group of rows of data. With the Pixar database we have been using,
aggregate functions can be used to answer questions like, "How many movies has
Pixar produced?", or "What is the highest grossing Pixar film each year?".

```sql
SELECT AGG_FUNC(column_or_expression) AS aggregate_description, ...
FROM mytable
WHERE constraint_expression;
```

Without a specified grouping, each aggregate function is going to run on the
whole set of result rows and return a single value. And like normal expressionsm
giving your aggregate functions an alias ensures that the results will be easier
to read and process.

#### Common Aggregate Functions

Below are some common aggregate functions that we will be using in fututre
exercises:

| **Function**                         | Description                                                                                                                                                                                                 |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`COUNT(*)`** **`COUNT`**`(column)` | A common function used to count the number of rows in the group is no column name is specified. Otherwise, count the number of rows in the group with non-NULL values in the specified column.              |
| **`MIN`**`(column)`                  | Finds the smallest numerical value in the specified column for all rows in the group.                                                                                                                       |
| **`MAX`**`(column)`                  | Finds the largest numerical value in the specified column for all rows in the group.                                                                                                                        |
| **`AVG`**`(column)`                  | Finds the average numerical value in the specified column for all rows in the group.                                                                                                                        |
| **`SUM`**`(column)`                  | Finds the sum of all numerical values in the specified column for the rows in the group.                                                                                                                    |
| Docs:                                | [MySQL](https://dev.mysql.com/doc/refman/5.6/en/group-by-functions.html), [Postgres](http://www.postgresql.org/docs/9.4/static/functions-aggregate.html), [SQLite](http://www.sqlite.org/lang_aggfunc.html) |
