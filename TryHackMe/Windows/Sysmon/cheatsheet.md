# Cheatsheet - Sysmon

| Concept / Task                  | Tool / Event | Example Snippet / Rule | Notes |
|---------------------------------|--------------|----------------------|-------|
| **Process Creation**             | Sysmon ID 1  | `<ProcessCreate onmatch="include">` | Monitor full path, command line, parent process |
| **File Creation**                | Sysmon ID 11 | `<FileCreate onmatch="include">` | Useful for Startup, Start Menu, Temp, Downloads |
| **Registry Key Persistence**     | Sysmon ID 12 | `<RegistryEvent onmatch="include">` | CurrentVersion\Run, Group Policy Scripts |
| **Network Connections / RATs**   | Sysmon ID 3  | `<NetworkConnect onmatch="include"><DestinationPort condition="is">8080</DestinationPort></NetworkConnect>` | Exclude safe apps (e.g., OneDrive) to reduce noise |
| **LSASS Access / Mimikatz**      | Sysmon ID 10 | `<ProcessAccess onmatch="include"><TargetImage condition="image">lsass.exe</TargetImage></ProcessAccess>` | Exclude `svchost.exe` to filter normal events |
| **Remote Threads / Injection**   | Sysmon ID 8  | `<CreateRemoteThread onmatch="exclude"><SourceImage condition="is">svchost.exe</SourceImage></CreateRemoteThread>` | Detects DLL injection / reflective PE injection |
| **Alternate Data Streams (ADS)** | Sysmon ID 15 | `<FileCreateStreamHash onmatch="include"><TargetFilename condition="contains">Downloads</TargetFilename></FileCreateStreamHash>` | Hunt malware hiding in Temp / Downloads / .hta / .bat |
| **PowerShell: Filter Event by ID** | PS / Get-WinEvent | `Get-WinEvent -Path <Path> -FilterXPath '*/System/EventID=<ID>'` | Replace `<ID>` with Sysmon EventID |
| **PowerShell: Filter LSASS access** | PS / Get-WinEvent | `Get-WinEvent -Path <Path> -FilterXPath '*/System/EventID=10 and */EventData/Data[@Name="TargetImage"] and */EventData/Data="C:\Windows\system32\lsass.exe"'` | Hunt Mimikatz / credential dumping |
| **PowerShell: Filter RAT / C2 port** | PS / Get-WinEvent | `Get-WinEvent -Path <Path> -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort"] and */EventData/Data=<Port>'` | Replace `<Port>` with suspicious backconnect port |
| **PowerShell: Filter File / Registry / ADS** | PS / Get-WinEvent | Use `EventID` 11 / 12 / 15 with XPath to search specific filenames or registry keys | Combine with Sysmon config rules for precise hunting |
| **Startup Persistence Detection** | Sysmon ID 11 | `<FileCreate onmatch="include"><TargetFilename condition="contains">\Startup\</TargetFilename></FileCreate>` | Detect malicious executables in Startup folder |
| **Registry Persistence Detection** | Sysmon ID 12 | `<RegistryEvent onmatch="include"><TargetObject condition="contains">CurrentVersion\Run</TargetObject></RegistryEvent>` | Track scripts or binaries added to Run keys |
| **Hunting Malware / RATs** | Sysmon ID 3 | `<NetworkConnect onmatch="include"><DestinationPort condition="is">1034</DestinationPort></NetworkConnect>` | Include known suspicious ports, exclude safe applications |
| **Detect Evasion Techniques (ADS & Remote Threads)** | Sysmon ID 15 / 8 | `<FileCreateStreamHash onmatch="include">...<CreateRemoteThread onmatch="exclude">...</CreateRemoteThread>` | Detect files hidden in NTFS streams & thread injections |

