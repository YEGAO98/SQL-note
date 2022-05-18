# SQL-note
study note and question note
## Q1
1. **having** can be used in aggregation and function such as **SUM(),AVG()
2. **WHERE** cannot be used in aggregation
## Q2
From the bike_trips table, return the hour from the Start_Time and End_Time, and convert the hour to the NUMERIC data type.
-- bike_trips
|   Trip_ID  |   Start_Time           |   End_Time            |
|------------|------------------------|-----------------------|
|   2023364  |   2016-07-08T09:24:00  |   2016-07-08T09:57:00 |
|   2182651  |   2016-07-09T19:08:00  |   2016-07-09T20:22:00 |
|   2286870  |   2016-07-10T10:56:00  |   2016-07-10T12:23:00 |

**ANSWER:**
SELECT Trip_ID,
      *MY time*:
      Start_Time :: NUMERIC AS Start_Hour,
      End_Time :: NUMERIC AS End_Hour
      *Correct Answer*:
      EXTRACT(hour FROM Start_Time) :: NUMERIC AS Start_Hour,
      EXTRACT(hour FROM End_Time) :: NUMERIC AS End_Hour
FROM bike_trips;

## Q3
Return the rows that appears both in the movie_2000 and movie_2000 table.

-- movie_2000
| year    | title                    | budget       |
|---------|--------------------------|--------------|
|   2000  |   Mission: Impossible 2  |   125000000  |
|   2004  |   Shrek 2                |   150000000  |
|   2008  |   The Dark Knight        |   185000000  |
|   2010  |   Toy Story 3            |   200000000  |
-- movie_2010
|   year  |   title                            |   budget       |
|---------|------------------------------------|----------------|
|   2010  |   Toy Story 3                      |   200000000    |
|   2014  |   Transformers: Age of Extinction  |   210000000    |
|   2015  |   Star Wars: The Force Awakens     |   245000000    |
|   2016  |   Captain America: Civil War       |   250000000    |

**ANSWER**
SELECT *
FROM movie_2000 
INTERSECT 
SELECT *
FROM movie_2010;

## Q4
Add the rows from the movie_2010 table to movie_2000 but remove the duplicates.

-- movie_2000
| year    | title                    | budget       |
|---------|--------------------------|--------------|
|   2000  |   Mission: Impossible 2  |   125000000  |
|   2004  |   Shrek 2                |   150000000  |
|   2008  |   The Dark Knight        |   185000000  |
|   2010  |   Toy Story 3            |   200000000  |
-- movie_2010
|   year  |   title                            |   budget       |
|---------|------------------------------------|----------------|
|   2010  |   Toy Story 3                      |   200000000    |
|   2014  |   Transformers: Age of Extinction  |   210000000    |
|   2015  |   Star Wars: The Force Awakens     |   245000000    |
|   2016  |   Captain America: Civil War       |   250000000    |

**ANSWER:**
SELECT *
FROM movie_2000
UNION 
SELECT *
FROM movie_2010
ORDER BY year;

## Q5
