### Gobuster Notes

#### **Using `dir` Mode**

**Basic Command:**
```bash
gobuster dir -u "http://www.example.thm" -w /path/to/wordlist
```

**Explanation of Flags:**
- `dir`: Enables directory and file enumeration.
- `-u`: Sets the target URL.
- `-w`: Specifies the wordlist for scanning.

**Example Usage:**
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```
- **-r**: Follows redirect responses (e.g., 301 status).

**File Enumeration Example:**
To specify file extensions:
```bash
gobuster dir -u "http://www.example.thm" -w /path/to/wordlist -x .php,.js
```
- **-x**: Scans for specific file types (e.g., `.php`, `.js`).

---

#### **Using `dns` Mode**

**Basic Command:**
```bash
gobuster dns -d example.thm -w /path/to/wordlist
```

**Explanation of Flags:**
- `dns`: Enables subd### Gobuster Notes

#### **Using `dir` Mode**

**Basic Command:**
```bash
gobuster dir -u "http://www.example.thm" -w /path/to/wordlist
```

**Explanation of Flags:**
- `dir`: Enables directory and file enumeration.
- `-u`: Sets the target URL.
- `-w`: Specifies the wordlist for scanning.

**Example Usage:**
```bash
gobuster dir -u "http://www.example.thm" -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
```
- **-r**: Follows redirect responses (e.g., 301 status).

**File Enumeration Example:**
To specify file extensions:
```bash
gobuster dir -u "http://www.example.thm" -w /path/to/wordlist -x .php,.js
```
- **-x**: Scans for specific file types (e.g., `.php`, `.js`).

---

#### **Using `dns` Mode**

**Basic Command:**
```bash
gobuster dns -d example.thm -w /path/to/wordlist
```

**Explanation of Flags:**
- `dns`: Enables subdomain enumeration.
- `-d example.thm`: Sets the target domain.
- `-w`: Specifies the wordlist for subdomain names.

**Example Usage:**
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```
- **gobuster dns**: Enumerates subdomains on the target domain.
- **-d**: Specifies the domain, e.g., `example.thm`.
- **-w**: Sets the wordlist (`subdomains-top1million-5000.txt`). Each entry is used to form DNS queries (e.g., `all.example.thm`).omain enumeration.
- `-d example.thm`: Sets the target domain.
- `-w`: Specifies the wordlist for subdomain names.

**Example Usage:**
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```
- **gobuster dns**: Enumerates subdomains on the target domain.
- **-d**: Specifies the domain, e.g., `example.thm`.
- **-w**: Sets the wordlist (`subdomains-top1million-5000.txt`). Each entry is used to form DNS queries (e.g., `all.example.thm`).


### VHost (virtual host)
	### Gobuster - Using `vhost` Mode

**Purpose:**  
The `vhost` mode in Gobuster allows brute-forcing of virtual hosts (websites on the same server, using the same IP but identified by different hostnames). Unlike `dns` mode, which performs DNS lookups, `vhost` mode sends requests to the URL by combining the configured HOSTNAME with each wordlist entry.

**Basic Command:**
```bash
gobuster vhost -u "http://example.thm" -w /path/to/wordlist
```

**Example Usage with Additional Flags:**
```bash
gobuster vhost -u "http://10.10.247.28" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```

**Explanation of Important Flags:**
- **-u**: Target URL for virtual host scanning.
- **-w**: Wordlist to use for testing possible hostnames.
- **--domain**: Sets the base domain to append to each wordlist entry.
- **--append-domain**: Adds the domain from `--domain` to each wordlist entry (e.g., `blog.example.thm`).
- **--exclude-length**: Excludes responses based on the content length (useful to ignore duplicate or unwanted responses).

**Quick Help:**  
For a full list of available flags:
```bash
gobuster vhost --help
```

**Commonly Used Flags Summary:**
- `-u`: Target URL
- `-w`: Wordlist path
- `--domain`: Base domain for virtual hosts
- `--append-domain`: Enables domain appending to each entry
- `--exclude-length`: Filters results based on response length