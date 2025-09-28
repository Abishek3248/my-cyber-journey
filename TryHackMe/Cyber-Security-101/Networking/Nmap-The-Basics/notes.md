# Nmap-The Basics

## Introduction
- A very efficient solution that can solve the above two requirements and many more is the Nmap network scanner. Nmap is an open-source network scanner that was first published in 1997. Since then, plenty of features and options have been added. It is a powerful and flexible network scanner that can be adapted to various scenarios and setups.


## Host Discovery

### Concepts learned
- **Goal:** find who is online on a network before probing services.  
- **Target notation:** Nmap accepts ranges (`192.168.0.1-10`), CIDR (`192.168.0.0/24`), or hostnames (`example.thm`).  
- **Ping scan (`-sn`)**: discover live hosts only — no port scanning. Nmap uses different probe types depending on whether the target is local or remote.  
- **Local vs remote discovery:** on a directly connected (local) network Nmap uses **ARP** to reliably discover hosts; on a remote network it falls back to ICMP, TCP, and UDP probes (because ARP cannot cross routers).  
- **Discovery tuning:** you can request TCP SYN/ACK/UDP probes for discovery (`-PS`, `-PA`, `-PU`) to bypass ICMP filtering or tune behaviour.  
- **Listing targets (`-sL`)**: prints the list of targets without sending probes — useful to verify scope before scanning.

## Commands / tools
- `nmap -sn 192.168.66.0/24`  
  Run a ping sweep (host discovery) on the /24 network.
- `nmap -sn 192.168.0.1-10`  
  Ping-scan a small IP range.
- `nmap -sn example.thm`  
  Discover whether a named host is up.
- `nmap -sL 192.168.0.0/24`  
  List the targets that would be scanned (no probes sent).
- Discovery probe tuning (examples — advanced):  
  - `-PS22,80` → send TCP SYN to ports 22 and 80 for host discovery.  
  - `-PA443` → send TCP ACK to port 443.  
  - `-PU53` → send UDP probe to port 53.

## Notes
- On **local networks** ARP is used and you typically get MAC addresses and vendor info (helpful to guess device types). Output shows `Host is up` plus latency and MAC vendor when available.  
- On **remote networks** Nmap will try ICMP, TCP, and UDP probes; routers and intermediate devices can produce ICMP unreachable messages that affect results.  
- `-sn` is quieter than full port scans (good for inventory/low-noise discovery) but **does not reveal open services** — use a port scan when you need service information.


## Port Scanning

### Concepts learned
- **Goal:** discover which TCP/UDP ports on a host have services listening.  
- **TCP vs UDP:** TCP is connection-oriented (3-way handshake), UDP is connectionless — both have 65,535 ports.  
- **Connect scan (`-sT`)**: completes the full TCP handshake (equivalent to trying to `telnet` to a port). Works without raw-socket privileges but is noisier.  
- **SYN scan (`-sS`)**: sends a SYN and inspects the reply without completing the handshake — faster and “stealthier” (requires root/raw sockets).  
- **UDP scan (`-sU`)**: probes UDP ports; responses (or ICMP port-unreachable) indicate state. UDP scanning is slower and less reliable.  
- **Port selection:** Nmap scans the top 1,000 ports by default; use `-F`, `-p`, or `-p-` to change scope.

## Commands / tools
- `nmap -sT <target>`  
  TCP connect scan (completes full handshake).
- `sudo nmap -sS <target>`  
  TCP SYN (stealth) scan — preferred for speed/stealth when you have privileges.
- `sudo nmap -sU <target>`  
  UDP scan — probe common UDP services (DNS, NTP, SNMP, etc.).
- `nmap -F <target>`  
  Fast mode: scan the 100 most common ports.
- `nmap -p 1-1024 <target>`  
  Scan a specific port range.
- `nmap -p- <target>`  
  Scan all TCP ports (1–65535).
- (Manual check) `telnet <host> <port>`  
  Quick test for establishing a TCP connection to a port (connect-scan style).

## Notes
- **Privileges matter:** raw-packet scans (SYN, many NSE scripts, ARP discovery) need root/sudo. Connect scans (`-sT`) work without root.  
- **SYN vs Connect:** SYN scans tend to generate fewer application-level logs because connections aren’t completed; however, modern IDS/host logging often captures SYN activity. Treat "stealth" as relative, not invisible.  
- **UDP caveats:** UDP scans are slow and prone to false negatives — many services don't respond, and ICMP unreachable messages can be rate-limited or blocked. Consider combining UDP scans with service/version checks for confirmation.  
- **Default ports:** Nmap’s default (top 1000) covers common services; use `-p-` for a thorough audit but expect longer runtime and more noise.  
- **Tune for environment:** use timing (`-T`) and retries to balance speed vs reliability; faster scans may increase false positives/alerting.  
- **Safety & ethics:** scanning can be disruptive and is often logged; only scan systems you own or have explicit permission to test.


## Version & OS Detection

### Concepts learned
- **OS detection (`-O`)**: Nmap fingerprints the target's TCP/IP stack and other responses to make an educated guess about the operating system (e.g., "Linux 4.x|5.x"). Results are heuristic — helpful clues but not guaranteed accurate.  
- **Service/version detection (`-sV`)**: Probes open ports to identify the application and version (e.g., `OpenSSH 8.9p1`), which is useful for vulnerability assessment and prioritization.  
- **All-in-one aggressive (`-A`)**: Enables OS detection, version detection, script scanning, and traceroute in a single run for a richer picture (noisy and more intrusive).  
- **Force-scan (`-Pn`)**: Skip host discovery and assume hosts are up; useful when ICMP/host discovery is blocked but increases noise and runtime.

### Commands / tools
- `sudo nmap -sS -O <target>`  
  SYN scan with OS detection.
- `sudo nmap -sS -sV <target>`  
  SYN scan with service/version detection.
- `sudo nmap -A <target>`  
  Aggressive scan: OS, versions, scripts, traceroute.
- `nmap -Pn <target>`  
  Treat hosts as up (skip discovery) and run scans regardless of ping responses.

### Notes
- **Accuracy:** OS and version detection are heuristic and can produce false positives/ambiguous ranges (e.g., "Linux 4.15 - 5.8"). Use these results as investigation leads, not absolute facts.  
- **Privileges:** Some detection features (especially `-O` and SYN-based scans) work best with root/administrator privileges.  
- **Noise & safety:** `-A` and aggressive version probes are noisy and may trigger IDS/IPS — get authorization and use in lab or with permission.  
- **Verification:** Always corroborate Nmap-detected versions with other evidence (service banners, authenticated probes, or manual checks).  
- **Reporting:** Nmap invites users to submit incorrect OS/version fingerprints to improve the database (`nmap.org/submit/`).  
- **When to use `-Pn`:** Use `-Pn` when hosts appear down due to filtering but you suspect services are listening; be aware it will significantly increase scan scope and noise.


## Timing & Performance Tuning

### Concepts learned
- Nmap timing controls how fast and aggressively scans run — important for stealth, reliability, and avoiding detection.  
- Timing templates `-T0`..`-T5` (or names paranoid, sneaky, polite, normal, aggressive, insane) adjust timeouts, retries, and parallelism automatically.  
- Slower templates reduce noise and likelihood of triggering IDS but greatly increase total scan time; faster templates complete quickly but are noisier and may cause packet loss or false results.  
- You can explicitly tune parallelism and send rate (`--min-parallelism`, `--max-parallelism`, `--min-rate`, `--max-rate`) for fine-grained control over probe concurrency and packet-per-second behavior.  
- `--host-timeout` sets a per-host maximum wait time to avoid indefinite hanging on slow/filtered hosts.

### Commands / tools
- `nmap -sS -T0 <target>` — paranoid timing (very slow, stealthy).  
- `nmap -sS -T2 <target>` — polite timing (reduced load).  
- `nmap -sS -T4 <target>` — aggressive timing (faster, noisier).  
- `nmap -sS -T3 <target>` — normal/default timing.  
- `nmap --min-parallelism 10 --max-parallelism 50 -p 1-1000 <target>`  
  Control minimum/maximum concurrent probes.
- `nmap --min-rate 20 --max-rate 100 -p- <target>`  
  Control send rate (packets per second) for the whole scan.
- `nmap --host-timeout 5m -p 1-65535 <target>`  
  Give up on a host after 5 minutes (avoid stuck hosts).

### Notes
- Use **slower templates** (`T0`,`T1`) when scanning sensitive networks or when you want to minimize detection — expect very long runtimes.  
- Use **faster templates** (`T4`,`T5`) in trusted lab environments where speed matters. `T3` is a safe default for typical scans.  
- `--min/max-parallelism` and `--min/max-rate` let you tune scans when default adaptive behavior doesn’t match your network conditions (e.g., on lossy links or very high-bandwidth links).  
- Rates/parallelism apply to the entire scan, not per-host — be conservative in shared environments to avoid saturating networks.  
- `--host-timeout` prevents scans from hanging on individual hosts; combine with `-Pn` carefully if ICMP is blocked.  
- Always balance speed against accuracy and stealth: extreme speed can cause dropped probes and inaccurate results; extreme slowness may be impractical.  
- When in doubt, test timing settings in a lab before running them against production targets.


## Output & Verbosity

### Concepts learned
- Nmap can show live progress and debug info (verbosity/debugging) and can save scan results in multiple formats for later analysis.  
- **Verbosity** (`-v`) reveals runtime stages (ping scan, DNS resolution, scan phase) and discovered findings as they happen; add more `v` (or numeric `-v2`, `-v4`) for extra detail.  
- **Debugging** (`-d`) is more detailed than verbosity and is intended for troubleshooting Nmap itself; levels range up to `-d9`.  
- **Output formats** let you save results for reporting or automated parsing: human-readable, XML, and grepable (and a combined option to produce all at once).

## Commands / tools
- `nmap <target> -v`  
  Verbose output (show progress and scan stages).
- `nmap <target> -vv` or `nmap <target> -v2`  
  Increase verbosity for more realtime detail.
- `nmap <target> -d` or `nmap <target> -d3`  
  Debugging output (much more detailed; `-d9` is very noisy).
- `nmap -sS 192.168.139.1 -oN report.nmap`  
  Save normal (human-readable) output to `report.nmap`.
- `nmap -sS 192.168.139.1 -oX report.xml`  
  Save XML output for machine parsing.
- `nmap -sS 192.168.139.1 -oG report.gnmap`  
  Save grepable output (useful for `grep`/`awk`).
- `nmap -sS 192.168.139.1 -oA basename`  
  Save all major formats at once (`basename.nmap`, `basename.xml`, `basename.gnmap`).

## Notes
- Use `-v` when you want to see what Nmap is doing step-by-step (helpful for long scans and learning). Verbose output often includes staged messages like "Initiating ARP Ping Scan", "Initiating SYN Stealth Scan", discovered open ports, and raw packet statistics at the end.  
- Debugging (`-d`) is intended for developers or deep troubleshooting — it prints protocol-level details and internals; expect very large output at high levels.  
- Save scans in **XML** when you need structured, machine-readable output (parsers, import to tools). The **normal** format is human-friendly and fine for reports; **grepable** (`-oG`) is convenient for quick text-processing pipelines.  
- `-oA` is handy for automation/record-keeping because it produces all common formats with a single command. Name files clearly (include timestamps) to avoid overwriting and to keep audit trails.  
- Verbosity and debug output may reveal sensitive info in logs — treat saved output as potentially sensitive and protect it appropriately.  
- Combining verbosity with slow timing or large port ranges can produce very large console output; redirect to file (`>`) if needed.  
- As always, only save and analyze scan output for systems you are authorized to test.


## Key Takeaways
- Start with host discovery to find live systems before deeper scanning.  
- Pick scan types based on goals and privileges; some are noisier, some are stealthier.  
- Include UDP checks when relevant — they’re slower and less reliable but necessary for certain services.  
- Scope port ranges thoughtfully to balance thoroughness with time and noise.  
- Version and OS detection are useful leads but not definitive — corroborate findings.  
- Use timing settings to balance speed, accuracy, and detectability; slower scans are quieter.  
- The Nmap Scripting Engine greatly extends capabilities; choose scripts by purpose and impact.  
- Save outputs in machine-readable formats for later analysis and reporting.  
- Increase verbosity or use debug mode when troubleshooting long or complex scans.  
- Always verify results with additional evidence and act within legal/ethical boundaries.  
- Maintain good operational hygiene: document scope, timestamp results, and use lab environments for risky options.

- Use `-sL` to confirm scan scope before running noisy probes.  
- Be mindful of firewalls and IDS: discovery probes can be blocked or logged. Always have authorization before scanning other networks.
