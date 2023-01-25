## Week 1 Homework

In this homework we'll prepare the environment 
and practice with Docker and SQL


## Question 1. Knowing docker tags

Run the command to get information on Docker 

```docker --help```

Now run the command to get help on the "docker build" command

Which tag has the following text? - *Write the image ID to the file* 

- `--imageid string`
- `--iidfile string`
- `--idimage string`
- `--idfile string`

>Docker Command
```
docker build --help
```
>Answer
```
--iidfile string
```

## Question 2. Understanding docker first run 

Run docker with the python:3.9 image in an interactive mode and the entrypoint of bash.
Now check the python modules that are installed ( use pip list). 
How many python packages/modules are installed?

- 1
- 6
- 3
- 7

>Answer
```
3
```


## Question 3. Count records 

How many taxi trips were totally made on January 15?

Tip: started and finished on 2019-01-15. 

Remember that `lpep_pickup_datetime` and `lpep_dropoff_datetime` columns are in the format timestamp (date and hour+min+sec) and not in date.

- 20689
- 20530
- 17630
- 21090

> Answer
```
20689
```
> SQL Query
```
SELECT COUNT(*) 
FROM public.green_taxi_data 
WHERE DATE(lpep_pickup_datetime)='2019-01-15' AND
      DATE(lpep_pickup_datetime)='2019-01-15' 
```

## Question 4. Largest trip for each day

Which was the day with the largest trip distance
Use the pick up time for your calculations.

- 2019-01-18
- 2019-01-28
- 2019-01-15
- 2019-01-10

> Answer
```
2019-01-15
```

> SQL Query
```
SELECT CAST(lpep_pickup_datetime AS DATE)as pickup_datetime,
       MAX(trip_distance) as largest_trip
FROM public.green_taxi_data 
GROUP BY 1 
ORDER BY 2 DESC 
LIMIT 1
```

## Question 5. The number of passengers

In 2019-01-01 how many trips had 2 and 3 passengers?
 
- 2: 1282 ; 3: 266
- 2: 1532 ; 3: 126
- 2: 1282 ; 3: 254
- 2: 1282 ; 3: 274

> Answer
```
2: 1282 ; 3: 254
```

> SQL Query
```
SELECT COUNT(CASE WHEN passenger_count = 2 THEN 1 ELSE null END) AS trip_with_2_passengers,
	   COUNT(CASE WHEN passenger_count = 3 THEN 1 ELSE null END) AS trip_with_3_passengers
FROM public.green_taxi_data 
WHERE CAST(lpep_pickup_datetime AS DATE)= '2019-01-01' 
```

## Question 6. Largest tip

For the passengers picked up in the Astoria Zone which was the drop off zone that had the largest tip?
We want the name of the zone, not the id.


- Central Park
- Jamaica
- South Ozone Park
- Long Island City/Queens Plaza

> Answer
```
Long Island City/Queens Plaza
```

> SQL Query
```
SELECT 
	zpu."Zone" as pick_up_location,
	zdo."Zone" as drop_off_location,
	MAX(t.tip_amount) as largest_tip
FROM public.green_taxi_data t
JOIN zones zpu
ON t."PULocationID"=zpu."LocationID"
JOIN zones zdo
ON t."DOLocationID"=zdo."LocationID"
WHERE zpu."Zone" = 'Astoria'
GROUP BY 1,2
ORDER BY 3 DESC
LIMIT 1
```

## Week 1 Homework part b terraform

## Question 1. Creating Resources

After updating the main.tf and variable.tf files run:

```
terraform apply
```

Paste the output of this command into the homework submission form.












