# John the Ripper

- `hashcat` -> helps you crack hashes with a wordlist
- `john` -> cracks hashes
- hash-id.py -> helps identify a hash type. Can be downloaded [here](https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py) if needed use `wget` or `curl` in terminal. Run with `python 3 hash-id.py`

<hr />

**Auto Cracking**

`john --wordlist=[path to wordlist] [path to file]`

<hr />

**Format Specific Cracking**

`john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt`
- *For windows hashes use the format nt*

<hr />
