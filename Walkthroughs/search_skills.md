# 🔍 TryHackMe — Search Skills

## Introduction

This room focuses on effective searching across the internet, cybersecurity platforms, and technical documentation.

In cybersecurity, knowing **what to search for** is not enough. You also need to know **where to search** and **how to find reliable information quickly**.

---

## 1. Shodan

**Shodan** is a search engine for internet-connected devices and publicly exposed services.

It can be used to discover:

* Web servers
* Network devices
* Internet-connected cameras
* Industrial control systems
* Open ports and services
* Software versions exposed in service banners

### Useful Filters

| Filter     | Purpose                       | Example                |
| ---------- | ----------------------------- | ---------------------- |
| `country`  | Limit results to a country    | `country:IE`           |
| `port`     | Search by open port           | `port:22`              |
| `org`      | Search within an organization | `org:"Amazon"`         |
| `hostname` | Search by hostname or domain  | `hostname:example.com` |

### Example Search

```text
apache 2.4.1
```

This query searches for systems that identify themselves as running the specified Apache version.

Website: https://www.shodan.io/

---

## 2. VirusTotal

**VirusTotal** analyzes files, URLs, domains, IP addresses, and file hashes using multiple security engines.

### Supported Indicators

* Files
* URLs
* Domains
* IP addresses
* File hashes

### Common Uses

* Checking suspicious files
* Analyzing unknown links
* Reviewing antivirus detections
* Investigating domains and IP addresses
* Gathering threat intelligence

> A positive or negative VirusTotal result is not definitive. It should be combined with additional analysis.

Website: https://www.virustotal.com/

---

## 3. CVE and Vulnerability Databases

**CVE** stands for Common Vulnerabilities and Exposures.

It provides a standardized naming system for publicly known security vulnerabilities.

### CVE Format

```text
CVE-YEAR-NUMBER
```

Example:

```text
CVE-2025-55182
```

A CVE identifier allows vendors, researchers, security tools, and organizations to refer to the same vulnerability consistently.

### CVSS

**CVSS**, or Common Vulnerability Scoring System, is used to estimate the severity of a vulnerability.

Important scoring factors include:

* Attack complexity
* Required privileges
* User interaction
* Impact on confidentiality
* Impact on integrity
* Impact on availability

Organizations often use CVSS scores to prioritize patching and remediation.

### Useful Resources

* CVE: https://www.cve.org/
* NVD: https://nvd.nist.gov/
* Exploit Database: https://www.exploit-db.com/

---

## 4. Official Documentation

Official documentation should usually be the first place to look when learning a tool or troubleshooting an error.

Official documentation is generally:

* More accurate
* More up to date
* Version-specific
* Supported by practical examples
* More complete than third-party tutorials

> Check official documentation before relying on blogs, forum posts, or unofficial guides.

---

## 5. Linux Man Pages

Linux manual pages provide built-in documentation for commands and tools.

### Open a Manual Page

```bash
man <command>
```

Example:

```bash
man nc
```

### Search Inside a Man Page

```text
/search-term
```

Press `n` to move to the next result.

Press `q` to exit.

### Netcat Example

Connect to `host.example.com` on port `42`:

```bash
nc host.example.com 42
```

### Common Man Page Sections

* `NAME`: Command name and short description
* `SYNOPSIS`: Command syntax
* `DESCRIPTION`: Detailed explanation
* `OPTIONS`: Available flags and arguments
* `EXAMPLES`: Usage examples
* `SEE ALSO`: Related commands and documentation

Online Linux manual pages:

https://man7.org/linux/man-pages/

---

## 6. GitHub for Security Research

GitHub is a valuable source for technical research related to vulnerabilities and cybersecurity tools.

Security researchers may publish:

* Proof-of-concept code
* Vulnerability scanners
* Detection scripts
* Technical write-ups
* Malware analysis tools
* Detection rules
* Lab exploitation tools

### Example Search

```text
CVE-2026-1337
```

Searching for a CVE identifier may reveal proof-of-concept repositories, scanners, technical analysis, or detection methods.

### Security Precautions

Never execute unknown proof-of-concept code without reviewing it first.

Before running a repository:

1. Read the source code.
2. Check the author and repository history.
3. Review stars, forks, and contributors.
4. Read open issues and pull requests.
5. Scan downloaded files.
6. Use an isolated lab environment.
7. Avoid running unknown code as `root`.

Some repositories may pretend to contain a legitimate exploit while actually distributing malware.

Website: https://github.com/

---

## Additional Useful Resources

| Resource                    | Purpose                                         |
| --------------------------- | ----------------------------------------------- |
| https://www.google.com/     | General research and advanced search operators  |
| https://www.shodan.io/      | Internet-connected devices and exposed services |
| https://www.virustotal.com/ | File, URL, domain, IP, and hash analysis        |
| https://www.cve.org/        | Official CVE identifiers                        |
| https://nvd.nist.gov/       | CVE details and CVSS scores                     |
| https://www.exploit-db.com/ | Public exploits and proof-of-concept code       |
| https://github.com/         | Security tools, code, and research              |
| https://man7.org/           | Linux command documentation                     |
| https://attack.mitre.org/   | Adversary tactics and techniques                |
| https://urlscan.io/         | Website and network-request analysis            |
| https://crt.sh/             | Certificate Transparency searches               |
| https://who.is/             | WHOIS and domain-registration information       |

---

## Key Takeaways

* Use Shodan to search for exposed internet services.
* Use VirusTotal to inspect suspicious files, URLs, and indicators.
* Search CVE identifiers when researching vulnerabilities.
* Use CVSS to understand vulnerability severity.
* Prefer official documentation over unofficial sources.
* Use Linux man pages for command-line help.
* Review GitHub proof-of-concept code before running it.
* Execute unknown security tools only in isolated lab environments.

---

## Room Information

* **Platform:** TryHackMe
* **Room:** Search Skills
* **Difficulty:** Easy
* **Estimated Time:** 15 minutes
* **Room Link:** https://tryhackme.com/room/searchskillscS

> This write-up is intended for legal, ethical, and educational cybersecurity activities only.
