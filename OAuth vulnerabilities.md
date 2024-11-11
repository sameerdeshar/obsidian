# OAuth 2.0 Key Concepts

Understand these OAuth 2.0 concepts to secure web applications or conduct pentesting effectively.

---

## 1. Resource Owner
- **Definition**: The person who controls specific data and can authorize apps to access it.
- **Example**: You, as a coffee shop customer, can control your account info and allow the shop's app to access it.

## 2. Client
- **Definition**: The app or service requesting access to data.
- **Example**: The coffee shop’s app, which you use to order and pay, acts as the client.

## 3. Authorization Server
- **Definition**: Issues access tokens to clients after verifying the resource owner's consent.
- **Example**: The coffee shop’s backend that authenticates you and grants access to the app.

## 4. Resource Server
- **Definition**: Hosts and protects data, allowing access only with valid tokens.
- **Example**: The coffee shop's database that stores your account info and order history.

## 5. Authorization Grant
- **Definition**: A temporary credential the client uses to get an access token.
- **Types**: Authorization Code, Implicit, Password, Client Credentials.
- **Example**: Logging in to the app grants an authorization code for access.

## 6. Access Token
- **Definition**: A credential that allows the client to access data temporarily.
- **Example**: Once logged in, the app uses an access token to order coffee without asking you to re-login.

## 7. Refresh Token
- **Definition**: Used to obtain a new access token without re-authentication.
- **Example**: When your access token expires, the app uses a refresh token to keep you logged in.

## 8. Redirect URI
- **Definition**: The URL where the authorization server sends the user after login.
- **Example**: After logging in, the app redirects you to the server’s confirmation page.

## 9. Scope
- **Definition**: Limits the client’s access to specified data.
- **Example**: The app may request access to your order history and payment info.

## 10. State Parameter
- **Definition**: Ensures the response matches the client’s request, preventing CSRF attacks.
- **Example**: The app sends a state parameter with the login request for added security.

## 11. Token & Authorization Endpoint
- **Authorization Endpoint**: Where the resource owner authenticates and authorizes the client.
- **Token Endpoint**: Where the client exchanges grants for access tokens.

---

## OAuth 2.0 Authorization Code Flow

The **Authorization Code Flow** is the most common and secure OAuth 2.0 flow, primarily used by web and mobile apps to obtain access tokens. It involves the following steps:

1. **Resource Owner Authorization**: The client (e.g., coffee shop app) directs the user to the authorization server (e.g., coffee shop's backend) for authentication and authorization. The user logs in and grants permission.
    
2. **Authorization Code Grant**: The authorization server provides an **Authorization Code** to the client via a redirect URI.
    
3. **Exchange Authorization Code for Access Token**: The client sends the authorization code to the **Token Endpoint** of the authorization server, along with client credentials (if applicable) to request an access token.
    
4. **Access Token Issuance**: The authorization server verifies the authorization code and issues an **Access Token** (and optionally a **Refresh Token**) back to the client.
    
5. **Access Resource Server**: The client uses the access token to access resources on the **Resource Server** (e.g., coffee shop’s database) on behalf of the user.


Here’s a quick breakdown of the OAuth 2.0 Authorization Code Flow in simple text, which you could sketch or adapt into a minimal diagram on your end:
t
1. **User → Client**: User wants to access a resource, so the Client (like the coffee shop app) initiates a request.
2. **Client → Authorization Server**: Client redirects User to the Authorization Server for login and consent.
3. **Authorization Server → Client**: Authorization Server sends an Authorization Code to the Client.
4. **Client → Authorization Server**: Client exchanges the Authorization Code for an Access Token.
5. **Client → Resource Server**: Client uses the Access Token to request resources on behalf of the User.



The **authorization code** is a temporary, single-use code that serves as a bridge between Facebook and Spotify. Here’s why it’s important, how it’s used, and what makes it secure:

### What the Authorization Code Does
The authorization code plays a crucial role in OAuth security by separating the user login from the access request. Here’s how it works:

1. **Temporary, One-Time Use**: The authorization code is a short-lived code that can only be used once by Spotify. After the user approves access on Facebook, Facebook provides this code to Spotify.
2. **Access Token Request**: Spotify uses the authorization code to request an **access token** from Facebook. Spotify exchanges the authorization code at Facebook’s **token endpoint** by including:
   - **Spotify’s credentials** (Client ID and Client Secret).
   - **Authorization Code** from Facebook.
   - **Redirect URI** (must match the initial request URI for security).
   
   By using this code in exchange for an access token, Spotify ensures that the request is coming from an authorized source (itself) and that Facebook can validate the original user approval.

### Why This Step Is Important
The separation between the authorization code and the access token is key to security. It minimizes exposure of the access token by only issuing it directly to Spotify’s back-end server. This approach avoids the access token appearing on the client-side, where it could be intercepted more easily.

### How Facebook Issues and Validates the Access Token
- **Token Issuance**: When Spotify requests an access token using the authorization code, Facebook first checks:
   - That the authorization code is valid and hasn’t been used.
   - That Spotify’s Client ID and Client Secret are correct.
   - That the redirect URI matches the original.
   
   Once verified, Facebook issues an **access token** back to Spotify, which represents Spotify’s permissions to access your profile data.

- **Token Validation**: Later, whenever Spotify uses this token to request data, Facebook will:
   - Check if the token is still valid (it may have an expiration time).
   - Verify the token against the permissions that you approved.
   
   Facebook may store the token details temporarily in its database to check that it’s still active and belongs to the authorized client (Spotify).

### Security Against Interception
OAuth is designed to be secure against interception, but here’s how it manages specific threats:

1. **HTTPS**: OAuth typically requires all communication over HTTPS, which encrypts data to prevent attackers from seeing the authorization code or access token in transit.

2. **Authorization Code Confidentiality**: Since the authorization code is short-lived and used only by the server side of the client (Spotify’s back-end), it reduces exposure to attacks like **token interception**.

3. **State Parameter**: The **state** parameter, added to the initial request, helps prevent **CSRF attacks** by ensuring that the response Facebook sends back is tied to Spotify’s request. Spotify can confirm that the response is valid by checking that the state matches what it sent.

4. **Access Token Expiration and Refresh**: The access token has a limited lifespan, so even if someone intercepts it, the token will expire, limiting potential damage. A refresh token, if issued, also requires Spotify’s credentials for a new access token.

5. **Token Validation on Facebook’s End**: Facebook continuously validates each request that uses the access token, ensuring that the token is still active and matches the approved permissions. This check happens at Facebook’s resource server, which controls the data being accessed.

OAuth 2.0’s layered security mechanisms—like the authorization code flow, HTTPS, and token expiration—make it robust against interception risks.









JWT, or **JSON Web Token**, is commonly used in OAuth 2.0 as a format for **access tokens**. Here’s where it fits into the process and why it’s valuable in OAuth and similar authentication/authorization flows:

### Where JWT Fits in OAuth
In OAuth 2.0, when the authorization server (like Facebook) issues an access token to the client (like Spotify), this access token can be in the form of a **JWT**. Unlike a basic token (a random string), a JWT has special structure and features that enhance security and usability:

1. **Self-contained Information**: JWTs carry their own data within the token, including user identity, permissions (scope), and expiration details. This makes JWTs **self-contained**, meaning the resource server (Facebook's data server) doesn’t have to check with the authorization server every time to validate a token.

2. **JWT Structure**: A JWT is composed of three parts:
   - **Header**: Contains metadata about the token, like the algorithm used for signing (e.g., `HS256`).
   - **Payload**: Holds the token's claims, such as user info and permissions.
   - **Signature**: Verifies that the token is authentic and hasn’t been tampered with.

3. **Example JWT Token**: Here’s a simplified JWT to show what one looks like:
   ```
   eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
   .
   eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ
   .
   SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
   ```
   This token can be easily decoded to see its contents (the payload), but its signature verifies its integrity and authenticity.

### Why JWT Is Used in OAuth
JWTs offer several advantages as access tokens in OAuth:

1. **Efficiency**: Because JWTs carry all necessary information within them, the resource server can verify and decode the JWT without having to make a call back to the authorization server. This reduces server load and improves speed.

2. **Security via Signature**: The JWT is signed by the authorization server’s private key, ensuring that the token is tamper-proof. The resource server (Facebook’s data server) can validate the JWT with the public key. Any attempt to change the JWT’s data will invalidate the signature.

3. **Compact and Portable**: JWTs are URL-safe and easy to pass between services, whether in HTTP headers, URL parameters, or cookies.

4. **Expiration and Revocation**: JWTs contain an expiration date, so they automatically become invalid after a certain period. Though they’re self-contained, OAuth implementations sometimes combine JWTs with additional mechanisms, like token blacklists, to revoke tokens before they expire.

5. **Compatibility with Multiple Systems**: JWTs are widely compatible with various systems because they’re based on JSON, making them easily interpretable by different languages and platforms.

### Example Scenario Using JWT in OAuth
When Facebook issues a JWT access token to Spotify, the token might include:
   - **User ID**: So Spotify knows which Facebook user is connected.
   - **Scope**: Permissions like “read profile” or “read friends list.”
   - **Expiration**: A timestamp after which the token is no longer valid.
   - **Signature**: A cryptographic signature Facebook uses to confirm that it issued the token.

When Spotify wants to access Facebook data, it sends this JWT access token with the request. Facebook’s resource server decodes and validates the token’s signature and expiration time. If the token checks out, Facebook grants access to the requested data.

### JWT and Interception
Because JWTs are usually passed over HTTPS, they’re secure in transit. However, if someone were to steal a JWT, they could potentially use it until it expires. This is why it’s important to secure tokens well, use HTTPS, and issue short-lived tokens, refreshing them periodically to minimize security risks.

In summary, JWTs make OAuth workflows more efficient and secure by creating a self-contained, signed, and easily verifiable access token format.



### Identity Provider -> Okta, microsoft AD, google etc.
These are the which validates the request to authenticate to multiple apps from the single point.
### Service Provider -> slack, dropbox, 
Or any other products that is used in the office