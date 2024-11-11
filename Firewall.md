---
tags:
  - firewall
  - networking
  - intrusion-detection
  - idss
  - snort
---

### Types of Firewalls

1. **Stateless Firewall**  
   - **Layers**: 3 and 4 (Network, Transport)
   - **Purpose**: Filters traffic based on preset rules without tracking connections.
   - **Pros**: Fast processing.
   - **Cons**: Doesn't remember past traffic, so each packet is treated as new.

2. **Stateful Firewall**  
   - **Layers**: 3 and 4
   - **Purpose**: Tracks connections, allowing traffic based on past connections.
   - **Pros**: More secure, remembers past traffic patterns.
   - **Cons**: Slightly slower than stateless due to connection tracking.

3. **Proxy Firewall (Application-Level Gateway)**  
   - **Layer**: 7 (Application)
   - **Purpose**: Inspects packet content and forwards requests on behalf of users.
   - **Pros**: Anonymity, content filtering, can decrypt SSL/TLS traffic.
   - **Cons**: Slower; more complex configuration.

4. **Next-Generation Firewall (NGFW)**  
   - **Layers**: 3 to 7
   - **Purpose**: Advanced inspection with real-time threat detection.
   - **Pros**: Intrusion prevention, SSL/TLS decryption, anomaly detection.
   - **Cons**: Higher cost, more resources required.

---

### Comparison Table

| **Firewall Type**      | **Key Features**                                          |
|------------------------|-----------------------------------------------------------|
| **Stateless**          | Basic filtering, no connection tracking, high speed       |
| **Stateful**           | Tracks connections, allows complex rules, more secure     |
| **Proxy**              | Deep packet inspection, anonymity, SSL/TLS decryption     |
| **Next-Generation**    | Advanced threat detection, SSL/TLS inspection, heuristic analysis |


### Intrusion Detection System
Here's a simplified note on Intrusion Detection System (IDS) types:

---
IDS example -> snort
### IDS Categories

#### Deployment Modes
1. **Host Intrusion Detection System (HIDS)**  
   - **Installed on each host** to monitor only that host.
   - **Pros**: Detailed visibility on each device.
   - **Cons**: Hard to manage in large networks, resource-heavy.

2. **Network Intrusion Detection System (NIDS)**  
   - **Monitors entire network traffic** for suspicious activity.
   - **Pros**: Centralized view of network security.
   - **Cons**: Less detailed than HIDS on individual hosts.

---

#### Detection Modes
1. **Signature-Based IDS**  
   - Detects known threats using **attack signatures**.
   - **Pros**: Quick detection of known threats.
   - **Cons**: Cannot detect zero-day attacks (new, unknown threats).

2. **Anomaly-Based IDS**  
   - Learns normal behavior (baseline) and flags deviations.
   - **Pros**: Can detect zero-day attacks.
   - **Cons**: High chance of false positives; requires fine-tuning.

3. **Hybrid IDS**  
   - Combines **signature** and **anomaly** detection for broader coverage.
   - **Pros**: Detects both known and unknown threats.

---

| **IDS Type** | **Key Features** |
|--------------|-------------------|
| **HIDS**     | Host-based, detailed per-device |
| **NIDS**     | Network-based, central monitoring |
| **Signature**| Detects known threats, fast |
| **Anomaly**  | Detects unknown threats, prone to false positives |
| **Hybrid**   | Covers both known and unknown threats |