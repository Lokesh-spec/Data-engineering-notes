#bigquery #postgreSQL
# What is BigQuery?

BigQuery is Google Cloud's fully managed, serverless, and highly scalable data warehouse designed for large-scale data analytics. It allows users to run super-fast SQL queries on massive datasets without needing to manage infrastructure.

Here are some key features of BigQuery:
- **Fully Managed and Serverless**: BigQuery handles the infrastructure, so users can focus on data analysis without worrying about servers, storage, or scaling.
- **Real-Time Data Analysis**: It supports real-time data ingestion, making it ideal for applications where up-to-the-minute data is needed, such as streaming analytics.
- **SQL Querying**: BigQuery is compatible with standard SQL, making it accessible to users familiar with SQL-based databases. It also supports complex data types like arrays and structs.
- **Massive Scalability**: BigQuery can analyze terabytes or even petabytes of data quickly using Google’s infrastructure, which is optimized for large-scale data processing.
- **Integration with Other Google Cloud Services**: It works well with other Google Cloud products, such as Google Sheets, Google Data Studio, and AI/ML tools like Vertex AI, making it versatile for a range of analytics and machine learning tasks.
- **Data Security and Access Control**: BigQuery provides strong security features, including fine-grained access controls, encryption, and integration with Cloud Identity and Access Management (IAM) for managing permissions.
- **Flexible Pricing**: BigQuery offers on-demand pricing (pay for the amount of data processed per query) and flat-rate pricing (fixed monthly cost), which can help optimize costs depending on usage patterns.

BigQuery is widely used for analyzing large datasets, building data warehouses, and supporting real-time analytics for businesses in a scalable and cost-effective way.

## Data types

BigQuery supports a variety of data types to handle diverse data requirements. Here’s a breakdown of the main data types available in BigQuery:

### 1. Scalar Data Types

- **INT64**: 64-bit integer for storing whole numbers.
- **FLOAT64**: 64-bit floating-point number for handling decimal numbers.
- **NUMERIC**: Exact 38-digit precision for numbers (up to 9 decimal places), useful for financial and precise calculations.
- **BIGNUMERIC**: Extended precision with 76 digits (up to 38 decimal places), for larger or more precise numeric values.
- **BOOL**: Boolean type for storing true/false values.

### 2. String and Binary Types

- **STRING**: Variable-length UTF-8 encoded string for text data.
- **BYTES**: For binary data, useful for storing encoded data, files, or other binary objects.

### 3. Date and Time Types

- **DATE**: Calendar date (e.g., `YYYY-MM-DD`).
- **TIME**: Time of day without a date (e.g., `HH:MM:SS`).
- **DATETIME**: Combination of date and time (e.g., `YYYY-MM-DD HH:MM:SS`).
- **TIMESTAMP**: Exact point in time with timezone, stored in UTC (e.g., `2024-11-14 15:30:00 UTC`).
- **INTERVAL**: Represents a span of time, useful for time-based calculations.

### 4. Complex Data Types

- **ARRAY**: Ordered list of values of the same data type (e.g., `ARRAY<STRING>` for an array of strings). Arrays are useful for handling repeated fields.
- **STRUCT**: Collection of key-value pairs, where each field can have a name and type (like a JSON object or a row with named columns). For example, `STRUCT<name STRING, age INT64>`.

### 5. Geographic Data Types

- **GEOGRAPHY**: Represents geographic data, useful for GIS applications and spatial data. It allows for the storage of points, lines, and polygons based on Earth’s surface.

### 6. JSON Data Type

- **JSON**: Stores JSON-formatted data, useful for semi-structured data that doesn’t fit into traditional relational formats. This type allows parsing and querying of nested JSON structures.

### Type Conversion and Flexibility

BigQuery allows casting and converting between compatible types, which can be helpful when working with data that needs transformation. Some functions and operators are available for specific types, allowing for detailed data manipulations, aggregations, and filtering.

Each data type is designed to help BigQuery handle a wide range of analytics, from simple queries to complex, structured, and geospatial data.

### Creating Database / Dataset 

Creating a database (or technically, a "dataset" in BigQuery terminology) in BigQuery using the Google Cloud Console GUI is straightforward. Here’s how to create a dataset named `test_db` in the `my_first_project` project with the region set to `multi-region`:

1. **Open BigQuery Console**:
	- Go to the Google Cloud Console BigQuery page.
1. **Select Project**:
    - Ensure you’re working within your project, `my_first_project`. You can select the project from the dropdown list at the top of the console.
3. **Create Dataset**:
    - In the BigQuery Console, click on the **+ CREATE DATASET** button on the left panel.
4. **Dataset Configuration**:
    - In the **Create dataset** panel, enter the following details:
        - **Dataset ID**: Enter `db_1`.
        - **Data location**: Select a multi-region location, such as `US` or `EU`, depending on your needs. Note that BigQuery doesn’t support a global multi-region, so you'll need to choose between regions like `US` or `EU` for a multi-regional option.
5. **Other Dataset Settings** (optional):
    - **Default table expiration**: Set if you want tables in this dataset to expire automatically.
    - **Encryption**: Choose **Google-managed key** (default) or specify a Customer-managed key if required.
6. **Create**:
	- Click **Create dataset** to save the dataset configuration.

After completing these steps, the db_1 dataset will appear in the **Explorer** panel under `my_first_project`, and it will be ready to use for creating tables and running queries.

### Creating table using query

To create a table in BigQuery using the SQL syntax `CREATE TABLE IF NOT EXISTS`, you can use the following SQL query in the BigQuery Console:

```sql
CREATE TABLE IF NOT EXISTS db_1.customer_table (
  cust_id INT64,
  first_name STRING,
  last_name STRING,
  age INT64,
  email_id STRING
);
```

### Upload csv to BigQuery

To upload a file (e.g., `customer_data.csv`) from **Google Drive** to **BigQuery** using the **Google Cloud Console** or the **bq command-line tool**, follow these steps:

### Method 1: Upload File from Google Drive to BigQuery via Google Cloud Console

1. **Prepare the File in Google Drive**:
    - Make sure your `customer_data.csv` file is uploaded to **Google Drive**.
    - Ensure the file is accessible to your Google Cloud project (you may need to adjust sharing settings).
2. **Open BigQuery Console**:
    - Go to the Google Cloud Console.
    - Navigate to the **BigQuery** section by searching for **BigQuery** in the search bar or directly going to BigQuery Console.
3. **Create or Select a Dataset**:
    - In the BigQuery Console, on the left panel, expand your project.
    - Either select an existing dataset or create a new one by clicking the **+ CREATE DATASET** button.
4. **Load Data**:
    - After selecting the dataset, click on the **Create Table** button at the top of the page.
    - For **Create Table**, choose **Google Drive** as the **Source**.
5. **Select the Google Drive File**:
    - In the **Source** section, click **Browse** and enter the URL of the **Google Drive file**.
    - You’ll need to format the URL like: `drive://<file_id>` (replace `<file_id>` with the actual file ID from the file’s link).
    - Grant access to the file by clicking **Authorize** (if prompted).
6. **Set the Table Configuration**:
    - Set the **Destination** (Dataset and Table name).
    - Configure the schema (column names and types). You can either set this manually or let BigQuery auto-detect the schema based on the CSV structure.
7. **Configure Data Load Options**:
    - Choose the file format (`CSV`).
    - Set the **Delimiter** (typically `,` for CSV).
    - Set the **Field Options** (e.g., if the CSV has a header row, check "Header row").
8. **Create the Table**:
    - Once all configurations are done, click **Create Table**.

BigQuery will load the data from the Google Drive file into your BigQuery table.

### Method 2: Upload File from Google Drive to BigQuery using the `bq` Command-line Tool

1. **Install and Set Up the `bq` Tool**:
    
    - Install the Google Cloud SDK if you haven't already.
    - Authenticate with your Google Cloud account:
	 ``` bash
	     gcloud auth login
	 ```
2. **Get the File URL from Google Drive**:
    - Get the **file ID** from the file’s URL in Google Drive.
    - You can find the file ID in the URL of the file (e.g., `https://drive.google.com/file/d/<file_id>/view`).
3. **Share the File with Google Cloud**:
    - Ensure the file is shared with the Google Cloud project by setting proper permissions.
4. **Upload Using `bq` Command**: Use the `bq load` command to upload the CSV file directly to BigQuery. First, you need to download the file from Google Drive (since `bq` does not directly support Google Drive as a source). You can use the `gdrive` API, or download the file manually to your local machine and then upload it to BigQuery.
    - Here’s the general command structure for loading a CSV file from your local machine to BigQuery:
	   ``` bash
bq load --source_format=CSV --autodetect \   your_project_id:your_dataset_name.customer_table \   ./customer_data.csv
		```
    - `--source_format=CSV`: Specifies the format of the file.
    - `--autodetect`: Tells BigQuery to automatically detect the schema from the file.
    - `your_project_id:your_dataset_name.customer_table`: This specifies the destination dataset and table.
    - `./customer_data.csv`: Path to the CSV file (ensure you replace this with the correct path to the file you downloaded).

### Exercise

Make sure the `Student.csv` present in the `cloud SDK` folder

```bash
bq load --skip_leading_rows=1 classroom.science_class Student.csv
```

### Additional Option: Using Google Cloud Storage (GCS) as an Intermediate Step

If you prefer a more scalable solution, you can use **Google Cloud Storage (GCS)** as an intermediate step:

1. **Upload the File to Google Cloud Storage**:
    - Upload the CSV file from **Google Drive** to a **Google Cloud Storage bucket**.
    - This can be done manually via the Google Cloud Console or using `gsutil`:
        ``` bash
        gsutil cp customer_data.csv gs://your_bucket_name/
		```
2. **Load Data from Google Cloud Storage to BigQuery**:
    - Once the file is in Google Cloud Storage, you can load it to BigQuery using the `bq load` command:        
        ``` bash
    bq load --source_format=CSV --autodetect \   your_project_id:your_dataset_name.customer_table \   gs://your_bucket_name/customer_data.csv
		```

### SELECT in BigQuery 

In **BigQuery**, the queries you've mentioned are quite similar to what you'd see in SQL-based systems, but there are a few specifics related to BigQuery's environment. Here’s a breakdown of each query in simple terms:

1. **`SELECT first_name FROM db_1.cust_upload;`**
    - **What it does**: This query retrieves the **`first_name`** column from the `cust_upload` table in the dataset `db_1`.
    - **In BigQuery**: BigQuery allows querying across datasets, and here `db_1` is the dataset where the table `cust_upload` is stored.
    - **Result**: A list of first names from all the rows in the `cust_upload` table within the dataset `db_1`.
2. **`SELECT first_name, last_name FROM db_1.cust_upload;`**
    - **What it does**: This query retrieves both the **`first_name`** and **`last_name`** columns from the `cust_upload` table in the `db_1` dataset.
    - **In BigQuery**: Again, you are specifying a specific dataset (`db_1`) and table (`cust_upload`) to get two columns: `first_name` and `last_name`.
    - **Result**: A list of first names and last names from all the rows in the `cust_upload` table within `db_1`.
3. **`SELECT * FROM db_1.cust_upload;`**
    - **What it does**: This query retrieves **all columns** (`*` means all columns) from the `cust_upload` table in the `db_1` dataset.
    - **In BigQuery**: You are asking BigQuery to return all available data (all columns) from the `cust_upload` table in the dataset `db_1`.
    - **Result**: A full list of all columns and their values for every row in the `cust_upload` table.

### Key Points in BigQuery:

- **Dataset**: In BigQuery, a **dataset** is a container for your tables. It’s referenced as `db_1` in your queries.
- **Table**: The actual data resides in tables (e.g., `cust_upload`).
- **Column Names**: You are querying specific columns from a table (e.g., `first_name`, `last_name`), or using `*` to select all columns.

### Distinct in Biquery


```sql
SELECT DISTINCT cust_id FROM db_1.customer_table;
```
#### What it does:

- **`DISTINCT`**: This ensures that only **unique** values for the specified column (`cust_id`) are returned, eliminating any duplicates.
- **`cust_id`**: This specifies the column to retrieve the unique values from. In this case, it’s the `cust_id` column, which likely represents a unique identifier for customers.
- **`db_1.customer_table`**: This refers to the `customer_table` located in the `db_1` dataset (or schema) in the database.
#### Explanation:

- The query will return a list of **distinct customer IDs** from the `customer_table` in the `db_1` dataset, meaning if there are duplicate `cust_id` values, only one unique instance of each `cust_id` will be included in the result.
#### Example:

If the `customer_table` has the following data:

| cust_id |
| ------- |
| 101     |
| 102     |
| 101     |
| 103     |
| 102     |

The query would return:

| cust_id |
| ------- |
| 101     |
| 102     |
| 103     |

This removes the duplicate `cust_id` values and returns only the distinct ones.

### WHERE

```sql 
SELECT DISTINCT first_name, email_id FROM `db_1.customer_table` WHERE age > 30;
```

#### What it does:

- **`SELECT DISTINCT first_name, email_id`**: This selects the unique combinations of **`first_name`** and **`email_id`** columns. If the same pair of `first_name` and `email_id` appears multiple times, only one occurrence will be shown.
- **`FROM db_1.customer_table`**: This specifies the dataset (`db_1`) and the table (`customer_table`) you are querying from in BigQuery.
- **`WHERE age > 30`**: This condition filters the data, so only rows where the **age** is greater than 30 will be included in the results.
#### Explanation:

- The query retrieves unique pairs of `first_name` and `email_id` from the `customer_table` where the **age** is greater than 30.
- **`DISTINCT`** ensures that only one row is returned for each unique combination of `first_name` and `email_id`, even if there are duplicates in the table for the same `first_name` and `email_id` combination.
#### Example:

If the `customer_table` has the following data:

|first_name|email_id|age|
|---|---|---|
|John|john@example.com|35|
|Alice|alice@example.com|40|
|John|john@example.com|45|
|Bob|bob@example.com|33|
|Alice|alice@example.com|29|
|Carol|carol@example.com|32|

- **For `SELECT DISTINCT first_name, email_id FROM db_1.customer_table WHERE age > 30;`**  
    The result would be:

|first_name|email_id|
|---|---|
|John|john@example.com|
|Alice|alice@example.com|
|Bob|bob@example.com|
|Carol|carol@example.com|

### Summary:

- **`DISTINCT`** eliminates duplicate combinations of `first_name` and `email_id` in the result.
- **`WHERE age > 30`** filters the rows to only include customers older than 30 years.

### Logical Operator 

Here are the four queries in **BigQuery** format with explanations of a **database**  `db_1` and **table** is `customer_table`:
#### 1. Excluding rows where age is 25


``` sql
SELECT first_name, last_name, age  FROM `db_1.customer_table` WHERE NOT age = 25;
```

- **Explanation**:
    - This query selects **`first_name`**, **`last_name`**, and **`age`** columns from the `customer_table`.
    - The `WHERE NOT age = 25` condition filters out any rows where the **age** is 25.
    - The `NOT` operator negates the condition `age = 25`, so this returns all customers whose age is **not** 25.

**Example Data in `customer_table`:**

| first_name | last_name | age |
| ---------- | --------- | --- |
| John       | Doe       | 25  |
| Alice      | Smith     | 22  |
| Bob        | Johnson   | 19  |
| Carol      | Williams  | 28  |
| Dave       | Brown     | 25  |

**Result after query execution:**

| first_name | last_name | age |
| ---------- | --------- | --- |
| Alice      | Smith     | 22  |
| Bob        | Johnson   | 19  |
| Carol      | Williams  | 28  |


---

#### 2. Excluding rows where first name is 'John'

``` sql
SELECT first_name, last_name, age  FROM `db_1.customer_table` WHERE NOT first_name = 'John';
```

- **Explanation**:
    - This query selects **`first_name`**, **`last_name`**, and **`age`** columns from the `customer_table`.
    - The `WHERE NOT first_name = 'John'` condition filters out any rows where the **first name** is `'John'`.
    - The `NOT` operator negates the condition `first_name = 'John'`, so this returns all customers whose **first name is not 'John'**.

**Example Data in `customer_table`:**

|first_name|last_name|age|
|---|---|---|
|John|Doe|25|
|Alice|Smith|22|
|John|Johnson|19|
|Carol|Williams|28|
|Dave|Brown|31|

**Result after query execution:**

| first_name | last_name | age |
| ---------- | --------- | --- |
| Alice      | Smith     | 22  |
| Carol      | Williams  | 28  |
| Dave       | Brown     | 31  |

---

#### 3. Selecting customers whose age is between 20 and 30 (exclusive)

``` sql
SELECT first_name, last_name FROM `db_1.customer_table` WHERE age > 20 AND age < 30;
```

- **Explanation**:
    - This query selects the **`first_name`** and **`last_name`** columns from the `customer_table`.
    - The condition `WHERE age > 20 AND age < 30` filters the data to include only those rows where the **age** is **greater than 20** and **less than 30**.
    - This is a **range condition** that retrieves customers in the age group of 21 to 29.

**Example Data in `customer_table`:**

|first_name|last_name|age|
|---|---|---|
|John|Doe|25|
|Alice|Smith|22|
|Bob|Johnson|19|
|Carol|Williams|28|
|Dave|Brown|31|

**Result after query execution:**

| first_name | last_name |
| ---------- | --------- |
| John       | Doe       |
| Alice      | Smith     |
| Carol      | Williams  |

---

#### 4. Selecting customers where age is greater than 20, less than 20, or first name is 'John'

``` sql
SELECT first_name, last_name FROM `db_1.customer_table` WHERE age > 20 OR age < 20 OR first_name = 'John';
```


- **Explanation**:
    - This query selects the **`first_name`** and **`last_name`** columns from the `customer_table`.
    - The condition `WHERE age > 20 OR age < 20 OR first_name = 'John'` means **any** of the following conditions can be true for a row to be included in the result:
        1. The **age is greater than 20**.
        2. The **age is less than 20**.
        3. The **first name is 'John'**.
    - Since **OR** is used, a row will be returned if it satisfies **at least one** of these conditions. If a customer has an age above 20, below 20, or their first name is 'John', they will appear in the result.

**Example Data in `customer_table`:**

|first_name|last_name|age|
|---|---|---|
|John|Doe|25|
|Alice|Smith|22|
|Bob|Johnson|19|
|Carol|Williams|28|
|Dave|Brown|17|

**Result after query execution:**

| first_name | last_name |
| ---------- | --------- |
| John       | Doe       |
| Alice      | Smith     |
| Bob        | Johnson   |
| Carol      | Williams  |
| Dave       | Brown     |

---
### Summary of Each Query:

- **Query 1**: Excludes customers who are 25 years old.
- **Query 2**: Excludes customers whose first name is 'John'.
- **Query 3**: Selects customers whose age is strictly between 20 and 30.
- **Query 4**: Selects customers who are either older than 20, younger than 20, or have the first name 'John'.

These queries are written for **BigQuery** in the format `db_1.customer_table`, following the syntax conventions used in BigQuery SQL.


In BigQuery, the `UPDATE` statement works similarly to SQL but with some differences, such as the need for a specific `FROM` clause when updating a table based on certain conditions. Here’s how the query would look in BigQuery:

---

### UPDATE
#### Query in BigQuery:

```sql
UPDATE `db_1.customer_table` SET last_name = 'pe' WHERE cust_id = 2;
```

### Explanation:

- **UPDATE `db_1.customer_table`**: This specifies that you want to update the `customer_table` in the `db_1` dataset.
- **SET last_name = 'pe'**: This sets the `last_name` column to `'pe'` for the rows where the condition is true.
- **WHERE cust_id = 2**: This condition ensures that only the row where `cust_id = 2` gets updated.
### Example Before and After the Update:

**Before the Update:**

|cust_id|first_name|last_name|age|
|---|---|---|---|
|1|John|Doe|25|
|2|Alice|Smith|30|
|3|Bob|Johnson|22|

**After the Update:**

|cust_id|first_name|last_name|age|
|---|---|---|---|
|1|John|Doe|25|
|2|Alice|pe|30|
|3|Bob|Johnson|22|

In this example, the `last_name` of the customer with `cust_id = 2` (Alice) was successfully updated to `'pe'` in BigQuery.

---

### DELETE

In BigQuery, the `DELETE` statement is used similarly to SQL, but it has some specific syntax and limitations, such as working with partitions or specific filters on large datasets.

Here’s how to perform a `DELETE` in BigQuery:
### General Syntax for `DELETE` in BigQuery:

``` sql
DELETE FROM `project_id.dataset_id.table_name` WHERE condition;
```

- **`project_id.dataset_id.table_name`**: The fully qualified name of the table you are updating, which includes the project ID, dataset ID, and table name.
- **`condition`**: The condition that specifies which rows to delete.
### Example: Deleting a Row from `customer_table` in BigQuery

Let’s assume you want to delete the record of a customer with `cust_id = 2` from the `customer_table` in the `db_1` dataset of your BigQuery project.
### Query:

``` sql
DELETE FROM `db_1.customer_table` WHERE cust_id = 2;
```

### Explanation:

- **DELETE FROM `db_1.customer_table`**: This specifies that you want to delete data from the `customer_table` in the `db_1` dataset.
- **WHERE cust_id = 2**: This condition ensures that only the row where `cust_id = 2` is deleted.
### Example Before and After the DELETE Operation:

**Before the DELETE operation:**

|cust_id|first_name|last_name|age|
|---|---|---|---|
|1|John|Doe|25|
|2|Alice|Smith|30|
|3|Bob|Johnson|22|

**After the DELETE operation (where `cust_id = 2`):**

|cust_id|first_name|last_name|age|
|---|---|---|---|
|1|John|Doe|25|
|3|Bob|Johnson|22|

In the above example, the row where `cust_id = 2` (Alice) was deleted.

### Important Notes:

- **Partitioned tables**: If you’re working with partitioned tables, you can only delete from partitions that are available for deletion.
- **Deletion limits**: BigQuery charges for deletes on large tables, so keep in mind that there might be costs involved with deleting large amounts of data.

---

### ALTER

In BigQuery, the `ALTER TABLE` functionality is somewhat limited compared to PostgreSQL, especially when it comes to operations like modifying column data types or adding certain types of constraints (e.g., primary key or foreign key). However, you can still perform some of the operations like adding and renaming columns, and adding partitioning or clustering options. Let's walk through how to perform similar tasks using BigQuery, assuming a table named `customer_table` in dataset `db_1`.

### Example: `customer_table` in BigQuery

Assuming the `customer_table` structure as:

|cust_id|first_name|last_name|age|
|---|---|---|---|
|1|John|Doe|25|
|2|Alice|Smith|30|
|3|Bob|Johnson|22|

#### 1. Add a Column

To add a new column `email` to the `customer_table`:

```sql
ALTER TABLE `db_1.customer_table` ADD COLUMN email STRING;
```

This adds the `email` column with a `STRING` data type.

#### 2. Drop a Column

BigQuery does not support dropping columns directly. Instead, you need to recreate the table without the column you want to drop. Here's how:

1. Create a new table with the desired columns:
	    ``` CREATE OR REPLACE TABLE `db_1.customer_table` AS SELECT cust_id, first_name, last_name, age FROM `db_1.customer_table  ```
	    
    This query creates a new `customer_table` without the `email` column (or any other unwanted columns).
    
2. The original table (`customer_table`) can then be dropped if necessary.
    

#### 3. Modify a Column

BigQuery doesn't support changing the data type of an existing column directly. You would need to create a new table with the updated column definition, then insert the data from the original table.

For example, if you wanted to change the `age` column data type from `INTEGER` to `FLOAT64`:

1. Create a new table with the desired column type:
		
    ``CREATE OR REPLACE TABLE `db_1.customer_table` AS SELECT cust_id, first_name, last_name, CAST(age AS FLOAT64) AS age FROM `db_1.customer_table`;``
    
    This will recreate the table with `age` as `FLOAT64` instead of `INTEGER`.
    

#### 4. Rename a Column

To rename a column, you would need to create a new table with the updated column name:

``CREATE OR REPLACE TABLE `db_1.customer_table` AS SELECT cust_id, first_name, AS surname FROM `db_1.customer_table`;``

This renames the `last_name` column to `surname` by creating a new table with the updated name.

#### 5. Rename the Table

To rename a table in BigQuery, you can't use `ALTER TABLE`. Instead, you need to create a new table with the desired name and then delete the old one:

``CREATE OR REPLACE TABLE `db_1.clients_table` AS SELECT * FROM `db_1.customer_table`;``

This renames `customer_table` to `clients_table`.

### 6. Add Partitioning

If you want to add partitioning (e.g., partitioning by `age`):

``CREATE OR REPLACE TABLE `db_1.customer_table` PARTITION BY age AS SELECT * FROM `db_1.customer_table`;``

This partitions the table by the `age` column.

#### 7. Add Clustering

BigQuery allows adding clustering to a table:

``CREATE OR REPLACE TABLE `db_1.customer_table` CLUSTER BY first_name AS SELECT * FROM `db_1.customer_table`;``

This will cluster the `customer_table` by `first_name`.

#### 8. Adding Constraints

BigQuery does **not** support adding constraints like `PRIMARY KEY`, `FOREIGN KEY`, or `CHECK` directly to a table. You would need to handle these kinds of constraints at the application level or through data validation in your ETL pipeline.

However, for data integrity, you can enforce uniqueness or referential integrity in your queries, like using `DISTINCT`, `JOIN`, or `GROUP BY`.

For example, to ensure that `cust_id` is unique (manually ensuring it):

``SELECT DISTINCT cust_id FROM `db_1.customer_table`;``

#### Summary of BigQuery Operations for `customer_table`:

1. **Add a Column**:
    
    ``ALTER TABLE `db_1.customer_table` ADD COLUMN email STRING;``
    
2. **Drop a Column** (workaround):
    
    ``CREATE OR REPLACE TABLE `db_1.customer_table` AS SELECT cust_id, first_name, last_name, age FROM `db_1.customer_table`;``
    
3. **Modify a Column** (workaround):

    ``CREATE OR REPLACE TABLE `db_1.customer_table` AS SELECT cust_id, first_name, last_name, CAST(age AS FLOAT64) AS age FROM `db_1.customer_table`;``
    
4. **Rename a Column** (workaround):
    
    ``CREATE OR REPLACE TABLE `db_1.customer_table` AS SELECT cust_id, first_name, last_name AS surname, age FROM `db_1.customer_table`;``
    
5. **Rename the Table** (workaround):
    

    
    ``CREATE OR REPLACE TABLE `db_1.clients_table` AS SELECT * FROM `db_1.customer_table`;``
    
6. **Add Partitioning**:
    
    ``CREATE OR REPLACE TABLE `db_1.customer_table` PARTITION BY age AS SELECT * FROM `db_1.customer_table`;``
    
7. **Add Clustering**:
    
    ``CREATE OR REPLACE TABLE `db_1.customer_table` CLUSTER BY first_name AS SELECT * FROM `db_1.customer_table`;``
    
8. **Add Constraints** (handled at the application level, no direct support in BigQuery).

BigQuery is optimized for analytics and supports a different set of operations compared to traditional relational databases like PostgreSQL. Let me know if you need further details!

---



---
# What is PostgreSQL?

PostgreSQL is an open-source, powerful, and advanced relational database management system (RDBMS) known for its reliability, performance, and robust feature set. It's designed to handle a wide range of data workloads, from simple applications to complex data analytics and large-scale data warehousing. Here’s an overview of PostgreSQL's key features and strengths:

1. **ACID Compliance**: PostgreSQL is fully ACID-compliant (Atomicity, Consistency, Isolation, Durability), ensuring reliable transactions and high data integrity.
2. **Relational and Non-Relational Capabilities**: It supports traditional relational data with tables, rows, and columns, as well as complex data types like JSON, JSONB (binary JSON for faster processing), arrays, and hstore (for key-value pairs).
3. **Advanced SQL Compliance**: PostgreSQL is highly SQL-compliant, supporting advanced SQL functions, complex queries, joins, indexing, and more. It adheres to many SQL standards, making it suitable for a wide range of applications.
4. **Extensibility**: One of PostgreSQL’s standout features is its extensibility. Users can define custom functions, data types, operators, and even add procedural languages, enabling deep customization for specific applications.
5. **MVCC for Concurrency**: PostgreSQL uses Multiversion Concurrency Control (MVCC), which allows multiple transactions to occur simultaneously without locking rows, improving performance and supporting high concurrency.
6. **Strong Community and Ecosystem**: PostgreSQL is supported by a large community that continuously enhances it, providing tools, extensions (like PostGIS for geographic data), and documentation.
7. **Replication and Clustering**: PostgreSQL supports streaming replication and logical replication for creating replicas and distributing data across multiple servers, aiding in load balancing and high availability.
8. **Security Features**: PostgreSQL provides robust security, including authentication, data encryption, and access controls. It integrates with LDAP, SSL, and other security protocols for secure data handling.
9. **Cross-Platform**: PostgreSQL is compatible with various operating systems (e.g., Linux, Windows, macOS), making it flexible for deployment across different environments.
10. **Open Source and Free**: PostgreSQL is open-source under the PostgreSQL License, a permissive license similar to MIT. This allows users to freely use, modify, and distribute PostgreSQL, making it cost-effective for businesses.

Because of its versatility and extensive features, PostgreSQL is widely used for web applications, data warehousing, data science, and geographic information systems (GIS), among other applications.

## Data types

PostgreSQL offers a wide array of data types to handle various data formats and requirements. Here’s a rundown of PostgreSQL’s key data types:

### 1. Numeric Types

- **SMALLINT**: 2-byte integer, ranging from -32,768 to +32,767.
- **INTEGER (INT)**: 4-byte integer, ranging from -2,147,483,648 to +2,147,483,647.
- **BIGINT**: 8-byte integer, for larger whole numbers.
- **NUMERIC (DECIMAL)**: Exact numeric type with configurable precision and scale, ideal for financial calculations (e.g., `NUMERIC(10, 2)` for two decimal places).
- **REAL**: 4-byte floating-point number, approximate precision.
- **DOUBLE PRECISION**: 8-byte floating-point number with higher precision.
- **SERIAL** and **BIGSERIAL**: Auto-incrementing integer types, often used for primary keys.

### 2. Monetary Types

- **MONEY**: Stores currency amounts with a fixed fractional precision. Useful for financial applications, though often replaced by `NUMERIC` for flexibility.

### 3. Character Types

- **CHAR(n)**: Fixed-length character type, right-padded with spaces (e.g., `CHAR(5)`).
- **VARCHAR(n)**: Variable-length character type with a specified limit (e.g., `VARCHAR(255)`).
- **TEXT**: Variable-length string with unlimited length, ideal for large text fields.

### 4. Binary Types

- **BYTEA**: Variable-length binary data. Commonly used for storing binary data like files or images.

### 5. Date and Time Types

- **DATE**: Stores dates only (e.g., `YYYY-MM-DD`).
- **TIME**: Stores time of day only, without time zone (e.g., `HH:MM:SS`).
- **TIME WITH TIME ZONE**: Time of day including time zone.
- **TIMESTAMP**: Stores both date and time (e.g., `YYYY-MM-DD HH:MM:SS`).
- **TIMESTAMP WITH TIME ZONE**: Date and time including time zone (referred to as `timestamptz`).
- **INTERVAL**: Represents a duration or span of time (e.g., `INTERVAL '1 day'`).

### 6. Boolean Type

- **BOOLEAN**: Stores `TRUE`, `FALSE`, or `NULL`. Useful for binary state fields.

### 7. Enumerated Types (ENUM)

- **ENUM**: Allows the creation of a custom type with a predefined set of values (e.g., `CREATE TYPE mood AS ENUM ('happy', 'sad', 'neutral');`). This is useful for fields with a limited set of options.

### 8. Geometric Types

- **POINT, LINE, LSEG, BOX, PATH, POLYGON, CIRCLE**: These types are for storing geometric data, such as points, lines, and shapes, useful for spatial applications.

### 9. Network Address Types

- **CIDR**: IPv4 or IPv6 network.
- **INET**: IPv4 or IPv6 host address.
- **MACADDR**: MAC address type, useful for storing network-related data.

### 10. JSON and JSONB Types

- **JSON**: Stores JSON data as text, ideal for simple JSON documents.
- **JSONB**: Binary storage format for JSON, allowing efficient indexing and querying of JSON data. Recommended for complex JSON structures.

### 11. UUID Type

- **UUID**: 128-bit universally unique identifier, useful for keys or unique identifiers.

### 12. Array Type

- **ARRAY**: PostgreSQL supports arrays of any data type (e.g., `INT[]`, `TEXT[]`). This can be useful for storing lists of values.

### 13. Range Types

- **INT4RANGE, INT8RANGE, NUMRANGE, TSRANGE, TSTZRANGE, DATERANGE**: These types represent ranges of values, such as date ranges or numeric ranges, and are useful for scheduling and time-based applications.

### 14. Composite Types

- Composite types allow combining multiple fields into a single field (similar to structs). They can be created from table structures or custom definitions.

### 15. XML Type

- **XML**: For storing XML data, supporting functions to parse, query, and manipulate XML documents.

### 16. Special Types

- **TSVECTOR**: Full-text search type, used for indexing and searching text.
- **TSQUERY**: Used to represent search queries for full-text search.

PostgreSQL’s broad set of data types makes it flexible and capable of handling diverse data needs across a range of applications, from standard relational tasks to specialized JSON, spatial, and text-search applications.

### Creating Database in PostgreSQL

Here’s how to create a database in **pgAdmin** (PostgreSQL GUI) in simple steps:

1. **Open pgAdmin**: Launch the **pgAdmin** tool.
2. **Connect to Server**: On the left side, right-click **Servers** and click **Connect to Server**. Enter your login details.
3. **Create Database**:
	- Right-click on **Databases** and select **Create > Database**.
	- Name your database (e.g., `db_1`).
	- Click **Save**.

### Creating Table in PostgreSQL

```sql 
CREATE TABLE IF NOT EXISTS customer_table (
	cust_id INT,
	first_name VARCHAR,
	last_name VARCHAR,
	age SMALLINT,
	email_id VARCHAR
);
```

### Copying Data from a CSV File:

```sql 
COPY customer_table FROM 'C:\Program Files\PostgreSQL\17\data\data_copy\copy.csv'
DELIMITER ',' CSV HEADER;
```

- **Explanation**: This command copies data from a CSV file located at `C:\Program Files\PostgreSQL\17\data\data_copy\copy.csv` into the `customer_table` table.
- **CSV HEADER**: This tells PostgreSQL that the first row of the CSV file contains column names, so it will ignore that row for inserting data.

### Copying Data from a Text File:

```sql
COPY customer_table FROM 'C:\Program Files\PostgreSQL\17\data\data_copy\copytext.txt' 
DELIMITER ',';
```

- **Explanation**: This command copies data from a plain text file (`copytext.txt`) into the `customer_table` table. It assumes that the fields in the text file are separated by commas.

### Exercise

Make sure the `Student.csv` file present in the `Postgres\17\data\data_copy` folder

```sql
COPY science_class FROM 'C:\Program Files\PostgreSQL\17\data\data_copy\Student.csv' 
DELIMITER ',' HEADER;
```

### SELECT in Postgres

Here’s a simple explanation for each of your SQL queries:

1. **`SELECT first_name FROM customer_table;`**
    - **What it does**: This query asks the database to show you only the **first_name** column from the `customer_table`. It will display all the values from the **first_name** column for every record in the table.
    - **Result**: A list of first names from all the rows in `customer_table`.
2. **`SELECT first_name, last_name FROM customer_table;`**
    - **What it does**: This query asks the database to show you both the **first_name** and **last_name** columns from the `customer_table`. It will display both values for every record in the table.
    - **Result**: A list of first names and last names from all the rows in `customer_table`.
3. **`SELECT * FROM customer_table;`**
    - **What it does**: This query asks the database to show you **all columns** (`*` means all columns) from the `customer_table`. It will display all the data available in every column for every row in the table.
    - **Result**: A full list of all columns and their values for every record in `customer_table`.

---
#### Distinct

In **PostgreSQL**, the query:
```sql
SELECT DISTINCT first_name FROM customer_table;
```


##### What it does:

- **`DISTINCT`**: This keyword ensures that the query will return **only unique (non-duplicate)** values from the specified column.
- **`first_name`**: This specifies the column you want to retrieve.
- **`customer_table`**: This is the name of the table from which you are selecting the data.
#####  Explanation:
- The query selects all the **unique first names** from the `customer_table`.
- If the table has multiple rows with the same `first_name`, **only one occurrence** of each unique first name will be returned.
##### Example:
If the `customer_table` has the following data:

|first_name|
|---|
|John|
|Alice|
|John|
|Bob|
|Alice|

The query would return:

| first_name |
| ---------- |
| John       |
| Alice      |
| Bob        |

It removes duplicates and only shows distinct first names.
### Where 

Here’s what each of these queries does:

1. **`SELECT first_name FROM customer_table WHERE age = 25;`**
    - **What it does**: This query retrieves the **first_name** column from the `customer_table` but **only for rows where the age is exactly 25**.
    - **Explanation**: It filters the rows based on the condition `age = 25`. Only customers with an age of 25 will have their `first_name` shown in the result.
2. **`SELECT first_name FROM customer_table WHERE age > 25;`**
    - **What it does**: This query retrieves the **first_name** column from the `customer_table` but **only for rows where the age is greater than 25**.
    - **Explanation**: It filters the rows based on the condition `age > 25`. Only customers older than 25 will have their `first_name` shown in the result.
3. **`SELECT first_name FROM customer_table WHERE age < 25;`**
    - **What it does**: This query retrieves the **first_name** column from the `customer_table` but **only for rows where the age is less than 25**.
    - **Explanation**: It filters the rows based on the condition `age < 25`. Only customers younger than 25 will have their `first_name` shown in the result.
### Example:

If the `customer_table` has the following data:

| first_name | age |
| ---------- | --- |
| John       | 24  |
| Alice      | 25  |
| Bob        | 26  |
| Carol      | 23  |
| Dave       | 27  |

- **For `SELECT first_name FROM customer_table WHERE age = 25;`**  
    The result would be:
    |`Alice|`
    
- **For `SELECT first_name FROM customer_table WHERE age > 25;`**  
    The result would be:
     `|Bob|`
     `|Dave|`
     
- **For `SELECT first_name FROM customer_table WHERE age < 25;`**  
    The result would be:
    `|John|
    `|Carol|`

### Logical Operator

1. **`SELECT first_name, last_name FROM customer_table WHERE age > 20 AND age < 30;`**

	- **What it does**: This query retrieves the **`first_name`** and **`last_name`** columns from the `customer_table` where the **age** is **between 20 and 30** (exclusive).
	- **Explanation**: The condition `age > 20 AND age < 30` means that it selects rows where the age is **greater than 20 and less than 30**.
#### Example:

If the `customer_table` has the following data:

|first_name|last_name|age|
|---|---|---|
|John|Doe|25|
|Alice|Smith|22|
|Bob|Johnson|19|
|Carol|Williams|28|
|Dave|Brown|31|

- The query will return:

|first_name|last_name|
|---|---|
|John|Doe|
|Alice|Smith|
|Carol|Williams|

It excludes Bob (age 19) and Dave (age 31) because their ages are outside the specified range.

---

2. **`SELECT first_name, last_name FROM customer_table WHERE age > 20 OR age < 20 OR first_name = 'John';`**

	- **What it does**: This query retrieves the **`first_name`** and **`last_name`** columns from the `customer_table` where **any of the conditions** are true:
	    1. **`age > 20`**: The age is greater than 20.
	    2. **`age < 20`**: The age is less than 20.
	    3. **`first_name = 'John'`**: The `first_name` is 'John'.
	- **Explanation**: Since the **`OR`** operator is used, only **one of the conditions** needs to be true for the row to be included in the result. So, this query will select all customers who are either:
	    - Older than 20,
	    - Younger than 20,
	    - Or have the first name 'John' (regardless of age).

#### Example:

If the `customer_table` has the following data:

|first_name|last_name|age|
|---|---|---|
|John|Doe|25|
|Alice|Smith|22|
|Bob|Johnson|19|
|Carol|Williams|28|
|Dave|Brown|17|

- The query will return:

|first_name|last_name|
|---|---|
|John|Doe|
|Alice|Smith|
|Bob|Johnson|
|Carol|Williams|
|Dave|Brown|

This is because:

- Alice, Bob, Carol, and Dave are included because their ages meet the conditions (`age > 20` or `age < 20`).
- John is also included because his `first_name` is 'John', which satisfies the condition `first_name = 'John'`

---

 3. **`SELECT first_name, last_name, age FROM customer_table WHERE NOT age = 25;`**
 
	- **What it does**: This query retrieves the **`first_name`**, **`last_name`**, and **`age`** columns from the `customer_table`, but **excludes rows where the age is 25**.
	- **Explanation**: The `NOT age = 25` condition means that it selects all rows where the age is **not equal to 25**. It acts as an exclusion filter for age 25.

#### Example:

If the `customer_table` has the following data:

|first_name|last_name|age|
|---|---|---|
|John|Doe|25|
|Alice|Smith|22|
|Bob|Johnson|19|
|Carol|Williams|28|
|Dave|Brown|25|

- The query will return:

|first_name|last_name|age|
|---|---|---|
|Alice|Smith|22|
|Bob|Johnson|19|
|Carol|Williams|28|

**John** and **Dave** are excluded because their ages are 25.

---

4. **`SELECT first_name, last_name, age FROM customer_table WHERE NOT first_name = 'John';`**

- **What it does**: This query retrieves the **`first_name`**, **`last_name`**, and **`age`** columns from the `customer_table`, but **excludes rows where the first name is 'John'**.
- **Explanation**: The `NOT first_name = 'John'` condition means that it selects all rows where the `first_name` is **not equal to 'John'**. It acts as an exclusion filter for the name 'John'.

#### Example:

If the `customer_table` has the following data:

|first_name|last_name|age|
|---|---|---|
|John|Doe|25|
|Alice|Smith|22|
|John|Johnson|19|
|Carol|Williams|28|
|Dave|Brown|31|

- The query will return:

|first_name|last_name|age|
|---|---|---|
|Alice|Smith|22|
|Carol|Williams|28|
|Dave|Brown|31|

Both **John** rows are excluded from the result because of the `NOT first_name = 'John'` condition.
### Summary:

- **First query**: It filters customers with ages strictly between 20 and 30 (exclusive).
- **Second query**: It selects all customers who meet at least one of the following conditions: age is greater than 20, age is less than 20, or their first name is 'John'.
-  **Third query**: Excludes customers whose age is 25.
- **Fourth query**: Excludes customers whose first name is 'John'.

---

### UPDATE 

The SQL query you provided updates the `customer_table` to change the `last_name` of the customer with `cust_id = 2`. Here's a breakdown of the query:
#### Query:

```sql
UPDATE customer_table SET last_name = 'pe' WHERE cust_id = 2;
```

### Explanation:

- **UPDATE customer_table**: This tells the database that you want to modify the data in the `customer_table`.
- **SET last_name = 'pe'**: This specifies that you want to change the value of the `last_name` column to `'pe'`.
- **WHERE cust_id = 2**: This condition restricts the update to only the row(s) where the `cust_id` is 2. This ensures that only the customer with `cust_id = 2` will have their `last_name` updated.\
### Example Before and After the Update:

**Before the Update:**

|cust_id|first_name|last_name|age|
|---|---|---|---|
|1|John|Doe|25|
|2|Alice|Smith|30|
|3|Bob|Johnson|22|

**After the Update:**

|cust_id|first_name|last_name|age|
|---|---|---|---|
|1|John|Doe|25|
|2|Alice|pe|30|
|3|Bob|Johnson|22|

In the above example, the `last_name` of the customer with `cust_id = 2` (Alice) was updated to `'pe'`.

---

### DELETE

In PostgreSQL, the `DELETE` statement is used to remove rows from a table based on a specified condition.

Here’s the structure and an example of how to use the `DELETE` statement in PostgreSQL:
#### General Syntax for `DELETE` in PostgreSQL:

``` sql
DELETE FROM table_name WHERE condition;
```

- **`table_name`**: The name of the table from which you want to delete data.
- **`condition`**: A condition that specifies which rows to delete. If no condition is specified, **all rows** in the table will be deleted.
### Example: Deleting a Row from `customer_table`

Let's assume you want to delete the record of a customer with `cust_id = 2` from the `customer_table`.
### Query:

``` sql
DELETE FROM customer_table WHERE cust_id = 2;
```
### Explanation:

- **DELETE FROM customer_table**: This specifies that you want to delete data from the `customer_table`.
- **WHERE cust_id = 2**: This condition limits the deletion to the row where the `cust_id` is `2`.

### Example Before and After the `DELETE` Operation:

**Before the DELETE operation:**

| cust_id | first_name | last_name | age |
| ------- | ---------- | --------- | --- |
| 1       | John       | Doe       | 25  |
| 2       | Alice      | Smith     | 30  |
| 3       | Bob        | Johnson   | 22  |

**After the DELETE operation (where `cust_id = 2`):**

| cust_id | first_name | last_name | age |
| ------- | ---------- | --------- | --- |
| 1       | John       | Doe       | 25  |
| 3       | Bob        | Johnson   | 22  |

In the example above, the row where `cust_id = 2` (Alice) is deleted from the table.

### Important Notes:

- **Without a `WHERE` clause**: If you run a `DELETE` statement without a `WHERE` clause, it will delete **all rows** in the table.

    Example:
    
	 ``` sql
	 DELETE FROM customer_table;
	```
    
    This would delete every row in the `customer_table`.

---
### ALTER

In PostgreSQL, you can modify tables using the `ALTER TABLE` statement to add, drop, modify, or rename columns and apply constraints. Below are the different variations and examples of how to use `ALTER TABLE` for these operations.

#### Example: `customer_table`

Let’s assume the `customer_table` has the following structure:

|cust_id|first_name|last_name|age|
|---|---|---|---|
|1|John|Doe|25|
|2|Alice|Smith|30|
|3|Bob|Johnson|22|

#### 1. Add a Column

To add a new column `email` to the `customer_table`:

``` sql 
ALTER TABLE customer_table ADD COLUMN email VARCHAR(255);
```

This adds the `email` column with a data type of `VARCHAR(255)`.

#### 2. Drop a Column

To drop the `email` column from the `customer_table`:

``` sql
ALTER TABLE customer_table DROP COLUMN email;
```

This deletes the `email` column from the table.
#### 3. Modify a Column

To change the `age` column data type from `INTEGER` to `BIGINT`:

``` sql
ALTER TABLE customer_table ALTER COLUMN age SET DATA TYPE BIGINT;
```

This modifies the `age` column to a larger data type `BIGINT` to accommodate larger values.
#### 4. Rename a Column

To rename the column `last_name` to `surname`:

``` sql
ALTER TABLE customer_table RENAME COLUMN last_name TO surname;
```

This renames the `last_name` column to `surname`.
#### 5. Rename the Table

To rename the `customer_table` to `clients_table`:

``` sql
ALTER TABLE customer_table RENAME TO clients_table;
```

This renames the entire table from `customer_table` to `clients_table`.
#### 6. Add a Primary Key Constraint

To add a primary key constraint on the `cust_id` column:

``` sql
ALTER TABLE customer_table ADD CONSTRAINT pk_customer PRIMARY KEY (cust_id);
```

This makes the `cust_id` column the primary key of the table.
#### 7. Add a Foreign Key Constraint

Suppose we have another table called `orders` with a `cust_id` column, and we want to establish a foreign key relationship between `orders` and `customer_table`.

``` sql
ALTER TABLE orders ADD CONSTRAINT fk_customer FOREIGN KEY (cust_id) REFERENCES customer_table (cust_id);
```

This ensures that every `cust_id` in the `orders` table must exist in the `customer_table` as a valid `cust_id`.

#### 8. Add a Unique Constraint

To add a unique constraint to the `email` column to ensure no two customers can have the same email:

``` sql
ALTER TABLE customer_table ADD CONSTRAINT unique_email UNIQUE (email);
```

This ensures that every email in the `customer_table` is unique.
#### 9. Add a Check Constraint

To ensure that the `age` column only accepts values greater than 18:

``` sql
ALTER TABLE customer_table ADD CONSTRAINT check_age CHECK (age > 18);
```

This adds a check constraint ensuring that every value in the `age` column is greater than 18.

#### 10. Drop a Constraint

To drop the primary key constraint `pk_customer`:

```sql
ALTER TABLE customer_table DROP CONSTRAINT pk_customer;
```

This removes the primary key constraint on the `cust_id` column.

#### Summary of Operations for `customer_table`:

1. **Add a Column**:  
    `ALTER TABLE customer_table ADD COLUMN email VARCHAR(255);`
    
2. **Drop a Column**:  
    `ALTER TABLE customer_table DROP COLUMN email;`
    
3. **Modify a Column**:  
    `ALTER TABLE customer_table ALTER COLUMN age SET DATA TYPE BIGINT;`
    
4. **Rename a Column**:  
    `ALTER TABLE customer_table RENAME COLUMN last_name TO surname;`
    
5. **Rename a Table**:  
    `ALTER TABLE customer_table RENAME TO clients_table;`
    
6. **Add a Primary Key**:  
    `ALTER TABLE customer_table ADD CONSTRAINT pk_customer PRIMARY KEY (cust_id);`
    
7. **Add a Foreign Key**:  
    `ALTER TABLE orders ADD CONSTRAINT fk_customer FOREIGN KEY (cust_id) REFERENCES customer_table (cust_id);`
    
8. **Add a Unique Constraint**:  
    `ALTER TABLE customer_table ADD CONSTRAINT unique_email UNIQUE (email);`
    
9. **Add a Check Constraint**:  
    `ALTER TABLE customer_table ADD CONSTRAINT check_age CHECK (age > 18);`
    
10. **Drop a Constraint**:  
    `ALTER TABLE customer_table DROP CONSTRAINT pk_customer;`

---
