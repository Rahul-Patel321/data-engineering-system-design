# 📚 Data Engineering Cheatsheet

A quick revision guide for Data Engineering interviews covering SQL, PySpark, AWS, Data Warehousing, Streaming, and System Design.

---

# 🏗️ Data Engineering Pipeline

```
Source Systems
      ↓
Ingestion
      ↓
Raw Layer
      ↓
Transformation
      ↓
Curated Layer
      ↓
Data Warehouse
      ↓
BI / Reporting
```

---

# ☁️ AWS Services

| Service | Purpose |
|----------|----------|
| Amazon S3 | Data Lake Storage |
| AWS Glue | Serverless ETL |
| AWS DMS | Change Data Capture (CDC) |
| Amazon Redshift | Data Warehouse |
| Amazon Athena | SQL on S3 |
| AWS Lambda | Event-driven processing |
| Step Functions | Workflow orchestration |
| CloudWatch | Monitoring |
| SNS | Notifications |
| IAM | Access Management |

---

# 🔷 Azure Equivalent

| AWS | Azure |
|------|--------|
| S3 | ADLS Gen2 |
| Glue | Azure Data Factory |
| Redshift | Synapse Analytics |
| Lambda | Azure Functions |
| CloudWatch | Azure Monitor |
| SNS | Event Grid |
| IAM | Microsoft Entra ID |
| Athena | Synapse Serverless SQL |
| EMR | Azure Databricks |

---

# 🥉🥈🥇 Medallion Architecture

```
Bronze
↓
Raw Data

↓

Silver
↓
Cleaned & Validated Data

↓

Gold
↓
Business Ready Data
```

---

# 🗂️ ETL vs ELT

| ETL | ELT |
|-----|-----|
| Transform before loading | Transform after loading |
| Traditional DW | Modern Data Lake |
| Slower | More scalable |

---

# 📦 Batch vs Streaming

| Batch | Streaming |
|--------|-----------|
| Scheduled | Continuous |
| High Latency | Low Latency |
| Large Volume | Real-time Events |

---

# 🔄 Change Data Capture (CDC)

Captures only changed records.

Common operations:

- INSERT
- UPDATE
- DELETE

Benefits:

- Faster loads
- Lower compute cost
- Incremental processing

AWS Service:

- AWS DMS

---

# 📂 Data Lake vs Data Warehouse

| Data Lake | Data Warehouse |
|------------|----------------|
| Raw Data | Curated Data |
| Cheap Storage | Optimized Analytics |
| Schema-on-Read | Schema-on-Write |
| S3 | Redshift |

---

# ⚡ PySpark Optimizations

- Filter early
- Select only required columns
- Broadcast small tables
- Partition large datasets
- Avoid collect()
- Avoid UDFs where possible
- Cache reusable DataFrames
- Use Parquet format
- Compress with Snappy

---

# 🛠️ Spark Transformations

- select()
- filter()
- withColumn()
- groupBy()
- agg()
- join()
- union()
- distinct()
- dropDuplicates()
- orderBy()

---

# 🚀 Spark Actions

- show()
- count()
- collect()
- take()
- first()
- write()

---

# 🔥 Join Types

- Inner Join
- Left Join
- Right Join
- Full Join
- Cross Join
- Left Semi Join
- Left Anti Join

---

# 🗄️ SQL Order of Execution

```
FROM

↓

JOIN

↓

WHERE

↓

GROUP BY

↓

HAVING

↓

SELECT

↓

ORDER BY

↓

LIMIT
```

---

# 📊 Window Functions

Common Functions

- ROW_NUMBER()
- RANK()
- DENSE_RANK()
- LAG()
- LEAD()
- NTILE()

---

# 🎯 Data Modeling

Fact Table

- Business Metrics
- Sales
- Orders
- Revenue

Dimension Table

- Customer
- Product
- Date
- Store

Schema Types

- Star Schema
- Snowflake Schema

---

# 📈 Partitioning

Advantages

- Faster Queries
- Reduced Scan Cost
- Better Parallelism

Common Columns

- Date
- Year
- Month
- Region

---

# 📁 File Formats

| Format | Use Case |
|----------|----------|
| CSV | Data Exchange |
| JSON | APIs |
| Parquet | Analytics |
| ORC | Hive |
| Avro | Streaming |

---

# 🔐 Security

- IAM Roles
- Least Privilege
- Encryption at Rest
- Encryption in Transit
- AWS KMS
- Secrets Manager
- Row Level Security

---

# 📊 Monitoring

Monitor:

- Job Failures
- Pipeline Duration
- Data Freshness
- Record Counts
- SLA Compliance
- CloudWatch Metrics

---

# 💰 Cost Optimization

- Incremental Loads
- Partitioning
- Compression
- Parquet Format
- Auto Scaling
- Lifecycle Policies
- Spot Instances (where appropriate)

---

# 📚 Common Interview Questions

### What is ETL?

Extract, Transform and Load data into analytical systems.

---

### Why use Parquet?

- Columnar Storage
- Compression
- Faster Analytics

---

### Why use S3 as Data Lake?

- Low Cost
- Highly Scalable
- Durable
- Supports Multiple Analytics Engines

---

### Difference between Data Lake and Warehouse?

Lake stores raw data.

Warehouse stores business-ready structured data.

---

### What is CDC?

Capture only changed records instead of reloading entire tables.

---

### Why partition data?

Improves query performance and reduces cost.

---

### Why use Redshift?

Columnar data warehouse optimized for analytical workloads.

---

### Why use Athena?

Run SQL directly on S3 without loading data into a warehouse.

---

### Why use Kafka?

Distributed platform for real-time event streaming.

---

### Difference between Batch and Streaming?

Batch processes data on a schedule.

Streaming processes events continuously.

---

# 🧠 Interview Revision Checklist

✅ SQL

✅ Joins

✅ Window Functions

✅ CTE

✅ PySpark

✅ Spark Optimization

✅ AWS Services

✅ Azure Services

✅ Data Modeling

✅ ETL

✅ ELT

✅ CDC

✅ Streaming

✅ Kafka

✅ Data Lake

✅ Data Warehouse

✅ System Design

✅ Monitoring

✅ Security

✅ Cost Optimization

---

# 💡 Final Tip

Don't memorize services.

Understand:

- Why is this service used?
- What problem does it solve?
- What are the alternatives?
- What are the trade-offs?
