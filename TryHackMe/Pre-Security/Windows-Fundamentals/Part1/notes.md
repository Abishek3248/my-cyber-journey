# Windows Fundamentals - Part1

## Introduction
- The Windows operating system (OS) is one of the most widely used platforms in both personal and enterprise environments. It provides a graphical user interface (GUI), a wide range of system utilities, and extensive compatibility with applications, making it user-friendly and versatile.
- This module offers an overview of some core components of Windows: navigating the user interface, managing system settings, and performing basic administrative tasks. The content is designed for beginners who want to become comfortable with the Windows OS and understand its structure at a practical level.


## Windows Editions

### Concepts Learned
- Windows OS has evolved since 1985 and remains the most widely used desktop operating system.
- Each version has brought usability and security improvements, though some versions were poorly received.
- Current desktop version: Windows 11 (Home & Pro editions).
- Current server version: Windows Server 2025.
- Support timelines matter, as end-of-life can force users and organizations to upgrade.

### Explanation
- Windows has a long history, with major releases like XP, Vista, 7, 8, 10, and 11. Some versions (e.g., Vista, 8) were short-lived, while others (XP, 7, 10) had wide adoption. Microsoft continues to release improvements in usability and security, while also setting retirement dates to encourage upgrades. Today, Windows 11 is the current desktop OS, and Windows Server 2025 is the latest server OS.

### Notes
- Windows XP → very popular, but retired.
- Windows Vista → poorly received, quickly replaced.
- Windows 7 → widely adopted, later retired.
- Windows 8.x → short-lived.
- Windows 10 → long-running, retirement set for October 14, 2025.
- Windows 11 → current desktop OS (Home & Pro).
- Windows Server 2025 → current server OS.



## GUI (Graphical User Interface)

### Concepts Learned
- The Windows Desktop (GUI) is the first environment seen after logging in with valid credentials.
- Main GUI components include the Desktop, Start Menu, Search Box, Task View, Taskbar, Toolbars, and Notification Area.
- The Desktop provides quick access to files, folders, and programs, while personalization options allow customization.
- The Start Menu is the central hub for apps, programs, utilities, and account-related actions.
- The Taskbar displays active applications, pinned items, and provides previews.
- The Notification Area shows system icons like volume, network, date/time, and customizable shortcuts.

### Explanation
- The Windows GUI simplifies interaction with the operating system by offering a visual, user-friendly interface.
- The Desktop acts as a workspace for files and shortcuts, with customization options via right-click menus and personalization settings.
- The Start Menu provides structured access to applications, utilities, recent items, and account controls. Tiles on the right can be customized for quick access.
- The Taskbar keeps track of active or pinned applications and allows switching between them using thumbnails and tooltips.
- The Notification Area shows background services and system status, with options to configure visible icons.
- This structure enables efficient navigation, multitasking, and personalization for both casual and professional users.

### Notes
**Desktop**
- Quick access to apps, folders, files.
- Right-click menu allows icon size changes, arrangement, and creating shortcuts/folders.
- Display and personalization settings allow resolution, orientation, wallpapers, and themes.
**Start Menu**
- Access to installed programs, utilities, account controls, settings, and power options.
- Organized into recent apps, alphabetical listings, and customizable tiles.
- Apps can be pinned/unpinned or resized in the Start Menu.
**Taskbar**
- Shows active apps and pinned shortcuts.
- Hover previews help identify open windows.
- Right-click allows customization of visible components.
**Notification Area**
- Displays date/time, volume, network, and other system icons.
- Icons can be added/removed via Taskbar settings.
- Tip: Right-clicking any file, folder, or icon provides additional actions or properties.
- VM provided in lab → Windows Server 2019 Standard.



## Filesystem

### Concepts Learned
- Modern Windows uses NTFS (New Technology File System).
- Older systems used FAT16/FAT32 and HPFS; FAT still common in USBs and memory cards.
- NTFS supports large files, permissions, compression, and encryption.
- NTFS features: file/folder permissions, journaling, and Alternate Data Streams (ADS).

### Explanation
- NTFS replaced FAT and HPFS to overcome limitations like file size caps and lack of security. It’s a journaling filesystem, meaning it can recover from crashes using its log system. NTFS permissions allow fine-grained access control for files and folders, making it essential for security. It also supports encryption via EFS and can compress data.
- A unique feature is Alternate Data Streams (ADS), where files can hold hidden streams of data. ADS is sometimes used by malware to hide, but also has legitimate uses like tagging downloaded files with their origin.

### Notes
- FAT partitions: still common in USBs, MicroSD cards, but not main Windows drives.
**NTFS features:**
- Supports files >4GB
- Permissions: Full Control, Modify, Read & Execute, List Folder Contents, Read, Write
- File/folder compression and EFS encryption
- Journaling for crash recovery
- Checking filesystem: Right-click drive → Properties.
- Viewing permissions: Right-click → Properties → Security tab.
- ADS (Alternate Data Streams): Hidden file attribute in NTFS, viewable with PowerShell.
- Malware may abuse ADS to hide data.
- Legitimate use: downloaded files marked as "from the Internet".



## Windows\System32 Folders

### Concepts Learned
- The C:\Windows folder contains the operating system files but doesn’t have to reside specifically on the C: drive.
- The System32 folder inside C:\Windows holds critical system files required for Windows to function.
- Environment variables like %windir% ensure that the system can reference the correct Windows directory regardless of its location.
- System32 should be handled with extreme caution, as deleting or modifying files here can render Windows unusable.

### Explanation
- The Windows folder (C:\Windows) is the central location of the OS. Although traditionally installed on the C drive, Windows can technically reside on other drives or in different folders. To manage this, Windows uses environment variables (such as %windir%) so the system always knows where the OS files are located.
- Within this folder, the System32 directory is especially critical. It contains essential executables, libraries, and configuration files that allow the operating system to run. This is where many built-in tools and utilities are located.

### Notes
- %windir% → system environment variable pointing to the Windows directory.
- System32 contains critical executables and libraries.
- Deleting or modifying files in System32 can break the OS.
- Many of the utilities you’ll learn in Windows Fundamentals reside here.


## User Accounts, Profiles, and Permissions

### Concepts Learned
- Windows user accounts can be Administrator or Standard User, determining what system actions they can perform.
- User accounts have associated profiles stored under C:\Users\<username>.
- Permissions are managed via Local Users and Groups, where users inherit permissions from groups they belong to.
- Administrators can create, modify, or remove users and assign them to groups.

### Explanation
- Administrator accounts can make system-wide changes, including installing software, adding/removing users, and modifying group memberships.
- Standard User accounts are restricted to personal files/folders and cannot make system-level changes.
- When a new user logs in for the first time, a user profile is automatically created in C:\Users\<username>, containing default folders like Desktop, Documents, Downloads, Music, and Pictures.
- Permissions for users are inherited from the groups they belong to. Groups can be managed via lusrmgr.msc, accessible through the Run dialog.

### Notes
- Use the Start Menu → Other Users to view and manage user accounts.
- Only Administrators see options to Add someone else to this PC or Change account type.
- The Run command lusrmgr.msc opens Local Users and Groups for advanced user/group management.
- Groups define a set of permissions, and assigning a user to a group automatically applies those permissions.
- Users can belong to multiple groups and inherit cumulative permissions.


## User Account Control

### Concepts Learned
- User Account Control (UAC) helps protect Windows systems by limiting elevated privileges even for administrator accounts.
- Standard users cannot perform actions requiring higher privileges without entering administrator credentials.
- UAC reduces the risk of malware compromise by prompting for permission when elevated actions are attempted.

### Explanation
- Most home users operate with local administrator accounts, which can modify system settings.
- Running all tasks with elevated privileges increases security risks, as malware could execute with full administrative rights.
- UAC ensures that even administrator accounts run standard sessions by default; only actions requiring higher privileges trigger a prompt.
- Programs needing elevated permissions display a shield icon, indicating that a UAC confirmation is required.

### Notes
- Built-in administrator accounts are exempt from UAC prompts by default.
- Standard users attempting to perform administrative actions will be prompted to enter administrator credentials.
- UAC prompts disappear if no response is provided, preventing unauthorized operations.
- Access UAC settings and behavior via the Security tab in program properties or system settings.
- UAC is a core security feature in Windows versions since Vista and helps mitigate malware risks.


## Settings And Control Panel

### Concepts Learned
- Windows provides two main interfaces for making system changes: Settings and Control Panel.
- The Settings menu is the modern interface, introduced in Windows 8, optimized for touchscreens, and now the primary location for most user adjustments.
- The Control Panel is the traditional interface for more advanced or complex system configurations.

### Explanation
- Settings and Control Panel can both be accessed via the Start Menu search.
- Some actions in Settings will redirect you to Control Panel for advanced options (e.g., network adapter settings).
- The icons and layout may vary depending on the Windows version.
- Searching for a particular setting is a reliable way to determine which interface to use.

### Notes
- Settings: Primary location for personalizing Windows, changing wallpapers, adjusting themes, managing accounts, and general configuration.
- Control Panel: Used for advanced configurations like printer management, uninstalling programs, network adapters, and system tools.
- Users may navigate from Settings to Control Panel depending on the specific task.
- Familiarity with both interfaces ensures efficient system management and troubleshooting.


## Task Manager

### Concepts Learned
- The Task Manager provides a snapshot of applications, processes, and system resource usage (CPU, RAM, disk, network).
- It is an essential tool for monitoring system performance and managing running programs.

### Explanation
- Access Task Manager by right-clicking the taskbar and selecting Task Manager.
- By default, it opens in Simple View, showing only running applications.
- Clicking More details expands the view to show:
- All running processes (apps and background processes).
- CPU, memory, disk, and network usage
- Performance metrics for the system

### Notes
- Task Manager can be used to end unresponsive applications.
- It provides insights into which processes are consuming the most resources.
- Learning about core Windows processes helps in troubleshooting and system optimization.
- For in-depth information on processes, refer to resources like the Core Windows Processes room.


## Key Takeaway
- Gained practical understanding of the Windows operating system and its core components.
- Navigated the GUI, including Desktop, Start Menu, Taskbar, and Notification Area.
- Managed system settings via Settings and Control Panel.
- Explored the NTFS file system, folder structures like C:\Windows\System32, and file/folder permissions.
- Learned about user accounts (Administrator vs Standard User) and user profiles.
- Understood User Account Control (UAC) to protect the system from unauthorized changes and malware.
- Monitored and managed applications and processes using Task Manager.
- Developed the ability to securely interact with Windows at both user and administrative levels.
- Strengthened understanding of how core Windows components work together to maintain functionality and security.
