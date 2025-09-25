# Sysmon

## Introduction
- Sysmon (System Monitor) is a Windows system service and driver from the Sysinternals suite that provides detailed event logging for security monitoring and incident response. While similar to Windows Event Logs, Sysmon offers far more granular visibility into system activities, such as process creation, network connections, file modifications, and registry changes.
-  Enterprises often deploy Sysmon as part of their security stack to enhance detection capabilities and build a richer audit trail for threat hunting and forensic investigations.


## Overview

### Concepts Learned
- Sysmon is part of the Windows Sysinternals suite, providing advanced logging beyond standard Windows Event Logs.
- Sysmon relies on configuration files to filter events (exclude/include rules).
- Important Sysmon Event IDs to monitor include: process creation, network connections, DLL loads, code injection, file creation, registry changes, alternate data streams, and DNS queries.

### Explanation
- Sysmon (System Monitor) is a Windows service and driver that runs in the background and logs detailed system activity. Unlike normal Windows Event Logs, Sysmon provides more granular insights, useful for detecting malware, persistence, or anomalous behavior.
**Logs Location:**
  - Applications and Services Logs/Microsoft/Windows/Sysmon/Operational.
**Configuration:**
  - Sysmon uses XML-based config files to control what is logged.
  - Common configs: SwiftOnSecurity’s sysmon-config (focuses on excluding normal noise) and ION-Storm’s fork (more proactive, includes rules).
  - Config tuning is critical to balance visibility and performance.
**Notable Event IDs:**
  1 – Process Creation → Identifies suspicious or abnormal commands.
  3 – Network Connection → Logs outbound connections, useful for detecting C2 traffic.
  7 – Image Loaded → Detects DLL injection/hijacking (can be noisy).
  8 – CreateRemoteThread → Detects process injection, common with Cobalt Strike or Meterpreter.
  11 – File Created → Captures new files (useful for ransomware or malware drops).
  12/13/14 – Registry Events → Persistence or credential manipulation attempts.
  15 – FileCreateStreamHash → Monitors alternate data streams, often abused for hiding malicious payloads.
  22 – DNS Queries → Captures DNS lookups; useful for spotting suspicious domains.

### Notes
- Sysmon provides 29 total Event IDs, but SOC teams prioritize high-value ones (1, 3, 7, 8, 11, 12–14, 15, 22).
- DNS logging is useful but generates lots of noise — filtering trusted domains is necessary.


## Installing and Preparing Sysmon

### Concepts Learned
- Sysmon installation requires downloading the binary from Microsoft Sysinternals.
- It can be installed as a standalone tool or as part of the full Sysinternals Suite.
- A configuration file is necessary for meaningful logging and filtering.
- Sysmon is installed and started from the command line with administrator privileges.
- Logs are stored under Applications and Services Logs → Microsoft → Windows → Sysmon → Operational.

### Explanation
- Installing Sysmon is a straightforward process. The binary can be downloaded directly or as part of the entire Sysinternals Suite. There’s also an option to grab all the tools at once using PowerShell.
- Sysmon works best when paired with a configuration file. These XML-based configs define what activity should be logged and how noise should be filtered out. Two popular community configs are SwiftOnSecurity, which aims to reduce noise and keep logs focused, and ION-Storm, which uses more proactive inclusion rules.
- To install, open PowerShell or Command Prompt as an Administrator and run:
  Sysmon.exe -accepteula -i ..\Configurations\swift.xml
- This installs Sysmon, accepts the license agreement, and applies the chosen configuration. Once installed, Sysmon immediately begins logging activity. The logs can be reviewed in Event Viewer under the Sysmon Operational log.
- Configurations can be changed at any time without uninstalling Sysmon by simply updating the config file and reloading it.

### Notes
- Sysmon installs both a service and a driver (SysmonDrv).
- During setup, the configuration file is validated against the current schema.
- Without a config, logs are extremely noisy. Using a config is essential to filter out normal system behavior and focus on suspicious activity.
- Logs are located in Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational.
- Updating a config can be done with Sysmon.exe -c new_config.xml.
- To uninstall Sysmon, use Sysmon.exe -u.
- Event ID 7 (Image Loaded) can impact performance; use cautiously.
- Sysmon starts logging early in the boot process, making it more reliable for tracking initial malware execution.


## Cutting Out The Noise

### Concepts Learned
- Importance of filtering out noise in Sysmon logs to focus on suspicious activity.
- Common malicious behaviors detectable with Sysmon (e.g., ransomware, persistence, Mimikatz, Metasploit, C2 beacons).
- Best practices for creating and tuning Sysmon configurations.
- Methods for filtering Sysmon logs with Event Viewer, PowerShell, and CLI tools.

### Explanation
- Sysmon produces a large number of logs, but most of them represent normal activity. By excluding routine events (“noise”), analysts can focus on anomalies and malicious activity. This filtering makes it easier to detect threats like ransomware, persistence mechanisms, credential dumping (Mimikatz), exploitation tools (Metasploit), and command-and-control (C2) traffic.
- To effectively use Sysmon, good configuration is key. Rules typically exclude normal activity rather than include specific events—this prevents missing something important while keeping logs manageable. The command line interface (CLI) provides greater control for filtering and analysis compared to Event Viewer’s limited GUI options.
**Filtering can be done in several ways:**
 - Event Viewer → Filter by EventID, keywords, or custom XML (basic, but limited).
 - PowerShell (Get-WinEvent + XPath) → Provides powerful filtering using XML attributes and event data.
 - wevtutil.exe → Command-line tool for querying logs directly.
- Knowing your environment is essential before deploying Sysmon rules, since what counts as “normal” varies across organizations.

### Notes
**Best Practices:**
- Favor exclude rules over include rules.
- Use CLI (Get-WinEvent / wevtutil.exe) for advanced filtering.
- Tailor Sysmon configs to the environment to avoid alert fatigue.
**Filtering Examples:**
- By EventID → */System/EventID=<ID>
- By XML attribute → */EventData/Data[@Name="<Attribute>"]
- By Event Data → */EventData/Data=<Data>
**PowerShell Example:**
Get-WinEvent -Path <PathToLog> -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort"] and */EventData/Data=4444'
- (Filters for Sysmon network connections on port 4444, often linked to Metasploit.)


## Detecting Mimikatz

### Concepts Learned
- Techniques for detecting Mimikatz and credential dumping activity using Sysmon.
- Monitoring file creation and abnormal LSASS behavior to detect suspicious activity.
- Filtering out normal processes to reduce noise for efficient hunting.
- Using PowerShell to query Sysmon logs with granular filters.

### Explanation
- Mimikatz is a well-known post-exploitation tool mainly used for dumping credentials from memory (e.g., LSASS). While Anti-Virus often detects it, obfuscation or droppers may allow it to bypass detection.
-  Sysmon allows hunting for Mimikatz by detecting suspicious file creations, monitoring LSASS access by unusual processes, and filtering out benign activities.  - Using a well-crafted configuration file alongside PowerShell queries enables efficient identification of anomalies.

### Notes
- Focus on hunting for mimikatz-related binaries and abnormal LSASS behavior.
- Exclude normal processes like svchost.exe to reduce event log noise.
- PowerShell’s Get-WinEvent with XPath queries can help filter for suspicious events.
- Open the provided log Hunting_LSASS.evtx to observe Mimikatz activity and validate hunting methods.


## Hunting Metasploit

### Concepts Learned
- Techniques to hunt for malware using Sysmon, focusing on RATs and backdoors.
- Hypothesis-based hunting: defining what to monitor before actively hunting.
- Monitoring network connections for suspicious open ports.
- Importance of carefully excluding normal events to avoid missing malicious activity.

### Explanation
- Malware comes in many forms, with RATs (Remote Access Trojans) and backdoors being common threats.
- RATs typically use client-server architecture, anti-detection techniques, and provide easy-to-use interfaces.
- Hunting malware effectively involves knowing which malware to look for and configuring Sysmon to highlight suspicious events while filtering out normal activity
- Monitoring for abnormal open ports, unusual network connections, and using configuration files for detection are key methods in this process.
-  PowerShell and XPath queries can be used to refine searches and reduce noise.

### Notes
- Focus on detecting RATs or backdoors by monitoring specific network ports.
- Use hypothesis-based hunting to decide which events or ports to monitor.
- Be cautious with exclusions in configuration files—malware may exploit commonly excluded ports (e.g., port 53).
- Validate hunting techniques by opening provided logs (Hunting_Rats.evtx) to see real RAT activity.
- PowerShell filtering allows granular inspection of network connection events and destination ports.


## Hunting Persistance

### Concepts Learned
- Techniques attackers use to maintain persistent access on a compromised machine.
- Monitoring for persistence through registry modifications and startup scripts.
- Filtering Sysmon events to focus on anomalies while reducing noise.

### Explanation
- Persistence Overview: Attackers maintain access after compromise using various techniques.
- Startup Scripts: Adding malicious files to \Startup\ or \Start Menu\ directories ensures execution on user login.
- Registry Modifications: Changes to registry keys like HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run or Group Policy scripts allow malware to execute on system startup.
- Sysmon Monitoring: File Creation and Registry Modification events can be logged and filtered to detect persistence.
- Configuration Files: Using configs like SwiftOnSecurity’s allows filtering by Rule Names (T1023 for startup, T1060 for registry) to reduce noise.
- Investigation: Identify anomalies by checking both the file path and corresponding registry key to confirm malicious activity.
- Event Logs: Use Event Viewer to analyze logs such as T1023.evtx and T1060.evtx.

### Notes
- Startup Persistence: Investigate any suspicious files placed in startup directories.
- Registry Key Persistence: Monitor changes in critical registry paths that allow automatic execution.
- Filtering by Rule Name: Helps to quickly locate relevant events and reduces irrelevant noise.
- Real Investigation: Requires checking both the modified registry key and the associated file.


## Detecting Evasion Technique

### Concepts Learned
- Evasion techniques used by attackers to bypass security monitoring.
- Alternate Data Streams (ADS) and Remote Thread creation as common evasion methods.
- Using Sysmon Event IDs to detect stealthy malware activity.
- Filtering events to reduce noise and focus on suspicious behavior.

### Explanation
**Evasion Overview:**
- Malware authors use various techniques to avoid detection, such as ADS, injections, masquerading, packing, obfuscation, and anti-reversing techniques.
**Alternate Data Streams (ADS):**
- Allows files to be hidden from normal inspection by storing data in non-default NTFS streams.
- Sysmon Event ID 15 detects file creation or access in alternate streams.
- Investigators can identify suspicious files and their content for further analysis.
**Remote Thread Creation / DLL Injection:**
- Adversaries can inject code into other processes using Windows API functions like CreateRemoteThread.
- Sysmon Event ID 8 logs these events and helps detect techniques such as reflective PE injection or process hollowing.
- Filtering out legitimate system threads reduces noise.
**PowerShell Hunting:**
- Get-WinEvent with XPath queries can filter for Event IDs related to ADS (15) or Remote Threads (8).
- Configuration files handle most heavy filtering; PowerShell refines searches further.

### Notes
- ADS Detection: Look for unusual file storage in Temp, Downloads, or using .hta/.bat extensions.
- Remote Thread Detection: Identify processes creating threads in other processes; suspicious if unexpected parent-child relationships occur.
- Reducing Noise: Exclude known safe processes (like svchost.exe or Chrome) when monitoring Event ID 8.
**Investigation Steps:**
- Open relevant event logs from Practice folder to analyze potential evasion.
- Verify file locations and hashes if ADS is detected.
- Correlate remote thread creation with process behavior to confirm malicious activity.


# Practical Investigation

## Concepts Learned
- Hands-on application of Sysmon event logs for real-world attacks.  
- Identifying malicious USB activity, masked payloads, persistence, and C2 communications.  
- Using event logs to track processes, registry modifications, and network connections.  
- Applying investigative techniques to correlate Sysmon logs with MITRE ATT&CK tactics.  

## Explanation / Notes

### Investigation 1 – Malicious USB (BILL THAT'S THE WRONG USB!)
- **Goal:** Detect malicious file dropped via USB.  
- **Key Findings:**  
  - USB device registry key:  
    `HKLM\System\CurrentControlSet\Enum\WpdBusEnumRoot\UMB\2&37c186b&0&STORAGE#VOLUME#_??_USBSTOR#DISK&VEN_SANDISK&PROD_U3_CRUZER_MICRO&REV_8.01#4054910EF19005B3&0#\FriendlyName`  
  - Device name accessed by RawAccessRead: `\Device\HarddiskVolume3`  
  - First executed process: `rundll32.exe`  

### Investigation 2 – Masked HTML Payload (This isn't an HTML file?)
- **Goal:** Detect malicious file masquerading as HTML.  
- **Key Findings:**  
  - Payload path: `C:\Users\IEUser\AppData\Local\Microsoft\Windows\Temporary Internet Files\Content.IE5\S97WTYG7\update.hta`  
  - Masked file path: `C:\Users\IEUser\Downloads\update.html`  
  - Signed binary executing payload: `C:\Windows\System32\mshta.exe`  
  - Adversary IP: `10.0.2.18`  
  - Back connect port: `4443`  

### Investigation 3.1 – Persistence Setup (Where's the bouncer when you need him)
- **Goal:** Identify how adversary gained persistence.  
- **Key Findings:**  
  - Adversary IP: `172.30.1.253`  
  - Endpoint hostname: `DESKTOP-O153T4R`  
  - C2 server hostname: `empirec2`  
  - Registry location for payload: `HKLM\SOFTWARE\Microsoft\Network\debug`  
  - PowerShell launch code:  
    ```
    "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -c "$x=$((gp HKLM:Software\Microsoft\Network debug).debug);start -Win Hidden -A \"-enc $x\" powershell";exit;
    ```  

### Investigation 3.2 – Scheduled Task Persistence
- **Goal:** Detect scheduled task used to maintain access.  
- **Key Findings:**  
  - Adversary IP: `172.168.103.188`  
  - Payload path: `c:\users\q\AppData:blah.txt`  
  - Scheduled task command:  
    ```
    "C:\WINDOWS\system32\schtasks.exe" /Create /F /SC DAILY /ST 09:00 /TN Updater /TR "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -NonI -W hidden -c \"IEX ([Text.Encoding]::UNICODE.GetString([Convert]::FromBase64String($(cmd /c ''more < c:\users\q\AppData:blah.txt'''))))\""
    ```  
  - Process accessed by schtasks.exe (suspicious): `lsass.exe`  

### Investigation 4 – C2 Communications (Mom look! I built a botnet!)
- **Goal:** Detect C2 activity on endpoints.  
- **Key Findings:**  
  - Adversary IP: `172.30.1.253`  
  - C2 port: `80`  
  - C2 tool used: `Empire`  


## Key Takeaways
- Sysmon provides **granular logging** of Windows events, enabling detection of malware, persistence, evasion, and other suspicious activity.  
- **Installation and configuration:** Using a well-built Sysmon configuration file (like SwiftOnSecurity or ION-Storm) is crucial to minimize noise and focus on meaningful events.  
- **Malware detection:** Hunt RATs, backdoors, and Metasploit payloads by monitoring file creations, network connections, and suspicious ports.  
- **Credential theft detection:** Mimikatz and LSASS access can be detected via process access events (Event ID 10). Filtering by abnormal processes reduces log noise.  
- **Persistence tracking:** Monitor startup folders, registry keys, and scheduled tasks to detect attackers maintaining access.  
- **Evasion techniques:** Alternate Data Streams (Event ID 15) and remote threads (Event ID 8) allow detection of stealth techniques like DLL injection and process hollowing.  
- **Practical investigations:** Real-world scenarios reinforce event correlation, registry and file path analysis, and network monitoring.  
- **Best practices:**  
  - **Exclude before include** in configuration files to minimize irrelevant events.  
  - Use **PowerShell and CLI tools** (Get-WinEvent, wevutil.exe) for precise filtering.  
  - Understand your **environment** before deploying detection rules.  
- Effective Sysmon deployment requires a combination of **well-configured rules, real-time monitoring, and manual investigation skills** to detect advanced threats.

