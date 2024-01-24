# Azure End to End Data Engineering Pipeline

This project builds an End-to-End Azure Data Engineering Solution. A Pipeline performing Data Ingestion, ETL and Analytics all-in-one solution using Microsoft Azure Services and Power BI.

## Goal of the Project

The goal is to create an Azure solution which can take an On-premise Database such as the Microsoft SQL Server Management System (SSMS) and move it to the Cloud. It does so by building an ETL pipeline using Azure Data Factory, Azure Databricks and Azure Synapse Analytics.

The project is also connected to a reporting dashboard using Microsoft Power BI.

![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/22a54fc9-6cb9-4bfa-a3cc-c4cf31019ce3)


Data Migration to the Cloud is one of the most common scenarios the Data Engineers encounter when building solutions for a small-medium organization.
By working on this project, I was able to learn these skills:

* Data Ingestion
* ETL techniques using Azure Cloud Services
* Data Transformation
* Data Analytics and Dashboard Reporting
* Data Security and Governance


References: 
Mr. K Talks Tech video on E2E Azure Data Engineering Project 
[https://www.youtube.com/watch?v=iQ41WqhHglk&t=3624s]


## Prerequisites:

1) Microsoft SQL Server Managment System (SSMS)
2) Azure Subscription (Azure Data Lake Storage Gen2, Azure Data Factory, Azure Key Vault, Azure Databricks, Azure Synapse Analytics, Microsoft Entra ID)
3) Microsoft Power BI


The Database used for this project demonstration is:
AdventureWorks2022LT Sales Database
[https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms]

## Implementation:

### Part 1: Data Ingestion

1. Restore the Adventure Works Database from the .bak file.
   
![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/62507b81-59eb-48bb-a2b6-ebbca3314283)

3. Setup the Microsoft Integration Runtime between Azure and the On-premise SQL Server.
4. Create a Copy Pipeline which loads the data from local on-premise server into Azure Data Lake Storage Gen2 "bronze" directory.

Data is stored in "Parquet format" in ADLS Gen2 storage folders.

![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/d2126d21-6f67-4fd1-bfa8-0902c5182ddc)

### Part 2: Data Transformation

The Initial Data is cleaned and processed in two steps. Bronze to Silver and Silver to Gold. The Final Gold-level Data is suitable for business reporting and making dashboard visualizations.

We achieve this transformation by running PySpark powered notebooks using Azure Databricks and performing Schema manipulations and adjustments.

Gold-level data is in "Delta" format.

![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/cff35231-e9d0-4a82-b857-dfcc2845c7cb)


1. Launch Azure Databricks and run transformations using the notebooks "bronze to silver" and "silver to gold".

![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/782503d8-453b-4bc4-8b24-5a2417bff378)


### Part 3: Data Loading

Load the gold level data and run Synapse Pipeline to Create Views dynamically in Azure SQL Database

![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/7f935213-4dd9-471a-aa24-bc4b1c68f41b)


### Part 4: Data Reporting

Finally, load the data from the views using Microsoft Power BI. The Data is retrieved using DirectQuery to automatically run and update from the Synapse Cloud Pipelines.
An Interactive Dashboard is created to showcase the sales data figures.

![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/aabd6309-ef85-4ed9-af1a-171dbd7c2505)


### Part 5: End-to-end Pipeline Testing

Create a scheduled trigger in Azure Data Factory which will allow the pipeline to be run according to the schedule.

![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/d28f9c77-0027-4bb5-96f4-104109346f82)


Using this trigger, it makes it easy to automatically extract, load , transform the latest data. This data can be refreshed in Power BI from time to time.


* Before running the trigger:

![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/51405c5f-331a-4bbd-83cf-439f91ca2525)

* After running the trigger:

![image](https://github.com/Shashi42/Azure-End-to-End-Sales-Data-Analytics-Pipeline/assets/26250463/578aca35-89b1-4a31-b1e0-27fb7fd923ed)



## End Notes

* This project provides a great overview to many of Azure services such as Azure Data Factory, Azure Databricks, Azure Synapse Analytics.

* The resources we create in Azure can be secured by adding contributors into a Security Group. This feature is offered in Microsoft Entra ID (previously Azure Active Directory).
Thus, whoever belonging to the Security group can access and contribute to the project freely.

* The Database is although small, made it easier to visualize the scope and working of various services at once.





