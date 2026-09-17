
2025-03-06 22:30

Tags: #linux  

## Remote Desktop Protocols in Linux

- Remote desktop protocols: provide ==graphical remote== to the system -> manage, configure, maintenance system remotely

- 2 common protocols:
	- ==Remote Desktop Protocol== (RDP): often used in Windows
	- Virtual Network Computing (VNC): tool in Linux, cross-platform (can connect to Windows, macOS, etc) 

- VNC is cross-platform but RDP is more optimized for Windows

## XServer

- X11 (X Window System network protocol): provides graphical user interface (GUI), acts as an ==intermediary== between applications and the display hardware, managing windows, input devices (keyboard, mouse), and screen rendering
  
- XServer is part of X11

- Support ==network transparency==: apps can run on 1 machine and display on the other

- Use TCP port 6001-6009

- Is ==uncrypted== -> there might be security risk (using tools like xwd and xgrabsc) -> need to use SSH tunneling or VNC or RDP

- X11Forwarding: change to yes: `cat /etc/ssh/sshd_config | grep X11Forwarding`

- XDMCP (X Display Manager Control Protocol): used by the X Display Manager to remote control X Window System through UDP port 177
	- Is not secured and outdated, vulnerable to man-in-the-middle attack


## VNC

- VNC (Virtual Network Computing): ==remote desktop sharing system== using RTB protocol, help us control other computer remotely, mainly used in Linux host

- Has encryption, adn required authentication

- Two primary modes: 1 share host's actual screen and 1 offer virtual session

- Mainly use TCP port 5900 for displaying 0

- Common tools:
	- TigerVNC
	- TightVNC
	- RealVNC
	- UltraVNC

- Might need to install XFCE4 desktop manager since this is light-weight GUI environment, perfect when the VNC need to provide the GUI, GNOME is heavier
- TigerVNC installation in the link

## References:

[Linux Fundamentals](https://academy.hackthebox.com/module/18/section/1776)