# SQL #002
Count of employees \
Site: [[HackerRank](https://www.hackerrank.com/)] \
Difficulty per Site: Medium

## Problem 
Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code. [[Full Description](https://www.hackerrank.com/challenges/the-company/problem?isFullScreen=true)]

## ✅ Submitted Solution 

Uses COUNT(DISTINCT ...) to ensure unique role counts per company. \
Uses a simple JOIN with GROUP BY to aggregate results at the company level.
```

SELECT 
  comp.company_code, 
  comp.founder,
  COUNT(DISTINCT emp.lead_manager_code) AS total_lead_managers,
  COUNT(DISTINCT emp.senior_manager_code) AS total_senior_managers,
  COUNT(DISTINCT emp.manager_code) AS total_managers,
  COUNT(DISTINCT emp.employee_code) AS total_employees
FROM Company comp
JOIN Employee emp
  ON comp.company_code = emp.company_code
GROUP BY comp.company_code, comp.founder
ORDER BY comp.company_code;

```

## 🚀 Advanced Solution

Uses subqueries to aggregate role counts separately per company, then joins those aggregates to the Company table.

```

SELECT C.company_code, founder, num_lm, num_sm, num_m, num_e
FROM Company AS C
JOIN (SELECT company_code, count(distinct lead_manager_code) AS num_lm
     FROM Lead_Manager
     GROUP BY company_code) AS LM ON C.company_code = LM.company_code
JOIN (SELECT company_code, count(distinct senior_manager_code) AS num_sm
     FROM Senior_Manager
     GROUP BY company_code) AS SM ON C.company_code = SM.company_code
JOIN (SELECT company_code, count(distinct manager_code) AS num_m
     FROM Manager
     GROUP BY company_code) AS M ON C.company_code = M.company_code
JOIN (SELECT company_code, count(distinct employee_code) AS num_e
     FROM Employee
     GROUP BY company_code) AS E ON C.company_code = E.company_code
ORDER BY C.company_code

```
