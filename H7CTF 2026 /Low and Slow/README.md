# Low and Slow 
>this one is pretty straightforward

### Wireshark

I opened ```capture.pcap``` in Wireshark to inspect the captured traffic.

The capture contained HTTP requests, DNS queries, and TCP connections. Rather than focusing only on HTTP traffic, I decided to inspect the DNS queries for unusual hostnames.

In Wireshark, I used the display filter:
```
dns
```
To show only DNS queries rather than responses, I used:
```
dns.flags.response == 0
```
Most queried domains appeared routine. However, three unique hostnames stood out because they shared an unusual suffix:
```
sync.cdn-telemetry-lab.net
```
The relevant query labels were:
```
00ja3ugvcgpm3doobx
01mi4dmy3dg43tozru
02gi3geoldgb6q
```
Yup, these are definitely base 32 strings.If you notice this anomaly repeats itself in the following dns traffic.

### Flag with Cyberchef

I used CyberChef to decode the strings with the From Base32 operation after removing the prefixes 00,01,02.

Flag found:
```
H7CTF{6787b86cc777f426b9c0}
```
