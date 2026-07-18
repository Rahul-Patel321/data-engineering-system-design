# PySpark Interview Guide

A production-oriented PySpark interview guide for Data Engineer and Senior Data Engineer interviews.

---

# 1. What is PySpark?

## Expected Answer

PySpark is the Python API for Apache Spark. It enables distributed data processing across a cluster for batch and streaming workloads.

---

## Why Interviewer Asks

To assess your understanding of distributed computing rather than just Python programming.

---

## Production Perspective

PySpark is widely used for large-scale ETL pipelines, data transformation, data quality checks, and machine learning preprocessing.

---

# 2. Why PySpark instead of Pandas?

| Pandas | PySpark |
|----------|----------|
| Single Machine | Distributed |
| Memory Bound | Cluster Computing |
| Small Data | Big Data |
| GBs | TBs / PBs |

---

## Production Perspective

Use Pandas for local analysis and small datasets.

Use PySpark for distributed data processing.

---

# 3. What is Lazy Evaluation?

## Expected Answer

PySpark does not execute transformations immediately.

Execution starts only when an action is triggered.

---

Example

```python
df.filter(...)
  .select(...)
  .groupBy(...)
```

Nothing runs yet.

Execution starts only when:

```python
df.show()
```

or

```python
df.write.parquet(...)
```

---

## Why Interviewer Asks

To evaluate whether you understand Spark execution.

---

# 4. What are Transformations?

Transformations create a new DataFrame.

Common Transformations

- select()
- filter()
- withColumn()
- drop()
- groupBy()
- join()
- union()
- orderBy()
- repartition()
- coalesce()

---

# 5. What are Actions?

Actions trigger execution.

Examples

- show()
- count()
- collect()
- first()
- take()
- write()

---

# 6. Difference between repartition() and coalesce()

## repartition()

- Shuffle occurs
- Increase or decrease partitions
- Better data distribution

## coalesce()

- No full shuffle
- Usually decrease partitions
- Faster than repartition for reducing partitions

---

## Production Tip

Use coalesce() when writing output files to reduce the number of small files.

---

# 7. What is Partitioning?

Partitioning splits data into multiple parts for parallel processing.

Benefits

- Faster queries
- Better parallelism
- Reduced execution time

Common Partition Columns

- Date
- Year
- Month
- Region
- Country

---

# 8. Explain Broadcast Join

Broadcast Join sends a small table to all executors.

Advantages

- Avoids shuffle
- Faster joins
- Better performance

Use when one table is significantly smaller than the other.

---

# 9. What causes Shuffle?

Common operations

- join()
- groupBy()
- distinct()
- orderBy()
- repartition()

Shuffles are expensive because data moves across executors.

---

# 10. How do you optimize a PySpark job?

Expected Answer

- Read only required columns
- Filter early
- Use Parquet
- Use partition pruning
- Broadcast small tables
- Cache reused DataFrames
- Avoid unnecessary shuffles
- Use incremental loads
- Tune Spark configurations

---

# 11. Cache vs Persist

## Cache

Stores data in memory.

## Persist

Can store in memory and/or disk using different storage levels.

Use persist() when the dataset may not fit entirely in memory.

---

# 12. What are Narrow and Wide Transformations?

## Narrow

No shuffle required.

Examples

- select()
- filter()
- withColumn()

## Wide

Shuffle required.

Examples

- join()
- groupBy()
- distinct()
- orderBy()

---

# 13. What file format should you use?

Recommended

✅ Parquet

Reasons

- Columnar storage
- Compression
- Predicate pushdown
- Faster queries

Avoid CSV for analytics workloads due to larger size and slower reads.

---

# 14. Explain the Spark Execution Flow

```
Driver Program
        │
        ▼
Spark Session
        │
        ▼
DAG Scheduler
        │
        ▼
Task Scheduler
        │
        ▼
Executors
        │
        ▼
Cluster
```

---

# 15. Common Spark Interview Questions

- Difference between DataFrame and RDD
- Why DataFrame instead of RDD?
- What is Catalyst Optimizer?
- What is Tungsten?
- What is Adaptive Query Execution (AQE)?
- What is partition pruning?
- What is predicate pushdown?
- What is skewed data?
- How do you handle skew?
- Difference between cache() and persist()

---

# 16. Production Challenges

| Problem | Solution |
|----------|----------|
| Too many small files | coalesce(), compaction |
| Data skew | Salting, broadcast joins, repartition |
| Slow joins | Broadcast small tables |
| High memory usage | Persist to disk, optimize partitions |
| Long-running jobs | Filter early, reduce shuffle |

---

# 17. Common Mistakes

❌ Using collect() on large datasets.

❌ Using Python UDFs when built-in Spark functions are available.

❌ Selecting all columns with `select("*")` unnecessarily.

❌ Repartitioning without understanding the impact.

❌ Writing thousands of tiny output files.

---

# 18. Production Best Practices

- Use DataFrames over RDDs for most ETL workloads.
- Store data in Parquet or Delta format.
- Partition large datasets thoughtfully.
- Monitor Spark UI for bottlenecks.
- Prefer built-in functions over Python UDFs.
- Use incremental processing instead of full reloads when possible.
- Tune executor memory and shuffle partitions based on workload.

---

# Final Interview Advice

When discussing PySpark:

✅ Explain *why* an optimization improves performance.

✅ Mention trade-offs (for example, broadcasting only works well for sufficiently small tables).

✅ Talk about reducing shuffles, partitioning strategy, and file formats.

Interviewers are usually more interested in your reasoning and performance awareness than in memorizing API names.
