## Week 3 Homework

## Question 1:
What is the count for fhv vehicle records for year 2019?
- 65,623,481
- 43,244,696
- 22,978,333
- 13,942,414

> Answer
```
43244696
```
> SQL Query
```
SELECT COUNT(*) FROM `original-folio-375016.ny_taxi_data.external_fhv_tripdata`;
```
## Question 2:
Write a query to count the distinct number of affiliated_base_number for the entire dataset on both the tables.</br> 
What is the estimated amount of data that will be read when this query is executed on the External Table and the Table?

- 25.2 MB for the External Table and 100.87MB for the BQ Table
- 225.82 MB for the External Table and 47.60MB for the BQ Table
- 0 MB for the External Table and 0MB for the BQ Table
- 0 MB for the External Table and 317.94MB for the BQ Table 

> Answer
```
0 MB for the External Table and 317.94MB for the BQ Table 
```
> SQL Query
```
SELECT COUNT(*) FROM `original-folio-375016.ny_taxi_data.external_fhv_tripdata`;
```
## Question 3:
How many records have both a blank (null) PUlocationID and DOlocationID in the entire dataset?
- 717,748
- 1,215,687
- 5
- 20,332

> Answer
```
717,748
```
> SQL Query
```
SELECT COUNT(*) FROM 
 `original-folio-375016.ny_taxi_data.external_fhv_tripdata` 
 where PUlocationID IS NULL and 
 DOlocationID IS NULL;
```

## Question 4:
What is the best strategy to optimize the table if query always filter by pickup_datetime and order by affiliated_base_number?
- Cluster on pickup_datetime Cluster on affiliated_base_number
- Partition by pickup_datetime Cluster on affiliated_base_number
- Partition by pickup_datetime Partition by affiliated_base_number
- Partition by affiliated_base_number Cluster on pickup_datetime
> Answer
```
Partition by pickup_datetime Cluster on affiliated_base_number
```
## Question 5:
Implement the optimized solution you chose for question 4. Write a query to retrieve the distinct affiliated_base_number between pickup_datetime 2019/03/01 and 2019/03/31 (inclusive).</br> 
Use the BQ table you created earlier in your from clause and note the estimated bytes. Now change the table in the from clause to the partitioned table you created for question 4 and note the estimated bytes processed. What are these values? Choose the answer which most closely matches.
- 12.82 MB for non-partitioned table and 647.87 MB for the partitioned table
- 647.87 MB for non-partitioned table and 23.06 MB for the partitioned table
- 582.63 MB for non-partitioned table and 0 MB for the partitioned table
- 646.25 MB for non-partitioned table and 646.25 MB for the partitioned table
> Answer
```
647.87 MB for non-partitioned table and 23.06 MB for the partitioned table
```
> SQL Query
```
 CREATE OR REPLACE TABLE original-folio-375016.ny_taxi_data.fhv_tripdata_partitoned_clustered
 PARTITION BY DATE(pickup_datetime)
 CLUSTER BY Affiliated_base_number AS
 SELECT * FROM original-folio-375016.ny_taxi_data.external_fhv_tripdata;
 
SELECT COUNT(DISTINCT Affiliated_base_number)
FROM `original-folio-375016.ny_taxi_data.fhv_tripdata_partitoned_clustered` 
WHERE pickup_datetime BETWEEN '2019-03-01' AND '2019-03-31';
```

## Question 6: 
Where is the data stored in the External Table you created?

- Big Query
- GCP Bucket
- Container Registry
- Big Table
> Answer
```
GCP Bucket
```

## Question 7:
It is best practice in Big Query to always cluster your data:
- True
- False

> Answer
```
True
```

