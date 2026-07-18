# Data Warehouse Design

## Overview

A Data Warehouse is a centralized repository that stores cleaned, integrated, and historical data from multiple business systems. Unlike a Data Lake, which stores raw data, a Data Warehouse is optimized for analytical queries, reporting, dashboards, and business intelligence.

It enables organizations to make data-driven decisions by providing a single source of truth.

---

# Data Warehouse vs Data Lake

| Data Lake | Data Warehouse |
|------------|----------------|
| Stores raw data | Stores processed data |
| Schema-on-Read | Schema-on-Write |
| Supports structured, semi-structured, and unstructured data | Primarily structured data |
| Low-cost object storage | Optimized analytical storage |
| Used by Data Engineers & Data Scientists | Used by Business Analysts & BI Teams |
| Examples: Amazon S3, ADLS | Examples: Redshift, Snowflake, Synapse |

---

# Why Data Warehouses?

Organizations need

- Faster reporting
- Historical analysis
- KPI tracking
- Executive dashboards
- Single source of truth
- High-performance SQL queries

---

# Typical Architecture

```
Operational Databases
        │
        ▼
ETL / ELT Pipelines
        │
        ▼
Data Warehouse
        │
        ▼
Data Marts
        │
        ▼
Power BI / Tableau / QuickSight
```

---

# Core Components

## Fact Table

Fact tables contain measurable business events.

Examples

- Sales
- Orders
- Payments
- Transactions

Typical columns

- Order ID
- Customer ID
- Product ID
- Quantity
- Sales Amount
- Profit
- Order Date

Fact tables are usually very large.

---

## Dimension Table

Dimension tables describe facts.

Examples

- Customer
- Product
- Employee
- Region
- Date

Dimension tables change slowly.

---

# Star Schema

Star Schema consists of

One Fact Table

Connected to

Multiple Dimension Tables

Advantages

- Fast queries
- Easy joins
- BI friendly
- Simple design

Example

```
          Customer
             │
Product ─ Fact Sales ─ Date
             │
          Region
```

---

# Snowflake Schema

Snowflake Schema normalizes dimensions.

Example

```
Country

↓

State

↓

City

↓

Customer
```

Advantages

- Less redundancy
- Better storage efficiency

Disadvantages

- More joins
- Slightly slower queries

---

# Star vs Snowflake

| Star | Snowflake |
|-------|------------|
| Denormalized | Normalized |
| Faster | Slightly slower |
| Less joins | More joins |
| Easier for BI | Better for storage |

---

# Fact Table Types

### Transaction Fact

One row per transaction.

Example

Sales Order

---

### Snapshot Fact

Stores values at regular intervals.

Example

Daily Inventory

---

### Accumulating Snapshot

Tracks a business process.

Example

Loan Approval

---

# Dimension Types

Common dimensions

- Customer
- Product
- Store
- Employee
- Geography
- Calendar

---

# Slowly Changing Dimensions (SCD)

## Type 1

Overwrite old value.

No history maintained.

Example

Customer Name Correction.

---

## Type 2

Create new row.

History preserved.

Most commonly used.

---

## Type 3

Add new column.

Limited history.

---

## Type 4

History stored in separate table.

---

## Type 6

Combination of Type 1 + Type 2 + Type 3.

---

# Surrogate Key vs Natural Key

Natural Key

Business generated.

Example

PAN Number

Employee Code

---

Surrogate Key

System generated.

Example

Customer_ID

Preferred in Data Warehouses.

---

# Partitioning

Large fact tables should be partitioned.

Common partition keys

- Date
- Region
- Country

Benefits

- Faster queries
- Lower scan cost
- Better maintenance

---

# Distribution Keys (Amazon Redshift)

Distribution Styles

- EVEN
- KEY
- ALL
- AUTO

Choosing the correct distribution style minimizes data movement during joins.

---

# Sort Keys

Sort Keys improve query performance by reducing the amount of data scanned.

Common choices

- Date
- Customer_ID
- Transaction_ID

---

# Materialized Views

Materialized Views store precomputed query results.

Benefits

- Faster dashboards
- Reduced query execution time

---

# ETL Best Practices

- Incremental loading
- Data validation
- Deduplication
- Error logging
- Retry mechanism
- Audit tables
- Metadata tracking

---

# Common Interview Questions

## Why use Star Schema?

Because it provides faster query performance and is easier for BI tools.

---

## When would you choose Snowflake Schema?

When reducing redundancy is more important than query simplicity.

---

## Why use Surrogate Keys?

They remain stable even if business identifiers change.

---

## Why is SCD Type 2 commonly used?

Because it preserves historical changes.

---

## Difference between OLTP and OLAP?

OLTP

- Small transactions
- High concurrency
- Frequent inserts and updates

OLAP

- Large analytical queries
- Historical analysis
- Read optimized

---

# Best Practices

- Keep dimensions small.
- Keep fact tables narrow.
- Use surrogate keys.
- Partition large tables.
- Maintain history with SCD Type 2.
- Create summary tables for dashboards.
- Optimize joins using proper distribution keys.
- Use materialized views for frequently accessed reports.

---

# Key Takeaways

- Data Warehouses are optimized for analytics.
- Fact tables store business events.
- Dimension tables provide descriptive information.
- Star Schema is preferred for BI reporting.
- Snowflake Schema improves normalization.
- SCD Type 2 is the most widely used history management technique.
