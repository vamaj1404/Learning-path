https://tryhackme.com/room/furthernmap?vccr=3

# NMAP
## Basics
ports: when we connect to port 443 in server . our computer maybe open a port with random number like 43556  
total port: 65535  
help: nmap -map or man nmap  
-p- : scan all ports  
-p 80 : port 80 scan  
-T5 : timing- more is faster  
-A : very deep and resource using scan. aggressive scan  
-oN : see output in normalmode  
-v : increase verbosity to better understanding  
### most useful:
-sT :TCP Connect Scans (-sT)  
-sS :SYN "Half-open" Scans (-sS) - faster and hider need sudo     
-sU :UDP Scans (-sU) - open|filtered - it suspects that the port is open, but it could be firewalled  
	nmap -sU --top-ports 20 <target> : becasue udp scan is soo slow   

by TCP port scanning three answers are :  
syn/ack - RST - nothing  
it means : open - close/firewall - firewall  
-sS is half open because shows closed and firewall but not open ports completely  

-sN / -sF / -sX send packets with other or null flag . so can bypass firewalls in modern systems  
-sn : ping sweep : for ip range : nmap -sn 192.168.0.0/24  


### Nmap Scripting Engine (NSE)
Lua programming language  
If the command --script=safe is run, then any applicable safe scripts will be run against the target  
--script=smb-enum-users,smb-enum-shares  
example: nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'  

Your typical Windows host will, with its default , block all ICMP packets. so :   
-Pn: which tells Nmap to not bother pinging the host before scanning it. BUT WITH MORE TIME TO SCAN  
in local net: Nmap can also use ARP requests to determine host activity.  
more details for firewall evation: https://nmap.org/book/man-bypass-firewalls-ids.html  
-f:- Used to fragment the packets  


when we need more details about scan result we can use -vv for more details:  
nmap -sX -p 1-999 10.67.131.211 -vv  





