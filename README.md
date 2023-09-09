# DataAnalysis-SQL

### DEMO 1
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

### DEMO 2
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

### DEMO 3
The `apps` table has the following columns:

`id` - the app id

`name` - the app name

`genre` - the genre of the app

`rating` - the app rating

`reviews` - the number of reviews
