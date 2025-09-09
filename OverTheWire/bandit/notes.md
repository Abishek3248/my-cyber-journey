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
- SSH private keys can be used as an alternative to passwords.  
- The `-i` flag in `ssh` specifies an identity (private key) file for authentication.  
- Access control: even if a file exists, you can only read it with the correct permissions or user account.  

**Tools / Commands Used:**  
- `ls` – found `sshkey.private` in the home directory.  
- `ssh -i sshkey.private bandit14@localhost` – logged in as `bandit14` using the private key.  
- `cat /etc/bandit_pass/bandit14` – retrieved the password once logged in.  

**My Experience / Challenges:**  
- Initially couldn’t read `/etc/bandit_pass/bandit14` because it’s restricted to `bandit14`.  
- Didn’t know what the private key was at first, so I researched and learned about SSH key-based authentication.  
- Tried using `ssh` with the `-i` flag and successfully logged in as `bandit14`.  
- After logging in, reading the password file became straightforward.  

**Takeaway:**  
- When direct access is restricted, look for alternative authentication methods (like SSH keys).  
- Always check the home directory for useful files.  
- Understanding `ssh` options is essential for system access in different scenarios.




## Level 14  

**Concepts Learned:**  
- Basics of networking and ports.  
- How to connect to a specific port on a host.  
- Using `nc` (netcat) for sending data over a network connection.  

**Tools / Commands Used:**  
- `nc localhost 30000` – connected to the specified port.  
- Copied and pasted the current level password into the netcat session to submit it.  

**My Experience / Challenges:**  
- Initially didn’t realize that the empty line from `nc` was waiting for input.  
- After recalling the question, I submitted the password and successfully received the next level’s password.  
- Learned the practical use of `nc` for network communication.  

**Takeaway:**  
- Ports are endpoints for communication; you can send/receive data using tools like `nc`.  
- Always read the question carefully — the tool may be waiting for input.  
- Understanding basic networking concepts is essential for penetration testing tasks.



## Level 15  

**Concepts Learned:**  
- Using SSL/TLS encryption for secure communication.  
- Connecting to encrypted ports using `openssl s_client`.  
- Difference between plain TCP connections (`nc`) and encrypted connections.  

**Tools / Commands Used:**  
- `openssl s_client -connect localhost:30001` – connected to the encrypted port.  
- Copied and pasted the current level password into the session to retrieve the next password.  

**My Experience / Challenges:**  
- Initially tried using `nc` like before, but it didn’t work due to SSL/TLS encryption.  
- Researched and learned that `openssl s_client` can handle encrypted connections.  
- Successfully connected using `openssl s_client` and submitted the password to get the next level.  

**Takeaway:**  
- SSL/TLS requires special handling for connections; plain TCP tools won’t work.  
- `openssl s_client` is a valuable tool for testing encrypted ports.  
- Understanding the difference between encrypted and unencrypted connections is essential for secure communications.




