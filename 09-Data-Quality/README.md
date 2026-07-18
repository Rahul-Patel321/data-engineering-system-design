# Data Quality

## Overview

Data Quality ensures that data is accurate, complete, consistent, valid, unique, and timely before it is used for reporting, analytics, or machine learning.

Poor-quality data leads to incorrect business decisions, compliance risks, failed pipelines, and loss of trust in data.

Data quality checks should be integrated into every stage of a data pipeline.

---

# Why Data Quality Matters

Poor data quality can result in:

- Incorrect dashboards
- Duplicate records
- Missing values
- Revenue reporting issues
- Compliance failures
- Customer dissatisfaction

A production-grade pipeline should always validate data before loading it into downstream systems.

---

# Dimensions of Data Quality

## Accuracy

Data correctly represents the real-world value.

Example:

Customer Age = 30

Not

Customer Age = 300

---

## Completeness

Required fields should not be NULL.

Example

Customer_ID

Transaction_Date

Amount

---

## Consistency

The same data should have identical values across systems.

Example

Customer Name

CRM

=

Customer Name

Warehouse

---

## Validity

Data should conform to predefined rules.

Example

Email

abc@gmail.com ✅

abc@@gmail ❌

---

## Uniqueness

Duplicate records should not exist.

Example

Customer_ID should appear only once in the Customer table.

---

## Timeliness

Data should arrive within expected SLA.

Example

Daily sales data should be available by 7:00 AM.

---

# Common Data Quality Checks

- Null value validation
- Duplicate record detection
- Primary key validation
- Foreign key validation
- Data type validation
- Range validation
- Format validation
- Record count validation
- Business rule validation

---

# Null Check Example

Customer_ID

NULL ❌

Customer_ID

12345 ✅

---

# Duplicate Check

Incorrect

Order_ID

1001

1001

Correct

1001

1002

1003

---

# Range Validation

Age

0–120 ✅

Age

999 ❌

---

# Referential Integrity

Ensure relationships remain valid.

Example

Every Order must reference an existing Customer.

Orders.Customer_ID

↓

Customer.Customer_ID

---

# Record Count Validation

Compare

Source Count

↓

Target Count

Large differences should trigger alerts.

---

# Schema Validation

Verify

- Column names
- Data types
- Number of columns

Detect schema changes before processing.

---

# Data Quality Workflow

Source Data

↓

Validation Rules

↓

Failed Records

↓

Error Table / Quarantine

↓

Valid Records

↓

Transformation

↓

Warehouse

---

# Data Quality Tools

Open Source

- Great Expectations
- Deequ
- Soda Core

Cloud

AWS Glue Data Quality

Azure Data Factory Validation

Databricks Expectations

---

# Error Handling

Invalid records should not stop the entire pipeline.

Recommended approach:

Valid Records

↓

Warehouse

Invalid Records

↓

Quarantine Table

↓

Review

↓

Reprocess

---

# Monitoring Data Quality

Track

- Null %
- Duplicate %
- Failed Rules
- Missing Records
- SLA Compliance
- Data Freshness

---

# Best Practices

- Validate data at ingestion.
- Keep validation rules reusable.
- Separate valid and invalid records.
- Log every validation failure.
- Monitor data quality metrics.
- Automate alerts for failures.
- Define SLAs with business teams.
- Version validation rules.
- Regularly review thresholds.

---

# Common Interview Questions

## What is data quality?

The process of ensuring data is accurate, complete, valid, consistent, unique, and timely.

---

## How do you handle bad records?

Store invalid records in a quarantine table, log the reason, and continue processing valid records.

---

## Why validate schema?

To detect unexpected column additions, removals, or data type changes before processing.

---

## What is referential integrity?

Ensuring foreign keys always reference valid primary keys.

---

## Which tools have you used?

Examples include AWS Glue Data Quality, Great Expectations, Deequ, and custom PySpark validation logic.

---

# Key Takeaways

- Data quality is essential for reliable analytics.
- Validation should be automated within ETL pipelines.
- Invalid data should be isolated, not silently discarded.
- Continuous monitoring helps maintain trust in enterprise data platforms.
