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
D LOGOUT
```
