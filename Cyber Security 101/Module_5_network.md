## 2- Networking Essentials
Dynamic Host Configuration Protocol (DHCP) is an application-level protocol that relies on UDP ; the server listens on UDP port 67, and the client sends from UDP port 68. Your smartphone and laptop are configured to use by default DHCP.  
ARP  is considered layer 2 because it deals with MAC addresses  

`traceroute` : It uses ICMP to discover the route from your host to the target.  
` ping` command sends an ICMP Echo Request (ICMP Type 8) receiving end responds with an ICMP Echo Reply (ICMP Type 0)  
`ping 192.168.11.1 -c 4` stops after 4 packet  

`traceroute example.com`  

Network Address Translation (NAT) :  one public IP address to provide Internet access to many private IP addresses  

## 3- Networking Core Protocols
`nslookup` : look up the IP address of a domain  

**task 4:**
Retrieving a Web Page with Telnet

Connect to the target's HTTP service on port 80:

```bash
telnet <TARGET_IP> 80
```

Request the file by sending:

```http
GET /flag.html HTTP/1.1
Host: <TARGET_IP>

```

> **Important:** Press **Enter twice** after the `Host` header to send a blank line, which marks the end of the HTTP request.

### task 5
**FTP Basics**

- FTP is used for **file transfer** (default port: **21**).
- Common commands:
  - `USER` → username
  - `PASS` → password
  - `RETR` → download a file
  - `STOR` → upload a file
- Login with anonymous:
  ```bash
  ftp <TARGET_IP>
  ```
- Useful commands:
  ```bash
  ls
  type ascii
  get <file>
  quit
  ```
- FTP uses a **separate data connection** for directory listing and file transfers.

  

If successful, the server returns an HTTP response containing the contents of `flag.html`, including the hidden flag.


### task 6: SMTP Basics

- SMTP is used to **send emails** (default port: **25**).
- Common commands:
  - `HELO` / `EHLO` → Start session
  - `MAIL FROM` → Sender
  - `RCPT TO` → Recipient
  - `DATA` → Start email body
  - `.` → End email body
  - `QUIT` → Close connection

#### Using Telnet with SMTP

```bash
telnet <TARGET_IP> 25
```

```text
HELO client
MAIL FROM:<user@test.com>
RCPT TO:<admin@test.com>
DATA
Subject: Test

Hello from Telnet!
.
QUIT
```

> `DATA` starts the email body, and a single `.` on a new line ends the message.


### task7: POP3 Basics

- POP3 is used to **receive emails** (default port: **110**).
- Common commands:
  - `USER` → Username
  - `PASS` → Password
  - `STAT` → Mailbox status
  - `LIST` → List emails
  - `RETR <id>` → Read/download an email
  - `DELE <id>` → Delete an email
  - `QUIT` → Exit

#### Using Telnet

```bash
telnet <TARGET_IP> 110
```

```text
USER linda
PASS Pa$$123
LIST
RETR 4
QUIT
```

> POP3 is for **receiving** emails, while SMTP is for **sending** emails.



### task 8: IMAP Basics

- IMAP is used to **receive and sync emails** across multiple devices (default port: **143**).
- Unlike POP3, emails stay on the server and remain synchronized.
- Common commands:
  - `LOGIN` → Login
  - `SELECT inbox` → Open mailbox
  - `FETCH <id> body[]` → Read an email
  - `MOVE` → Move an email
  - `COPY` → Copy an email
  - `LOGOUT` → Exit

#### Using Telnet

```bash
telnet <TARGET_IP> 143
```

```text
A LOGIN <user> <password>
B SELECT inbox
C FETCH 4 body[]
```

## 4-Networking Secure Protocols
### TLS Basics

- TLS is the secure successor to **SSL**.
- Provides:
  - **Confidentiality** (encrypts data)
  - **Integrity** (prevents data modification)
- Secure protocols:
  - HTTP → **HTTPS**
  - SMTP → **SMTPS**
  - POP3 → **POP3S**
  - IMAP → **IMAPS**

### Certificates

- Servers use **digital certificates** to prove their identity.
- Certificates are signed by a **Certificate Authority (CA)**.
- **Let's Encrypt** provides free trusted certificates.
- **Self-signed certificates are not trusted** for verifying server identity.

### HTTPS Basics

- **HTTPS = HTTP + TLS** (default port: **443**)
- Connection flow:
  1. TCP Handshake
  2. TLS Handshake
  3. Encrypted HTTP communication
- Without the TLS key, Wireshark only shows **encrypted Application Data**.
- With the decryption key, HTTPS traffic can be decrypted and inspected.
- TLS secures HTTP without changing the HTTP or TCP protocols.
D LOGOUT

### SSH Basics

- **SSH** is the secure replacement for **Telnet** (default port: **22**).
- Provides:
  - Encrypted communication
  - Secure authentication (password, public key, 2FA)
  - Data integrity
  - SSH Tunneling
  - X11 Forwarding

### Connect

```bash
ssh <user>@<host>
```

> **OpenSSH** is the most common open-source implementation of SSH.

### SFTP Basics

- **SFTP (SSH File Transfer Protocol)** uses **SSH** for secure file transfer (default port: **22**).
- Common commands:
  - `get` → Download a file
  - `put` → Upload a file

```bash
sftp <user>@<host>
```

### SFTP vs FTPS

- **SFTP** → Uses **SSH** (Port **22**).
- **FTPS** → Uses **TLS/SSL** (Usually Port **990**) and requires a valid certificate.
- SFTP is generally easier to configure than FTPS.


## 5-Wireshark: The Basics
It only allows analysts to discover and investigate the packets in depth. It also doesn't modify packets; it reads them.   
wireshark has coloring rules : view > coloring rules  
<img width="94" height="37" alt="image" src="https://github.com/user-attachments/assets/e1fc87b0-f4e3-4616-a9ac-28c402373d16" />  start, stop , restart network sniffing  
File>merge : for merging pcap files  
Statistics --> Capture File Properties : for file details [or use left down icon in the window]  

**Severity 	Colour 	Info**
- Chat 	**Blue** 	Information on usual workflow.
- Note 	**Cyan** 	Notable events like application error codes.
- Warn 	**Yellow** 	Warnings like unusual error codes or problem statements.
- Error 	**Red** 	Problems like malformed packets.

Frequently encountered information groups are listed in the table below. You can refer to Wireshark's official documentation (opens in new tab) for more information on the expert information entries.
- Group 	Info 	Group 	Info
- Checksum 	Checksum errors 	Deprecated 	Deprecated protocol usage
- Comment 	Packet comment detection 	Malformed 	Malformed packet detection

You can use the "lower left bottom section" in the status bar or "Analyse --> Expert Information" menu to view all available information entries via a dialogue box. It will show the packet number, summary, group protocol and total occurrence.  

use `Go` menu to see specific packet by number  

### Packet filtering
"right-click menu" or "Analyse --> Apply as Filter" menu to filter the specific value  
"right-click menu" or "Analyse --> Conversation Filter" menu to filter conversations.  
**note**:conversation shows server and cliend packets but apply as filter just a specific packet  
"right-click menu" or "View --> Colourise Conversation" : lice conversation but dont remove other packets  
