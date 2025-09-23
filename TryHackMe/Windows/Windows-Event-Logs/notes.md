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


