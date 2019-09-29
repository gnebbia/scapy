
We can show info about a packet by doing:
```python
packet.show()
# or for a shorter summary
packet.summary()
```

We can also inspect informations about only a specific protocol/layer by doing:
```python
packet[TCP].show()
```

Of course we can also query single fields from a specific protocol by selecting
the field with the dot '.' notation, like this:
```python
time_to_live = packet[IP].ttl
myprotocol = packet[IP].proto
```

If we have a list of packets, we can of course select also a single packet from
that list and select a specific protocol on that packet:
```python
packets[2][UDP].show()
```

Given a set of packets we can also visualize them on wireshark by doing:
```python
pkts = sniff(filter="tcp or arp", count=20)
wireshark(pkts)
```


