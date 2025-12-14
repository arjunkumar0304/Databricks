# Databricks


## 1. Databricks

### 1.1 Workspace UI

* The main user interface where you interact with Databricks.
* Contains left-side menu, main workspace area, and top navigation.

### 1.2 Overview of UI Components

* **Home**: Shows recent notebooks and resources.
* **Workspace**: Your folders, notebooks, and files.
* **Recent**: Quickly access recently opened items.
* **Catalog**: Shows available databases, tables, and files.
* **Compute**: Where clusters are created and managed.
* **Jobs & Pipelines**: Scheduling workflows.
* **Marketplace**: Install external datasets and solutions.

### 1.3 Workspaces

* A storage area where you organise notebooks, datasets, folders.
* Each user has a personal workspace.

### 1.4 Notebooks

* Interactive development environment for writing **PySpark, SQL, Python, Scala**.

### 1.5 Libraries

* External packages installed to clusters.
* In free edition, library installation options are limited.

### 1.6 Data

* Section where you upload files, explore tables, or connect to external storage.

### 1.7 Clusters

* Machines used to run notebooks.
* Free edition supports **single-node compute only**.

---

## 2. Workspace Navigation

### 2.1 Creating and Managing Notebooks

* Go to **Workspace → Right-click → Create → Notebook**.
* Select language (Python/SQL).

### 2.2 Uploading and Managing Data

* Go to **Catalog → Add Data → Upload file**.
* The file is stored in `/Volumes/...` or DBFS.

### 2.3 Managing Clusters

* Go to **Compute**.
* Free edition: Only default single-node cluster available.

### 2.4 Accessing Libraries

* Go to **Compute → Libraries**.
* Install `.whl` or `.jar` if supported.

### 2.5 Collaboration and Sharing

* Share notebooks with others (not fully available in free edition).

### 2.6 Sharing Notebooks

* Use **Share** button → Grant view/edit access.

### 2.7 Collaborative Editing

* In paid versions, multiple users edit same notebook.

### 2.8 Version History

* Tracks notebook changes.
* Restore previous versions anytime.

---

## 3. Cluster Creation

### 3.1 Cluster Configuration

* Choose Cluster Name
* Node type (default VM)
* Driver type

### 3.2 Cluster Type

* **Standard**: General purpose (Paid edition only)
* **High Concurrency**: Multi-user mode (Paid edition only)
* **Single Node**: Available in free edition

### 3.3 Worker Node Types

* Worker machines used in multi-node clusters.
* Not available in free edition.

### 3.4 Auto Scaling Options

* Automatically increases or decreases cluster size.
* Only available for multi-node clusters in paid plans.

---




## 4. dbutils Command

### 4.1 Overview of dbutils

`dbutils` is a utility in Databricks used for:

* File system operations
* Running external notebooks
* Managing libraries
* Creating widgets (UI elements)
* Handling secrets (not available in free edition)

It simplifies automation and interaction with DBFS and Databricks runtime.

### 4.2 Accessing dbutils in Notebooks

You can access `dbutils` directly in any Databricks notebook:

```python
dbutils.fs.ls("/FileStore/")
```

In some rare cases:

```python
dbu = dbutils
```

### 4.3 Common dbutils Commands

* `dbutils.fs` → File operations
* `dbutils.notebook` → Run child notebooks
* `dbutils.library` → Install/manage libraries
* `dbutils.widgets` → Input widgets for notebooks

### 4.4 dbutils.fs (File System Operations)

* List files → `dbutils.fs.ls(path)`
* Create folder → `dbutils.fs.mkdirs(path)`
* Copy → `dbutils.fs.cp(src, dst)`
* Move → `dbutils.fs.mv(src, dst)`
* Delete → `dbutils.fs.rm(path, recurse=True)`

### 4.5 dbutils.notebook (Notebook Operations)

```python
dbutils.notebook.run("/Workspace/childNotebook", 60)
```

Magic command:

```python
%run /Workspace/childNotebook
```

### 4.6 dbutils.library (Library Operations)

```python
dbutils.library.installPyPI("pandas")
dbutils.library.restartPython()
```

Note: Limited support in Community Edition.

### 4.7 dbutils.widgets (Widget Operations)

Widgets create interactive elements in notebooks.

* Text widget → `dbutils.widgets.text()`
* Dropdown widget → `dbutils.widgets.dropdown()`
* Combobox widget → `dbutils.widgets.combobox()`
* Multiselect widget → `dbutils.widgets.multiselect()`

<img width="1575" height="866" alt="Screenshot 2025-12-08 160240" src="https://github.com/user-attachments/assets/0649f2e5-e73f-4de0-a60b-035b53e0060e" />
<img width="1508" height="240" alt="Screenshot 2025-12-08 160252" src="https://github.com/user-attachments/assets/0a3f05c6-be97-4aee-a78d-5843d6c3cfe3" />

---

## 5. Example Usages

### 5.1 Uploading and Downloading Files

* Upload via **Add Data** → `/FileStore/` path.
* View uploaded files:

```python
dbutils.fs.ls("/FileStore/")
```

### 5.2 Running External Notebooks

```python
result = dbutils.notebook.run("/Workspace/Users/User/Child", 60)
print(result)
```

### 5.3 Installing and Managing Libraries

```python
dbutils.library.installPyPI("numpy")
```

### 5.4 Interacting with Widgets

```python
dbutils.widgets.dropdown("country", "India", ["India", "USA", "UK"])
print(dbutils.widgets.get("country"))
```

---

## 6. Read and Write in DBFS Path

### 6.1 Introduction to DBFS (Databricks File System)

DBFS is a distributed file system on top of cloud storage used by Databricks.
It supports storing data, notebooks, models, logs, and more.

### 6.2 Overview of DBFS

Common paths:

* `/FileStore/` → Public files
* `/mnt/` → Mounted cloud storage (not in free edition)
* `dbfs:/` → URI-based DBFS path

### 6.3 Mount Points

Used to connect Azure Blob, ADLS, or S3 storage.
(Not supported in Community Edition.)



### 6.4 Reading Data from DBFS

```python
df = spark.read.csv("/FileStore/data.csv", header=True)
df.show()
```

### 6.5 Reading CSV/Parquet Files

CSV example:

```python
df = spark.read.option("header", "true").csv("/FileStore/files/sample.csv")
```

Parquet example:

```python
df = spark.read.parquet("/FileStore/parquet/")
```

### 6.6 Reading Other File Formats

JSON:

```python
df = spark.read.json("/FileStore/json/")
```



---

## **7. Writing Data to DBFS**

### **7.1 Writing CSV/Parquet Files in Databricks**

DBFS (Databricks File System) allows you to write data in multiple file formats easily using PySpark.

---

### **7.2 Commands for Writing CSV**

```python
# Writing CSV
(df
 .write
 .mode("overwrite")          # overwrite, append, errorIfExists
 .option("header", True)
 .csv("/dbfs/FileStore/csv/output_data"))
```

---

### **7.3 Commands for Writing Parquet**

```python
# Writing Parquet
(df
 .write
 .mode("overwrite")
 .parquet("/dbfs/FileStore/parquet/output_data"))
```

---

### **7.4 Writing Other File Formats**

#### **Write JSON**

```python
(df.write.mode("overwrite").json("/dbfs/FileStore/json/output_data"))
```

## **8. Medallion Architecture**

A popular data engineering design pattern used in Databricks.

---

### **8.1 Introduction to Medallion Architecture**

Medallion = Three-layer architecture:

1. **Bronze Layer** – Raw data ingestion.
2. **Silver Layer** – Cleaned + standardized data.
3. **Gold Layer** – Business-level curated data.

This architecture improves data quality step-by-step.

---

### **8.2 Use Cases and Applications**

* ETL data pipelines
* Data Warehousing
* Machine Learning pipelines
* BI dashboards
* Slowly changing dimensions
* Incremental processing
* Streaming pipelines

Bronze → Silver → Gold flow ensures reliability and quality.

---

## **9. Delta Lake (Theory)**

Delta Lake is a storage layer that brings **ACID** transactions & reliability to data lakes.

---

### **9.1 Introduction to Delta Lake**

Delta Lake stores data in Parquet + maintains a transaction log (`_delta_log`).
It enables:

* Version control
* Schema enforcement
* Time travel
* Reliable reads/writes

---

### **9.2 ACID Transactions**

ACID stands for:

* A – Atomicity: Complete write happens or nothing happens

* C – Consistency: Ensures data always remains valid

* I – Isolation: Parallel writes do not corrupt data

* D – Durability: Once data is written, it is safe and permanent


---

### **9.3 Time Travel**

You can query old versions of a Delta table by:

* Version number
* Timestamp

Example:

```python
df = spark.read.format("delta").option("versionAsOf", 3).load("/delta/table_path")
```

---

### **9.4 Delta Table**

A Delta table = Parquet files + transaction log.
Stored at:

```
/_delta_log
```

Supports:

* MERGE
* UPDATE
* DELETE
* OPTIMIZE

---

### **9.5 Delta Log**

The **_delta_log** folder stores JSON/Checkpoint files that record:

* Changes
* Commits
* Schema updates
* Transactions

This enables ACID and time travel.

---

### **9.6 Usage and Benefits**

Key benefits:

* Reliable pipelines
* Faster reads
* Schema enforcement
* Versioning/time travel
* Transaction support
* Scalable for batch + streaming

---

### **9.7 Schema Evolution**

Schema Evolution means Delta Table automatically adapts to new columns, data types, or structure changes during write operations.



## 10.1 Lakeflow Connect

### 10.1.1 Upload Files

* Allows you to upload CSV, JSON, Parquet, Excel files into Databricks.
* Supports drag-and-drop or browse upload.

### 10.1.2 Managed Connectors

* Prebuilt connectors provided by Databricks.
* Connect to cloud storage, databases, SaaS apps.
* Fully managed and optimized.

### 10.1.3 Standard Connectors

* Basic connectors like JDBC, S3, ADLS.
* You configure authentication and options manually.

### 10.1.4 Data Formats

* Supported formats: CSV, JSON, Parquet, Delta, ORC, Avro.
* Delta is recommended for performance and ACID features.

### 10.1.5 Migrate to Delta Table

* Convert existing CSV/Parquet tables to Delta.
* Uses `CONVERT TO DELTA` or rewrite using `format("delta")`.

---

## 10.2 Delta Lake

### 10.2.1 Operations

* CREATE, READ, WRITE, MERGE, UPDATE, DELETE.
* Time travel using version or timestamp.

### 10.2.2 Data Layout

* **Liquid Clustering:** Auto-organizes data without partitions.
* **Data Skipping:** Uses file stats to skip irrelevant data.
* **Tune File Size:** Optimize file sizes using OPTIMIZE.
* **Table Size:** Use DESCRIBE DETAIL.
* **Partition Tables:** Improves filter performance.

### 10.2.3 Schema Enforcement & Evolution

* Enforcement: Ensures wrong schema data cannot be written.
* Evolution: Allows adding new columns automatically.

### 10.2.4 Table Features

* **Change Data Feed (CDF):** Captures row changes.
* **Table Constraints:** NOT NULL, CHECK constraints.
* **Generated Columns:** Auto-calculated columns.
* **Row Tracking:** Tracks row identifiers.
* **Type Widening:** Allows safe datatype changes.

---

## 10.3 Structured Streaming

* Real-time processing using micro-batch engine.
* Supports Delta as sink & source.
* Auto-recovery and fault tolerance.

---

## 10.4 Data Governance with Unity Catalog

* Centralized governance for data, AI assets, models.
* Fine‑grained permissions.
* Secure sharing.

---

## 10.5 Unity Catalog

* Logical structure: **Metastore → Catalog → Schema → Table**.
* Manages permissions, lineage, auditing.

---

## 10.6 Catalog Explorer

* GUI to browse tables, schemas, catalogs.
* Shows metadata, preview, lineage.





