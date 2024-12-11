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

<img width="468" alt="image" src="https://github.com/user-attachments/assets/c5f488e2-5161-4e45-b363-888f25cd5128"> <br>

After publishing the recipe, I create the job with two output locations, System and User. The file type that will be saved in the System is Parquet, and it uses Compression Snappy. Whereas the file type that will be generated in the User folder is CSV with Maintainer (Park/Engineering) partition.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/6c82b282-520c-451e-a7d0-48c47becb0ea"> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/6ac312bb-4baf-4f98-a7a4-dfa9af93e515"> <br>



## Insights and Findings

## Tools and Technologies
The project involves:


## Deliverables
The project involves:

## Conclusion



