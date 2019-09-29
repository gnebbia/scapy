
## Scapy not working normally on loopback interface

Read here:
[scapy loopback problem](https://scapy.readthedocs.io/en/latest/troubleshooting.html#i-can-t-ping-127-0-0-1-scapy-does-not-work-with-127-0-0-1-or-on-the-loopback-interface)

In order to fix it, do this:
```python
conf.L3socket
<class __main__.L3PacketSocket at 0xb7bdf5fc>
conf.L3socket=L3RawSocket
sr1(IP(dst="127.0.0.1")/ICMP())
```


