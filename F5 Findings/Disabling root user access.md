First create a user with the adminstrative privilage
![[Pasted image 20240917152924.png]]
Now then head to the Platform and click on the disable default admin and use alternate
	Here make sure to chose the alternate user
![[Pasted image 20240917152808.png]]

Now the root has been disable so the you can login with other admin credentials

Now there may be problem in navigating in the security tabs / ASM with error message such as 
	"# Error message on GUI: Error getting auth token from login provider"

So in the terminal restart the following services and boom now the solution is done.
		bigstart restart restjavad
		bigstart restart restnoded
![[Pasted image 20240917153339.png]]

