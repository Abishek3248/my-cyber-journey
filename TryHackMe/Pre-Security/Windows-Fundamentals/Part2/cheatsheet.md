# Cheatsheet - Windows Fundamentals Part 2

| Tool / Command           | Purpose / Description                                                                                 | Notes / Key Points                                                                 |
|--------------------------|-------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| **MSConfig (System Configuration)** | Diagnose startup issues, manage services, control boot options                                      | Tabs: General, Boot, Services, Startup, Tools                                      |
| **User Account Control (UAC)**     | Controls elevated privilege prompts to prevent unauthorized changes                                | Adjust using UAC settings; not applied to built-in admin account                  |
| **Task Scheduler**        | Automate tasks (run scripts or applications at specific times or events)                             | Create Basic Task or Advanced Task                                                |
| **Event Viewer**          | View system logs to diagnose issues or audit events                                                  | Event types: Information, Warning, Error, Audit Success, Audit Failure            |
| **Shared Folders**        | View/manage shared folders and permissions                                                          | Check sessions and open files                                                      |
| **Performance Monitor (Perfmon)** | Monitor system performance in real-time or from logs                                               | Can analyze CPU, memory, disk, network metrics                                     |
| **Device Manager**        | Manage and configure hardware devices                                                               | Disable/enable hardware, view properties                                          |
| **Disk Management**       | Create, extend, shrink partitions, assign/change drive letters                                      | Requires administrative privileges                                                |
| **System Information (msinfo32)** | View hardware, software environment, and system components                                        | Sections: System Summary, Hardware Resources, Components, Software Environment     |
| **Environment Variables** | Store OS environment info (paths, TEMP folder, WINDIR, etc.)                                        | Accessible via System Properties or msinfo32                                      |
| **Resource Monitor (resmon)** | Real-time monitoring of CPU, memory, disk, and network usage                                      | Includes per-process analysis and filtering                                       |
| **Command Prompt (cmd)**  | Run commands for system and network info, troubleshooting                                          | Common commands: hostname, whoami, ipconfig, netstat, net, cls                     |
| **Windows Registry (regedit)** | Central database storing configuration for OS, users, apps, hardware                               | Editing requires caution; can affect system behavior                               |

