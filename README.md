# Cisco-NAT-DHCP
Cisco NAT and DHCP lab allowing LAN clients to reach the internet via router-modem setup

# 🛰️ NAT + DHCP Internet Access Lab

This lab simulates a real-world scenario where a Cisco router connects an internal LAN to the internet using **NAT (Network Address Translation)** and provides IP addresses to LAN clients using **DHCP**. The setup is ideal for testing internet access from a local machine through a Cisco router and modem combination.

## 📡 Topology

[Laptop/PC] ←→ [Switch] ←→ [R1 Gi0/0] --- NAT --- [R1 Gi0/1] ←→ [Modem] IP: DHCP IP: 192.168.10.1 IP: DHCP (from modem)


## ⚙️ Configuration - R1


## ! Configure Interfaces
interface GigabitEthernet0/0
 description INSIDE (LAN)
 ip address 192.168.10.1 255.255.255.0
 ip nat inside
 no shutdown

## interface GigabitEthernet0/1
 description OUTSIDE (WAN)
 ip address dhcp
 ip nat outside
 no shutdown

## ! NAT Configuration
ip access-list standard NAT_ACL
 permit 192.168.10.0 0.0.0.255

## ip nat inside source list NAT_ACL interface GigabitEthernet0/1 overload

## ! DHCP Configuration
ip dhcp pool LOCAL
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8 1.1.1.1

## ip dhcp excluded-address 192.168.10.1 192.168.10.10

✅ Test Steps
Connect your laptop to the switch via Ethernet.

Turn off Wi-Fi and ensure your laptop receives IP from the router (check with ipconfig or ip a).

Test with:

ping 8.8.8.8

Open youtube.com or google.com in a browser.

🧠 Result
Everything worked successfully. NAT translated internal traffic to a public IP (from the modem), and DHCP dynamically assigned IPs to LAN devices. This simulates basic but essential small-office/home-office (SOHO) internet setups using Cisco devices.

## Contact
https://github.com/IlkinNureddinov
