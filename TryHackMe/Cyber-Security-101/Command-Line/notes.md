# Windows Command Line

## Introduction
- GUIs are intuitive; CLIs are faster and more efficient once mastered.  
- CLI advantages: lower resource usage, easy automation, better for remote/headless systems.  
- Common CLI benefits: repeatable commands, scripting, quicker troubleshooting.  
- This room focuses on `cmd.exe` for: showing system info, network troubleshooting, file/folder management, and process inspection.  
- Prerequisite: Windows & Active Directory fundamentals recommended.


## Basic System Info

**Concepts Learned**  
- Commands must be executed within Windows PATH.  
- Methods to check OS version and detailed system info.  
- Tricks to handle long output in CLI.

**Commands**  
- `set` → Displays environment variables and PATH.  
- `ver` → Shows Windows version.  
- `systeminfo` → Detailed system info (OS, build, processor, memory).  
- `driverquery` → List installed drivers.  
- `driverquery | more` → View driver list page by page.  
- `help` → Help for a specific command.  
- `cls` → Clear the Command Prompt screen.

**Notes**  
- Always check the PATH to ensure commands execute correctly.  
- Use `systeminfo` to gather host details, useful for reconnaissance in pentesting.  
- Pipe output through `more` for readability when dealing with long results.  
- `ver` is a quick check for OS version; `systeminfo` gives deeper insight.


## Network Troubleshooting

**Concepts Learned**  
- How to view current network configuration and troubleshoot connectivity issues.  
- Methods to check IP address, subnet mask, default gateway, DNS servers, and DHCP status.  
- Tools to test connectivity and trace network paths.  
- Methods to inspect active connections and associated processes.  

**Commands**  
- `ipconfig` → Shows basic network configuration (IP, subnet, gateway).  
- `ipconfig /all` → Detailed network info including DNS servers and DHCP.  
- `ping <target>` → Test connectivity to a host and measure round-trip time.  
- `tracert <target>` → Trace the route packets take to reach a host.  
- `nslookup <domain>` → Resolve domain names to IP addresses.  
- `nslookup <domain> <server>` → Use a specific DNS server for lookup.  
- `netstat` → Displays active connections and listening ports.  
- `netstat -a` → All established connections and listening ports.  
- `netstat -b` → Show executable associated with each connection.  
- `netstat -o` → Show PID associated with each connection.  
- `netstat -n` → Show numerical addresses and ports.  
- `netstat -abon` → Combine all options (-a -b -o -n) for detailed view.  

**Notes**  
- `ping` helps verify connectivity to a host; successful replies indicate reachability.  
- `tracert` shows all hops to the target; useful for diagnosing routing issues.  
- `nslookup` can query different DNS servers; helps verify name resolution.  
- `netstat -abon` is essential in pentesting to identify listening services, associated executables, and PIDs.  
- Long command outputs can be piped through `more` for easier viewing.


## File and Disk Management

**Concepts Learned**  
- Navigating directories and drives using the command line.  
- Viewing directory contents including hidden and system files.  
- Creating, deleting, and organizing directories.  
- Viewing and managing file contents.  
- Copying, moving, and deleting files, including using wildcards for multiple files.  

**Commands**  
- `cd` → Display current directory or change to target directory.  
- `cd ..` → Move up one directory level.  
- `dir` → List contents of current directory.  
- `dir /a` → Include hidden and system files.  
- `dir /s` → Include all subdirectories.  
- `tree` → Visual representation of directory and subdirectory structure.  
- `mkdir <directory_name>` → Create a new directory.  
- `rmdir <directory_name>` → Remove a directory.  
- `type <file_name>` → Display contents of a text file.  
- `more <file_name>` → Display long files page by page.  
- `copy <source> <destination>` → Copy files.  
- `move <source> <destination>` → Move files.  
- `del <file_name>` or `erase <file_name>` → Delete a file.  
- `*` (wildcard) → Apply commands to multiple files, e.g., `copy *.md C:\Markdown`.  

**Notes**  
- Use `cd` without arguments to confirm your current path.  
- Combining `dir` options helps inspect all files, including hidden/system files.  
- `tree` is helpful for visualizing folder hierarchy.  
- `more` is useful for reading large text files without flooding the terminal.  
- Wildcards make bulk file operations efficient (e.g., copy, delete multiple files at once).  
- Always verify the path before deleting or moving files to avoid accidental data loss.  


## Task and Process Management

**Concepts Learned**  
- Listing running processes using the command line.  
- Filtering and searching processes by name or other attributes.  
- Terminating processes using the process ID (PID).  
- Managing system resources without relying on Task Manager.  

**Commands**  
- `tasklist` → Display all running processes.  
- `tasklist /FI "imagename eq <process_name>"` → Filter processes by name.  
- `taskkill /PID <pid>` → Terminate a process using its PID.  
- `taskkill /IM <image_name>` → Terminate a process by its image name.  
- `taskkill /F /PID <pid>` → Forcefully terminate a process.  

**Notes**  
- Use filters with `tasklist` to quickly find specific processes, especially when the list is long.  
- Knowing the PID is important for terminating the correct process without affecting critical system tasks.  
- Forceful termination (`/F`) should be used cautiously to avoid system instability.  
- Combine filtering and taskkill to efficiently manage tasks, similar to what Task Manager does graphically.  


## Key Takeaways
- CLI mastery allows faster and more efficient system interactions compared to GUI.  
- You can retrieve detailed system and network information using commands like `systeminfo`, `ipconfig`, `ping`, `tracert`, `nslookup`, and `netstat`.  
- File and directory management is easily handled with commands like `cd`, `dir`, `mkdir`, `rmdir`, `copy`, `move`, and `del`.  
- Task and process management is possible with `tasklist`, `taskkill`, and filtering options for precision.  
- Command-line skills support automation, remote administration, and troubleshooting, essential for Windows administration and penetration testing.


