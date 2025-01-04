# Personal Project: Virtual Lab Setup for Cybersecurity Testing

This repository contains the documentation for a comprehensive Virtual Lab Setup I created to simulate a real-world enterprise network infrastructure, aimed at enhancing my skills in cybersecurity. The lab is designed to provide hands-on experience with domain management, network security, vulnerability testing, and log aggregation, with integration of tools commonly used in the field.

## Table of Contents
- [Network Topolgy](#network-topology)
- [Project Overview](#project-overview)
- [Virtual Lab Architecture](#virtual-lab-architecture)
- [Steps Taken](#steps-taken)
  - [VM Setup](#vm-setup)
  - [Active Directory Configuration](#active-directory-configuration)
  - [Network Configuration and Troubleshooting](#network-configuration-and-troubleshooting)
  - [Firewall Configuration with pfSense](#firewall-configuration-with-pfsense)
  - [Remote Desktop Setup](#remote-desktop-setup)
  - [Security Tool Integration](#security-tool-integration)
  - [Log Management and Monitoring](#log-management-and-monitoring)
- [Learning Outcomes](#learning-outcomes)
- [Tools Used](#tools-used)
- [Conclusion](#conclusion)
- [License](#license)

## Network Topolgy
![image alt](https://github.com/itspavit/Personal-Homelab-Project/blob/main/network-topology.jpg?raw=true)

## Project Overview
This project focuses on setting up a virtualized network environment that mirrors a typical enterprise infrastructure. The virtual lab setup includes three virtual machines, each configured with specific roles and services to simulate a small organizational network.

The lab consists of:
- **Windows Server 2019** as the Domain Controller and DNS Server.
- **Windows 10** as a client machine.
- **Debian 12** as a Linux-based client machine.
- **pfSense Firewall** for network security.
- Security tools such as **Wapati**, **Nmap**, and **Splunk** for vulnerability testing, network scanning, and log aggregation.

The primary goal of this project is to enhance practical knowledge of managing network infrastructure, domain integration, and using security tools to protect and monitor the network.

## Virtual Lab Architecture
The virtual lab architecture consists of the following components:

- **Windows Server 2019 VM:**
  - Acts as the Domain Controller and DNS server.
  - Hosts the Active Directory for managing users, groups, and domain policies.
  - Configured with static IP: `192.168.1.11`.

- **Windows 10 VM:**
  - A client machine that joins the Active Directory domain.
  - Static IP: `192.168.1.10`.

- **Debian 12 VM:**
  - A Linux-based machine joined to the Active Directory domain.
  - Static IP: `192.168.1.12`.

- **pfSense Firewall:**
  - Provides security and traffic management for the internal network.
  - Network configuration with LAN, WAN, and NAT interfaces.

## Steps Taken

### VM Setup
I created and configured the following virtual machines in VirtualBox:
- **Windows Server 2019 VM** with a static IP of `192.168.1.11`, acting as the DNS Server and Domain Controller.
- **Windows 10 VM** with a static IP of `192.168.1.10`, which joined the domain for testing.
- **Debian 12 VM** with a static IP of `192.168.1.12`, also joined to the domain for integration.

For each VM, I configured two network adapters:
- **Internal Network Adapter:** Allowed communication between the VMs on the same network.
- **NAT Adapter:** Enabled access to the internet through the host machine.

### Active Directory Configuration
To simulate a real-world enterprise network, I configured Active Directory on the Windows Server 2019 VM:
- Installed the **Active Directory Domain Services** role.
- Promoted Windows Server 2019 to become the Domain Controller for the domain `mylab.local`.
- Configured DNS on the server to ensure name resolution for all internal devices.
- Set up Organizational Units (OUs), created test users, and assigned them to departments.
- Configured domain policies and added groups like HR, Sales, IT, and Support.
- Joined Windows 10 and Debian 12 to the domain by running domain join commands on each system.

### Network Configuration and Troubleshooting
For all VMs, I configured the network to ensure proper connectivity and communication:
- Configured DNS on the Windows Server 2019 to resolve domain names internally and added Forwarders to public DNS servers (e.g., Google DNS `8.8.8.8`).
- Fixed network connectivity issues on Debian 12 by editing the network interfaces file to enable the second interface (`enp0s8`) and configure it with DHCP.
- Ensured all VMs had connectivity between each other and the internet using the correct network adapters and configuration.

### Firewall Configuration with pfSense
I installed and configured pfSense as a firewall to manage network traffic:
- Set up three network adapters for pfSense:
  - **WAN:** Connected to the external network.
  - **LAN:** For internal network communication.
  - **NAT:** Allowed the VMs to access external resources.
- Configured firewall rules on pfSense to control traffic between the internal and external networks using its web GUI at `192.168.1.1`.

### Remote Desktop Setup
To facilitate remote administration, I enabled Remote Desktop access on both Windows Server 2019 and Windows 10:
- Enabled Remote Desktop on both systems.
- Configured Windows Firewall to allow RDP connections within the internal subnet (`192.168.1.0/24`).
- Installed **Remmina** on Debian 12 for RDP access to the Windows systems.
- Tested RDP connectivity using both **Remmina** and the built-in Remote Desktop Connection on the Windows VM.

### Security Tool Integration
For added security, I installed and configured various tools for vulnerability scanning and network monitoring:
- **Wapati:** A web vulnerability scanner used to identify security flaws in web applications running on the network.
- **Nmap:** A powerful network scanning tool used to identify open ports, services, and vulnerabilities across the network.
- **Splunk:** A log management platform for collecting and analyzing logs. I configured Splunk Forwarders on both Debian 12 and Windows Server 2019 to forward logs to the Splunk server on Windows 10 for analysis.

### Log Management and Monitoring
To monitor the environment effectively, I set up log aggregation with Splunk:
- Configured Splunk to receive and analyze logs from both Debian 12 and Windows Server 2019.
- Used Splunk Forwarders on both Linux and Windows systems to push logs to the central Splunk instance.
- Monitored network events, user logins, and system activities to detect any unusual activity or security incidents.

## Learning Outcomes
This project has provided me with hands-on experience in several key areas of cybersecurity:
- **Domain Management:** Setting up and managing Active Directory for user and group management.
- **Network Security:** Using pfSense to control network traffic and segment the internal network.
- **Security Tool Integration:** Deploying tools like Wapati, Nmap, and Splunk for vulnerability scanning, network discovery, and log aggregation.
- **Remote Administration:** Configuring and testing Remote Desktop access for Windows systems in a virtualized environment.
- **Log Monitoring:** Aggregating and analyzing logs to detect potential security events using Splunk.

## Tools Used
- **VirtualBox:** A free and open-source virtualization software for creating and managing virtual machines.
- **Windows Server 2019:** Used as the domain controller and DNS server for the virtual lab.
- **Windows 10:** A client machine that joined the Active Directory domain for testing.
- **Debian 12:** A Linux-based client joined to the Active Directory domain for integration testing.
- **pfSense:** A popular open-source firewall used for managing network traffic between internal and external networks.
- **Wapati:** A web application vulnerability scanner.
- **Nmap:** A network scanning tool used for host discovery and vulnerability scanning.
- **Splunk:** A platform for searching, monitoring, and analyzing machine-generated big data via a web-style interface.

## Conclusion
This project allowed me to gain practical experience in simulating an enterprise network with multiple systems, including a Windows Domain Controller, Linux-based clients, and a pfSense firewall. It also gave me hands-on exposure to the integration of key cybersecurity tools for monitoring and analyzing network traffic and system logs.

Through this project, I enhanced my skills in network administration, system configuration, security monitoring, and vulnerability management—all essential for a career in cybersecurity.


