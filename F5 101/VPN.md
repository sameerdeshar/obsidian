

![[Pasted image 20240920171148.png]]
TYpes of vpn:
1. Site-site VPN
3. Client-site VPN

## HA in global scale in F5
Load balancing to the server around the globe.
Meaning the server is in various data centers and big IP load balances it
![[Pasted image 20240921031830.png]]



For the having multiple F5 then 
use DSC (Device Service CLuster)
	->this is used for maintaining multiple big ip device providing various services

#### Methods for HA in F5
1. Active/Standby Pair
2. Device Service Cluster(DSC)




### Ip address for FailOver
Local Static Ip  For Vlan HA
Local Mgmt IP 
Floating IP

### SNMP (Simple Network Management Protocol)
SNMP is used to gather information from network devices, such as:

1. CPU usage
2. Memory usage
3. Temperatures
4. Fan speed

It allows network administrators to query and monitor these devices effectively.

### SNMP Trap
An SNMP Trap is a mechanism where devices automatically send alerts to the SNMP manager when they reach certain thresholds or encounter specific issues. This proactive notification allows for immediate action to be taken without waiting for a query from the administrator.


