# SQL

## Procedures

### Detect consecutive dates ranges using SQL

````sql
WITH t AS (
  SELECT <DATE_COLUMN> d,ROW_NUMBER() OVER(ORDER BY <DATE_COLUMN>) i
  FROM <TABLE>
  GROUP BY <DATE_COLUMN>
)
SELECT MIN(d),MAX(d)
FROM t
GROUP BY DATEDIFF(day,i,d)
````

### Count comma separated items

````sql
LENGTH(fooCommaDelimColumn) - LENGTH(REPLACE(fooCommaDelimColumn, ',', ''))
````

### Build time scale table in MySQL

````sql
SET @d0 = "2020-01-02";
SET @d1 = "2030-12-31";

SET @date = date_sub(@d0, interval 1 day);

INSERT INTO <TIME_TABLE>(<DATE_COL>, <YEAR_COL>, <MONTH_COL>)
SELECT @date := date_add(@date, interval 1 day) as <DATE_COL>,
year(@date) as <YEAR_COL>,
month(@date) as <MONTH_COL>
FROM <BIG_TABLE> -- biger than scale table
WHERE date_add(@date, interval 1 day) <= @d1
ORDER BY <DATE_COL>;

````

### Greatest N per group

````sql
SELECT c.*, p1.* 
FROM customer c 
JOIN purchase p1 ON (c.id = p1.customer_id) 
LEFT OUTER JOIN purchase p2 ON (c.id = p2.customer_id AND (p1.date < p2.date OR p1.date = p2.date AND p1.id < p2.id)) 
WHERE p2.id IS NULL;
````

## Documentation

[Analytic functions](https://blog.jooq.org/tag/analytic-functions/)