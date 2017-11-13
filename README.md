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
- Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

```
/*
SELECT max(LENGTH(city)), min(LENGTH(city)) from station;

SELECT city, LENGTH(city) from station where length(city) = ( SELECT max(LENGTH(city)) from station ) and ( SELECT min(LENGTH(city)) from station )

SELECT city, LENGTH(city) from station where length(city) = 21 or length(city) = 3

SELECT city, LENGTH(city) from station where length(city) = ( SELECT max(LENGTH(city)) from station ) or length(city) = ( SELECT min(LENGTH(city)) from station order by city asc LIMIT 1)

SELECT city, LENGTH(city) from station where length(city) = ( SELECT max(LENGTH(city)) from station ) or length(city) = ( SELECT min(LENGTH(city)) from station )
*/

select CITY, length(CITY) from station order by length(CITY), city limit 1; select CITY, length(CITY)from station order by length(CITY) desc, city limit 1; 
```

- Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

```
select distinct city from station where city like 'a%' or city like 'e%' or city like 'i%' or city like 'o%' or city like 'u%'
```

- Query the list of CITY names from STATION that starts and ends with vowels. Your result cannot contain duplicates.

#### regular expression is better

```
SELECT DISTINCT CITY FROM STATION WHERE CITY REGEXP '^[AEIOU][A-Z \s]*[AEIOU]$';
```
- Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.
```
/*
Enter your query here.
*/
Select DISTINCT CITY
FROM
STATION
Where CITY NOT LIKE 'A%' AND CITY NOT LIKE 'E%' AND CITY NOT LIKE 'I%' AND CITY NOT LIKE 'O%' AND CITY NOT LIKE 'U%';
```
