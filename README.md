# mysql-query-practice

- difference of two count queries
  select (select count(city) from station) - (select count(distinct city) from station)

- can not be created complex group function query like -
```
  SELECT city, max(LENGTH(city)), min(LENGTH(city)) from station
```
or like -
 ```
 SELECT city, LENGTH(city) from station where LENGTH(city) = max(LENGTH(city))
```
#### It should be like -
```
SELECT city, LENGTH(city) from station where (SELECT max(LENGTH(city)), min(LENGTH(city)) from station )
```
