# Cryptography Module — README

## What I Learned and Gained
- Through this module I built a practical foundation in modern cryptography and its applications for securing communications, authentication, and data integrity. I learned both the theory (how primitives work and why they’re secure) and hands‑on workflows for using and assessing real tools (SSH, certificates, hashing, and password‑cracking toolchains).

## Key Concepts Covered
- Cryptography fundamentals — purpose (confidentiality, integrity, authenticity), plaintext vs ciphertext, ciphers, and basic crypto math (XOR, modulo).
- Historical ciphers — Caesar, Vigenère, Enigma, and one‑time pad — why they matter historically and why they are insecure today.
- Symmetric encryption — shared‑key model, common ciphers (DES, 3DES, AES), and key distribution challenges.
- Asymmetric encryption & key exchange — public/private key pairs, RSA basics, Diffie‑Hellman key agreement, and when to use asymmetric vs symmetric algorithms.
- Public‑key applications — SSH key authentication, server/client authentication, and practical key management (key generation, known_hosts, authorized_keys).
- Digital signatures & certificates — signing for integrity/authenticity, certificate chains, and trust models used by TLS/HTTPS.
- PGP/GPG — public‑key email/file encryption, signing, key generation and import/export workflows.
- Hashing basics — properties of hash functions (fixed output, deterministic, avalanche), collision concepts, and common hash algorithms and weaknesses (MD5, SHA1).
- Secure password storage — salts, slow KDFs (bcrypt, scrypt, Argon2, yescrypt), and why encryption is not a substitute for proper hashing.
- Recognising & cracking hashes — /etc/shadow formats, common prefixes, NTLM context, and using Hashcat / John the Ripper with wordlists and rules.
- Integrity & HMACs — verifying downloads (sha256sum), duplicate detection, and keyed HMAC for combined integrity+authenticity.
- Practical tooling — using John the Ripper (modes, formats, conversion helpers), Hashcat for GPU cracking, and GPG/ssh-keygen workflows.

## Practical Skills
- Generated and managed SSH and GPG keypairs, and understood secure handling of private keys (permissions and passphrases).
- Performed RSA/Diffie‑Hellman conceptual calculations and recognised the security assumptions behind them.
- Identified hash types from context and prefixes, and applied appropriate cracking workflows (wordlists + rules → tuned attacks → fallback brute force).
- Used unshadow, zip2john, ssh2john, and other converters to prepare targets for John the Ripper; managed results with john --show.
- Verified file integrity with hash utilities and validated signed checksum files (PGP‑signed checksums).
- Explained how TLS, SSH, and VPNs rely on these primitives to secure real network traffic.
- Applied secure password storage best practices: unique salts + memory/CPU‑hard KDFs (Argon2, bcrypt, scrypt, yescrypt).

## Overall Takeaway

- This module tied cryptographic theory to everyday security practice. I can now explain why different primitives exist, choose appropriate algorithms for confidentiality/integrity/authentication, manage public‑key credentials (SSH/GPG/TLS), and evaluate or perform practical tasks such as verifying integrity, recognising hash formats, and responsibly preparing and executing password‑cracking workflows for assessment and defensive hardening.
