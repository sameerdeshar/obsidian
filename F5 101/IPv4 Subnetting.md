Subnet mask is the only used to identify network and host.

**CLASS A IP -> 1-126.x.x.x**

**CLASS B IP -> 128-191.x.x.x**

**CLASS A IP -> 192-223.x.x.x**

Why we care about the class A,B or C 
It is due to default mask different for different Classes
**CLASS A** has first octect as network
**CLASS B** has  1st and 2nd octect as network
**CLASS C** has 1st 2nd and third octect as network


**Binary** **Number**
**128  64  32  16  8  4  2  1** 
1        0    0   0  1   0   1   1

128 * 1 + 64 * 0 + 32 * 0 + 16 * 0 + 8 * 1 + 4 * 0 + 2 * 1 + 1 * 1 = 128 + 8 + 2 + 1 = 139
This is 8bit binary
1 byte is 8 bit 



### **NETWORK MASK**
![[Pasted image 20240916112222.png]]
Here in the above fig it is a /24 network of has mask of 255.255.255.0 
This means the last portion of 8bits is used for host and 24 bits are being used as network.

**So FOR /23 network mask**
There are 9 bits used for host meaning 23 = 32 - 9 **(000000000)**
To know how many exactly host can be configure 
![[Pasted image 20240916115119.png]]
 So what is the range in the third octet for network now?
 so we look in the above table 
 ![[Pasted image 20240916115314.png]]
so now the these rectangle box contains the network range in the /23
i.e 128 + 64 + 32 +16 +8 +4 +2 = 254 
Meaning the subnet mask will be 255.255.254.0

## **Determining the Subnet mask**
So we given the network of **27.0.1.64/26**
Then we have to create 5 subnets 

So we go on calculate the host bits we are stealing 
For 5 subnet       look here with respect to the hand with for each digit it contains 1 additional bit ( 2 , 4, 8, 16, 32, 64, 128 )

That would mean for 5 subnet it falls under 8 so that would be 3 bit addition

Now the subnet obtained is **27.0.1.64/29**

Now for the number of host in each subnet we look into the LSB as shown in below 
For this condition LSB is 8 for the new mask.

So the subnet formed would be 
**27.0.1.64/29**
**27.0.1.72/29**
**27.0.1.80/29**


BLOCK SIZE
	LSB
	![[Pasted image 20240916123249.png]]
	When stealing 4 bits for the subnet the LSB in this condition becomes 16 which is the least and becomes the block size
Now the subnet formed are started from 0 and add the LSB (16)
Here the subnet formed are 
- 10.0.0.0/12
- 10.16.0.0/12
- 10.32.0.0./12 ..................

**### Valid Host in Subnet**
So in the subnet of 32,  64, 96,  128.......
So here the 192.168.1.1 is the valid host and last host is 192.168.1.30 where .31 is for brodcast and .0 is the gateway

## **WildCard Masks**
It is inversion of subnet mask and is use in ACL(Access Control List ) for routers and firewalls.
Which bits in the network should be matched and which are to be ignored 
For example is there is subnet mask of **255.255.255.0**
The wildcard can look like **0.0.0.255**

Here , 0.0.0 means the 1st three should exactly match the octact to the network and the last octect is where the any number can be put as wildcard. 

**What for the subnet without the clean boundries?
Not 8,16 or 24 like /19**

For this calculate the subnet LSB(least significant bit ) -1 
/19
![[Pasted image 20240916150215.png]]
So here for /19 the LSB should be 32.
Now the wildcard mask should be 
**0.0.(32-1).255**
**i.e 0.0.31.255**


## **Non Octet Boundaries**
That does not align with the normal subnet i.e. 8, 16, 24
So if it is subnetting of /26 it is referred to it .

## **Variable Length Subnet Masking( VLSM)**
Different length mask in different subnet 
This is used to utilize the IP that is only necessary.
![[Pasted image 20240916153952.png]]

