# DAY 2 SQL Q
## - [ ]  Q5
Join the bike_trips table with bike but keep all the records no matter whether they have a match.

-- bike_trips
| trip_ID | duration | bikeID |
|---------|----------|---------|
|     364 | 60       | 5000    |
|     365 | 900      | 2300    |
|     366 | 720      | 2350    |
-- bike
| bike_ID | last_date_in_use | color |
|---------|------------------|-------|
|    2300 |      2020-04-15  | blue  |
|    2350 |      2020-04-15  | green |
|    3000 |      2020-04-18  | green |

### **ANSWER**
*SELECT Trip_ID, Duration, bikeID, last_date_in_use, color 
FROM bike_trips AS t*
**FULL** JOIN bike AS b
ON t.bikeID = b.bike_ID;

## - [ ] Q6
From the speaker table, recode the price column into a categorical column called price_level. For prices lower than 100, we consider them as low. For prices higher than 1000, we consider them as high. The rest would be medium.

-- speaker
|   model                             |   price  |
|-------------------------------------|----------|
|   Bowers & Wilkins Formation Wedge  |   899    |
|   Bang & Olufsen Beosound Balance   |   2250   |
|   Xiaomi Mi Smart Speaker HD        |   50     |

### **ANSWER**
SELECT model,price,
      **WRONG**:  *price < 100 AS 'low'
        price > 1000 AS 'high'
       price between 100 and 1000 'medium'
       price_l*
      **CORRECT** CASE WHEN price < 100 THEN 'low'
       WHEN price > 1000 THEN 'high'
       ELSE 'medium'
       END AS price_level 
FROM speaker;

## - [ ] Q7
In the vendors table, some entries in the zip_code have 9 digits. Return a zip_code column that only contains the first 5 digits from the zip_code column.

-- vendors
| vendor_name                               | zip_code   |
|-------------------------------------------|------------|
| CHONZIE INC                               | 28803      |
| VAUGHN & MELTON CONSULTING ENGINEERS,INC. | 28806-1721 |
| TEG LEASE FEE                             | 339073835  |

### ANSWER:
SELECT vendor_name, 
      LEFT(zip_code,5) AS zip_code
FROM vendors;

## - [ ] Q8
The bike_stations table contains the newly built bike stations' locations. The bike_trips table contains the bike trips that have started at either existing or newly built bike stations.

Return each bike trip only started in newly built bike stations.

-- bike_trips
|   Trip_ID  |   Start_Time               |   Starting_Station     |
|------------|----------------------------|------------------------|
|   2023364  |   2016-07-08T09:24:00.000  |   3044                 |
|   2023365  |   2016-07-09T19:08:00.000  |   3046                 |
|   2023366  |   2016-07-10T10:56:00.000  |   3046                 |
-- bike_stations
|   Station_ID  |   Latitude   |   Longitude    |
|---------------|--------------|----------------|
|   3045        |   34.028511  |   -118.25667   |
|   3046        |   34.05302   |   -118.247948  |
|   3055        |   34.044159  |   -118.251579  |

### ANSWER:
SELECT Trip_ID, Station_ID, Latitude, Longitude 
FROM bike_trips AS t
INNER JOIN bike_stations AS s
ON t.Starting_Station = s.Station_ID;

## - [ ] Q9
Replace the missing value in the state column with None.

-- vendors
|   vendor_name             |      city      |   state  |
|---------------------------|----------------|----------|
|   CHONZIE INC             |   ASHEVILLE    |   NC     |
|   WEBSEDGE LIMITED        |   LONDON       |          |
|   HILTON GARDEN INN TAMP  |   TAMPA        |   FL     |

### ANSWER:
SELECT name, city, state is NULL = NONE AS state
SELECT name, city, COALESCE(state,'None') AS state
FROM vendors;

## - [ ] Q10 (Medium）
From the speaker table, use self join to return the pairs of the speaker model with the same launch date.

-- speaker
| Product_ID | model                             | price | launch     |
|------------|-----------------------------------|-------|------------|
|    1       | Bowers & Wilkins Formation Wedge  | 899   | 2019-06-01 |
|    2       | Harman Kardon Citation 200        | 349   | 2020-09-01 |
|    3       | Sonos Five                        | 449   | 2021-06-01 |
|    4       | Naim Mu-so 2nd Generation         | 1690  | 2019-06-01 |

### ANSWER:
SELECT name, city, COALESCE(state,'None') AS state
FROM vendors;

[^1]: **COALESCE**:

## - [ ] Q11(MEDIUM)
From the vendors table, return the top 5 states with the largest number of vendors.

--vendors
|   vendor_name             |   vendor_city     |   vendor_state  |
|---------------------------|-------------------|-----------------|
|   CHONZIE INC             |   ASHEVILLE       |   NC            |
|   INREACH ONLINE CLE      |   AUSTIN          |   TX            |
|   HENDERSONVILLE JEEP CH  |   HENDERSONVILLE  |   NC            |
|   ....................... |   ............... |   ..            |

### ANSWER:
SELECT vendor_state, COUNT(*) AS number_vendors
FROM vendors
GROUP BY vendor_state
ORDER BY number_vendors DESC
LIMIT 5;

# NOTE 
Modify your query so that only years with an average budget of greater than $60 million are included.
[^1]: SELECT is processed after HAVING
