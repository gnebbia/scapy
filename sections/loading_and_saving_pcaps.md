
We can read from a pcap/pcapng file by doing:
```python
packets = rdpcap('capture_file.pcapng')
```

We can save a list of packets to a pcap by doing:
```python
wrpcap("temp.cap", pkts)
```


We can read packets from a file and apply a BPF filter by doing:
```python
packets = sniff(offline='capture_file.pcapng', filter='port 80')
```


