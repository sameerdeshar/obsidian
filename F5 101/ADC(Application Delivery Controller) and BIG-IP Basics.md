## Proxies
	It is a go-between
Something that lies in between and goes through
Request goes through it and forwards the data to the server.


## ADC
Fancy way of saying Load Balancing 
	Content redirection to the respective server
	Server Health Monitoring 
	NAT to the server (Ip change for server)
	SSL offloading (Big ip itself encrypts and decrypts so the server load is reduced)
	IP traffic optimization
	WAF(Web Application Firewall) -> works in Layer 7
		checks for web protocol like http get http put etc to protect the application itself.

## Big Ip Architecture
![[Pasted image 20240917160823.png]]

## Default Settings and Management Access
Defaul IP address
Hardware appliance: 192.168.1.245
Virtual appliance: DHCP configured

Management access from : internal and external interface
External VLAN = none

## What is big-ip?
