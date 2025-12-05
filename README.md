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

