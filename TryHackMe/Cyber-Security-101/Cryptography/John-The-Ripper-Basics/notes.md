# JohnTheRipper - Basics

## Introduction
- John the Ripper (JtR) is a popular password-cracking tool. John supports many encryption technologies for Windows and Unix systems (Mac included).
- One remarkable feature of John is that it can autodetect the encryption for common formats. This will save you a lot of time in researching the hash formats and finding the correct tool to crack them.
- John is also a dictionary-based tool. This means that it works with a dictionary of common passwords to compare it with the hash in hand. Here is a common password list called rockyou.txt.
- While you can use popular wordlists like RockYou, John also has its own set of wordlists with thousands of common passwords. This makes John very effective when cracking systems with weak passwords.


## Basic terms

### Concepts Learned
- A hash is a fixed-length representation of input data produced by a hashing algorithm.
- Popular hash algorithms: MD4, MD5, SHA1, NTLM.
- Hashing is a one-way function — easy to compute forward, hard to reverse.
- The difficulty of reversing a hash relates to complexity classes (P vs NP) — hashing is easy to compute, finding the preimage is computationally infeasible in general.
- Dictionary attacks: hash many candidate words and compare results to a target hash.
- John the Ripper (Jumbo) is a commonly used tool for fast dictionary and brute-force cracking.

### Commands
- No specific commands for this topic.

### Notes
- Hash functions map inputs of any length to a fixed-length string, masking the original data.
**Example MD5 outputs:**
  - polo → b53759f3ce692de7aff1b5779d3964da
  - polomints → 584b6e4f4586e136bc280f27f9c64f3b
  - Both examples produce 32-character MD5 hashes despite differing input lengths.
- One-way property: generating a hash from input is straightforward; recovering input from hash is generally infeasible without additional information.
- Practical cracking bypasses the one-way property by trying many inputs (e.g., dictionaries); when a generated hash equals the target, the original input is recovered.
- This room uses the Jumbo variant of John the Ripper for practical exercises.


## Creating basic hashes

### Concepts Learned
- John the Ripper basic structure: john [options] [file path].
- Wordlist mode: John tries candidate passwords from a supplied wordlist.
- Automatic detection: John can try to detect hash types automatically (useful for quick attempts but not always reliable).
- Hash identification: use a separate identifier to determine likely hash formats, then force John to that format.
- Formats: John uses specific format names (often raw- prefixed for common hashes); list formats to check exact names.

### Commands
- Basic invocation: john /path/to/hashfile.txt
- Wordlist mode: john --wordlist=/usr/share/wordlists/rockyou.txt /path/to/hashfile.txt
- Download & run hash identifier: wget <url-to-hash-id.py> then python3 hash-id.py and paste the hash when prompted
- Force a format with a wordlist: john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt /path/to/hashfile.txt
- List all formats: john --list=formats (or john --list=formats | grep -iF "md5" to search)
- Show cracked results: john --show /path/to/hashfile.txt
- Incremental/brute-force mode: john --incremental /path/to/hashfile.txt
- Wordlist + rules: john --wordlist=/usr/share/wordlists/rockyou.txt --rules /path/to/hashfile.txt

### Notes
- Running john without extra options will try to auto-detect the hash type and pick strategies — quick but sometimes wrong.
- Wordlist mode hashes each candidate with the chosen algorithm and compares it to the target hash.
- If automatic detection fails, identify the hash type (e.g., with hash-id.py) and use --format= to force the correct format.
- Many standard hash types require a raw- prefix in John (e.g., raw-md5), but confirm with --list=formats.
- hash-id.py or similar tools return probable formats — try the top suggestions first.
- Use --show to confirm cracked passwords and map them back to the original hashes.
- Combining wordlists (rockyou, custom lists) with rules is far more effective than pure brute-force for common passwords.
- Practical files for the room are in ~/John-the-Ripper-The-Basics/Task04/ on the VM.
- Lab: cracked several task hashes — hash1.txt (MD5) → biscuit; hash2.txt (SHA1) → kangeroo; hash3.txt (SHA256) → microphone; hash4.txt (Whirlpool) → colossal.


## Cracking Windows Authentication Hashes

### Concepts Learned
- Authentication hashes: hashed passwords stored by OSes; can be cracked or abused (e.g., pass-the-hash).
- NT hash / NTLM: modern Windows format for storing user/service passwords (often referred to as NTLM).
- SAM and NTDS.dit: SAM stores local account hashes; NTDS.dit holds Active Directory hashes.
- Common acquisition methods: dumping SAM, using Mimikatz, or extracting from NTDS.dit (requires privileges).
- Attack options: crack weak hashes with wordlists/rules or reuse them directly with pass-the-hash techniques.

### Commands
- Basic John invocation: john /path/to/ntlm_hashes.txt
- Wordlist mode: john --wordlist=/usr/share/wordlists/rockyou.txt /path/to/ntlm_hashes.txt
- Force NT/NTLM format: john --format=nt --wordlist=/usr/share/wordlists/rockyou.txt /path/to/ntlm_hashes.txt
- List formats to confirm naming: john --list=formats | grep -i nt

### Notes
- NTLM (NThash) is what's commonly used on modern Windows to store password hashes.
- You often need elevated access to obtain these hashes; acquisition tools include Mimikatz or direct NTDS.dit/SAM extraction.
- Cracking is useful when pass-the-hash is not possible or when you need the plaintext for other steps.
- Lab: cracked an NTLM hash during the exercises — plaintext was mushroom.


## Cracking /etc/shadow Hashes

### Concepts Learned
- /etc/shadow stores Linux password hashes and related metadata; usually root-only access.
- You need sufficient privileges to read /etc/shadow (or a copy) to attempt cracking.
- John needs a combined passwd+shadow format to parse Linux hashes correctly — that’s what unshadow does.
- Common Linux hash formats include sha512crypt (often $6$), bcrypt, etc.; you may need to force the format for reliable cracking.

### Commands
- Combine passwd and shadow: unshadow /path/to/passwd /path/to/shadow > unshadowed.txt
- Run John against the unshadowed file (example forcing sha512crypt): john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
- List John formats to confirm names: john --list=formats
- Show cracked results: john --show unshadowed.txt

### Notes
- unshadow merges matching lines from /etc/passwd and /etc/shadow into a format John understands.
- You can supply entire passwd/shadow files or just the relevant user lines (e.g., root) to unshadow.
- Many Linux installs use sha512crypt (noted by $6$) — check and force format if auto-detection fails.
- If you can’t read /etc/shadow on a target, privilege escalation or dump tools are required (requires caution and authorization).
- Lab: cracked the provided root hash — plaintext password: 1234.


## Single Crack Mode

### Concepts Learned
- Single mode builds a targeted wordlist from account data (username, GECOS fields) and mangles those words to generate password guesses.
- Word mangling applies small mutations: numbers appended, letter-case changes, special characters, common leet substitutions, etc.
- GECOS (the fifth field in /etc/passwd) can supply useful user info (full name, home dir, etc.) that John uses to expand its candidate list.
- Single mode is effective against weak passwords derived from user info and is faster than blind brute-force for such cases.

### Commands
- Use single mode: john --single --format=raw-sha256 hashes.txt
- Force format if needed: john --single --format=sha512crypt unshadowed.txt
- Prepare file for single mode by prepending username: joker:1efee03cdcb96d90ad48ccc7b8666033 (username lowercase as appropriate)

### Notes
- Single mode does not need an external wordlist — it generates candidates from usernames/GECOS and applies mangling rules.
- To use single mode, provide entries in the username:hash form so John can extract the username for generation.
- Mangling examples for username "Markus": Markus1, MArkus, Markus!, MARKUS123, markus$ — John automates these variations based on rules.
- GECOS data (full name, office, phone) increases candidate relevance — include it when available.
- Single mode is a good first step for user-based hashes before moving to broader wordlists or brute-force.
- Lab: cracked the provided Joker hash — plaintext password: Jok3r.


## Custom Rules

### Concepts Learned
- Custom rules let you define how John mutates words from a wordlist to match predictable password patterns.
- Rules are useful when you know likely password structure (e.g., capital first letter, number + symbol at end).
- Mangling modifiers: Az (append), A0 (prepend), c (capitalize positionally) — combine them for finer control.
- Character sets in rules define what gets appended/prepended, e.g., [0-9], [A-Z], [a-z], [!£$%@].
- Jumbo John ships with many built-in rules; custom rules supplement or target specific patterns you expect.

### Commands
- john with a custom rule: john --wordlist=/path/to/wordlist --rule=PoloPassword /path/to/hashfile
- list John formats: john --list=formats
- view john.conf to edit or add rules: open /opt/john/john.conf or /etc/john/john.conf depending on install

### Notes
- john.conf is where rules are defined (TryHackMe AttackBox: /opt/john/john.conf; package installs often use /etc/john/john.conf).
- Define a rule block header like [List.Rules:RuleName] and add rule lines beneath it.
**Example rule to match a pattern like Polopassword1!:**
  - Rule header: [List.Rules:PoloPassword]
  - Rule body: cAz"[0-9] [!£$%@]"
  - Meaning: c capitalizes the first letter; Az appends; [0-9] picks a digit; [!£$%@] picks a symbol.
  - Character-set shorthand notes: [a] is literal 'a'; [0] is literal '0'; [A-z] includes both cases (be careful with ranges).
- Test rules incrementally — talk out the intended pattern while writing the rule to avoid syntax mistakes.
- If your syntax fails, check Jumbo John’s rules around the built-in list for examples and edge cases.
- Use custom rules when you can predict password structure (corporate policies or observed user behavior); otherwise rely on jumbo rules + wordlists.


## Cracking Password Protected Zip Files

### Concepts Learned
- John can crack password-protected ZIP files after converting them into a hash-like format John understands.
- zip2john converts ZIP archives into an attackable format (extracts the password-relevant data).
- Once converted, treat the output like any other hash file and run John with wordlists/rules.
- This workflow mirrors unshadow → john for /etc/shadow, but uses zip2john → john.

### Commands
- Convert a zip to John format: zip2john zipfile.zip > zip_hash.txt
- Crack the resulting file with a wordlist: john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
- Force formats or add rules as needed: john --format=[format] --wordlist=/path/to/wordlist --rule=RuleName zip_hash.txt
- Show cracked results: john --show zip_hash.txt

### Notes
- zip2john extracts the necessary verification data from the ZIP and outputs it in a form John can parse.
- Use a wordlist + rules first; brute-force/incremental only if necessary.
- Keep the original ZIP safe; work with the converted hash file for cracking attempts.
- Lab: cracked the provided secure.zip — password: pass123.


## Cracking Password-Protected RAR Archives

### Concepts Learned
- RAR archives are compressed files (created by WinRAR) that can be password-protected.
- John can crack RAR passwords after converting the archive into a John‑readable hash format.
- rar2john extracts the password-relevant data from a RAR and outputs it for John to attack.
- Workflow: convert archive → crack converted output with wordlists/rules → verify cracked result.

### Commands
- Convert RAR to John format: rar2john rarfile.rar > rar_hash.txt
- Crack the resulting file with a wordlist: john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
- Force formats or add rules if needed: john --format=[format] --wordlist=/path/to/wordlist --rule=RuleName rar_hash.txt
- Show cracked results: john --show rar_hash.txt

### Notes
- rar2john extracts the verification data and writes it to a file John can parse; work on that file rather than the original archive.
- Start with wordlists + rules; fall back to incremental/brute-force only if necessary.
- Keep the original archive backed up and work on the converted hash file for repeated attempts.
- Lab: cracked the provided secure.rar — password: password.


## Cracking SSH Keys with John

### Concepts Learned
- SSH private keys (id_rsa) can be encrypted with a passphrase; cracking the passphrase allows using the key for authentication.
- John can crack SSH key passphrases after converting the key into a John-readable format.
- ssh2john (or ssh2john.py) converts id_rsa into a hash-like output John can attack.
- Workflow: convert key → run John with wordlists/rules → verify cracked passphrase.

### Commands
- Convert id_rsa to John format: ssh2john id_rsa > id_rsa_hash.txt (or python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt)
- Crack the converted output with a wordlist: john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
- Show cracked result: john --show id_rsa_hash.txt
- If ssh2john not in PATH, run the script from its location: python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt

### Notes
- ssh2john extracts the encrypted-key metadata into a format John understands; work on that file for cracking.
- Start with wordlists + rules before attempting incremental brute-force.
- Keep the original key file backed up and work on the converted hash file for repeated attempts.
- Lab: cracked the provided SSH private key — passphrase: mango.


## Key Takeaways
- Hashes map data of any length to a fixed-length string and are designed to be one-way (easy to compute, hard to reverse).
- Identifying the hash type first speeds up cracking — use an identifier (e.g., hash-id) and then force John to the correct format.
- John the Ripper’s common workflow: convert target (if needed) → prepare input in the format John expects → run with wordlists and rules → verify with --show.
- Automatic detection is a useful quick attempt, but forcing --format= is more reliable and often much faster.
- Wordlists + rules are the most efficient first approach; incremental/brute-force is a last resort.
- Single mode generates targeted guesses from usernames/GECOS and is effective against passwords derived from user info.
- Custom rules in john.conf let you model predictable password structures (prepend/append, capitalization, symbol/number placement).
- Always convert special targets to John-friendly formats: unshadow (passwd+shadow), zip2john (ZIP), rar2john (RAR), ssh2john (SSH keys).
- For Windows hashes, NTLM (NThash) is common; you may also be able to reuse hashes directly with pass-the-hash where applicable.
- For Linux, combine passwd and shadow with unshadow and check formats like sha512crypt ($6$) when cracking /etc/shadow.
- Record lab results consistently (file, hash type, cracked value or redact) and keep wordlists/rules referenced for reproducibility.
- Keep sensitive plaintext out of public repos or redact before publishing; store sensitive data in private storage if needed.
- Start targeted (single mode, forced format, custom rules) before escalating to broad attacks — it saves time and increases success rate.
- Jumbo John includes many built-in rules; use them as a baseline and add custom rules only when you can predict patterns.
- Always validate cracked results and document methods used (wordlist name, rules, format) so you can reproduce or audit your steps.
