# Table of Contents


# General Info
This is a data engineering project regarding Covid 19, assisted by a udemy course by Ramesh Retnasamy https://www.udemy.com/course/learn-azure-data-factory-from-scratch/


# Datasets
Confirmed cases, mortality, hospitalization/ICU cases, covid testing numbers, Country's population by age group from ECDC website (European Centre for Disease Control) 

# Technologies
**Storage:**
Azure Datalake Gen2
Azure Blob Storage

**Transformations:**
Databricks
HDInsight
Data Flows

**Orchestration:**
Azure Data Factory

# Setup

Setup HTTP connector in ADF to get data from website regarding conformed cases, mortality, hospitalization/ICU cases (3 files). 

Save populations file in Azure Blob Storage (to practise transferring to data lake through ADF). 


# Architecture

![alt text](https://user-images.githubusercontent.com/21047696/241493403-d0ea6b13-c593-4da9-b2a3-e026a704bee9.png)

Population data: ADF detects if population data lands in Azure Blob Storage through trigger. It invokes pipelines to 
copy the file into Azure Data Lake, raw file and delete it from Blob storage. 
apply transformations in Databricks and save the processed file into Data lake's 'proccessed' file.

**RAW POPULATION FILE**
![alt text](https://user-images.githubusercontent.com/21047696/241617306-0cb8ef26-9fa9-4130-9af8-62b637b0c1ab.png)

**TRANSFORMED POPULATION FILE**

![alt text](https://user-images.githubusercontent.com/21047696/241617300-6328f60b-7088-4b82-9764-a57ffc25620c.png)



Confirmed cases and hospital admissions data: ADF tumbling window triggers run everyday at midnight to access the website for data. 
ADF pipeline goes through a lookup list of files to get from the websiite and copies them to data lake. raw file. 
Additional triggers for proccessing in Data flow is invokes when the first trigger is successful. Data is transformed in Data flow and saved in processed file in data lake.
ADF also copies the files into Azure SQL Database so it can be accessed for analysis and dashboarding. 

Testing data:
For practise testing data was transformed in HD Insight.
Transformed files were copied into Azure SQL Database for analysis and dashboarding.


# Triggers 
