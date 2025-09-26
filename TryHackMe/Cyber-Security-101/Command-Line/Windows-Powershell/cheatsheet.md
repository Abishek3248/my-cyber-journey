# Cheatsheet - Powershell Command Line

## Basics & Launch
| Cmdlet / Concept | Description / Usage | Example |
|-----------------|-------------------|---------|
| Launch PowerShell | Start PowerShell via GUI, Run, File Explorer, Task Manager, or cmd.exe | `powershell` |
| Cmdlet Structure | Verb-Noun naming convention | `Get-Content`, `Set-Location` |

## Help & Discovery
| Cmdlet / Concept | Description / Usage | Example |
|-----------------|-------------------|---------|
| `Get-Help` | Show usage, syntax, and examples of a cmdlet | `Get-Help Get-Date -Examples` |
| `Get-Command` | List all available cmdlets, functions, aliases | `Get-Command` |
| `Get-Alias` | Show alias names for cmdlets | `Get-Alias` |

## File System Navigation
| Cmdlet / Concept | Description / Usage | Example |
|-----------------|-------------------|---------|
| `Get-ChildItem` | List files and directories | `Get-ChildItem` |
| `Set-Location` | Change directory | `Set-Location .\Documents` |
| `New-Item` | Create files or directories | `New-Item -Path .\file.txt -ItemType File` |
| `Remove-Item` | Delete files or directories | `Remove-Item -Path .\file.txt` |
| `Copy-Item` | Copy files or directories | `Copy-Item -Path file.txt -Destination file2.txt` |
| `Move-Item` | Move files or directories | `Move-Item -Path file.txt -Destination ..\` |
| `Get-Content` | Read/display file contents | `Get-Content file.txt` |

## Piping, Filtering & Sorting
| Cmdlet / Concept | Description / Usage | Example |
|-----------------|-------------------|---------|
| Piping `|` | Pass objects from one cmdlet to another | `Get-ChildItem | Sort-Object Length` |
| `Sort-Object` | Sort objects by property | `Sort-Object Length` |
| `Where-Object` | Filter objects by condition | `Where-Object -Property Extension -eq ".txt"` |
| `Select-Object` | Select specific object properties or limit results | `Select-Object Name, Length` |
| `Select-String` | Search for text patterns in files | `Select-String -Path file.txt -Pattern "hat"` |

### Comparison Operators
| Operator | Description |
|---------|-------------|
| `-eq` | Equal to |
| `-ne` | Not equal to |
| `-gt` | Greater than |
| `-ge` | Greater than or equal to |
| `-lt` | Less than |
| `-le` | Less than or equal to |
| `-like` | Pattern match |

## System Info
| Cmdlet / Concept | Description |
|-----------------|-------------|
| `Get-ComputerInfo` | Comprehensive system info |
| `Get-LocalUser` | List local users |
| `Get-NetIPConfiguration` | Show network interface info |
| `Get-NetIPAddress` | Show all IP addresses |

## Real-Time System Analysis
| Cmdlet / Concept | Description |
|-----------------|-------------|
| `Get-Process` | View running processes |
| `Get-Service` | View service status |
| `Get-NetTCPConnection` | View active TCP connections |
| `Get-FileHash` | Generate file hash for integrity check |

## Scripting & Remote Commands
| Cmdlet / Concept | Description / Usage | Example |
|-----------------|-------------------|---------|
| Scripting | Automate tasks via text files | - |
| `Invoke-Command` | Run commands/scripts on remote systems | `Invoke-Command -ComputerName RoyalFortune -ScriptBlock { Get-Service }` |
