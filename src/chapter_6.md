# Chapter 8: **Python for Reconnaissance and Initial Access**

## **Objective:**

This lab is designed to introduce students to the use of Python for reconnaissance and initial access in cybersecurity. Students will learn how to perform port scanning, DNS exploration, and subdomain enumeration using Python scripts. These techniques are essential for gathering information about a target system or network during the initial stages of a penetration test.

## **Lab Overview:**

1. **Port Scanning**: Students will use Python and the Scapy library to perform a SYN scan on a target host to identify open ports.
2. **DNS Exploration**: Students will explore DNS records, perform reverse DNS lookups, and enumerate subdomains using Python and the `dnspython` library.

## **Lab Setup:**

- **Python 3.x** installed on the system.
- **socket** comes with Python
  - A built-in Python library that provides a low-level networking interface. In this chapter, it's used specifically for reverse DNS lookups to convert IP addresses to hostnames, complementing the DNS reconnaissance capabilities.
- **Scapy** library installed (`pip install scapy`).
  - A powerful Python library for packet manipulation and network scanning. It allows for low-level network operations like crafting custom TCP/IP packets, performing port scans, and network discovery. In this chapter, it's used for SYN scanning to identify open ports on target systems.
- **dnspython** library installed (`pip install dnspython`).
  - A comprehensive DNS toolkit for Python that enables DNS queries, zone transfers, and dynamic updates. In this chapter, it's used for DNS record exploration, reverse DNS lookups, and subdomain enumeration to gather information about target domains and their infrastructure.
- A text file named `subdomains.txt` containing a list of common subdomains.

## **Lab Exercises:**

---

## **Exercise 1: Port Scanning with Scapy**

**Objective:** Perform a SYN scan on a target host to identify open ports.

**Code Provided:**

```python
# port scan
from scapy.all import *

ports = [25, 80, 53, 443, 445, 8080, 8443]

def SynScan(host):
    ans, unans = sr(IP(dst=host)/TCP(dport=ports, flags="S"), timeout=2, verbose=0)
    print("Open ports at %s:" % host)
    for (s, r) in ans:
        if s.haslayer(TCP) and r.haslayer(TCP):
            if s[TCP].dport == r[TCP].sport:
                print(s[TCP].dport)

def DNSScan(host):
    ans, unans = sr(IP(dst=host)/UDP(dport=53)/DNS(rd=1, qd=DNSQR(qname="google.com")), timeout=2, verbose=0)
    if ans:
        print("DNS Server at %s" % host)

host = "8.8.8.8"

SynScan(host)
DNSScan(host)
```

**Tasks:**

1. **Run the Code**: Execute the provided code to perform a SYN scan on the target host `8.8.8.8`. Observe the open ports and the DNS server status.
2. **Modify the Code**: Change the `ports` list to include additional ports of interest. Run the code again and compare the results.
3. **Analyze the Output**: Explain the significance of the open ports and how they can be used in a penetration test.

```

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------
```

---

## **Exercise 2: DNS Exploration and Subdomain Enumeration**

**Objective:** Explore DNS records, perform reverse DNS lookups, and enumerate subdomains.

**Code Provided:**

```python
# DNS Exploration
import dns
import dns.resolver
import socket

def ReverseDNS(ip):
    try:
        result = socket.gethostbyaddr(ip)
        return [result[0]] + result[1]
    except socket.herror:
        return None

def DNSRequest(domain):
    ips = []
    try:
        result = dns.resolver.resolve(domain)
        if result:
            print(domain)
            for answer in result:
                print(answer)
                print("Domain Names: %s" % ReverseDNS(answer.to_text()))
    except (dns.resolver.NXDOMAIN, dns.exception.Timeout):
        return []
    return ips

def SubdomainSearch(domain, dictionary, nums):
    successes = []
    for word in dictionary:
        subdomain = word + "." + domain
        DNSRequest(subdomain)
        if nums:
            for i in range(0, 10):
                s = word + str(i) + "." + domain
                DNSRequest(s)

domain = "google.com"
d = "subdomains.txt"
dictionary = []
with open(d, "r") as f:
    dictionary = f.read().splitlines()
SubdomainSearch(domain, dictionary, True)
```

**Tasks:**

1. **Run the Code**: Execute the provided code to enumerate subdomains of `google.com`. Observe the output and note any interesting findings.
2. **Modify the Code**: Change the `domain` variable to a different target domain (e.g., `example.com`). Run the code again and compare the results.
3. **Analyze the Output**: Discuss the importance of subdomain enumeration in reconnaissance and how it can lead to discovering potential attack vectors.

```

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------

--------------------------------------------------------------------
```

---

### **Additional Resources:**

- **Scapy Documentation**: https://scapy.readthedocs.io/
- **dnspython Documentation**: https://dnspython.readthedocs.io/
- **Common Subdomains List**: https://github.com/danielmiessler/SecLists/blob/master/Discovery/DNS/subdomains-top1million-5000.txt
