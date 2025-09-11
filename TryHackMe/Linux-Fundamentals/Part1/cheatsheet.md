# Linux Fundamentals - Part 1 Cheatsheet

## Basic Commands
| Command        | Description                        | Example                  |
|----------------|------------------------------------|--------------------------|
| `echo <text>`  | Output text to terminal            | `echo Hello`             |
| `whoami`       | Show current user                  | `whoami`                 |
| `ls`           | List files/directories             | `ls`                     |
| `cd <dir>`     | Change to directory                | `cd Documents`           |
| `cat <file>`   | Display contents of a file         | `cat todo.txt`           |
| `pwd`          | Print current directory path       | `pwd`                    |

## Searching Files
| Command                     | Description                       | Example                     |
|------------------------------|-----------------------------------|-----------------------------|
| `find -name <filename>`      | Search for file by name           | `find -name passwords.txt`  |
| `grep "<pattern>" <file>`    | Search string/pattern in a file  | `grep "error" access.log`   |

## Shell Operators
| Operator | Description                                      | Example                    |
|----------|--------------------------------------------------|----------------------------|
| `&`      | Run command in background                        | `sleep 10 &`               |
| `&&`     | Combine commands; second runs if first succeeds | `echo hi && ls`            |
| `>`      | Redirect output to a file (overwrite)           | `echo hi > file.txt`       |
| `>>`     | Redirect output to a file (append)              | `echo hi >> file.txt`      |

