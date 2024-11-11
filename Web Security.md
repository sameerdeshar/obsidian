**HTTP Security Headers** help protect web applications from attacks like XSS, clickjacking, and more. Here’s a quick breakdown of key headers:

### 1. Content-Security-Policy (CSP)
CSP defines allowed sources for content, reducing the risk of malicious code injection.  
Example:
```plaintext
Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.example.com; style-src 'self'
```
- `default-src 'self'`: Only allows resources from the same domain.
- `script-src 'self' https://cdn.example.com`: Scripts are permitted from the same domain and a specific CDN.
- `style-src 'self'`: Stylesheets allowed only from the same domain.

### 2. Strict-Transport-Security (HSTS)
Enforces HTTPS connections to the site.  
Example:
```plaintext
Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
```
- `max-age`: Duration for HTTPS enforcement.
- `includeSubDomains`: Applies to all subdomains.
- `preload`: Adds the site to a preload list for HSTS.

### 3. X-Content-Type-Options
Prevents MIME type guessing, reducing the risk of content injection.  
Example:
```plaintext
X-Content-Type-Options: nosniff
```
- `nosniff`: Forces the browser to use the specified Content-Type.

### 4. Referrer-Policy
Controls what referrer info is sent when users navigate.  
Examples:
- `no-referrer`: Sends no referrer info.
- `same-origin`: Referrer info sent only within the same domain.
- `strict-origin`: Sends only the origin, maintaining HTTPS if used.
- `strict-origin-when-cross-origin`: Full URL for same-origin, origin-only for cross-origin.

Tools like [securityheaders.io](https://securityheaders.io/) can help analyze these headers on any website.