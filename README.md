# DataAnalysis-SQL

## DEMO 1
The `books` table has the following columns:

`id` - the book id

`title` - the book title

`author` - the book author

`average_rating` - the average rating

`num_pages` - the number of pages

- Select the `title`, `author`, and `average_rating` of each book with an `average_rating` between 3.5 and 4.5.
```
  SELECT title, author, average_rating
  FROM books 
  WHERE average_rating
  BETWEEN 3.5 AND 4.5;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/328e9713-f64f-43d6-a5eb-a4cde278bb2a)

- Select all the unique `author`s from the table.
```
  SELECT DISTINCT author FROM books;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/80fb8e69-cf86-4005-9b01-bceb4246fd14)

## DEMO 2
The `nba_matches` table has the following columns:

`id` - the match id

`date` - the date of the match

`home_team` - the home team

`away_team` - the away team

`home_points` - the home team points

`away_points` - the away team points

- Given the final scores of several NBA games, use `CASE` to return the results for each game:If `home team` won, return ‘HOME WIN’.If `away team` won, return ‘AWAY WIN’. Select the `id` column and the `CASE` result.
```
SELECT id, 
  CASE
    WHEN home_points > away_points
      THEN 'HOME WIN'
    ELSE 'AWAY WIN'
  END AS 'result'
FROM nba_matches;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/12694302-29fb-4a4e-aa40-94262e54eb52)

## DEMO 3
The `apps` table has the following columns:

`id` - the app id

`name` - the app name

`genre` - the genre of the app

`rating` - the app rating

`reviews` - the number of reviews

- Find the number of apps by `genre`.
```
SELECT genre, COUNT(*) AS '# apps'
FROM apps
GROUP BY genre;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/3fb986c6-e491-4be3-a211-988c323f657a)

- Get the total number of `reviews` of all apps by `genre`. Limit the results for genres where the total number of app reviews is over 30 million.
```
SELECT genre, SUM(reviews) AS 'Total Reviews' 
FROM apps
GROUP BY genre
HAVING SUM(reviews) > 30000000;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/080639ce-d298-4699-b552-d42d3a6c7e88)

- Select the `name`, `genre`, and `rating` of `apps` in descending order of their rating, and limit the result to 20 rows.
```
SELECT name, genre, rating
FROM apps
ORDER BY rating DESC
LIMIT 20;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/3567a656-82fd-4a37-9913-e15e4983f3d0)

- Find the lowest and highest rating for all apps using two different queries.
```
SELECT MIN(rating)
FROM apps;

SELECT MAX(rating)
FROM apps;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/80648c60-a539-4a1b-b24f-360ce774537d)

- Get the average rating of all apps, rounded to 2 decimal places. Alias the result column as ‘average rating’.
```
SELECT ROUND(AVG(rating), 2) AS 'average rating'
FROM apps;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/c3aae384-41b4-4ad9-8fcf-86778b751f8f)

## DEMO 4
The `projects` table has the following columns:

`id` - the project id

`employee_id` - the id of the employee assigned to this project

The `employees` table has the following columns:

`id` - the id of the employee

`first_name` - the first name of the employee

`last_name` - the last name of the employee

- The projects table stores the employee_id for the employee assigned to each project. Perform an inner join on the two tables, matching on the primary key and foreign key described above, and select all columns.
```
SELECT *
FROM projects
JOIN employees
  ON projects.employee_id = employees.id;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/f437afc5-122b-4f9a-a80e-fc474cf8ca96)

- Perform a join between the two tables, such that it selects all projects even if there is no employee assigned to it.
```
SELECT *
FROM projects
LEFT JOIN employees
  ON projects.employee_id = employees.id;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/5a681db5-4e4a-4726-9c99-ae25f62a2f9f)

