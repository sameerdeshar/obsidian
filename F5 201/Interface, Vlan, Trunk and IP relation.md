### What is trunk??
Trunk is what combining multiple interfaces into one
![[Pasted image 20240925143953.png]]
-> Combining the these interface to act as one
	Here this require some protocol to understand these are done like that
	So **LACP (link aggregation control protocol)** is what makes it possible for interfaces to be combined.


In this which mac will be used of the interface??
So by default the big ip will use the lower number port's mac address as combined interface.


### How many ports can be combined to formed trunk?
this command shows how many ports can be combined in one trunk.
	guishell —c " select MAX_MBRS_PER_TRUNK from platform"


##  Create a Trunk in BIG ip
1. Create a trunk
2. Create a Vlan and attach the trunk as a interface
3. create a self ip .


## EGRESS Action
Where the data is going?
	tmsh show /net route
	
![[Pasted image 20240925153603.png]]

Shows where the next data goes
![[Pasted image 20240925155212.png]]



