# Drinking Fountains Data Analytics Platform (City Of Vancouver)

## Table of Contents
1. [Project Description](#project-description)
2. [Project Title](#project-title)
3. [Objective](#objective)
4. [Dataset](#dataset)
5. [Methodology](#methodology)
6. [Insights and Findings](#insights-and-findings)
7. [Tools and Technologies](#tools-and-technologies)
8. [Deliverables](#deliverables)
9. [Conclusion](#conclusion)

## Project Description
Exploring Vancouver's Public Drinking Fountains

## Project Title
City of Vancouver Drinking Fountains: An Exploratory Data Analysis

## Objective
Exploratory Data Analysis (EDA) will be conducted to examine the relationship between pet-friendly parks and the public drinking fountains in Vancouver City. The project will involve analyzing the area, operation times, maintainers, and additional information about pet-friendly parks.

## Dataset
The dataset of Drinking Fountains consists of several columns as listed below:
  - **MAPID**: A unique identifier for every single drinking fountain.
  - **NAME**: The name of the drinking fountain is located at, while the location is additional location information.
  - **LOCATION**: The additional location information or direction of the drinking fountain.
  - **MAINTAINER**: The department responsible for maintaining the drinking fountain.
  - **IN_OPERATION**: The the time when the drinking fountain is in operation.
  - **GEO LOCAL AREA**: The area where the drinking fountain is located.
  - **PET_FRIENDLY**: The drinking fountain is pet-friendly (Yes/No).

<img width="800" alt="image" src="https://github.com/user-attachments/assets/39aae78d-e112-4419-ab3d-3e8909d41ed9">

## Methodology
In the methodolgy section, the discussion will be including Data Profiling, Data Cleaning, ETL Pipeline Design, Data Enriching, Data Protection, Data Governance, and Data Observability.

### 1. Data Ingestion
The first step is to create the bucket and folders in S3. For the tags,  Category = Water. In addition, the storage class is Glacier Instant Retrieval because the data will be accessed around once a semester. This storage is suitable for rarely accessed data but requires retrieval in milliseconds when needed. This is the directory path that is used to store the raw data:

*df-raw-des> Drinking_Fountains/ ingestion_year=2024/ ingestion_semester=2/*

<img width="800" alt="image" src="https://github.com/user-attachments/assets/ba540904-6609-41d9-9127-f411f38e3451">

*df-raw-des> DrinkingFountains_PetFriendly/*

<img width="800" alt="image" src="https://github.com/user-attachments/assets/7b1068da-436b-43bd-8002-ef62bc9f390e">

### 2. Data Profiling
The next step is Data Profiling. The purpose of data profiling is to understand the data, such as if there are missing values or duplicate or invalid data. Some of the information can be used for data cleaning. Data profiling can be processed in AWS Glue DataBrew. To preview the data, the new dataset, dfdataset-des was created. 

<img width="800" alt="image" src="https://github.com/user-attachments/assets/30adf692-351b-435e-8c25-90312e628c8e"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/0017a82f-99ff-4da9-9c8c-a4dadd905d58"> <br>

Next, run Data Profile in the Data Profile Overview tab. The job output is the folder *df-trf-des> Drinking_Fountains/ data-profiling/*. The result of data profiling can be seen and analyzed through the summary and column summary. It shows the missing cells, duplicate rows, and the information for each column, such as column type, data quality, and total values.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/ae172c1f-b583-4f5a-a040-fb23ea5c2970"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/49513bae-a449-4f72-b715-17de1584af8c"><br>

After analyzing the data profiling, a project was created with this dataset to continue the data cleaning process

### 3. Data Cleaning
Before doing data cleaning, a new folder was created to store the data cleaning process. In the data cleaning folder, there are two folders, System and User.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/f88fd16e-ea1e-444d-b5ba-2766a9efef1e"> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/fa71902c-8851-47dc-9ad6-c36683bbb6da"> <br>

On the data cleaning step, there are some steps, like removing white spaces for some columns, filling the missing values with the last valid value, renaming the column name and deleting empty rows with missing values in Geo_Local_Area column.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/fdb861a4-fc51-4e69-b02d-b5d65b71ee70"><br>

For another dataset, there are some steps to do, like removing white spaces for some columns and deleting some not used columns. The final columns are MAPID and Pet_Friendly 

<img width="800" alt="image" src="https://github.com/user-attachments/assets/c5f488e2-5161-4e45-b363-888f25cd5128"> <br>

After publishing the recipe, the job was created with two output locations, System and User. The file type that will be saved in the System is Parquet, and it uses Compression Snappy. Whereas the file type that will be generated in the User folder is CSV.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/6c82b282-520c-451e-a7d0-48c47becb0ea"> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/92c1572b-a170-4f41-9b6a-a9dccf153777"> <br>

### 4. Data Pipeline Design
The data pipeline is designed to answer and deliver the data question regarding the hypothesis or diagnostic analysis, which is the relationship between pet-friendly parks and areas of drinking fountains. AWS Glue is used to design the pipeline.

The first step is creating the Visual ETL with the name dfpet-dataset-des. The data that has been cleaned is exported from S3://df-trf-des/Drinking_Fountains/data-cleaning/User.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/98ed46d0-ee87-4192-9b22-1179fe16a3ec"><br>

On the other side, another dataset that has been cleaned is exporred from S3://df-trf-des/DrinkingFountains_PetFriendly/data-cleaning/User/. 

<img width="800" alt="image" src="https://github.com/user-attachments/assets/f3af8b94-33b2-4930-8459-fc27afb1107a"><br>

Next, the two datasets are joined with the key MAP ID. After that, I aggregate using count to see the number of pet-friendly parks according to the drinking fountain area.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/01df5056-1af1-4100-9250-0c32603e6070"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/7f5e1a02-ca15-4f1c-b4af-e8977b3e8629"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/695f8518-38a2-4729-a52b-9525959f069a"><br>

To store the result from the data pipeline process, a new folder is created  with two folders inside, System and User.

*df-cur-des> DrinkingFountains_and_PetFriendly/*
<img width="800" alt="image" src="https://github.com/user-attachments/assets/0a1f4a79-89ec-4c57-8ab3-bfcf0fb1d182"> <br>

Below is the overall pipeline design for answering the exploratory analysis.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/5761e4c0-ddbe-4442-a20a-01723de55d1f"> <br>

### 5. Data Enriching
The first step in Data Enriching is creating the Data Catalog using AWS Glue. The name of the database is df-datacatalog-des.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/5dc7977c-bb0f-4187-845d-eb069e9d08ed"><br>

After that, I will crawl all the datasets to tables, including raw, transform, and curated buckets in S3.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/a9d6786a-c78e-4da6-b46e-1942be03e704"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/e4af94e4-9662-44c5-bcd6-586b7d2d39d6"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/7c69d191-9b48-496b-be07-4ab05655ad93"><br>

After running the crawler, the result can be seen in the Databases – Tables.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/abeb7d5f-7e69-4b41-a8c0-5a80932a40ad"> <br>

Athena is an interactive analysis where we can write the query. The result will be saved in s3://df-cur-des/

<img width="800" alt="image" src="https://github.com/user-attachments/assets/7227b045-e27e-410b-94c0-d9a8a566ef09"> <br>

The query for descriptive analytics is to count the drinking fountains that are operated throughout the year. Based on the data, there are 37 drinking fountains.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/11406858-2b7d-46aa-ae22-4b22e23c63a1"><br>

### 6. Data Protection
To protect the operational datasets from CIA threats, AWS provides some services, such as Identity and Access Management (IAM) and AWS Key Management Services (KMS). The first step is creating a key through the Key Management Service, with the name df-key-des.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/6e07385b-887d-4abe-ac24-f5c5916d7ecd"><br>

LabRole will be granted the permission. LabRole will become a key user and key administrator.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/152ad6af-3c4c-4f8d-9d4f-1e29c3aaaa64"><br>

This key will be used for encryption, decryption, and storing data when uploading data.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/591f100a-d68f-418e-9290-6c17073cc622"> <br>

After making the key, this key needs to be applied to the S3 storage. df-key-des will be used for every storage.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/b79efd9f-978a-47e9-843d-654c6f86ae2d"><br>

The bucket versioning is changed to enabled in order to maintain the integrity, so the version of the object can be maintained.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/e71c1716-1f0f-4574-9027-698d153353f4"><br>

After that, create an empty backup and the application rule. The bucket is created with the name df-raw-back-des, df-trf-back-des and df-cur-back-des.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/48274257-b43f-467e-934c-6c3b21130588"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/3a541dc5-c178-45b4-a7bc-21da57f8c71b"><br>

After finishing the backup for raw, transform, and curated, go to the original bucket, for example, df-raw-des, and go to the Management Tab, and create the replication rule. The name of the replication rule is df-reprul-des.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/557b5b31-8e84-417d-8ebd-21862db99722"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/8c03eac5-44b5-489d-8f52-cc35bdd353c0"><br>

Below are the replication rules with the source bucket of df-raw-des, df-trf-des, df-cur-des.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/c9b2fba3-de8d-4d42-afb7-3cc7cf120ddc"> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/ce4f871a-b491-4a7c-9716-3cc2148de1df"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/c7f5d195-9fa2-4870-8c51-5dfb6b2db196"><br>


### 7. Data Governance
Data governance is the process to ensure quality, including completeness and uniqueness, privacy, compliance, and protection. The first step is creating a new bucket, which is data-quality with two folders inside, Failed and Passed.

*df-trf-des> Drinking_Fountains/ data-quality/*

<img width="800" alt="image" src="https://github.com/user-attachments/assets/7211d3d9-989e-4961-84b7-4d9c41d2a902"><br>

After that, go to AWS Glue and make the new Visual ETL with the name df-QPC-Des. First, take the data from the S3 bucket. 
s3://df-trf-des/Drinking_Fountains/data-cleaning/System/ 

<img width="800" alt="image" src="https://github.com/user-attachments/assets/4f5252e0-71ef-4d9d-8bb3-4e37ab5df41e"><br>

Then, check the privacy of the data using Detect Sensitive Data. Replace the detected entity using data masking to handle the privacy issue. 

<img width="800" alt="image" src="https://github.com/user-attachments/assets/966c94de-301c-4183-8bcd-4d6ab98a788e"><br>

The next step is to evaluate data quality by checking the completeness and uniqueness.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/66d1d65b-dd1e-477d-9fa6-bb6102f524ba"><br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/aa19700b-ff4d-458b-8070-2754ec26a44e"><br>

According to the conditions above, conditional router will be used to divide the passed and failed data. 

<img width="800" alt="image" src="https://github.com/user-attachments/assets/9c76298b-b9fe-4b50-b7b1-837531e61747"><br>

Then, the data is ready to be stored in the S3 bucket in data-quality bucket, depending on the evaluation result (Failed or Passed). Below is the overall pipeline of the data governance process to ensure privacy, completeness and uniqueness.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/fde9caf9-4c23-4929-ab63-09ac73c43c03"><br>


## Insights and Findings

<img width="800" alt="image" src="https://github.com/user-attachments/assets/8f4d5af8-c457-4ae8-8a95-be7e965939a0"><br>


## Tools and Technologies
The project involves:


## Deliverables
The project involves:

## Conclusion



