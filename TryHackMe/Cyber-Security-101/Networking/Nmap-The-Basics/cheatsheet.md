# Cheatsheet - Nmap Basics

| Task / Feature                | Option / Description                                                                 |
|-------------------------------|-------------------------------------------------------------------------------------|
| Host Discovery                 | -sn : Ping scan to find live hosts                                                  |
| Target Specification           | IP range (192.168.0.1-10), subnet (192.168.0.0/24), hostname (example.thm)          |
| TCP Connect Scan               | -sT : Complete TCP three-way handshake                                             |
| TCP SYN Scan (Stealth)         | -sS : Sends SYN only, does not complete handshake                                   |
| UDP Scan                       | -sU : Scan for services listening on UDP ports                                      |
| Limit Ports                    | -F : Fast scan (top 100 ports) <br> -p[range] : Specify port(s)                     |
| Version Detection               | -sV : Detect service and version                                                    |
| OS Detection                    | -O : Guess target OS                                                                 |
| Aggressive Scan                 | -A : OS detection + version + traceroute + more                                     |
| Treat All Hosts as Online       | -Pn : Scan hosts that appear down                                                   |
| Timing / Speed                  | -T0 to -T5 : Paranoid → Insane <br> --min/--max-parallelism <br> --min/--max-rate   |
| Verbosity                       | -v / -vv / -vvv : Increase output detail                                           |
| Debugging                       | -d / -d1 to -d9 : Debug output                                                      |
| Save Output                     | -oN : Normal <br> -oX : XML <br> -oG : Grepable <br> -oA : All formats               |
