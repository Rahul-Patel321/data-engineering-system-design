# Data Security & Governance

## Overview

Data Security and Governance ensure that enterprise data is protected, compliant, accessible only to authorized users, and managed throughout its lifecycle.

Modern data platforms process sensitive information such as customer details, financial transactions, healthcare records, and business-critical data. Implementing strong security controls and governance policies is essential to prevent unauthorized access, ensure regulatory compliance, and maintain trust in data.

---

# Why Data Security Matters

Without proper security:

- Sensitive data may be exposed.
- Unauthorized users may access confidential information.
- Regulatory violations may occur.
- Financial loss and reputational damage can result.
- Compliance requirements may not be met.

Security should be integrated into every stage of the data pipeline.

---

# Security Principles

## Confidentiality

Only authorized users can access data.

Example

Customer account details should only be accessible to authorized employees.

---

## Integrity

Data should not be modified without authorization.

Example

Transaction amounts should not change unexpectedly.

---

## Availability

Data should remain accessible to authorized users whenever required.

Example

Business dashboards should remain available even during high traffic.

---

# Authentication vs Authorization

## Authentication

Verifies identity.

Examples

- Username & Password
- Multi-Factor Authentication (MFA)
- Single Sign-On (SSO)

---

## Authorization

Determines what an authenticated user is allowed to access.

Example

Data Engineer

↓

Read + Write

Business Analyst

↓

Read Only

---

# Role-Based Access Control (RBAC)

Permissions are assigned to roles rather than individuals.

Example

Admin

- Full Access

Data Engineer

- Read
- Write

Analyst

- Read Only

Auditor

- Read Logs

Benefits

- Easier administration
- Improved security
- Better compliance

---

# Principle of Least Privilege

Grant only the minimum permissions required to perform a task.

Example

A BI user should not have permission to delete production tables.

---

# Encryption

## Encryption at Rest

Protects stored data.

Examples

- Amazon S3
- Redshift
- Azure Data Lake

---

## Encryption in Transit

Protects data while moving between systems.

Examples

- HTTPS
- TLS
- SSL

---

# Data Masking

Sensitive information is partially hidden.

Examples

Original

9876543210

Masked

987******0

---

Email

rahul@example.com

↓

r****@example.com

---

# Tokenization

Sensitive values are replaced with unique tokens.

Example

Credit Card

4111 1111 1111 1111

↓

TKN_123456

Unlike encryption, tokens cannot be mathematically reversed without the token vault.

---

# Data Classification

Examples

Public

- Product Catalog

Internal

- Employee Directory

Confidential

- Financial Reports

Restricted

- Banking Transactions
- Customer PII

---

# Audit Logging

Track all important activities.

Examples

- Login attempts
- Table access
- Data updates
- Permission changes
- Pipeline executions

Audit logs support compliance and incident investigations.

---

# Data Governance

Data governance defines how data is managed across the organization.

Key Areas

- Ownership
- Data Quality
- Metadata
- Lineage
- Compliance
- Policies

---

# Data Lineage

Shows the complete journey of data.

Example

Source Database

↓

AWS Glue

↓

Amazon S3

↓

Amazon Redshift

↓

Power BI Dashboard

Benefits

- Easier debugging
- Impact analysis
- Regulatory compliance

---

# Compliance Standards

Examples

- GDPR
- HIPAA
- PCI DSS
- ISO 27001
- SOC 2

Financial organizations often follow PCI DSS for payment data.

---

# AWS Security Services

- AWS IAM
- AWS KMS
- AWS Secrets Manager
- AWS Lake Formation
- AWS CloudTrail
- Amazon Macie

---

# Azure Security Services

- Azure Active Directory
- Azure Key Vault
- Microsoft Purview
- Azure RBAC
- Azure Defender

---

# Best Practices

- Apply least privilege access.
- Use IAM roles instead of hardcoded credentials.
- Encrypt data at rest and in transit.
- Rotate secrets regularly.
- Enable audit logging.
- Implement RBAC.
- Classify sensitive data.
- Monitor unauthorized access.
- Use centralized secret management.
- Regularly review permissions.

---

# Common Interview Questions

## What is RBAC?

Role-Based Access Control assigns permissions to roles rather than directly to users, simplifying administration and improving security.

---

## Difference between Authentication and Authorization?

Authentication verifies identity.

Authorization determines access permissions.

---

## Difference between Encryption and Tokenization?

Encryption can be decrypted using a key.

Tokenization replaces sensitive data with non-sensitive tokens stored separately.

---

## Why use AWS Secrets Manager?

To securely store and rotate database passwords, API keys, and other secrets instead of hardcoding them in applications.

---

## What is Data Lineage?

Data lineage tracks the movement and transformation of data from its source to its final destination.

---

# Key Takeaways

- Security should be built into every layer of the data platform.
- Use RBAC and least privilege to minimize risk.
- Encrypt sensitive data both at rest and in transit.
- Maintain audit logs and data lineage for compliance.
- Strong governance improves trust, security, and regulatory readiness.
