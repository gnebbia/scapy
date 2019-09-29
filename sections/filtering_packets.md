
We can filter packets in a simple way by using the BPF notation in the `sniff()`
function.

Anyway once we have a list of packets we can leverage python for filtering
purposes.
This section will explore techniques to perform filtering by using python and
scapy without calling the `sniff()` function.

N.B.: If you want to use the power of BPF, there are some tricks, like using a
dummy interface or saving a pcap and re-reading it with the sniff function and
the offline parameter set.

We can implement basic filters on layers by doing things like:
```python
filtered = []
for packet in pkts:
    if (packet.haslayer(ICMP)):
        print("Gotcha")
        filtered += packet
```





