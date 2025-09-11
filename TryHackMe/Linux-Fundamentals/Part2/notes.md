## Introduction
Part 2 builds on Part 1 by introducing working with **remote terminals**, using **flags and arguments** with commands, **advanced filesystem operations**, **file access management**, and running **scripts and executables**.


## Concept: Accessing Your Linux Machine Using SSH

### Concepts Learned
- SSH (Secure Shell) is the standard protocol for **remotely connecting to Linux machines**.  
- All communication over SSH is **encrypted** for security.  
- Commands executed after connecting run on the **remote machine**.  
- SSH is a **fundamental skill**, used extensively in Bandit for logging into successive user accounts.

### Commands
- `ssh username@IP_ADDRESS` — Connect to a remote Linux machine.  
  *Example:* `ssh tryhackme@MACHINE_IP`

### Notes
- Password input may not show feedback; this is normal.  
- SSH is a fundamental skill that was applied extensively in Bandit, reinforcing practical experience with remote system access.



## Concept: Flags and Switches

### Concepts Learned
- Many Linux commands accept **arguments** known as **flags or switches** to modify their default behavior.  
- Flags are typically preceded by a hyphen (`-`) for short options or two hyphens (`--`) for long options.  
- The `--help` flag can be used with most commands to **display available options and usage instructions**.  
- Manual pages (**man pages**) provide **detailed documentation** for Linux commands and applications.  
- Understanding flags and switches **enhances command flexibility**, a skill reinforced in Bandit through practical use.

### Commands
- `ls -a` — Lists all files, including hidden files (those starting with `.`).  
- `ls --help` — Displays a help menu listing available flags and their descriptions.  
- `man <command>` — Opens the manual page for a given command.  
  *Example:* `man ls`  

### Notes
- By default, `ls` only shows non-hidden files; `-a` reveals hidden ones.  
- Flags can be combined with commands to customize output (e.g., `ls -la`).  
- Manual pages are a **reliable source** for understanding command functionality and available flags.  
- Prior experience in Bandit familiarized you with using flags like `-a` and `-l` for efficient navigation and file inspection.



## Concept: Managing Files and Directories

### Concepts Learned
- Expanded practical skills for interacting with the Linux filesystem.  
- Learned to create, move, copy, and delete files and directories.  
- Determining file types to understand contents without relying on extensions.  
- Reinforced commands already frequently used in Bandit (`touch`, `mkdir`, `cp`, `mv`, `rm`, `file`).  

### Commands
- `touch` – used to create a new blank file (e.g., `touch note`).  
- `mkdir` – used to create a new directory/folder.  
- `cp` – used to copy files or directories.  
- `mv` – used to move or rename files or directories.  
- `rm` – used to remove files or directories (with `-R` for folders).  
- `file` – used to determine the type of a file.  

### Notes
- We now have the ability to **interact with files and directories more effectively**. Creating new files or folders allows us to organize information, while copying and moving helps manage and restructure the filesystem. Deleting files or directories removes unnecessary data and keeps the system tidy.
- The `file` command is particularly useful when file extensions are missing or misleading, allowing us to understand the contents and purpose of a file before attempting to read or execute it.
- Many of these commands were applied throughout Bandit, giving practical familiarity with filesystem management. This reinforces prior knowledge while allowing us to handle larger tasks efficiently, such as organizing, modifying, or inspecting files on a Linux machine.



## File Permissions and User Management
### Concepts Learned
- Linux permissions control which users can access or modify files and folders.
- Each file/folder has three main permission types: Read, Write, Execute.
- Users and groups can have different sets of permissions for the same file/folder.
- Permissions allow fine-grained control, essential for multi-user environments like servers.
- Switching between users is performed using the su command, optionally with the -l (login) switch to inherit the new user’s environment.

### Commands
- ls -l — View detailed file/folder permissions.
- su user — Switch to another user account.
- su -l user — Switch to another user and inherit their login environment.
- Example:
      su -l user2
      Password:
      user2@linux2:~$ pwd
      /home/user2

### Notes
- Using ls -l shows the permission string (e.g., -rw-r--r--) which indicates read/write/execute permissions for owner, group, and others.
- User ownership and group ownership determine who can perform actions on the file.
- Switching users with su allows you to test permissions or perform actions as another user.
- The -l switch ensures the session mimics a real login of that user, including environment variables and the home directory.
- These concepts are applied frequently in Bandit, where checking file permissions and switching users is critical to progressing through levels.



## Common Directories
###  Concepts Learned

- Linux systems have a hierarchical directory structure, with certain root directories serving specific purposes. Understanding these directories is important for navigation, administration, and security assessments.
- /etc: Stores system-wide configuration files. Important files include sudoers (permissions for sudo), passwd and shadow (user accounts and encrypted passwords).
- /var: Short for “variable,” this directory stores data frequently written by services or applications, such as logs, temporary files, or databases.
- /root: Home directory for the root user, accessible only by root.
- /tmp: Temporary directory, cleared on reboot. Writable by all users, useful for temporary files or pentesting scripts.

### Commands
 <No specific commands used for this topic.>

### Notes
- These directories are essential to understand when navigating a Linux system. Knowing their purpose helps locate configuration files, logs, temporary data, and understand user-specific directories. Familiarity with these directories also aids in tasks such as enumeration or pentesting, as they often store sensitive or important data.


## Key Takeaway
- Connecting to remote Linux machines using SSH.
- Using flags and switches to extend command functionality and reading man pages.
- Performing advanced filesystem interactions: creating, moving, copying, and removing files/folders.
- Understanding file permissions and switching between users.
- Familiarity with important root directories (/etc, /var, /root, /tmp) and their uses.
