# Cheatsheet - Linux Shells

| Category | Command / Syntax | Description |
|----------|----------------|-------------|
| **Navigation** | `pwd` | Print current working directory |
|  | `cd <directory>` | Change directory |
|  | `cd ..` | Go up one directory level |
|  | `ls` | List files and directories |
|  | `ls -a` | List all files including hidden |
|  | `ls -l` | Detailed list with permissions |
|  | `tree` | Visual directory tree |
| **File Operations** | `cat <file>` | Display file content |
|  | `cp <src> <dest>` | Copy file |
|  | `mv <src> <dest>` | Move or rename file |
|  | `rm <file>` | Delete file |
|  | `touch <file>` | Create empty file |
|  | `mkdir <directory>` | Create directory |
|  | `rmdir <directory>` | Remove empty directory |
| **Search** | `grep <pattern> <file>` | Search for a pattern in file |
|  | `find <path> -name <file>` | Search files by name |
| **Shell Info** | `echo $SHELL` | Display current shell |
|  | `cat /etc/shells` | List all installed shells |
|  | `chsh -s /path/to/shell` | Change default shell |
| **Scripting** | `#!/bin/bash` | Shebang to define interpreter |
|  | `chmod +x <script.sh>` | Make script executable |
|  | `./<script.sh>` | Run script in current directory |
| **Variables** | `name="value"` | Assign value to a variable |
|  | `$name` | Access variable value |
| **Loops** | `for i in {1..10}; do <commands>; done` | Repeat commands multiple times |
| **Conditionals** | `if [ condition ]; then <commands>; else <commands>; fi` | Execute code based on condition |
| **Comments** | `# comment` | Add comments for readability |

