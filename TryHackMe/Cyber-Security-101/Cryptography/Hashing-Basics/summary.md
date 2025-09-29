# Summary – Hashing Basics

**In this room, I explored the foundations and applications of hashing from both defensive and offensive security perspectives.**

- Learned the **properties of hash functions**: fixed-size output, deterministic behavior, and the avalanche effect.  
- Understood **secure password storage** practices: using salts and slow algorithms (bcrypt, scrypt, yescrypt, Argon2) instead of weak ones like MD5 or SHA1.  
- Studied how **Linux systems** store password hashes in `/etc/shadow` with the format `$prefix$options$salt$hash`.  
- Examined **Windows password hashing** with NTLM stored in the SAM file, highlighting the role of context in identifying hash types.  
- Practiced **hash recognition**, using prefixes, context clues, and tools to determine hash algorithms.  
- Gained experience in **password cracking** using Hashcat and John the Ripper with wordlists like `rockyou.txt`.  
- Learned the role of **GPUs** in accelerating cracking, while understanding limitations in VMs and resistance in algorithms like bcrypt.  
- Explored **hashing for integrity checking**: verifying file authenticity with tools like `sha256sum` and detecting duplicate files.  
- Understood **HMACs (Hash-based Message Authentication Codes)** as a way to combine a secret key with a hash function for ensuring both integrity and authenticity.  

**This room strengthened my understanding of how hashes secure authentication systems, how attackers attempt to crack them, and how hashing also plays a critical role in verifying data integrity.**  
