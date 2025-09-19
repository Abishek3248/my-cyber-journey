# Core Windows Processes

## Introduction
- Windows is the most widely used operating system, and most users only care that it “just works” for daily tasks like browsing, email, shopping, or media. Security awareness was once limited to antivirus software, but modern threats have evolved far beyond what traditional AV can handle.
- Today, endpoint security uses a layered defense approach with tools like EDR (Endpoint Detection and Response). Even so, no solution is 100% effective — attackers can still bypass defenses.
- This makes it crucial for security professionals (SOC Analysts, Threat Hunters, Detection Engineers) to understand normal Windows processes and behaviors. By recognizing what’s expected, we can spot anomalies and distinguish legitimate activity from malicious behavior when alerts are triggered.


## Task Manager

### Concepts Learned
- Task Manager is a built-in GUI tool for monitoring processes and resources.
- Processes are categorized into Apps, Background, and Windows processes.
- Key columns: Type, Publisher, PID, Process name, Command line, CPU, and Memory.
- Task Manager lacks parent–child process visibility.
- Alternative tools: Process Hacker, Process Explorer, and CLI utilities.

### Explanation
- Task Manager shows what’s running and resource usage (CPU, memory).
- More details expands visibility into process categories and columns.
- Columns like Image path name and Command line help spot anomalies (e.g., fake system processes).
- Each process is assigned a unique PID; multiple instances of the same program get different PIDs.
- Parent–child process relationships are crucial for detection, but not visible in Task Manager.
- Tools like Process Hacker and Process Explorer fill this gap with richer views.
- Command-line alternatives (tasklist, Get-Process, wmic) provide lightweight process inspection.

### Notes
- PID (Process ID) is unique for each running process.
- svchost.exe should always have services.exe as parent — mismatches may indicate malicious activity.
**Useful CLI commands:**
   - tasklist → list tasks with PID, memory usage
   - Get-Process / ps (PowerShell) → get detailed process info
   - wmic process list → query process details including command line
   - Process Explorer and Process Hacker are recommended for detailed analysis.
 

## System

### Concepts Learned
- The System process (PID 4) is unique and always runs in kernel mode.
- It is critical for managing kernel-mode system threads, which execute OS-level functions.
- Normal vs. unusual behavior must be understood for threat detection.

### Explanation
- PID Uniqueness: Unlike most processes, the System process always has PID 4.
**Kernel-mode threads:**
- Similar to user-mode threads but run only in kernel mode.
- Execute code from ntoskrnl.exe or loaded drivers.
- No user process address space; rely on system memory pools.
**Properties (via Process Explorer/Process Hacker):**
- Image Path: N/A in Explorer, C:\Windows\system32\ntoskrnl.exe in Hacker.
- Parent Process: None (Explorer) or System Idle Process (0) (Hacker).
- User Account: Local System.
- Instances: Only one.
- Start Time: At boot time.
- Verified as legitimate Windows component in Process Hacker.
**Unusual behaviors (red flags):**
- Parent process other than System Idle Process (0).
- Multiple instances of the System process.
- PID not equal to 4.
- Running outside of Session 0.

### Notes
- The System process is core to Windows stability—if compromised, attackers gain kernel-level privileges.
- Any deviation from its expected properties should be treated as highly suspicious.
- Detection tip: Always verify PID (4), instance count (1), and parent process.


## smss.exe process

### Concepts Learned
- smss.exe (Session Manager Subsystem) is the first user-mode process started by the Windows kernel.
- It creates and manages Windows sessions, initializing both kernel-mode and user-mode subsystems.
- Responsible for starting essential processes like csrss.exe, wininit.exe, and winlogon.exe.
- Manages session environment variables, paging files, and subsystem initialization.

### Explanation
**Role in Boot Process:**
- Starts immediately after the kernel.
- Launches kernel-mode (win32k.sys) and user-mode components (winsrv.dll, csrss.exe).
**Session 0 (OS services):**
- Launches csrss.exe and wininit.exe.
**Session 1 (User session):**
- Launches csrss.exe and winlogon.exe.
- Copies itself into new sessions and then self-terminates child instances.
**Registry Role:**
- Launches any subsystems listed under
  'HKLM\System\CurrentControlSet\Control\Session Manager\Subsystems'.
**Responsibilities:**
- Creates environment variables.
- Configures virtual memory paging.
- Starts winlogon.exe for handling logon.

### Notes
**Normal Behavior**
- Image Path: %SystemRoot%\System32\smss.exe
- Parent Process: System (PID 4)
- Instances: One master instance, one child per session (children terminate afterward).
- User: Local System
- Start Time: Seconds after boot for the master instance.
**Unusual / Suspicious Behavior**
- Parent process is not System (4).
- Image path differs from C:\Windows\System32\smss.exe.
- Multiple persistent instances (children should terminate).
- Running user is not SYSTEM.
- Unexpected registry entries in Subsystems.


## csrss.exe process

### Concepts Learned
- User-mode side of the Windows subsystem.
- Critical system process; terminating it causes system failure.
- Handles Win32 console windows, thread creation/deletion, Windows API access, and shutdown tasks.
- Spawned by smss.exe during startup for Session 0 and Session 1.

### Explanation
- Critical Role: Manages essential user-mode operations (Win32 console, thread handling, drive mappings, shutdown).
**Startup:**
- Session 0 → created by smss.exe (PID ~392).
- Session 1 → also created by smss.exe (PID ~512).
- Additional instances are created when new sessions start.
- DLLs Loaded: Includes csrsrv.dll, basesrv.dll, winsrv.dll, etc.
- API Support: Makes the Windows API available to other processes.
- Parent Process: Technically smss.exe, but since smss.exe self-terminates, csrss.exe often appears with no visible parent.

### Notes
**Normal Behavior**
- Image Path: %SystemRoot%\System32\csrss.exe
- Parent Process: Created by smss.exe (self-terminates afterward).
- Instances: Two or more (at least one for Session 0 and one for Session 1).
- User Account: Local System
- Start Time: Within seconds of boot for Sessions 0 & 1.
**Unusual Behavior**
- Visible parent process (shouldn’t normally have one).
- Image path not C:\Windows\System32.
- Subtle misspellings (e.g., crss.exe) indicating masquerading malware.
- Running under a user account other than SYSTEM.


## wininit.exe process

### Concepts Learned
- Critical background Windows process responsible for starting essential services.
- Launches services.exe (Service Control Manager), lsass.exe (Local Security Authority), and optionally lsaiso.exe (if Credential Guard is enabled).
- Runs within Session 0.

### Explanation
- Role: Initializes core Windows service processes at boot.
**Process Tree: Spawns:**
- services.exe → manages system services.
- lsass.exe → handles authentication and security policies.
- lsaiso.exe → only present if Credential Guard/KeyGuard is enabled.
- Parent Process: Created by smss.exe, which self-terminates.
- Session Context: Always runs in Session 0 (OS-level session).

### Notes
**Normal Behavior**
- Image Path: %SystemRoot%\System32\wininit.exe
- Parent Process: Spawned by smss.exe (invisible after termination).
- Instances: Exactly one.
- User Account: Local System
- Start Time: Within seconds of boot.
**Unusual Behavior**
- Visible parent process (shouldn’t normally have one).
- Image path different from C:\Windows\System32.
- Subtle misspellings (e.g., wninit.exe, winlnt.exe).
- Multiple running instances (should only be one).
- Running under any account other than SYSTEM.


## services.exe process

### Concepts Learned
- Core Windows process that manages system services (loading, starting, stopping, interacting).
- Maintains a services database, accessible via sc.exe.
- Loads auto-start device drivers into memory.
- Responsible for updating the Last Known Good Configuration in the registry after successful login.
- Parent process for critical service-hosting processes like svchost.exe, spoolsv.exe, msmpeng.exe, and dllhost.exe.

### Explanation
- Role: Central service controller of Windows, ensuring essential services and drivers run properly.
**Registry Interaction:**
*Services configuration stored in:*
  - HKLM\System\CurrentControlSet\Services
*Updates LastKnownGood key in:*
  - HKLM\System\Select\LastKnownGood
- Command-Line Interaction: Managed via sc.exe, which can query, start, or stop services.
- Process Tree: Parent to many service-hosting and background processes.
- Parent Process: Created by wininit.exe.

### Notes
**Normal Behavior**
- Image Path: %SystemRoot%\System32\services.exe
- Parent Process: wininit.exe
- Instances: Exactly one
- User Account: Local System
- Start Time: Within seconds of boot
**Unusual Behavior**
- Parent process other than wininit.exe
- Image path not equal to C:\Windows\System32
- Subtle misspellings (e.g., servicess.exe, servlces.exe)
- Multiple instances (should only be one)
- Not running as SYSTEM


## svchost.exe process

### Concepts Learned
- Hosts and manages Windows services that run as DLLs.
**Service DLLs are registered in the registry under:**
   - HKLM\SYSTEM\CurrentControlSet\Services\SERVICE NAME\Parameters\ServiceDLL
- Uses the -k parameter to group similar services into shared processes.
- Since Windows 10 (1703+), on systems with >3.5 GB RAM, most services run in their own process to improve isolation and security.
- A common target for adversaries: malware can masquerade as svchost.exe or load malicious DLLs as fake services.

### Explanation
- Role: Runs and groups multiple Windows services under a single process.
- Registry Link: Each service points to its DLL in the registry (ServiceDLL).
**Binary Path Identifier:**
- Legitimate instances always include -k (e.g., svchost.exe -k DcomLaunch).
- Each -k group corresponds to different service sets (e.g., DcomLaunch, LSM).
- Design Purpose: Originally used to conserve resources by grouping services.
- Security Risk: Attackers exploit this by:
- Naming malware svchost.exe or a misspelled variant (scvhost.exe).
- Registering malicious DLLs as services.

### Notes
**Normal Behavior**
- Image Path: %SystemRoot%\System32\svchost.exe
- Parent Process: services.exe
- Instances: Multiple (expected)
- User Accounts: SYSTEM, Network Service, Local Service (sometimes logged-in user on Win10+)
- Start Time: Some at boot, others may appear later
**Unusual Behavior**
- Parent process other than services.exe
- Image path not equal to C:\Windows\System32
- Subtle misspellings (scvhost.exe, etc.)
- Missing -k parameter in binary path


## Lsass.exe process

### Concepts Learned
- LSASS (Local Security Authority Subsystem Service) enforces security policy in Windows.
- Handles user authentication, password changes, and generates access tokens.
- Writes security events into the Windows Security Log.
- Targets of attacks like credential dumping (e.g., with mimikatz) and process masquerading.

### Explanation
- Role: Validates logons, manages authentication packages, and enforces security policies.
- Tokens: Creates access tokens for SAM, Active Directory, and NETLOGON.
- Registry: Uses authentication packages defined under HKLM\System\CurrentControlSet\Control\Lsa.
- Threats: Attackers dump credentials from LSASS memory or disguise malware as lsass.exe.
- Defense: Microsoft added protections to prevent unauthorized LSASS access.

### Notes

**Normal Behavior**
- Image Path: %SystemRoot%\System32\lsass.exe
- Parent Process: wininit.exe
- Number of Instances: One
- User Account: Local System
- Start Time: Within seconds of boot
**Unusual Behavior**
- Parent process not wininit.exe
- Image path other than C:\Windows\System32
- Subtle misspellings (e.g., Isass.exe)
- Multiple instances running
- Not running as SYSTEM


## winlogon.exe process

### Concepts Learned
- winlogon.exe handles the Secure Attention Sequence (SAS) — CTRL+ALT+DELETE.
- Manages user logon, loading user profiles, and launching user shells.
- Responsible for screen locking, screensavers, and managing session logons.
- Launched by smss.exe in Session 1 alongside csrss.exe.

### Explanation
- Authentication: Captures SAS (CTRL+ALT+DELETE) and prompts login credentials.
- Profile Management: Loads NTUSER.DAT into HKCU, with userinit.exe starting the user’s shell (explorer.exe).
- Session Handling: Runs for Session 1 (interactive logon) and spawns new instances for Remote Desktop or Fast User Switching sessions.
- System Control: Handles lock screen, screensaver execution, and system-related session management.
- Startup: Created by smss.exe, which self-terminates (so tools rarely show a parent).

### Notes
**Normal Behavior**
- Image Path: %SystemRoot%\System32\winlogon.exe
- Parent Process: Created by smss.exe (self-terminates, so often hidden in analysis tools)
- Number of Instances: One for Session 1; additional instances possible for RDP or Fast User Switching
- User Account: Local System
- Start Time: Within seconds of boot for Session 1
**Unusual Behavior**
- Visible/active parent process (should not persist)
- Image path not in C:\Windows\System32
- Misspelled names (winilogon.exe, etc.)
- Not running as SYSTEM
- Registry anomaly: Shell value not set to explorer.exe


## explorer.exe process

### Concepts Learned
- explorer.exe provides the Windows graphical shell, including desktop, Start Menu, Taskbar, and file browsing.
- It is launched indirectly by winlogon.exe via userinit.exe.
- Acts as a parent for many user-initiated child processes.

### Explanation
- GUI Shell: Provides user access to files, folders, Start Menu, Taskbar, and desktop environment.
- Process Launch: winlogon.exe runs userinit.exe, which references the Shell registry value and launches explorer.exe. After spawning, userinit.exe exits.
- Parent Process: None visible, since userinit.exe terminates after spawning explorer.
- Multiple Instances: One or more instances depending on the number of interactively logged-in users.
- Child Processes: Many applications/processes launched by the user will appear under explorer.exe.

### Notes
**Normal Behavior**
- Image Path: %SystemRoot%\explorer.exe
- Parent Process: Created by userinit.exe (but parent disappears as it exits)
- Number of Instances: One or more per logged-in user session
- User Account: Interactive logged-in user(s)
- Start Time: When the first user session begins
**Unusual Behavior**
- Active parent process (should not exist — userinit.exe exits)
- Image path not in C:\Windows
- Running under an unknown or unexpected user account
- Misspelled variants (e.g., explorrer.exe)
- Unexpected outbound network connections (not normal for explorer.exe)


## Key Takeaways
- Windows has a set of core system processes that are critical for the OS to function properly. These include: System, smss.exe, csrss.exe, wininit.exe, services.exe, svchost.exe, lsass.exe, winlogon.exe, and explorer.exe.
- Each process has a specific role, from managing sessions and services to enforcing security policies and providing the user interface.
- Normal behavior patterns include expected image paths, parent processes, instance counts, user accounts, and start times.
- Anomalies such as multiple instances, incorrect paths, unusual parent processes, or running under unexpected user accounts may indicate malware or system compromise.
- Understanding these processes is essential for endpoint analysis, threat detection, and incident response, helping analysts distinguish between legitimate system activity and suspicious behavior.
