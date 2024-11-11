-sn -> ping and discover the hosts in the network
|   |   |
|---|---|
|`-O`|OS detection|
|`-sV`|Service and version detection|
|`-A`|OS detection, version detection, and other additions|
|`-Pn`|Scan hosts that appear to be down|

|                 |                                                               |
| --------------- | ------------------------------------------------------------- |
| `-sT`           | TCP connect scan – complete three-way handshake               |
| `-sS`           | TCP SYN – only first step of the three-way handshake          |
| `-sU`           | UDP scan                                                      |
| `-F`            | Fast mode – scans the 100 most common ports                   |
| `-p[range]`     | Specifies a range of port numbers – `-p-` scans all the ports |
|                 |                                                               |
| Timing          | Total Duration                                                |
| T0 (paranoid)   | 9.8 hours                                                     |
| T1 (sneaky)     | 27.53 minutes                                                 |
| T2 (polite)     | 40.56 seconds                                                 |
| T3 (normal)     | 0.15 seconds                                                  |
| T4 (aggressive) | 0.13 seconds                                                  |