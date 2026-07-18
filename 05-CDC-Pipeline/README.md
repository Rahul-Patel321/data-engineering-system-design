# Change Data Capture (CDC)

## Overview

Change Data Capture (CDC) is a data integration technique used to identify and capture changes (INSERT, UPDATE, DELETE) made to a source database and propagate only those changes to downstream systems.

Instead of reloading an entire table, CDC processes only the changed records, reducing data movement, execution time, and infrastructure cost.

CDC is widely used in modern data engineering pipelines for building near real-time analytics platforms, data lakes, and data warehouses.

---

# Why CDC?

Traditional full data loads become inefficient as datasets grow larger.

Example:

Customer Table

10 Million Records

Daily Changes

25,000 Records

Without CDC

Process 10 Million Records

With CDC

Process only 25,000 Records

Benefits

- Faster pipelines
- Lower compute cost
- Reduced network traffic
- Near real-time synchronization
- Better scalability

---

# Types of CDC

## Timestamp-Based CDC

Tracks records using a timestamp column.

Example

Last_Updated

Advantages

- Simple
- Easy to implement

Limitations

- Requires reliable timestamp
- Cannot detect deleted records

---

## Incremental ID

Uses increasing IDs.

Example

Order_ID

Suitable when records are append-only.

---

## Log-Based CDC

Reads database transaction logs.

Captures

- INSERT
- UPDATE
- DELETE

Advantages

- Very efficient
- Minimal database impact
- Supports deletes

Most preferred in enterprise systems.

---

## Trigger-Based CDC

Database triggers write changes into audit tables.

Advantages

Simple implementation.

Disadvantages

Higher database overhead.

---

# CDC Architecture

Source Database

↓

Transaction Logs

↓

CDC Tool

↓

Kafka

↓

Spark / Glue

↓

Data Lake

↓

Data Warehouse

↓

Power BI

---

# Popular CDC Tools

Open Source

- Debezium
- Kafka Connect

AWS

- AWS DMS

Azure

- Azure Data Factory CDC
- SQL Change Tracking

Commercial

- Qlik Replicate
- Informatica

---

# AWS CDC Architecture

Source Database

↓

AWS Database Migration Service (DMS)

↓

Amazon S3

↓

AWS Glue

↓

Amazon Redshift

↓

Power BI

---

# Azure CDC Architecture

SQL Database

↓

Azure Data Factory

↓

Azure Data Lake

↓

Azure Databricks

↓

Azure Synapse

↓

Power BI

---

# MERGE (Upsert)

CDC pipelines commonly use MERGE operations.

Pseudo Logic

WHEN MATCHED

Update existing row

WHEN NOT MATCHED

Insert new row

Benefits

- No duplicates
- Supports incremental updates
- Simplifies synchronization

---

# Delete Handling

Deleted records must also be propagated.

Common Approaches

- Soft Delete
- Hard Delete
- Delete Flag
- Tombstone Records

---

# Slowly Changing Dimension (SCD) Integration

CDC is often combined with SCD Type 2.

Benefits

- Historical tracking
- Regulatory compliance
- Auditing

---

# Common Challenges

- Duplicate events
- Out-of-order events
- Missing transaction logs
- Schema changes
- Large transaction batches
- Network failures

---

# Best Practices

- Prefer log-based CDC.
- Track processed offsets.
- Make pipelines idempotent.
- Validate row counts.
- Log every batch.
- Monitor CDC lag.
- Handle schema evolution.
- Use MERGE instead of INSERT.
- Archive processed files.

---

# Common Interview Questions

## What is CDC?

A technique for capturing only INSERT, UPDATE, and DELETE operations from a source system instead of processing the entire dataset.

---

## Why is CDC better than Full Load?

It reduces execution time, compute cost, and unnecessary data movement.

---

## Which CDC approach is best?

Log-based CDC because it captures all database changes with minimal impact.

---

## How do you process Deletes?

Using delete flags, tombstone records, or hard deletes depending on business requirements.

---

## What is MERGE?

MERGE combines INSERT and UPDATE operations into a single statement, commonly used in incremental pipelines.

---

# Key Takeaways

- CDC enables efficient incremental data processing.
- Log-based CDC is the preferred enterprise approach.
- MERGE operations simplify synchronization.
- CDC reduces cost and improves scalability.
- Combining CDC with SCD Type 2 enables historical tracking.
