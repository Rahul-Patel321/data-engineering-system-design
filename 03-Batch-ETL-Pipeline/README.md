# Batch ETL Pipeline

## Overview

A Batch ETL Pipeline extracts data from one or more source systems, transforms it into a standardized format, and loads it into a centralized storage or data warehouse for reporting and analytics.

Batch processing is suitable for workloads where near real-time data is not required. It is commonly scheduled to run hourly, daily, or weekly depending on business requirements.

---

# ETL vs ELT

| ETL | ELT |
|-----|-----|
| Transform before loading | Transform after loading |
| Suitable for traditional data warehouses | Suitable for modern cloud platforms |
| Less flexible | More scalable |
| Processing outside warehouse | Processing inside warehouse |

---

# Typical Batch Pipeline

```
Source Systems
        │
        ▼
Extract
        │
        ▼
Landing (Raw)
        │
        ▼
Validation
        │
        ▼
Transformation
        │
        ▼
Business Rules
        │
        ▼
Curated Data
        │
        ▼
Data Warehouse
        │
        ▼
Power BI / Tableau
```

---

# Common Data Sources

- MySQL
- PostgreSQL
- SQL Server
- Oracle
- REST APIs
- CSV
- Excel
- JSON
- ERP Systems
- CRM Systems

---

# AWS Batch ETL Architecture

Source Systems

↓

Amazon S3 (Landing)

↓

AWS Glue

↓

Amazon S3 Curated

↓

Amazon Redshift

↓

Power BI

AWS Services Used

- Amazon S3
- AWS Glue
- IAM
- CloudWatch
- Step Functions
- Redshift
- Athena

---

# Azure Batch ETL Architecture

Source Systems

↓

Azure Data Factory

↓

Azure Data Lake Storage

↓

Azure Databricks

↓

Azure Synapse Analytics

↓

Power BI

---

# ETL Stages

## Extract

Responsibilities

- Read source data
- Validate connectivity
- Fetch incremental records
- Log extraction metadata

---

## Transform

Typical transformations

- Remove duplicates
- Handle null values
- Data type conversion
- Standardize formats
- Business calculations
- Join datasets
- Aggregations

---

## Load

Destination options

- Data Lake
- Data Warehouse
- Delta Lake
- Redshift
- Synapse

Loading Strategies

- Full Load
- Incremental Load
- Merge (Upsert)

---

# Full Load

Characteristics

- Deletes existing data
- Reloads everything
- Simple implementation
- Longer execution time

Suitable For

- Small tables
- Dimension tables
- Initial load

---

# Incremental Load

Only processes newly added or modified records.

Advantages

- Faster
- Lower compute cost
- Smaller data movement

Common Techniques

- Timestamp
- CDC
- Auto Increment ID
- Watermark
- Version Column

---

# Idempotent Pipelines

A pipeline is idempotent if running it multiple times produces the same result.

Best Practices

- MERGE instead of INSERT
- Deduplicate data
- Track processed batches
- Use checkpoints
- Maintain audit tables

---

# Error Handling

Common Errors

- Source unavailable
- Invalid schema
- Corrupted files
- Network failures
- Permission issues

Handling Strategy

- Retry failed tasks
- Log exceptions
- Send alerts
- Move bad records to quarantine
- Continue processing valid records

---

# Retry Strategy

Typical Configuration

Retry Count : 3

Retry Interval : 5 Minutes

Exponential Backoff

---

# Audit Table

Typical Columns

- Batch ID
- Pipeline Name
- Start Time
- End Time
- Records Read
- Records Loaded
- Failed Records
- Status

Benefits

- Monitoring
- Troubleshooting
- SLA Reporting

---

# Logging

Capture

- Pipeline Start
- Pipeline End
- Execution Time
- Failed Step
- Error Message
- Record Count

AWS

CloudWatch Logs

Azure

Azure Monitor

---

# Scheduling

Daily

Hourly

Weekly

Monthly

Tools

- AWS Step Functions
- Amazon EventBridge
- MWAA (Airflow)
- Azure Data Factory Triggers
- Cron Jobs

---

# Performance Optimization

- Read only required columns
- Predicate Pushdown
- Partition large datasets
- Avoid small files
- Parallel processing
- Incremental loading
- Optimize joins
- Cache reusable datasets
- Compress output files

---

# Security

- IAM Roles
- Encryption at Rest
- Encryption in Transit
- Secrets Manager
- RBAC
- Least Privilege Access

---

# Best Practices

- Separate raw and curated data.
- Never overwrite raw data.
- Keep pipelines idempotent.
- Monitor execution metrics.
- Maintain audit tables.
- Validate incoming schema.
- Use incremental loading wherever possible.
- Automate retries.
- Store logs centrally.
- Document every pipeline.

---

# Common Interview Questions

## What is ETL?

Extract data from sources, transform it into the required format, and load it into the target system.

---

## Difference between ETL and ELT?

ETL transforms data before loading, whereas ELT loads raw data first and performs transformations later.

---

## Why Incremental Loading?

It reduces execution time, compute cost, and unnecessary data movement.

---

## What is an Idempotent Pipeline?

A pipeline that produces the same output even if executed multiple times.

---

## How do you handle failed jobs?

- Retry
- Logging
- Alerts
- Audit Tables
- Resume from checkpoint

---

## How do you monitor pipelines?

Using logs, audit tables, CloudWatch/Azure Monitor, execution metrics, and alerting.

---

# Key Takeaways

- Batch ETL remains the foundation of enterprise data platforms.
- Incremental processing improves scalability and reduces cost.
- Idempotency ensures reliable reruns.
- Monitoring, logging, and audit tables are essential for production systems.
- Well-designed ETL pipelines are secure, observable, and easy to maintain.
