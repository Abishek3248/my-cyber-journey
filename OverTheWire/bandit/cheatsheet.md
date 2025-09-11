# Bandit Cheatsheet – OverTheWire

Quick reference of key commands and concepts learned while solving Bandit wargame.

| Category             | Command / Example                                                                 | Notes / Concept |
|----------------------|------------------------------------------------------------------------------------|-----------------|
| **File Handling**    | `cat file`                                                                        | Read file contents |
|                      | `cat ./-`                                                                         | Handle files starting with `-` |
|                      | `cat "file with spaces"`                                                          | Handle spaces in filenames |
|                      | `ls -a`                                                                           | Show hidden files |
| **Searching**        | `find . -type f -size 1033c ! -executable`                                        | Find file by size & permissions |
|                      | `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`                       | Find by user/group, suppress errors |
|                      | `grep "pattern" file`                                                             | Search text in files |
|                      | `strings file | grep "=="`                                                        | Extract strings from binary |
| **Text Processing**  | `sort file | uniq -u`                                                             | Unique line detection |
|                      | `base64 -d file`                                                                  | Decode Base64 |
|                      | `cat file | tr 'A-Za-z' 'N-ZA-Mn-za-m'`                                           | Decode ROT13 |
|                      | `xxd -r file > out`                                                               | Reverse hex dump |
| **Compression**      | `file data.bin`                                                                   | Identify file type |
|                      | `gunzip file.gz`                                                                  | Decompress gzip |
|                      | `bunzip2 file.bz2`                                                                | Decompress bzip2 |
|                      | `tar -xf file.tar`                                                                | Extract tar archive |
| **SSH & Keys**       | `ssh user@host -p 2220`                                                           | SSH connection |
|                      | `ssh -i sshkey.private user@host -p 2220`                                         | SSH with private key |
| **Networking**       | `cat pass.txt \| nc host port`                                                    | Send file via netcat |
|                      | `openssl s_client -connect host:port`                                             | Encrypted connection |
|                      | `nmap -p 31000-32000 localhost`                                                   | Scan open ports |
| **Comparison**       | `diff file1 file2`                                                                | Compare files |
| **Privilege Esc.**   | `./setuid-binary command`                                                         | Run with elevated privileges |
|                      | `vi → :set shell=/bin/bash → :shell`                                              | Escape restricted shell |
| **Automation**       | `for i in {0000..9999}; do echo $i \| nc localhost port; done`                    | Brute-force loop |
| **Cron Jobs**        | `cat /etc/cron.d/*`                                                               | View cron jobs |
|                      | *(Writable cron jobs can be exploited for privilege escalation)*                   | Exploitation concept |

