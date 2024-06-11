### What do you mean by foreign key? 
A Foreign key is a field that can uniquely identify each row in another table. 
### INNER JOIN
The INNER JOIN keyword selects all rows from both tables as long as the condition is satisfied i.e. the value of the common field will be the same.
### LEFT JOIN or LEFT OUTER JOIN
This join returns all the rows of the table on the left side of the join and matching rows for the table on the right side of the join. 
### RIGHT JOIN or RIGHT OUTER JOIN
This join returns all the rows of the table on the right side of the join and matching rows for the table on the left side of the join. 
### FULL JOIN
FULL JOIN creates the result set by combining the results of both LEFT JOIN and RIGHT JOIN. The result set will contain all the rows from both tables. 
For the rows for which there is no matching, the result set will contain NULL values.
### 

|Show first name of patients that start with the letter 'C'| SELECT first_name FROM patients where first_name like 'C%' ;| 
|Show first name and last name of patients who does not have allergies. (null)| SELECT first_name,last_name  FROM patients where allergies is null; |
|Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)|SELECT first_name, last_name FROM patients where  weight between 100 and 120 ;|
|Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'|update patients set allergies='NKA' where allergies is null ;|
|Show first name and last name concatinated into one column to show their full name.|SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM patients;|
|Show first name, last name, and the full province name of each patient.|SELECT patients.first_name, patients.last_name, province_names.province_name from patients join province_names on province_names.province_id==patients.province_id;|
|Show how many patients have a birth_date with 2010 as the birth year.|select count(*) AS Total_patient from patients where year(birth_date)=2010;|
|Show the first_name, last_name, and height of the patient with the greatest height.|select first_name, last_name, MAX(height) as height from patients;|
|Show the first_name, last_name, and height of the patient with the shortest height.|select first_name, last_name, MIN(height) as height from patients;|
|Show all columns for patients who have one of the following patient_ids:1,45,534,879,1000| select * from patients where patient_id IN (1,45,534,879,1000);|
|Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?|select distinct(city) from patients where province_id='NS'; |
|Write a query to find list of patients first_name, last_name, and allergies where allergies are not null and are from the city of 'Hamilton'|select first_name, last_name, allergies from patients where allergies is not null and city='Hamilton'; |
|Show unique birth years from patients and order them by ascending.|select distinct(year(birth_date)) as year from patients order by YEAR ;|
|Show unique first names from the patients table which only occurs once in the list.| SELECT first_name FROM patients GROUP BY first_name HAVING COUNT(first_name) = 1|
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||


### 
### 
### 
### 
### 
### 
### 
### 
