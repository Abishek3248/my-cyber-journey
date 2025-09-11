# Linux Fundamentals - Part 2 Cheatsheet

## SSH & Remote Access
| Command / Concept | Description                          | Example / Notes               |
|------------------|--------------------------------------|-------------------------------|
| `ssh`            | Connect to remote machine securely    | `ssh username@IP_ADDRESS`     |

## Flags & Manual Pages
| Command / Concept | Description                          | Example / Notes               |
|------------------|--------------------------------------|-------------------------------|
| `ls`             | List directory contents, can use flags | `ls -a` (show hidden files)  |
| `man`            | Access manual pages for commands     | `man ls`                      |

## Filesystem Interaction
| Command / Concept | Description                          | Example / Notes               |
|------------------|--------------------------------------|-------------------------------|
| `touch`          | Create a new file                     | `touch note`                  |
| `mkdir`          | Create a new directory                | `mkdir mydirectory`           |
| `rm`             | Remove files or directories           | `rm file.txt`, `rm -R folder`|
| `cp`             | Copy files or directories             | `cp file1 file2`              |
| `mv`             | Move or rename files/directories      | `mv file1 newname`            |
| `file`           | Determine type of a file              | `file note`                   |

## User Management & Permissions
| Command / Concept | Description                          | Example / Notes               |
|------------------|--------------------------------------|-------------------------------|
| `su`             | Switch user                           | `su -l user2`                 |
| File Permissions  | Check read, write, execute access    | `ls -lh` (view permissions)  |

## Common Root Directories
| Directory | Description                             | Notes                           |
|-----------|-----------------------------------------|---------------------------------|
| `/etc`    | System configuration files              | `sudoers`, `passwd`, `shadow`  |
| `/var`    | Variable data; logs, databases         | `backups`, `log`, `tmp`        |
| `/root`   | Home directory of root user             | `myfile`, `myfolder`           |
| `/tmp`    | Temporary files, cleared on reboot     | `todelete`, `trash.txt`, `rubbish.bin` |
