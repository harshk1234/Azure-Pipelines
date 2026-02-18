# Azure-Pipelines

1. demonstrates a dynamic and scalable Azure Data Factory (ADF) pipeline that copies multiple tables from Azure SQL Database to Azure Data Lake Storage Gen2 using a ForEach loop and parameterized datasets. Instead of creating separate pipelines for each table, this solution dynamically iterates through a list of tables.

How It Works
createArray() expression generates a list of table names.
ForEach activity loops sequentially over each table.
Copy Activity:
Reads data from Azure SQL Database.
Uses parameterized dataset (tablename = @item()).
Writes output to ADLS Gen2 as .txt (CSV format).
Output folder dynamically created using table name.

pipeline:
<img width="562" height="377" alt="image" src="https://github.com/user-attachments/assets/8a429251-bf68-4d2b-8b3d-bcbba787161b" />

output:
<img width="508" height="137" alt="image" src="https://github.com/user-attachments/assets/86f1f555-3029-46a6-9836-6c291b88e0ea" />


2. This pipeline dynamically retrieves all tables from a specific SQL schema and copies them to ADLS Gen2 using a Lookup + ForEach pattern.

How It Works
Lookup Activity

Executes query:
SELECT table_name 
FROM information_schema.tables 
WHERE table_schema = 'SalesLT'

Returns list of tables dynamically.

ForEach Activity
Iterates over:
@activity('get table names').output.value

Copy Activity
Uses parameterized dataset:
@item().table_name
pipeline

<img width="698" height="382" alt="image" src="https://github.com/user-attachments/assets/8f190fcb-40e7-412f-a303-712665dcec76" />

output
<img width="590" height="300" alt="image" src="https://github.com/user-attachments/assets/61c9ab69-bd2e-4b76-81f9-925e0f01f671" />




Writes each table as .txt file in ADLS.

