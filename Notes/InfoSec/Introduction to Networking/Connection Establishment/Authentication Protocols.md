
2025-05-27 21:51

Tags: #network  

## Authentication Protocols

- **Authentication protocols**: to **verify the identity** of users, devices, and other entities.

- These protocols also facilitate the **secure exchange of information**

- **Common Protocols**:

| **Protocol** | **Description**                                                                                                                                                                                                                                                                                                    |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Kerberos`   | Uses tickets in domain environments via a Key Distribution Center (KDC).                                                                                                                                                                                                                                           |
| `SRP`        | A password-based protocol using cryptography against eavesdropping and man-in-the-middle (MitM) attacks.                                                                                                                                                                                                           |
| `SSL`        | A cryptographic protocol for secure network communication.                                                                                                                                                                                                                                                         |
| `TLS`        | The successor to SSL, providing communication security over the internet.                                                                                                                                                                                                                                          |
| `OAuth`      | An open standard for authorization, allowing third-party access to web resources without sharing passwords.                                                                                                                                                                                                        |
| `OpenID`     | A decentralized protocol enabling users to use a single identity across multiple websites.                                                                                                                                                                                                                         |
| `SAML`       | Security Assertion Markup Language is an XML-based standard for exchanging authentication and authorization data.                                                                                                                                                                                                  |
| `2FA`        | Uses two different factors to verify identity.                                                                                                                                                                                                                                                                     |
| `FIDO`       | Develops open standards for strong authentication.                                                                                                                                                                                                                                                                 |
| `PKI`        | A system for secure information exchange using public and private keys for encryption and digital signatures.                                                                                                                                                                                                      |
| `SSO`        | Allows users to access multiple applications with a single set of credentials.                                                                                                                                                                                                                                     |
| `MFA`        | Uses multiple factors (knowledge, possession, inherence) for verification.                                                                                                                                                                                                                                         |
| `PAP`        | Sends passwords in clear text (insecure).                                                                                                                                                                                                                                                                          |
| `CHAP`       | Uses a three-way handshake for identity verification.                                                                                                                                                                                                                                                              |
| `EAP`        | A framework supporting multiple authentication methods.                                                                                                                                                                                                                                                            |
| `SSH`        | This is a network protocol for secure communication between a client and a server. We can use it for remote command-line access and remote command execution, as well as for secure file transfer. SSH uses encryption to protect against eavesdropping and other attacks and can also be used for authentication. |
| `HTTPS`      | A secure version of HTTP using SSL/TLS for encrypted communication and authentication.                                                                                                                                                                                                                             |
| `LEAP`       | A Cisco wireless authentication protocol using EAP and RC4; vulnerable and largely replaced.                                                                                                                                                                                                                       |
| `PEAP`       | A secure tunneling protocol (wireless/wired) based on EAP, using TLS and server-side certificates; more secure than LEAP.                                                                                                                                                                                          |

- **Comparison (LEAP vs. PEAP)**:
	- **PEAP is generally more secure** than LEAP. PEAP uses a server-side public key certificate and encrypts MSCHAPv2 hashes.
	- LEAP relies on a shared secret and does not encrypt MSCHAPv2 hashes; it also uses the weaker RC4 algorithm.
	- Both LEAP and PEAP have vulnerabilities and are being replaced by more secure protocols like EAP-TLS.

- **Physical Connections**: Protocols like **SSH or HTTPS (using SSL/TLS)** are default choices. They use robust encryption, support digital certificates, and PKI to prevent MitM attacks, and are widely supported.

## References:
[Introduction to Networking](https://academy.hackthebox.com/module/34/section/1876)
