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

### Wireshark - Display Filters

#### Display Filters

Wireshark provides **Display Filters** to reduce noise and focus on the traffic you need.

> 💡 Tip: **If you can click it, you can filter or copy it.**

---

#### Useful Right-Click Options

##### Apply as Filter
Filters packets based on a **single selected field**.

**Example:**
- `ip.src == 192.168.1.10`

---

##### Conversation Filter
Shows the **entire conversation** (both request and response) between two endpoints.

Useful for analyzing a complete communication session.

---

##### Colourise Conversation
Highlights all packets in the same conversation **without hiding other packets**.

---

##### Prepare as Filter
Creates a filter but **does not apply it immediately**. You can edit it before pressing **Enter**.

---

##### Apply as Column
Adds the selected field as a **new column** in the packet list, making it easier to compare values across packets.

---

##### Follow Stream
Reconstructs the full application-level conversation (TCP, HTTP, etc.).

Useful for viewing:
- HTTP requests/responses
- FTP commands
- Plaintext usernames & passwords (if not encrypted)

> Server traffic is **Blue**, client traffic is **Red**.

---

#### Common Display Filters

##### Filter by Protocol

```text
http
dns
tcp
udp
ftp
smtp
imap
arp
dhcp
```

##### Filter by Port

```text
tcp.port == 80
udp.port == 53
```

##### Filter by IP Address

```text
ip.addr == 192.168.1.2
```

##### Filter by Source/Destination

```text
ip.src == 192.168.1.2
ip.dst == 192.168.1.2
```

## 6-Tcpdump: The Basics

- **tcpdump** is a lightweight **command-line** packet capture tool.
- It uses the **libpcap** library to capture network traffic.
- Main uses:
  - Capture packets
  - Save traffic to `.pcap` files
  - Filter packets
  - Control packet output

#### Tcpdump vs Wireshark

| Tcpdump | Wireshark |
|---------|-----------|
| CLI | GUI |
| Lightweight & fast | Powerful packet analysis |
| Best for capturing traffic | Best for analyzing traffic |

> A common workflow is to **capture packets with tcpdump** and **analyze them later in Wireshark**.

`tcpdump` is a command-line packet analyzer used to capture and inspect network traffic. In real-world scenarios, you should specify the network interface, capture destination, packet count, and output format.

### Common Options

| Command                | Description                                               |
| ---------------------- | --------------------------------------------------------- |
| `tcpdump -i INTERFACE` | Captures packets on a specific network interface          |
| `tcpdump -i any`       | Captures packets on all available interfaces              |
| `tcpdump -w FILE`      | Writes captured packets to a file, usually a `.pcap` file |
| `tcpdump -r FILE`      | Reads and displays packets from a capture file            |
| `tcpdump -c COUNT`     | Stops after capturing a specific number of packets        |
| `tcpdump -n`           | Disables IP address-to-hostname resolution                |
| `tcpdump -nn`          | Disables both hostname and port/service name resolution   |
| `tcpdump -v`           | Displays more packet details                              |
| `tcpdump -vv` / `-vvv` | Increases the level of output verbosity                   |

To list the available network interfaces:

```bash
ip address show
```

Short version:

```bash
ip a s
```

### Examples

#### 1. Capture and display 50 packets

```bash
sudo tcpdump -i eth0 -c 50 -v
```

This command listens on the `eth0` interface, captures 50 packets, and displays additional packet details.

#### 2. Capture packets and save them to a file

```bash
sudo tcpdump -i wlo1 -w data.pcap
```

This command captures traffic on the `wlo1` Wi-Fi interface and saves it to `data.pcap`. The capture continues until it is stopped with `CTRL+C`.

The saved packets can be read later with:

```bash
tcpdump -r data.pcap
```

They can also be analyzed using tools such as Wireshark.

#### 3. Capture traffic on all interfaces without name resolution

```bash
sudo tcpdump -i any -nn
```

This command captures packets on all network interfaces and displays IP addresses and port numbers in numeric form without performing DNS or service-name lookups.

### 3- Packet Filtering

Running `tcpdump` without filters may produce too much output to analyze effectively. Filters allow you to capture only the traffic related to a specific host, port, protocol, source, or destination.

#### Common Filtering Expressions

| Filter                       | Description                                               |
| ---------------------------- | --------------------------------------------------------- |
| `host IP` or `host HOSTNAME` | Captures packets sent to or received from a specific host |
| `src host IP`                | Captures packets originating from a specific host         |
| `dst host IP`                | Captures packets sent to a specific host                  |
| `port PORT_NUMBER`           | Captures packets sent to or received from a specific port |
| `src port PORT_NUMBER`       | Captures packets originating from a specific port         |
| `dst port PORT_NUMBER`       | Captures packets sent to a specific destination port      |
| `tcp`                        | Captures TCP packets                                      |
| `udp`                        | Captures UDP packets                                      |
| `icmp`                       | Captures ICMP packets                                     |
| `ip`                         | Captures IPv4 packets                                     |
| `ip6`                        | Captures IPv6 packets                                     |
| `and`                        | Matches packets when both conditions are true             |
| `or`                         | Matches packets when either condition is true             |
| `not`                        | Excludes packets that match a condition                   |

### Practical Examples

#### 1. Capture SSH Traffic on All Interfaces

```bash
sudo tcpdump -i any tcp port 22 -nn
```

This command:

* Listens on all available network interfaces.
* Captures only TCP traffic on port `22`.
* Displays IP addresses and port numbers without name resolution.

#### 2. Capture DNS Traffic on a Wi-Fi Interface

```bash
sudo tcpdump -i wlo1 udp port 53 -n
```

This command:

* Listens on the `wlo1` Wi-Fi interface.
* Captures UDP-based DNS traffic on port `53`.
* Disables hostname resolution to improve speed and readability.

#### 3. Capture HTTPS Traffic for a Specific Host

```bash
sudo tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap
```

This command:

* Listens on the `eth0` interface.
* Captures traffic exchanged with `example.com`.
* Filters only TCP traffic using port `443`.
* Saves the captured packets to `https.pcap` for later analysis.

The saved capture can be read with:

```bash
tcpdump -r https.pcap -nn
```

### 4-Advanced filtering

Advanced filters allow `tcpdump` to select packets by length, header bytes, and TCP flags.

#### Packet Length

Use `greater LENGTH` or `less LENGTH` to capture packets above or below a specified size.

```bash
# Capture packets larger than 15,000 bytes
sudo tcpdump -nn -r traffic.pcap 'greater 15000'
```

#### Binary Operations

Header filters commonly use these bitwise operators:
* `&` (**AND**) returns `1` only when both bits are `1`.
* `|` (**OR**) returns `1` when at least one bit is `1`.
* `!` (**NOT**) changes `1` to `0` and `0` to `1`.

#### Filtering Header Bytes

The `pcap-filter` syntax for accessing protocol header bytes is:

```text
proto[expr:size]
```

* `proto`: Protocol name, such as `arp`, `ether`, `icmp`, `ip`, `ip6`, `tcp`, or `udp`.
* `expr`: Byte offset; `0` represents the first byte.
* `size`: Number of bytes to read: `1`, `2`, or `4`. It is optional and defaults to `1`.

Examples:

```bash
# Match Ethernet packets sent to a multicast address
sudo tcpdump 'ether[0] & 1 != 0'

# Match IPv4 packets containing IP options
sudo tcpdump 'ip[0] & 0xf != 5'
```

The first filter checks the least significant bit of the first Ethernet-header byte. The second checks whether the IPv4 header length differs from the standard five 32-bit words.

#### Filtering TCP Flags

Use `tcp[tcpflags]` to access the TCP flags field.

| Filter constant | Flag              |
| --------------- | ----------------- |
| `tcp-syn`       | SYN — Synchronize |
| `tcp-ack`       | ACK — Acknowledge |
| `tcp-fin`       | FIN — Finish      |
| `tcp-rst`       | RST — Reset       |
| `tcp-push`      | PSH — Push        |

Use `==` when the specified flag must be the **only** flag set:

```bash
# Capture packets with only the SYN flag set
sudo tcpdump 'tcp[tcpflags] == tcp-syn'

# Count packets with only the RST flag set
sudo tcpdump -r traffic.pcap 'tcp[tcpflags] == tcp-rst' | wc -l
```

Use bitwise AND when the specified flag may be set together with other flags:

```bash
# Capture packets where at least the SYN flag is set
sudo tcpdump 'tcp[tcpflags] & tcp-syn != 0'

# Capture packets where at least SYN or ACK is set
sudo tcpdump 'tcp[tcpflags] & (tcp-syn|tcp-ack) != 0'

# Capture packets where both SYN and ACK are set
sudo tcpdump \
  'tcp[tcpflags] & (tcp-syn|tcp-ack) == (tcp-syn|tcp-ack)'
```

Custom filters can be created by combining packet-length conditions, protocol-header offsets, comparison operators, and TCP flag masks.
