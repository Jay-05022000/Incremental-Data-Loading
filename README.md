                                  Incremental Data Loading from Amazon S3 to AWS Redshift Using AWS Glue ETL
![Amazon S3](https://a11ybadges.com/badge?logo=amazons3)  ![AWS Glue](https://img.shields.io/badge/AWS%20Glue-ETL-blue?logo=amazon-aws&style=flat-square) ![Amazon Redshift](https://img.shields.io/badge/Amazon%20Redshift-Data%20Warehouse-red?logo=amazon-aws&style=flat-square)





Aim:

The aim of this project is to perform incremental data loading from the data lake Amazon S3 to the data warehouse AWS Redshift using a Glue ETL job.



Tools Used:

1) AWS S3: A simple storage service (Data Lake) used to store raw data and act as a data source for the Glue ETL pipeline.
2) AWS Glue: An ETL service offered by AWS used to visually create an ETL pipeline. It takes raw data from the S3 bucket, transforms it, and loads the data into the Redshift table. The ETL pipeline is configured to perform incremental data loading into Redshift, ensuring only updated or new records since the last load are processed, optimizing performance and reducing data redundancy.
3) AWS Redshift: A data warehouse service used to centrally store large amounts of clean data, query it using SQL, and provide required data to downstream teams for data analysis, reporting, and machine learning to accomplish business goals.



Data:

Dataset: Kaggle - Instacart Market Basket Analysis

Aisles_V0: Contains 120 records of information regarding aisles within the Instacart store. Necessary changes are made in the Aisles_V0 file to simulate real-world changing data and verify the project's performance.



Workflow:


![Workflow](https://github.com/user-attachments/assets/0f37f553-6f34-4f7e-9490-e09efb0d3987)



1) Creating Redshift Cluster:
   Create an endpoint for S3 in your VPC to enable communication between your Redshift cluster and S3 for data loading operations.
   Edit inbound rules of your default security group in VPC to allow access from any IP address to the cluster.
   
2) IAM Role:
   Create an IAM role for AWS Glue to access resources in S3 and Redshift on your behalf.
   
3) Crawler:
   Create a crawler to crawl the S3 bucket and create an Athena table.
   
4) Connection:
   Create and test a connection between AWS Glue and Redshift from the 'Connections' tab in AWS Glue.

5) ETL Job:
   Create a visual ETL job in AWS Glue.

6) Workflow Creation:
   Create a Workflow to orchestrate the operation of crawler and ETL job in an easy and automated way.



Notes:

1) Ensure the column names in the Redshift table match those in your raw dataset or source table.
2) S3 bucket versioning works when you upload files with the same name (data might differ but should have the same structure).
3) A Glue ETL job can be scheduled to run using Glue Workflows, which allow job scheduling based on desired times or events.



Automation:

Once a file is uploaded to the specified S3 bucket, an event notification is sent to AWS EventBridge. Based on the received signal, an EventBridge rule triggers the created Glue Workflow that automates the data transfer from S3 into Redshift in an incremental load manner. Glue Workflow is an orchestration feature of Glue that coordinates the operations of crawlers and ETL jobs based on its design.



Use Cases:

1) Data Transfer: Transfer data from one storage service to Redshift for backup or disaster recovery in an incremental or normal order.
2) Personal Case: Integrate this project with the Adzuna data analysis project to obtain only updated or new data at runtime.
