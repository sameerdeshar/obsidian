## 1:1 mapping of MAC to IP
ARP table is created with the IP with associated MAC.
This is put in the cache by the BIG IP

## MAC Masquerading 
-> Maintaining floating MAC in BIG IP
This is used for HA(high availability )
	When once crashes others comes alive 
	![[Pasted image 20240920103223.png]]
	Point to be noted here is that when the A fails the floating mac it is used is transferred to B so that B takes over the place of A and there is seamless connection without interruption.

## Acquiring packet capture in BIG IP
TCP dump can be very useful for analyzing the packets

- Listing the interfaces
	- tcpdump -D
	- ifconfig -a
	-![[Pasted image 20240920105146.png]]
- Packet capture in the interface
		tcpdump -i eth0 
	For host specific and port specific
		tcpdump -i eth0 host 10.1.0.1
		tcpdump -i eth0 port 80

##  Saving the tcpdump packet
Capturing the packet and saving the output
![[Pasted image 20240920105910.png]]
	tcpdump -i eth0 port 80 -w http_traffic.pcap

Viewing the capture packet
![[Pasted image 20240920111602.png]]
	tcpdump -r http_traffic.pcap


## Front Pannel Lights
![[Pasted image 20240920112046.png]]

