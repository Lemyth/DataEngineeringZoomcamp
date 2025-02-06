# Module 2 Homework: Workflow orchestration with Kestra

## Question 1

Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file yellow_tripdata_2020-12.csv of the extract task)?

![alt text](image1.png)

## Question 2

What is the rendered value of the variable file when the inputs taxi is set to green, year is set to 2020, and month is set to 04 during execution?

The rendered value is `green_tripdata_2020-04.csv`




## Question 3
How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?

``` SQL 
SELECT COUNT(*) 
FROM `zoomcamp.yellow_tripdata` 
WHERE filename LIKE 'yellow_tripdata_2020%';
```
Answer is `24648499`

## Question 4
How many rows are there for the Green Taxi data for all CSV files in the year 2020?


``` SQL 
SELECT COUNT(*) 
FROM `zoomcamp.green_tripdata` 
WHERE filename LIKE 'green_tripdata_2020%';
```
Answer is `1734051`

## Question 5
How many rows are there for the Yellow Taxi data for the March 2021 CSV file?

``` SQL
SELECT COUNT(*) 
FROM `zoomcamp.yellow_tripdata` 
WHERE filename LIKE 'yellow_tripdata_2021-03%';
```
Answer is `1734051`

## Question 6
How would you configure the timezone to New York in a Schedule trigger?
In the documentation it is stated the format of the timezone property is IANA format.
So the correct answer is : Add a `timezone property` set to `America/New_York` in the Schedule trigger configuration

## Question 7
