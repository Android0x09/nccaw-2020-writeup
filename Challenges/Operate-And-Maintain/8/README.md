# FTP Attack (45 points)

File(s): [packets.pcap](packets.pcap)

## Description:

This looks like a brute-force attack on an FTP server. Can you find the password for the successful login?

### Answer:

temppw

### Solution:

CTRL-F for "login successful"

Then move up from that packet (packet #1714) until you find the packet containing the last attempted password in packet #1707.

| [Previous Challenge](/Challenges/Operate-And-Maintain/7) | [Return to Challenges](/Challenges/../../../#modules) | [Next Challenge](/Challenges/Oversee-And-Govern/1) |
| :------- | :-----: | ------: |