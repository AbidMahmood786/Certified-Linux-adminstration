CHAPTER 7 — Networking & Firewalld (RHCSA Exam‑Focused)
1. RHCSA Objectives

Configure network interfaces using nmcli
Set static IP, DNS, gateway
Bring interfaces up/down
Control firewall rules with firewalld
Open/close ports and services
Use zones and understand their purpose
Verify connectivity with ping, ip, and ss


2. Essential Commands
Network Management
nmcli device status
nmcli connection show
nmcli connection add
nmcli connection modify
nmcli connection up eth0
ip a
ping -c3 8.8.8.8

Set Static IP
nmcli connection modify eth0 ipv4.addresses 192.168.1.50/24
nmcli connection modify eth0 ipv4.gateway 192.168.1.1
nmcli connection modify eth0 ipv4.dns 8.8.8.8
nmcli connection modify eth0 ipv4.method manual
nmcli connection up eth0

Firewalld
firewall-cmd --state
firewall-cmd --get-active-zones
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --zone=public --add-port=8080/tcp --permanent
firewall-cmd --reload
firewall-cmd --list-all

Check listening services
ss -tlnp


3. Fast Theory

NetworkManager controls network interfaces in RHEL.
nmcli is the main RHCSA exam tool for network config.
IP assignment methods:

manual → static
auto → DHCP


Firewalld uses:

Zones (public, home, internal)
Services (http, ssh, samba)
Ports (8080/tcp)


Permanent changes require --permanent + reload.


4. RHCSA Labs
Lab 1 — Set Static IP
nmcli connection modify eth0 ipv4.addresses 10.10.0.50/24
nmcli connection modify eth0 ipv4.gateway 10.10.0.1
nmcli connection modify eth0 ipv4.dns 1.1.1.1
nmcli connection modify eth0 ipv4.method manual
nmcli connection down eth0
nmcli connection up eth0

Validate:
ip a, ping -c3 10.10.0.1

Lab 2 — Configure Firewalld for HTTP
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --reload
firewall-cmd --list-services


Lab 3 — Open Custom Port 8080
firewall-cmd --add-port=8080/tcp --permanent
firewall-cmd --reload


Lab 4 — Verify Listening Services
ss -tlnp


5. Troubleshooting






























IssueDiagnosticFixCan't reach networkip a, nmcli dev statusInterface down or wrong IPDNS problemscat /etc/resolv.confUpdate DNS via nmcliPorts blockedfirewall-cmd --list-allAdd service/portService listening but unreachabless -tlnpFirewall not configured

6. MCQs


Which command shows network interfaces?
A) ifconfig B) netstat C) ip a D) lsnet
Answer: C


To set static IP, set ipv4.method to:
A) default B) static C) manual D) custom
Answer: C


To allow HTTP service:
A) firewall-cmd --add http
B) firewall-cmd --add-service=http
C) firewall-cmd add service
D) systemctl allow http
Answer: B


To list all firewall rules:
A) firewall-cmd --show
B) firewall-cmd --view
C) firewall-cmd --list-all
D) firewall-cmd --all
Answer: C


Which tool configures networking in RHEL?
A) ifconfig B) netctl C) nmcli D) netadm
Answer: C
