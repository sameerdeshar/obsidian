As usuall the our go to while scanning, nmap scanning is done to the machine
![[Pasted image 20240912214152.png]]

Now going through it various ports are opened in the machine what caught the attention is port 80 where where disallowed entry for robots.txt was shown
![[Pasted image 20240912214401.png]]

Now immeditely going to the website/robot.txt
![[Pasted image 20240912214526.png]]
A disallowed entry is shown following up to paste it in the browser and boom
RSA is provided
![[Pasted image 20240912214724.png]]


Now immediately doing the ssh to the server with the command 
![[Pasted image 20240912214840.png]]
Here the hello.txt contains the RSA key provided from the browser earlier

And VOLA we are in the machine 
Explore different directories to capture the flag if any.

Now the race to become the root starts
So i scp the linpeas.sh file to the server to see any vectors for privilege escalation
![[Pasted image 20240912215152.png]]

From it I found two major vector that could potentially escalate the privilege
![[Pasted image 20240912215322.png]]

With some google search I found gdb is a debbuger
and with I can potentially escalate the privilege
![[Pasted image 20240912215555.png]]
