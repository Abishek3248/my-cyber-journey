# Summary – Core Windows Processes

**This room focused on the critical processes running in Windows, how they relate to each other, and how to identify normal vs unusual behavior for security monitoring.**

- Understanding the System process (PID 4) as the kernel-mode core of Windows, running system threads and memory allocation.
- Learning about smss.exe (Session Manager Subsystem) as the first user-mode process that initializes sessions and starts core subsystem processes.
- Exploring csrss.exe (Client Server Runtime Process) as the user-mode component of the Windows subsystem, responsible for console windows, process threads, and API access.
- Reviewing wininit.exe (Windows Initialization Process) which launches critical processes like services.exe, lsass.exe, and lsaiso.exe.
- Examining services.exe (Service Control Manager) for managing Windows services and device drivers, and its role as a parent to svchost.exe and other services.
- Investigating svchost.exe (Service Host) for hosting multiple Windows services in shared processes, and understanding the -k parameter for grouping services.
- Analyzing lsass.exe (Local Security Authority Subsystem Service) for enforcing security policies, handling logins, and generating access tokens.
- Understanding winlogon.exe (Windows Logon) for handling Secure Attention Sequence (CTRL+ALT+DEL), user profiles, and session logons.
- Reviewing explorer.exe (Windows Explorer) as the primary user interface process, responsible for the desktop, Start Menu, and Taskbar.
- Learning normal and unusual indicators for each process: parent process, number of instances, session, image path, and user account, which are essential for endpoint analysis and detecting malicious activity.
