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

<img width="700" alt="image" src="https://github.com/user-attachments/assets/3158ff59-20eb-409b-8fbf-7994c8230b78" /> <br>


### 2. Data Profiling
The next step is Data Profiling. The purpose of data profiling is to understand the data, such as if there are missing values or duplicate or invalid data. Some of the information can be used for data cleaning. Data profiling can be processed in AWS Glue DataBrew.

<img width="800" alt="image" src="https://github.com/user-attachments/assets/4e0da2b5-a5ba-4d0e-8c93-41260c815cb9" /> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/ba6b4e4a-a3dc-4a41-8e6a-582f71bd59e4" /> <br>

<img width="800" alt="image" src="https://github.com/user-attachments/assets/28fa42e0-d7be-440c-a201-04362e50fc12" /> <br>

After analyzing the data profiling, a project was created with this dataset to continue the data cleaning process

### 3. Data Cleaning
On the data cleaning step, there are some steps, such as removing white spaces for some columns, filling the missing values with the last valid value, renaming the column name and deleting empty rows with missing values. It can be processed in AWS Glue DataBrew. The cleaning dataset will be stored in *ro-trf-des> Complaints/ Data-Cleaning/*. In data cleaning folder, there are two folders, System and User. 

<img width="800" alt="image" src="https://github.com/user-attachments/assets/dd4e4ef3-dc94-4974-bf6e-77210758193f" /> <br>

<img width="700" alt="image" src="https://github.com/user-attachments/assets/556ddc26-1867-4ac3-a447-88e6a0891d3a" /> <br>




## Tools and Technologies
The project involves:


## Deliverables
The project involves:

## Conclusion
