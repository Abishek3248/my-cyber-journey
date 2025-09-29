# Cheatsheet - Cryptographic Basics

| **Concept**            | **Explanation**                                                                 | **Examples / Notes**                       |
|------------------------|---------------------------------------------------------------------------------|-------------------------------------------|
| **Plaintext**           | Original, readable data before encryption                                       | "hello", images, docs                     |
| **Ciphertext**          | Encrypted, unreadable data                                                      | WUBKDFNPH                                  |
| **Cipher**              | Algorithm to convert plaintext ↔ ciphertext                                     | Caesar, AES, RSA                          |
| **Key**                 | Secret string of bits used in cipher for encryption/decryption                  | Symmetric key / Public–Private key        |
| **Encryption**          | Process of converting plaintext → ciphertext                                    | Uses cipher + key                          |
| **Decryption**          | Process of converting ciphertext → plaintext                                    | Requires correct key                       |
| **Symmetric Encryption**| Same key for encryption & decryption (fast, needs secure sharing)              | DES, 3DES, AES                             |
| **Asymmetric Encryption**| Uses public key (encrypt) and private key (decrypt), more secure but slower    | RSA, Diffie-Hellman, ECC                  |
| **XOR (⊕)**             | Bitwise operation: 1 if bits differ, 0 if same                                  | Used in simple symmetric crypto           |
| **Modulo (a mod n)**    | Remainder after division, fundamental in cryptographic math                     | 23 mod 7 = 2                               |
