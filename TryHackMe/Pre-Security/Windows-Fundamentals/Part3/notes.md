# Windows Fundamentals part3

## Introduction
- In the previous two modules, we explored the core structure and utilities of the Windows operating system:
- Windows Fundamentals 1 – Covered the desktop, file system, user accounts, control panel, settings, and task manager.
- Windows Fundamentals 2 – Focused on system utilities such as System Configuration, Computer Management, Resource Monitor, and other administrative tools.
- Windows Fundamentals 3 will shift focus towards the security features of Windows, including permissions, processes, and services—essential knowledge for both system administration and cybersecurity.


## Windows Update

### Concepts Learned
- Windows Update provides security patches, feature enhancements, and updates for Windows and Microsoft products.
- Updates are usually released on Patch Tuesday (2nd Tuesday of each month).
- Critical updates may be released outside of Patch Tuesday.
- Updates in Windows 10+ cannot be ignored indefinitely—they can only be postponed.

### Explanation
- Windows Update is Microsoft’s built-in service for keeping the operating system and related products secure and up to date.
It can be accessed via:
- *Settings > Update & Security > Windows Update*
- Or by running control /name Microsoft.WindowsUpdate from Run/CMD.
- Updates often require a system restart. In Windows 10 and newer versions, Microsoft enforces updates to ensure security—users can postpone but not permanently avoid them.

### Notes
- Updates include security patches, driver updates, Defender updates, and OS improvements.
- Managed devices (e.g., enterprise environments) may show a message that updates are controlled by the organization.
- Restart options allow scheduling reboots at a convenient time.
- Microsoft Security Update Guide: official source for update details.


## Windows Security

### Concepts Learned
- Windows Security is the central hub for managing tools that protect the system and data.
- Found in Settings → Update & Security → Windows Security.
**Main Protection areas:**
- Virus & Threat Protection
- Firewall & Network Protection
- App & Browser Control
- Device Security
**Status icons meaning:**
- Green → Device protected, no issues.
- Yellow → Recommendations to review.
- Red → Immediate attention required.

### Explanation
- Windows Security consolidates protection features into one place for easier management.
- Provides real-time feedback on the health and protection level of the system.
- Focus areas (Virus protection, Firewall, App control, and Device security) give visibility into different aspects of defense.
- Icons act as quick indicators for the user to know whether immediate action is required or not.
- Visual layout differs between Windows 10 and Windows Server 2019, but features largely remain the same.

### Notes
- Access via Settings or directly with Windows Security app.
- Essential for maintaining system safety and compliance.
- Quick color-coded indicators simplify security management.


## Virus & Threat Protection

### Concepts Learned
- Virus & Threat Protection is divided into:
- Current Threats → shows scan options & threat history.
- Protection Settings → manage real-time defense, cloud updates, exclusions, etc.
- Offers multiple scan modes (Quick, Full, Custom).
- Provides real-time protection features like ransomware defense & cloud-delivered updates.
- Caution when allowing threats or excluding files, as it may compromise system safety.

### Explanation
- **Current Threats**
**Scan options:**
- Quick scan → checks common threat locations.
- Full scan → checks all files/programs (can take >1 hr).
- Custom scan → user-defined scan locations.
**Threat history:**
- Last scan → shows last automatic scan by Defender.
- Quarantined threats → isolated from running.
- Allowed threats → manually permitted (high risk).
- Virus & Threat Protection Settings
- Real-time protection → blocks malware at runtime.
- Cloud-delivered protection → faster detection via Microsoft cloud.
- Automatic sample submission → shares suspicious files with Microsoft.
- Controlled folder access → protects sensitive files/folders.
- Exclusions → skip selected items (dangerous if misused).
- Notifications → alerts about system health & threats.
- Updates & Ransomware Protection
- Check for updates → refresh Defender definitions manually.
- Ransomware protection → requires Controlled Folder Access + Real-time protection.
- Tip: Right-click any file/folder → “Scan with Microsoft Defender” for on-demand scans.

### Notes
- Real-time protection must always be enabled on personal devices.
- Updates usually happen automatically; manual checks ensure latest definitions.
- Exclusions and Allowed threats should be used only with 100% certainty.
- Defender integrates tightly with Windows for baseline protection, reducing need for 3rd party AV.


## Firewall And Network Protection

### Concepts Learned
- A firewall controls traffic flow through ports, acting like a security guard.
- Windows Firewall has three profiles: Domain, Private, and Public.
- Users can allow/block apps, but advanced configuration is for experienced users.
- Command to open Firewall: wf.msc.

### Explanation
- Controls inbound/outbound traffic through network ports.
- Prevents unauthorized access and enforces security rules.
**Firewall Profiles**
- Domain → Active when system authenticates with a domain controller (work/corporate).
- Private → User-assigned for trusted networks (home).
- Public → Default for untrusted networks (coffee shops, airports).
**Profile Options**
- Turn firewall on/off.
- Block all incoming connections (stricter security).
- Recommendation: Keep firewall enabled unless fully confident.
**Allowing Apps Through Firewall**
- Apps can be allowed access on Private or Public networks.
- The “Details” button may give extra info on why the app needs access.
**Advanced Settings**
- Used for fine-grained control (inbound/outbound rules, port rules).
- Recommended for advanced users only.
- Tip : Run wf.msc to open Windows Defender Firewall directly.

### Notes
- Public networks = highest risk → keep firewall ON.
- Misconfigured firewall rules can expose system vulnerabilities.
- Always verify apps before allowing them through.
- Advanced firewall configuration is typically handled by IT/security professionals.


## App & Browser Control

### Concepts Learned
- Microsoft Defender SmartScreen protects against malicious websites, apps, and downloads.
- Provides options to check apps/files and block potentially harmful content.
- Includes Exploit Protection to mitigate attacks.
- Best practice: Keep default settings unless fully confident.

### Explanation
**SmartScreen Protection**
- Helps defend against phishing, malware websites, and unsafe downloads.
- Checks unrecognized apps/files from the web to prevent accidental execution of malicious software.
**Exploit Protection**
- Built into Windows 10 and Windows Server 2019.
- Protects against common exploit techniques used by attackers.
- Operates in the background with minimal user interaction.
**Important Note**
- Default settings are designed for strong protection.
- Misconfiguration may weaken system defenses → leave unchanged unless you know exactly what you’re doing.

### Notes
- SmartScreen is an extra layer of defense against social engineering attacks.
- Exploit protection is part of system-hardening in Windows.
- Disabling these features can expose the device to malware and exploits.


## Device Security

### Concepts Learned
- Core Isolation adds virtualization-based protection to critical system processes.
- Memory Integrity prevents injection of malicious code into high-security processes.
- Trusted Platform Module (TPM) provides hardware-based cryptographic operations for stronger security.
- Default settings should not be changed unless fully understood.

### Explanation
- Core Isolation & Memory Integrity
- Core isolation uses virtualization to isolate sensitive processes from the rest of the OS.
- Memory integrity ensures attackers cannot easily inject malicious code into protected processes.
- Security Processor (TPM)
- TPM is a dedicated hardware chip used for encryption and secure operations.
**Provides features such as:**
- BitLocker drive encryption support.
- Secure key storage.
- Hardware-level protection against tampering.
- Malicious software cannot interfere with TPM’s protected cryptographic functions.

### Notes
- Core Isolation → strengthens OS-level defense.
- TPM → hardware-based security, resistant to tampering.
- Device Security = combination of virtualization-based protections and hardware safeguards.
- Recommended: Always keep default settings enabled for maximum protection.


## BitLocker

### Concepts Learned
- BitLocker provides encryption to protect data from theft or exposure.  
- Works best when paired with a Trusted Platform Module (TPM).  
- Designed for securing data on lost, stolen, or improperly decommissioned computers.  

### Explanation
- BitLocker Drive Encryption is a Microsoft feature that integrates with the operating system to provide **data protection**.  
**Its primary purpose is to mitigate risks of **data theft or exposure** in scenarios such as:**  
- Lost or stolen devices.  
- Systems being decommissioned without proper data wiping.  
**When a device is equipped with a **Trusted Platform Module (TPM)** chip (v1.2 or later), BitLocker offers maximum protection. The TPM ensures that:** 
- The system has not been tampered with while offline.  
- Encryption keys are securely stored in hardware.  
- This combination strengthens the integrity and security of the device.  

### Notes
- BitLocker works at the **disk encryption level**, securing entire drives rather than just files.  
- Requires administrator rights to enable and configure.  
- Not available in all Windows editions (e.g., not included in the attached VM).  
- Best practice: Use BitLocker **with TPM** for hardware-backed protection.  


## Volume Shadow Copy Service (VSS)

### Concepts Learned
- VSS creates consistent snapshots (shadow copies) of data for backup and recovery.
- Shadow copies are stored in the System Volume Information folder.
- Enables restore points and system recovery options.
- Attackers often target and delete shadow copies to prevent recovery during ransomware attacks.

### Explanation
**The Volume Shadow Copy Service (VSS) is a Windows feature that allows point-in-time copies of files and volumes to be created while the system is running. This enables:**
- Restore points to roll back system changes.
- System restore for recovery from errors or corruption.
- Configuration of restore settings and deletion of restore points.
- Shadow copies are stored on each protected drive, inside the hidden System Volume Information folder.
- From a security standpoint, ransomware often attempts to delete shadow copies to make recovery impossible unless backups exist.

### Notes
- Command to manage shadow copies: SystemPropertiesProtection (opens System Protection settings).
- Requires System Protection to be enabled for restore functionality.
- Best practice: always maintain offline/off-site backups in case shadow copies are deleted by malware.


## Key Takeaways
- Windows Update ensures security and stability; updates can be postponed but not skipped.
- Windows Security centralizes all core protection tools.
- Virus & threat protection offers scans, real-time defense, and ransomware protection.
- Firewall controls inbound/outbound traffic using Domain, Private, and Public profiles.
- SmartScreen protects against phishing, malicious apps, and unsafe downloads.
- Core isolation and TPM strengthen hardware-level security.
- BitLocker provides full-disk encryption, best with TPM.
- Volume Shadow Copy enables restore points but is often targeted by ransomware.
