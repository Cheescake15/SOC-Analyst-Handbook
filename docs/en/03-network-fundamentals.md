# 03 — Network Fundamentals

[← Back to the English contents](README.md) | [Magyar változat](../hu/03-network-fundamentals.md)

## Introduction

This chapter summarises the network concepts that may be useful for a beginner SOC analyst.

In addition to international protocol specifications, the chapter also uses Hungarian educational material. A Hungarian National Cyber Security Center publication titled *Informatikai behatolások és felismerésük* discusses network models, protocols, and the recognition of intrusion-related activity.

The aim is not to cover networking in full detail. The focus is on understanding how IP addresses, ports, protocols, and network logs appear during a security investigation.

## 1. The OSI Model

| Layer | Name | Example |
|---:|---|---|
| 7 | Application | HTTP, DNS, SMTP |
| 6 | Presentation | encoding, encryption |
| 5 | Session | session management |
| 4 | Transport | TCP, UDP |
| 3 | Network | IPv4, IPv6, ICMP |
| 2 | Data Link | Ethernet, MAC address |
| 1 | Physical | cable, radio signal |

The model can help organise the investigation of a network problem.

## 2. The TCP/IP Model

| Layer | Examples |
|---|---|
| Application | HTTP, DNS, SMTP, SSH |
| Transport | TCP, UDP |
| Internet | IPv4, IPv6, ICMP |
| Network Access | Ethernet, Wi-Fi, ARP |

## 3. IP Addresses

IPv4 example:

```text
192.168.1.25
```

Common private ranges:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

IPv6 example:

```text
2001:db8:85a3::8a2e:370:7334
```

A SOC may need visibility into both IPv4 and IPv6 traffic.

## 4. Subnets

CIDR notation shows how much of an address identifies the network.

```text
192.168.1.0/24
```

This can help determine whether addresses belong to the same network.

## 5. MAC Addresses and ARP

ARP connects IPv4 addresses with MAC addresses on a local network.

Possible signs of ARP spoofing include:

- an unexpected MAC address for an existing IP
- several IP addresses linked to one MAC
- gateway changes
- connection problems

## 6. TCP and UDP

TCP uses a three-way handshake:

```text
Client → Server: SYN
Server → Client: SYN-ACK
Client → Server: ACK
```

UDP does not use this handshake and does not guarantee delivery.

Common UDP uses include DNS, DHCP, streaming, and some VPN solutions.

## 7. Ports

| Port | Service |
|---:|---|
| 22 | SSH |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 123 | NTP |
| 389 | LDAP |
| 443 | HTTPS |
| 445 | SMB |
| 3389 | RDP |

A port number alone does not prove which application is using the connection.

## 8. DNS

Common records include:

- A
- AAAA
- CNAME
- MX
- NS
- TXT
- PTR

Potentially suspicious patterns include:

- very long domain names
- random-looking subdomains
- many failed queries
- known malicious domains
- unusual TXT query volume

These patterns require context and do not prove malicious activity by themselves.

Hungarian National Cyber Security Center articles on DNS security also describe how the original DNS design creates security and privacy challenges. Technologies such as DNSSEC and encrypted DNS attempt to address different parts of these problems.

## 9. DHCP

DHCP may assign:

- IP address
- subnet mask
- default gateway
- DNS server

The DORA process is:

```text
Discover
Offer
Request
Acknowledge
```

## 10. ICMP

ICMP is used for network status and error messages.

The `ping` command commonly uses ICMP Echo Request and Echo Reply.

## 11. HTTP and HTTPS

Common HTTP methods include GET, POST, PUT, and DELETE.

Common status codes include:

- 200
- 301
- 400
- 401
- 403
- 404
- 500

HTTPS encrypts the content of HTTP communication, but some metadata may remain visible.

## 12. NAT

NAT translates between internal and public addresses.

During an investigation, analysts may need:

- NAT logs
- firewall logs
- source ports
- exact timestamps
- DHCP records

## 13. Simple SOC Example

A workstation connects to the same external IP address over port 443 every five minutes.

This may be legitimate software activity, but it may also require investigation.

The analyst may review:

1. the process creating the connection
2. the related domain
3. whether the destination is expected
4. whether other endpoints show the same pattern
5. the amount of traffic
6. related alerts

Regular repeated communication may be described as beaconing.


## Chapter Summary

Useful beginner-level topics include:

- IP addresses
- TCP and UDP
- ports
- DNS
- DHCP
- ARP
- ICMP
- HTTP and HTTPS
- NAT

The aim is to recognise unusual activity and identify which additional data may be needed.


## References

1. IETF RFC 9293: Transmission Control Protocol  
   https://datatracker.ietf.org/doc/html/rfc9293

2. IETF RFC 8200: Internet Protocol, Version 6 Specification  
   https://datatracker.ietf.org/doc/html/rfc8200

3. IETF RFC 1034: Domain Names, Concepts and Facilities  
   https://datatracker.ietf.org/doc/html/rfc1034

4. IETF RFC 1035: Domain Names, Implementation and Specification  
   https://datatracker.ietf.org/doc/html/rfc1035

5. IETF RFC 9110: HTTP Semantics  
   https://datatracker.ietf.org/doc/html/rfc9110

6. MITRE ATT&CK: Network Traffic  
   https://attack.mitre.org/datasources/DS0029/

7. Hungarian National Cyber Security Center  
   **Informatikai behatolások és felismerésük** [Hungarian]  
   https://nki.gov.hu/wp-content/uploads/2019/07/04-Informatikai-behatol%C3%A1sok-%C3%A9s-felismer%C3%A9s%C3%BCk.pdf

8. Hungarian National Cyber Security Center  
   **DNS biztonsági és adatvédelmi technológiák előnyei és hátrányai** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/tanacsok/dns-biztonsagi-es-adatvedelmi-technologiak-elonyei-es-hatranyai/

9. Hungarian National Cyber Security Center  
   **Egyes népszerű DNS biztonsági és adatvédelmi technológiák főbb jellemzőinek összehasonlítása** [Hungarian]  
   https://nki.gov.hu/it-biztonsag/tudastar/egyes-nepszeru-dns-biztonsagi-es-adatvedelmi-technologiak-fobb-jellemzoinek-osszehasonlitasa/

10. Gyaraki Réka, editor  
    **Az információbiztonság alapjai** [Hungarian]  
    National University of Public Service, 2023  
    https://rtk.uni-nke.hu/document/rtk-uni-nke-hu/az_informaciobiztonsag_alapjai_konyv_kesz_2.pdf
