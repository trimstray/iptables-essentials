<h2 align="center">Iptables Essentials: Common Firewall Rules and Commands</h2>

<br>

<p align="center">
  <a href="https://github.com/trimstray/iptables-essentials/pulls">
    <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?longCache=true" alt="Pull Requests">
  </a>
  <a href="LICENSE.md">
    <img src="https://img.shields.io/badge/License-MIT-lightgrey.svg?longCache=true" alt="MIT License">
  </a>
</p>

<p align="center">
  <a href="https://twitter.com/trimstray" target="_blank">
    <img src="https://img.shields.io/twitter/follow/trimstray.svg?logo=twitter">
  </a>
</p>

<div align="center">
  <sub>Created by
  <a href="https://twitter.com/trimstray">trimstray</a> and
  <a href="https://github.com/trimstray/iptables-essentials/graphs/contributors">contributors</a>
</div>

<br>

## :ballot_box_with_check: TODO

- [ ] Add useful Iptables configuration examples
- [x] Add useful Kernel Settings (sysctl) configuration
- [ ] Add links to useful external resources
- [x] Add advanced configuration examples, commands, rules

****

## Table of Contents

- [Tools to help you configure Iptables](#tools-to-help-you-configure-iptables)
- [Manuals/Howtos/Tutorials](#manualshowtostutorials)
- [Useful Kernel Settings (sysctl) configuration](#useful-kernel-settings-sysctl-configuration)
  * [rp_filter](#rp_filter)
  * [log_martians](#log_martians)
  * [send_redirects](#send_redirects)
  * [accept_source_route](#accept_source_route)
  * [accept_redirects](#accept_redirects)
  * [tcp_syncookies](#tcp_syncookies)
  * [icmp_echo_ignore_broadcasts](#icmp_echo_ignore_broadcasts)
  * [ip_forward](#ip_forward)
- [How it works?](#how-it-works)
- [Iptables Rules](#iptables-rules)
  * [Saving Rules](#saving-rules)
    - [Debian Based](#debian-based)
    - [RedHat Based](#redhat-based)
  * [List out all of the active iptables rules with verbose](#list-out-all-of-the-active-iptables-rules-with-verbose)
  * [List out all of the active iptables rules with numeric lines and verbose](#list-out-all-of-the-active-iptables-rules-with-numeric-lines-and-verbose)
  * [Print out all of the active iptables rules](#print-out-all-of-the-active-iptables-rules)
  * [List Rules as Tables for INPUT chain](#list-rules-as-tables-for-input-chain)
  * [Print all of the rule specifications in the INPUT chain](#print-all-of-the-rule-specifications-in-the-input-chain)
  * [Show Packet Counts and Aggregate Size](#show-packet-counts-and-aggregate-size)
  * [To display INPUT or OUTPUT chain rules with numeric lines and verbose](#to-display-input-or-output-chain-rules-with-numeric-lines-and-verbose)
  * [Delete Rule by Chain and Number](#delete-rule-by-chain-and-number)
  * [Delete Rule by Specification](#delete-rule-by-specification)
  * [Flush All Rules, Delete All Chains, and Accept All](#flush-all-rules-delete-all-chains-and-accept-all)
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
  * [Drop All Outgoing to Facebook Networks](#drop-all-outgoing-to-facebook-networks)
  * [Log and Drop Packets](#log-and-drop-packets)
  * [Log and Drop Packets with Limited Number of Log Entries](#log-and-drop-packets-with-limited-number-of-log-entries)
  * [Drop or Accept Traffic From Mac Address](#drop-or-accept-traffic-from-mac-address)
  * [Block or Allow ICMP Ping Request](#block-or-allow-icmp-ping-request)
  * [Specifying Multiple Ports with `multiport`](#specifying-multiple-ports-with-multiport)
  * [Load Balancing with `random*` or `nth*`](#load-balancing-with-random-or-nth)
  * [Restricting the Number of Connections with `limit` and `iplimit*`](#restricting-the-number-of-connections-with-limit-and-iplimit)
  * [Maintaining a List of recent Connections to Match Against](#maintaining-a-list-of-recent-connections-to-match-against)
  * [Matching Against a `string*` in a Packet's Data Payload](#matching-against-a-string-in-a-packets-data-payload)
  * [Time-based Rules with `time*`](#time-based-rules-with-time)
  * [Packet Matching Based on TTL Values](#packet-matching-based-on-ttl-values)
  * [Protection against port scanning](#protection-against-port-scanning)
  * [SSH brute-force protection](#ssh-brute-force-protection)
  * [Syn-flood protection](#syn-flood-protection)
    - [Mitigating SYN Floods With SYNPROXY](#mitigating-syn-floods-with-synproxy)
  * [Block New Packets That Are Not SYN](#block-new-packets-that-are-not-syn)
  * [Force Fragments packets check](#force-fragments-packets-check)
  * [XMAS packets](#xmas-packets)
  * [Drop all NULL packets](#drop-all-null-packets)
  * [Block Uncommon MSS Values](#block-uncommon-mss-values)
  * [Block Packets With Bogus TCP Flags](#block-packets-with-bogus-tcp-flags)
  * [Block Packets From Private Subnets (Spoofing)](#block-packets-from-private-subnets-spoofing)
- [Advanced configuration examples](#advanced-configuration-examples)
  * [Packet handling in Python using NFQUEUE target](#packet-handling-in-python-using-nfqueue-target)
    - [ACCEPT all packets from specific source on (filter:INPUT) and DROP everything else](#accept-all-packets-from-specific-source-on-filterinput-and-drop-everything-else)
    - [Write your own port knocking script to secure ssh access](#write-your-own-port-knocking-script-to-secure-ssh-access)

****

## Tools to help you configure Iptables

<p>
&nbsp;&nbsp;:small_orange_diamond: <a href="http://shorewall.org/"><b>Shorewall</b></a> - advanced gateway/firewall configuration tool for GNU/Linux.<br>
&nbsp;&nbsp;:small_orange_diamond: <a href="https://firewalld.org/"><b>Firewalld</b></a> - provides a dynamically managed firewall.<br>
&nbsp;&nbsp;:small_orange_diamond: <a href="https://wiki.ubuntu.com/UncomplicatedFirewall"><b>UFW</b></a> - default firewall configuration tool for Ubuntu.<br>
&nbsp;&nbsp;:small_orange_diamond: <a href="https://github.com/firehol/firehol"><b>FireHOL</b></a> - offer simple and powerful configuration for all Linux firewall and traffic shaping requirements.<br>
</p>

## Manuals/Howtos/Tutorials

<p>
&nbsp;&nbsp;:small_orange_diamond: <a href="https://major.io/2010/04/12/best-practices-iptables/"><b>Best practices: iptables - by Major Hayden</b></a><br>
&nbsp;&nbsp;:small_orange_diamond: <a href="https://www.booleanworld.com/depth-guide-iptables-linux-firewall/"><b>An In-Depth Guide to Iptables, the Linux Firewall</b></a><br>
&nbsp;&nbsp;:small_orange_diamond: <a href="https://linuxgazette.net/108/odonovan.html"><b>Advanced Features of netfilter/iptables</b></a><br>
&nbsp;&nbsp;:small_orange_diamond: <a href="http://www.linuxhomenetworking.com/wiki/index.php/Quick_HOWTO_:_Ch14_:_Linux_Firewalls_Using_iptables"><b>Linux Firewalls Using iptables</b></a><br>
&nbsp;&nbsp;:small_orange_diamond: <a href="https://serverfault.com/questions/696182/debugging-iptables-and-common-firewall-pitfalls"><b>Debugging iptables and common firewall pitfalls?</b></a><br>
&nbsp;&nbsp;:small_orange_diamond: <a href="https://www.netfilter.org/documentation/HOWTO/netfilter-hacking-HOWTO-4.html"><b>Netfilter Hacking HOWTO</b></a><br>
&nbsp;&nbsp;:small_orange_diamond: <a href="https://making.pusher.com/per-ip-rate-limiting-with-iptables/"><b>Per-IP rate limiting with iptables</b></a><br>
</p>

## Useful Kernel Settings (sysctl) Configuration

##### rp_filter

  > _Disable routing triangulation. Respond to queries out the same interface, not another. Also protects against IP spoofing._

```bash
cat << EOF >> /etc/sysctl.d/40-custom.conf
net/ipv4/conf/all/rp_filter = 1
EOF
```

- [rp_filter and LPIC-3 Linux Security](https://www.theurbanpenguin.com/rp_filter-and-lpic-3-linux-security/)
- [Linux kernel rp_filter settings (Reverse path filtering)](https://www.slashroot.in/linux-kernel-rpfilter-settings-reverse-path-filtering)
- [Reverse Path Filtering](http://tldp.org/HOWTO/Adv-Routing-HOWTO/lartc.kernel.rpf.html)

##### log_martians

  > _Enable logging of packets with malformed IP addresses._

```bash
cat << EOF >> /etc/sysctl.d/40-custom.conf
net/ipv4/conf/all/log_martians = 1
EOF
```

- [What is the usefulness of logging of martians packet?](https://serverfault.com/questions/570980/what-is-the-usefulness-of-logging-of-martians-packet-e-g-net-ipv4-conf-all-lo)

##### send_redirects

  > _Disables sending of all IPv4 ICMP redirected packets on all interfaces._

```bash
cat << EOF >> /etc/sysctl.d/40-custom.conf
net/ipv4/conf/all/send_redirects = 0
EOF
```

- [Disable source routing](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security_guide/sect-security_guide-server_security-disable-source-routing)
- [What are ICMP redirects and should they be blocked?](https://askubuntu.com/questions/118273/what-are-icmp-redirects-and-should-they-be-blocked)

##### accept_source_route

  > _Disable source routed packets (packets with the Strict Source Route (SSR) or Loose Source Routing (LSR) option set)._

```bash
cat << EOF >> /etc/sysctl.d/40-custom.conf
net/ipv4/conf/all/accept_source_route = 0
EOF
```

- [Disable source routing](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/security_guide/sect-security_guide-server_security-disable-source-routing)
- [The system must not accept IPv4 source-routed packets by default.](https://www.stigviewer.com/stig/red_hat_enterprise_linux_6/2017-12-08/finding/V-38529)

##### accept_redirects

  > _Disable acceptance of ICMP redirects._

```bash
cat << EOF >> /etc/sysctl.d/40-custom.conf
net/ipv4/conf/all/accept_redirects = 0
EOF
```

- [What are ICMP redirects and should they be blocked?](https://askubuntu.com/questions/118273/what-are-icmp-redirects-and-should-they-be-blocked)
- [The Red Hat Enterprise Linux operating system must ignore Internet Protocol version 4 (IPv4) Internet Control Message Protocol (ICMP) redirect messages.](https://www.stigviewer.com/stig/red_hat_enterprise_linux_7/2018-11-28/finding/V-73175)

##### tcp_syncookies

  > _Turn on SYN-flood protections (protection from Denial of Service (DOS) attacks)._

```bash
cat << EOF >> /etc/sysctl.d/40-custom.conf
net/ipv4/tcp_syncookies = 1
EOF
```

- [Hardening your TCP/IP Stack Against SYN Floods](https://www.ndchost.com/wiki/server-administration/hardening-tcpip-syn-flood)
- [Linux: Turn On TCP SYN Cookie Protection](https://www.cyberciti.biz/faq/enable-tcp-syn-cookie-protection/)
- [Better alternative for tcp_syncookies in Linux](https://serverfault.com/questions/705504/better-alternative-for-tcp-syncookies-in-linux)

##### icmp_echo_ignore_broadcasts

  > _Disable responding to ping broadcasts._

```bash
cat << EOF >> /etc/sysctl.d/40-custom.conf
net/ipv4/icmp_echo_ignore_broadcasts = 1
EOF
```

- [What is ICMP broadcast good for?](https://superuser.com/questions/306065/what-is-icmp-broadcast-good-for)
- [The system must not respond to ICMPv4 sent to a broadcast address.](https://www.stigviewer.com/stig/red_hat_enterprise_linux_6/2018-11-28/finding/V-38535)

##### ip_forward

  > _Enable IP routing. Required if your firewall is protecting a network, NAT included._

```bash
cat << EOF >> /etc/sysctl.d/40-custom.conf
net/ipv4/ip_forward = 1
EOF
```

- [Introduction to routers](http://linux-training.be/security/ch10.html)
- [How to Enable IP Forwarding in Linux](http://www.ducea.com/2006/08/01/how-to-enable-ip-forwarding-in-linux/)
- [What is kernel ip forwarding?](https://unix.stackexchange.com/questions/14056/what-is-kernel-ip-forwarding)

## How it works?

<p align="center">
    <img src="https://github.com/trimstray/iptables-essentials/blob/master/static/img/iptables-packet-flow-ng.png"
        alt="Master">
</p>

## Iptables Rules

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
iptables -A INPUT -s 192.168.252.10 -j DROP
```

#### Block and IP Address and Reject

```bash
iptables -A INPUT -s 192.168.252.10 -j REJECT
```

#### Block Connections to a Network Interface

```bash
iptables -A INPUT -i eth0 -s 192.168.252.10 -j DROP
```

#### Allow All Incoming SSH

```bash
iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow Incoming SSH from Specific IP address or subnet

```bash
iptables -A INPUT -p tcp -s 192.168.240.0/24 --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow Outgoing SSH

```bash
iptables -A OUTPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow Incoming Rsync from Specific IP Address or Subnet

```bash
iptables -A INPUT -p tcp -s 192.168.240.0/24 --dport 873 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
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
iptables -A INPUT -p tcp -s 192.168.240.0/24 --dport 3306 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -p tcp --sport 3306 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### Allow MySQL to Specific Network Interface

```bash
iptables -A INPUT -i eth1 -p tcp --dport 3306 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A OUTPUT -o eth1 -p tcp --sport 3306 -m conntrack --ctstate ESTABLISHED -j ACCEPT
```

#### PostgreSQL from Specific IP Address or Subnet

```bash
iptables -A INPUT -p tcp -s 192.168.240.0/24 --dport 5432 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
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

#### Log and Drop Packets

```bash
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -j LOG --log-prefix "IP_SPOOF A: "
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -j DROP
```

By default everything is logged to `/var/log/messages` file:

```bash
tail -f /var/log/messages
grep --color 'IP SPOOF' /var/log/messages
```

#### Log and Drop Packets with Limited Number of Log Entries

```bash
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -m limit --limit 5/m --limit-burst 7 -j LOG --log-prefix "IP_SPOOF A: "
iptables -A INPUT -i eth1 -s 10.0.0.0/8 -j DROP
```

#### Drop or Accept Traffic From Mac Address

```bash
iptables -A INPUT -m mac --mac-source 00:0F:EA:91:04:08 -j DROP
iptables -A INPUT -p tcp --destination-port 22 -m mac --mac-source 00:0F:EA:91:04:07 -j ACCEPT
```

#### Block or Allow ICMP Ping Request

```bash
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
iptables -A INPUT -i eth1 -p icmp --icmp-type echo-request -j DROP
```

#### Specifying Multiple Ports with `multiport`

```bash
iptables -A INPUT -i eth0 -p tcp -m state --state NEW -m multiport --dports ssh,smtp,http,https -j ACCEPT
```

#### Load Balancing with `random*` or `nth*`

```bash
_ips=("172.31.250.10" "172.31.250.11" "172.31.250.12" "172.31.250.13")

for ip in "${_ips[@]}" ; do
  iptables -A PREROUTING -i eth0 -p tcp --dport 80 -m state --state NEW -m nth --counter 0 --every 4 --packet 0 \
    -j DNAT --to-destination ${ip}:80
done
```

or

```bash
_ips=("172.31.250.10" "172.31.250.11" "172.31.250.12" "172.31.250.13")

for ip in "${_ips[@]}" ; do
  iptables -A PREROUTING -i eth0 -p tcp --dport 80 -m state --state NEW -m random --average 25 \
    -j DNAT --to-destination ${ip}:80
done
```

#### Restricting the Number of Connections with `limit` and `iplimit*`

```bash
iptables -A FORWARD -m state --state NEW -p tcp -m multiport --dport http,https -o eth0 -i eth1 \
    -m limit --limit 20/hour --limit-burst 5 -j ACCEPT
```

or

```bash
iptables -A INPUT -p tcp -m state --state NEW --dport http -m iplimit --iplimit-above 5 -j DROP
```

#### Maintaining a List of recent Connections to Match Against

```bash
iptables -A FORWARD -m recent --name portscan --rcheck --seconds 100 -j DROP
iptables -A FORWARD -p tcp -i eth0 --dport 443 -m recent --name portscan --set -j DROP
```

#### Matching Against a `string*` in a Packet's Data Payload

```bash
iptables -A FORWARD -m string --string '.com' -j DROP
iptables -A FORWARD -m string --string '.exe' -j DROP
```

#### Time-based Rules with `time*`

```bash
iptables -A FORWARD -p tcp -m multiport --dport http,https -o eth0 -i eth1 \
    -m time --timestart 21:30 --timestop 22:30 --days Mon,Tue,Wed,Thu,Fri -j ACCEPT
```

#### Packet Matching Based on TTL Values

```bash
iptables -A INPUT -s 1.2.3.4 -m ttl --ttl-lt 40 -j REJECT
```

#### Protection against port scanning

```bash
iptables -N port-scanning
iptables -A port-scanning -p tcp --tcp-flags SYN,ACK,FIN,RST RST -m limit --limit 1/s --limit-burst 2 -j RETURN
iptables -A port-scanning -j DROP
```

#### SSH brute-force protection

```bash
iptables -A INPUT -p tcp --dport ssh -m conntrack --ctstate NEW -m recent --set
iptables -A INPUT -p tcp --dport ssh -m conntrack --ctstate NEW -m recent --update --seconds 60 --hitcount 10 -j DROP
```

#### Syn-flood protection

```bash
iptables -N syn_flood

iptables -A INPUT -p tcp --syn -j syn_flood
iptables -A syn_flood -m limit --limit 1/s --limit-burst 3 -j RETURN
iptables -A syn_flood -j DROP

iptables -A INPUT -p icmp -m limit --limit  1/s --limit-burst 1 -j ACCEPT

iptables -A INPUT -p icmp -m limit --limit 1/s --limit-burst 1 -j LOG --log-prefix PING-DROP:
iptables -A INPUT -p icmp -j DROP

iptables -A OUTPUT -p icmp -j ACCEPT
```

##### Mitigating SYN Floods With SYNPROXY

```bash
iptables -t raw -A PREROUTING -p tcp -m tcp --syn -j CT --notrack
iptables -A INPUT -p tcp -m tcp -m conntrack --ctstate INVALID,UNTRACKED -j SYNPROXY --sack-perm --timestamp --wscale 7 --mss 1460
iptables -A INPUT -m conntrack --ctstate INVALID -j DROP
```

#### Block New Packets That Are Not SYN

```bash
iptables -A INPUT -p tcp ! --syn -m state --state NEW -j DROP
```

or

```bash
iptables -t mangle -A PREROUTING -p tcp ! --syn -m conntrack --ctstate NEW -j DROP
```

#### Force Fragments packets check

```bash
iptables -A INPUT -f -j DROP
```

#### XMAS packets

```bash
iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP
```

#### Drop all NULL packets

```bash
iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP
```

#### Block Uncommon MSS Values

```bash
iptables -t mangle -A PREROUTING -p tcp -m conntrack --ctstate NEW -m tcpmss ! --mss 536:65535 -j DROP
```

#### Block Packets With Bogus TCP Flags

```bash
iptables -t mangle -A PREROUTING -p tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG NONE -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags FIN,SYN FIN,SYN -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags SYN,RST SYN,RST -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags FIN,RST FIN,RST -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags FIN,ACK FIN -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags ACK,URG URG -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags ACK,FIN FIN -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags ACK,PSH PSH -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags ALL ALL -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags ALL NONE -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags ALL FIN,PSH,URG -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags ALL SYN,FIN,PSH,URG -j DROP
iptables -t mangle -A PREROUTING -p tcp --tcp-flags ALL SYN,RST,ACK,FIN,URG -j DROP
```

#### Block Packets From Private Subnets (Spoofing)

```bash
_subnets=("224.0.0.0/3" "169.254.0.0/16" "172.16.0.0/12" "192.0.2.0/24" "192.168.0.0/16" "10.0.0.0/8" "0.0.0.0/8" "240.0.0.0/5")

for _sub in "${_subnets[@]}" ; do
  iptables -t mangle -A PREROUTING -s "$_sub" -j DROP
done
iptables -t mangle -A PREROUTING -s 127.0.0.0/8 ! -i lo -j DROP
```

## Advanced configuration examples

### Packet handling in Python using NFQUEUE target

  > _This target passes the packet to userspace using the nfnetlink_queue handler. The packet is put into the queue identified by its 16-bit queue number. Userspace can inspect and modify the packet if desired. Userspace must then drop or reinject the packet into the kernel._

#### ACCEPT all packets from specific source on (filter:INPUT) and DROP everything else

  > _This rule forwards all filter:INPUT packets to queue 1 with NFQUEUE target._

```bash
iptables -A INPUT -j NFQUEUE --queue-num 1
```

  > _Script to bind to netfilter queue 1 and handle packets._
  
```python
#!/usr/bin/python3

from netfilterqueue import NetfilterQueue
from scapy.all import *

def packetanalyzer(pkt):
    ip=IP(pkt.get_payload())
    if(ip.src=="192.168.122.1"):
        print(f"New packet from {ip.src}")
        pkt.accept()
    else:
	pkt.drop()

nfqueue=NetfilterQueue()
nfqueue.bind(1, packetanalyzer)
nfqueue.run()
```

#### Write your own port knocking script to secure ssh access

  > _DROP all ssh requests and send secret port requests to user-space with NFQUEUE target._

```bash
iptables -t filter -I INPUT -p tcp --dport 22 -j DROP
iptables -t raw -I PREROUTING -p tcp --sport 65534 --dport 65535 -j NFQUEUE --queue-num 1
```

  > _This script capture packet from netfilter queue 1 and check SOURCEPORT and SECRETPORT for port knocking and allow source to connect to ssh for EXPIRETIME, default is 30 minutes.
  
```python
#!/usr/bin/python3

from os	import system
from netfilterqueue import NetfilterQueue
from scapy.layers.inet import IP
from time import time

SOURCEPORT=65534
SECRETPORT=65535
EXPIRETIME=30
ALLOWED={}

def portknocking(pkt):
    packet=IP(pkt.get_payload())
    currtime=time()
    for item in list(ALLOWED):
        if(currtime-ALLOWED[item] >= EXPIRETIME*60):
            del ALLOWED[item]
    if(packet.sport==SOURCEPORT and packet.dport==SECRETPORT and packet.src not in ALLOWED):
        print(f"Port {packet.dport} knocked by {packet.src}:{packet.sport}")
        system(f"iptables -I INPUT -p tcp --dport 22 -s {packet.src} -j ACCEPT")
        system(f"echo 'iptables -D INPUT -p tcp --dport 22 -s {packet.src} -j ACCEPT' | at now + {EXPIRETIME} minutes")
        ALLOWED[packet.src]=time()
        pkt.drop()

nfqueue=NetfilterQueue()
nfqueue.bind(1, portknocking)

try:
    nfqueue.run()
except KeyboardInterrupt:
    print("\nExit with Keyboard Interrupt")
```

  > _To knocking port and allow ssh connections from your computer just execute this command:_

```bash
nc -p 65534 SERVER 65535
```
