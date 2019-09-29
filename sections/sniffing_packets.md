
Let's see an example of packet sniffing:
```python
pkts = sniff(filter="tcp or arp", iface="eth0", count=20)
# we specify a filter in this case catching only tcp or arp traffic
# filters are specified with the BPF notation
# we catch on the network interface eth0
# we sniff 20 packets
```


