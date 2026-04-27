# SQL Injection – Basics

## Overview

SQL Injection is a vulnerability where user input is directly included in SQL queries without proper validation or sanitization. This allows an attacker to manipulate the query logic and access or modify database data.

## Vulnerable Query

Consider a login system:

```sql
SELECT * FROM users WHERE username = 'admin' AND password = '1234';
```

## Exploitation

An attacker can input:

```sql
' OR 1=1 --

```
This input modifies the original query:

```sql
SELECT * FROM users WHERE username = '' OR 1=1 --' AND password = '';
```

---
## Explanation

- The attacker closes the original string using `'`
- `OR 1=1` makes the condition always TRUE
- `--` comments out the rest of the query
- The password check is bypassed completely

## Root Cause

- Direct concatenation of user input into SQL queries  
- No input validation or sanitization  
- Absence of parameterized queries  

## Impact

- Authentication bypass  
- Unauthorized data access  
- Potential database modification or deletion  
- Full system compromise in severe cases  

## Mitigation

- Use parameterized queries (prepared statements)  
- Implement input validation  
- Use ORM frameworks where possible  
- Apply least privilege principle to database users
