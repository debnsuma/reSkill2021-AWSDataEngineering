Lab 1
======

Glue Data Catalog and Athena 
----------------------------

1. Store File in S3 
2. Collect metabada with Glue ETL 
3. Run Query using Athena 
----------------------------

1. Create a S3 bucket (name: <your bucket name>), in this example the bucket name: aws-glue-suman
    - Copy all the 3 folder under Data in this bucket

2. Open Glue 
    - Crawler   > Name "sales_crawler"
    - Path      > s3://aws-glue-suman/sales
    - IAM Role  > default
    - DB Name   > mydb
    - Prefix    > sales_

3. Open Athena 
    
    SELECT * FROM "mydb"."sales_salesdata" 
    WHERE  sales > 5000
    limit 10;

    SELECT count(*) AS COUNT 
    FROM "mydb"."sales_salesdata" 


Lab 2
======

Glue ETL
--------

1. Convert CSV to Parquet 
    - Glue ETL will provision required Apache Spark infrastructure to run the job
    - Pick the same file (sales.CSV) 
    - Walk through the code 

----------------------------

2. Open Glue 
    - Add Job 
    - Name      > sales_csv_to_parquet
    - IAM       > default
    - Prefix    > iris_

    - Select "Create tables in your data target"
    - Format : Parquet
    - Target path > s3://aws-glue-suman/SalesData/parquet/

    - While its running, check in S3 and see the new file in parquet format 
    - Create a crawler
    - Query with Athena

Lab 3 
=====

(Lamnda + Kinesis)
------------------

1. Open "Querying Amazon Customer Review Dataset"
    https://s3.amazonaws.com/amazon-reviews-pds/readme.html
    
2. S3 Location: https://s3.console.aws.amazon.com/s3/buckets/amazon-reviews-pds/parquet/?region=us-east-1

3. Show the lambda function (product_review_sentiment)

3. Athena SQL Query Editior : Create the table 

SELECT sentiment, star_rating, product_title, review_headline, review_body
FROM "mydb"."review_product_review_kinesis"
WHERE star_rating > 3 and sentiment = 'POSITIVE'
limit 100;

