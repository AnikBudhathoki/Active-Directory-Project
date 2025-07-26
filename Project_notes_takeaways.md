# Active Directory

# Domain Controller

# Active Directory Domain Services (Windows Server)

  - __Forest__: The entire Corporation (e.g., "Acme Global Inc."). It has one overarching legal structure, corporate identity, and a set of fundamental rules that apply to everyone.
    The Forest Root Domain (acmeglobal.com) is like the Headquarters or the initial core business unit from which everything else grew.

  - __Domains__: These are like major business divisions or subsidiaries within the corporation (e.g., "Acme Sales Division - sales.acmeglobal.com," "Acme Research & Development - rnd.acmeglobal.com").
    Each division (domain) has its own leadership, budget, and specific operational policies that apply to its employees and assets.
    They can authenticate their own employees, manage their own computers, and set their own security rules (e.g., "Sales staff must change passwords every 60 days," "R&D computers require specific encryption").
    Crucially, because they are part of the same corporation (forest), there are established trust relationships that allow employees from one division to access resources in another, provided they have the necessary             permissions.

  - __Organizational Units (OUs)__: Within each domain, you'd then use Organizational Units (OUs). These are like the departments within each division (e.g., within the Sales division, you might have "North America Sales,"       "Europe Sales," "Sales Management").
    OUs allow for even more granular administrative delegation and Group Policy application within a domain. You can delegate management of "North America Sales" users to a specific team without giving them control over all      of Sales, let alone the entire corporation.
