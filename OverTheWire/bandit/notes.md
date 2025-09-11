# OverTheWire: Bandit Walkthrough
## Level 0  

**Concepts Learned:**  
- Logging into a remote server using SSH  
- Navigating to the home directory  
- Accessing and reading files  

**Tools / Commands Used:**  
- `ssh` – to connect to the Bandit server  
- `ls` – to list files in the directory  
- `cat` – to read the contents of files  

**My Experience / Challenges:**  
- This was my first time using SSH to connect to a remote system.  
- At first, I wasn’t confident doing it on my own, but after following steps, I understood the process.  
- I successfully located the `readme` file in the home directory and used `cat` to view the password for the next level.  


## Level 1  

**Concepts Learned:**  
- Handling files with special characters in their names  
- Understanding how `./` can be used to reference files that may conflict with command names  

**Tools / Commands Used:**  
- `ls` – to list files in the home directory  
- `cat ./-` – to read the file named `-`  

**My Experience / Challenges:**  
- The challenge was that the password file had the name `-`, which conflicted with standard command options.  
- At first, I tried different approaches like using quotes, but they didn’t work.  
- I finally learned that prefixing the filename with `./` allows me to directly reference the file and read its contents successfully.  



## Level 2  

**Concepts Learned:**  
- Handling filenames that contain spaces  
- Escaping characters (using `\`) to correctly reference such files  
- Using `./` to handle filenames starting with `-`  

**Tools / Commands Used:**  
- `ls` – to view files in the directory  
- `cat ./--spaces\ in\ this\ filename--` – to read the password file  

**My Experience / Challenges:**  
- The file name contained spaces and began with a `-`, which made it tricky to access.  
- I initially struggled and experimented with quotes and other methods, but couldn’t make it work.  
- After looking up references, I learned about **escaping spaces** using `\`, which allowed me to read the file successfully.  
- This helped me realize the importance of understanding how the shell interprets special characters.  


## Level 3  

**Concepts Learned:**  
- Understanding hidden files in Linux (files starting with `.`)  
- Using options with commands (`-a` with `ls`) to display hidden files  
- Navigating directories with `cd`  

**Tools / Commands Used:**  
- `cd` – to change into the `inhere` directory  
- `ls -a` – to list files, including hidden ones  
- `cat .hidden` – to read the password file  

**My Experience / Challenges:**  
- This level was simpler compared to the previous ones.  
- The key learning was how hidden files work in Linux and how to reveal them with `ls -a`.  
- It helped reinforce the importance of checking for hidden files when searching for information.  

**Takeaway:**  
- Always check for hidden files.


## Level 4  

**Concepts Learned:**  
- Identifying human-readable files in a directory  
- Using `file` to determine file types  
- Searching files efficiently with `find`  
- Applying commands to multiple files with `xargs` and piping  

**Tools / Commands Used:**  
- `ls` – list files in the directory  
- `file` – check file type  
- `find` – search for files with patterns  
- `xargs` – apply commands to multiple inputs  
- Piping (`|`) – connect commands together  

**My Experience / Challenges:**  
- The password files were named `-file00`, `-file01`, etc., and I first tried checking each file manually using `file` after reading its `man` page.  
- Doing it one by one was inefficient, so I searched online for better methods and discovered `xargs`.  
- My first attempt with `ls | xargs file` didn’t work, so I combined it with `find`: `find -type f -name "-file*" | xargs file`.  
- This successfully identified the human-readable file.  
- This level reinforced how reading documentation and researching solutions is key to solving Linux challenges efficiently.  

**Takeaway:**  
- When handling multiple files, use `find` and `xargs` together instead of processing files manually.



## Level 5  

**Concepts Learned:**  
- Searching for files recursively using `find`  
- Filtering files by type, size, readability, and executability  
- Combining multiple `find` options to narrow down search efficiently  

**Tools / Commands Used:**  
- `find -type f -size 1033c -readable ! -executable` – locate the target file  
- `cat` – to read the password file  

**My Experience / Challenges:**  
- The challenge required finding a human-readable file of a specific size (1033 bytes) that was not executable in a nested directory.  
- I used `find` with `-type`, `-size`, and `-readable` to locate it.  
- I initially tried `! -perm 777` to check for non-executable files, but learned that `! -executable` was the correct way to filter out executable files.  
- This level reinforced how combining multiple `find` options can efficiently locate specific files in a recursive directory structure.  

**Takeaway:**  
- When searching recursively, combine multiple `find` options (`-type`, `-size`, `-readable`, `! -executable`) to narrow down results efficiently.



## Level 6  

**Concepts Learned:**  
- Searching files by ownership (`-user`, `-group`) in addition to type and size  
- Understanding how `find` behaves when encountering directories with restricted permissions  
- Adjusting search paths to locate files outside the home directory  

**Tools / Commands Used:**  
- `find -type f -size 33c -user bandit7 -group bandit6` – locate the target file  
- `cd` – navigate directories  

**My Experience / Challenges:**  
- The goal was to find a 33-byte file owned by user `bandit7` and group `bandit6`.  
- Initially, I ran the command in the home directory but got no results.  
- After re-reading the question, I realized the file could be elsewhere on the server.  
- I tried running the command from the root directory, which produced many "Permission denied" messages.  
- I manually scanned the output, found the correct file without permission issues, and read it using `cat`.  
- This level reinforced careful reading of instructions and understanding how `find` interacts with filesystem permissions.  

**Takeaway:**  
- Always pay attention to the search path and filesystem permissions when using `find` with ownership filters.



## Level 7 

**Concepts Learned:**  
- Searching for specific text patterns in files using `grep`  
- Understanding how to quickly locate information without reading the entire file  

**Tools / Commands Used:**  
- `grep "millionth" data.txt` – search for the word "millionth" in `data.txt`  

**My Experience / Challenges:**  
- The password was located next to the word "millionth" in `data.txt`.  
- I had not used `grep` before, so I read its `man` page to understand its usage.  
- Using `grep` allowed me to quickly find the password without manually scanning the file.  

**Takeaway:**  
- Use `grep` to efficiently search for specific patterns in files instead of reading them line by line.



## Level 8  

**Concepts Learned:**  
- Finding unique lines in a file using `uniq`  
- Sorting data with `sort` before using `uniq`  
- Understanding how piping works and how commands take input  

**Tools / Commands Used:**  
- `sort data.txt | uniq -u` – find the only unique line in `data.txt`  

**My Experience / Challenges:**  
- The goal was to find a line that was the only unique one in the file.  
- I first tried `uniq -u data.txt` directly, but it didn’t work because `uniq` requires the input to be sorted.  
- I then experimented with `sort data.txt | uniq -u data.txt`, but realized that giving the filename after piping overrides the piped input.  
- Removing the filename after the pipe (`sort data.txt | uniq -u`) finally worked.  
- This level helped me understand how **piping passes output between commands** and why order matters.  

**Takeaway:**  
- When using piping, avoid specifying a filename after a command that takes input from the pipe; always ensure commands are applied to the intended input.



## Level 9  

**Concepts Learned:**  
- Extracting human-readable strings from binary or non-text files using `strings`  
- Filtering output with `grep` to quickly locate patterns  

**Tools / Commands Used:**  
- `strings data.txt` – list human-readable text from `data.txt`  
- `strings data.txt | grep "==="` – filter lines preceded by `===`  

**My Experience / Challenges:**  
- The password was one of the few human-readable lines in `data.txt`, preceded by `===`.  
- I first tried `strings` to view all ASCII text, which helped locate the password manually.  
- To make it more efficient, I piped the output through `grep "==="` to quickly filter and find the correct line.  
- This level introduced me to extracting text from files and combining commands to streamline searches.  

**Takeaway:**  
- Use `strings` to extract readable content from non-text files, and combine it with `grep` to efficiently locate specific patterns.



## Level 10  

**Concepts Learned:**  
- Understanding Base64 encoding and decoding  
- Using `base64` command to decode encoded data  

**Tools / Commands Used:**  
- `base64 -d data.txt` – decode the Base64-encoded content in `data.txt`  

**My Experience / Challenges:**  
- The password was stored in Base64 encoding inside `data.txt`.  
- I read the `man` page for `base64` and discovered the `-d` flag for decoding.  
- Using `base64 -d data.txt`, I was able to decode the content and retrieve the password.  
- This level introduced me to encoding concepts and how to decode data efficiently.  

**Takeaway:**  
- Use `base64 -d` to decode Base64-encoded files and extract readable content quickly.



## Level 11  

**Concepts Learned:**  
- Introduction to ROT13 (a substitution cipher where letters are rotated by 13 places in the alphabet)  
- Using the `tr` command to perform character substitution and decoding  

**Tools / Commands Used:**  
- `tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt` – decode the ROT13-encoded content in `data.txt`  

**My Experience / Challenges:**  
- The file contained text encoded with ROT13, but I didn’t know how to approach it initially.  
- I tried using `man` and `apropos` with “rotate,” but couldn’t find a direct solution.  
- The definition of `tr` hinted it could transform characters, but I wasn’t sure how.  
- After researching online, I learned about ROT13 and how to apply it with `tr`.  
- This gave me a better understanding of both simple ciphers and how flexible `tr` can be.  

**Takeaway:**  
- When encountering encoded data, research the encoding type.  
- ROT13 can be decoded in Linux using the `tr` command for character substitution.



## Level 12  

**Concepts Learned:**  
- Using `/tmp` for safe experimentation (`mkdir`, `cp`, `mv`)  
- Hexdump and reversing it with `xxd`  
- Redirecting command output with `>`  
- Detecting file types with `file`  
- Handling multiple compression formats: gzip, bzip2, tar  
- Importance of file extensions for proper decompression  

**Tools / Commands Used:**  
- `mkdir /tmp/mydir && cp data.txt /tmp/mydir/` – prepare workspace  
- `xxd -r data.txt > data1.bin` – reverse hexdump into a binary file  
- `file data1.bin` – check file type after each step  
- `mv data1.bin data1.gz && gzip -d data1.gz` – decompress gzip file  
- `mv data2.bin data2.bz2 && bzip2 -d data2.bz2` – decompress bzip2 file  
- `tar -xf data3.tar` – extract tar archives  
- Repeated the cycle (`file → rename with correct extension → decompress`) until final file revealed the password  

**My Experience / Challenges:**  
- At first, I was confused after reversing the hexdump since the content didn’t look different.  
- Learned to redirect decoded output into a new file with `>`.  
- `file` showed it was gzip-compressed, so I renamed with `.gz` and decompressed.  
- I thought it failed since the file looked similar, but after checking with `file` again, I realized it was actually **bzip2** compressed.  
- That’s when I understood this challenge required **repeated decompression** using different tools.  
- Step by step, I used `gzip`, `bzip2`, and `tar` depending on the detected format.  
- Finally, after multiple iterations, I found the password inside `data8.bin`.  

**Takeaway:**  
- Always use `file` after each step to confirm file type.  
- File extensions matter for decompression tools — rename files accordingly.  
- Some challenges require patience and repeated transformations, reinforcing persistence and attention to detail.



## Level 13  

**Concepts Learned:**  
- Using SSH keys (`-i`) to authenticate as another user  
- Understanding the purpose of SSH keys as an alternative to passwords  

**Tools / Commands Used:**  
- `ssh -i bandit13_key bandit14@localhost` – login to the next Bandit level using SSH key  
- `cat /etc/bandit_pass/bandit14` – read the password for the next level  

**My Experience / Challenges:**  
- The password was stored in `/etc/bandit_pass/bandit14`, but I didn’t have direct access as bandit13.  
- I found an SSH key in the home directory and researched its purpose online.  
- Learned that SSH keys are a safer alternative to passwords.  
- Using the `-i` flag with `ssh`, I logged in as bandit14 and accessed the password file successfully.  

**Takeaway:**  
- SSH keys allow secure login without using passwords.  
- Always check for alternative authentication methods provided in a challenge.  


## Level 14  

**Concepts Learned:**  
- Networking basics: understanding ports and connections  
- Using `nc` (netcat) to send data to a specific port  

**Tools / Commands Used:**  
- `nc localhost 30000` – connect to port 30000 and send current password  

**My Experience / Challenges:**  
- I needed to submit the current password to port 30000.  
- Initially, connecting with `nc` gave an empty line; I didn’t realize I needed to submit the password.  
- After recalling the question, I sent the password using `nc`, which returned the next level’s password.  

**Takeaway:**  
- Netcat is a simple tool for sending and receiving data over TCP/UDP ports.  
- Understand the requirements of a networking challenge before sending data.  


## Level 15  

**Concepts Learned:**  
- Connecting to ports with SSL/TLS encryption  
- Using `openssl s_client` to establish a secure connection  

**Tools / Commands Used:**  
- `openssl s_client -connect localhost:30001` – connect securely to the port and submit password  

**My Experience / Challenges:**  
- The challenge required sending the password to a port using SSL/TLS.  
- I initially tried `nc`, but it didn’t work for encrypted connections.  
- Researching online, I learned `openssl s_client` can handle SSL/TLS connections.  
- Using `openssl s_client`, I connected securely and submitted the password successfully.  

**Takeaway:**  
- SSL/TLS connections require proper tools like `openssl` rather than plain `nc`.  
- Understanding encryption protocols is important for secure communication challenges.  


## Level 16  

**Concepts Learned:**  
- Scanning a range of ports for open services using `nmap`  
- Identifying services that support SSL/TLS  
- Connecting to SSL/TLS-enabled ports using `ncat --ssl`  
- Using SSH keys to log into a remote account  
- Using temporary directories (`/tmp`) when home directory is restricted  
- Editing files with `nano` and `vim`  
- Managing SSH key permissions with `chmod`  

**Tools / Commands Used:**  
- `nmap -p 31000-32000 localhost` – scan a range of ports to find open ones  
- `openssl s_client -connect localhost:<port>` – test SSL/TLS support for each open port  
- `ncat --ssl localhost <port>` – send password securely to SSL/TLS-enabled port  
- `nano /tmp/mykey` – create/edit a file (initial attempt, encountered history file issue)  
- `vim /tmp/mykey` – create/edit a file successfully  
- `chmod 700 /tmp/mykey` – set correct permissions for the private SSH key  
- `ssh -i /tmp/mykey bandit17@localhost` – log in using the retrieved SSH key  
- `cat /etc/bandit_pass/bandit17` – retrieve the password for the next level  

**My Experience / Challenges:**  
- I had to find which port in the range 31000–32000 supported SSL/TLS to send the password.  
- `nmap` identified 5 open ports; `openssl s_client` revealed only 2 supported SSL.  
- Sending the password to both ports initially failed ("key update" messages).  
- The SSH key was given as text, not a file. I tried creating it in my home directory using `nano` but faced issues with the history file.  
- I switched to `vim` in `/tmp` to create the key file successfully.  
- SSH complained the key was unprotected; I fixed this with `chmod 700` on the key.  
- Using `ssh -i` with the key allowed me to log into bandit17.  
- After logging in, the password was located in `/etc/bandit_pass/bandit17`.  

**Takeaway:**  
- Use `/tmp` to create files if home directory permissions are restricted.  
- Always check SSH key permissions; unprotected keys may prevent login.  
- `nano` and `vim` are useful for creating and editing files, but issues like history files may require switching editors.  
- Combining `nmap`, `openssl`, `ncat`, and SSH is critical for challenges involving SSL/TLS and remote authentication.



## Level 17  

**Concepts Learned:**  
- Comparing files to identify differences using `diff`  
- Understanding how minimal changes (like a single password line) can be tracked  
- Recognizing that login issues may be intentional hints for the next level  

**Tools / Commands Used:**  
- `diff passwords.old passwords.new` – compare the two files and show differing lines  

**My Experience / Challenges:**  
- The two files (`passwords.old` and `passwords.new`) were mostly identical except for the password line.  
- Using `diff` revealed the line that changed, which contained the password for the next level.  
- When trying to use this password to log in, the response was just "byebye," which initially caused confusion.  
- The Bandit question explicitly mentioned that this login behavior was related to the **next level**, so I noted the password and moved on.  

**Takeaway:**  
- `diff` is a powerful tool to compare files and identify even small changes.  
- Pay attention to challenge instructions; sometimes login issues are intentional hints for the next level.



## Level 18  

**Concepts Learned:**  
- Understanding `.bashrc` and how it affects login behavior  
- Using SSH command options to execute commands remotely before full login  
- Retrieving passwords even when interactive login is blocked  

**Tools / Commands Used:**  
- `ssh bandit18@localhost 'cat readme'` – execute `cat readme` remotely without fully logging in  

**My Experience / Challenges:**  
- The `.bashrc` file in the home directory was modified, preventing normal login.  
- Unlike previous levels, I couldn’t even get to the shell prompt to manually check files.  
- I researched online and learned that SSH allows executing a command on the remote server directly when connecting.  
- By appending the command to `ssh`, I was able to read the `readme` file and retrieve the password without logging in interactively.  

**Takeaway:**  
- `.bashrc` can block interactive login, but SSH command execution can bypass it.  
- Understanding remote execution techniques is useful when normal login is restricted.


### Level 19

**Concepts Learned:**  
- Introduction to **setuid binaries** and privilege escalation  
- Setuid binaries run with the **owner’s privileges** instead of the user’s  
- Learned to use `id` to check UID/GID for different users  
- Understood that the binary itself decides what functionality is exposed — not every command can be used  
- In this case, the binary allowed passing a command as an argument, so I could run commands as the next user  
- Learned how such binaries can help derive **which files I can access** or **whether I can execute commands** with elevated privileges  

**Tools / Commands Used:**  
- `ls -l` → check file permissions and notice the `s` bit (setuid)  
- `id` → view user and group IDs  
- `./bandit20` → test running the binary without arguments to see usage format  
- `./bandit20 cat /etc/bandit_pass/bandit20` → run `cat` with elevated privileges to read the password  

**My Experience / Challenges:**  
- At first, I explored the binary by running it directly; it showed the usage format.  
- I tried arguments like `bandit18`, `bandit19`, and even numeric IDs from `id`, but none worked.  
- Re-reading the challenge text, I realized it expected me to use the binary to access the password file.  
- Inspired by the previous SSH trick, I tested `./bandit20 cat /etc/bandit_pass/bandit20` — and it worked.  

**Takeaway:**  
- Setuid binaries can provide controlled access to higher privileges.  
- They don’t always allow arbitrary command execution; it depends on how the binary is coded.  
- In this challenge, the binary was intentionally designed to execute commands passed to it.  
- Learned to always check usage hints and combine privilege escalation concepts with file access knowledge.



## Level 20  

**Concepts Learned:**  
- Role of a setuid binary that connects to a port and validates input.  
- Difference between a client (`suconnect`) and a server (listening port).  
- Using `ncat -l` to create a listening port on localhost.  
- Importance of sending the **password to the correct side** of the connection.  
- Using `tmux` to manage multiple windows/sessions simultaneously.  

**Tools / Commands Used:**  
- `./suconnect 30005` – connect to the listening port.  
- `ncat -l localhost 30005` – open a listening port on localhost.  
- `tmux` – manage multiple windows for client and server.  
- Paste current password into the `ncat` session – validates and outputs next password.  

**My Experience / Challenges:**  
- First, I tried running `./suconnect 30005`, but it showed **“could not connect”** since no port was listening.  
- After researching online, I realized I needed to open a listening port before connecting.  
- That’s when I set up a `tmux` session so I could run the server (`ncat`) in one window and the client (`suconnect`) in another.  
- Initially, I wasted some time experimenting with `nc -b`, thinking “broadcast” might help.  
- Eventually, I discovered that `ncat -l` is the correct way to listen for incoming connections.  
- After running `ncat -l localhost 30005` in one `tmux` window and `./suconnect 30005` in another, the connection was established.  
- At first, I pasted the password in the wrong window and nothing happened, but when I entered it into the `ncat` session, it worked and revealed the password for the next level.  

**Takeaway:**  
- A client program cannot connect if there’s no server waiting — both sides must be set up.  
- `ncat`/`nc` can act as both client and server depending on the flags.  
- Bandit’s “Commands you may need” section mentioned only `nc`, not `ncat`, which was confusing and delayed my solution.  
- Using `tmux` is essential when you need multiple interactive sessions at once.  


## Level 21  

**Concepts Learned**  
- Cron jobs run scheduled tasks automatically at defined intervals.  
- System-wide cron jobs are stored in `/etc/cron.d/`.  
- Cron jobs may execute scripts as specific users.  
- Redirection (`>`) is used in scripts to write command outputs into files.  

**Tools / Commands Used:**  
- `cat cronjob_bandit22` – inspect the cron job for the next user  
- `cat` – read the file where the cron job stored the password  

**My Experience / Challenges**  
I noticed a cron job file named `cronjob_bandit22` that runs as the `bandit22` user. At first, I didn’t fully understand it, so I researched about cron and scheduled scripts. After opening the script, I saw it used commands like `chmod` (to change permissions) and `cat /etc/bandit_pass/bandit22 > /tmp/...` to write the password to a file.  

By locating and reading that file, I was able to obtain the password for the next level.  

**Takeaway**  
Cron jobs can expose useful information by writing data to files. Always check how scheduled tasks are configured and where they store their outputs.  



## Level 22  

**Concepts Learned:**  
- Inspecting cron jobs in `/etc/cron.d` to understand automated tasks  
- Reading and analyzing shell scripts  
- Understanding variables in scripts  
- Learning about MD5 hashing and how it transforms input into a fixed hash value  

**Tools / Commands Used:**  
- `cat` – to read cron job and script contents  
- `md5sum` – to generate the MD5 hash  

**My Experience / Challenges:**  
- I started by checking `/etc/cron.d/cronjob_bandit23`, which pointed to a script running as `bandit23`.  
- At first, the script was confusing, so I researched how shell scripts and variables work.  
- The script contained a line like:
  
echo I am user $myname | md5sum

- This command takes the string "I am user <username>", replaces $myname with the actual username, and then generates an MD5 hash of it.
- After learning what it does, I tried running this line in my terminal. It generated a hash, which I initially thought was the password, but it didn’t work. Looking further into the script, I saw:

cat /etc/bandit_pass/bandit23 > /tmp/$mytarget

- Here, the $mytarget variable was derived from the earlier echo … | md5sum line. This meant the password was being written to a file under /tmp/ with a name equal to that hash.

- At first, I mistakenly used the hash from echo I am user bandit22, but realized the correct username should be bandit23. After correcting this, I ran:

echo I am user bandit23 | md5sum

- This produced the correct hash. I then accessed the file:

cat /tmp/<hash>

- Inside it was the password for the next level.

**Takeaway**  
Understanding shell scripts is key to solving automation-related challenges.
MD5 hashing transforms input text into a fixed hash, which can sometimes be used directly as a password or verification string.
How environment variables work in Bash scripts.
Importance of paying attention to the correct username in scripted commands.



## Level 23: Writing My First Script for a Cron Job  

**Concepts Learned:**  
- Cron jobs and how they execute files at regular intervals.  
- How a script can check file names and ownership before execution.  
- The importance of file permissions (`chmod +x`) for making scripts executable.  
- Writing and running a simple Bash script with a shebang (`#!/bin/bash`).  

**Tools / Commands Used:**  
- `cat` – to read the cron job script in `/etc/cron.d/cronjob_bandit24`.  
- `vim` – to create a script (`iam.sh`).  
- `chmod +x` – to make the script executable.  
- `cat /etc/bandit_pass/bandit24 > /tmp/hari/password.txt` – the key command inside my script.  
- `mkdir /tmp/hari` – to create a directory for storing the output.  
- `stat %u` – used in the cron job script to check file ownership.  

**My Experience / Challenges:**  
- When I first looked at `/etc/cron.d/cronjob_bandit24`, I saw the script checked the `/var/spool/bandit24/foo` directory. It ignored files with `.` or `..`, then used `stat %u` to check the owner. If the owner was `bandit23`, it executed the file and then deleted it.  

- I understood the logic but wasn’t sure what to do next. Since the instructions mentioned creating my first script, I researched online and realized the key: **anything I placed in that directory would be executed as long as it was owned by bandit23.**  

- I created a script named `iam.sh` with:  

#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/hari/password.txt

- At first, it didn’t work — no file appeared in /tmp/hari. After some frustration, I realized I had forgotten to make the script executable. Once I ran chmod +x iam.sh, everything worked. Within 30–60 seconds, the cron job executed my script, and when I checked /tmp/hari/password.txt, I found the password for the next level.

**Takeaway**
- Cron jobs can be exploited by placing controlled scripts in monitored directories.
- File ownership is critical — only bandit23-owned files were executed.
- Always remember to give scripts execution permissions with chmod +x.
- Creating and running even a simple Bash script gave me confidence to build on scripting skills further.


## Level 24  

**Concepts Learned:**  
- Understanding how daemons listen on ports and can accept input  
- Using brute force techniques when a 4-digit code is required  
- Writing simple Bash scripts for automation  
- Using loops (`for` + `seq`) to generate number ranges with leading zeros  
- Piping script output into `nc` (netcat) to interact with a listening service  

**Tools / Commands Used:**  
- `seq -w 0 9999` – generate numbers from 0000 to 9999 with leading zeros  
- `for` loop in Bash – to iterate through the generated numbers  
- `echo` – to send data (password + 4-digit code)  
- `nc` – to connect to the daemon on port 30002  
- Bash scripting (`#!/bin/bash`, `chmod +x script.sh`, `./script.sh`)  

**My Experience / Challenges:**  
- The challenge required connecting to a daemon on port `30002` that would accept the current level password plus a 4-digit code.  
- I realized brute forcing was necessary since the code could be anything from `0000` to `9999`.  
- I learned a bit of Bash scripting to handle this. I wrote a loop using:  

  ```bash
  for i in $(seq -w 0 9999); do
      echo "$pass $i"
  done
- Before the loop, I stored the password in a variable:

 pass="jdfhjhfdkjdshkdkhkjdhkj"


- At first, I tried running nc localhost 30002 inside the script, but later learned it’s better to pipe the script output into netcat:

 ./script.sh | nc localhost 30002


-This worked, and I got the password for the next level.
-Final Script:

#!/bin/bash
pass="jdfhjhfdkjdshkdkhkjdhkj"

for i in $(seq -w 0 9999); do
    echo "$pass $i"
done

-Run it with:

chmod +x script.sh
./script.sh | nc localhost 30002

**Takeaway**
- When brute forcing, automation with Bash loops and seq makes the process efficient.
- Piping script output into tools like nc is a powerful way to test inputs against network services.



## Level 25  

**Concepts Learned:**  
- Identifying user shells from `/etc/passwd`  
- Understanding restricted shells and their limitations  
- Using `more` and `vi` to escape restricted environments  
- Leveraging editor commands (`:set shell=` and `:shell`) to spawn a proper shell  

**Tools / Commands Used:**  
- `cat /etc/passwd | grep bandit26` – check the login shell of `bandit26`  
- `ssh -i bandit26.sshkey bandit26@localhost` – attempt login with SSH key  
- `more` and `vi` – text viewers/editors used as escape points from restricted shells  
- `:set shell=/bin/bash` and `:shell` – commands in `vi` to switch to a proper Bash shell  

**My Experience / Challenges:**  
- The task involved figuring out how to access `bandit26`, whose shell was not the usual `/bin/bash`.  
- By checking `/etc/passwd`, I found that `bandit26`’s shell was set to a program called `showtext` instead of a standard shell.  
- I tried using the SSH key available in the home directory to log in as `bandit26`, but the connection closed immediately, confirming the restricted shell was blocking access.  
- After researching, I learned that resizing the terminal triggered `more` when displaying output, which in turn allowed switching to `vi`.  
- Inside `vi`, I discovered that I could escape the restricted environment by setting the shell manually:  
  ```vim
  :set shell=/bin/bash
  :shell
- This provided me a working Bash shell as bandit26. From there, I accessed the password file:

cat /etc/bandit_pass/bandit26

- This was my first time using an editor as an escape mechanism, and it helped me understand how non-standard shells can be bypassed in practice.

**Takeaway**
- Restricted shells are often vulnerable to escape methods via built-in programs like more or vi.
- Exploring editor commands is a powerful way to break out of limited environments and gain a proper shell.


## Level 26  

**Concepts Learned:**  
- Revisiting the concept of setuid binaries  
- Using setuid files to execute commands with elevated privileges  
- Applying previously learned techniques to new challenges  

**Tools / Commands Used:**  
- `ls` – to identify files in the home directory  
- `./bandit27-do <command>` – run commands with `bandit27`’s privileges  
- `cat /etc/bandit_pass/bandit27` – read the password file  

**My Experience / Challenges:**  
- This level had a setuid file named `bandit27-do` in the home directory.  
- From earlier levels (around Level 19), I already learned how setuid binaries can be used to run commands as another user.  
- I directly applied that knowledge here by executing:  
  ```bash
  ./bandit27-do cat /etc/bandit_pass/bandit27
- This returned the password for the next level.

**Takeaway**
Concepts from earlier challenges often reappear in later ones. Recognizing patterns and reusing past solutions saves time.



## Level 27  

**Concepts Learned:**  
- Accessing Git repositories over SSH  
- Understanding how to specify custom ports in Git URLs  
- Working with temporary directories when permissions are restricted  
- Using Git to clone repositories and inspect contents  

**Tools / Commands Used:**  
- `git clone <repo-url>` – clone the Git repository  
- `ssh://user@host:port/path/to/repo` – Git URL format with custom port  
- `mkdir /tmp/<dir>` and `cd` – create and move into a writable directory  
- `cat` – read the contents of files  

**My Experience / Challenges:**  
- This level involved cloning a Git repository hosted on the Bandit server.  
- The repo link provided was:  
  ssh://bandit27-git@localhost/home/bandit27-git/repo

- I knew the server was using port `2220`, so I first tried:  

  git clone ssh://bandit27-git@localhost/home/bandit27-git/repo -p 2220

- but that didn’t work, since Git doesn’t accept ports that way.

- I also experimented with ssh -p 2220, but that wasn’t correct either.

- Since I didn’t have permissions to clone directly into the home directory, I created a writable directory under /tmp and worked there.

- The key realization came when I remembered how URLs are written in host:port style (like in web addresses). I applied that here:

  git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo

- This worked, asked for the password, and successfully cloned the repo into /tmp/github.clone.

- Inside the repository, I found a README file. Reading it with cat revealed the password for the next level.

**Takeaway**
- Git over SSH requires the port to be specified in the URL (host:port).
- When working in restricted environments, use /tmp as a safe writable directory.


## Level 28  

**Concepts Learned:**  
- Reusing Git over SSH with custom ports  
- Exploring Git commit history to find past changes  
- Using `git log` to view commit metadata  
- Using `git show <commit-id>` to inspect changes made in specific commits

**Tools / Commands Used:**  
- `git clone ssh://bandit28-git@localhost:2220/home/bandit28-git/repo` – clone the repository  
- `cd repo` – move into the cloned repository  
- `cat README.md` – check the file contents  
- `git log` – list commit history  
- `git show <commit-id>` – view details and changes from specific commits  

**My Experience / Challenges:**  
- After cloning the repository into `/tmp/git-clone`, I noticed that it contained a directory named `repo`. Inside this, there was a `README.md` file.  
- Reading the file showed notes for *Bandit Level 29*, but the password field was just `xxxxxxxx`, suggesting it had been altered.  
- Since the instructions hinted at using Git, I explored its functionality and learned about commits and history.  
- Running `git log` revealed previous commit hashes.  
- Using:  
  ```bash
  git show <commit-id>
- I examined an earlier version of the README.md file and found the actual password for the next level.

**Takeaway**
- Git repositories can hide sensitive information in their history, even if the current version looks harmless.
- Always check commit logs and previous versions when analyzing repositories in security challenges.



## Level 29  

**Concepts Learned:**  
- My introduction to Git branches and how information can be hidden in them
- Investigating Git branches to uncover hidden information
- Using remote branches (`remotes/origin/<branch>`) to access alternate content  
- Using `git branch -a` to list all local and remote branches  
- Using `git show <branch>` to view the contents of files in specific branches  

**Tools / Commands Used:**  
- `git clone ssh://bandit29-git@localhost:2220/home/bandit29-git/repo` – clone the repository  
- `cd <repo>` – move into the cloned directory  
- `cat README.md` – check the current file contents  
- `git log` – view commit history  
- `git branch -a` – list all local and remote branches  
- `git show <branch>` – view file contents from specific branches  

**My Experience / Challenges:**  
- As usual, I created a directory in `/tmp` and cloned the repository. Inside, I found the `README.md` file.  
- The README indicated no password in production instead of `xxxxxxxx`, unlike the previous level.  
- I tried checking all commit logs using `git log` and `git show`, but none revealed the password.  
- After researching, I learned that Git stores information in branches too.  
- I used `git branch` but didn’t find anything useful at first, then discovered the `-a` flag, which listed all local and remote branches.  
- Inspecting the remote branch `remotes/origin/dev` with `git show remotes/origin/dev` finally revealed the password for the next level.  

**Takeaway:**  
- Passwords or sensitive information may not always be in the main branch; exploring remote or alternative branches can reveal hidden data.  
- Understanding the structure of Git repositories (commits, branches, remotes) is crucial in security challenges.  



## Level 30  

**Concepts Learned:**  
- Continuing exploration of Git repository internals  
- Understanding that Git tags can also store historical or hidden information  
- Using `git tag` to list all tags  
- Using `git show <tag>` to inspect the content associated with a tag  

**Tools / Commands Used:**  
- `git clone ssh://bandit30-git@localhost:2220/home/bandit30-git/repo` – clone the repository  
- `cd <repo>` – move into the cloned directory  
- `cat README.md` – check the file contents  
- `git branch -a` – list all local and remote branches  
- `git show <branch>` – view contents from specific branches  
- `git tag` – list all tags  
- `git show <tag>` – view contents associated with a specific tag  

**My Experience / Challenges:**  
- As usual, I created a directory in `/tmp` and cloned the repository. Inside, I found the `README.md` file.  
- Unlike the previous levels, the README was essentially empty, showing just a placeholder message instead of any information.  
- I checked all commits and branches using `git log`, `git show`, and `git branch -a`, but still found nothing useful.  
- Based on experience from the past few levels, I suspected there might be other hidden locations where Git stores data.  
- After researching, I discovered that Git tags can also store information.  
- Running `git tag` revealed a tag named `secret`. Using:  
  ```bash
  git show secret
- I was able to retrieve the password for the next level.

**Takeaway:**
- Information in Git repositories can be hidden not only in branches and commits but also in tags.
- Exploring all Git mechanisms (branches, commits, and tags) is essential when hunting for hidden data in security challenges.


## Level 31  

**Concepts Learned:**  
- Pushing changes to a remote Git repository  
- Preparing files for commit using `git add`  
- Saving changes locally with `git commit`  
- Understanding the relationship between local branches and remote branches (`origin/master`)  
- Using `git push` to send changes to a remote repository  

**Tools / Commands Used:**  
- `git clone ssh://bandit31-git@localhost:2220/home/bandit31-git/repo` – clone the repository  
- `cd <repo>` – move into the cloned directory  
- `cat README.md` – read instructions  
- `echo "May I come in?" > key.txt` – create the required file  
- `git branch` – check the current branch  
- `git add key.txt` – stage the file for commit  
- `git commit -m "upload a file"` – commit changes locally  
- `git push -u origin master` – push changes to the remote repository  

**My Experience / Challenges:**  
- As usual, I created a directory in `/tmp` and cloned the repository.  
- The `README.md` file contained a message specifying the task: push a file to the remote repository. It clearly displayed the details — the filename, the content to include, and the branch (`master`).  
- I created the file `key.txt` with the content `May I come in?` and confirmed that the branch was already `master`.  
- I first tried to push directly, but the process failed because the file had not been staged or committed yet.  
- After researching the proper Git workflow, I used:  
  ```bash
  git add key.txt
  git commit -m "upload a file"
  git push -u origin master
- The push resulted in an error, but during the connection process, the password for the next level was revealed.

**Takeaway:**
- Pushing changes to a remote repository requires staging and committing files first.
- Even if the push fails, interactions with the remote host can sometimes reveal useful information, like credentials or passwords.



## Level 32  

**Concepts Learned:**  
- Working with non-standard shells and their limitations  
- Using special shell variables like `$0` to interact with the environment  
- Escaping restricted shells to access a standard Bash or sh shell  

**Tools / Commands Used:**  
- `$0` – to spawn a subshell from a restricted or unusual shell  
- `cat /etc/bandit_pass/bandit33` – read the password file once a proper shell was obtained  

**My Experience / Challenges:**  
- In this level, the shell provided was a custom program that converts everything typed into uppercase. This made running normal commands impossible.  
- I tried various approaches, including using `$SHELL`, but none worked.  
- After researching online, I discovered that the `$0` variable could be used as an alternative to invoke a shell.  
- I expected it might just display the shell name, but instead it spawned a standard `sh` subshell.  
- From this subshell, I was able to run normal commands, including:  
  ```bash
  cat /etc/bandit_pass/bandit33
 which gave me the password for the next level.

**Takeaway:**
- Non-standard shells can often be bypassed using built-in shell variables like $0.
- Exploring environment variables and thinking creatively about shell behavior is essential when dealing with restricted environments.


