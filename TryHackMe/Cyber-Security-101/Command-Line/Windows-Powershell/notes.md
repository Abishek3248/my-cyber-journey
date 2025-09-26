# Powershell Command Line

## Introduction
- PowerShell is Microsoft’s cross-platform tool for task automation and configuration management.  
- It combines a command-line shell with a scripting language built on the .NET framework.  
- Unlike the traditional Command Prompt, PowerShell is **object-oriented**, allowing more powerful data handling.  
- Developed in the early 2000s by Jeffrey Snover to overcome cmd.exe and batch file limitations.  
- Released in **2006** and later expanded with **PowerShell Core (2016)** to support Windows, macOS, and Linux.  
- Objects in PowerShell have **properties** (data) and **methods** (actions), making automation more efficient.  
- Cmdlets return objects instead of plain text, enabling flexible data manipulation and chaining commands.  

## Powershell Basics

### Concepts Learned
- PowerShell can be launched in multiple ways: Start Menu, Run dialog, File Explorer, Task Manager, or from Command Prompt.
- Once launched, the prompt is `PS C:\>`.
- PowerShell commands are called **cmdlets** and follow a **Verb-Noun** naming convention (e.g., `Get-Content`, `Set-Location`).
- Cmdlets return **objects** instead of plain text, allowing easier data manipulation.
- PowerShell provides built-in tools for discovering commands (`Get-Command`), learning their usage (`Get-Help`), viewing aliases (`Get-Alias`), and extending functionality (`Find-Module`, `Install-Module`).

### Commands / Tools
- `powershell` → Launches PowerShell from cmd.exe or Run dialog.  
- `Get-Command` → Lists all cmdlets, functions, aliases, and scripts in the current session.  
- `Get-Command -CommandType Function` → Filters to show only functions.  
- `Get-Help <cmdlet>` → Displays detailed info about a cmdlet, including syntax and parameters.  
- `Get-Help <cmdlet> -examples` → Shows practical usage examples.  
- `Get-Alias` → Lists all aliases for cmdlets (e.g., `dir` = `Get-ChildItem`).  
- `Find-Module -Name "pattern*"` → Searches online repositories (e.g., PSGallery) for modules.  
- `Install-Module -Name <ModuleName>` → Installs a module from an online repository.  

### Notes
- Cmdlets follow a consistent Verb-Noun structure for clarity.  
- Objects returned by cmdlets contain properties and methods, unlike plain text in CMD.  
- `Get-Help` is essential for understanding cmdlets and their usage.  
- Aliases allow smooth transition from traditional CMD commands to PowerShell.  
- Modules expand PowerShell functionality; PSGallery is the main source for additional modules.  


## Navigating The FileSystem And Working With Files

### Concepts Learned
- PowerShell provides cmdlets for navigating and managing the filesystem, similar to traditional CLI commands.
- `Get-ChildItem` lists files and directories in a specified path; defaults to current directory if no path is given.
- `Set-Location` changes the current directory, similar to `cd`.
- `New-Item` can create both files and directories in one cmdlet by specifying `-ItemType`.
- `Remove-Item` deletes both files and directories (replaces `del` and `rmdir`).
- `Copy-Item` and `Move-Item` handle copying and moving files/directories.
- `Get-Content` displays the content of a file, similar to `type` or `cat`.

### Commands / Tools
- `Get-ChildItem` → List contents of a directory.  
- `Set-Location -Path <Path>` → Change current working directory.  
- `New-Item -Path <Path> -ItemType "File|Directory"` → Create a file or directory.  
- `Remove-Item -Path <Path>` → Delete a file or directory.  
- `Copy-Item -Path <Source> -Destination <Destination>` → Copy file or directory.  
- `Move-Item -Path <Source> -Destination <Destination>` → Move file or directory.  
- `Get-Content -Path <FilePath>` → Display content of a file.

### Notes
- PowerShell cmdlets unify file and directory operations, unlike the split commands in traditional CLI.  
- Objects returned by cmdlets retain properties, enabling more complex operations (like filtering by file attributes).  
- Using `Get-ChildItem` with `-Path` allows exploring any directory; without it, defaults to current location.  
- `New-Item` and `Remove-Item` handle nested directories or files, simplifying scripting and automation.  
- `Copy-Item` and `Move-Item` can handle multiple items or directories recursively with parameters.  
- `Get-Content` is versatile and can read entire files or stream content line by line for processing.


## Piping, Filtering, and Sorting Data

### Concepts Learned
- Piping (`|`) allows the output of one cmdlet to be passed as input to another, enabling complex command sequences.
- PowerShell passes objects, not plain text, through the pipeline, preserving properties and methods.
- `Sort-Object` sorts objects based on specified properties.
- `Where-Object` filters objects based on conditions using comparison operators (-eq, -ne, -gt, -ge, -lt, -le, -like).
- `Select-Object` refines output by selecting specific properties or limiting the number of objects.
- `Select-String` searches for text patterns in files, supporting regex for advanced pattern matching.

### Commands / Tools
- `Get-ChildItem | Sort-Object <Property>` → Sort objects by a property (e.g., file size).  
- `Get-ChildItem | Where-Object -Property <Property> -eq <Value>` → Filter objects by property value.  
- Comparison Operators: `-eq` (equal), `-ne` (not equal), `-gt` (greater than), `-ge` (greater than or equal), `-lt` (less than), `-le` (less than or equal), `-like` (pattern match).  
- `Get-ChildItem | Select-Object <Property1,Property2>` → Display only selected properties.  
- `Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 1` → Example: get largest file.  
- `Select-String -Path <FilePath> -Pattern "<pattern>"` → Search file content for a text pattern.  

### Notes
- PowerShell’s object-based piping allows chaining multiple cmdlets efficiently.  
- Sorting and filtering can be combined to extract detailed information from large datasets.  
- `Where-Object` supports flexible conditions for numeric, string, and pattern-based filtering.  
- `Select-Object` is useful to simplify output or focus on essential properties.  
- `Select-String` is ideal for analyzing log files or text data, and regex extends its capability for complex searches.  
- Building pipelines lets you perform advanced queries in a single command, reducing the need for manual post-processing.


## System and Network Information

### Concepts Learned
- PowerShell provides cmdlets to retrieve detailed system and network information for management and monitoring.
- `Get-ComputerInfo` offers a comprehensive snapshot of system configuration, including OS, hardware, and BIOS details.
- `Get-LocalUser` lists all local user accounts with properties like username, enabled status, and description.
- `Get-NetIPConfiguration` provides detailed information about network interfaces, including IP addresses, gateways, and DNS servers.
- `Get-NetIPAddress` retrieves all IP addresses on the system, including active and inactive ones, with detailed properties.

### Commands / Tools
- `Get-ComputerInfo` → Retrieve comprehensive system information (OS, hardware, BIOS, etc.).  
- `Get-LocalUser` → List all local user accounts and account details.  
- `Get-NetIPConfiguration` → Show network interface details, including IP, gateway, and DNS.  
- `Get-NetIPAddress` → Display all IP addresses configured on the system.  

### Notes
- PowerShell provides more detailed and structured information than traditional commands like `systeminfo` or `ipconfig`.  
- `Get-ComputerInfo` outputs multiple object properties, enabling easy filtering or selection in scripts.  
- Local user management and auditing are simplified using `Get-LocalUser`, which can also be combined with filtering or export commands.  
- Network information cmdlets allow IT professionals to quickly assess connectivity, routing, and configuration without relying on multiple separate commands.  
- These cmdlets are essential for monitoring, troubleshooting, and automating system and network management tasks in both local and remote environments.


## Real-Time System Analysis

### Concepts Learned
- PowerShell provides cmdlets to monitor and analyze real-time system information.
- Get-Process lists all currently running processes with details like CPU, memory usage, and process ID.
- Get-Service shows the status of Windows services (running, stopped, paused) and is useful for troubleshooting and forensic analysis.
- Get-NetTCPConnection displays active TCP connections, including local/remote addresses and ports, helping in incident response.
- Get-FileHash generates cryptographic hashes of files, useful for integrity verification, malware analysis, and threat hunting.
- These cmdlets allow IT professionals to perform dynamic system monitoring beyond static system information.

### Commands/Tools
- Get-Process – Lists all running processes.
- Get-Service – Shows all services and their status.
- Get-NetTCPConnection – Displays active TCP connections.
- Get-FileHash -Path <file> – Computes the hash of a file.

### Notes
- Get-Process can be used to monitor CPU/memory usage and identify suspicious processes.
- Get-Service is essential for detecting tampered or unauthorized services; combining it with filtering (Where-Object) can help isolate problematic services.
- Get-NetTCPConnection shows which processes own which connections (OwningProcess property).
- Get-FileHash supports multiple algorithms (SHA256, SHA1, MD5) and helps validate the integrity of critical files.
- These cmdlets are crucial for incident response, threat hunting, and system troubleshooting.


## Scripting

### Concepts Learned
- Scripting is writing a sequence of commands in a text file (script) to automate tasks in PowerShell.
- Scripts reduce errors, save time, and can handle complex or repetitive tasks.
**PowerShell scripting is essential in cyber security for both blue team and red team tasks:**
  - Blue team: log analysis, anomaly detection, IOC extraction, malware analysis, automated response.
  - Red team: system enumeration, remote command execution, obfuscated scripts for testing defenses.
  - System admins: automate integrity checks, manage configurations, enforce security policies.
- Invoke-Command allows executing commands or scripts on remote systems, making it crucial for automation, remote management, and penetration testing.
- Using Invoke-Command with -FilePath runs a local script on a remote computer; using -ScriptBlock allows inline commands to run remotely.

### Commands/Tools
- Invoke-Command -ComputerName <RemoteComputerName> -FilePath <ScriptPath> → Runs a script on a remote computer.
- Invoke-Command -ComputerName <RemoteComputerName> -ScriptBlock { <Command(s)> } → Executes commands directly on the remote system.

### Notes
- Invoke-Command does not require scripting knowledge for simple tasks; -ScriptBlock can run single or multiple commands.
- Can be combined with custom scripts to automate tasks across multiple systems.
- Useful for incident response, system administration, and penetration testing.


## Key Takeaways
- PowerShell is a powerful object-based shell for automation, system management, and advanced data handling, going beyond traditional Windows CLI capabilities.
- Cmdlets follow a Verb-Noun structure, providing consistency and clarity in command usage.
- File system navigation and management are simplified, allowing efficient handling of directories and files.
- Piping (|) enables chaining cmdlets to filter, sort, and manipulate data effectively.
- System and network information can be retrieved and analyzed quickly, supporting administration, monitoring, and troubleshooting tasks.
- Real-time system monitoring allows inspection of processes, services, network connections, and file integrity, essential for both defensive and offensive cybersecurity roles.
-  PowerShell scripting automates repetitive or complex tasks, and Invoke-Command facilitates remote management and execution.
- Hands-on exercises in this room reinforced learning by practicing file navigation, object filtering, system and network checks, process and service monitoring, and remote command execution.
- Mastery of these concepts and practical skills lays a strong foundation for cybersecurity work, system administration, and efficient workflow automation.
