1. **Create OU and then User**
![[Active_directory_OU.png]]

Now Create a User on the OU ->right click-> new -> users
![[AD_USERS.png]]

Fin the OU and DC of the 
```
dsquery user -name user1
```
![[Query_User.png]]

Now integrate the AD in F5
![[F5_AD_integrate.png]]
Test the integration via terminal
Login to the f5 terminall shell 
