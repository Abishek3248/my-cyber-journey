## Windows Command Line Cheatsheet

| Concept                  | Command / Syntax                                  | Notes / Description |
|---------------------------|--------------------------------------------------|-------------------|
| **Check OS Version**      | `ver`                                            | Displays Windows version |
| **System Information**    | `systeminfo`                                     | Detailed system info (OS, RAM, CPU, etc.) |
| **View Environment Path** | `set`                                            | Check system paths where commands are executed |
| **Clear Screen**          | `cls`                                            | Clears the Command Prompt window |
| **Help**                  | `help`                                           | Lists available commands or help for a specific command |
| **Network Info**          | `ipconfig`                                       | Displays IP, subnet, gateway |
| **All Network Details**   | `ipconfig /all`                                  | Shows DNS, DHCP info, MAC address, etc. |
| **Ping**                  | `ping <target>`                                  | Test connectivity to a host |
| **Trace Route**           | `tracert <target>`                               | Shows the path packets take to a host |
| **DNS Lookup**            | `nslookup <domain>`                               | Resolves domain names to IP |
| **List Connections**      | `netstat`                                        | Shows active network connections |
| **Detailed Connections**  | `netstat -abon`                                  | Displays connections, ports, PIDs, programs |
| **View Current Directory**| `cd`                                             | Shows current working directory |
| **List Directory Files**  | `dir`                                            | Lists files and folders |
| **List Hidden/System Files** | `dir /a`                                      | Shows hidden/system files |
| **List All Subdirectories** | `dir /s`                                       | Lists files in all subdirectories |
| **Visual Directory Tree** | `tree`                                           | Graphical view of folders |
| **Change Directory**      | `cd <folder>`                                    | Navigate to target folder |
| **Create Directory**      | `mkdir <folder>`                                 | Makes a new folder |
| **Remove Directory**      | `rmdir <folder>`                                 | Deletes a folder |
| **View File Contents**    | `type <file>`                                    | Displays file content |
| **View Long Files Page-by-Page** | `more <file>`                               | Useful for large files |
| **Copy Files**            | `copy <source> <destination>`                    | Copies file to target location |
| **Move Files**            | `move <source> <destination>`                    | Moves file to target location |
| **Delete Files**          | `del <file>` or `erase <file>`                   | Deletes specified file |
| **List Processes**        | `tasklist`                                       | Lists running processes |
| **Filter Processes**      | `tasklist /FI "imagename eq <process>"`         | Show specific process info |
| **Kill Process**          | `taskkill /PID <pid>`                            | Terminates a process using PID |

