Lab 2
-----

Glue ETL
--------

1. Convert CSV to Parquet 
    - Glue ETL will provision required Apache Spark infrastructure to run the job

----------------------------

1. Open Glue 
    - Add Job 
    - Name      > iris_csv_to_parquet
    - IAM       > data-engg-demo

    - Select "Create tables in your data target"
    - data target > s3://aws-glue-suman/iris-data/parquet

Lab 3 
-----

1. Open "Querying Amazon Customer Review Dataset"
    https://s3.amazonaws.com/amazon-reviews-pds/readme.html
    
2. S3 Location: https://s3.console.aws.amazon.com/s3/buckets/amazon-reviews-pds/parquet/?region=us-east-1

3. Athena SQL Query Editior : Create the table 

4. RUN: MSCK REPAIR TABLE amazon_reviews_parquet

5. RUN:

SELECT product_title, star_rating, review_body
FROM "data_engg_demo_db"."amazon_reviews_parquet" 
WHERE product_category = 'Personal_Care_Appliances'
and star_rating > 3
limit 100;

Lab 4 (Customer Review with Glue) Jupyter Notebook
---------------------------------------------------
s3://aws-glue-suman/customer_review/customer_reviews_with_sentiment_compressed.txt.gz

SELECT sentiment, star_rating, product_title, review_headline, review_body
FROM "data_engg_demo_db"."amazon_customer_review"
WHERE star_rating > 3 and sentiment != 'POSITIVE'
limit 100;

Lab 5 (Lamnda + Kinesis)
-------------------------

1. Show the lambda function 
2. Create Kinesis Data Firehose
    Name:   CustomerReviewStream
    S3 Prefix : product_review_kinesis/

3. Create a Glue Crawler 
4. Query with Athena 

