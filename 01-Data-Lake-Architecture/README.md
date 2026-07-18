# Data Lake Architecture

## Overview

A Data Lake is a centralized storage system designed to store structured, semi-structured, and unstructured data at any scale. Unlike traditional data warehouses, a Data Lake stores raw data in its original format and allows different teams to process it for analytics, reporting, machine learning, and business intelligence.

Modern Data Lakes are built on cloud object storage such as Amazon S3 or Azure Data Lake Storage (ADLS Gen2), providing high durability, scalability, and cost efficiency.

---

# Why Do We Need a Data Lake?

Organizations generate data from multiple sources every day:

- Databases
- Mobile Applications
- Websites
- APIs
- IoT Devices
- Log Files
- ERP Systems
- CRM Systems

Instead of storing this data in different systems, a Data Lake centralizes everything in one place, making it easier to process, govern, and analyze.

---

# Characteristics

- Stores raw and processed data
- Supports structured, semi-structured, and unstructured formats
- Highly scalable
- Cost-effective storage
- Schema-on-read approach
- Supports batch and streaming ingestion
- Enables analytics, BI, AI, and ML workloads

---

# Common Data Sources

- MySQL
- PostgreSQL
- SQL Server
- Oracle
- MongoDB
- REST APIs
- Kafka
- IoT Devices
- Application Logs
- CSV Files
- JSON Files
- Excel Files

---

# Data Lake Architecture

A modern Data Lake generally consists of the following layers:

1. Source Layer
2. Ingestion Layer
3. Storage Layer
4. Processing Layer
5. Serving Layer
6. Consumption Layer

---

## Source Layer

Responsible for generating business data.

Examples:

- Banking transactions
- E-commerce orders
- Customer data
- CRM
- ERP
- Website clickstream
- Mobile events

---

## Ingestion Layer

Collects data from various systems.

Batch Ingestion:

- AWS Glue
- Azure Data Factory

Streaming Ingestion:

- Apache Kafka
- Amazon Kinesis
- Azure Event Hub

---

## Storage Layer

Stores all incoming data.

AWS

- Amazon S3

Azure

- Azure Data Lake Storage Gen2

Common File Formats

- CSV
- JSON
- Parquet
- ORC
- Avro

Recommended Format:

Parquet

Reason:

- Columnar Storage
- Compression
- Faster Queries

---

## Processing Layer

Responsible for cleaning, transforming, validating, and enriching data.

Common Technologies

- Apache Spark
- PySpark
- Databricks
- AWS Glue
- EMR

Typical Tasks

- Remove duplicates
- Handle null values
- Standardize formats
- Join datasets
- Aggregate data
- Data quality validation

---

## Serving Layer

Stores processed data for analytics.

Examples

- Amazon Redshift
- Azure Synapse Analytics
- Snowflake
- BigQuery

---

## Consumption Layer

Business users consume processed data through:

- Power BI
- Tableau
- Amazon QuickSight
- Excel
- Machine Learning models
- REST APIs

---

# Medallion Architecture

Modern Data Lakes commonly use the Medallion Architecture.

## Bronze Layer

Purpose:

Store raw data exactly as received.

Characteristics

- Immutable
- Historical data
- Minimal transformations

Example

Customer transactions arriving from Kafka.

---

## Silver Layer

Purpose

Clean and standardized data.

Transformations

- Remove duplicates
- Handle null values
- Standardize columns
- Apply business rules

---

## Gold Layer

Purpose

Business-ready data.

Examples

- Daily Sales
- Monthly Revenue
- Customer KPIs
- Executive Dashboards

---

# Batch vs Streaming

| Batch | Streaming |
|--------|-----------|
| Runs every few hours | Continuous |
| High throughput | Low latency |
| Scheduled | Event-driven |
| Large data volumes | Small continuous events |

---

# AWS Data Lake Example

Source Systems

↓

Amazon S3

↓

AWS Glue

↓

Amazon Redshift

↓

Amazon Athena

↓

Power BI

---

# Azure Data Lake Example

Source Systems

↓

Azure Data Factory

↓

Azure Data Lake Storage

↓

Azure Databricks

↓

Azure Synapse

↓

Power BI

---

# Best Practices

- Use Parquet instead of CSV.
- Partition large datasets.
- Separate raw and curated data.
- Enable version control.
- Monitor pipeline failures.
- Implement data quality checks.
- Encrypt data at rest and in transit.
- Use IAM/RBAC for access control.
- Automate orchestration.
- Maintain metadata using a catalog.

---

# Interview Questions

### Why use a Data Lake instead of a Data Warehouse?

Because it stores raw structured and unstructured data at low cost and supports multiple downstream use cases.

---

### Why Parquet instead of CSV?

- Smaller storage
- Faster queries
- Columnar format
- Better compression

---

### Why Bronze-Silver-Gold?

It separates raw, cleaned, and business-ready datasets, making pipelines easier to maintain and audit.

---

### Difference between Schema-on-Read and Schema-on-Write?

Schema-on-Read validates data when it is queried, while Schema-on-Write validates data before storing it.

---

# Key Takeaways

- A Data Lake is the foundation of modern analytics platforms.
- Object storage like S3 or ADLS provides scalable and durable storage.
- The Medallion Architecture improves data quality and governance.
- Batch and Streaming pipelines can coexist in the same Data Lake.
- Proper partitioning, security, and monitoring are essential for production systems.
