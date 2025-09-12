## Defensive Security Intro

### Introduction

*Defensive security focuses on **preventing intrusions** and **detecting/responding to attacks**. While offensive security (red teams) identifies and exploits vulnerabilities, defensive security (blue teams) ensures systems remain secure and operational.*
*Key aspects include:*
- **User awareness**: Training users to recognize and avoid attacks.  
- **Asset management**: Documenting and managing systems and devices.  
- **Patching and updates**: Keeping computers, servers, and network devices secure.  
- **Preventative devices**: Firewalls and Intrusion Prevention Systems (IPS) to block malicious traffic.  
- **Logging and monitoring**: Detecting unauthorized devices and malicious activity.  
*Other relevant areas:* Security Operations Centers (SOC), Threat Intelligence, Digital Forensics and Incident Response (DFIR), and Malware Analysis.


## Areas of Defensive Security

- In this section, I learned and gained an understanding of the core domains within defensive security and how organizations protect their systems from attacks.

### Security Operations Center (SOC) & Threat Intelligence
- A Security Operations Center (SOC) is a team of cybersecurity professionals that monitor networks and systems to detect and respond to malicious activities. Key responsibilities include:
- Identifying vulnerabilities and taking preventive measures.
- Detecting policy violations and unauthorized activity.
- Monitoring network intrusions to minimize damage.
- Threat Intelligence involves collecting and analyzing information about potential adversaries. This allows organizations to predict attacker tactics, techniques, and procedures, creating a threat-informed defense. Data comes from both local sources (logs) and public sources (forums), and is processed to generate actionable insights for mitigation and response.

### Digital Forensics and Incident Response (DFIR)
- Digital Forensics is the application of scientific methods to investigate cyber incidents, focusing on:
- *File systems:* Analyzing storage images for installed programs, deleted files, and other traces.
- *System memory:* Capturing memory to analyze malware or attacks that don't leave disk traces.
- *Logs:* Reviewing system and network logs to trace attacker activity.
- Incident Response (IR) defines the methodology to handle cyber incidents efficiently. The four major phases include:
- *Preparation:* Ensuring the team is trained and preventive measures are in place.
- *Detection & Analysis:* Identifying incidents and assessing their severity.
- *Containment, Eradication & Recovery:* Stopping the incident, removing threats, and restoring systems.
- *Post-Incident Activity:* Documenting lessons learned and preventing future occurrences.

### Malware Analysis
- Malware refers to malicious software that compromises systems. Common types include:
- *Viruses:* Spread between systems, altering or deleting files.
- *Trojan Horses:* Appear legitimate but conceal malicious functions.
- *Ransomware:* Encrypts user files and demands a ransom for decryption.
- Malware Analysis is performed to understand malware behavior and mitigate risks:
- **Static Analysi:* Examining the malware code without execution.
- *Dynamic Analysis:* Running the malware in a controlled environment to observe its behavior.



## SIEM Simulation & SOC Practical Exercise

### Concepts Learned
- Understanding the role of a SOC analyst in monitoring and responding to alerts.
- Identifying malicious IP addresses and suspicious user behavior.
- Basic usage of a Security Information and Event Management (SIEM) system for alert detection and analysis.
- Introduction to threat intelligence sources like AbuseIPDB and Cisco Talos Intelligence.
- Reporting incidents and coordinating with team leads for proper mitigation.

### Tools Used
- **SIEM Simulation:** to detect and investigate suspicious activity.
- *IP-Scanner.THM:* to check the reputation and geolocation of IP addresses.
- **AbuseIPDB and Cisco Talos Intelligence:** for professional threat intelligence and verification.

### Notes / Experience
- Detected a malicious IP with multiple failed login attempts, eventually leading to a successful login.
- Verified the IP’s reputation and location using IP-Scanner.THM, AbuseIPDB, and Cisco Talos Intelligence.
- Learned the workflow of a SOC analyst: detect → investigate → report → mitigate.
- Practiced using alert logs to trace suspicious activity and determine potential threats.

### Mitigations
- Incident Verification: Confirmed the malicious nature of the IP using multiple intelligence sources (IP-Scanner.THM, AbuseIPDB, Cisco Talos).
- Escalation: Reported the suspicious activity to the SOC team lead with all relevant logs and details.
- Containment: Collaborated with the SOC lead to block the malicious IP on the network to prevent further unauthorized access.
- Documentation: Logged the incident in the SOC system for post-incident analysis, including steps taken, detection method, and any potential impact.
- Preventative Recommendations: Suggested monitoring for similar patterns in future alerts and implementing stricter access controls for sensitive accounts.

### Key Takeaways
- Defensive security focuses on preventing, detecting, and responding to attacks.
- SOCs and threat intelligence help anticipate and mitigate adversary actions.
- DFIR provides a structured approach to investigating and recovering from incidents.
- Malware analysis is critical for understanding malicious software and developing defense strategies.
- SOC analysts must combine alert monitoring, threat intelligence, and investigative skills to respond to incidents effectively.
- Professional tools like AbuseIPDB and Cisco Talos provide actionable intelligence for decision-making.
- Proper incident reporting and escalation are critical to maintaining network security.
- Hands-on practice with simulated SIEM systems builds the foundation for real-world defensive security operations.
