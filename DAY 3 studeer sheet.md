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

##RIGHT JOIN
SELECT cities.name AS city, urbanarea_pop, countries.name AS country,
       indep_year, languages.name AS language, percent
FROM languages
  RIGHT JOIN countries
    ON languages.code = countries.code
  RIGHT JOIN cities
    ON **countries.code = cities.country_code** 这里接上表的code
ORDER BY city, language;
