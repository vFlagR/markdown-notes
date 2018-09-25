<html><link rel="stylesheet" href="../css/air.css"></html>

[Home](../index.html)

# MySQL Notes

##### Find InnoDB size #####
```MySQL
SELECT table_schema, 
       Sum(data_length + index_length) / 1024 / 1024 AS total_mb, 
       Sum(data_length) / 1024 / 1024                AS data_mb, 
       Sum(index_length) / 1024 / 1024               AS index_mb, 
       Count(*)                                      AS tables, 
       Curdate()                                     AS today 
FROM   information_schema.tables 
GROUP  BY table_schema 
ORDER  BY 2 DESC; 
```

##### Find count of items with greater than given threshold

~~~MySql
SELECT DISTINCT(FIELD) AS FIELD_NAME, COUNT(FIELD) AS Count
FROM TABLE_NAME
GROUP BY FIELD
HAVING COUNT(FIELD) > 300000000;
~~~

