** QUESTION **
SELECT acts after Group by but whether group by can use name (newly named) used in select?

## NOTE
here are a few unique considerations when working with subqueries in SELECT. The first is that the subquery needs to return a single value.
If your subquery result returns multiple rows, your entire query will generate an error.

indow functions are processed after the entire query except the final ORDER BY statement. 
Thus, the window function uses the result set to calculate information, as opposed to using the database directly. 
Second, it's important to know that window functions are available in PostgreSQL, Oracle, MySQL, but not in SQLite.
