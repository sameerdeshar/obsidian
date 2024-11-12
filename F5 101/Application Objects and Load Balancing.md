Load Balancing
Load Balancing is maintaining the server load to be distributed to various server such that it doesn't exhaust the server resource and maintain high availability. 

So in F5 the load balancing can be done via various method one is pool member
![[Pasted image 20240918114420.png]]
In this representation 
Member load balancing is made based upon the connection in the specific services or can be said as looking based upon the port 
Here the based upon the member load balancing in https pool new connection goes to B
and for sftp new connection can go to either A or C


## Node/Server Load Balancing
-> So in the Node load balancing all the service is combined and new connection goes to the least connection from altogether for a specific node/server.
In the above context new connection goes to the server C as it has leasst connection with combined of 35+5 = 40 which is the least among all other.


## Static Load Balancing
Round Robin and Ratio Based
Ratio based is assigning the server with compartively higher or lower connection than the other one.
For e.g. with the server A,B,C having
**10:5:5** ratio then, the server A recives 2 times more connection than B and C.


## Dynamic Load Balancing
-> Also knows as intelligent load balancing
-> Not just Round Robin checks different criteria to balance the load 
-> For instance Least connection load balancing is one of it's types.
Different types are:

- Fastest-> based upon fastest response time. Used when the server are at different networks.
- Weighted least connection -> Some weight that the server  has some capacity and connection established in the server. With the calculation of percentage the weight is calculated to load balance.
- Predictive -> Watches the server overtime and looks at performance,, resource and learns and makes prediction to make the load balance to the respective server.

## Priority Group Activation
Active and standby pool members for load balancing
So it is making given pool is active and in case of any failure other comes to be active that is standby to take over

![[Pasted image 20240918121020.png]]
So here the priority group is set by the value so with A and B having 20 20 these are running and incase of any failure among A or B then standby members C and D becomes active along with A and C and D.
The group is also defined as how many active member is required so here at least two member is made so when one of them is down the priority group triggers the C and D to be active.
![[Pasted image 20240918121538.png]]

So after B comes back online the connection will go back to just A and B.

## Fallback Hosts
When the nodes and pools stop responding or are down, then the request is redirected to a fall back hosts which simply shows that there is some issues and wait for a while message.
This doesn't provide services but just a redirection to make that the pools are not working to prevent error being poped up in the client side.
![[Pasted image 20240918122603.png]]
![[Pasted image 20240918122934.png]]
Now it is done.....
