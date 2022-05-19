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
