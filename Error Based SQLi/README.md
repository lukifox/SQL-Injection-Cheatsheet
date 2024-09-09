# MySQL Error based SQL Injection Cheatsheet

This is probably the easiest vulnerability along the SQL Injection attack. An attacker can enumerate and dump the MySQL database by using the SQL error messages to his advantage.

## Detecting the vulnerability

<code>https://site.com/index.php?id=1</code>
Website load successfully.

<code>https://site.com/index.php?id=1'</code>
Error message show up: <code>You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near...</code>
