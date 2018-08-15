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

## Table Of Content

- [Tools to help you configure Iptables](#tools-to-help-you-configure-iptables)
- [Iptables Rules](#iptables-rules)
  * [Saving Rules](#saving-rules)
  * [List out all of the active iptables rules with verbose](#list-out-all-of-the-active-iptables-rules-with-verbose)
  * [List out all of the active iptables rules with numeric lines and verbose](#list-out-all-of-the-active-iptables-rules-with-numeric-lines-and-verbose)
  * [Print out all of the active iptables rules](#print-out-all-of-the-active-iptables-rules)
  * [List Rules as Tables for INPUT chain](#list-rules-as-tables-for-input-chain)
  * [Print all of the rule specifications in the INPUT chain](#print-all-of-the-rule-specifications-in-the-input-chain)
  * [Show Packet Counts and Aggregate Size](#show-packet-counts-and-aggregate-size)
  * [To display INPUT or OUTPUT chain rules with numeric lines and verbose](#to-display-input-or-output-chain-rules-with-numeric-lines-and-verbose)
  * [Delete Rule by Chain and Number](#delete-rule-by-chain-and-number)
  * [Delete Rule by Specification](#delete-rule-by-specification)
  * [Flush All Rules, Delete All Chains, and Accept All](#flush-all-rules--delete-all-chains--and-accept-all)
  * [Flush All Chains](#flush-all-chains)
  * [Flush a Single Chain](#flush-a-single-chain)
  * [Insert Firewall Rules](#insert-firewall-rules)
  * [Allow Loopback Connections](#allow-loopback-connections)
  * [Allow Established and Related Incoming Connections](#allow-established-and-related-incoming-connections)
  * [Allow Established Outgoing Connections](#allow-established-outgoing-connections)
  * [Internal to External](#internal-to-external)
  * [Drop Invalid Packets](#drop-invalid-packets)
  * [Block an IP Address](#block-an-ip-address)
  * [Block and IP Address and Reject](#block-and-ip-address-and-reject)
  * [Block Connections to a Network Interface](#block-connections-to-a-network-interface)
  * [Block Connections to a Network Interface](#block-connections-to-a-network-interface-1)
  * [Allow All Incoming SSH](#allow-all-incoming-ssh)
  * [Allow Incoming SSH from Specific IP address or subnet](#allow-incoming-ssh-from-specific-ip-address-or-subnet)
  * [Allow Outgoing SSH](#allow-outgoing-ssh)
  * [Allow Incoming Rsync from Specific IP Address or Subnet](#allow-incoming-rsync-from-specific-ip-address-or-subnet)
  * [Allow All Incoming HTTP](#allow-all-incoming-http)
  * [Allow All Incoming HTTPS](#allow-all-incoming-https)
  * [Allow All Incoming HTTP and HTTPS](#allow-all-incoming-http-and-https)
  * [Allow MySQL from Specific IP Address or Subnet](#allow-mysql-from-specific-ip-address-or-subnet)
  * [Allow MySQL to Specific Network Interface](#allow-mysql-to-specific-network-interface)
  * [PostgreSQL from Specific IP Address or Subnet](#postgresql-from-specific-ip-address-or-subnet)
  * [Allow PostgreSQL to Specific Network Interface](#allow-postgresql-to-specific-network-interface)
  * [Block Outgoing SMTP Mail](#block-outgoing-smtp-mail)
  * [Allow All Incoming SMTP](#allow-all-incoming-smtp)
  * [Allow All Incoming IMAP](#allow-all-incoming-imap)
  * [Allow All Incoming IMAPS](#allow-all-incoming-imaps)
  * [Allow All Incoming POP3](#allow-all-incoming-pop3)
  * [Allow All Incoming POP3S](#allow-all-incoming-pop3s)
  * [Drop Private Network Address On Public Interface](#drop-private-network-address-on-public-interface)
  * [Only Block Incoming Traffic](#only-block-incoming-traffic)
  * [Drop All Outgoing to Facebook Networks](#drop-all-outgoing-to-facebook-networks)


****

### Tools to help you configure Iptables

- **[Shorewall](http://shorewall.org/)**
- **[Firewalld](https://firewalld.org/)**
- **[FireHOL](https://github.com/firehol/firehol)**
- **[UFW](https://wiki.ubuntu.com/UncomplicatedFirewall)**

### Iptables Rules

#### Saving Rules

###### Debian Based

```bash
netfilter-persistent save
```

###### RedHat Based

```bash
service iptables save
```

#### List out all of the active iptables rules with verbose

```bash
iptables -n -L -v
```

#### List out all of the active iptables rules with numeric lines and verbose

```bash
iptables -n -L -v --line-numbers
```

#### Print out all of the active iptables rules

```bash
iptables -S
```

#### List Rules as Tables for INPUT chain

```bash
iptables -L INPUT
```

#### Print all of the rule specifications in the INPUT chain

```bash
iptables -S INPUT
```

#### Show Packet Counts and Aggregate Size

```bash
iptables -L INPUT -v
```

#### To display INPUT or OUTPUT chain rules with numeric lines and verbose

```bash
iptables -L INPUT -n -v
iptables -L OUTPUT -n -v --line-numbers
```

#### Delete Rule by Chain and Number

```bash
iptables -D INPUT 10
```

#### Delete Rule by Specification

```bash
iptables -D INPUT -m conntrack --ctstate INVALID -j DROP
```

#### Flush All Rules, Delete All Chains, and Accept All

```bash
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

iptables -t nat -F
iptables -t mangle -F
iptables -F
iptables -X
```

#### Flush All Chains

```bash
iptables -F
```

#### Flush a Single Chain

```bash
iptables -F INPUT
```

#### Insert Firewall Rules

```bash
iptables -I INPUT 2 -s 202.54.1.2 -j DROP
```

#### Allow Loopback Connections

```bash
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT
```

#### Allow Established and Related Incoming Connections

```bash
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

#### Allow Established Outgoing Connections

```bash
iptables -A OUTPUT -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Internal to External

```bash
iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```

#### Drop Invalid Packets

```bash
iptables -A INPUT -m conntrack --ctstate INVALID -j DROP
```

#### Block an IP Address

```bash
iptables -A INPUT -s 15.15.15.51 -j DROP
```

#### Block and IP Address and Reject

```bash
iptables -A INPUT -s 15.15.15.51 -j REJECT
```

#### Block Connections to a Network Interface

```bash
iptables -A INPUT -i eth0 -s 15.15.15.51 -j DROP
```

#### Block Connections to a Network Interface

```bash
iptables -A INPUT -i eth0 -s 15.15.15.51 -j DROP
```

#### Allow All Incoming SSH

```bash
iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow Incoming SSH from Specific IP address or subnet

```bash
iptables -A INPUT -p tcp -s 15.15.15.0/24 --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow Outgoing SSH

```bash
iptables -A OUTPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow Incoming Rsync from Specific IP Address or Subnet

```bash
iptables -A INPUT -p tcp -s 15.15.15.0/24 --dport 873 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 873 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow All Incoming HTTP

```bash
iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 80 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow All Incoming HTTPS

```bash
iptables -A INPUT -p tcp --dport 443 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 443 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow All Incoming HTTP and HTTPS

```bash
iptables -A INPUT -p tcp -m multiport --dports 80,443 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp -m multiport --dports 80,443 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow MySQL from Specific IP Address or Subnet

```bash
iptables -A INPUT -p tcp -s 15.15.15.0/24 --dport 3306 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 3306 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow MySQL to Specific Network Interface

```bash
iptables -A INPUT -i eth1 -p tcp --dport 3306 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -o eth1 -p tcp --sport 3306 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### PostgreSQL from Specific IP Address or Subnet

```bash
iptables -A INPUT -p tcp -s 15.15.15.0/24 --dport 5432 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 5432 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow PostgreSQL to Specific Network Interface

```bash
iptables -A INPUT -i eth1 -p tcp --dport 5432 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -o eth1 -p tcp --sport 5432 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Block Outgoing SMTP Mail

```bash
iptables -A OUTPUT -p tcp --dport 25 -j REJECT
```

#### Allow All Incoming SMTP

```bash
iptables -A INPUT -p tcp --dport 25 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 25 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow All Incoming IMAP

```bash
iptables -A INPUT -p tcp --dport 143 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 143 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow All Incoming IMAPS

```bash
iptables -A INPUT -p tcp --dport 993 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 993 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow All Incoming POP3

```bash
iptables -A INPUT -p tcp --dport 110 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 110 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow All Incoming POP3S

```bash
iptables -A INPUT -p tcp --dport 995 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 995 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Drop Private Network Address On Public Interface

```bash
iptables -A INPUT -i eth1 -s 192.168.0.0/24 -j DROP
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -j DROP
```

#### Only Block Incoming Traffic

```bash
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
iptables -A INPUT -m state --state NEW,ESTABLISHED -j ACCEPT
```

#### Drop All Outgoing to Facebook Networks

Get Facebook AS:

```bash
whois -h v4.whois.cymru.com " -v $(host facebook.com | grep "has address" | cut -d " " -f4)" | tail -n1 | awk '{print $1}'
```

Drop:

```bash
for i in $(whois -h whois.radb.net -- '-i origin AS32934' | grep "^route:" | cut -d ":" -f2 | sed -e 's/^[ \t]*//' | sort -n -t . -k 1,1 -k 2,2 -k 3,3 -k 4,4 | cut -d ":" -f2 | sed 's/$/;/') ; do

  iptables -A OUTPUT -s "$i" -j REJECT

done
```
