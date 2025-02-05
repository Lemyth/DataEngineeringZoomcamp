# Module 2 Homework: Workflow orchestration with Kestra

## Question 1

Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file yellow_tripdata_2020-12.csv of the extract task)?

``` bash 
    # Linux command to create a python:3.12.8 container in interactive mode 

    docker run -it --entrypoint /bin/bash python:3.12.8
```

We will use this bash command to get the pip version : 

``` bash
# inside container 
pip --version
```

## Question 2






## Question 3
During the period of October 1st 2019 (inclusive) and November 1st 2019 (exclusive), how many trips, respectively, happened
1- Up to 1 mile
``` SQL 
SELECT COUNT(1)
FROM (
    SELECT * 
    FROM green_taxi_trips 
    WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00'
) AS Oct_trips
WHERE trip_distance <= 1;
```
Answer is `104802`

2- In between 1 (exclusive) and 3 miles (inclusive),
``` SQL 
SELECT COUNT(1)
FROM (
    SELECT * 
    FROM green_taxi_trips 
    WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00'
) AS Oct_trips
WHERE trip_distance > 1 AND trip_distance <= 3;
```
Answer is `198924`

3- In between 3 (exclusive) and 7 miles (inclusive)
``` SQL 
SELECT COUNT(1)
FROM (
    SELECT * 
    FROM green_taxi_trips 
    WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00'
) AS Oct_trips
WHERE trip_distance > 3 AND trip_distance <= 7;
```
Answer is `109603`

4- In between 7 (exclusive) and 10 miles (inclusive)
``` SQL 
SELECT COUNT(1)
FROM (
    SELECT * 
    FROM green_taxi_trips 
    WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00'
) AS Oct_trips
WHERE trip_distance > 7 AND trip_distance <= 10;
```
Answer is `27678`

5- Over 10 miles
``` SQL 
SELECT COUNT(1)
FROM (
    SELECT * 
    FROM green_taxi_trips 
    WHERE lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND lpep_dropoff_datetime < '2019-11-01 00:00:00'
) AS Oct_trips
WHERE trip_distance > 10;
```
Answer is `35189`

## Question 4
Which was the pick up day with the longest trip distance? Use the pick up time for your calculations.
``` SQL
SELECT DISTINCT DATE(lpep_pickup_datetime) AS pickup_day, MAX(trip_distance) AS longest_dist
FROM green_taxi_trips
GROUP BY pickup_day
ORDER BY longest_dist DESC
LIMIT 1;
```

## Question 5
Which were the top pickup locations with over 13,000 in total_amount (across all trips) for 2019-10-18?
Consider only lpep_pickup_datetime when filtering by date.

``` SQL
SELECT t."PULocationID", z."Zone", SUM(t.total_amount) AS DayRevenue
FROM green_taxi_trips AS t
INNER JOIN taxi_zones AS z
	ON t."PULocationID" = z."LocationID"
WHERE(t.lpep_pickup_datetime >= '2019-10-18 00:00:00' 
    AND t.lpep_pickup_datetime < '2019-10-19 00:00:00') 
GROUP BY t."PULocationID", z."Zone"
HAVING SUM(t.total_amount) > 13000
ORDER BY DayRevenue DESC ;
```

## Question 6
For the passengers picked up in October 2019 in the zone named "East Harlem North" which was the drop off zone that had the largest tip?
``` SQL
SELECT z."Zone", MAX(t.tip_amount) AS max_tip
FROM (SELECT tr."PULocationID", tr."DOLocationID", tr.lpep_pickup_datetime, tr.tip_amount, zo."Zone"
		FROM green_taxi_trips AS tr
		INNER JOIN taxi_zones AS zo
		ON tr."PULocationID" = zo."LocationID"
		WHERE  zo."Zone" = 'East Harlem North' )  AS t
INNER JOIN taxi_zones AS z
	ON t."DOLocationID" = z."LocationID"
WHERE(t.lpep_pickup_datetime >= '2019-10-01 00:00:00' 
    AND t.lpep_pickup_datetime < '2019-11-01 00:00:00') 
GROUP BY t."DOLocationID", z."Zone"
ORDER BY max_tip DESC
LIMIT 1;
```
## Question 7
