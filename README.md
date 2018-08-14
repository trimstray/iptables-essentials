<h2 align="center">Iptables Essentials: Common Firewall Rules and Commands</h2>

<br>

<p align="center">
  <a href="https://github.com/trimstray/iptables-essentials/tree/master">
    <img src="https://img.shields.io/badge/Branch-master-green.svg?longCache=true"
        alt="Branch">
  </a>
  <a href="http://www.gnu.org/licenses/">
    <img src="https://img.shields.io/badge/License-GNU-blue.svg?longCache=true"
        alt="License">
  </a>
</p>

<div align="center">
  <sub>Created by
  <a href="https://twitter.com/trimstray">trimstray</a> and
  <a href="https://github.com/trimstray/iptables-essentials/graphs/contributors">
    contributors
  </a>
</div>

<br>

****

### Tools to help you configure Iptables

- **[Shorewall](http://shorewall.org/)**
- **[Firewalld](https://firewalld.org/)**
- **[FireHOL](https://github.com/firehol/firehol)**


### Iptables Rules

- [1. Saving Rules](#1-saving-rules)
- [2. List out all of the active iptables rules](#2-list-out-all-of-the-active-iptables-rules)
- [3. List out all of the active iptables rules with numeric lines](#3-list-out-all-of-the-active-iptables-rules-with-numeric-lines)
- [4. List Rules as Tables](#4-list-rules-as-tables)
- [5. List Rules as Tables for INPUT chain](#5-list-rules-as-tables-for-input-chain)
- [6. Show all of the rule specifications in the INPUT chain](#6-show-all-of-the-rule-specifications-in-the-input-chain)
- [7. Show Packet Counts and Aggregate Size](#7-show-packet-counts-and-aggregate-size)
- [8. Delete Rule by Chain and Number](#8-delete-rule-by-chain-and-number)
- [9. Delete Rule by Specification](#9-delete-rule-by-specification)
- [10. Flush All Rules, Delete All Chains, and Accept All](#10-flush-all-rules--delete-all-chains--and-accept-all)
- [11. Flush All Chains](#11-flush-all-chains)
- [12. Flush a Single Chain](#12-flush-a-single-chain)
- [13. Allow Loopback Connections](#13-allow-loopback-connections)
- [14. Allow Established and Related Incoming Connections](#14-allow-established-and-related-incoming-connections)
- [15. Allow Established Outgoing Connections](#15-allow-established-outgoing-connections)
- [16. Internal to External](#16-internal-to-external)
- [17. Drop Invalid Packets](#17-drop-invalid-packets)
- [18. Block an IP Address](#18-block-an-ip-address)
- [19. Block and IP Address and Reject](#19-block-and-ip-address-and-reject)
- [20. Block Connections to a Network Interface](#20-block-connections-to-a-network-interface)
- [21. Block Connections to a Network Interface](#21-block-connections-to-a-network-interface)
- [22. Allow All Incoming SSH](#22-allow-all-incoming-ssh)
- [23. Allow Incoming SSH from Specific IP address or subnet](#23-allow-incoming-ssh-from-specific-ip-address-or-subnet)
- [24. Allow Outgoing SSH](#24-allow-outgoing-ssh)
- [25. Allow Incoming Rsync from Specific IP Address or Subnet](#25-allow-incoming-rsync-from-specific-ip-address-or-subnet)
- [26. Allow All Incoming HTTP](#26-allow-all-incoming-http)
- [27. Allow All Incoming HTTPS](#27-allow-all-incoming-https)
- [28. Allow All Incoming HTTP and HTTPS](#28-allow-all-incoming-http-and-https)
- [29. Allow MySQL from Specific IP Address or Subnet](#29-allow-mysql-from-specific-ip-address-or-subnet)
- [30. Allow MySQL to Specific Network Interface](#30-allow-mysql-to-specific-network-interface)
- [31. PostgreSQL from Specific IP Address or Subnet](#31-postgresql-from-specific-ip-address-or-subnet)
- [32. Allow PostgreSQL to Specific Network Interface](#32-allow-postgresql-to-specific-network-interface)
- [33. Block Outgoing SMTP Mail](#33-block-outgoing-smtp-mail)
- [34. Allow All Incoming SMTP](#34-allow-all-incoming-smtp)
- [35. Allow All Incoming IMAP](#35-allow-all-incoming-imap)
- [36. Allow All Incoming IMAPS](#36-allow-all-incoming-imaps)
- [37. Allow All Incoming POP3](#37-allow-all-incoming-pop3)
- [38. Allow All Incoming POP3S](#38-allow-all-incoming-pop3s)

#### 1. Saving Rules

###### Debian Based

```bash
apt-get install iptables-persistent
```

If you update your firewall rules and want to save the changes, run this command:

```bash
netfilter-persistent save
```

###### RedHat Based

```bash
service iptables save
```

#### 2. List out all of the active iptables rules

```bash
iptables -S
```

#### 3. List out all of the active iptables rules with numeric lines

```bash
iptables -L --line-numbers
```

#### 4. List Rules as Tables

```bash
iptables -L
```

#### 5. List Rules as Tables for INPUT chain

```bash
iptables -L INPUT
```

#### 6. Show all of the rule specifications in the INPUT chain

```bash
iptables -S INPUT
```

#### 7. Show Packet Counts and Aggregate Size

```bash
iptables -L INPUT -v
```

#### 8. Delete Rule by Chain and Number

```bash
iptables -D INPUT 10
```

#### 9. Delete Rule by Specification

```bash
iptables -D INPUT -m conntrack --ctstate INVALID -j DROP
```

#### 10. Flush All Rules, Delete All Chains, and Accept All

```bash
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

iptables -t nat -F
iptables -t mangle -F
iptables -F
iptables -X
```

#### 11. Flush All Chains

```bash
iptables -F
```

#### 12. Flush a Single Chain

```bash
iptables -F INPUT
```

#### 13. Allow Loopback Connections

```bash
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT
```

#### 14. Allow Established and Related Incoming Connections

```bash
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

#### 15. Allow Established Outgoing Connections

```bash
iptables -A OUTPUT -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 16. Internal to External

```bash
iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```

#### 17. Drop Invalid Packets

```bash
iptables -A INPUT -m conntrack --ctstate INVALID -j DROP
```

#### 18. Block an IP Address

```bash
iptables -A INPUT -s 15.15.15.51 -j DROP
```

#### 19. Block and IP Address and Reject

```bash
iptables -A INPUT -s 15.15.15.51 -j REJECT
```

#### 20. Block Connections to a Network Interface

```bash
iptables -A INPUT -i eth0 -s 15.15.15.51 -j DROP
```

#### 21. Block Connections to a Network Interface

```bash
iptables -A INPUT -i eth0 -s 15.15.15.51 -j DROP
```

#### 22. Allow All Incoming SSH

```bash
iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 23. Allow Incoming SSH from Specific IP address or subnet

```bash
iptables -A INPUT -p tcp -s 15.15.15.0/24 --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 24. Allow Outgoing SSH

```bash
iptables -A OUTPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 25. Allow Incoming Rsync from Specific IP Address or Subnet

```bash
iptables -A INPUT -p tcp -s 15.15.15.0/24 --dport 873 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 873 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 26. Allow All Incoming HTTP

```bash
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 80 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 27. Allow All Incoming HTTPS

```bash
iptables -A INPUT -p tcp --dport 443 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 443 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 28. Allow All Incoming HTTP and HTTPS

```bash
iptables -A INPUT -p tcp -m multiport --dports 80,443 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp -m multiport --dports 80,443 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 29. Allow MySQL from Specific IP Address or Subnet

```bash
iptables -A INPUT -p tcp -s 15.15.15.0/24 --dport 3306 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 3306 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 30. Allow MySQL to Specific Network Interface

```bash
iptables -A INPUT -i eth1 -p tcp --dport 3306 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -o eth1 -p tcp --sport 3306 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 31. PostgreSQL from Specific IP Address or Subnet

```bash
iptables -A INPUT -p tcp -s 15.15.15.0/24 --dport 5432 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 5432 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 32. Allow PostgreSQL to Specific Network Interface

```bash
iptables -A INPUT -i eth1 -p tcp --dport 5432 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -o eth1 -p tcp --sport 5432 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 33. Block Outgoing SMTP Mail

```bash
iptables -A OUTPUT -p tcp --dport 25 -j REJECT
```

#### 34. Allow All Incoming SMTP

```bash
iptables -A INPUT -p tcp --dport 25 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 25 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 35. Allow All Incoming IMAP

```bash
iptables -A INPUT -p tcp --dport 143 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 143 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 36. Allow All Incoming IMAPS

```bash
iptables -A INPUT -p tcp --dport 993 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 993 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 37. Allow All Incoming POP3

```bash
iptables -A INPUT -p tcp --dport 110 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 110 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### 38. Allow All Incoming POP3S

```bash
iptables -A INPUT -p tcp --dport 995 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 995 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```
