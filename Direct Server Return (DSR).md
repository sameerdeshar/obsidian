---
category:
  - Networking
  - CCNA
  - f5
tags:
  - direct_server_return
published: false
date: 2024-09-30T14:17:00
excalidraw-plugin: parsed
excalidraw-open-md: true
---
In **Direct Server Return (DSR)**, the load balancer forwards client requests to the server, but the **server responds directly to the client** without routing the response back through the load balancer. This method is often used to improve performance and reduce the load on the load balancer by avoiding unnecessary forwarding of responses in a [[Half Proxy]] setup.
##### **Example**
1. **Client IP:** `192.168.1.10`
2. **Load Balancer VIP (Virtual IP):** `192.168.2.1`
3. **Server IP:** `192.168.3.5`
##### **Step-by-Step Breakdown:**
1. **Client sends a request to the Load Balancer:**
    - The client sends a request to the load balancer’s **Virtual IP** (VIP) at **192.168.2.1**.
    - **Client Request:**
        - Source IP: `192.168.1.10`
        - Destination IP: `192.168.2.1` (Load Balancer VIP)
2. **Load Balancer forwards the request to the Server:**
    - The load balancer receives the request but does not modify the **IP header** (it keeps the original source and destination IPs).
    - The load balancer forwards the packet to the server by altering the **Layer 2 (MAC address)** so the server receives the packet.
    - **Forwarded Request to the Server:**
        - Source IP: `192.168.1.10` (Client)
        - Destination IP: `192.168.2.1` (VIP)
        - [[#Server processes the request because it recognizes the VIP as one of its assigned IPs]].
3. **Server responds directly to the Client:**
    - Instead of sending the response back to the load balancer, the server responds directly to the client.
    - The server uses the **client’s IP** as the destination IP in the response.
    - **Server Response:**
        - Source IP: `192.168.3.5` (Server)
        - Destination IP: `192.168.1.10` (Client)

This means the **response bypasses the load balancer**, improving performance by reducing the load balancer's involvement in the return path.
### Server processes the request because it recognizes the VIP as one of its assigned IPs
In a **Direct Server Return (DSR)** setup, the **server recognizes the Virtual IP (VIP)** as one of its own IPs because the VIP is **configured on the server** as a **loopback** or **secondary IP address**. This configuration is crucial for DSR to function properly, allowing the server to respond directly to client requests while keeping the VIP intact.
1. **VIP Configuration on the Server**:
    - In DSR, the **Virtual IP (VIP)** (e.g., `192.168.2.1`) is usually assigned to the load balancer to receive incoming traffic from clients. However, the **same VIP is also configured on the server**, typically as a **loopback address** (a virtual network interface).
    - This setup allows the server to receive and process traffic sent to the VIP without needing to forward responses back through the load balancer.
2. **How the Server Uses the VIP**:
    - When the load balancer forwards the packet to the server, the **destination IP** in the packet remains the VIP (e.g., `192.168.2.1`).
    - Since the server has the VIP configured as a local loopback IP, it recognizes this as its own address and accepts the packet, even though the original request was made to the load balancer.
3. **Loopback Interface**:
    - The server is configured to respond from the VIP, but instead of routing traffic back through the load balancer, it responds directly to the client using its own **real IP address** (e.g., `192.168.3.5`).
    - The **VIP is not tied to a physical network interface** on the server. It’s typically assigned to a loopback interface (e.g., `lo:0`), allowing the server to handle traffic directed at the VIP.
### **Configuration Example on the Server (Linux)**:
In a DSR setup, a server might have the VIP (`192.168.2.1`) configured as a loopback interface:
`sudo ifconfig lo:0 192.168.2.1 netmask 255.255.255.255 up`
This ensures that when the load balancer forwards packets with `192.168.2.1` as the destination IP, the server recognizes it as its own IP and processes the request.
### **How the DSR Process Works**:
1. **Client Request:**
    - Client (`192.168.1.10`) sends a request to the VIP (`192.168.2.1`).
2. **Load Balancer Forwards Request:**
    - The load balancer forwards the request to the server (`192.168.3.5`), keeping the VIP as the destination IP.
3. **Server Recognizes VIP:**
    - The server, with the VIP (`192.168.2.1`) configured on its loopback interface, recognizes the packet as meant for itself and processes the request.
4. **Server Responds Directly:**
    - The server responds directly to the client using the client’s IP address (`192.168.1.10`), bypassing the load balancer.


%%
# Excalidraw Data
## Text Elements
%%
## Drawing
```compressed-json
N4KAkARALgngDgUwgLgAQQQDwMYEMA2AlgCYBOuA7hADTgQBuCpAzoQPYB2KqATLZMzYBXUtiRoIACyhQ4zZAHoFAc0JRJQgEYA6bGwC2CgF7N6hbEcK4OCtptbErHALRY8RMpWdx8Q1TdIEfARcZgRmBShcZQUebTiADho6IIR9BA4oZm4AbXAwUDAiiBJuCAAxAEYeAFEAGSEAaQAlTShiAC0ASQBrAHkAYQoARyFiADZkoshYRDKAM0CETyp+

YsxuHgB2AGZtLYBWNcgYbmcdhK3jiAoSdW4ABm0Hl8rryQRCZWlH59fr6zKYKPa7MKCkNg9BADNj4NikMoAYkqCBRKKmxU0uGwPWUEKEHGIMLhCIk4OszDguECmQxkHmhHw+AAyrBgRJBB46RAwRCoQB1O6STag8GQhCsmDs9Cc0rXfHfDjhbJoN75SBsKnYNSnVUva544RwLrEFWoHIAXWui1w6RN3A4QiZ10IhKwZVwD25+MJSuYZsdzvVPIQy

24lUOCQALJUdgdKuNrowWOwuGgjsHk6xOAA5ThiTZRqM7ACcWwjfGDhGYABFUlAw2hwUIENdNMJCTVgulMgGnfhrkI4MRcA3iOGtjxYwl41txlGHmrphAiBweg7+9c4TjG6h5gQwtc4GxXVlcuqwHlpkUHscbxerRer9eni9F3ewK/Xg/1Y/l3BAn9ERwlyP9ilYfQnVHBAAAVAOYYDuGbVtg3wUIoBhfR9DUMcYJPWk0GfG8/nfC8v0XX98gAXz

WQpilKCQhB4DpnAAQXGYZWNwHgowAITEGBmQACQADWcGoAH1uVmcR0EWUMVm5DY0C2BJxn2DNl11VBnCjA4EmuW5iHuNByKXYoPi+H5TJI8zIEBaVb2DXlxWJeEkTRVEkDbbFcR9IlYXcslyA4SlqQyKBuQZJlJWlHlYTlZyxQFIURSSvkJTZWT4q5eVhEVZVw2uTVsR1cN9WDQ0hxNM1LWtcg7XHNBAwHKs3WU9BcEqb0O2IP0+yDZcwl3HgHhL

KNxhLA4Sx4pMmGzNNUE04os1TPMOALNAdkqB4EkqGddpdWt613ZC216rs0gigbWuXIcRzHCcpwueMEh2csdi3V112azdULYHcmr3A8UP/fCz0Ip8L0/D8HgfO8iOIt87KR79rwtX8j3g4DarAgRCEgtCGzg5VEKbUgWy3dDMOwmRljw09zxfWy7zMyiiio8A/wgXA4DgVloO4OjoA+dIyiIb5IrWBhCAQCheN8qrCTc0l0EReYNc1jEIGwEQaSgL

oG30VkMpVjyvPRaXddIfXDbSBWcSVgKSTKclQqpfXtet22jfKRkWSyspZXHK29Yiu3jeShBBWM4U0ErYpvfDo2TfFWLsuDr2w8yCPmnyyR+qK/Idezg2jb6LUyr1JzE9LiPyk4KByltRltPMkubeTtIG8yZlCCMWTRtDzuc6NgAVLAoFYiXFpXBB5il4uk9HtIBdIKebbYCgPlwIGWuHn20hqQlWM37eQiBnmz+15hsAhJkRO4VT1MOaXb/v/AAE

1uAmgzi6MNgBghaZgIC2cM1ED5d30HnAkfVCoSH8trPEJA+4Dw3INSAyDnZBVQHRSAvFYSX0RAMEsJCSHlHKNyZoCBlBQVVhARENQaxMKYRQiAECl6l1TlCCuUBUw3WlgBBAZhhDMAAOKkBQf3WS+9i42nSNQt0kiODKGAcuDIuBNDBCBmdYM2AiBwCQhTUGxQOC2lkro5cwgoCrgscYjhxQ7AACsEDYCyMyMxcAACybBiAIGPpo7R3B9z4DCOAG

idBoogTQMATmVEgA
```
%%