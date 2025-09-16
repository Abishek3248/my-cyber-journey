# Cheatsheet - Windows Fundamentals Part3

| Feature / Tool                  | Purpose / Description | Key Points / Commands |
|---------------------------------|--------------------|---------------------|
| **Windows Update**               | Keeps system and Microsoft products updated with security patches and feature updates | Patch Tuesday (2nd Tuesday each month); `control /name Microsoft.WindowsUpdate` |
| **Windows Security**             | Central hub for device and data protection | Protection areas: Virus & threat protection, Firewall & network protection, App & browser control, Device security |
| **Virus & Threat Protection**    | Detects and manages malware | Scan options: Quick, Full, Custom; Threat history: Quarantined, Allowed; Settings: Real-time protection, Controlled folder access |
| **Windows Defender Firewall**    | Controls network traffic | Profiles: Domain, Private, Public; Command: `WF.msc`; Can allow/block apps per profile |
| **SmartScreen**                  | Protects against phishing/malware sites and apps | Checks apps & files; Exploit protection built-in |
| **Core Isolation / Memory Integrity** | Hardware-level protection against code injection attacks | Default settings recommended; uses TPM when available |
| **TPM (Trusted Platform Module)**| Secure crypto-processor for encryption and device integrity | Works with BitLocker for best protection |
| **BitLocker**                     | Full-disk encryption to protect data | Best with TPM v1.2+; encrypts offline and lost/stolen devices; VM may not include feature |
| **Volume Shadow Copy Service (VSS)** | Creates restore points / snapshots for system recovery | Stores copies in System Volume Information; allows restore, configure, or delete restore points |

