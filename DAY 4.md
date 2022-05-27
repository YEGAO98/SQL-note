# 1
In this exercise, for each of the six continents listed in 2015, you'll identify which country had the maximum inflation rate, 
and how high it was, using multiple subqueries. 
+------------+---------------+-------------------+
| name       | continent     | inflation_rate    |
|------------+---------------+-------------------|
| <country1> | North America | <max_inflation1>  |
| <country2> | Africa        | <max_inflation2>  |
| <country3> | Oceania       | <max_inflation3>  |
| <country4> | Europe        | <max_inflation4>  |
| <country5> | South America | <max_inflation5>  |
| <country6> | Asia          | <max_inflation6>  |
+------------+---------------+-------------------+
  
## 1
  Select the maximum inflation rate in 2015 AS max_inf grouped by continent using the previous step's query as a subquery in the FROM clause.
Thus, in your subquery you should:
Create an inner join with countries on the left and economies on the right with USING (without aliasing your tables or columns).
Retrieve the country name, continent, and inflation rate for 2015.
Alias the subquery as subquery.
This will result in the six maximum inflation rates in 2015 for the six continents as one field table. Make sure to not include continent in the outer SELECT statement.
  
**ANSWER**
  -- Select the maximum inflation rate as max_inf
SELECT MAX(inflation_rate) AS max_inf
  -- Subquery using FROM (alias as subquery)
  FROM (
      SELECT name, continent, inflation_rate
      FROM countries
      INNER JOIN economies
      USING (code)
      WHERE year = 2015) AS Subquery
-- Group by continent
GROUP BY continent;
  
 ## 2
  Now it's time to append your second query to your first query using AND and IN to obtain the name of the country, its continent, and the maximum inflation rate for each continent in 2015.
For the sake of practice, change all joining conditions to use ON instead of USING.
  
  **ANSWER**
  -- Select fields
SELECT name, continent, inflation_rate
  -- From countries
  FROM countries
	-- Join to economies
	INNER JOIN economies
	-- Match on code
	ON countries.code = economies.code
  -- Where year is 2015
  WHERE year = 2015
    -- And inflation rate in subquery (alias as subquery)
    AND inflation_rate IN (
        SELECT MAX(inflation_rate) AS max_inf
        FROM (
             SELECT name, continent, inflation_rate
             FROM countries
             INNER JOIN economies
             ON countries.code=economies.code
             WHERE year = 2015) AS subquery
      -- Group by continent
        GROUP BY continent);
