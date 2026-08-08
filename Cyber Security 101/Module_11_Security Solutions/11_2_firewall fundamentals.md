# Firewall Basics

A **firewall** controls incoming and outgoing network traffic based on predefined rules. Firewall rules usually consider properties such as:

* **Source / Destination IP**
* **Port**
* **Protocol**
* **Direction** — Inbound or Outbound
* **Action** — Allow, Deny, or Forward

## Common Firewall Types

* **Stateless Firewall** — Filters packets independently based on predefined rules. Mainly operates at OSI Layers 3–4.
* **Stateful Firewall** — Tracks active connections using a state table and makes decisions based on connection history. Layers 3–4.
* **Proxy / Application Firewall** — Inspects application-level traffic and packet contents. Operates at Layer 7.
* **Next-Generation Firewall (NGFW)** — Provides deep packet inspection, IPS, heuristic analysis, threat intelligence integration, and SSL/TLS inspection. Can operate across Layers 3–7.

### Rule Actions

* `Allow` → Permit matching traffic
* `Deny` → Block matching traffic
* `Forward` → Redirect matching traffic to another destination

### Rule Direction

* `Inbound` → Traffic entering the system/network
* `Outbound` → Traffic leaving the system/network
* `Forward` → Traffic being routed to another network segment

---

# Windows Defender Firewall

**Windows Defender Firewall** is the built-in firewall available in Windows. It can control application access and incoming/outgoing traffic through predefined or custom rules.

Windows mainly uses different firewall profiles:

* **Private** → Trusted networks such as home networks
* **Public** → Untrusted networks such as public Wi-Fi

Advanced firewall settings allow the creation of custom **Inbound** and **Outbound** rules.

### Example: Block HTTP/HTTPS Outbound Traffic

A custom outbound rule can block web traffic using:

```text
Direction:    Outbound
Protocol:     TCP
Remote Ports: 80,443
Action:       Block the connection
```

Common ports:

```text
22  → SSH
25  → SMTP
80  → HTTP
443 → HTTPS
```

---

# Linux Firewalls

Linux provides firewall functionality mainly through the **Netfilter** framework inside the Linux kernel.

Netfilter provides:

* Packet filtering
* NAT
* Connection tracking

Several firewall tools use Netfilter:

| Tool        | Description                                             |
| ----------- | ------------------------------------------------------- |
| `iptables`  | Traditional and widely used Netfilter interface         |
| `nftables`  | Modern successor to iptables                            |
| `firewalld` | Firewall manager based on predefined network zones      |
| `ufw`       | Beginner-friendly interface for managing firewall rules |

## UFW Quick Reference

**UFW (Uncomplicated Firewall)** provides a simpler way to manage firewall rules.

Check status:

```bash
sudo ufw status
```

Enable firewall:

```bash
sudo ufw enable
```

Disable firewall:

```bash
sudo ufw disable
```

Allow outgoing traffic by default:

```bash
sudo ufw default allow outgoing
```

Block incoming SSH traffic:

```bash
sudo ufw deny 22/tcp
```

List rules with numbers:

```bash
sudo ufw status numbered
```

Delete a rule:

```bash
sudo ufw delete 2
```

### Quick Reminder

```text
allow     → Permit traffic
deny      → Block traffic

IN        → Incoming traffic
OUT       → Outgoing traffic

Netfilter → Linux kernel firewall framework
iptables  → Traditional rule manager
nftables  → Modern iptables replacement
firewalld → Zone-based firewall manager
ufw       → Simplified firewall interface
```
