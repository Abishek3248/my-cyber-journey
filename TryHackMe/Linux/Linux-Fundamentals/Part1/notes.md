# Linux Fundamentals - Part 1

## Introduction & Background

### Concepts Learned
- Linux is an open-source OS based on UNIX, lighter than Windows.  
- Used in websites, cars, PoS systems, and critical infrastructure.  
- Distributions (Ubuntu, Debian, etc.) serve different purposes like servers, desktops, or embedded systems.  
- Ubuntu Server can run on as little as **512MB RAM**.  

### Commands
*(No commands in this section.)*

### Notes
- First Linux release: **1991**.  
- Realized Linux is far more common in daily life than I thought.  


## Using the Linux Machine

### Concepts Learned
- THM provides an Ubuntu machine in-browser for practice.  
- Includes IP address, expiry timer, and machine controls.  
- Always terminate machines when finished.  

### Commands
*(No new commands in this section.)*

### Notes
- Already familiar with remote Linux access from Bandit, so this step felt straightforward.  
- Marked the milestone: **Deployed my first Linux machine in THM**.  


## Basic Commands

### Concepts Learned
- Linux systems can be lightweight and may not have a GUI; interaction is often via the **Terminal** (text-based interface).  
- Terminal usage allows navigation, file management, and executing commands.  
- First commands introduced in THM: `echo` and `whoami`, previously used in Bandit but now formally documented.

### Commands
- `echo <text>` → prints text to the terminal.  
  - Example: `echo "Hello Friend!"` → outputs *Hello Friend!* (quotes needed if spaces are present).  
  - Previously used in Bandit; now formally documented.  
- `whoami` → shows the current logged-in user.  
  - Previously used in Bandit; now formally documented.

### Notes
- Practiced and formally documented basic commands (`echo`, `whoami`) used in Bandit, reinforcing proper usage and syntax.  
- THM provided a structured way to revisit and consolidate these commands.


## Interaction with the Filesystem

### Concepts Learned
- Navigating the filesystem is crucial when using Linux without a GUI.  
- Core filesystem commands allow us to list files, change directories, view file contents, and find the current path.  
- Practiced and reinforced skills with `ls`, `cd`, and `cat`; learned `pwd` to explicitly display the full path.

### Commands
- `ls` → list files and directories in the current location.  
- `cd <directory>` → change to a different directory.  
- `cat <file>` → output the contents of a file.  
- `pwd` → print the full path of the current working directory.  

### Notes
- THM provided a structured overview of filesystem interaction.  
- Reinforced practical skills previously gained from Bandit while learning the importance of `pwd`,
  Useful even if the path is partially visible in the prompt.



## Searching for Files

### Concepts Learned
- Linux allows efficient searching of files and content without manually navigating directories.  
- Reinforced commands `find` and `grep`, which were **very useful and frequently used in Bandit**
  
### Commands
- `find -name <filename>` → search for files by name within the current directory and its subdirectories.  
- `grep "<pattern>" <file>` → search for a specific string or pattern within a file.  

### Notes
- THM emphasized structured usage of `find` and `grep` to efficiently locate files and search their contents.  
- Reinforced practical skills from Bandit.  
- Understanding these commands improves efficiency in navigating and managing Linux systems.



## Introduction to Shell Operators

### Concepts Learned
- Explored basic Linux shell operators to enhance command efficiency.  
- Learned how to run commands in the background, combine multiple commands, and redirect output to files.  

### Operators
- `&` → run a command in the background, allowing the terminal to remain free for other tasks.  
- `&&` → combine multiple commands; the second command runs only if the first succeeds.  
- `>` → redirect command output to a file, **overwriting** existing contents.  
- `>>` → redirect command output to a file, **appending** to existing contents.

### Notes
- THM provided practical examples of using operators with commands like `echo` and `cat`.  
- Operators explored improve efficiency and control when working in the Linux shell.  
- Only the `>` operator was previously encountered in Bandit; the others were new explorations.



## Key Takeaways
- Linux is widely used across servers, embedded systems, and critical infrastructures.  
- Gained hands-on experience interacting with a Linux machine in-browser.  
- Reinforced fundamental commands (`echo`, `whoami`, `ls`, `cd`, `cat`) and learned `pwd` for current directory paths.  
- Explored searching files efficiently using `find` and `grep`.  
- Learned basic shell operators (`&`, `&&`, `>`, `>>`) to enhance command-line efficiency.  
- Frequent practice helps build familiarity and confidence with Linux commands and navigation.

