-> check the status of the server, nodes, pool etc

Different types health monitor
- ICMP ping 
- TCP echo
- Service check monitor
	-http or https or dns or ssh 
- Window Management  Instrumentation(WMI)
	-it is a service running in window server which provides performance statistics. 
- Passive Monitoring


When using ICMP to check the host 
It only checks for the network and doesn't checks for service. Thus when the service in the port is down and also in that condition the ICMP monitor makes the server being up and working when application is not working.

So never trust icmp monitor for application level checking such as http, http  services running in the node.
