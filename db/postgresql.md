<html><link rel="stylesheet" href="../assets/css/air.css"></html>

[Home](../index.html)

# PostgreSQL Notes

### Connecting to a PostgreSQL DB ###
~~~
psql -h HOSTNAME/ENDPOINT -p PORT -U USER -W DATABASE
~~~

### Find running queries (via PSQL) ###
~~~sql
SELECT pid, age(query_start, clock_timestamp()), usename, query
FROM pg_stat_activity
WHERE query != '<IDLE>' AND query NOT ILIKE '%pg_stat_activity%'
ORDER BY query_start desc;
~~~

### Find running queries (without logging in to PSQL) ###
~~~shell
sudo su -
su - POSTGRES_USER
pg_top
~~~

### List of useful CLI commands once logged in to PSQL ###
##### Quit/Exit #####
~~~sql 
\q 
~~~
##### Connect to a database #####
~~~sql 
\c DATABASE_NAME 
~~~
##### Show table definition including triggers #####
~~~sql 
\d TABLE_NAME 
~~~
##### List tables from all schemas (if *.* is omitted will only show SEARCH_PATH ones) #####
~~~sql 
\dt *.* 
~~~
##### List databases #####
~~~sql 
\l 
~~~
##### List schemas #####
~~~sql 
\dn 
~~~
##### List functions #####
~~~sql 
\df 
~~~
##### Show code for specified function #####
~~~sql 
\df+ FUNCTION_NAME 
~~~
##### List views #####
~~~sql 
\dv 
~~~
##### list extensions #####
~~~sql 
\dx 
~~~
##### List users #####
~~~sql 
\du 
~~~
##### List a username if present. #####
~~~sql 
\du USERNAME 
~~~
##### Create a role with an existing username. #####
~~~sql 
create role USERNAME1 
~~~
##### Create a role with username and password. #####
~~~sql 
create role USERNAME2 noinherit login password PASSWORD;  
~~~
##### Change role for current session to USERNAME1. #####
~~~sql 
set role USERNAME1;  
~~~
##### Allow USERNAME1 to set its role as USERNAME2. #####
~~~sql 
grant USERNAME2 to USERNAME1;  
~~~


