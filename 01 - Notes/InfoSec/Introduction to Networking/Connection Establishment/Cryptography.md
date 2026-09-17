
2025-05-28 17:14

Tags: #network  

## Cryptography

- Uses *mathematical algorithms* to encrypt data, making it unreadable to unauthorized individuals and protecting it from manipulation during internet transmission.

- The security of encryption depends on the *methods* and *key lengths* used

- There are two main types of encryption: **symmetric** and **asymmetric**.

#### Symmetric Encryption

- Also known as **secret key encryption**.

- Uses the **same key** for both encryption and decryption.

- Requires secure distribution, storage, and exchange of the shared key.

- If the key is compromised, data security is lost.

- Often used for encrypting large amounts of data (e.g., hard drive files, network data).

- Examples:
	- **Advanced Encryption Standard (AES)**
	- **Data Encryption Standard (DES)**

- **AES** is currently considered the most secure symmetric algorithm.

#### Asymmetric Encryption

- Also known as **public-key encryption**.

- Uses **two different keys**: a **public key** (for encryption) and a **private key** (for decryption).

- The public key can be shared openly, while the *private key must be kept secret by the recipient*.

- This method *bypasses the key exchange problem* found in symmetric encryption.
	- If someone get the key of symmetric encryption when it is exchanging, they can get the message

- Offers high security based on hard-to-solve mathematical problems.

- Enables authentication through **digital signatures**.

- *Examples:*
	- **Rivest–Shamir–Adleman (RSA)**
	- **Pretty Good Privacy (PGP)**
	- **Elliptic Curve Cryptography (ECC)**

- Applications include **E-Signatures, SSL/TLS, VPNs, SSH, PKI, and Cloud security**.


## Data Encryption Standard (DES)

- A **symmetric-key block cipher**.
	- *Block cipher* (symmetric only) means it transforms a plaintext block of a *specific size* into a ciphertext block of the *exact same size*

- Uses a **64-bit key**, but 8 bits are for checksum, so the effective key length is **56 bits**.

- Encrypts 64-bit blocks of plaintext into 64-bit blocks of ciphertext.

- **Triple DES (3DES)** is an extension that encrypts data three times (encrypt-decrypt-encrypt) for increased security but is still limited by the 56-bit key concept.

- **AES** is its successor, offering higher security.

## Advanced Encryption Standard (AES)

- Uses **128-bit, 192-bit, or 256-bit keys**.

- **Faster** than DES due to a more efficient algorithm structure that can process multiple data blocks simultaneously.

- Widely used in applications and protocols like **WLAN IEEE 802.11i, IPsec, SSH, VoIP, PGP, and OpenSSL**.

## Cipher Modes

- Define how a **block cipher algorithm** processes and combines fixed-size data blocks (usually 64 or 128 bits) to encrypt messages of any length.

| **Cipher Mode**               | **Description**                                                                                                          |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| *Electronic Code Book (ECB)*  | Not recommended due to susceptibility to attacks and poor hiding of data patterns.                                       |
| *Cipher Block Chaining (CBC)* | Default for AES; used for disk encryption and email (e.g., TrueCrypt, VeraCrypt, TLS, SSL).                              |
| *Cipher Feedback (CFB)*       | Suited for real-time data stream encryption (e.g., network communication, PKCS, BitLocker).                              |
| *Output Feedback (OFB)*       | Used for real-time data stream encryption, considered better for streams due to key stream generation (e.g., PKCS, SSH). |
| *Counter (CTR)*               | Encrypts real-time data streams; used by AES for network communication, disk encryption (e.g., IPsec, BitLocker).        |
| *Galois/Counter (GCM)*        | Used when both confidentiality and integrity are needed (e.g., wireless communications, VPNs).                           |
## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/2026)