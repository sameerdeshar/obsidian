---
tags:
  - kerberos
  - windows
  - active-directory
  - ticket
date:
---
### What is Kerberos?

Kerberos is the default authentication service for Microsoft Windows domains. It is intended to be more "secure" than NTLM by using third party ticket authorization as well as stronger encryption. Even though NTLM has a lot more attack vectors to choose from Kerberos still has a handful of underlying vulnerabilities just like NTLM that we can use to our advantage.


### How kerberos work?
-> It is a SSO network authentication protocol using ticket scheme.
Passwords are saved in SAM file in windows
```
system32/config/sam
```

1. Passwords hash is used to encrypt the whole message 
2. This is then decrpted by the authenticating server as it already has the password hash stored in the database while creating the user.
### Common Terminology 

- **Ticket Granting Ticket (TGT)** - A ticket-granting ticket is an authentication ticket used to request service tickets from the TGS for specific resources from the domain.
- **Key Distribution Center (KDC)** - The Key Distribution Center is a service for issuing TGTs and service tickets that consist of the Authentication Service and the Ticket Granting Service.
- **Authentication Serv****ice (AS)** - The Authentication Service issues TGTs to be used by the TGS in the domain to request access to other machines and service tickets.
- **Ticket Granting Service (TGS)** - The Ticket Granting Service takes the TGT and returns a ticket to a machine on the domain.  
    
- **Service Principal Name (SPN)** - A Service Principal Name is an identifier given to a service instance to associate a service instance with a domain service account. Windows requires that services have a domain service account which is why a service needs an SPN set.
- **KDC Long Term Secret Key (KDC LT Key)** - The KDC key is based on the KRBTGT service account. It is used to encrypt the TGT and sign the PAC.
- **Client Long Term Secret Key (Client LT Key)** - The client key is based on the computer or service account. It is used to check the encrypted timestamp and encrypt the session key.
- **Service Long Term Secret Key (Service LT Key)** - The service key is based on the service account. It is used to encrypt the service portion of the service ticket and sign the PAC.
- **Session Key** - Issued by the KDC when a TGT is issued. The user will provide the session key to the KDC along with the TGT when requesting a service ticket.
- **Privilege Attribute Certificate (PAC)** - The PAC holds all of the user's relevant information, it is sent along with the TGT to the KDC to be signed by the Target LT Key and the KDC LT Key in order to validate the user.


### Step-by-Step with Encryption and Hashing in Kerberos

---

### 1. **Authentication Phase (Getting the Ticket Granting Ticket - TGT)**

- **Step 1**: The user enters their **password ("password123")** on their workstation.
    
- **Step 2**: The workstation **hashes** the password using SHA-256 to create a **password hash**.
    
    - **Hashing the Password**:
        
        makefile
        
        Copy code
        
        `password_hash = SHA-256("password123")  # Example output (truncated for simplicity): 5e88489da59090b30...`
        
    - This hash is used as the key for encrypting messages with the **Authentication Server (AS)**.
- **Step 3**: The client sends a request to the **AS** with the username. No password is sent over the network.
    
- **Step 4**: The AS verifies the username and looks up the hashed password associated with it from its database.
    
- **Step 5**: The AS creates a **Ticket Granting Ticket (TGT)** and a **session key**. The TGT contains:
    
    - User ID
    - Timestamp
    - Expiration time
    - Session Key (encrypted)
- **Step 6**: The AS encrypts the TGT and session key with the **user’s hashed password** (so only the user can decrypt it).
    
    - **Encrypting the TGT and Session Key**:
        
        scss
        
        Copy code
        
        `encrypted_TGT = AES_encrypt(TGT, key=password_hash)`
        
    - The AS sends the **encrypted TGT and session key** back to the client.
- **Step 7**: The client receives the encrypted TGT and session key and **decrypts it using their hashed password**.
    
    - If decryption is successful, the user has authenticated. The client now has a valid TGT to use for requesting services.

---

### 2. **Ticket Granting Phase (Getting the Service Ticket)**

- **Step 8**: When the user wants to access a network service, they use the TGT to request access from the **Ticket Granting Server (TGS)**.
    
- **Step 9**: The client sends the TGT (encrypted) and an **Authenticator** to the TGS.
    
    - The **Authenticator** is a timestamp encrypted with the **session key** shared between the client and TGS.
    - **Creating the Authenticator**:
        ```scss
`authenticator = AES_encrypt(current_timestamp, key=session_key)```
        
- **Step 10**: The TGS decrypts the TGT using its own secret key (only the TGS and AS know this key). Once decrypted, it retrieves the session key and decrypts the Authenticator to verify the timestamp.
    
    - If the timestamp is valid, the TGS verifies that the request is genuine and not a replay.
- **Step 11**: The TGS creates a **Service Ticket** for the requested service, containing:
    
    - User ID
    - Expiration time
    - Session Key for client-service communication
    - This is encrypted with the service’s secret key.
- **Step 12**: The TGS sends the **encrypted Service Ticket** and a session key to the client.
    

---

### 3. **Service Access Phase (Using the Service Ticket)**

- **Step 13**: The client contacts the service, presenting:
    
    - The **Service Ticket** from the TGS.
    - A new **Authenticator** (timestamp encrypted with the session key shared with the service).
- **Step 14**: The service decrypts the Service Ticket using its own key, retrieves the session key, and decrypts the Authenticator to validate the timestamp.
    
- **Step 15**: If the Service Ticket and Authenticator are valid, the client is granted access to the service.
![[Kerberos authentication.png]]

### Steps
AS-REQ - 1.) The client requests an Authentication Ticket or Ticket Granting Ticket (TGT).

AS-REP - 2.) The Key Distribution Center verifies the client and sends back an encrypted TGT.

TGS-REQ - 3.) The client sends the encrypted TGT to the Ticket Granting Server (TGS) with the Service Principal Name (SPN) of the service the client wants to access.

TGS-REP - 4.) The Key Distribution Center (KDC) verifies the TGT of the user and that the user has access to the service, then sends a valid session key for the service to the client.

AP-REQ - 5.) The client requests the service and sends the valid session key to prove the user has access.

AP-REP - 6.) The service grants access

### Kerberos Tickets Overview

The main ticket you will receive is a ticket-granting ticket (TGT). These can come in various forms, such as a .kirbi for Rubeus and .ccache for Impacket. A ticket is typically base64 encoded and can be used for multiple attacks. 

The ticket-granting ticket is only used to get service tickets from the KDC. When requesting a TGT from the KDC, the user will authenticate with their credentials to the KDC and request a ticket. The server will validate the credentials, create a TGT and encrypt it using the krbtgt key. The encrypted TGT and a session key will be sent to the user.

When the user needs to request a service ticket, they will send the TGT and the session key to the KDC, along with the service principal name (SPN) of the service they wish to access. The KDC will validate the TGT and session key. If they are correct, the KDC will grant the user a service ticket, which can be used to authenticate to the corresponding service.



Attacking the kerberos protocol

-> ﻿Kerbrute is a popular enumeration tool used to brute-force and enumerate valid active-directory users by abusing the Kerberos pre-authentication.

```
kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt
```
```
kerbrute userenum users.txt -d spookysec.local --dc 10.10.74.37
```