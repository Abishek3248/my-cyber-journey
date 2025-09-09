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



## Level 8  

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














