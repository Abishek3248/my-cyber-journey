# Cheatsheet - JohnTheRipper Basics

| Concept              | Commands/Explanation                                                                |
|----------------------|-----------------------------------------------------------------------------|
| **Basic john run**   | john /path/to/hashfile.txt — auto-detects format(s) and runs default cracking modes. |
| **Wordlist mode** | john --wordlist=/usr/share/wordlists/rockyou.txt /path/to/hashfile.txt — best first attempt; fast and practical.   |
| **Force format**  | john --format=raw-md5 --wordlist=... /path/to/hashfile.txt — use --format= when auto-detect fails (many plain hashes use raw- prefix).     |
| **List formats**     | john --list=formats — view supported formats to choose the correct --format=.             |
| **Show cracked / pot**   | john --show /path/to/hashfile.txt — display cracked plaintexts (checks ~/.john/john.pot).        |
| **Single mode**|john --single --format=raw-sha256 unshadowed.txt — username-based mangling; input often user:hash (use unshadow). |
| **Incremental (brute)**       |john --incremental /path/to/hashfile.txt — exhaustive brute-force; very slow, use only as last resort.    |
| **Use custom rule**   | john --wordlist=/path/to/wordlist --rule=RuleName /path/to/hashfile.txt — define RuleName in john.conf under [List.Rules:RuleName].                |
| **View / edit rules**|Open /etc/john/john.conf or /opt/john/john.conf — Jumbo John includes many example rules to adapt.          |
| **Identify hash (local helper)**            | python3 hash-id.py <hash> — helps guess hash type; always confirm with context and --list=formats.                      |
| **unshadow (passwd+shadow)**            | unshadow /path/to/passwd /path/to/shadow > unshadowed.txt — creates user:hash file usable by John (requires root).|
|**zip2john (zip)**|zip2john secure.zip > zip_hash.txt — convert ZIP to John-readable hash for cracking.|
|**zip2john (zip)**|zip2john secure.zip > zip_hash.txt — convert ZIP to John-readable hash for cracking.|
|**rar2john (rar)**|rar2john secure.rar > rar_hash.txt — extract RAR password-hash for John.|
|**ssh2john (SSH key)**|ssh2john id_rsa > id_rsa_hash.txt — prepare private-key passphrase hash for cracking.|
|**Check john pot file**|john --show /path/to/hashfile.txt — verify which hashes are cracked and map plaintexts to hashes.|
|**Use rules file explicitly**|john --rules --config=/path/to/john.conf --wordlist=wl hashes.txt — point John to custom rules/config when needed.|
|**Typical formats to try**|raw-md5, raw-sha1, raw-sha256, nt (NTLM), sha512crypt (often $6$ in /etc/shadow).|
|**Recommended first approach**|Wordlist + rules + forced format — fastest and highest-yield strategy before resorting to brute force.|
