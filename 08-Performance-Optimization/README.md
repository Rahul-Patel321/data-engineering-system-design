# Performance Optimization

## Overview

Performance optimization is the process of improving the speed, efficiency, and resource utilization of data processing systems. It helps reduce execution time, lower infrastructure costs, and improve the scalability of data pipelines.

Optimization techniques apply across Spark, SQL, Data Warehouses, Data Lakes, and cloud platforms such as AWS and Azure.

---

# Why Performance Optimization?

Large-scale data platforms process millions or billions of records daily.

Poorly optimized pipelines can lead to:

- Long execution times
- High cloud costs
- Resource bottlenecks
- Failed SLAs
- Slow dashboards

A well-optimized pipeline delivers data faster while consuming fewer resources.

---

# Spark Optimization

## Partitioning

Partitioning divides data into smaller chunks for parallel processing.

Benefits

- Improves parallelism
- Reduces execution time
- Better resource utilization

Guidelines

- Avoid too few partitions (underutilization)
- Avoid too many partitions (scheduling overhead)

---

## Repartition vs Coalesce

### Repartition

- Increases or decreases partitions
- Causes full shuffle
- Used for balancing data

### Coalesce

- Reduces partitions
- Minimal shuffle
- Faster than repartition
- Ideal before writing output

---

## Predicate Pushdown

Filter records as early as possible.

Instead of reading all records and filtering later:

```
Read All Data
↓

Filter
```

Use:

```
Read Filtered Data Only
```

Benefits

- Lower I/O
- Faster execution
- Reduced memory usage

---

## Column Pruning

Read only required columns.

Avoid

```
SELECT *
```

Prefer

```
SELECT customer_id,
       amount
```

Benefits

- Less data scanned
- Lower network traffic
- Faster execution

---

## Broadcast Join

Used when one table is significantly smaller.

Spark broadcasts the small table to every executor.

Advantages

- Avoids shuffle
- Faster joins
- Lower network overhead

Suitable when dimension tables are relatively small.

---

## Shuffle Optimization

Shuffle is one of the most expensive Spark operations.

Caused by

- Joins
- groupBy
- distinct
- orderBy

Best Practices

- Broadcast small tables
- Filter early
- Reduce unnecessary joins
- Partition wisely

---

## Caching

Cache datasets that are reused multiple times.

Benefits

- Avoid recomputation
- Improve iterative processing

Do not cache data used only once.

---

## File Size Optimization

Avoid

Thousands of small files.

Preferred file size

128 MB – 512 MB

Benefits

- Faster reads
- Lower metadata overhead
- Better parallel processing

---

## Parquet vs CSV

| Parquet | CSV |
|----------|-----|
| Columnar | Row-based |
| Compressed | Uncompressed |
| Faster queries | Slower |
| Supports predicate pushdown | No |
| Recommended | Not recommended for analytics |

---

# SQL Optimization

Best Practices

- Avoid SELECT *
- Filter early
- Use proper indexes
- Avoid unnecessary DISTINCT
- Optimize JOIN conditions
- Analyze execution plans
- Partition large tables

---

# Redshift Optimization

## Distribution Styles

- AUTO
- EVEN
- KEY
- ALL

Choose the distribution style based on join patterns.

---

## Sort Keys

Sort frequently filtered columns.

Examples

- Date
- Customer_ID

Benefits

- Faster scans
- Lower I/O

---

## Vacuum

Reclaims storage and reorders data.

---

## Analyze

Updates table statistics used by the query optimizer.

---

# Data Lake Optimization

- Store data in Parquet
- Compress files
- Partition by date
- Avoid millions of tiny files
- Archive cold data
- Optimize metadata

---

# AWS Optimization

Services

- S3 Lifecycle Policies
- Glue Job Bookmarks
- Auto Scaling
- EMR Managed Scaling
- Athena Partition Projection

---

# Monitoring Performance

Track

- Execution time
- CPU utilization
- Memory usage
- Shuffle size
- Data skew
- Failed tasks

Tools

- Spark UI
- CloudWatch
- Ganglia
- Databricks Metrics

---

# Common Performance Bottlenecks

- Data skew
- Small files
- Large shuffles
- Wide transformations
- Poor partitioning
- Unoptimized joins
- Reading unnecessary columns

---

# Best Practices

- Read only required columns.
- Filter early.
- Use Parquet instead of CSV.
- Partition large datasets.
- Broadcast small tables.
- Minimize shuffles.
- Cache reusable datasets.
- Monitor execution plans.
- Tune executor memory and cores.
- Regularly analyze warehouse statistics.

---

# Common Interview Questions

## Why is Spark slow?

Common reasons include excessive shuffling, poor partitioning, data skew, unnecessary caching, and inefficient joins.

---

## Difference between Repartition and Coalesce?

Repartition reshuffles data and can increase or decrease partitions.

Coalesce reduces partitions with minimal shuffle.

---

## What is Predicate Pushdown?

Filtering data at the storage layer so only required records are read.

---

## Why Parquet over CSV?

Parquet provides columnar storage, compression, and faster analytical queries.

---

## What causes data skew?

Uneven distribution of records across partitions, causing some executors to process significantly more data than others.

---

# Key Takeaways

- Performance optimization improves speed and reduces cloud costs.
- Spark optimization focuses on minimizing shuffles, choosing the right partitioning strategy, and using efficient storage formats.
- SQL and warehouse tuning complement Spark optimization.
- Continuous monitoring helps identify bottlenecks before they impact production.
