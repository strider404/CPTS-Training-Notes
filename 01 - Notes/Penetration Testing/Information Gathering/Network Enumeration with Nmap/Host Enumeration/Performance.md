
2025-08-19 11:17

Tags: #nmap  

## Timeouts

- Controls how long Nmap **waits for a response** (Round-Trip-Time or RTT) 

- **Default**: `--min-RTT-timeout`= 100ms

- **Options** include `--initial-rtt-timeout` and `--max-rtt-timeout`.

- **Trade-off:** Lowering timeout values (e.g., `50ms` and `100ms`) can dramatically *reduce scan time*. However, setting them too low may cause Nmap to *miss hosts or ports that are slow to respond.*

## Max Retries

- Determines how many times Nmap will **re-transmit a packet to a port if no response is received.**

- **Default**: 10

- The relevant **option** is `--max-retries`. 

- **Trade-off:** Reducing retries (e.g., to `0`) *speeds up* the scan by not waiting for unresponsive ports. This also carries the risk of *missing open ports* if the initial packet is lost.

## Packet Rates

- Sets the **number of packets sent per second.**
  
- The option is `--min-rate`.
  
- **Use Case:** This is particularly effective in white-box tests where the scanner is *whitelisted* and *network bandwidth* is known. It can significantly speed up scans without sacrificing accuracy.


## Timing

- Nmap provides six predefined templates (`-T <0-5>`) that bundle various performance settings for convenience.
  
- The templates range from `-T0` (**paranoid**) to `-T5` (**insane**).
  
- The **default** template is `-T3` (**normal**).
  
- **Trade-off:** More aggressive templates (`-T4`, `-T5`) are *much faster* but *generate significant network traffic*, which can be detected and potentially blocked by security systems (IDS/IPS, firewalls). Slower templates are stealthier.

## References:

https://academy.hackthebox.com/module/19/section/105