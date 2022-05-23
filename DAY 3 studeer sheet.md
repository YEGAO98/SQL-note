# NOTE
## Difference between LEFT JOIN & INNER JOIN
1.返回不同
inner join：inner join只返回两个表中联结字段相等的行。
left join：left join返回包括左表中的所有记录和右表中联结字段相等的记录。
2.数量不同
inner join：inner join的数量小于等于左表和右表中的记录数量。
left join：left join的数量以左表中的记录数量相同。
3.记录属性不同
inner join：inner join不足的记录属性会被直接舍弃。
left join：left join不足的记录属性用NULL填充。
TIPS:
1.对查询进行优化，应尽量避免全表扫描，首先应考虑在 where 及 order by 涉及的列上建立索引。
2、应尽量避免在 where 子句中使用!=或&lt;&gt;操作符，否则将引擎放弃使用索引而进行全表扫描。
3、应尽量避免在 where 子句中对字段进行 null 值判断，否则将导致引擎放弃使用索引而进行全表扫

## RIGHT JOIN
SELECT cities.name AS city, urbanarea_pop, countries.name AS country,
       indep_year, languages.name AS language, percent
FROM languages
  RIGHT JOIN countries
    ON languages.code = countries.code
  RIGHT JOIN cities
    ON **countries.code = cities.country_code** 这里接上表的code
ORDER BY city, language;

## UNION
UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。

SQL UNION 语法
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
注释：默认地，UNION 操作符选取不同的值。如果允许重复的值，请使用 UNION ALL。

