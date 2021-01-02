```SQL
CREATE OR REPLACE TABLE `dsmbootcamp.dogukan_nefis.semi_structured_hw`
as
SELECT * FROM `dsmbootcamp.sample.semi_structured_hw`;

CREATE OR REPLACE TABLE `dsmbootcamp.dogukan_nefis.semi_structured_hw_expected`
as
SELECT * FROM `dsmbootcamp.sample.semi_structured_hw_expected`;

Select * from dogukan_nefis.semi_structured_hw_expected;
Select * from dogukan_nefis.semi_structured_hw;


SELECT name,c.id AS car_id,c.model AS car_model,m.year AS manufacture_year,
  ARRAY(
  SELECT
    AS STRUCT p.* REPLACE(TIMESTAMP_ADD(p.date, INTERVAL 3 HOUR) AS date)
  FROM
    UNNEST(purchase) AS p) 
    AS purchase
FROM
  dogukan_nefis.semi_structured_hw as semi
cross join unnest(manufacture) as m
cross join unnest(car) as c
```
