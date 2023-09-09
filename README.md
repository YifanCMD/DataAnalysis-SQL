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

## DEMO 5
The `math_students` and `english_students` tables have the following columns:

`student_id` - the student id

`grade` - the grade level of the student

`first_name` - the student’s first name

`last_name` - the student’s last name

- Using a subquery, get all students in math who are also enrolled in english.
```
SELECT *
FROM math_students
WHERE student_id IN (
  SELECT student_id
  FROM english_students
);
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/5a25f2fd-22b8-4aae-a1d3-cab02be525af)

- Using a subquery, find out which students in math are in the same grade level as the student with id `7`.
```
SELECT *
FROM math_students
WHERE grade IN (
  SELECT grade
  FROM math_students
  WHERE student_id = 7
);
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/efbcc80b-bd18-4540-959e-bcd482e0dd67)

- Using a subquery, find all students enrolled in english class who are not also enrolled in math class.
```
SELECT *
FROM english_students
WHERE student_id
NOT IN (
  SELECT student_id
  FROM math_students
);
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/0aeb2e0b-710e-4f71-9752-889429fa5e37)

- Using a subquery, find out what grade levels are represented in both the math and english classes.
```
SELECT grade
FROM math_students
WHERE EXISTS (
  SELECT grade
  FROM english_students
);
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/a90241a8-7ac3-4330-b9d2-6c3f51a9f0c1)

## DEMO 6
The `box_office` table has the following columns:

`id` - the id of each row

`title` - the title of the movie

`week` - the week following the film’s release

`gross` - the gross for that week

`to_date_gross` - the total gross of the movie up to each week

- Using a window function with `PARTITION BY`, get the running total in gross for each movie up to the current week and display it next to the current week column along with the `title`, `week`, and `gross` columns.
```
SELECT title, week, gross, 
  SUM(gross) OVER (
    PARTITION BY title 
    ORDER BY week
  ) AS 'running_total_gross'
FROM box_office;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/41930df3-adf3-428b-8b68-cbc36cebec4c)

- Write a query using a window function with ROW_NUMBER and ORDER BY to see where each row falls in the amount of gross.
```
SELECT ROW_NUMBER()
OVER (
  ORDER BY gross
) AS 'row_num', title, week, gross
FROM box_office;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/da87d3bf-ecb3-44b2-be60-6d46f9ee32d2)

## DEMO 7
The `orders` table has the following columns:

`id` - the order id

`product_id` - the product id

`price` - the price of the individual product item

`quantity` - the quantity of items in the order

- Given an orders table, calculate the price times quantity of each order. Include the id and product_id columns in the result.
```
SELECT id, product_id, price * quantity
FROM orders;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/8b579608-76a5-4f04-b1c6-7bf679fc0bdf)

## DEMO 8
The `weather` table has the following columns:

`id` - the id of each entry

`date` - the date of each entry

`high` - the high temperature of the date, in Fahrenheit

`low` - the low temperature of the date, in Fahrenheit

- Utilize `CAST` to calculate the average of the `low` and `high` temperatures for each date such that the result is of type `REAL`. Select the `date` column and alias this result column as ‘average’.
```
SELECT date, (CAST(high AS 'REAL') + 
  CAST(low AS 'REAL')) / 2.0 AS 'average'
FROM weather;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/cac1be41-6504-4f56-931d-86510c0a41ec)

## DEMO 9
The `purchases` table has the following columns:

`purchase_id` - the id of the purchase

`purchase_date` - the date of the purchase

- After a purchase is created, it can be returned within 7 days for a full refund. Using modifiers, get the date of each purchase offset by 7 days in the future.
```
SELECT purchase_id, DATE(purchase_date, '+7 days')
FROM purchases;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/9aa23b70-f8dc-43b5-8de6-b5dbe12d3283)

- Get the hour that each purchase was made. Which hour had the most purchases made?
```
SELECT strftime('%H',purchase_date) 
     AS 'Hour',
   COUNT(strftime('%H',purchase_date)) 
     AS 'Purchases'
FROM purchases 
GROUP BY 1 
ORDER BY 2 desc;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/72480ba1-f38a-46f5-ac4e-a05de62090a0)

- Using string formatting and substitutions, get the month and day for each purchase in the form ‘mm-dd’. Give this new column a name of ‘reformatted’.
```
SELECT STRFTIME('%m-%d', purchase_date) AS 'reformatted'
FROM purchases;
```
![image](https://github.com/YifanCMD/DataAnalysis-SQL/assets/96324028/ce98a367-65fd-4bbb-895b-31c640c0ee95)
