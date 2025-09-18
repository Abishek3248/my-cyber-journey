# Lay Of The Land

## Introduction
- In real-world red team engagements, it’s crucial to understand the environment after gaining initial access to a compromised machine. Reconnaissance and enumeration help gather information that guides the next stages of an attack.

## Network Infrastructure

### Concepts Learned
- Importance of enumeration after gaining initial access.
- Network segmentation and VLANs.
- Internal networks and their purpose.
- DMZ as an edge security layer.
- Basics of network enumeration (ports, routing, ARP).
- Role of internal network services.

### Explanation
- Enumeration helps identify where we are, what services exist, and the type of network.
- Network segmentation improves security by dividing networks into subnets.
- VLANs are used for segmentation, controlling broadcasts, and isolating hosts.
- Internal networks are segmented for data sensitivity, collaboration, and security.
- DMZ provides controlled access for public-facing services while protecting internal systems.
- Network enumeration uses commands like netstat and arp to discover connections, open ports, and devices.
- Internal services (DNS, web, custom apps) are accessible once inside the network.

### Notes
- Network segmentation → prevents unauthorized access to sensitive assets.
- VLANs → isolate hosts, improve security.
- Internal networks → used for collaboration, operational systems, internal services.
- DMZ → separates untrusted internet traffic from internal LAN.
- netstat -na → view open TCP/UDP ports and connections.
- arp -a → view IP/MAC addresses of communicating devices.


## Active Directory Environment

### Concepts Learned
- Role of Active Directory in centralized management.
- Key AD components (Domain Controllers, OUs, Objects, Domains, Forests, Service Accounts).
- Importance of AD enumeration after initial access.
- Checking if a machine is part of an AD environment.

### Explanation
- Active Directory stores and manages objects (users, computers, groups, printers, etc.) and provides authentication and authorization in a corporate network.
- A Domain Controller (DC) manages users, groups, and policies; attackers target it due to the high-value information it stores.
- Organizational Units (OUs) provide a hierarchical structure for grouping and managing AD objects.
- AD Objects include users, computers, and GPOs.
- Domains are collections of AD components; Forests are multiple domains that trust each other.
- Service Accounts (local users, domain users, managed service accounts) are used to run services and processes.
- Enumeration of AD helps attackers map users, groups, and permissions for lateral movement.
- To verify AD membership, the systeminfo command reveals domain details.

### Notes
- AD → centralized authentication, authorization, and object management.
- Domain Controller → critical target; controls access, encryption, and policies.
- OUs → containers for organizing objects hierarchically.
- Objects → users, computers, printers, GPOs.
- Domains → building blocks of AD; Forests → collection of trusting domains.
- Service Accounts → special accounts for services.
- Enumeration of AD = key step for lateral movement.
- systeminfo | findstr Domain → check if machine is part of AD (shows domain name).
- If output = WORKGROUP → machine is not part of AD.


## Users And Groups Management In AD

### Concepts Learned
- Importance of account discovery after initial access.
- Different account types in AD (local, domain, managed service, privileged accounts).
- Key administrator groups in AD.
- Enumerating users and groups with PowerShell.
- Use of Distinguished Name (DN) and LDAP hierarchy in enumeration.

### Explanation
- Enumeration of users and groups helps understand available accounts, permissions, and potential escalation paths.
**Types of accounts in AD:**
   - Local accounts → manage only the local system.
   - Domain user accounts → managed by AD; access AD services.
   - Managed service accounts → special accounts with higher privileges to run services.
   - Domain Administrators → full control over AD environment (prime red team target).
**Key AD administrator groups include:**
   - BUILTIN\Administrator → local admin on DC.
   - Domain Admins → access to all resources in domain.
   - Enterprise Admins → only in forest root.
   - Schema Admins → modify domain/forest.
   - Server Operators → manage domain servers.
   - Account Operators → manage non-privileged users.
**PowerShell Enumeration:**
   - Get-ADUser -Filter * → list all AD users.
   - Get-ADUser -Filter * -SearchBase "CN=Users,DC=THMREDTEAM,DC=COM" → list users from a specific container.
   - Distinguished Name (DN) identifies objects in AD using CN (Common Name), OU (Organizational Unit), and DC (Domain Component).

### Notes
-  Account discovery = first step post-compromise.
- Local users → not part of AD.
- Domain users → authenticate with AD, access AD services.
- Managed service accounts → higher privileges for services.
- Domain Administrators → full AD control.
**Important AD admin groups:**
   - Domain Admins, Enterprise Admins, Schema Admins, Server Operators, Account Operators.
**PowerShell commands:**
   - Get-ADUser -Filter * → all users.
   - Get-ADUser -Filter * -SearchBase "CN=Users,DC=THMREDTEAM,DC=COM" → filter by container.
   - DN = unique identifier in AD; built from CN, OU, and DC.
 

## Host Security Solution #1

### Concepts Learned
- Importance of enumerating host-based security solutions after initial access.
- Antivirus software and detection methods (signature, heuristic, behavior-based).
- Windows Defender protection modes and status checks.
- Role and enumeration of host-based firewalls.
- Using PowerShell for AV and firewall discovery.

### Explanation
- Host security solutions include:
- Antivirus software (third-party AV, Windows Defender).
- Host-based firewall.
- Event logging/monitoring, HIDS/HIPS, EDR.
**Antivirus detects threats using:**
- Signature-based → matches known malware.
- Heuristic-based → analyzes suspicious code or API use.
- Behavior-based → monitors abnormal runtime activity.
**Windows Defender:**
- Active mode (primary AV).
- Passive mode (secondary when 3rd-party AV present).
- Disabled mode.
- Status checked via Get-Service WinDefend or Get-MpComputerStatus.
**Host-based firewall:**
- Controls inbound/outbound traffic.
- Can block ICMP, ports, or app-layer traffic.
- Enumerated with Get-NetFirewallProfile and Get-NetFirewallRule.
- Connectivity tested with Test-NetConnection or TcpClient.
- Enumerating host security is critical for staying undetected and planning next steps.
**Hands-on:** checked Defender alerts, firewall status, and specific rules (THM-Connection rule).

### Notes
- AV software → prevents malicious code execution.
- Detection methods: signature / heuristic / behavior-based.
**Enumerate AV with:**
- wmic /namespace:\\root\securitycenter2 path antivirusproduct
- Get-CimInstance -Namespace root/SecurityCenter2 -ClassName AntivirusProduct
**Windows Defender:**
- Check status → Get-Service WinDefend
- Check protections → Get-MpComputerStatus
- Detected threats → Get-MpThreat
**Firewall:**
- Profiles → Get-NetFirewallProfile
- Rules → Get-NetFirewallRule
- Disable (if admin) → Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled False
- Connectivity test → Test-NetConnection -ComputerName <target> -Port <port>
**Hands-on results:**
- Host-based firewall → Disabled (N).
- Defender alert → caused by PowerView.ps1.
- Firewall rule THM-Connection → allowed a specific port.


## Host Security Solution #2

### Concepts Learned
- Security Event Logging and Monitoring
- System Monitor (Sysmon)
- Host-based Intrusion Detection/Prevention System (HIDS/HIPS)
- Endpoint Detection and Response (EDR)

### Explanation
**Security Event Logging and Monitoring**
- Operating systems (like Windows) log activity into different categories (application, system, security, services, etc.).
- Logs help admins monitor, investigate, and respond to incidents.
- Get-EventLog -List in PowerShell shows all logs and can reveal installed services (e.g., AD, DNS).
- Corporate environments often centralize logs using agents for better monitoring.
**System Monitor (Sysmon)**
- Part of Microsoft Sysinternals, not default but widely used.
- Logs detailed events like process creation, network connections, file modifications, and memory access.
- Detection: look for Sysmon processes, services, or registry keys.
- If configuration files are accessible, attackers can see what defenders are monitoring.
**HIDS/HIPS**
- HIDS: Host-based Intrusion Detection System. Detects suspicious activities but doesn’t block them. Uses signature-based and anomaly-based methods.
- HIPS: Host-based Intrusion Prevention System. Detects and blocks malicious activity. Can audit logs, monitor processes, and protect system resources.
**Endpoint Detection and Response (EDR)**
- Next-gen solution beyond AV and HIDS/HIPS.
- Detects malware, ransomware, exploit chains, and abnormal behaviors.
- Popular tools: Cylance, Crowdstrike, Symantec, SentinelOne.
- Even if attackers bypass it initially, EDR continues to monitor and may stop later actions.
- Enumeration scripts like Invoke-EDRChecker and SharpEDRChecker can reveal installed security tools.

### Notes
- Event logs can unintentionally reveal valuable details (installed services, AD roles, etc.).
- Sysmon provides detailed visibility for defenders, making stealth important for attackers.
- HIDS = detection only, HIPS = detection + prevention.
- EDR combines multiple layers of protection and is harder to evade than traditional AV.
- Enumeration of security products is critical before taking action in red team ops.


## Network Security Solution

### Concepts Learned
- Network Firewall
- Security Information and Event Management (SIEM)
- Intrusion Detection/Prevention System (NIDS/NIPS)

### Explanation
**Network Firewall**
- Acts as the first checkpoint for untrusted traffic entering a network.
- Filters traffic based on defined rules/policies before it reaches internal systems.
- Can separate external, internal, or application-specific traffic.
**Types include:**
- Packet-filtering firewalls
- Proxy firewalls
- NAT firewalls
- Web application firewalls
- Security Information and Event Management (SIEM)
   - Combines SIM + SEM for real-time monitoring and analysis of logs/events.
   - Collects log files from different sensors across the enterprise.
**Functions:**
- Log management (real-time data capture)
- Event analytics (detect anomalies, visualize in dashboards)
- Incident monitoring & alerts (detects attacks and alerts admins)
- Compliance & reporting (generates reports anytime)
- Can detect insider threats, phishing, DDoS, web attacks, vulnerabilities, etc.
- Common products: Splunk, LogRhythm, SolarWinds, Datadog.
**Intrusion Detection & Prevention System (IDS/IPS)**
- IDS = monitors packets, flags suspicious activity → requires manual/3rd party action.
- IPS = actively blocks/rejects malicious packets automatically based on rules.
- Operates at the network level, analyzing packets via sensors/agents.
- Common solutions: Palo Alto Networks, Cisco NGIPS, McAfee NSP, Trend Micro TippingPoint, Suricata.
### Notes
- Firewalls = traffic filtering + access control at the network boundary.
- SIEM = central hub for collecting, analyzing, and alerting based on logs.
- IDS = detection only, IPS = detection + prevention.
- Enterprises often deploy multiple solutions together (Firewall + SIEM + IDS/IPS).


## Application And Services

### Concepts Learned
- Installed applications enumeration
- Services and processes reconnaissance
- File and printer sharing enumeration
- Internal services (DNS, web apps, databases) discovery

### Explanation
**Installed Applications:**
- Enumerating installed software helps identify outdated or vulnerable applications that can be exploited. Tools like wmic product get name,version and PowerShell Get-ChildItem are useful for checking applications, hidden files, and directories.
**Services and Processes:**
- Windows services may be misconfigured, leading to privilege escalation. Process discovery provides insight into custom or internal software that may expose vulnerabilities. Enumeration can be done with net start, wmic service, and Get-Process.
**File and Printer Sharing:**
- Misconfigured file shares and printers can reveal sensitive information, credentials, or lateral movement opportunities.
**Internal Services:**
- DNS, email, web apps, file shares, and databases are common internal services. Discovering and enumerating them provides insight into the broader environment. Zone transfers using nslookup can leak valuable records.

### Notes
**Installed Applications**
- wmic product get name,version
- Get-ChildItem -Hidden -Path C:\Users\kkidd\Desktop\
**Service Enumeration**
- net start
- wmic service where "name like 'THM Demo'" get Name,PathName
- Get-Process -Name thm-demo
- netstat -noa |findstr "LISTENING" |findstr "3212"
- Found THM Demo service → running as c:\Windows\thm-demo.exe
- Listening on port 13337
- Visiting localhost:13337 revealed flag: THM{S3rv1cs_1s_3numerat37ed}
**DNS Enumeration**
    "nslookup.exe
    > server 10.201.37.76
    > ls -d thmredteam.com"
- Successfully performed a DNS zone transfer
- Discovered domain controller: ad.thmredteam.com


## Key Takeaways
- Reconnaissance and enumeration are the foundation of post-exploitation.
- Learned how to discover users, groups, and AD accounts with PowerShell.
- Understood host security solutions (AV, Defender, firewalls, Sysmon, HIDS/HIPS, EDR) and how to detect/enumerate them.
- Covered network security solutions (firewalls, SIEM, IDS/IPS) and their role in monitoring and detection.
- Practiced enumerating applications, services, processes, shares, and internal services like DNS and web apps.
- Hands-on enumeration revealed running services (THM Demo), listening ports, DNS zone transfer, and flags.
- Core idea: staying stealthy while gathering as much environment information as possible for lateral movement and privilege escalation.
