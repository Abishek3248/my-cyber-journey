# Cryptography Basics

## Introduction
- Cryptography is the science of securing information by transforming it into a form that is unreadable to unauthorized users while allowing legitimate parties to recover the original data. It plays a critical role in cybersecurity, ensuring confidentiality, integrity, authentication, and non-repudiation of information.
- In practice, cryptography uses mathematical algorithms and keys to encrypt (scramble) data and decrypt (unscramble) it when needed. It is applied in securing communications, protecting stored data, verifying identities, and ensuring trust in digital systems.


## Importance of Cryptography

### Concepts Learned
- Cryptography ensures secure communication in the presence of adversaries.
- Core goals: confidentiality, integrity, and authenticity of data.
- Widely used in everyday digital activities like logins, banking, file verification, and secure remote access.
- Compliance requirements (PCI DSS, HIPAA, GDPR, etc.) enforce encryption standards for sensitive data.

### Explanation
- Definition: Cryptography is the practice and study of techniques for protecting communication and data against adversaries.
- Confidentiality: Prevents unauthorized disclosure of data.
- Integrity: Prevents unauthorized alteration of data.
- Authenticity: Verifies the source of data.
**Real-world usage:**
  - Encrypted login credentials.
  - SSH sessions encrypted against eavesdropping.
  - Browser certificate checks during online banking.
  - File verification through hash functions.
**Regulations:**
  - PCI DSS → Encryption required for credit card handling (at rest and in motion).
  - HIPAA, HITECH, GDPR, DPA → Standards for securing sensitive data like medical records.
    
### Notes
- Cryptography works mostly in the background, hidden from direct user access.
- Legal frameworks enforce its use in industries dealing with financial data and personal health data.
- Without cryptography, trust in digital communication and transactions would collapse.


## Plaintext to Ciphertext

### Concepts Learned
- Plaintext is the original readable data before encryption.
- Ciphertext is the scrambled, unreadable output of encryption.
- A cipher is the algorithm that converts plaintext ↔ ciphertext.
- Keys are secret values used with ciphers for encryption and decryption.
- Encryption converts plaintext into ciphertext using a cipher and key.
- Decryption converts ciphertext back into plaintext using the correct key.

### Explanation
- Plaintext → Encryption Function (with Key) → Ciphertext
- Ciphertext → Decryption Function (with Key) → Plaintext
- Cipher itself is public knowledge, but the key must remain secret.
- Without the correct key, recovering the plaintext should be computationally infeasible.

### Notes
- Any data type (text, image, audio, video, etc.) can be plaintext.
- Ciphertext should ideally reveal no information except approximate size of plaintext.
- Encryption secures data, but security relies on key secrecy, not hiding the cipher.
- Both encryption and decryption are symmetric processes in terms of structure (opposites).


## Historical Ciphers

### Concepts Learned
- Cryptography dates back to ancient civilizations (Egypt ~1900 BCE).
- Caesar Cipher: a simple substitution cipher that shifts letters by a fixed number.
- Decryption with Caesar Cipher just shifts back by the same number.
- Caesar Cipher is insecure by modern standards (only 25 possible keys → brute force feasible).
- Other notable historical ciphers include the Vigenère Cipher, Enigma Machine, and One-Time Pad.

### Explanation
- Encryption (Caesar Cipher): Shift plaintext letters right by key.
- Decryption (Caesar Cipher): Shift ciphertext letters left by key.
**Example:**
  - Plaintext: TRYHACKME
  - Key: 3
  - Ciphertext: WUBKDFNPH
  - Brute force: Try all 25 possible keys until plaintext is revealed.

### Notes
- Caesar Cipher illustrates the basic principle of substitution.
- Modern cryptography evolved because historical ciphers were vulnerable to brute-force or frequency analysis.
- One-time pad is theoretically unbreakable if used correctly (random key, same length as message, used once).
- Historical ciphers laid the foundation for modern encryption systems.


## Types of Encryption

### Concepts Learned
- Two main categories of encryption: symmetric and asymmetric.
- Symmetric encryption: Same key used for both encryption and decryption.
- Asymmetric encryption: Uses a key pair — public key (encryption) and private key (decryption).

### Explanation
**Symmetric Encryption**
  - Also called private key cryptography.
  - Security challenge: securely sharing the secret key with all intended parties.
**Examples:**
  - DES → 56-bit key, broken by 1999 (insecure).
  - 3DES → DES applied 3 times, effective 112-bit security, deprecated in 2019.
  - AES → Modern standard since 2001; supports 128, 192, 256-bit keys.
**Asymmetric Encryption**
  - Also called public key cryptography.
  - Uses a public key for encryption and a private key for decryption.
**Examples:**
  - RSA → 2048/3072/4096-bit keys, 2048-bit minimum recommended.
  - Diffie-Hellman → secure key exchange, 2048+ bits recommended.
  - Elliptic Curve Cryptography (ECC) → shorter keys, stronger security (ECC-256 ≈ RSA-3072).
  - Based on mathematical problems that are easy one-way but infeasible to reverse.
  - Slower than symmetric but solves the key distribution issue.

### Notes
- Symmetric = fast, but key distribution is a problem.
- Asymmetric = slower, but removes the need for secret key sharing.
- Real-world systems often combine both (e.g., TLS/HTTPS uses asymmetric to exchange a key, then symmetric for the actual communication).


## Basic Math

### Concepts Learned
- XOR operation (⊕): Used in cryptography for simple encryption and decryption.
- Modulo operation (mod or %): Provides remainders and is fundamental in cryptographic algorithms.

### Explanation
**XOR Operation**
- *Logical operation on binary digits:*
  - 0 ⊕ 0 = 0
  - 0 ⊕ 1 = 1
  - 1 ⊕ 0 = 1
  - 1 ⊕ 1 = 0
- Example: 1010 ⊕ 1100 = 0110
**Key properties:**
  - A ⊕ A = 0
  - A ⊕ 0 = A
- Commutative → A ⊕ B = B ⊕ A
- Associative → (A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)
**Use in cryptography:**
  - Encryption: C = P ⊕ K (ciphertext = plaintext XOR key)
  - Decryption: P = C ⊕ K
  - Demonstrates simple symmetric encryption principle.
**Modulo Operation**
- Definition: X % Y = remainder when X is divided by Y.
**Examples:**
  - 25 % 5 = 0
  - 23 % 6 = 5
  - 23 % 7 = 2
**Properties:**
- Result is always in the range 0 to (n-1) for divisor n.
- Not reversible (x % n = r can have infinite solutions).
- Usage in cryptography: essential in modular arithmetic for RSA, Diffie-Hellman, ECC and other algorithms.

### Notes
- XOR is simple but powerful; forms the base of many symmetric encryption schemes.
- Modulo is a core building block of public-key cryptography, where large numbers and remainders are used to ensure security.


## Key Takeaway
- Cryptography transforms plaintext → ciphertext → plaintext using ciphers and keys.
- Historical ciphers (like Caesar) are easy to break and insecure today.
- Symmetric encryption uses one shared secret key (fast but hard to share securely).
- Asymmetric encryption uses a public–private key pair (secure but slower).
- Mathematics (XOR, modulo) is the backbone of modern cryptography.
- Goal: ensure confidentiality, integrity, authenticity, and security of data.
