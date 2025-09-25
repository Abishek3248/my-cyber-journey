# Linux Shells

## Introduction
- CLI allows direct interaction with the OS, offering more control than GUI.
- Shells guide users in executing commands efficiently.
- Using CLI is faster, more resource-friendly, and supports automation.


## Interact with Shell

**Concepts Learned**
- Default Linux shell is usually Bash.
- Current working directory (cwd) matters when performing operations.
- Viewing directory contents and reading files in shell.
- Searching for patterns or keywords in files.

**Commands**
- `pwd` – Print current working directory.
- `cd <directory>` – Change to specified directory.
- `ls` – List contents of the current directory.
- `cat <filename>` – Display file contents.
- `grep <pattern> <filename>` – Search for a specific pattern in a file.

**Notes**
- By default, terminal opens in home directory.
- `pwd` helps confirm your current location.
- Use `cd` to navigate directories.
- `ls` shows files and subdirectories; combine with options like `-l` or `-a` for more details.


## Types of Linux Shells

**Concepts Learned**
- Linux supports multiple shells, each with unique features.
- Default shell is usually Bash; other popular shells include Fish and Zsh.
- Shells can be switched temporarily or set as default permanently.
- Feature comparison helps choose the best shell for your needs.

**Commands**
- `echo $SHELL` – Display the current shell.
- `cat /etc/shells` – List all available shells on the system.
- `<shell_name>` – Switch to another shell temporarily (e.g., `zsh`).
- `chsh -s /path/to/shell` – Change default shell permanently.

**Notes**
- **Bash (Bourne Again Shell)**: Default in most distributions, supports scripting, tab completion, command history.
- **Fish (Friendly Interactive Shell)**: Focuses on user-friendliness, auto spell correction, syntax highlighting, themes.
- **Zsh (Z Shell)**: Modern shell, highly customizable, supports advanced tab completion, scripting, and plugins.
- Choosing a shell depends on tasks, scripting needs, and personal preference.


## Shell Scripting and Components

**Concepts Learned**
- Shell scripts are a set of commands saved in a file to automate tasks.
- Scripts start with a shebang (`#!`) to define the interpreter.
- Scripts use **variables** to store values for reuse.
- **Loops** allow repeated execution of commands.
- **Conditional statements** control the flow based on conditions.
- **Comments** improve readability and maintainability of scripts.

**Commands**
- `nano script_name.sh` – Create or edit a script file.
- `chmod +x script_name.sh` – Give execution permission to a script.
- `./script_name.sh` – Execute a script in the current directory.
- `echo $variable` – Display the value of a variable.
- `read variable` – Take user input and store in a variable.

**Notes**
- **Variables**: Store reusable data; accessed using `$variable_name`.
- **Loops**: Use `for` or `while` loops to iterate over values.
  # Example for loop
  for i in {1..10}; do
      echo $i
  done
- Conditional Statements: Use if, then, else, fi for decision making.
# Example conditional
 if [ "$name" = "Stewart" ]; then
     echo "Welcome Stewart!"
 else
     echo "Sorry! You are not Welcomed."
 fi
- Comments: Use # to write explanations without affecting script execution.
- Always use meaningful variable names and comments in complex parts of scripts.


## Practical Exercise

**Concepts Learned**
- Applying shell scripting knowledge in a real-world scenario.
- Running scripts as a normal user vs. root user.
- Modifying scripts to provide input values for automated tasks.
- Searching for specific content in files using scripts.

**Commands**
- `sudo su` – Switch to root user for full system access.
- `nano script_name.sh` – Open script file for editing.
- `./script_name.sh` – Execute the script in the current directory.

**Notes**
- The script searches for a keyword in `.log` files within a directory.
- Important variables in the script must be filled before execution:
  - **Flag:** `thm-flag01-script`
  - **Directory:** `/var/log`
- Use root privileges to access all files in protected directories.
- Ensure no spaces inside the quotation marks when inserting values in the script.
- This exercise reinforces the practical application of variables, loops, and conditional statements in a real Linux environment.


**Key Takeaways**
- Linux shells provide a powerful interface to interact with the operating system beyond the GUI, enabling faster and more efficient operations.  
- The default shell on most Linux distributions is Bash, but other shells like Fish and Zsh offer unique features, customization, and user-friendly options.  
- Basic shell commands (`pwd`, `cd`, `ls`, `cat`, `grep`) are essential for navigating directories, viewing file contents, and searching for patterns within files.  
- Shell scripting allows automation of repetitive tasks by combining multiple commands into a single executable script.  
- Shebang (`#!`) defines the interpreter for a script, ensuring consistent execution across environments.  
- Variables store values that can be reused, reducing redundancy and making scripts more maintainable.  
- Loops (`for`, `while`) help perform repeated actions efficiently, such as iterating over files or numbers.  
- Conditional statements (`if`, `else`, `elif`) enable decision-making within scripts, allowing execution of code based on specific conditions.  
- Comments (`#`) improve script readability and maintainability without affecting execution.  
- Practical exercises reinforce the ability to modify and execute scripts, apply root privileges when necessary, and manipulate files across the system.  
- Mastery of shell commands, scripting, and different shell types lays the groundwork for advanced Linux system administration, automation, and cybersecurity tasks.

- `cat` displays full file contents; `more` or `less` can be used for long files.
- `grep` extracts specific lines matching a pattern; extremely useful for large files.
