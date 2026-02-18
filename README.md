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

