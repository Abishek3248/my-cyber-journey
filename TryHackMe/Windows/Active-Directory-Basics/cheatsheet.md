# Windows Domain & Active Directory – Quicklook Cheatsheet  

| **Concept / Command**     | **Description**                                                                 |
|----------------------------|---------------------------------------------------------------------------------|
| **Domain**                | Centralized network environment managed by Domain Controllers (DCs).            |
| **Domain Controller (DC)**| Server that authenticates users/computers and manages security in the domain.    |
| **Organizational Unit (OU)** | Logical container for users, groups, and computers; allows policy management.   |
| **Workstations**          | User PCs; should never run privileged accounts.                                 |
| **Servers**               | Provide services to users or other servers in the domain.                       |
| **Domain Controllers**    | Most sensitive machines; store hashed passwords and AD data.                     |
| **Kerberos**              | Default authentication protocol (ticket-based, uses TGT & TGS).                 |
| **NetNTLM**               | Legacy authentication (challenge-response).                                     |
| **Group Policy Object (GPO)** | Collection of settings applied to OUs; can target users or computers.            |
| **SYSVOL**                | Network share used to distribute GPOs across domain machines.                    |
| **Trees**                 | Multiple domains sharing the same namespace (e.g., uk.thm.local, us.thm.local). |
| **Forests**               | Collection of trees with different namespaces (e.g., thm.local + mht.local).   |
| **Trust Relationships**   | Allow cross-domain access; can be one-way (directional) or two-way (mutual).    |
| **Enterprise Admins**     | Security group with admin rights across all domains in the forest.              |
| `gpupdate /force`         | Force update of Group Policy Objects (GPOs) immediately.                        |
| `Get-ADUser -Filter *`    | List all users in Active Directory (PowerShell).                                |
| `Get-ADComputer -Filter *`| List all computers in Active Directory (PowerShell).                            |
| `Get-ADGroup -Filter *`   | List all groups in Active Directory (PowerShell).                               |
| `dsquery user`            | Query domain users from command line.                                           |
| `net user /domain`        | Show all domain users.                                                          |
| `net group /domain`       | Show all domain groups.                                                         |
| `nltest /dclist:<domain>` | List all Domain Controllers in a given domain.                                  |
| `echo %logonserver%`      | Display the Domain Controller that authenticated your session.                  |
| `whoami /groups`          | Display current user’s group memberships.                                       |

