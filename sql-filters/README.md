# Apply Filters to SQL Queries

## Overview
This project is a SQL filtering exercise completed as part of the Google Cybersecurity Certificate (Course 5: Tools of the Trade — Linux and SQL). Using SQL logical operators (AND, OR, NOT) and pattern matching (LIKE), I investigated potential security issues by querying an organization's login attempt and employee data.

## Scenario
As a security analyst, I investigated suspicious login activity and identified employee machines requiring security updates. I used SQL filters on two tables — `log_in_attempts` and `employees` — to retrieve specific subsets of data supporting each investigation.

## Skills Demonstrated
- Filtering with `AND` to narrow results by requiring multiple conditions simultaneously
- Filtering with `OR` to broaden results by accepting either of multiple conditions
- Filtering with `NOT` to exclude specific groups efficiently
- Using `LIKE` with `%` wildcards to match partial string values (e.g., country codes, building names)
- Filtering by date and time columns in SQL
- Applying filters across multiple tables for different investigation scenarios

## Files
- [`apply-filters-to-sql-queries.md`](./apply-filters-to-sql-queries.md) — full written portfolio document
- [`apply-filters-to-sql-queries.pdf`](./apply-filters-to-sql-queries.pdf) — PDF version

## Key Queries
- After-hours failed logins: `WHERE login_time > '18:00' AND success = 0`
- Specific dates: `WHERE login_date = '2022-05-09' OR login_date = '2022-05-08'`
- Outside Mexico: `WHERE NOT country LIKE 'MEX%'`
- Marketing + East building: `WHERE department = 'Marketing' AND office LIKE 'East%'`
- Finance or Sales: `WHERE department = 'Finance' OR department = 'Sales'`
- Not IT: `WHERE NOT department = 'Information Technology'`
