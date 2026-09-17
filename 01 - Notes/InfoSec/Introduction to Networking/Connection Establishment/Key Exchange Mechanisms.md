
2025-05-25 10:38

Tags: #network  

## Key Exchange Mechanisms

- To securely exchange cryptographic keys between two parties.

- Essential for cryptographic protocols as communication security relies on key secrecy.

- Methods involve agreeing on a shared secret key over an insecure channel, often using mathematical operations.

## Diffie-Hellman

- Allows two parties to agree on a shared secret key without prior communication.

- Based on generating a *shared secret key* for encrypting/decrypting messages.

- Vulnerable to **MITM attack**

- Require a lot of CPU power


## RSA

- Uses properties of *large prime numbers* to generate a shared secret key.

- Relies on the difficulty of factoring the product of large prime numbers.

- **Applications:**
	- Encrypting and signing messages.
	- Protecting data in transit (e.g., **SSL/TLS**).
	- Generating and verifying digital signatures.
	- Authenticating users and devices (e.g., **PKINIT** in Kerberos).
	- Protecting sensitive information.


## ECDH

- A *variant of Diffie-Hellman* using elliptic curve cryptography.

- **Advantages:** More efficient and secure than traditional Diffie-Hellman.

- **Applications:**
	- Establishing secure communication channels (e.g., **TLS**).
	- Providing **forward secrecy**.
		- past communications cannot be revealed even if the private keys are compromised
	- Authenticating users and devices (e.g., **Internet Key Exchange (IKE)** in VPNs).


## ECDSA

- Uses elliptic curve cryptography to generate digital signatures.

- Authenticates parties involved in key exchange.


| **Algorithm**                                | **Acronym** | **Security**                                                               |
| -------------------------------------------- | ----------- | -------------------------------------------------------------------------- |
| `Diffie-Hellman`                             | `DH`        | Relatively secure and computationally efficient                            |
| `Rivest–Shamir–Adleman`                      | `RSA`       | Widely used and considered secure, but computationally intensive           |
| `Elliptic Curve Diffie-Hellman`              | `ECDH`      | Provides enhanced security compared to traditional Diffie-Hellman          |
| `Elliptic Curve Digital Signature Algorithm` | `ECDSA`     | Provides enhanced security and efficiency for digital signature generation |

## Internet Key Exchange

- **Internet Key Exchange (IKE):** Protocol to *establish and maintain* secure communication sessions (e.g., VPNs).

- Uses a combination of **Diffie-Hellman** and other cryptographic techniques.

- Key component of many VPN solutions for secure key exchange.

- Often used with **RSA** (key exchange, digital signatures) and **AES** (data encryption).

- Operating **Modes**:
	- **Main Mode:**
		- Default and generally more secure.
		- *Three-phase* key exchange.
		- Greater flexibility and security, but potentially slower.
	- **Aggressive Mode:**
        - Faster performance (fewer round trips).
        - *Two-phase* key exchange (all parameters in the first phase).
        - May reduce security; does not provide identity protection.

- **Pre-Shared Keys (PSK)**: A *secret value* shared between two parties for authentication and establishing a shared secret.
	- Must be securely exchanged beforehand
	- **Advantage:** Adds an extra layer of authentication.
	- **Limitations:** Secure exchange can be difficult; if compromised (e.g., MITM), IKE session security may be compromised.

## References:

[Introduction to Networking](https://academy.hackthebox.com/module/34/section/1875)