# yousef_hassan_2305049_lab4

## what i did

- so i set up mutillidae and then i used semgrep to automatically look for vulnerabilities in the code

===========================================================================================================================================================
## the SQL injection i found

- the SQL injection vulnerability where the code takes user input and just puts it directly into database queries without checking it first
code example --> "SELECT * FROM accounts WHERE username='" . $username . "'";
it takes the username and put it right into the query thats bad because if someone puts in something like ' OR '1' = '1 then the query becomes
--->  SELECT * FROM accounts WHERE username='' OR '1' = '1'
and that would return ALL the user accounts.  in my video i actually tried this attack and it worked i was able to bypass the login
=======================================
my semgrep rule for SQL injection
i made this custom rule to find SQL injection
pattern-regex: 'SELECT.*\..*\$'
what this does is it looks for any SELECT statements in the code that have a dot then a dollar sign which in php means theyre using variables directly
 in the query which is how SQL injection happens

===========================================================================================================================================================
## the XSS vulnerability i found

then theres this xss vulnerability where the website takes whatever you put in the URL and just displays it on the page without making it safe first
the vulnerable code looks like this ---> <input type="hidden" name="page" value="<?php echo $_REQUEST['page']?>">

see how it just echoes whatever is in the page parameter right into the HTML? thats dangerous because i can put javascript code in there

- how i exploited the XSS i went to this URL in my browser

http://localhost/source-viewer.php?page="><script>alert('XSS')</script>
and what happens is my javascript code actually runs and shows an alert box which proves the vulnerability is real
===========================================================================================================================================================
what semgrep found:

6 SQL injection vulnerabilities in the code
1 XSS vulnerability in the code
