# Active Directory Basics

## Introduction
Microsoft's Active Directory (AD) is the backbone of the corporate world. It simplifies the management of devices and users within a corporate environment. In this room, we’ll take a deep dive into the essential components of Active Directory.
**Topics To Be Covered**
- What Active Directory is  
- What an Active Directory Domain is  
- What components go into an Active Directory Domain  
- Forests and Domain Trust  
- And much more!  


## Windows Domain

### Concepts Learned
- A Windows domain centralizes management of users, computers, and policies in a network.
- Active Directory (AD) is the repository that manages identities and policies.
- The Domain Controller (DC) is the server running Active Directory services.
- Domains make it possible to scale management from a few systems to hundreds across multiple offices.

### Explanation
- Managing a handful of computers manually is possible, but as organizations grow, it becomes inefficient to configure and troubleshoot each system individually. A Windows domain solves this by centralizing identity and policy management. Instead of having separate user accounts on every machine, accounts and policies are stored in Active Directory and enforced by the Domain Controller.
- This allows IT administrators to configure users, groups, and security policies once, and apply them across the network. It also enables features like:
- Centralized authentication (log into any domain-joined computer with the same credentials).
- Network-wide policies (e.g., restricting control panel access, enforcing password complexity).
- In real-world environments like schools, universities, or workplaces, when you log in with a username and password, the machine forwards authentication to Active Directory. This means your credentials don’t need to be stored locally, and access is managed centrally.

### Notes
- Windows Domain: Group of users and computers managed centrally with AD.
- Active Directory (AD): Central repository for managing identities and policies.
- Domain Controller (DC): Server that runs AD services.
**Advantages:**
- Centralized identity management.
- Security policies applied across the network.


## Active Directory

### Concepts Learned
- Active Directory Domain Services (AD DS) as the central catalogue for all network objects.
- Objects in AD: Users, Machines, Security Groups, Printers, Shares, etc.
- Security principals (users, machines, groups) that can authenticate and act on resources.
- Machine accounts and their naming scheme.
- Default and custom security groups in a domain.
- Organizational Units (OUs) for grouping and applying policies.
- Difference between Security Groups and OUs.
- Tools: Active Directory Users and Computers (ADUC) for managing objects.

### Explanation
- Active Directory is the heart of a Windows domain. AD DS provides a structured way to store, manage, and authenticate objects such as users, machines, and groups.
- Users: Represent either people (employees) or services (like IIS, MSSQL). Service accounts have limited rights, enough to run their respective services.
- Machines: Each computer joining the domain gets a machine object, which is also a security principal. Their accounts (e.g., DC01$) rotate long random passwords automatically.
- Security Groups: Collections of users/machines that simplify permission management. Groups can include other groups, making access control scalable.
- OUs: Container objects that organize users/machines, often by department. Policies are applied at the OU level, enforcing configurations on users within them.
- While OUs classify users/machines for policy enforcement, Groups manage permissions over resources like files and printers. A user can belong to many groups but only one OU.
- The ADUC tool provides a GUI to create, manage, and organize users, groups, and OUs. For example, at THM Inc., the AD structure mimics business departments (IT, Management, Marketing, R&D, Sales).

### Notes
- Security Principals: Any object that can authenticate and act on resources (users, machines, groups).
- Machine Accounts: Named <computername>$, auto-rotating passwords (~120 chars).
**Important Security Groups:**
- Domain Admins → Admin rights over the entire domain.
- Server Operators → Manage DCs without changing admin groups.
- Backup Operators → Access files bypassing permissions.
- Account Operators → Create/modify accounts.
- Domain Users → All user accounts.
- Domain Computers → All computers in domain.
- Domain Controllers → All DCs.
**Default Containers:**
- Builtin → Default groups.
- Computers → Default location for new machines.
- Domain Controllers → Holds DCs.
- Users → Default users/groups.
- Managed Service Accounts → Service-specific accounts.
**OU vs Groups:**
- OU = Policy application (one per user).
- Groups = Permissions to resources (many per user).
- Scalability for larger environments.
- Example: University logins → one username/password works on all lab computers.


## Managing Users in Active Directory

### Concepts Learned
- Understanding Organizational Units (OUs) and their role in AD.
- Protecting and deleting OUs (accidental deletion protection).
- Creating and deleting users to match organizational needs.
- Delegation in AD: granting specific permissions to non-admin users.
- Using RDP to connect with domain user accounts.
- Resetting passwords with delegated privileges via PowerShell.

### Explanation
- In AD, administrators can organize users into OUs for better management. OUs are protected against accidental deletion, but admins can disable this feature if removal is needed. Users can be created or removed to reflect organizational changes.
- Delegation allows administrators to give specific users limited control, such as resetting passwords within an OU, without giving them full domain admin rights. This reduces overhead and improves efficiency.
- In practice, RDP can be used to log in as delegated users. Even though delegated users don’t have access to AD management tools, they can still perform tasks like password resets using PowerShell. This provides secure and restricted administrative capabilities.

### Notes
**OU Deletion Protection**
- Default setting prevents accidental deletion.
- Can be disabled via Properties → Object tab.
**Delegation**
- Grants granular control (e.g., reset passwords).
- Example: Phillip (IT Support) delegated password reset control for Sales OU.
**PowerShell Commands**
*Resetting a password:*
- Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
**Forcing password change at next logon:**
- Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose
**RDP Usage**
- Login format: DOMAIN\username (e.g., THM\phillip).
- Used to connect as delegated users like Phillip or Sophie.


### Managing Computers in AD

#### Concepts Learned
- Default behavior: all machines (except DCs) join under the **Computers** container.  
- Best practice: segregate devices into dedicated OUs for better policy management.  
- Common categories of devices in AD:  
  - **Workstations** – used by end-users for daily tasks; no privileged accounts should log in here.  
  - **Servers** – provide services to users or other servers.  
  - **Domain Controllers** – manage the AD domain; most sensitive as they store all user password hashes.  
- Creating separate OUs for **Workstations** and **Servers** improves organization and policy application.  

#### Explanation
- When machines join the domain, they are automatically placed in the **Computers** container. This is not optimal since servers, workstations, and domain controllers require different security and usage policies.  

- To maintain structure, administrators should create **Organizational Units (OUs)** to separate machines by type or usage. *For example:*
   - Workstations OU → for employee computers and laptops.  
   - Servers OU → for infrastructure and service machines.  
   - Domain Controllers OU → automatically handled by Windows.  

- This logical grouping ensures policies can be applied consistently and securely across each type of device.  

#### Notes
- Moved devices from the default **Computers** container into their respective **Workstations** or **Servers** OUs.  
- Practiced creating OUs directly under `thm.local` domain.  
- This setup simplifies applying **Group Policies** to different machine types later.  


## Group Policy Objects (GPOs)

### Concepts Learned
- What GPOs are and how they work in Active Directory.
- How to configure and link GPOs to OUs.
- Difference between User and Computer configurations in GPOs.
- Default policies in AD (Default Domain Policy, RDP Policy, Default Domain Controllers Policy).
- Security filtering for targeted GPO application.
- SYSVOL share for GPO distribution.
- Practical examples of creating and applying custom GPOs:
- Restricting access to Control Panel for non-IT users.
- Auto-locking screens after 5 minutes of inactivity.

### Explanation
- Group Policy Objects (GPOs) are collections of settings applied to OUs within an Active Directory domain. They allow administrators to enforce consistent configurations and security baselines for users and computers. GPOs can contain User Configurations (settings for identities) and Computer Configurations (settings for machines).
- Default Domain Policy applies domain-wide, usually containing basic rules like password and lockout policies.
- Default Domain Controllers Policy applies only to Domain Controllers.
- GPOs can be linked to any OU, and their effects cascade down to sub-OUs.
- Administrators can configure settings using the Group Policy Management tool.
- GPO distribution is handled via the SYSVOL network share.
- By default, GPO changes take time to propagate, but admins can force sync using gpupdate /force.
- In practice, administrators create custom GPOs to enforce organizational rules, such as restricting access to system settings or enforcing inactivity timeouts.

### Notes
- Creating GPOs: First create under Group Policy Objects, then link to the OU.
- Security Filtering: By default applies to all authenticated users, but can be restricted to certain accounts.
- Editing GPOs: Access via Group Policy Management → Edit → navigate policies (e.g., password length, account lockout).
- SYSVOL Share: Located at C:\Windows\SYSVOL\sysvol\ on DCs; ensures GPOs replicate across the domain.
**Practical Hands-On (THM):**
- Created Restrict Control Panel Access GPO, linked to Marketing, Sales, and Management OUs.
- Created Auto Lock Screen GPO with 5-min inactivity timeout, applied at root domain level.
- Tested via RDP using Mark’s credentials → verified control panel restriction and auto lock.
**Important Command:**
 gpupdate /force
(forces GPO update on demand).


## Authentication Methods

### Concepts Learned
- Windows domains rely on Domain Controllers to store and verify credentials.
- Two authentication protocols exist: Kerberos (default, modern) and NetNTLM (legacy, compatibility).
- Kerberos uses tickets (TGT & TGS) for secure authentication.
- NetNTLM uses a challenge-response mechanism without transmitting passwords.

### Explanation
**Kerberos:**
- User sends encrypted credentials (username + timestamp) to the KDC (Key Distribution Center).
- KDC returns a Ticket Granting Ticket (TGT) + Session Key.
- When accessing services, the user requests a Ticket Granting Service (TGS) using the TGT.
- KDC issues a TGS encrypted with the Service Owner Hash, containing a Service Session Key.
- The service decrypts the TGS, validates the session key, and grants access.
**NetNTLM:**
- Authentication works with a challenge-response mechanism.
- Server sends a random challenge to the client.
- Client generates a response using their NTLM password hash + challenge.
- Server forwards this to the Domain Controller.
- DC recalculates and verifies the response.
- If valid, authentication succeeds.
- Password/hash is never directly sent over the network.

### Notes
- Kerberos is more secure and efficient (default in modern domains).
- Tickets (TGT & TGS) help reduce credential exposure by avoiding repeated password transmissions.
- TGT = proof of authentication, issued by KDC, encrypted with krbtgt hash.
- TGS = service-specific ticket, encrypted with the service account hash.
- NetNTLM still exists in networks for compatibility but is considered obsolete.
- Local accounts can authenticate via NetNTLM without contacting a Domain Controller (since SAM holds the password hash).


## Trees, Forests and Trusts

### Concepts Learned
- Single domain can become insufficient as organizations grow.
- Trees = multiple domains sharing the same namespace (e.g., uk.thm.local, us.thm.local).
- Forests = multiple trees with different namespaces (e.g., thm.local + mht.local).
- Enterprise Admins group manages across all domains in a forest.
- Trust relationships allow cross-domain or cross-forest access.
- Trusts can be one-way or two-way depending on direction of access.

### Explanation
- Single Domain: Easy to manage but limited when organizations expand.
**Trees:**
- Created when multiple domains share the same namespace.
- Example: thm.local root → subdomains uk.thm.local & us.thm.local.
- Each branch has its own Domain Controller (DC), admins, and policies.
- Local Domain Admins manage only their branch, while Enterprise Admins manage all.
**Forests:**
- Used when domains have different namespaces (e.g., THM acquiring MHT).
- A forest = collection of trees in a shared network.
- Allows different IT departments to manage independently but still be connected.
**Trust Relationships:**
- Enable resource access across domains/forests.
- One-way trust: Domain A trusts Domain B → users from B can access A’s resources (but not the reverse).
- Two-way trust: Mutual trust → both domains can authorise users across boundaries.
- By default, domains in a tree/forest establish two-way trusts.
- Trust only provides the possibility of cross-domain access; actual authorisation must be configured.

### Notes
- Trees = multiple domains under one namespace.
- Forests = multiple trees across different namespaces.
- Domain Admins control one domain; Enterprise Admins control the entire forest.
- Trusts can be one-way (direction matters) or two-way (mutual).
- Trust ≠ automatic access → permissions still need explicit authorisation.


## Key Takeaways
- Active Directory (AD) is the backbone of corporate environments, centralizing the management of users, devices, and resources.
- Domains are the fundamental building blocks of AD, managed by Domain Controllers (DCs).
- Organizational Units (OUs) allow logical grouping of users, groups, and devices for easier management and policy application.
- Computers in AD should be organized into categories (Workstations, Servers, Domain Controllers) to apply proper security policies.
- Authentication in AD mainly relies on Kerberos (default, ticket-based, secure) and NetNTLM (legacy, challenge-response).
- Trees group multiple domains under a shared namespace, while forests combine multiple trees across different namespaces.
- Enterprise Admins manage the entire forest, while Domain Admins are limited to their own domain.
- Trust relationships (one-way or two-way) enable controlled resource sharing across domains and forests.
- Proper design of AD structure (domains, OUs, forests, and trusts) is essential for scalability, security, and efficient administration.
