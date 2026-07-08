# Apply Filters to SQL Queries

**Analyst:** Mohammad
**Tables used:** `log_in_attempts`, `employees`
**Operators applied:** AND, OR, NOT, LIKE

---

## Project Description

As a security professional at a large organization, I was tasked with investigating potential security issues involving login attempts and employee machines. Using SQL filters on the organization's `log_in_attempts` and `employees` tables, I retrieved specific subsets of data to support the investigation — including after-hours failed logins, logins on suspicious dates, logins originating outside Mexico, and employee machines in specific departments requiring security updates.

---

## Retrieve After Hours Failed Login Attempts

A potential security incident occurred after business hours. I needed to identify all failed login attempts that took place after 18:00.

**Query:**
```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = 0;
```

**How it works:**
- `WHERE login_time > '18:00'` filters for attempts that occurred after 6:00 PM
- `AND success = 0` additionally requires the attempt to have failed (0 = failed, 1 = succeeded)
- Using `AND` means **both** conditions must be true simultaneously — only rows where the login was both after hours AND unsuccessful are returned

This narrows the results to the exact records most relevant to the after-hours incident investigation.

---

## Retrieve Login Attempts on Specific Dates

A suspicious event occurred on 2022-05-09. I needed to review all login attempts from that day and the day before (2022-05-08).

**Query:**
```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

**How it works:**
- `WHERE login_date = '2022-05-09'` matches attempts on the day of the suspicious event
- `OR login_date = '2022-05-08'` also includes the day before
- Using `OR` means **either** condition being true is enough — any login from either date is returned
- Note: even though both conditions filter the same column (`login_date`), the column name must be written out in full for each condition — `WHERE login_date = '2022-05-09' OR '2022-05-08'` would not work

---

## Retrieve Login Attempts Outside of Mexico

The team determined that suspicious activity did not originate from Mexico. I needed to find all login attempts from outside Mexico. The `country` column uses both `MEX` and `MEXICO` as values for Mexico.

**Query:**
```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

**How it works:**
- `LIKE 'MEX%'` matches any value in the `country` column that starts with "MEX" — this covers both `MEX` and `MEXICO` with a single pattern, using `%` as a wildcard for any characters that follow
- `NOT` negates the condition, so only rows where the country does **not** start with "MEX" are returned
- This approach is more efficient than writing `NOT country = 'MEX' AND NOT country = 'MEXICO'` separately

---

## Retrieve Employees in Marketing

The team needed to perform security updates on machines for Marketing department employees in the East building. Office values for the East building follow the pattern `East-` followed by a number (e.g., `East-170`, `East-320`).

**Query:**
```sql
SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East%';
```

**How it works:**
- `department = 'Marketing'` filters for Marketing employees only
- `AND office LIKE 'East%'` additionally requires the office to start with "East" — the `%` wildcard matches any room number that follows
- `AND` ensures both conditions are met: only Marketing employees in East building offices are returned

---

## Retrieve Employees in Finance or Sales

The team needed to apply a different security update to machines for employees in either the Finance or Sales departments.

**Query:**
```sql
SELECT *
FROM employees
WHERE department = 'Finance' OR department = 'Sales';
```

**How it works:**
- `department = 'Finance'` matches Finance employees
- `OR department = 'Sales'` also matches Sales employees
- Using `OR` means either condition being true is sufficient — employees from both departments are returned in one query, rather than running two separate queries

---

## Retrieve All Employees Not in IT

All employees outside the Information Technology department needed a specific machine update. IT employees had already received it.

**Query:**
```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

**How it works:**
- `NOT department = 'Information Technology'` excludes all IT employees
- Every other department is returned without needing to list them individually
- This is more efficient than writing `OR` conditions for every other department name, and automatically includes any new departments added in the future

---

## Summary

In this project, I used SQL filters with the `AND`, `OR`, `NOT`, and `LIKE` operators to investigate two security scenarios: suspicious login activity and employee machines requiring security updates. Across six queries, I filtered the `log_in_attempts` table by time, date, and country, and filtered the `employees` table by department and office location. The `LIKE` operator with `%` wildcards was particularly useful for matching partial values (such as country codes and building names) without requiring exact string matches.
