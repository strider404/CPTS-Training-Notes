
2025-09-20 14:33

Tags: #web  

## Well-Known URIs

- **Definition**: `.well-known` is a **standardized directory path (`/.well-known/`)** on web servers, as defined in RFC 8615.


- **Purpose**: It acts as a *centralized and predictable location* for a website's critical metadata. This includes configuration files, security policies, and information about services and protocols.


- **Function**: It *simplifies the discovery process* for clients like web browsers, applications, and security tools, allowing them to automatically find specific configuration data. For example, a security policy can consistently be found at `https://example.com/.well-known/security.txt`.


- **Registry**: The **Internet Assigned Numbers Authority (IANA)** maintains an official registry of `.well-known` URIs, each with a specific, standardized purpose. Examples include:

|URI Suffix|Description|Status|Reference|
|---|---|---|---|
|`security.txt`|Contains contact information for security researchers to report vulnerabilities.|Permanent|RFC 9116|
|`/.well-known/change-password`|Provides a standard URL for directing users to a password change page.|Provisional|https://w3c.github.io/webappsec-change-password-url/#the-change-password-well-known-uri|
|`openid-configuration`|Defines configuration details for OpenID Connect, an identity layer on top of the OAuth 2.0 protocol.|Permanent|http://openid.net/specs/openid-connect-discovery-1_0.html|
|`assetlinks.json`|Used for verifying ownership of digital assets (e.g., apps) associated with a domain.|Permanent|https://github.com/google/digitalassetlinks/blob/master/well-known/specification.md|
|`mta-sts.txt`|Specifies the policy for SMTP MTA Strict Transport Security (MTA-STS) to enhance email security.|Permanent|RFC 8461|

## Application in Web Reconnaissance

- **Value in Security**: In web reconnaissance and penetration testing, `.well-known` URIs are valuable for **discovering endpoints and configuration details** that can be further investigated for security vulnerabilities.


- **Key Example (`openid-configuration`)**:
	- This specific URI is part of the OpenID Connect Discovery protocol and reveals configuration metadata for identity services built on OAuth 2.0.
	  
	- Accessing this endpoint typically returns a JSON document.
	  
	- ![[Pasted image 20250922092111.png]]


- **Information Gathered from `openid-configuration`**:
	- **Endpoint Discovery**: It reveals critical URLs such as the `authorization_endpoint`, `token_endpoint`, `userinfo_endpoint`, and `jwks_uri` (which points to cryptographic keys).
	  
	- **Supported Features**: It lists supported scopes (e.g., `openid`, `profile`), response types (e.g., `code`, `token`), and signing algorithms (e.g., `RS256`).
	  
	- **Security Implications**: This information allows a security professional to map out the authentication/authorization functionality, understand its limitations, and analyze the security measures in place.
## References:

https://academy.hackthebox.com/module/144/section/3078