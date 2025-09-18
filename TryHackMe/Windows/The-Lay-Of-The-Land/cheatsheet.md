# Cheatsheet - Lay of the Land

| Category                  | Commands / Tools / Notes                                                                                  |
|----------------------------|----------------------------------------------------------------------------------------------------------|
| **Network Enumeration**    | `netstat -na` → List TCP/UDP connections and ports<br>`arp -a` → View ARP table<br>Check VLANs, DMZ, internal/external networks |
| **AD Environment**         | `systeminfo | findstr Domain` → Check domain membership<br>Domain Controllers, OUs, Users, Groups, Forests |
| **User & Group Enum**      | `Get-ADUser -Filter *` → List AD users<br>`Get-ADUser -Filter * -SearchBase "CN=Users,DC=domain,DC=com"`<br>Identify Domain Admins & Service Accounts |
| **Host Security Solutions**| Antivirus: `wmic /namespace:\\root\securitycenter2 path antivirusproduct`<br>Windows Defender: `Get-MpComputerStatus`<br>Firewall: `Get-NetFirewallProfile`<br>Sysmon: `Get-Process | Where-Object { $_.ProcessName -eq "Sysmon" }`<br>EDR/HIDS awareness |
| **Network Security**       | Firewalls (packet-filtering, proxy, NAT, WAF)<br>SIEM: log collection, alerts, dashboards<br>IDS/IPS: detect/prevent intrusions |
| **Applications & Services**| List apps: `wmic product get name,version`<br>List processes: `Get-Process`<br>Running services: `net start` / `wmic service`<br>Check ports: `netstat -noa`<br>DNS: `nslookup` and zone transfer |
| **File & Printer Shares**  | Enumerate shared resources using `Get-ChildItem -Hidden -Path <path>` and network share commands |
| **Internal Services**      | DNS, local web apps, email, file shares, databases → use for reconnaissance and lateral movement |

