https://tryhackme.com/room/furthernmap?vccr=3

# NMAP

## Basics

When we connect to port `443` on a server, our computer opens a temporary port with a random number, such as `43556`.

Nmap can scan ports `1` to `65535`.

Help:

```bash
nmap --help
```

```bash
man nmap
```

Scan all ports:

```bash
nmap -p- <target>
```

Scan port `80`:

```bash
nmap -p 80 <target>
```

`-T5`: Controls scan timing. A higher number is faster, but it may be less accurate or easier to detect.

`-A`: Performs an aggressive and resource-intensive scan.

`-oN`: Saves the output in normal format.

```bash
nmap -oN output.txt <target>
```

`-v`: Increases verbosity and shows more scan details.

## Most Useful Scan Types

`-sT`: TCP Connect Scan.

```bash
nmap -sT <target>
```

`-sS`: SYN or “Half-open” Scan. It is usually faster and requires `sudo`.

```bash
sudo nmap -sS <target>
```

`-sU`: UDP Scan. A result of `open|filtered` means that the port may be open, but a firewall may also be blocking the response.

```bash
sudo nmap -sU <target>
```

UDP scans are slow, so we can scan only the most common UDP ports:

```bash
sudo nmap -sU --top-ports 20 <target>
```

During TCP SYN scanning, there are usually three possible responses:

* `SYN/ACK`: The port is open.
* `RST`: The port is closed.
* No response: The port is probably filtered by a firewall.

The `-sS` scan is called half-open because it does not complete the full TCP connection.

`-sN`, `-sF`, and `-sX` send TCP packets with unusual or empty flags. They may bypass some old or stateless firewalls, but they are not reliable against modern firewalls.

`-sn`: Performs a ping sweep or host discovery scan.

```bash
nmap -sn 192.168.0.0/24
```

## Nmap Scripting Engine (NSE)

NSE scripts are written in the Lua programming language.

The following command runs all applicable scripts from the `safe` category:

```bash
nmap --script=safe <target>
```

Run specific SMB scripts:

```bash
nmap --script=smb-enum-users,smb-enum-shares <target>
```

Example:

```bash
nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php' <target>
```

Windows hosts may block ICMP packets by default. In this case, use `-Pn` to tell Nmap not to ping the host before scanning:

```bash
nmap -Pn <target>
```

Using `-Pn` may increase the scan time.

On a local network, Nmap can also use ARP requests to determine whether a host is active.

More details about firewall evasion:

https://nmap.org/book/man-bypass-firewalls-ids.html

`-f`: Fragments packets into smaller parts.

```bash
sudo nmap -f <target>
```

Use `-vv` when more details about the scan results are needed:

```bash
sudo nmap -sX -p 1-999 10.67.131.211 -vv
```
