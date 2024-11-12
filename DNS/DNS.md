**DNS** works on UDP mostly in the layer 7(Application layer)

Querying to the root server to obtain the TLD nameserver
```bash
dig @shikhar.mos.com.np samirdeshar.com.np NS
```
Now the root server responds with the TLD nameserver managing those domain.
![[DNS_Queryroot.png]]
Now the recursive dns maps the request to the obtain list of server that contains the records for the .com.np which are TLD (Top level Domain) servers
Moving forward
Now quering the TLD server to list get the record for samirdeshar.com.np 

![[DNS_TLD.png]]Here it provides the list of server that contains the zone files of the domain. i.e actuall record that maps ip to domain or can be said that resolves the DNS query
