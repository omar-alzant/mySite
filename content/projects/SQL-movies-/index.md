---
title: "Sql -Movies- "
date: 2022-06-08
draft: false
blog_tags: ["sql"]
status: "sql"
weight: 11
summary: "Write SQL queries to answer questions about a database of movies.
"
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://cs50.harvard.edu/x/2022/psets/7/movies/"
        weight: 1
    another_link:
        text: "Another github link"
        icon: "fab alt brands fa-github"
        href: "https://github.com/omar-alzant"
        weight: 2
---


</br>

<strong>
    All the files is included in the github page
    <a href="https://github.com/omar-alzant/files-for-mySite"> Here. </a>
</strong>

</br>
</br>

<a href="https://www.w3schools.com/sql/sql_ref_keywords.asp"> To learn SQL </a>
 and   <a href="https://www.sqlstyle.guide/"> This </a>.

</br>
</br>

```markdown
$ cat filename.sql | sqlite3 movies.db
```
</br>

OR 
to save it in a file :
</br>

```markdown
$ cat filename.sql | sqlite3 movies.db > output.txt

```
***

</br>

The Result:

<img src="./sql1.png" style="max-width: 600px;">


</br>
</br>

*** 

fileName -1- 

```sql
-- write a SQL query to list the titles of all movies released in 2008.
SELECT title 
FROM movies
WHERE year = 2008
```
</br>
</br>

*** 

fileName -2- 

```sql
--write a SQL query to determine the birth year of Emma Stone
SELECT birth
FROM people
WHERE name ='Emma Stone';
```
</br>
</br>


*** 

</br>
</br>

fileName -3- 

```sql
--write a SQL query to list the titles of all movies with a release date on or after 2018, in alphabetical order.
SELECT title
FROM movies
WHERE year >=2018
ORDER BY title ASC;
```
</br>
</br>

***

</br>
</br>

fileName -4- 

```sql
--write a SQL query to determine the number of movies with an IMDb rating of 10.0.
SELECT COUNT(movie_id)
FROM ratings
WHERE rating = 10;
```
</br>
</br>

***

</br>
</br>

fileName -5- 

```sql
-- write a SQL query to list the titles and release years of all Harry Potter movies, in chronological order.
SELECT title, year
FROM movies
WHERE title LIKE "Harry Potter%"
ORDER BY year;
```
</br>
</br>

***

</br>
</br>

fileName -6- 

```sql
--write a SQL query to determine the average rating of all movies released in 2012.
SELECT AVG(rating)
FROM ratings
JOIN movies
ON movies.id = ratings.movie_id
WHERE movies.year = 2012;
```
</br>
</br>

***

</br>
</br>

fileName -7- 

```sql
--write a SQL query to list all movies released in 2010 and their ratings, in descending order by rating. For movies with the same rating, order them alphabetically by title.
SELECT movies.title , ratings.rating
FROM movies
JOIN ratings
ON movies.id = ratings.movie_id
WHERE movies.year = 2010
ORDER BY ratings.rating DESC,movies.title ASC
```
</br>
</br>

***


</br>
</br>

fileName -8- 

```sql
--write a SQL query to list the names of all people who starred in Toy Story.
SELECT name
FROM people JOIN stars ON people.id = stars.person_id JOIN movies ON movies.id = stars.movie_id
WHERE title = 'Toy Story'
```
</br>
</br>

***

</br>
</br>

fileName -9- 

```sql
--write a SQL query to list the names of all people who starred in a movie released in 2004, ordered by birth year.
--If a person appeared in more than one movie in 2004, they should only appear in your results once.(GROUP BY )
SELECT name
FROM people JOIN stars ON stars.person_id = people.id JOIN movies ON movies.id = stars.movie_id
WHERE year = 2004
GROUP BY name,person_id
ORDER BY birth;
```
</br>
</br>

***

</br>
</br>

fileName -10- 

```sql
--write a SQL query to list the names of all people who have directed a movie that received a rating of at least 9.0.
SELECT name
FROM people
JOIN ratings ON ratings.movie_id = directors.movie_id
JOIN directors ON directors.person_id = people.id
WHERE rating >= 9.0
GROUP BY name,person_id
```
</br>
</br>

***

</br>
</br>

fileName -11- 

```sql
--In 11.sql, write a SQL query to list the titles of the five highest rated movies (in order) that Chadwick Boseman
--starred in, starting with the highest rated.
SELECT title
FROM people
JOIN stars ON stars.person_id = people.id
JOIN movies ON stars.movie_id = movies.id
JOIN ratings ON ratings.movie_id = stars.movie_id
WHERE name LIKE "Chadwick Boseman"
ORDER BY rating DESC
LIMIT 5;
```
</br>
</br>

***

</br>
</br>

fileName -12- 

```sql
--write a SQL query to list the titles of all movies in which both Johnny Depp and Helena Bonham Carter starred.(INTERSECT)
SELECT title
FROM movies
JOIN stars ON stars.movie_id = movies.id
JOIN people ON people.id = stars.person_id
WHERE name LIKE "Johnny Depp"
INTERSECT
SELECT title
FROM movies
JOIN stars ON stars.movie_id = movies.id
JOIN people ON people.id = stars.person_id
WHERE name LIKE  'Helena Bonham Carter'
```
</br>
</br>

***

</br>
</br>

fileName -13- 

```sql
-- write a SQL query to list the names of all people who starred in a movie in which Kevin Bacon also starred.
SELECT DISTINCT name
FROM stars JOIN people ON people.id = stars.person_id
WHERE movie_id IN
(
SELECT movie_id
FROM stars JOIN people ON stars.person_id = people.id
WHERE birth = 1958 AND name = "Kevin Bacon"
)
AND name != "Kevin Bacon"
```

</br>
</br>

***

## Understanding :

1- Provided to you is a file called movies.db, a SQLite database that stores data from IMDb about movies, the people who directed and starred in them, and their ratings. 
1- In a terminal window, run sqlite3 movies.db so that you can begin executing queries on the database.

2- First, when sqlite3 prompts you to provide a query, type .schema and press enter. This will output the CREATE TABLE statements that were used to generate each of the tables in the database. By examining those statements, you can identify the columns present in each table.

3- Notice that the movies table has an id column that uniquely identifies each movie, as well as columns for the title of a movie and the year in which the movie was released. The people table also has an id column, and also has columns for each person’s name and birth year.

4- Movie ratings, meanwhile, are stored in the ratings table. The first column in the table is movie_id: a foreign key that references the id of the movies table. The rest of the row contains data about the rating for each movie and the number of votes the movie has received on IMDb.

5- Finally, the stars and directors tables match people to the movies in which they acted or directed. (Only principal stars and directors are included.) Each table has just two columns: movie_id and person_id, which reference a specific movie and person, respectively.

The challenge ahead of you is to write SQL queries to answer a variety of different questions by selecting data from one or more of these tables.
</br>
</br>

## Specification :

For each of the following problems, you should write a single SQL query that outputs the results specified by each problem. Your response must take the form of a single SQL query, though you may nest other queries inside of your query. You should not assume anything about the ids of any particular movies or people: your queries should be accurate even if the id of any particular movie or person were different. Finally, each query should return only the data necessary to answer the question: if the problem only asks you to output the names of movies, for example, then your query should not also output each movie’s release year.


You’re welcome to check your queries’ results against IMDb itself, but realize that ratings on the website might differ from those in `movies.db`, as more votes might have been cast since we downloaded the data!


1- In 1.sql, write a SQL query to list the titles of all movies released in 2008.
Your query should output a table with a single column for the title of each movie.

2- In 2.sql, write a SQL query to determine the birth year of Emma Stone.
Your query should output a table with a single column and a single row (not including the header) containing Emma Stone’s birth year.
You may assume that there is only one person in the database with the name Emma Stone.

3- In 3.sql, write a SQL query to list the titles of all movies with a release date on or after 2018, in alphabetical order.
Your query should output a table with a single column for the title of each movie.
Movies released in 2018 should be included, as should movies with release dates in the future.

4- In 4.sql, write a SQL query to determine the number of movies with an IMDb rating of 10.0.
Your query should output a table with a single column and a single row (not including the header) containing the number of movies with a 10.0 rating.

5- In 5.sql, write a SQL query to list the titles and release years of all Harry Potter movies, in chronological order.
Your query should output a table with two columns, one for the title of each movie and one for the release year of each movie.
You may assume that the title of all Harry Potter movies will begin with the words “Harry Potter”, and that if a movie title begins with the words “Harry Potter”, it is a Harry Potter movie.

6- In 6.sql, write a SQL query to determine the average rating of all movies released in 2012.
Your query should output a table with a single column and a single row (not including the header) containing the average rating.

7- In 7.sql, write a SQL query to list all movies released in 2010 and their ratings, in descending order by rating. For movies with the same rating, order them alphabetically by title.
Your query should output a table with two columns, one for the title of each movie and one for the rating of each movie.
Movies that do not have ratings should not be included in the result.

8- In 8.sql, write a SQL query to list the names of all people who starred in Toy Story.
Your query should output a table with a single column for the name of each person.
You may assume that there is only one movie in the database with the title Toy Story.

9- In 9.sql, write a SQL query to list the names of all people who starred in a movie released in 2004, ordered by birth year.
Your query should output a table with a single column for the name of each person.
People with the same birth year may be listed in any order.
No need to worry about people who have no birth year listed, so long as those who do have a birth year are listed in order.
If a person appeared in more than one movie in 2004, they should only appear in your results once.

10- In 10.sql, write a SQL query to list the names of all people who have directed a movie that received a rating of at least 9.0.
Your query should output a table with a single column for the name of each person.
If a person directed more than one movie that received a rating of at least 9.0, they should only appear in your results once.

11- In 11.sql, write a SQL query to list the titles of the five highest rated movies (in order) that Chadwick Boseman starred in, starting with the highest rated.
Your query should output a table with a single column for the title of each movie.
You may assume that there is only one person in the database with the name Chadwick Boseman.

12- In 12.sql, write a SQL query to list the titles of all movies in which both Johnny Depp and Helena Bonham Carter starred.
Your query should output a table with a single column for the title of each movie.
You may assume that there is only one person in the database with the name Johnny Depp.
You may assume that there is only one person in the database with the name Helena Bonham Carter.

13- In 13.sql, write a SQL query to list the names of all people who starred in a movie in which Kevin Bacon also starred.
Your query should output a table with a single column for the name of each person.
There may be multiple people named Kevin Bacon in the database. Be sure to only select the Kevin Bacon born in 1958.
Kevin Bacon himself should not be included in the resulting list.




</br>
</br>


{{<youtube v5_A3giDlQs>}}


</br>
</br>

