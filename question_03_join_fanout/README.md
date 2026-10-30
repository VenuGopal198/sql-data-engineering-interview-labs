# SQL Question 3 — JOIN Fan-Out and Incorrect Aggregation

## Business Problem

An insurance claims report returned a total of **400**, while the correct claim-header amount was **300**.

## Root Cause

A one-to-many JOIN between `claims` and `claim_lines` repeated header-level claim amounts.

- Claim 1: amount 100, two matching lines
- Claim 2: amount 200, one matching line
- Incorrect joined total: 100 + 100 + 200 = 400
- Correct claim total: 100 + 200 = 300

## Solutions Implemented

1. Used `EXISTS` to select claims with matching detail records without duplicating header amounts.
2. Pre-aggregated claim lines using a CTE and `GROUP BY` before joining.
3. Preserved claim-level grain using a `LEFT JOIN`.
4. Used `COALESCE` to handle missing detail counts.

## Validation Results

| Validation | Result |
|---|---|
| Incorrect JOIN total | 400 |
| Corrected claim total | 300 |
| Source claim records | 2 |
| Claim-line records | 3 |
| Source minus target | 0 |
| Target minus source | 0 |
| Final validation | PASS |

## Skills Demonstrated

- INNER JOIN and LEFT JOIN
- One-to-many relationships and JOIN cardinality
- SQL aggregation and GROUP BY
- CTEs and pre-aggregation
- EXISTS and COALESCE
- Bidirectional EXCEPT reconciliation
- SQL data quality checks
- Python assertions
- Production troubleshooting

## Tech Stack

Python, SQLite, pandas, JupyterLab

## Key Learning

**A successful JOIN does not guarantee correct financial aggregation. Always validate the grain of each dataset before joining and summing measures.**

## Notebook

`SQL_Question_03_Join_Fanout.ipynb`

The notebook demonstrates the incorrect calculation, root-cause investigation, corrected queries, and validation checks.
