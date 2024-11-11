### Broken Access Control

**Definition**: Broken access control occurs when unauthorized users can access protected pages or functionality on a website, bypassing intended permissions.

**Risks**:
- Viewing sensitive information from other users.
- Accessing unauthorized features or functions.

**Example**: In 2019, a vulnerability allowed attackers to access frames from private YouTube videos. Users expect that private videos are fully protected, but this flaw demonstrated that attackers could reconstruct the video, highlighting a broken access control issue.

#### Key Takeaway
Proper access controls are essential to prevent unauthorized access to sensitive data and functionalities.

**Insecure Direct Object Reference (IDOR)**

IDOR is an access control vulnerability where an application exposes a Direct Object Reference, like an ID, allowing unauthorized access to resources. This flaw occurs if the application doesn’t validate whether the logged-in user has permission to access the referenced object.

**Example**:
If a user accesses a bank account page with a URL like `https://bank.example.com/account?id=111111`, changing the `id` to another user’s ID (e.g., `222222`) might allow unauthorized access to another account’s details if proper validation is missing. 

In summary, the issue isn't with exposing an ID but rather the lack of authorization checks on those references, leading to potential exposure of sensitive information.


