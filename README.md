# Active-Directory-Project
Active Directory lab environment to manage user accounts, organizational units, and group policies. Configured domain controllers, DNS, and Group Policy Objects (GPOs) for centralized authentication and access control. I wanted to create and manage this project to gain knowledge on setting up, configuring, and managing a simulated Active Directory enviornment. I wanted to gain knowledge on the fundamentals of infracture knowledge for identity and access management/system adminstration
  - I have two other files that I wrote while configuring and finshin this project. One of the files is for key terms/takeways I found while completing the project and the other file is short steps that I wrote down so I can easily recall what I did in the future if
I do decide to redo this project/expand upon it

**Lab Architecture**
Virtualization Platform
-  VirtualBox is used to host all virtual machines.

The environment consists of:

  - Windows Server 2019 (Domain Controller)

  - Windows 10 Client

![Diagram](https://media.discordapp.net/attachments/645079991310090243/1399570555849670767/AD_Flow.png?ex=68897b27&is=688829a7&hm=c1a5fe94ae0056d443caaffaeb0ec62c94f7981c478596caef798d6c7af98208&=&format=webp&quality=lossless)

# Network Configuration
Domain Controller (DC)
OS: Windows Server 2019

**Roles Installed:**

  - Active Directory Domain Services (AD DS)

  - DHCP Server

  - NAT Routing and Remote Access (RAS)

  - Domain Name: anikdomain.com

**Network Interfaces:**

  - NIC 1 (Internet):

      - DHCP from home router

      - Provides external internet access

  - NIC 2 (Internal):

    - IP: 172.16.0.1

    - Subnet Mask: 255.255.255.0

    - DNS: 127.0.0.1 (self)

# DHCP Configuration 
  - Scope Range: 172.16.0.100 - 172.16.0.200
  
  - Subnet Mask: 255.255.255.0
    
  - Gateway: 172.168.0.1
    
  - DNS Server: 172.16.0.1

# Client (Windows 10)

  - NIC (Internal): Obtains IP via DHCP from DC

**Joins the domain anikdomain.com**

# Active Directory Configuration
  - Domain: mydomain.com

# Organizational Units (OUs):

  - Created for structured management (e.g., Users, Groups)

# PowerShell Automation:

  - Script created to add 1,000+ user accounts in bulk to the AD domain.

# RAS / NAT Configuration
  - Configured on the DC to allow internal clients to access the internet through the DC.

  - External Network: Internet (via home router)

  - Internal Network: VirtualBox internal network

# Features Implemented 
  - Configured Active Directory Domain Services
  - Set up DHCP server for IP address allocation
  - Implemented NAT and Routing for internet access
  - Automated user account creation using PowerShell
  - Joined Windows 10 client to the domain

# Tools and Technologies
Windows Server 2019

Windows 10

PowerShell (for automation)

VirtualBox (virtualization platform)



