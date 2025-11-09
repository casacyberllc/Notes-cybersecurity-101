# Gobuster

`gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r`
- finds all the directories in a domain ex `http://www.example.thm/shop`

`gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,js`
- this is going to specify the type of files you're looking for by adding `-x`

`gobuster dns -d example.thm -w /path/to/wordlist`
- finds all the subdomains ex `shop.example.thm`

