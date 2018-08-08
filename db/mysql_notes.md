<html><link rel="stylesheet" href="path/to/css/retro.css"></html>

<link rel="stylesheet" href="path/to/css/retro.css">

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


