# Notes-cybersecurity-101

## web-app-basics

**Security Headers**

https://securityheaders.com/
- can be used to check security headers of any website.

**CSP headers**
  - additional security header than can help mitigate XSS attacks because admins specify the domains are considered safe.
  - There's a few different properties such as `default-src` and `script-src` that give admins the options for various levels of granularity, specifying which domains are allowed and for what types of content.

**Strict Transport Security Headers**
  - The HSTS header ensures that web browsers will always connect over HTTPS
    
**X Content Type Options**
  - The X-Content-Type-Options header can be used to instruct browsers not to guess the MIME time of a resource but only use the Content-Type header

**Referrer Policy**
  - Controls the amount of information sent to the destination web server when a user is redirected from the source web server, such as when they click a hyperlink. The header is available to allow a web administrator to control what information is shared.

