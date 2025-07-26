# Active-Directory-Project
Active Directory lab environment to manage user accounts, organizational units, and group policies. Configured domain controllers, DNS, and Group Policy Objects (GPOs) for centralized authentication and access control

#Lab Architecture
Virtualization Platform
-  VirtualBox is used to host all virtual machines.

The environment consists of:

  - Windows Server 2019 (Domain Controller)

  - Windows 10 Client

# Network Configuration
Domain Controller (DC)
OS: Windows Server 2019

Roles Installed:

  - Active Directory Domain Services (AD DS)

  - DHCP Server

  - NAT Routing and Remote Access (RAS)

  - Domain Name: anikdomain.com

* Network Interfaces:

  - NIC 1 (Internet):

      - DHCP from home router

      - Provides external internet access

  - NIC 2 (Internal):

    - IP: 172.16.0.1

    - Subnet Mask: 255.255.255.0

    - DNS: 127.0.0.1 (self)



