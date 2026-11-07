# SQL Question 4 — Month-over-Month Revenue Analysis

## Business Problem

A banking revenue reporting pipeline needs to calculate
month-over-month (MoM) growth across multiple regions.

A key challenge is handling missing calendar months,
because SQL LAG() retrieves the previous available row,
not necessarily the previous calendar month.

## Objectives

- Calculate previous-month revenue using LAG().
- Calculate MoM absolute and percentage change.
- Perform region-wise calculations using PARTITION BY.
- Detect missing reporting periods.
- Generate a monthly date spine.
- Avoid misleading MoM growth when revenue is missing.
- Validate source and target records.

## Technologies

- SQL (SQLite)
- Python
- pandas
- JupyterLab

## SQL Concepts Practiced

- LAG() window function
- OVER(), PARTITION BY, ORDER BY
- Common Table Expressions (CTEs)
- WITH RECURSIVE
- UNION ALL
- LEFT JOIN
- CASE WHEN
- COALESCE
- COUNT, SUM and DISTINCT
- Bidirectional EXCEPT reconciliation

## Example 1 — Normal MoM Calculation

| Region | Month | Revenue | MoM Growth |
|---|---|---:|---:|
| South | January | 10000 | NULL |
| South | February | 12000 | +20% |
| South | March | 15000 | +25% |
| North | January | 20000 | NULL |
| North | February | 18000 | -10% |
| North | March | 21000 | +16.67% |

## Example 2 — Missing-Month Scenario

| Month | Revenue | MoM Growth |
|---|---:|---:|
| January | 10000 | NULL |
| February | NULL | NULL |
| March | 15000 | NULL |

Without calendar validation, a naive LAG() calculation
would compare March against January and report 50%
growth, which is not a valid February-to-March comparison.

## Validation Results

- Normal regional MoM calculations: PASS
- Missing-month detection: PASS
- March MoM correctly undefined: PASS
- Source-to-target record differences: 0
- Duplicate region-month keys: 0
- Final notebook validation: PASS

## How to Run

1. Install Python, pandas and JupyterLab.
2. Open SQL_Question_04_Month_Over_Month.ipynb.
3. Run all cells in sequence.
4. Verify the final validation output.

The notebook includes code to create sample SQLite tables.
The local monthly_revenue.db file is not required for upload.

## Key Learning

A successful SQL window function can still produce
incorrect business results when reporting periods are missing.

Always validate calendar completeness and business grain
before publishing financial MoM metrics.
