## 2- Networking Essentials
Dynamic Host Configuration Protocol (DHCP) is an application-level protocol that relies on UDP ; the server listens on UDP port 67, and the client sends from UDP port 68. Your smartphone and laptop are configured to use by default DHCP.  
ARP  is considered layer 2 because it deals with MAC addresses  

`traceroute` : It uses ICMP to discover the route from your host to the target.  
` ping` command sends an ICMP Echo Request (ICMP Type 8) receiving end responds with an ICMP Echo Reply (ICMP Type 0)  
`ping 192.168.11.1 -c 4` stops after 4 packet  

`traceroute example.com`  

Network Address Translation (NAT) :  one public IP address to provide Internet access to many private IP addresses  


