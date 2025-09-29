# Hashing Basics

## Introduction
- A hash value is a fixed-size string or characters that is computed by a hash function. A hash function takes an input of an arbitrary size and returns an output of fixed length, i.e., a hash value. We will cover various exciting and clever uses of hash functions and values in this room.


## Hash Functions

### Concepts Learned
- Hash Functions
- Hash Collisions
- Importance of Hashing
- Common Hash Algorithms: MD5, SHA1, SHA256

### Explanation
- Hash functions take input of any size and produce a fixed-size output called a digest.
- Hashing does not use a key and is one-way: original input cannot be recovered from the hash.
**A good hash function is:**
  - Fast to compute
  - Unpredictable
  - Sensitive to input changes (small change in input drastically changes output – avalanche effect)
  - Hashing ensures data integrity and is widely used for password storage, file verification, and digital signatures.
  - Collisions happen when two different inputs produce the same hash; secure hash functions make collisions extremely unlikely.
  - Older algorithms like MD5 and SHA1 are insecure due to vulnerability to engineered collisions.

### Notes
- Hash functions produce fixed-length outputs regardless of input size.
- Output is usually encoded in hexadecimal or base64.
- Servers store password hashes, not plaintext passwords.
- Minor input changes create drastically different outputs.
- Collisions are inevitable (pigeonhole principle), but good hash functions minimize collision probability.
- MD5 and SHA1 are deprecated for security-critical applications; use SHA256 or higher.


## Insecure Password Storage for Authentication

### Concepts Learned
- Storing passwords securely is essential for authentication in web applications.
- Storing passwords in plaintext is highly insecure and exposes users to data breaches.
- Deprecated or weak encryption algorithms should not be used for password storage.
- Using insecure hash functions, such as SHA-1 without salting, compromises password security.
- Salting adds a random value to passwords before hashing to prevent attacks like rainbow table lookups.

### Explanation
- Web applications often need to verify user passwords for authentication. Poor password storage practices can compromise user security, especially if passwords are reused across multiple accounts. Three common insecure practices are: storing passwords in plaintext, using deprecated encryption, and using insecure hashing algorithms without proper protections like salting.
- Plaintext storage: Exposes all user passwords if the database is leaked. Example: RockYou breach with 14 million plaintext passwords.
- Insecure encryption: Deprecated encryption can be reversed to reveal passwords. Example: Adobe breach included password hints in plaintext.
- Insecure hashing: Weak hash functions without salting can be cracked efficiently. Example: LinkedIn breach used unsalted SHA-1 hashes.

### Notes
- RockYou.txt is a well-known list of leaked plaintext passwords.
- Salting hashes makes precomputed attacks (like rainbow tables) ineffective.
- Modern applications should use strong hashing algorithms like bcrypt, scrypt, or Argon2 for password storage.
- Avoid storing passwords directly or using outdated cryptographic methods.


## Using Hashing To Store Password

### Concepts Learned
- Storing password hashes instead of plaintext passwords improves security in case of database leaks.
- Hash functions always produce the same output for the same input, which can lead to duplicate hashes for identical passwords.
- Rainbow tables are precomputed hash-to-password lookup tables that can efficiently crack unsalted hashes.
- Adding a unique salt to each password prevents rainbow table attacks and ensures identical passwords produce different hashes.
- Secure hashing algorithms like Argon2, Bcrypt, Scrypt, or PBKDF2, combined with salts, are recommended for password storage.
- Encrypting passwords directly is less secure because the encryption key must be stored, making all passwords vulnerable if the key is compromised.

### Explanation
- Hashing allows storing only the hash of a password instead of the password itself.
- If a database is leaked, attackers must brute-force each hash to retrieve passwords.
- Identical passwords produce identical hashes, which can be exploited with rainbow tables.
- Rainbow tables are precomputed tables mapping hashes to common passwords.
- Adding a salt, a random value unique to each user, prevents rainbow table attacks.
- Salts are concatenated with the password before hashing.
- Modern hashing algorithms like Bcrypt, Scrypt, or Argon2 handle salting automatically.
- Encrypting passwords is discouraged because storing the encryption key creates a single point of failure.

### Notes
- Rainbow tables can crack unsalted hashes quickly using precomputed tables (e.g., CrackStation, Hashes.com).
- Salts should be unique per user and stored alongside the hash; they do not need to be secret.
**Best practices for password storage:**
  - Use a secure hashing algorithm (Argon2, Bcrypt, Scrypt, PBKDF2).
  - Generate a unique salt for each password.
  - Concatenate the salt and password, then compute the hash.
  - Store both the hash and the salt in the database.
  - Avoid encrypting passwords; if the encryption key is exposed, all passwords are compromised.
 

## Recognising Password Hashes

### Concepts Learned
- hash identification tools exist but are not always reliable; context matters when identifying hash types.
- Linux stores password hashes in /etc/shadow with a recognizable prefix format that indicates the hashing algorithm and parameters.
- Modern Unix-style password entries include prefix, options, salt, and hash in the form $prefix$options$salt$hash.
- Windows stores password hashes in the SAM database (NTLM / MD4-style); these can look similar to MD5/MD4 hashes and require context to identify.
- Learning common prefixes and formats (and consulting sources like Hashcat examples) speeds up recognition and cracking efforts.

### Explanation
- Use tools + context: Run automated detectors (hashID, etc.) but confirm results using where the hash came from (web DB, /etc/shadow, SAM dump) and known formats.
- Linux /etc/shadow format: Each user line is colon-separated; the password field often uses the $...$...$... format. The first $-prefixed token indicates algorithm.
- Prefix meaning: $prefix$options$salt$hash → prefix = algorithm id, options = algorithm parameters, salt = per-user random value, hash = resulting digest.
- Why salt matters: Salt prevents identical passwords having identical hashes and defeats precomputed rainbow tables.
- Windows hashes: NTLM (MD4 variant) and LM appear in SAM dumps; tools like Mimikatz can extract them. Their raw hex lengths can resemble other hash types, so use context.
- When unsure: Check hash length, character set, presence of separators ($), and the source application; consult Hashcat/John example lists for likely formats.

### Notes
- Tools like hashID help but always confirm results with context (where the hash came from).
- Linux /etc/shadow entries use the format $prefix$options$salt$hash, where the first $ token identifies the algorithm.
- Common Unix prefixes: $y$ (yescrypt), $7$ (scrypt), $2b$/$2y$ (bcrypt), $6$ (sha512crypt), $1$ (md5crypt).
- Windows password hashes come from the SAM database (NTLM/MD4-style) and can resemble MD5—use source/context to tell them apart.
- If a hash has a $ prefix, parse it first to find algorithm and salt.
- When unsure, check length/charset, source file, and Hashcat/John example lists before attempting cracking.


## Cracking Passwords

### Concepts Learned
- Password hashes cannot be “decrypted”; they must be cracked by guessing inputs, hashing them the same way, and comparing outputs.
- Rainbow tables are precomputed hash→plaintext lookup tables and only work against unsalted hashes.
- Modern cracking often uses GPU acceleration (e.g., Hashcat) for huge performance gains; some algorithms (bcrypt, scrypt, Argon2) are deliberately slow/CPU‑friendly to resist this.
- Salts (unique, per‑user random values) defeat rainbow tables and force per‑hash cracking efforts.
- Context (where the hash came from, hash format/prefix, length/charset) is essential for identifying the hash type before attempting to crack it.
- Cracking tools include Hashcat (GPU‑focused) and John the Ripper (CPU by default); choose the tool and environment accordingly.

### Explanation
- Cracking = generate candidate passwords → apply same hash algorithm (and salt if present) → compare with target hash. No key exists to “reverse” a hash.
- If a hash is unsalted, rainbow tables or simple lookups can be extremely fast; if salted, you must compute hashes per candidate per salt.
- GPUs massively parallelize the hash function computations, making dictionary, brute‑force, and combinator attacks far quicker for GPU‑friendly algorithms. For memory-/CPU‑hard algorithms (bcrypt, scrypt, Argon2) GPUs provide much less advantage.
- Virtual machines often lack direct GPU access (or are slower when passthrough is configured); for best performance run GPU cracking on the host. John the Ripper is convenient for CPU/VM use.
- Always identify the correct hash format first (prefixes, length, encoding) — using the wrong hash mode wastes time and resources. Use reputable wordlists (e.g., rockyou) and tailored rules/masks to improve success rates.

### Notes (hands‑on)
- Performed the lab exercises using Hashcat and John the Ripper to practise cracking a variety of hashes (unsalted, salted, and bcrypt/similar).
- Used wordlist (rockyou) and targeted modes to recover several passwords and verified how salts and stronger algorithms slow down cracking.
- Observed significant speed improvements when running GPU‑accelerated Hashcat on the host; confirmed that bcrypt/scrypt hashes resisted GPU advantage and required much longer runtimes.
- Took care to follow ethical guidelines: exercises performed only on authorised lab hashes and systems.


## Hashing For Integrity Checking

### Concepts Learned
- Hashing is used for file integrity verification.
- HMAC ensures both authenticity and integrity.

### Explanation
- Hashing allows us to confirm files haven’t been altered; even a 1-bit change produces a totally different hash. Comparing downloaded file hashes with official checksums ensures authenticity of the file.
- Hashes can also identify duplicate files since identical files produce identical hashes.
- HMAC (Hash-based Message Authentication Code) combines a cryptographic hash with a secret key. This proves the sender is genuine (authenticity) and that the message wasn’t altered (integrity).

### Notes
- Tools like sha256sum are commonly used for integrity checking of downloaded files.
- HMAC uses a secret key + hash function; final value is a fixed-length string.


## Key Takeaways
- Hashing fundamentals: Hash functions generate fixed-size outputs, are deterministic, and small input changes cause big output differences.
- Password storage: Storing plaintext passwords, using weak encryption, or outdated algorithms (like SHA-1) is insecure. Secure methods use strong, salted, and computationally expensive algorithms (e.g., bcrypt).
- Password cracking: Hashes can’t be decrypted; they must be cracked by comparing guesses. Tools like Hashcat and John the Ripper leverage CPUs/GPUs and wordlists such as rockyou.txt. Salting and slow hashing greatly increase resistance.
- Integrity checking: Hashes verify that files haven’t been tampered with, useful for software downloads and detecting duplicates.
- HMACs: Combine hashing with a secret key to ensure both authenticity (the source is genuine) and integrity (data is unmodified).
- Practical experience: Applied concepts by cracking sample hashes, reinforcing the importance of secure storage practices and strong hashing mechanisms.
