# Active Directory

Active Directory is a directory service developed by Microsoft for Windows domain networks. It stores information about objects on the network (such as users, computers, groups, printers, etc.) and makes this information easy to find and use for administrators and applications.

- Active Directory is the core component you're setting up in a Windows Server–based directory services project.
- It's used to centralize management of network resources, like users and computers, across the organization.
- AD allows for authentication (who you are) and authorization (what you can access).
- Admins use tools like Active Directory Users and Computers (ADUC) to create and manage accounts, set group policies, and control access.
- An AD project might involve designing the structure (domains, OUs, group policies), migrating users, or setting up trusts between domains.

  
# Domain Controller

A Domain Controller is a Windows Server that hosts a copy of the Active Directory database and is responsible for authenticating users, enforcing policies, and managing access to networked resources within a domain.

- In your project, you'll promote a Windows Server to a Domain Controller using the Active Directory Domain Services (AD DS) role.
- The Domain Controller is where AD lives—it stores the NTDS.dit database (which contains all AD objects and configurations).
- You typically have at least one DC, but for redundancy, multiple DCs are deployed.
- It handles login requests, validates credentials, applies Group Policy Objects (GPOs), and replicates changes to other DCs in the domain.
- In a larger AD deployment, you might also work with Read-Only Domain Controllers (RODCs) for branch offices or Global Catalog Servers for large forests.

# Active Directory Domain Services (Windows Server)

  - <ins>Forest</ins>: The entire Corporation (e.g., "Acme Global Inc."). It has one overarching legal structure, corporate identity, and a set of fundamental rules that apply to everyone.
    The Forest Root Domain (acmeglobal.com) is like the Headquarters or the initial core business unit from which everything else grew.

  - <ins>Domains</ins>: These are like major business divisions or subsidiaries within the corporation (e.g., "Acme Sales Division - sales.acmeglobal.com," "Acme Research & Development - rnd.acmeglobal.com").
    Each division (domain) has its own leadership, budget, and specific operational policies that apply to its employees and assets.
    They can authenticate their own employees, manage their own computers, and set their own security rules (e.g., "Sales staff must change passwords every 60 days," "R&D computers require specific encryption").
    Crucially, because they are part of the same corporation (forest), there are established trust relationships that allow employees from one division to access resources in another, provided they have the necessary             permissions.

  - <ins>Organizational Units (OUs)</ins>: Within each domain, you'd then use Organizational Units (OUs). These are like the departments within each division (e.g., within the Sales division, you might have "North America Sales,"       "Europe Sales," "Sales Management").
    OUs allow for even more granular administrative delegation and Group Policy application within a domain. You can delegate management of "North America Sales" users to a specific team without giving them control over all      of Sales, let alone the entire corporation.


# Organizational Unit (OUs)
An Organizational Unit (OU) is a container object within Active Directory used to logically group users, computers, groups, or other OUs. It provides structure within a domain and allows for delegated administration and application of Group Policies.

- You create OUs to reflect the organizational structure (e.g., departments like HR, IT, Sales).
- OUs allow you to apply Group Policy Objects (GPOs) at a granular level—for example, deploying specific security settings only to the HR department.
- You can delegate control of an OU to specific administrators without giving them full domain admin rights.
- OUs make it easier to manage large environments by grouping similar objects logically.


# Users -> MembersOf Attribute
Common Built-in Groups:
  - Domain Users (All new users are typically added to this by default)
  - Domain Admins (If Alice needs administrative privileges over the domain)
  - Enterprise Admins (If Alice needs administrative privileges over the entire forest)
  - Schema Admins (If Alice needs to modify the AD schema)
  - Account Operators (To create/manage user and group accounts)
  - Print Operators (To manage printers)
  - Server Operators (To manage servers)
  - Backup Operators (To perform backups)
  - Remote Desktop Users (To allow RDP access to servers)

# RAS/NAT

RAS (Remote Access Service) allows remote users to connect to the internal network via VPN or dial-up.
NAT (Network Address Translation) enables multiple devices on a private network to access the internet using a single public IP address.

- RAS is configured to allow remote employees or admins to securely access internal resources (like AD, file shares, etc.) over the internet.
- NAT is used to enable internal AD-connected machines (on a private IP scheme) to access the internet or to route traffic between subnets.
- When deploying domain-joined laptops or providing external access to DCs or internal services, RAS with NAT is often used in conjunction with Routing and Remote Access.

# Routing and Remote Access Tool [Windows Server]

RRAS is a role/service in Windows Server that allows a server to act as a VPN server, router, and provide NAT services.

- Enables VPN access so remote users can connect securely to the corporate network and access AD resources.
- Can be configured for LAN routing between subnets in a multi-site AD environment.
- Provides NAT, allowing internal AD clients to access the internet.
- Often used to implement site-to-site VPNs between different AD locations or branches.


#DHCP Server

A DHCP Server automatically assigns IP addresses and network configuration (like subnet mask, default gateway, DNS) to client devices on the network.

- Ensures all domain-joined machines receive valid IP settings to communicate with domain controllers and other network services.
- You configure DHCP scopes to define the range of IP addresses for different subnets or departments.
- In AD environments, DHCP is often integrated with Dynamic DNS (DDNS) so that hostnames of clients are automatically registered in DNS.
- You can set reservations for specific devices (like printers or servers) and apply DHCP options (e.g., default gateway, DNS server IPs).
