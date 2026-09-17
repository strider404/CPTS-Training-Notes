
2025-07-03 15:31

Tags: #network #hands-on 

## Decrypting RDP connections

- To decrypt it, we must have the *Key file*

- Filter for **port 3389**, don't filter for `rdp` because it is encrypted

- RDP use **TPKT protocol,** so when TPKT appears, it means there is a RDP conversation

- To apply the key in Wireshark:
	- go to Edit → Preferences → Protocols → TLS
	- On the TLS page, select Edit by RSA keys list → a new window will open.


## References:

[Hack The Box - Academy](https://academy.hackthebox.com/module/81/section/964)