# data-projects
# StratEdge Consulting – BI & Analytics Project

**Tools:** Power BI (dashboards), Salesforce (CRM leads), PostgreSQL (SQL data store), Python (EDA), Mockaroo (synthetic datasets)

This repository contains the end-to-end artefacts for a Business Intelligence & Business Analytics project delivered for a consulting scenario (StratEdge). The objective was to diagnose operational issues and implement data-driven dashboards aligned with a Balanced Scorecard.

## Highlights
- **Consultant Utilization Dashboard (Power BI):** under/over-utilization, billable vs non-billable, revenue potential.
- **Project Health Dashboard (Power BI):** delays vs target, budget vs billable revenue, project durations.
- **CRM Dashboard (Power BI + Salesforce):** conversion funnel, sources, rating, owner load.

## Data
- **Mockaroo CSVs:** `/data/` (consultants, projects, timesheets, clients)
- **Salesforce:** Lead objects pulled via Salesforce Developer Org (read-only). See `/salesforce/screenshots/`.

> Note: Some `.pbix` files are tracked with **Git LFS**.

## Notebooks (EDA)
- `/eda/BIBA.ipynb`: cleaning, joins, sanity checks, summary stats.

## SQL (PostgreSQL)
- Table creation and sample queries used to ingest & analyze data.

```sql
-- Example: create and load
CREATE TABLE consultants (
  consultant_id INT PRIMARY KEY,
  first_name TEXT, last_name TEXT,
  department TEXT, billable_rate NUMERIC, status TEXT
);
-- Load: \COPY consultants FROM '.../consultants.csv' CSV HEADER;

-- Example join
SELECT c.department, SUM(t.hours_worked) AS total_hours
FROM consultants c
JOIN timesheets t ON c.consultant_id = t.consultant_id
GROUP BY c.department;
