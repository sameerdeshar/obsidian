## TCP And UDP
#### DNS uses UDP
#### HTTP and https uses TCP
![[Pasted image 20240912124033.png]]

**Class A **
Subnet of 255.0.0.0
Class B -> Subnet of 255.255.0.0
Class C -> Subnet of 255.255.255.0

Each IPv4 contains 32 bit with 8 bits separated by period (.) Also knows as Octate.
/24 represents the mask  -> also know as CIDR notation


If there is no DHCP present and the device is not configured with static IP and gateway and mask 
then device gets APIPA address(**Automatic Private IP Addressing**) which are basically 
169.254
-> With these there is no communication of the device with anybody.

**Unicast**
->Sending packet to specific address (IP address)(One destination)
**Multicast**
-> Sending packet to multiple IP address in a group 
This falls under type D network 
Which has the IP addressing ranging from 224.0.0.0 to 239.255.255.255
Use case in a game of 100 sending each individual 100 packet is not necessary by making a multicast to send one packet only.
**Broadcast**
Sending packets to all the devices in the network
Used in ARP normally to find the IP associated with the MAC
Router prevents the broadcast being sent outside the network if it is a broadcast.
**AnyCast**
->Multiple servers sharing the same IP address so the packet is sent to the nearest server 
Google DNS 8.8.8.8
Here the DNS request is sent as anycast so any server nearest can receive the packet and send back the response.

**Private Address**
These address are private and used in private environment
RFC 1918 based.
There are three types of network using private network
10.x.x.x  /8
172.16-31.x.x   /12
192.168.x.x /16

These are used in private network. The main problem is these are not routable thus NAT (Network Address Translation) is done in these to make these address routable in public internet.






