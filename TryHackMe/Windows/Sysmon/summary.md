# Summary – Sysmon

**This room focused on using Sysmon and Windows Event Logs to monitor, hunt, and investigate suspicious activity on endpoints.**

- Understanding Sysmon installation and configuration, including the use of SwiftOnSecurity and ION-Storm config files to reduce noise and capture high-quality events.  
- Learning how to filter and monitor events in Event Viewer and via PowerShell for granular control over logs.  
- Detecting malicious activity by focusing on meaningful events and applying best practices like exclude > include and environment awareness.  
- Detecting Mimikatz by hunting for abnormal LSASS access and suspicious file creation events while filtering out safe processes.  
- Hunting malware such as RATs and backdoors by monitoring network connections, suspicious ports, and filtering known safe applications.  
- Identifying persistence mechanisms through startup folder modifications and registry key changes, using Sysmon EventIDs for FileCreate and RegistryEvent.  
- Detecting evasion techniques like Alternate Data Streams and Remote Thread creation to uncover hidden files and DLL injection attempts.  
- Performing practical investigations using EVTX samples to analyze malicious USB activity, payloads masquerading as HTML files, persistence setups, and C2 communications.  
- Gaining skills in correlating event logs, processes, registry keys, file paths, and network ports to conduct endpoint investigations.  
- Key takeaways include the importance of well-configured Sysmon, using PowerShell for filtering, reducing log noise while capturing critical events, and knowing normal system behavior for anomaly detection.

