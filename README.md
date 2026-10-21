# VLAN
Zero-Trust Home Lab Security 

This is documentation of the transformation of a regular, everyday home network into a segmented, zero-trust architecture. By leveraging Ubiquiti's native enterprise management ecosystem (UniFi OS), traffic analysis, IDS/IPS, and unified logging are built in and very easy to use and implement, thereby bypassing the usually arduous process of setting up a SIEM pipeline. Also, we will be segmenting the network with VLAN. This project is a step towards enterprise-level network security at the household level, which is increasingly important today.

Project Goals:

1 Network Segmentation: Transition to zero-trust segmented network w/ VLANs and firewall rules.

2 Security Visibility: Utilize event aggregation, threat management, and system logs.

3 Threat Defense: Use Intrusion Detection & Prevention Systems, and block unauthorized traffic.

How It Works!

Network Segmentation & VLANs via Controller

The network was restructured into isolated networks

Creating VLAN Networks:

  VLAN 10 (Management): Restrictive corporate/admin access.

  VLAN 20 (Servers): Hosts infrastructure, NAS, and local server workloads.

  VLAN 30 (Trusted): Daily driver devices and personal workstation.

  VLAN 40 (IoT/Guest): Isolated network with guest policies enforced.

  Configuring Wi-Fi SSIDs:

  Mapped specific SSIDs on AP1 and AP2 directly to VLAN 30 (Trusted) and VLAN 40 (IoT) to automatically partition wireless traffic at the access point level.

Zero-Trust Firewall & Traffic Rules

Rather than manual CLI rules, UniFi has native support via software :)
VLAN Restriction: default-deny rules preventing IoT devices (VLAN 40) from initiating communication with the Server/Storage VLAN (VLAN 20) or Management VLAN (VLAN 10).

Allowed admin Control: explicit allow rules permitting only the PC ( on VLAN 30) to access server management ports.

Native Threat Management & Security Monitoring

I <3 UniFi, makes life so easy
    Intrusion Detection & Prevention (IDS/IPS):

Detect and block mode on UniFi software uses signature matching to automatically intercept malicious traffic, port scans, and known exploit attempts across VLAN boundaries.

Activity Logs:

 The System Logs tab in UniFi can be used to review administrative actions, client connection events, and security alerts.

Challenges Overcome & Lessons Learned
Challenge 1: Broken AP

 Description: AP 1 was physically damaged and refused adoption :(

  Solution: RMA, new AP :)

Challenge 2: Firewall Rule Precedence

 Description: Initial firewall drop rules accidentally blocked gateway DNS for the trusted network.

 Solution: adjusted the rule order in the firewall to ensure established sessions and important local services (DNS, etc.) had higher priority than inter-VLAN blocking rules.


Network Architecture diagram:

<img width="1406" height="646" alt="image" src="https://github.com/user-attachments/assets/8e4e49fd-f275-4ecd-aac9-4a2df1d387d6" />

