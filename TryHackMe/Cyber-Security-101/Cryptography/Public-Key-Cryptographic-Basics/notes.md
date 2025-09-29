# Public Key Cryptographic Basics

## Introduction
- A public key is a user's publicly available unique key used in asymmetric cryptography (or public key encryption) to encrypt data or verify digital signatures. It is part of a key pair, where the other key is the private key, which remains confidential. This cryptographic system ensures secure communication and authentication over untrusted networks. It Includes:
  - Authentication: You want to be sure you communicate with the right person, not someone else pretending.
  - Authenticity: You can verify that the information comes from the claimed source.
  - Integrity: You must ensure that no one changes the data you exchange.
  - Confidentiality: You want to prevent an unauthorised party from eavesdropping on your conversations.


## Common Use Of Asymmetric Encryption

### Concepts Learned
- Asymmetric encryption is used to securely exchange keys for symmetric encryption.
- Asymmetric encryption is slower, so it is mainly used to negotiate symmetric keys.
- Public and private keys enable secure key exchange without transmitting the key in plain text.
- Digital signatures and certificates are used to verify identity in real-world key exchanges.

### Explanation
- Asymmetric encryption allows two parties to securely agree on a symmetric encryption key.
- You encrypt the symmetric key (or instructions) using the recipient’s public key, and only their private key can decrypt it.
- Once the symmetric key is exchanged, communication continues using faster symmetric encryption.

### Notes
- The “secret code” represents the symmetric encryption cipher and key.
- The “lock” represents the public key.
- The “lock’s key” represents the private key.
- Asymmetric encryption is primarily used once for key exchange.
- Subsequent communication uses symmetric encryption for efficiency.
- Digital signatures and certificates help verify identity in real-world communication.


## RSA — Notes

### Concepts Learned
- RSA is a public‑key (asymmetric) encryption algorithm used to secure data over insecure channels.
- Security relies on the difficulty of factoring the product of two large primes.
- Public key (n, e) is used to encrypt; private key (n, d) is used to decrypt.
- RSA is slow compared to symmetric ciphers, so it’s typically used to exchange symmetric keys.
- Common RSA variables in challenges/CTFs: p, q, n, e, d, m (plaintext), c (ciphertext).

### Explanation
- Core idea: choose two large primes p and q, compute n = p * q. The hardness of factoring n (when p and q are large) is what gives RSA its security.
**Key generation (high level):**
  - compute n = p * q and φ(n) (Euler’s totient).
  - pick public exponent e such that gcd(e, φ(n)) = 1.
  - compute private exponent d so that e * d ≡ 1 (mod φ(n)).
  - public key = (n, e), private key = (n, d).
**Encryption / Decryption (modular exponentiation):**
  - Encrypt: c = m^e mod n.
  - Decrypt: m = c^d mod n.
  - Correctness follows from properties of modular arithmetic (Euler/Fermat), which ensure m is recovered.
  - Practical notes: real RSA uses very large primes (hundreds of digits). Small keys or poor parameter choices make RSA breakable.
  - Typical usage: RSA establishes or encrypts a symmetric key (e.g., for AES); subsequent bulk communication uses the faster symmetric cipher.
-CTF relevance: RSA-related tasks often require recovering p and q, deriving d, or exploiting bad parameter choices (small e, shared factors, low-entropy primes, reused n, etc.). Tools like RsaCtfTool or rsatool are commonly used.

## Notes
- p, q → prime factors (secret).
- n = p * q → modulus (public).
- φ(n) or phi(n) → Euler’s totient, used to derive d.
- e → public exponent (part of public key).
- d → private exponent (part of private key).
- m → plaintext message (numerical representation).
- c → ciphertext (c = m^e mod n).
- Watch for common CTF patterns: small e (e.g., 3), low-entropy primes, shared prime factors across multiple n, or leaks of partial key material.
- RSA is deterministic on raw plaintext—real systems use padding schemes (OAEP, PKCS#1 v1.5) to provide semantic security.


## Diffie-Hellman Key Exchange

### Concepts Learned
- Diffie-Hellman (DH) is a method for establishing a shared secret key over an insecure channel.
- It allows two parties to independently generate a symmetric key without directly transmitting it.
- DH relies on public parameters (prime p and generator g) and private secrets from each party.
- DH is often used alongside RSA for authentication and digital signatures.

### Explanation
- Goal: Two parties (Alice and Bob) want a shared symmetric key but cannot safely transmit it.
**Process (simplified):**
  - Public agreement: choose large prime p and generator g (disclosed publicly).
  - Each party selects a private key (a for Alice, b for Bob).
  - Compute public keys: Alice calculates A = g^a mod p, Bob calculates B = g^b mod p.
  - Exchange public keys over the insecure channel.
  - Compute shared secret: Alice calculates s = B^a mod p, Bob calculates s = A^b mod p. Both results are equal: s = g^(ab) mod p.
  - Security principle: While public keys are visible, deriving the private keys or shared secret from them is computationally infeasible for large p.
  - Real-world application: DH uses very large primes and is implemented in protocols like TLS for key exchange.

### Notes
- Small numbers (like p = 29, g = 3) are only illustrative and insecure.
- DH provides confidentiality of the shared secret without prior secure channels.
- Typically combined with RSA or other asymmetric cryptography for authentication to prevent man-in-the-middle attacks.
- Shared secret from DH can then be used with a symmetric cipher (AES, etc.) for actual message encryption.


## SSH

### Concepts Learned
- SSH provides encrypted, authenticated remote access (confidentiality + integrity + authentication).
- Server authentication uses host keys (fingerprints) stored in ~/.ssh/known_hosts.
- Client authentication can be password-based or key-based (public/private key pairs).
- SSH key types: common algorithms include ed25519, rsa, ecdsa; ed25519 is compact and recommended.
- Private keys must remain secret; public keys are copied to the server (~/.ssh/authorized_keys).
- SSH supports additional features: port forwarding/tunneling, SFTP, X11 forwarding.
- Key-based auth + passphrase + correct permissions is more secure than password auth.

### Explanation
- Server authentication: on first connect the client shows the server public-key fingerprint. Accepting it records the fingerprint in known_hosts. If the server’s key later changes, SSH warns of a possible MITM.
- Key pairs: generate with ssh-keygen (choose type: ed25519, rsa, etc.). The public key (*.pub) is safe to share; the private key must be protected.
- How key auth works: client proves possession of the private key; server verifies against the corresponding public key in ~/.ssh/authorized_keys. No secret is transmitted.
- Passphrases: protect private keys at rest. Passphrases decrypt the private key locally — they do not identify you to the server.
- File permissions: SSH enforces strict permissions for private keys and ~/.ssh (private key 600, ~/.ssh 700) — otherwise keys are ignored.
- Host keys & fingerprints: fingerprints (SHA256 or MD5) provide a short identifier for host keys; verify them out-of-band when possible.
- Algorithms: ed25519 gives strong security with short keys; rsa remains common (use ≥2048 bits, preferably 3072/4096).
- Practical extras: SSH can tunnel ports (local/remote/ dynamic), transfer files with sftp/scp, and forward X11 sessions.

### Notes
- Default SSH port: 22 (can be changed for obscurity but not true security).
- Store public keys on servers in ~/.ssh/authorized_keys (one key per line).
- Use ssh-copy-id or manually append id_rsa.pub / id_ed25519.pub to authorized_keys.
- Protect private keys: never share, back them up securely, use strong passphrases.
- Keep ~/.ssh and private key permissions strict (chmod 700 ~/.ssh && chmod 600 ~/.ssh/id_*).
- Verify host fingerprints on first connection if possible (out-of-band check) to prevent MITM.
- Prefer key-based auth and disable password auth for hardened servers (/etc/ssh/sshd_config).
- Remove unused keys from authorized_keys and known_hosts to reduce attack surface.
- For automation, consider agent forwarding (ssh-agent) carefully — it can expose keys if a remote host is compromised.
- Use modern key types (ed25519 / ECDSA with well-chosen curves) and retire weak algorithms (DSA, small RSA).
- SSH is not only remote shell — use it for secure file transfer (SFTP), secure tunnels (proxying), and secure port forwarding.


## Digital Signatures And Certificates

### Concepts Learned
- Digital signatures verify authenticity (who created it) and integrity (has it been altered) of digital data.
- They rely on asymmetric cryptography: private key to sign, public key to verify.
- Certificates are digital documents that link identities to public keys, establishing trust.
- Certificate Authorities (CAs) validate and vouch for certificates, forming a chain of trust.
- Digital signatures and certificates are widely used in HTTPS to secure websites.

### Explanation
- Digital signatures: produce a signature with your private key; anyone with the public key can verify it. Signing usually involves hashing the message first, then encrypting the hash. This ensures the message hasn’t been altered.
- Certificates: issued by CAs to prove that a public key belongs to a particular entity. Browsers trust CAs by default; thus, a valid certificate ensures users are connecting to the correct server.
- Chain of trust: a certificate is signed by a CA; the CA may be signed by a higher-level CA; ultimately, a trusted root CA anchors the chain. Your system/browser trusts certificates that link to these roots.
- Practical use: HTTPS websites, signed emails, software distribution, and authentication systems use digital signatures and certificates.
- Difference from electronic signatures: pasting an image of a signature does not ensure integrity or authenticity; digital signatures provide cryptographic proof.

### Notes
- Always verify digital signatures when integrity and authenticity are critical (e.g., software downloads).
- Use trusted Certificate Authorities for issuing TLS/SSL certificates.
- Free certificates can be obtained via Let’s Encrypt for HTTPS.
- Digital signatures depend on keeping your private key secure; if compromised, signatures can be forged.
- Hashing is a crucial step in creating signatures to ensure message integrity; typically done before encrypting with the private key.
- The chain of trust is automatically managed by browsers and operating systems; manual verification may be needed in sensitive scenarios.
- Digital signatures are legally recognized in many countries, similar to handwritten signatures.


## PGP And GPG

### Concepts Learned
- PGP (Pretty Good Privacy) is software for encrypting files, signing data, and protecting digital communication.
- GnuPG (GPG) is an open-source implementation of the OpenPGP standard.
- GPG is commonly used to encrypt and sign emails, ensuring confidentiality, integrity, and authenticity.
- Key pairs consist of a public key (shared) and a private key (kept secret).
- Private keys can be protected with a passphrase for additional security.

### Explanation
- Key Generation: Using gpg --full-gen-key, you can create a key pair, selecting the type of key (RSA, ECC), purpose (signing, encryption, or both), key curve, expiry date, and user identity information.
**Using GPG:**
  - Share your public key with others to allow them to encrypt messages to you.
  - Use your private key to decrypt messages encrypted with your public key.
  - You can sign messages to prove authenticity and integrity.
  - Passphrase Protection: Private keys can be encrypted with a passphrase, similar to SSH keys, to prevent unauthorized use. Tools like John the Ripper with gpg2john can attempt to crack passphrases in CTF scenarios.
  - Key Management: Always back up your private key securely. On a new machine, import the backup using gpg --import backup.key to continue decrypting messages.

### Notes
- PGP/GPG ensures confidentiality (encryption), integrity (signed messages), and authenticity (proof of sender).
- Protect your private key at all costs; compromise allows attackers to decrypt messages meant for you.
- Public keys are safe to share widely.
- GPG is widely used in CTFs for challenges involving encrypted files.
- Expiry dates can be set for keys to enforce regular rotation and security.
- Always verify imported keys to avoid man-in-the-middle attacks.


## KeyTakeaways
- Cryptography ensures confidentiality, integrity, and authenticity of data in digital communication.
- Encryption converts plaintext to ciphertext; decryption requires the correct key.
- Symmetric encryption (AES, DES, 3DES) is fast; key distribution is the main challenge.
- Asymmetric encryption (RSA, Diffie-Hellman, ECC) solves secure key exchange and authentication; used to negotiate symmetric keys.
- RSA relies on factoring large semiprimes; public key encrypts, private key decrypts.
- Diffie–Hellman Key Exchange allows two parties to establish a shared secret over an insecure channel.
- Basic math concepts: XOR is reversible and used in symmetric crypto; modulo arithmetic is crucial for asymmetric algorithms.
- Historical ciphers like Caesar Cipher are simple but insecure today.
- Key terms: plaintext, ciphertext, cipher, key, encryption, decryption.
