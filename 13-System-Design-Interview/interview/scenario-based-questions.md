# Scenario-Based Data Engineering Interview Guide

This guide focuses on real-world production scenarios commonly discussed in Data Engineer and Senior Data Engineer interviews.

---

# Scenario 1

## Your AWS Glue job suddenly takes 5 hours instead of 30 minutes.

### How would you investigate?

Start with:

- Has the input data volume increased?
- Has the schema changed?
- Were new joins introduced?
- Did partitioning change?
- Did the cluster configuration change?

Check:

- Glue Job Metrics
- CloudWatch Logs
- Spark UI
- Input record count
- Output record count

Possible Causes

- Data skew
- Too many small files
- Shuffle-heavy joins
- Reading unnecessary columns
- Full load instead of incremental load

Possible Solutions

- Filter early
- Broadcast small tables
- Compact small files
- Partition properly
- Use Parquet
- Tune Spark partitions

---

# Scenario 2

## Business reports show duplicate records.

### Investigation

Check

- CDC logic
- Primary key
- Merge logic
- Incremental load process
- Retry mechanism

Possible Solution

Use ROW_NUMBER()

Keep only latest record.

Validate primary keys.

Implement idempotent pipeline.

---

# Scenario 3

## Dashboard data is delayed by 4 hours.

Possible Reasons

- Source delay
- Failed ETL
- Scheduler issue
- Long-running Spark job
- Warehouse loading delay

Investigation

- CloudWatch
- Scheduler logs
- Glue Job
- Redshift Load History

---

# Scenario 4

## Millions of very small files are generated every day.

Problems

- Slow reads
- Expensive metadata
- Long ETL jobs

Solutions

- Compaction
- Coalesce
- Repartition
- Larger output files
- Partition optimization

---

# Scenario 5

## One Spark executor is overloaded while others are idle.

Problem

Data Skew

Solutions

- Broadcast Join
- Salting
- Repartition
- Better partition key

---

# Scenario 6

## Business wants reports every 5 minutes instead of every day.

Current

Batch

Need

Near Real-Time

Architecture

```
Source

↓

Kafka

↓

Spark Streaming

↓

S3

↓

Warehouse

↓

Dashboard
```

---

# Scenario 7

## Source schema changes unexpectedly.

Example

A new column is added.

Approach

- Schema evolution
- Validation
- Versioning
- Alerting
- Backward compatibility

---

# Scenario 8

## Redshift queries become very slow.

Possible Reasons

- Missing Sort Key
- Missing Distribution Key
- Vacuum required
- Analyze required
- Large scans
- Bad joins

Optimization

- Vacuum
- Analyze
- Compression
- Better Distribution Key
- Better Sort Key

---

# Scenario 9

## Daily pipeline suddenly fails.

Checklist

- Source availability
- IAM permissions
- Storage availability
- Glue logs
- Spark logs
- Schema validation
- Recent deployment

---

# Scenario 10

## Business asks for historical replay.

Approach

Store immutable raw data.

Never overwrite raw layer.

Replay transformations from source data.

---

# Scenario 11

## Data quality issues are found.

Checks

- NULL values
- Duplicate records
- Invalid dates
- Invalid IDs
- Range validation
- Referential integrity

---

# Scenario 12

## Storage cost increases significantly.

Optimization

- Lifecycle policies
- Compression
- Parquet
- Incremental loads
- Archive old data
- Delete temporary data

---

# Scenario 13

## Sensitive customer data must be protected.

Discuss

- IAM
- Encryption
- Secrets Manager
- Data Masking
- Row Level Security
- Least Privilege

---

# Scenario 14

## Business wants to migrate from on-premise Hadoop to AWS.

Migration Plan

Assessment

↓

Data Migration

↓

Validation

↓

Parallel Run

↓

Production Cutover

↓

Monitoring

---

# Scenario 15

## Business asks whether to use Batch or Streaming.

Choose Batch When

- Daily reporting
- Low-frequency processing
- Lower cost

Choose Streaming When

- Fraud detection
- Live dashboards
- IoT
- Real-time alerts

---

# Production Mindset

Whenever you answer a scenario:

1. Understand the problem.
2. Ask clarifying questions.
3. Identify possible root causes.
4. Explain your investigation approach.
5. Recommend a solution.
6. Discuss trade-offs.
7. Explain monitoring.
8. Mention prevention strategies.

---

# Common Follow-up Questions

Interviewers may ask:

- How would you debug this?
- How would you monitor it?
- How would you prevent it?
- What metrics would you track?
- How would this scale?
- How would you reduce cost?
- What happens if one service fails?

Always think beyond fixing the immediate issue.

---

# Senior Data Engineer Mindset

A Senior Data Engineer should not only solve today's problem but also improve the system to reduce the likelihood of similar issues in the future.

Focus on:

- Scalability
- Reliability
- Maintainability
- Observability
- Security
- Cost Efficiency

These principles should guide your design decisions and troubleshooting approach.
