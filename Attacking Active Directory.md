---
tags:
  - active-directory
  - enummeration
  - kerberos
  - priv-escalation
---
Install **impacket, bloodhound and ne04j**


### 1. **enum4linux**

- **Command**: `enum4linux <target_ip>`
- **Usage**: Enum4linux is specifically designed for enumerating Windows information over SMB and NetBIOS. It gathers extensive data, including shares, users, and groups.
- **Options**: You can use `enum4linux -a <target_ip>` to perform all enumeration techniques at once.
```
enum4linux <ip>
```
### **Kerbrute**
-> Install kerbrute
