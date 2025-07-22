# Celebal_Final_Project

**Overview**
This project demonstrates a complete implementation of an ETL pipeline using Azure Data Factory (ADF) and Azure Databricks to perform Change Data Capture (CDC) from a SQL Server source. The final output is stored in Azure Blob Storage, and an automated email notification is sent upon successful execution.
**Note:** This project was developed and executed on macOS using only cloud services.

**Tools and Services Used:**
Azure SQL Server (Cloud-hosted)
Azure Data Factory
Azure Databricks
Azure Blob Storage
GitHub (for source control)
Outlook (SMTP) for notifications

**SQL Tables Structure**

**Four base tables were created:**
1. Customer Table
2. Product Table
3. Order Table
4. Inventory Table

**Step-by-Step Implementation
Step 1: Data Preparation**

Created all 4 tables with sample data directly in Azure SQL Server.
Enabled CDC on each table via SQL commands.

**Step 2: Azure Data Factory Setup**

Created Linked Service for Azure SQL Database.
Created datasets for all 4 tables.
Designed ADF pipeline to extract and copy each table’s data to Azure Blob Storage.
Sink: CSV files stored inside cdc-output container.

**Step 3: Databricks Notebook - cdc_etl_pipeline.ipynb**

Mounted Azure Blob container using SAS Token.
Read raw data into Spark DataFrames.
Applied CDC logic (e.g., filter only changes using __$operation, timestamps).
Cleaned and transformed data.
Wrote processed output back to Blob Storage with coalesce(1).

**Step 4: Scheduled Execution**

ADF trigger created to run the notebook every 1 hour.
Ensured the notebook is correctly linked and tested with dummy changes.

**Step 5: Email Notification**

Used Web Activity in ADF to send an Outlook email.
Body includes status and blob path like: dbfs:/CDC_output/
Sample email received in inbox with the expected format.

**GitHub Integration**

Connected ADF to GitHub repository: SanchiM29/Celebal_Final_Project
Collaboration branch: main
Publish branch: adf_publish
Enabled import of existing pipelines, datasets, and triggers.

**Remarks**

All integrations done without SHIR, using SAS tokens and Azure services.
Entire pipeline was tested end-to-end multiple times.
Final emails are being received successfully.

**Sample Email Output**

Subject: CDC Pipeline Executed Successfully
Message:Hello,The CDC ETL pipeline has successfully run.
Latest data is available at: dbfs:/CDC_output/
Regards,
Sanchi

**Note: My Azure for Students subscription has been automatically disabled after usage limit was reached. All configurations, pipelines, and resources were fully functional during development and have been documented with screenshots in this repository.**



