
# SQL Question 2 — Customer Deduplication & CDC

## Project Overview

Built a hands-on customer deduplication and
incremental CDC processing lab using Python,
pandas, SQLite, SQL, and JupyterLab.

## Business Problem

Customer records may arrive multiple times,
out of order, or with identical timestamps.

The objective is to retain the latest valid
customer version while preserving landing data.

## Technologies

- Python
- pandas
- SQLite / SQL
- JupyterLab

## Implementation

1. CSV ingestion and landing table creation
2. Source-to-target count reconciliation
3. ROW_NUMBER() window functions
4. CTE-based latest-record selection
5. Deterministic timestamp tie-breaking
6. Late-arriving event handling
7. Conditional UPSERT using ON CONFLICT
8. Idempotency validation through event replay
9. Post-load Data Quality checks
10. CDC audit and value-level reconciliation

## Validated Lab Results

| Metric | Result |
|---|---|
| Landing records | 4 |
| Distinct landing customers | 2 |
| Final current-state customers | 2 |
| UPSERT attempts | 4 |
| Inserts | 1 |
| Updates | 1 |
| Ignored attempts | 2 |
| Value-level matches | 2 |
| Value-level mismatches | 0 |
| Final validation | PASS |

## Key Engineering Learnings

- Latest arrival does not always mean latest event.
- Deduplication requires deterministic ordering.
- Older events must not overwrite newer target data.
- UPSERT logic should support safe retries.
- Matching record counts alone does not prove
  data correctness.

## Files

- `customers.csv` — Synthetic source customer records
- `SQL_Question_02_Deduplication.ipynb` —
  JupyterLab implementation and validations

## Note

This is a hands-on educational project using
synthetic customer data, not a production deployment.
