# random information about sql databases

**MariaDB**

`root` username allows you to login to mariadb without providing a password
`-U` switch allows you to provide a username to login to MariaDB

## USING MARIADB ON TERMINAL

`mariadb -u root -h ip-address --skip-ssl` - this is going to log you in

DO NOT FORGET TO ADD THE `;` AT THE END OF EVERY COMMAND IF YOU WANT IT TO RETURN ANYTHING BACK. 

You have to select the database before you're able to really interact or dump the contents within any of the table. Do this by using `USE db_name` and then to dump contents use `SELECT * FROM tablename`

