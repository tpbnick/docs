# Random SQL Problems

## Movies Exercise

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

## Houses Exercise
We are now going to implement a program to import Hogwarts student data into a database, and then produce class roseters.  

For this exercise we are going to use the files found in [houses.zip](https://cdn.cs50.net/2019/fall/psets/7/houses/houses.zip).  You will find the files `characters.csv`, `import.py`, `roster.py`, and `students.db`.  We will import all of the school's data into a database and write a Python program to query that database to get house rosters.  

### Breakdown

In `import.py`, we will write a program that imports data from a CSV spreadsheet.  The program should accept the name of a CSV file as a command-line argument.  

* If the incorrect number of command-line arguments are provided, our program should print an error and exit.  

* We are going to assume that the CSV file exists, and will have columns `name`, `house`, and `birth`.  

For each student in the CSV file, we are going to insert the student into the `students` table in the `students.db` database.  

* While the CSV file provided in houses.zip has just a `name` column, that database has separate columns for `first`, `middle`, and `last` names.  We will then want to first parse each name and separate it into first, middle, and last names.  We are going to assume that each person's name field will contain either two space-separated names (a first and last name) or three space-separated names (a first, middle, and last name).  For students without a middle name, we will leave their `middle` name field as `NULL` in the table.  

In `roster.py`, we will write a program that prints a list of students for a given house in alphabetical order.  

* We will make the program accept the name of a house as a command-line argument.  If the incorrect number of command-line arguments are provided, we will print an error or exit.  

* Our program will query the `students` table in the `students.db` database for all students in the specified house.  

* Or program should then print out each student's full name and birth year (formatted as, e.g., `Harry James Potter, born 1980` or `Luna Lovegood, born 1981`).  Each student will be printed on their own line.  Students should be ordered by last name.  If students share the same last name, we will order them by first name.  

### Solution

**`import.py`**
```py
from cs50 import SQL
from sys import argv
from sys import exit
import csv

#splits the names from the name column into their own array
def partition_name(full_name):
	names = full_name.split()
	return names if len(names) >= 3 else [names[0], None, names[1]]

#checks argument count
if len(argv) != 2:
	print("Arguments error")
	exit(1)

db = SQL("sqlite:///students.db")

csv_path = argv[1]
with open(csv_path) as csv_file:
	reader = csv.DictReader(csv_file)
	for row in reader:
		names = partition_name(row["name"]) #partition_name gives an array
		db.execute("INSERT INTO students(first, middle, last, house, birth) VALUES(?, ?, ?, ?, ?)", names[0], names[1], names[2], row["house"], row["birth"])
```

**`roster.py`**
```py
from cs50 import SQL
from sys import argv
from sys import exit

if len(argv) != 2:
    print("Argument Error")
    exit(1)

db = SQL("sqlite:///students.db")

house_chosen = argv[1]
rows = db.execute("SELECT * FROM students WHERE house = ? ORDER BY last, first", house_chosen)
for row in rows:
    first, middle, last, birth = row["first"], row["middle"], row["last"], row["birth"]
    if row["middle"] == None:
        print(f"{first} {last}, born {birth}")
    else:
        print(f"{first} {middle} {last}, born {birth}")
```
Now try running the following commands and check your answer:

```
$ python import.py characters.csv

$ python roster.py Gryffindor
Lavender Brown, born 1979
Colin Creevey, born 1981
Seamus Finnigan, born 1979
Hermione Jean Granger, born 1979
Neville Longbottom, born 1980
Parvati Patil, born 1979
Harry James Potter, born 1980
Dean Thomas, born 1980
Romilda Vane, born 1981
Ginevra Molly Weasley, born 1981
Ronald Bilius Weasley, born 1980
```