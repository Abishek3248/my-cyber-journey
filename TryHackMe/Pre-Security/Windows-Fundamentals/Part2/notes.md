# Windows Fundamentals 2

## Introduction

- Windows Fundamentals Part 2 builds on the basics learned in Part 1, diving deeper into the tools and utilities that help manage, monitor, and troubleshoot a Windows operating system. This module explores essential system utilities, methods to access them, and practical ways to use these tools to maintain, optimize, and secure a Windows environment.



## System Configuration (MSConfig)

### Concepts Learned
- System Configuration (MSConfig) is a Windows utility used for advanced troubleshooting and diagnosing startup issues.
- It provides control over which programs, services, and tools run during system boot.
- Offers quick access to many built-in Windows utilities via the Tools tab.

### Explanation
- MSConfig is designed to help administrators and advanced users troubleshoot and optimize the Windows startup process. It is divided into five main tabs:
**General Tab:**
- Selects the startup mode for Windows. Options include:
- Normal startup: Loads all devices and services.
- Diagnostic startup: Loads only basic devices and services for troubleshooting.
- Selective startup: Allows custom selection of devices/services to load.
**Boot Tab:**
- Defines various boot options for the OS, such as Safe Mode, boot logging, and setting timeout values.
**Services Tab:**
- Lists all services configured on the system, regardless of whether they are running or stopped.
- Services are background programs essential for system operations or specific applications.
- Services can be enabled or disabled to troubleshoot system performance or conflicts.
**Startup Tab:**
- Redirects users to Task Manager to manage startup programs (enable/disable).
- MSConfig itself does not manage startup items; Task Manager is used instead.
- In some virtual machines (like the attached THM VM), the Startup tab may appear empty.
**Tools Tab:**
- Provides a list of system utilities with brief descriptions of their purpose.
- Each tool shows the command needed to launch it via Run, Command Prompt, or MSConfig itself.
- Examples include Event Viewer, System Information, Registry Editor, Performance Monitor, etc.

### Notes
- MSConfig requires local administrator privileges to access.
- While MSConfig can help troubleshoot startup issues, it is not a replacement for Task Manager for managing startup programs.
- The Tools tab is a convenient way to launch multiple Windows utilities without remembering their commands.
- MSConfig is mostly used to:
- Diagnose boot issues
- Disable problematic services or startup programs temporarily
- Access Windows system tools quickly


## Change UAC Settings

### Concepts Learned
- User Account Control (UAC) settings can be adjusted through the System Configuration panel. The slider allows modification of UAC behavior, though turning it off is not recommended.

### Explanation
UAC helps prevent unauthorized system changes by requiring confirmation for elevated tasks. Adjusting the slider changes the level of notification for administrative actions.

### Notes
- UAC settings can be accessed via UserAccountControlSettings.exe or through the Control Panel.
- The default setting balances security and convenience.
- Disabling UAC increases risk of malware or accidental system changes.


## Computer Management

### Concepts Learned:
- System Tools: Task Scheduler, Event Viewer, Shared Folders, Local Users and Groups, Performance Monitor, Device Manager
- Storage: Disk Management
- Services and Applications: Services, WMI Control

### Explanation:
- Task Scheduler: Automates running programs or scripts based on schedules, login/logoff, or specific triggers. Useful for routine maintenance or monitoring tasks.
- Event Viewer: Maintains logs of system, application, and security events. Helps diagnose issues and understand system activity.
- Shared Folders: Lists shared resources, connected users, and open files. Permissions control access to these resources.
- Local Users and Groups: Manages user accounts and groups, including permissions and group memberships.
- Performance Monitor (Perfmon): Tracks real-time or logged system performance data to troubleshoot issues.
- Device Manager: Manages hardware devices; allows enabling, disabling, or configuring device properties.
- Disk Management: Performs storage tasks like creating drives, resizing partitions, and assigning drive letters.
- Services: Background applications that can be enabled, disabled, or configured.
- WMI Control: Manages Windows Management Instrumentation for local or remote administration. WMIC is deprecated; PowerShell is recommended.

### Notes:
- Access Computer Management via Start Menu → Run → compmgmt.msc.
- Task Scheduler: Create Basic Task under Actions pane.
- Event Viewer logs: Application, Security, Setup, System, Forwarded Events.
- Shared Folders default shares: C$, ADMIN$.
- Disk Management tasks: New Simple Volume, Extend, Shrink, Change Drive Letter.
- Services tab: Configure startup type and properties for background services.
- WMI Control: Command-line via WMIC (deprecated) or PowerShell for scripts.


## System Information

### Concepts Learned:
- Understanding the purpose of the System Information tool (msinfo32).
- Overview of hardware resources, components, and software environment in Windows.
- Using environment variables to access system paths and settings.
- Searching within the System Information utility for specific data, like IP addresses.

### Explanation:
- The System Information tool (msinfo32) provides a detailed overview of a computer's hardware, system components, and software environment. It is useful for diagnosing issues, checking configurations, and viewing technical specifications. The information is organized into three main sections:
- Hardware Resources: Contains technical details about memory, IRQs, I/O, and other system-level resources.
- Components: Shows installed hardware devices, such as display adapters, input devices, storage devices, etc.
- Software Environment: Displays information about installed programs, drivers, environment variables, network connections, and other system settings.
- Environment variables are stored system-wide or user-specific and provide critical paths and configurations that programs and the OS reference. For example, the - WINDIR variable points to the Windows installation directory.

### Notes:
- To open System Information: Press Windows + R → type msinfo32 → Enter.
- You can view Environment Variables directly within msinfo32 or through Control Panel / Settings:
- Control Panel > System and Security > System > Advanced system settings > Environment Variables
- Settings > System > About > Advanced system settings > Environment Variables
- Use the search bar in msinfo32 to locate specific information, such as IP addresses.
- System Summary provides high-level details, like processor type, OS version, and installed memory.


## Resource Monitor

### Concepts Learned:
- Resource Monitor (resmon) is a Windows utility that provides detailed, per-process and aggregate system resource usage information.
- It monitors CPU, memory, disk, and network usage and allows advanced filtering for process-specific analysis.
- The tool helps identify deadlocks, file locking conflicts, and unresponsive applications.

### Explanation:
- Resource Monitor displays resource usage in real-time across four main categories: CPU, Memory, Disk, and Network.
- Each category has its own tab providing deeper insights into processes, services, and modules using those resources.
- A graphical pane on the right visualizes resource usage for easier interpretation.

### Notes:
- Primarily used by advanced users for troubleshooting performance issues.
- Users can start, stop, pause, or resume services and close unresponsive applications.
- Resource Monitor helps diagnose conflicts without forcing application shutdowns, potentially preventing data loss.


## Command Prompt (Commands)

### Concepts Learned:
- Command Prompt (cmd) allows users to interact with the Windows OS via text commands.
- Even though Windows provides a GUI, the command line remains a powerful tool for system information and troubleshooting.
- Commands often have help manuals to understand syntax and available parameters.

### Explanation:
**Basic Commands:**
    - hostname → Displays the computer name.
    - whoami → Displays the currently logged-in user.
    - cls → Clears the command prompt screen.
**Networking Commands:**
    - ipconfig → Shows network address settings. Use ipconfig /? for command help.
    - netstat → Displays protocol statistics and TCP/IP connections. Parameters like -a, -b, -e modify output.
    - net → Manages network resources; sub-commands include user, localgroup, use, share, session. Use net help [sub-command] to get usage information.

### Notes:
- Each command can be expanded with parameters to provide more detailed output.
- Command Prompt is useful for troubleshooting, network diagnostics, and gathering system information quickly.
- Users can explore the full set of commands using Microsoft’s official documentation link.


## Registry Editor

### Concepts Learned:
- The Windows Registry is a central hierarchical database storing configuration information for users, applications, and hardware.
- It is continuously referenced by Windows during system operation.
- Editing the registry can have major impacts, so it is intended for advanced users.

### Explanation:
**The registry contains information such as:**
- User profiles
- Installed applications and associated document types
- Property sheet settings for folders and application icons
- Hardware configuration
- Ports in use
- The Registry Editor (regedit) is the primary tool to view and edit the registry.

### Notes:
- Use caution when modifying the registry, as incorrect changes can disrupt normal system operations.
- Always back up the registry or create a system restore point before making changes.
- Refer to Microsoft’s official documentation to understand the registry structure and best practices.


## Key Takeaways:
- The System Configuration utility (MSConfig) is essential for diagnosing startup issues and managing system services.
- User Account Control (UAC) protects against unauthorized changes by prompting for elevated permissions when needed.
- Computer Management provides tools like Task Scheduler, Event Viewer, Shared Folders, Device Manager, and Performance Monitor for advanced system administration and troubleshooting.
- Disk Management allows configuring storage drives, partitions, and drive letters.
- System Information (msinfo32) gives a detailed overview of hardware, components, and the software environment, including environment variables.
- Resource Monitor (resmon) provides real-time monitoring of CPU, memory, disk, and network usage per process.
- Command Prompt (cmd) remains a powerful tool for system interaction, troubleshooting, and querying network and user information.
- Windows Registry is a central database storing configuration settings for users, applications, and hardware; editing it should be done carefully.
