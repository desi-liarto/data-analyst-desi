# Student Rights and Responsibilities Data Analysis for UCW Registrar Office

## Table of Contents
1. [Project Description](#project-description)
2. [Project Title](#project-title)
3. [Objective](#objective)
4. [Dataset](#dataset)
5. [Methodology](#methodology)
6. [Tools and Technologies](#tools-and-technologies)
7. [Deliverables](#deliverables)
8. [Conclusion](#conclusion)

## Project Description
Student Rights and Responsibilities Data Analytics Platform

## Project Title
Student Misconduct Complaints: Descriptive Analytics and Insights

## Objective
The objective of this project is to analyze data for the UCW Registrar Office. The project will involve developing a data platform that stores, processes, and gives valuable information to the Student Rights & Responsibilities Advisor about student misconduct complaints, allegations, and resolutions, especially for critical complaints. The platform will provide detailed descriptive analytics that will enable Registrar Office to know what happened by offering insights into historical trends and patterns of student misconduct complaints.

## Dataset
The dcomplaints dataset consists of several columns as listed below:
- **Complaint_ID**: A unique identifier for each student misconduct complaint.
- **Student_Name**: The name of the student accused of misconduct.
- **Date_Received**: The date the complaint was received.
- **Issue_Type**: The category of the complaint (e.g., Grading, Harassment, Facilities).
- **Severity**: The seriousness of the complaint (e.g., Low, Medium, High, Critical).
- **Complaint_Status**: The current stage of the complaint process (e.g., Open, Pending, Closed).
- **Details**: A brief summary of the specific concerns raised in the complaint.
- **Assigned_Department**: The department or office responsible for handling the complaint
- **Response_Time(Days)**: The number of days it took to acknowledge the complaint
- **Resolved_By**: The name of the person or committee who made the final decision on the case

## Methodology
In the methodolgy section, the discussion will be including Data Profiling, Data Cleaning, ETL Pipeline Design, Data Enriching, Data Protection, Data Governance, and Data Observability.

### 1. Data Ingestion
The first step is to create the bucket and folders in S3. The storage class is S3 because the data will be accessed every month.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/4e087e20-6b10-49c1-99ac-0a0bc5dbfc7a" /><br>

<img width="600" alt="image" src="https://github.com/user-attachments/assets/3158ff59-20eb-409b-8fbf-7994c8230b78" /> <br>


### 2. Data Profiling
The next step is Data Profiling. The purpose of data profiling is to understand the data, such as if there are missing values or duplicate or invalid data. Some of the information can be used for data cleaning. Data profiling can be processed in AWS Glue DataBrew.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/4e0da2b5-a5ba-4d0e-8c93-41260c815cb9" /> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/ba6b4e4a-a3dc-4a41-8e6a-582f71bd59e4" /> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/28fa42e0-d7be-440c-a201-04362e50fc12" /> <br>

After analyzing the data profiling, a project was created with this dataset to continue the data cleaning process

### 3. Data Cleaning
On the data cleaning step, there are some steps, such as removing white spaces for some columns, filling the missing values with the last valid value, renaming the column name and deleting empty rows with missing values. It can be processed in AWS Glue DataBrew. The cleaning dataset will be stored in *ro-trf-des> Complaints/ Data-Cleaning/*. In data cleaning folder, there are two folders, System and User. 

<img width="800" alt="image" src="https://github.com/user-attachments/assets/dd4e4ef3-dc94-4974-bf6e-77210758193f" /> <br>

<img width="600" alt="image" src="https://github.com/user-attachments/assets/556ddc26-1867-4ac3-a447-88e6a0891d3a" /> <br>

### 4. Data Pipeline
The data pipeline is designed to answer and deliver the data question regarding the descriptive analysis about student misconduct complaints, especially the percentage of the critical complaints. AWS Glue is used to design the pipeline.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/ea5cc94e-9ca9-404b-a139-85e29d392b13" /> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/865fd7cf-35d8-43bf-a8ab-1d9e2aef2523" /> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/94a19b64-4f41-4c4a-ad9d-1dc9a9c94667" /> <br>

<img width="600" alt="image" src="https://github.com/user-attachments/assets/90cbf525-d7c7-4009-b2bd-df290718c96e" /> <br>

### 5. Data Enriching
After ingesting the clickstream data, the first step in data enrichment is to create a Data Catalog using AWS Glue. After that, I will crawl all the datasets to organize them into tables, which will include raw, transform, and curated buckets in S3

<img width="800" alt="image" src="https://github.com/user-attachments/assets/6130fa8c-4190-4600-bacf-c19cc95c6e0b" /><br>

After running the crawler, the result can be seen in the Databases – Tables.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/6376296d-64d5-4cfd-aa3c-675f2f8dcc46" /><br>

Athena supports interactive analysis, allowing users to write and execute queries directly.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/90821b29-62b6-408f-ade4-22d3da56dd0b" /><br>

### 6. Data Protection
To protect the confidentiality, integrity, and availability of operational datasets, AWS offers services such as Identity and Access Management (IAM) and AWS Key Management Service (KMS).

The first step is creating a key through the Key Management Service, with the name ro-srp-key-des.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/755ce9b4-f52c-4729-abce-7c3ae2f0d9ca" /> <br>

After making the key, this key needs to be applied to the S3 storage. ro-srp-key-des will be used for every storage.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/e0ee4f2c-e659-412e-8537-25eb310dd85a" /> <br>

Next, create the replication rule, with the name ro-srp-reprul-des.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/f5809f36-c12c-4e24-a958-e9bb83e5f6e2" /> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/1ff7aa8d-9e3d-405f-97d9-5e7f0346947b" /> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/f777698d-d7a8-4117-ba11-e410e54749eb" /> <br>

### 7. Data Governance
Data governance is the process of ensuring quality, including completeness and uniqueness, as well as privacy, compliance, and protection.  AWS Glue will be used to create a Visual ETL.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/0ff2ed65-7c11-448c-bc0a-aed4052d2c42" /> <br>

In addition, data freshness is crucial for maintaining the relevance of the information.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/976f6c4a-4011-4ebe-90b3-aa05480ae495" /> <br>

### 8. Data Observability
In data observability, the service is CloudWatch to monitor and control resources. Other than that, there is CloudTrail, which can be used to monitor user activities. 

<img width="800" alt="image" src="https://github.com/user-attachments/assets/b1d02306-26b6-47df-b64f-3bf65d4c509f" /> <br>


## Tools and Technologies
**_AWS Services:_**

S3: Data storage and management

AWS Glue: Data cleaning, transformation, and ETL pipeline

Amazon Athena: SQL queries

IAM and KMS: Data security.

Amazon CloudWatch: Resources monitoring and controlling

AWS CloudTrail: User activity tracking

**_Data Visualization:_**

Draw.io: ETL pipeline workflow visualization

## Deliverables
The key deliverable of this project is a fully functional data analytics platform that stores, processes, and provides descriptive insights into student misconduct complaints. This includes an end-to-end ETL pipeline designed using AWS Glue, facilitating data ingestion, cleaning, transformation, and enrichment, with organized storage in S3. Additionally, data security and governance are ensured through the use of AWS Identity and Access Management (IAM), Key Management Service (KMS), and data observability tools like CloudWatch and CloudTrail to maintain data integrity and observe data resources.

## Conclusion
The Student Rights and Responsibilities Data Analytics Platform helps track and analyze student misconduct complaints. It provides clear insights and supports better decision-making for the Registrar's Office and Student Rights & Responsibilities Advisor.
