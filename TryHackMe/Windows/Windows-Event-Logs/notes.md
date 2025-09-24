# Windows-Event-Logs

## Introduction
- Event logs track system activities, providing an audit trail for understanding behavior and diagnosing issues. They are especially useful in complex environments or applications with minimal user interaction, such as servers. By default, the operating system writes messages to these logs, which can be queried when troubleshooting problems.
- For defenders, event logs also help correlate entries from multiple sources, revealing patterns between seemingly unrelated events. This is where SIEMs like Splunk -and Elastic come in, enabling centralized monitoring, threat detection, investigation, and faster response times across large environments.
- While logs can be accessed on individual machines, SIEMs allow querying across multiple endpoints efficiently.
- Although other operating systems such as Linux and macOS have logging systems (e.g., Syslog on Linux), this room focuses specifically on Windows Event Logs.


## Event Viewer

### Concepts Learned
- Windows Event Logs are stored in a proprietary binary format (.evt or .evtx) and can be translated into XML via the Windows API.
- Logs reside in C:\Windows\System32\winevt\Logs.
- Logs are categorized by purpose: System, Security, Application, Directory Service, File Replication Service, DNS, and Custom Logs.
- Event logs can be accessed via Event Viewer (GUI), wevtutil.exe (CLI), or PowerShell (Get-WinEvent).

### Explanation
 **The Event Viewer is a Microsoft Management Console (MMC) snap-in that allows users to view and analyze Windows Event Logs. It provides a GUI with three main panes:**
- Left Pane – Hierarchical tree of log providers.
- Middle Pane – Overview and summary of events for the selected provider, with detailed columns:
- Level: Type of event (Information, Warning, Error).
- Date and Time: When the event was logged.
- Source: The software or service generating the event.
- Event ID: Numerical identifier for the event.
- Task Category: Defines the category of the event for filtering purposes.
- Right Pane (Actions) – Options to interact with logs, including opening saved logs, creating custom views, and filtering current logs.
- Event Viewer allows inspection of detailed logs, including General and Details views, with XML available for deeper analysis. Log rotation settings define maximum log size and overwrite policies. Security-conscious analysts should note that clearing logs can be legitimate maintenance but is also a tactic used by adversaries to avoid detection.

### Notes
- Standard logs are visible under Windows Logs, while Applications and Services Logs include logs like Microsoft > Windows > PowerShell > Operational.
- Properties for each log show location, size, creation/modification dates, and rotation settings.
- Filtering and creating custom views help isolate specific events, such as filtering only Event ID 4104 in PowerShell logs.
- Remote Event Viewer connections are possible via Connect to Another Computer…, enabling centralized log analysis.
- Always ensure the virtual machine is fully deployed before starting the room; allow about 3 minutes to load.


## Wevtutil

### Concepts Learned
- wevtutil is a command-line tool for managing and querying Windows event logs.
- It supports filtering, formatting, and retrieving logs directly from the terminal.

### Explanation
- Using wevtutil, you can pull logs from categories like Application, System, or Security without opening the Event Viewer GUI.
**For example:**
- /c:3 → limits output to 3 events.
- /rd:true → shows results in reverse chronological order.
- /f:text → formats output as text.
- This is useful for incident response and scripting since it provides flexible access to logs.

### Notes
- Commands will be stored separately in a cheatsheet.md for quick reference instead of cluttering the notes.
- Key Takeaways: wevtutil makes log retrieval faster, scriptable, and less resource-heavy compared to the GUI.


## Get-WinEvent

### Concepts Learned
- Get-WinEvent is a PowerShell cmdlet for retrieving events from event logs and event tracing log files, both locally and remotely.
- Supports advanced filtering with XPath, XML, and hash tables.
- Replaces the older Get-EventLog cmdlet.
  
### Explanation
- Get-WinEvent provides flexible and efficient ways to query event logs. It can combine multiple sources into a single query and filter directly at the source, which is faster than post-processing with Where-Object.

### Notes
- Use -FilterHashtable for efficient event log filtering.
- Hash tables follow the syntax: @{ <name> = <value>; ... }.
- Recommended for working with large event logs.


## XPath Query

### Concepts Learned
- XPath (XML Path Language) is a standard syntax for querying XML documents.
- Windows Event Logs support a subset of XPath 1.0 for filtering events.
- Both Get-WinEvent and wevtutil.exe can use XPath queries to filter logs.

### Explanation
- XPath queries allow precise selection of events based on XML elements like System, EventID, Provider, or EventData.
- You can construct queries directly from the Event Viewer’s XML View by following the XML structure of an event.
- Queries can combine multiple conditions, such as filtering by Event ID and Provider name.
- Using XPath is essential for automating log analysis and extracting only relevant events efficiently.

### Notes
- Use * or Event as the starting point of a query.
- For System elements: filter by EventID, Level, or Provider.
- For EventData elements: filter by attributes like TargetUserName.
- Combining multiple filters is possible using logical operators (and).
- This method applies to both Get-WinEvent and wevtutil.exe.


## Event IDs

### Concepts Learned
- Event IDs are numeric identifiers for specific actions or events in Windows Event Logs.
- Knowing relevant Event IDs is essential for monitoring, hunting, and incident response.
- Event IDs vary by log type (System, Security, Application) and feature (PowerShell, Process Creation, Firewall, etc.).

### Explanation
- Monitoring Event IDs allows detection of unusual or malicious activity, such as new service installation, account manipulation, or firewall changes.
- Resources to reference for Event IDs include:
- Windows Logging Cheat Sheet (Windows 7 – 2012) – guides which IDs to monitor and features to enable.
- NSA: Spotting the Adversary with Windows Event Log Monitoring – offers practical detection tips for common adversary behaviors.
- MITRE ATT&CK – maps techniques to event IDs for detection, e.g., T1098 (Account Manipulation).
- Microsoft documentation – Events to Monitor and Security Auditing references (comprehensive, official guides).
- Some events are not generated by default and require configuration:
- PowerShell logging – can be enabled via Group Policy or Registry to capture PowerShell events.
- Audit Process Creation – generates Event ID 4688 for command-line process auditing.

### Notes
- Event IDs are vital for targeted monitoring and threat hunting; you don’t need to memorize all, but focus on key ones relevant to your environment.
- Always verify that logging features are enabled for the events you want to monitor.
- Use the combination of official guides, threat intel, and ATT&CK references to build a baseline for detection.
- Key Takeaway: Effective monitoring depends on knowing what to look for and ensuring the system generates those logs.


## Hands-On Practice

### Concepts Learned
- Practical application of Windows Event Logs for monitoring and detection.
- Understanding how to correlate event IDs, logs, and activity for real-world scenarios.
- Using previously learned tools (Event Viewer, wevtutil, Get-WinEvent, XPath) for investigation.

### Explanation
- Hands-on scenarios simulate real monitoring and incident response tasks.
- Practice involves querying event logs to detect specific actions, such as:
- PowerShell activity – enabling logging to verify coverage and monitor executed commands.
- Event log clearance – detecting if logs are deleted, which could indicate tampering or adversary activity.
- Threat detection – searching for specific event IDs (e.g., 4104) and payloads to detect malware or malicious scripts.
- User activity monitoring – confirming suspicious actions, such as privilege enumeration or unusual command execution.

### Notes
- Scenarios require analyzing a provided external event log file (merged.evtx).
- Use all available tools and query techniques to locate relevant events.
- Online resources may be needed to understand event details, IDs, or filtering techniques.
- Key Takeaway: Practical experience reinforces how event logs support security monitoring, auditing, and incident response.


## Key Takeaways
- Event logs are essential for monitoring, troubleshooting, and understanding system activity.
- Event Viewer, wevtutil, and Get-WinEvent are primary tools for accessing and analyzing Windows Event Logs.
- XPath queries and FilterHashtable provide efficient ways to filter and extract relevant events.
- Event IDs are crucial for targeted monitoring; focus on key IDs related to your environment and threat scenarios.
- PowerShell logging and Audit Process Creation are examples of features that must be enabled for complete visibility.
- Hands-on practice reinforces understanding of how to query, filter, and analyze logs to detect malicious or unusual activity.
- Proactive monitoring and knowing what to look for are fundamental to effective detection and incident response.
