# Azure-Pipelines

1. demonstrates a dynamic and scalable Azure Data Factory (ADF) pipeline that copies multiple tables from Azure SQL Database to Azure Data Lake Storage Gen2 using a ForEach loop and parameterized datasets. Instead of creating separate pipelines for each table, this solution dynamically iterates through a list of tables

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

Writes each table as .txt file in ADLS.

pipeline
<img width="698" height="382" alt="image" src="https://github.com/user-attachments/assets/8f190fcb-40e7-412f-a303-712665dcec76" />

output
<img width="590" height="300" alt="image" src="https://github.com/user-attachments/assets/61c9ab69-bd2e-4b76-81f9-925e0f01f671" />

3. Data should only be ingested into the data lake if the number of records exceeds a minimum threshold (e.g., 300 records).

   How It Works
   Step 1: Lookup Activity
   Executes a SQL query to count records in the source table

   SELECT COUNT(*) AS recordcount
   FROM salesLT.customer
   WHERE CustomerID < 500

Step 2: If Condition Activity (Decision Logic)
Evaluates the record count returned by the Lookup activity
@greater(activity('Lookup1').output.firstRow.recordcount,300)
Logic:
If record count > 300 → proceed with data copy
If record count ≤ 300 → skip data movement

Step 3: Copy Activity (Conditional Execution)
Executes only when the condition is TRUE

pipeline: 
<img width="558" height="358" alt="image" src="https://github.com/user-attachments/assets/17710280-7208-4a97-b794-242b4f4111ce" />
output:
<img width="773" height="91" alt="image" src="https://github.com/user-attachments/assets/1eec53c2-f119-4b0a-9530-00fd8339ba9c" />

   






