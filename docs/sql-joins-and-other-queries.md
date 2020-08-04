# SQL `Joins` and Other Query Types

## Multi-Table queries with `JOIN`s
Up to now, we've been working with a single table, but entity data in the real world is often broken down into pieces and stored across multiple orthogonal tables using a process known as *normalization*.  

### Database Normalization
Tables that share information about a single entity need to have a *primary key* that identifies that entity *uniquely* across the database.  One common primary key type is an auto-incrementing integer (because they are space efficient), but it can also be a string, hashed value, so long as it is unique.  

Using the **`JOIN`** clause in a query, we can combine row data across two separate tables using this unique key.  The first of the joins that we will introduce is the **`INNER JOIN`**. 

```sql
SELECT column, another_table_column, ...
FROM mytable
INNER JOIN another_table
	ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, ... ASC/DESC
LIMIT num_limit OFFSET num_offset;
```

The **`INNER JOIN`** is a process that matches rows from the first table and the second table which have the same key (as defined by the **`ON`** constraint) to create a result row with the combined columns from both tables.  After the tables are joined, the other clauses we learned previously are then applied.  

??? tip "`JOIN` vs. `INNER JOIN`"
	You may see queries where the `INNER JOIN` is written simply as a `JOIN`.  These two are equivalent, but we will continue to refer to these joins as inner-joins because they make the query easier to read once you start using other types of joins. 

Let's do some exercises where we look at multiple tables.  We will use the [Movies.csv](https://nicklyss.com/wp-content/uploads/2020/07/Movies.csv) file from previous examples and a new [Boxoffice.csv](https://nicklyss.com/wp-content/uploads/2020/07/Boxoffice.csv) file with additional movie information.  

1. Find the domestic and international sales for each movie:
```sql
SELECT title, domestic_sales, international_sales
FROM movies
	JOIN boxoffice
		ON movies.id = boxoffice.movie_id;
```
2. Show the sales numbers for each movie that did better internationally rather than domestically:
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
