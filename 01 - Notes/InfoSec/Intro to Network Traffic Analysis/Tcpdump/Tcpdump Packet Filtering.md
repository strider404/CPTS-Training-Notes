
2025-06-26 12:12

Tags: #network #hands-on 

## Filtering

- `host [IP]`: Captures all traffic involving the *specified IP address* (both source and destination).
  
- `src/dst [host|net|port] [IP|Network Range|Port]`: Modifiers to specify traffic from a *source* or to a *destination* host, network, or port. (can use 1 and leave another)
  
- `net [network/CIDR]`: Filters for traffic originating from or destined for a *specific network range.*
  
- `[tcp/udp/icmp]`: Filters for a *specific protocol* (e.g., `tcp`, `udp`, `icmp`)
  
- `proto [protocol]`:  Use *protocol numbers* (e.g., `proto 17` for UDP).
  
- `port [port_number]`: Captures traffic on a *specific port* (both source and destination).
  
- `portrange [start-end]`: Filters for traffic within a *specified range of ports* (e.g., `portrange 0-1024`).
  
- `less` / `greater` (`<` / `>`): Filters packets based on a *size* in bytes (e.g., `less 64`).
  
- `and` / `&&`: Combines multiple filters; all conditions must be met.
  
- `or` / `||`: Combines filters; at least one condition must be met.
  
- `not` / `!`: Excludes traffic that matches the specified condition.

## Filter Application

- **Pre-Capture Filtering:** Applying filters during a live capture (`tcpdump -i eth0 [filter]`). This method discards any packets that do not match the filter, resulting in a smaller capture file. This is useful when you know exactly what you are looking for.
  
- **Post-Capture Processing:** Applying filters when reading a `.pcap` file (`tcpdump -r capture.pcap [filter]`). This method does not alter the original capture file but only displays the packets that match the filter. This preserves all original data for future analysis with different criteria.

## References:
[Hack The Box - Academy](https://academy.hackthebox.com/module/81/section/785)
