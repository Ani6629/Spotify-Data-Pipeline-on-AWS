# Spotify-Data-Pipeline-on-AWS
This project uses various AWS services to build an ETL (Extract, Transform, Load) pipeline for data fetched from the Spotify API. The pipeline retrieves data from the Spotify API, transforms it to a desired format, and loads it into an AWS data store for further analysis using Amazon Athena.

![alt text](https://github.com/Ani6629/Spotify-Data-Pipeline-on-AWS/blob/main/88C8909F-19E2-48DF-812D-F2FD99B77B63.jpg)
## Contents

- [Dataset/API](#datasetapi)
- [AWS Services Used](#aws-services-used)
- [Python Dependencies](#python-dependencies)
- [Execution Flow](#execution-flow)
- [Setup & Running](#setup--running)

<a name="datasetapi"></a>
## Dataset/API

The Spotify API provides extensive data about music artists, albums, and tracks. This project uses the Spotipy library, a lightweight Python library for the Spotify Web API, to extract this data.

<a name="aws-services-used"></a>
## AWS Services Used

This project uses the following AWS services:

- **Amazon S3:** Used as the data store. Raw data is stored in one S3 bucket, and transformed data in another.
- **AWS Lambda:** Lambda functions fetch data from the Spotify API and transform this raw data.
- **Amazon CloudWatch:** CloudWatch schedules the execution of Lambda functions and monitors the performance of the pipeline.
- **AWS Glue Crawler:** The Glue Crawler scans transformed data in S3, identifies its schema, and adds this schema to the AWS Glue Data Catalog.
- **AWS Glue Data Catalog:** This metadata repository makes the transformed data immediately searchable and available for querying.
- **Amazon Athena:** Athena provides an interface for querying the music data using standard SQL.

<a name="python-dependencies"></a>
## Python Dependencies

This project relies on the following Python packages:

- pandas
- numpy
- spotipy

<a name="execution-flow"></a>

## Execution Flow
The pipeline follows these steps:

- A CloudWatch event triggers the extraction Lambda function every hour.
- The function fetches data from the Spotify API and stores this raw data in an S3 bucket.
- The arrival of new data in the S3 bucket triggers the transformation Lambda function.
- The transformation function cleans and reshapes the data using pandas and numpy, and then loads the transformed data into a separate S3 bucket.
- A Glue Crawler scans the new data in S3, identifies its schema, and adds this schema to the Glue Data Catalog.
The transformed data can then be queried using Amazon Athena.

<a name="setup--running"></a>

## Setup & Running
To set up and run this project:

- Install the required Python packages.
- Set up your S3 buckets and folders as described in the "AWS Services Used" section.
- Create the Lambda functions and write your data extraction and transformation code. Remember to set up the necessary triggers.
- Create a Glue Crawler and set it to scan your transformed-data bucket.
- Run the Glue Crawler to populate the Glue Data Catalog with your transformed data's schema.
- Set up your query result location in Athena.

## Note
- If you encounter an error like "No output location provided...", you need to set the query result location in Athena. You can do this in the workgroup settings.
- You may also encounter an error while creating the Lambda function due to issues importing the pandas and spotipy packages. This is because AWS doesn't directly support these packages. To resolve this, you'll need to add a Lambda layer for these packages




