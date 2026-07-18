# Data Modeling

## Overview

Data modeling is the process of organizing data into logical and physical structures that support efficient storage, querying, and analytics.

A well-designed data model improves data quality, query performance, scalability, and maintainability.

Data modeling is widely used in OLTP systems, Data Warehouses, Data Lakes, and Business Intelligence platforms.

---

# Why Data Modeling?

Good data models help organizations:

- Improve query performance
- Reduce redundancy
- Maintain data consistency
- Support business reporting
- Simplify analytics
- Enable scalable data platforms

---

# Types of Data Models

## Conceptual Model

High-level business view.

Focuses on

- Business entities
- Relationships
- Business rules

Example

Customer

places

Order

---

## Logical Model

Technology independent.

Defines

- Tables
- Relationships
- Attributes
- Primary Keys
- Foreign Keys

---

## Physical Model

Implementation level.

Defines

- Data types
- Indexes
- Partitioning
- Storage
- Distribution Keys

---

# OLTP vs OLAP

| OLTP | OLAP |
|------|------|
| Operational systems | Analytical systems |
| Many inserts & updates | Mostly reads |
| Normalized | Denormalized |
| Small transactions | Large analytical queries |
| Low latency | High throughput |

Examples

OLTP

- Banking Transactions
- E-Commerce Orders
- CRM Systems

OLAP

- Power BI
- Redshift
- Snowflake
- Synapse
- BigQuery

---

# Normalization

Normalization reduces data redundancy.

Common Forms

## First Normal Form (1NF)

- Atomic values
- No repeating groups

---

## Second Normal Form (2NF)

- 1NF
- Remove partial dependencies

---

## Third Normal Form (3NF)

- 2NF
- Remove transitive dependencies

---

Advantages

- Less redundancy
- Better consistency

Disadvantages

- More joins
- Slower analytical queries

---

# Denormalization

Combines related tables.

Advantages

- Faster queries
- Better BI performance

Disadvantages

- Higher storage
- Data duplication

---

# Fact Table

Stores measurable business events.

Examples

- Sales
- Orders
- Transactions
- Payments

Common Columns

- Customer_ID
- Product_ID
- Date_ID
- Amount
- Quantity

---

# Dimension Table

Stores descriptive information.

Examples

- Customer
- Product
- Region
- Store
- Employee
- Calendar

---

# Primary Key

Uniquely identifies a record.

Example

Customer_ID

---

# Foreign Key

Creates relationships between tables.

Example

Customer_ID in Fact Table

---

# Surrogate Key

System-generated unique identifier.

Advantages

- Stable
- Independent of business values
- Better performance

---

# Natural Key

Business-generated identifier.

Examples

- PAN Number
- Passport Number
- Employee Code

---

# Slowly Changing Dimensions

Type 1

Overwrite values

No history

---

Type 2

Create new rows

Maintain history

Most commonly used

---

Type 3

Limited history

Additional columns

---

# Grain

Grain defines the level of detail stored in a fact table.

Examples

One Row Per

- Transaction
- Customer
- Product
- Invoice

Always define grain before designing a fact table.

---

# Partitioning

Large tables should be partitioned.

Common partition columns

- Date
- Country
- Region
- Year
- Month

Benefits

- Faster queries
- Lower scan cost
- Better maintenance

---

# Indexing

Indexes improve lookup performance.

Common Index Types

- Clustered
- Non-Clustered
- Composite

---

# Data Modeling Best Practices

- Keep dimensions descriptive.
- Keep facts numeric.
- Define grain early.
- Prefer surrogate keys.
- Avoid unnecessary joins.
- Partition large tables.
- Use meaningful naming conventions.
- Document relationships.

---

# Common Interview Questions

## Why normalize data?

To reduce redundancy and improve consistency.

---

## Why denormalize a warehouse?

To improve analytical query performance.

---

## What is grain?

The lowest level of detail stored in a fact table.

---

## Difference between Fact and Dimension tables?

Fact tables store measurable business events, while dimension tables provide descriptive attributes.

---

## Why use surrogate keys?

They remain stable even if business identifiers change and improve join performance.

---

## What is OLTP?

A transactional system optimized for inserts, updates, and deletes.

---

## What is OLAP?

An analytical system optimized for reporting and business intelligence.

---

# Key Takeaways

- Data modeling forms the foundation of scalable analytics platforms.
- Normalize transactional systems and denormalize analytical systems.
- Define grain before creating fact tables.
- Use surrogate keys and partitioning for better scalability.
- Well-designed models improve performance and simplify reporting.
