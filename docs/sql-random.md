# Random SQL Problems

## Movies

In the following problems we will be using [`movies.db`](https://cdn.cs50.net/2019/fall/psets/7/movies/movies.zip).  This database is made of of multiple tables: movies, ratings, stars, and directors.  We will need to `JOIN` some of these tables to answer some of the following problems:  

1. Write a SQL query to list the titles of all movies released in 2008.  Your query should output a table with a single column for the title of each movie.  
```sql
SELECT title
FROM movies
WHERE year = 2008;
```  

2. Write a SQL query to determine the birth year of Emma Stone.  Your query should output a table with a single column and a single row (plus optional header) containing Emma Stone’s birth year.  You may assume that there is only one person in the database with the name Emma Stone.  
```sql
SELECT birth
FROM people
WHERE name = 'Emma Stone';
```  

3. Write a SQL query to list the titles of all movies with a release date on or after 2018, in alphabetical order.  Your query should output a table with a single column for the title of each movie.  Movies released in 2018 should be included, as should movies with release dates in the future.
```sql
SELECT title
FROM movies
WHERE year >= 2018
ORDER BY title;
```  

4. Write a SQL query to determine the number of movies with an IMDb rating of 10.0.  Your query should output a table with a single column and a single row (plus optional header) containing the number of movies with a 10.0 rating.  
```sql
SELECT COUNT(*) AS NumberOfMoviesWith10Rating
FROM ratings
WHERE rating = 10;
```  

5. Write a SQL query to list the titles and release years of all Harry Potter movies, in chronological order.  Your query should output a table with two columns, one for the title of each movie and one for the release year of each movie.  You may assume that the title of all Harry Potter movies will begin with the words “Harry Potter”, and that if a movie title begins with the words “Harry Potter”, it is a Harry Potter movie. 
```sql
SELECT title, year
FROM movies
WHERE title LIKE "Harry Potter%"
ORDER BY year;
```  

6. Write a SQL query to determine the average rating of all movies released in 2012.  Your query should output a table with a single column and a single row (plus optional header) containing the average rating.  
```sql
SELECT AVG(rating)
FROM ratings JOIN movies ON movies.id = ratings.movie_id
WHERE year = 2012;
```  

7. Write a SQL query to list all movies released in 2010 and their ratings, in descending order by rating. For movies with the same rating, order them alphabetically by title.  Your query should output a table with two columns, one for the title of each movie and one for the rating of each movie.  Movies that do not have ratings should not be included in the result.  
```sql
SELECT title, rating
FROM movies JOIN ratings on movies.id = ratings.movie_id
WHERE year = 2010
ORDER BY rating DESC, title;
```  

8. Write a SQL query to list the names of all people who starred in Toy Story.  Your query should output a table with a single column for the name of each person.  You may assume that there is only one movie in the database with the title Toy Story.  
```sql
SELECT name
FROM people JOIN stars ON people.id = stars.person_id
JOIN movies ON movies.id = stars.movie_id
WHERE title = "Toy Story";
```  

9. Write a SQL query to list the names of all people who starred in a movie released in 2004, ordered by birth year.  Your query should output a table with a single column for the name of each person.  People with the same birth year may be listed in any order.  No need to worry about people who have no birth year listed, so long as those who do have a birth year are listed in order.  If a person appeared in more than one movie in 2004, they should only appear in your results once.
```sql
SELECT DISTINCT name
FROM people JOIN stars ON people.id = stars.person_id
JOIN movies on movies.id = stars.movie_id
WHERE year = 2004
ORDER BY birth;
```  

10. Write a SQL query to list the names of all people who have directed a movie that received a rating of at least 9.0.  Your query should output a table with a single column for the name of each person.
```sql
SELECT name
FROM people
JOIN directors ON directors.person_id = people.id
JOIN ratings ON directors.movie_id = ratings.movie_id
WHERE rating >= 9.0;
```  

11. Write a SQL query to list the titles of the five highest rated movies (in order) that Chadwick Boseman starred in, starting with the highest rated.  Your query should output a table with a single column for the title of each movie.  You may assume that there is only one person in the database with the name Chadwick Boseman.
```sql
SELECT DISTINCT title
FROM people JOIN stars ON people.id = stars.person_id
JOIN ratings ON ratings.movie_id = stars.movie_id
JOIN movies ON movies.id = stars.movie_id
WHERE name = "Chadwick Boseman"
ORDER BY rating DESC
LIMIT 5;
```  

12. Write a SQL query to list the titles of all movies in which both Johnny Depp and Helena Bonham Carter starred.  Your query should output a table with a single column for the title of each movie.  You may assume that there is only one person in the database with the name Johnny Depp.  You may assume that there is only one person in the database with the name Helena Bonham Carter.
```sql
SELECT title
FROM people JOIN stars ON stars.person_id = people.id
JOIN movies ON stars.movie_id = movies.id
WHERE name = "Johnny Depp"
AND movie_id IN (
    SELECT movie_id
    FROM people JOIN stars ON stars.person_id = people.id
    WHERE name = "Helena Bonham Carter"
);
```  

13. Write a SQL query to list the names of all people who starred in a movie in which Kevin Bacon also starred.  Your query should output a table with a single column for the name of each person.  There may be multiple people named Kevin Bacon in the database. Be sure to only select the Kevin Bacon born in 1958.  Kevin Bacon himself should not be included in the resulting list.
```sql
SELECT DISTINCT name
FROM people JOIN stars ON stars.person_id = people.id
WHERE name != "Kevin Bacon"
AND movie_id IN (
    SELECT movie_id
    FROM people JOIN stars ON stars.person_id = people.id
    WHERE name = "Kevin Bacon" AND birth = 1958
)
```