# Bash Scripting – Cheatsheet

| Concept | Usage / Syntax | Notes |
|---------|----------------|-------|
| **Basic Script** | `#!/bin/bash` | Required at the top of scripts |
| **Run Script** | `chmod +x script.sh` <br> `./script.sh` | Make executable and run |
| **Output** | `echo "text"` | Prints text or variable content |
| **Variable** | `name="Jammy"` <br> `$name` | No spaces around `=` |
| **Debugging** | `bash -x ./script.sh` <br> `set -x` / `set +x` | Shows command execution and errors |
| **Parameters** | `$1`, `$2`, ... <br> `read var` | Input via command-line or interactive |
| **Arrays** | `arr=('val1' 'val2')` <br> `${arr[0]}` <br> `${arr[@]}` <br> `unset arr[1]` | Index starts at 0, `@` for all elements |
| **Conditionals** | `if [ $var -eq 10 ]; then ... fi` | `-eq, -ne, -gt, -lt, -ge` |
| **File Checks** | `-f file`, `-w file` | Check if file exists and writable |
| **Logical Operators** | `&&`, `||` | Combine multiple conditions |
| **Interactive Input** | `read name` | Get user input during script execution |

