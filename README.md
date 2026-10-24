# SQL Data Engineering Interview Labs

Hands-on SQL Data Engineering projects focused on data quality, reconciliation, deduplication, window functions, production troubleshooting, and query optimization.

## Project 01: Insurance Claims Data Quality & Reconciliation

### Project Overview

This project demonstrates how to build and validate an insurance claims ingestion pipeline using Python, pandas, SQL, SQLite, and JupyterLab.

The objective is to detect data-quality issues, reconcile source and target records, quarantine invalid claims, and evaluate whether a batch is eligible for downstream publication.

**Note:** This project uses synthetic data for learning and demonstration.

### Technologies Used

- Python and pandas — CSV ingestion and data inspection
- SQLite — SQL landing and quarantine tables
- SQL — Data-quality checks and validation
- JupyterLab — Interactive development and troubleshooting

### Pipeline Architecture

```text
Insurance Claims CSV
        |
        v
Python / pandas Ingestion
        |
        v
SQLite Landing Table
        |
        v
SQL Data Quality Validation
        |
        +----> Duplicate Key Detection
        |
        +----> NULL Validation
        |
        +----> Count Reconciliation
        |
        +----> Amount Reconciliation
        |
        v
Data Quality Gate (PASS / FAIL)
        |
        +----> Invalid Records: Quarantine
        |
        +----> Eligible Records: Pending Batch Approval
```

### Data Quality Rules

1. Claim IDs must be present and unique.
2. Member IDs must not be NULL.
3. Source and target record counts must match.
4. Source and target financial totals must reconcile.
5. Critical data-quality failures must prevent batch publication.

### Hands-on Validation Results

| Validation Metric | Result |
|---|---:|
| Source records | 4 |
| Landing records | 4 |
| Source amount total | 675 |
| Target amount total | 675 |
| Missing member IDs | 1 |
| Excess claim-key occurrences | 1 |
| Quarantined records | 3 |
| Individually eligible records | 1 |
| Data Quality Gate | FAIL (Expected) |

The Data Quality Gate correctly identified invalid records, despite matching source and target counts and amounts.

### Production Troubleshooting Lessons

- Identified and corrected a CSV header interpretation issue that initially caused one record to be excluded.
- Investigated SQL syntax errors involving parentheses, aggregate functions, and column aliases.
- Used window functions to detect repeated business keys while preserving individual records.
- Stored invalid records in a separate quarantine table without modifying the original landing table.
- Distinguished successful ingestion reconciliation from successful business data-quality validation.

### Jupyter Notebook

[View SQL Data Quality Lab](Data_Quality_Lab.ipynb)

The notebook contains practical Python and SQL exercises with execution results.

### Key Learning

A successfully executed SQL query does not guarantee data correctness.

Reliable Data Engineering pipelines require validation at multiple levels, including record counts, financial totals, mandatory attributes, business-key uniqueness, and record-level integrity.

### Upcoming SQL Labs

- Question 02: Deterministic Deduplication using ROW_NUMBER()
- Question 03: Troubleshooting JOIN Fan-Out
- Question 04: Month-over-Month Analysis using LAG()
- Question 05: BigQuery Query Cost Optimization





---

**Author:** VenuGopal Komati

**Focus:** SQL | Python | Data Engineering | GCP | BigQuery | PySpark
