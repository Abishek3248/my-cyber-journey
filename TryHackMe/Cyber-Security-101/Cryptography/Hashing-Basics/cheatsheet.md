# Cheatsheet - Hashing Basics

| Concept              | Key Points                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| **Hashing Basics**   | Fixed-size output, deterministic, avalanche effect (tiny change → big diff). |
| **Password Storage** | Never store plaintext; use salts + slow, secure algorithms (bcrypt, scrypt, Argon2, yescrypt). |
| **Common Prefixes**  | `$y$` yescrypt, `$2b$` bcrypt, `$6$` sha512crypt, `$1$` md5crypt, etc.      |
| **Linux Hashes**     | Stored in `/etc/shadow` → format: `$prefix$options$salt$hash`.              |
| **Windows Hashes**   | Stored in SAM; NTLM (MD4 variant) used. Context helps identify type.        |
| **Password Cracking**| Hashes can’t be decrypted — use tools (Hashcat, John the Ripper) + wordlists. |
| **GPU vs CPU**       | GPUs = faster cracking for many hashes; bcrypt resists GPU acceleration.    |
| **VMs & Cracking**   | VM GPU passthrough is slow — better to run Hashcat on host.                 |
| **Integrity Checking**| Verify file authenticity (e.g., `sha256sum`), detect duplicates.           |
| **HMACs**            | Hash + secret key → ensures authenticity & integrity.                       |
| **Tools**            | `hashcat`, `john`, `sha256sum`, `man 5 shadow`, Hashcat example hashes page.|
