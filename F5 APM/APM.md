---
tags:
  - apm
  - f5
  - networking
category:
  - f5
  - Networking
  - cloud
date: 2024-10-16T10:52:00
published: true
---
## What is F5 APM?
F5 APM keeps company apps and data safe by making sure only the right people, with secure devices, can get in—whether they’re in the office or working from home.
It does this by:
- **Single Sign-On (SSO)**: Users log in once and can access all their apps.
- **Multi-Factor Authentication (MFA)**: Adds an extra step (like a code from your phone) to make sure it's really you.
- **Secure Remote Access**: Lets people safely connect to company systems from anywhere.
Other features:
- **Custom Access Rules**: Decide who can access what based on their role or device.
- **Device Security Checks**: Ensures the device is safe before letting it in.
![[F5APM working.png]]

#### How does the APM work?
1. **First the authentication** :Verify password from  AD, OAuth, SAML, local database etc.
2. **Access** : what method to be used for access the resources--> vpn tunneling, ssl vpn , direct access so on.
3. **Webtops** : Landing page for the authorization. Contains the list of the apps and files and folders that the user is accessible to use based on their policy and access. **Webtops** provide a secure, browser-based interface for accessing a virtual desktop environment with specific apps and files users are authorized to use, without needing full desktop access.
4. **Access Profiles and Policies**:
	- **Access Profiles** are sets of rules that define how a user or group of users can access resources. For example, one profile might allow remote workers to use a VPN, while another profile allows internal users direct access.
	- **Policies** within these profiles define specific conditions (like time of access, IP range, device type) and what happens when those conditions are met (grant access, deny access, or require multi-factor authentication).
### How it Works Together:
- First, the user is authenticated.
- Then, the system decides how the user will access resources.
- Based on their role, they’re shown the Webtop, which lists their authorized apps and files.
- The **Access Profiles and Policies** ensure that each user only accesses what they’re allowed to, according to the rules set for their group or role.



![[Pasted image 20241016110741.png]]

