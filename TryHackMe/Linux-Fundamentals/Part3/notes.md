# Linux Fundamentals - Part 3

## Introduction  
- Part 3 of the Linux Fundamentals module focuses on practical, day-to-day utilities.  
- Key areas include **automation, package management, and service/application logging**—advancing essential Linux skills beyond the basics.  

## Text Editors  

### Concepts Learned  
- Previously, I worked with files using `echo` and redirection operators (`>` and `>>`), but this approach isn’t practical for multi-line or complex editing.  
- Linux provides **terminal-based text editors** that make file editing more efficient.  
- Explored **Nano** for quick and simple editing, and got an introduction to **VIM**, a more advanced editor.  

### Commands  
- `nano <filename>` → open (or create) a file in Nano for editing.  
  - Example: `nano myfile`  

### Notes  
- Already familiar with Nano and Vim from Bandit challenges, so working with them here felt like a refresher.  
- Nano is beginner-friendly with essential features like **search, copy/paste, line navigation, and exiting via `Ctrl + X`**.  
- Vim, while harder to master, offers advanced functionality such as **customization, syntax highlighting, and universal availability across terminals**.  
- THM emphasized the importance of editors for real-world use, beyond just redirecting text into files.  



## File Transfer and Web Utilities  

### Concepts Learned  
- File transfer is a core part of system administration and security testing.  
- Learned how Linux provides multiple tools for **retrieving files, securely copying files, and serving files**.  
- **Wget** is useful for quickly pulling resources (scripts, binaries, configs) from the web without needing a browser.  
- **SCP** extends SSH, enabling encrypted file transfer between machines.  
- **Python HTTPServer** offers a lightweight way to host files locally, making it easy to share with another system on the same network.  
- Already familiar with **SSH** from Bandit, but **SCP, Wget, and HTTPServer** were new additions that expanded practical workflows.  

### Commands  
- **Wget**  
  - `wget <URL>` → download a file from the web.  
  - Example: `wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt`  

- **SCP**  
  - Copy from local → remote:  
    ```bash
    scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
    ```  
  - Copy from remote → local:  
    ```bash
    scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt
    ```  

- **Python HTTPServer**  
  - Start a quick web server in the current directory:  
    ```bash
    python3 -m http.server
    ```  
  - Download a file from the server (example on port 8000):  
    ```bash
    wget http://MACHINE_IP:8000/myfile
    ```  

### Notes  
- **Wget** felt like a convenient way to automate downloads, much faster than manual browser interaction.  
- **SCP** was new but intuitive since it follows the same source→destination logic as `cp`, with the benefit of SSH encryption.  
- Running a **Python HTTPServer** was surprisingly simple and useful for quick file hosting, though limited since it lacks indexing.  
- These tools together give flexibility in **retrieving, sending, and sharing files** across different environments.  



## Process Management and Services  

### Concepts Learned  
- Processes are running programs on the system, each identified by a unique **PID (Process ID)**.  
- The kernel manages all processes, and PIDs increment as new processes start.  
- Tools like **ps** and **top** help view active processes, with `ps aux` showing system-wide details.  
- Processes can be **terminated or controlled** with signals (`SIGTERM`, `SIGKILL`, `SIGSTOP`).  
- **Namespaces** isolate resources (CPU, RAM, etc.) across processes, improving efficiency and security.  
- **systemd** is the parent of most processes on Ubuntu, and **systemctl** provides control over services (start, stop, enable, disable).  
- Processes can run in the **foreground** (interactive, visible output) or **background** (detached, allows multitasking).  
- Operators and shortcuts like `&`, `Ctrl + Z`, and `fg` make managing foreground/background tasks efficient.  

### Commands  
- **View processes**  
  - `ps` → view processes in current session.  
  - `ps aux` → view all processes system-wide.  
  - `top` → view live system processes with usage statistics.  

- **Kill processes**  
  - `kill <PID>` → terminate a process.  
  - Common signals:  
    - `SIGTERM` (clean stop)  
    - `SIGKILL` (force stop)  
    - `SIGSTOP` (suspend)  

- **Service management with systemctl**  
  - `systemctl start <service>` → start a service.  
  - `systemctl stop <service>` → stop a service.  
  - `systemctl enable <service>` → start on boot.  
  - `systemctl disable <service>` → disable on boot.  

- **Foreground/Background control**  
  - Append `&` to run a process in the background.  
  - `Ctrl + Z` → suspend a process (background it).  
  - `fg` → bring a background process to the foreground.  

### Notes  
- Already comfortable with process concepts from Bandit (like backgrounding with `&`), but here I gained a deeper understanding of **signals**, **systemd/systemctl**, and **foreground vs background workflows**.  
- `ps aux` and `top` are especially useful for **monitoring live activity and troubleshooting**.  
- Learning `systemctl` tied process management to **services** like Apache, bridging user-level processes with system administration.  
- Overall, this section expanded my knowledge from simply running processes to **controlling, monitoring, and automating them**.  




## Task Automation with Cron  

### Concepts Learned  
- The **cron process** runs automatically on boot and is responsible for scheduling repetitive tasks.  
- Users interact with cron through **crontabs**, which define jobs to execute at specific times or intervals.  
- A crontab file consists of 6 fields:  
  - **MIN** → Minute  
  - **HOUR** → Hour  
  - **DOM** → Day of the month  
  - **MON** → Month  
  - **DOW** → Day of the week  
  - **CMD** → Command to execute  
- Wildcards (`*`) make scheduling flexible (e.g., run regardless of day/month).  
- Useful for automating tasks like **backups, script execution, or launching programs**.  

### Commands  
- **Edit crontab**  
  ```bash
  crontab -e
(Opens the crontab file in a text editor such as Nano.)

- Example job: Backup a Documents folder every 12 hours
   0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/

### Notes
- Cron jobs felt like a natural extension of Linux automation, allowing tasks to run without manual execution.
- Using wildcards in crontabs makes schedules highly customizable.
- Online helpers like Crontab Generator or Cron Guru simplify building correct syntax, reducing the learning curve.
- While I hadn’t worked with cron before, it adds significant value in system administration by making recurring tasks effortless.


## Packages & Software Repositories  

### Concepts Learned  
- Developers submit software to **APT repositories** (official or community).  
- **APT** makes software installation and updates easy compared to manual `dpkg`.  
- **GPG keys** verify the authenticity of repositories/software.  
- Repositories can be added or removed to extend OS functionality.  

---

### Commands  
- Add repository with GPG key:  
  ```bash
  wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
Create repo entry in /etc/apt/sources.list.d/ (e.g., sublime-text.list).
Update sources:
sudo apt update
Install package:
sudo apt install sublime-text
Remove repository:
sudo add-apt-repository --remove ppa:PPA_Name/ppa
Remove package:
sudo apt remove [package-name]

### Notes
- APT repositories can be vendor-maintained or community-provided.
- Keeping each repo in a separate .list file inside /etc/apt/sources.list.d/ is good practice.
- GPG keys act as a trust check — if mismatched, installation fails.



## Service & System Logs

### Concepts Learned
- Logs in Linux are stored in `/var/log` and record information about applications, services, and the OS itself.  
- The system automatically manages these logs with a process called **log rotation**.  
- Common services with logs include:  
  - **Apache2** (web server)  
  - **fail2ban** (monitors brute-force attempts)  
  - **UFW** (firewall)  
- Logs are critical for:  
  - Monitoring system health  
  - Diagnosing performance issues  
  - Investigating intruder activity  
- Key log types of interest:  
  - **Access logs** – record every request to a service (e.g., web server)  
  - **Error logs** – record issues or failures  

### Commands
- No specific commands introduced here (logs are viewed with tools like `cat`, `less`, or `tail`).  

### Notes
- Logs provide insight not only into services but also the **OS and user actions** (e.g., authentication attempts).  
- Essential for administrators to track both **normal activity** and **suspicious behavior**.



## Key Takeaways
- Created and edited files using Nano; Vim introduced as an advanced option.
- Downloaded files with Wget, copied files securely with SCP, and served files locally using Python HTTPServer.
- Monitored processes with ps, ps aux, and top; controlled them using SIGTERM, SIGKILL, SIGSTOP, background (&), and foreground (fg) commands.
- Managed services with systemd via systemctl to start, stop, enable, or disable applications, including configuring services to run on boot.
- Automated tasks using cron and crontabs; learned the 6-field format (MIN, HOUR, DOM, MON, DOW, CMD) and wildcard usage.
- Managed software via APT repositories; added/removed repositories, verified GPG keys, installed/removed packages, and extended system functionality with community repos.
- Reviewed system and service logs in /var/log to monitor system health, troubleshoot issues, and audit security events.
- Regular hands-on practice reinforced Linux efficiency, confidence, and preparedness for real-world administration and security tasks.
