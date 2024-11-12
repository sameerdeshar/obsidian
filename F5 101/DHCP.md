	Get a dynamic IP in the network 
	A device brodcast for asking the ip and dhcp provides a offer of an IP and the device request the IP and DHCP server acknowledges it .
	This process is also know as DORA (Discover, Offer, Requesst, Acknowledge)

## LAYER 2

Mac address is used for communication 
Mac address table with port associated in the switch is used (gb/2)

Layer 3 Communications
Router is associated with the layer 3 communication

Router learn routes 
Caches the routes in the routing table so the shortest path is taken
Counts the hop counts to reach the destination in shortest path

## VLAN(s)
It is a layer 2 segmentation.
Segregate or isolation in the network.

Each vlan is it's own subnet 
And each vlan has tagging so that it knows about which vlan is it on

### Untagged and Tagged
Tag-> The interface knows which vlan is it on.
	when the vlan is tagged it can be sent via a same interface and the frame is know by the vlan header.
Untagged-> Dedicated interface for a single Vlan

In case of CISCO 
	tag-> trunk  
	untagged-> access port
![[Pasted image 20240917115131.png]]

VLAN tagging ranges from 1-4094
 1 is for the default vlan and can't be used.


## VLAN double tagging (tag-in-tag)
	Have two vlan values in ethernet frame

![[Pasted image 20240917115435.png]]


## Firewall
->These are allow or deny
-> They are top-down setup

There are 3 main types of firewall:
1. Packet filtering
2. Stateful 
3. Application 

![[Pasted image 20240917122034.png]]
