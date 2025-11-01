# Shells

**Reverse Shell** - reverse shells initiate from the target machine back to the attacker machine. This can help avoid IDS and bypass firewalls since the connection is coming from and not to the machine. 
- you need to set up a listener for these.
- reverse shells connect back to the listener and you interact with it from there.
- **Any port can be used to wait for a connection, but attackers and pentesters tend to use known ports used by other applications like 53, 80, 8080, 443, 139, or 445.** This is to blend the reverse shell with legitimate traffic and avoid detection by security appliances.
- [Reverse shell payloads cheatsheet](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
