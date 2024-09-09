# SQL-Injection-Cheatsheet

**This repository contains a advanced methodology of all types of SQL Injection.**
## General Process:

- Find Injection Point
- Understand the website behavior
- Send queries for enumeration
- Understanding WAF and Bypass
- Dump the database

# Cheat Sheet Tree

## MySQL Injection Cheatsheet
- Error or Union Based SQLi
  - Routed queries (Advanced WAF Bypass)
  - Bypass Error - The used SELECT statement have a different number of columns
  - New Attacking vectors (Bypassing WAF)
    - The alternative way of using **And 0**
    - The alternative way of using **Null**
- Boolean-Based | Blind SQLi
- Time Based SQLi
- Whitespace Filter Bypass
- Local File Inclusion (LFI)
- Privilege Escalation

## PostgreSQL Injection Cheatsheet
- Error or Union Based SQLi

## Oracle Injection Cheatsheet
- Error- or UNION-based SQLi
  
## MSSQL Injection Cheatsheet
- Error- or UNION-based SQLi
- Privilege Escalation
