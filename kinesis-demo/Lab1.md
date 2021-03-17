Lab 1
======

Glue Data Catalog and Athena 
----------------------------

1. Store File in S3 
2. Collect metabada with Glue ETL 
3. Run Query using Athena 
----------------------------

1. Create a S3 bucket

2. Open Glue 
    - Crawler   > Name "iris_csv_crawler"
    - Path      > s3://aws-glue-suman/iris-data/csv/
    - IAM Role  > default
    - DB Name   > suman_db
    - Prefix    > iris_

3. Open Athena 
    
    WHERE fare_amount >= 15
    limit 10;

    WHERE class = 'Iris-setosa'
    limit 10;

    SELECT count(*) AS COUNT FROM "mydb"."data_engg_taxi";

Lab 2
======

Glue ETL
--------

1. Convert CSV to Parquet 
    - Glue ETL will provision required Apache Spark infrastructure to run the job

----------------------------

2. Open Glue 
    - Add Job 
    - Name      > iris_csv_to_parquet
    - IAM       > default
    - Prefix    > iris_

    - Select "Create tables in your data target"
    - data target > s3://aws-glue-suman/iris-data/parquet/

Lab 3 
======

1. Open "Querying Amazon Customer Review Dataset"
    https://s3.amazonaws.com/amazon-reviews-pds/readme.html
    
2. S3 Location: https://s3.console.aws.amazon.com/s3/buckets/amazon-reviews-pds/parquet/?region=us-east-1

3. Athena SQL Query Editior : Create the table 

4. RUN: MSCK REPAIR TABLE amazon_reviews_parquet

5. RUN:

SELECT product_title, star_rating, review_body
FROM "suman_db"."amazon_reviews_parquet" 
WHERE product_category = 'Personal_Care_Appliances'
and star_rating > 3
limit 10;


Lab 4
======

1. Explain the Jupyter notebook 

2. Create a Crawler 

S3 Location: s3://aws-glue-suman/customer_review/customer_reviews_with_sentiment_compressed.txt.gz

3. Athena Query 

SELECT sentiment, star_rating, product_title, review_headline, review_body
FROM "suman_db"."amazon_customer_review"
WHERE star_rating > 3 and sentiment = 'POSITIVE'
limit 100;

Lab 5 (Lamnda + Kinesis)
========================

1. Show the lambda function 
2. Create Kinesis Data Firehose
    Name:   CustomerReviewStream
    S3 Prefix : product_review_kinesis/

3. Create a Glue Crawler 
    S3: s3://aws-glue-suman/product_review_kinesis/
4. Query with Athena 

SELECT * FROM "suma_db"."suman_product_review_kinesis" 
WHERE sentiment != 'POSITIVE'
limit 100;