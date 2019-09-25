# Scapy

## Intro

Let's see some basic commands once we have our scapy shell open: 
```sh
 # list available protocols and layers
ls()

# list commands
lsc()

# show configuration
conf
```

We can get help for a specific command by doing:
```sh
help(<command_name>)

# for example
help(sniff)
```


## Showing packet information

We can show the current setting of the packet we are crafting by doing:
```python
pkt1.show()
# or alternatively to show what we have changed from the defaults we can do:
ls(pkt1)
```
We can also show the hexdump or the raw bytes of a specific packet by doing:
```python
# this prints the hexdump
hexdump(pkt1) 

# this prints the raw bytes
raw(pkt1)
```

## Assembling Packets

### Exploring Protocols
Listing protocols or protocols object which have in their string "DNS"
```python
protocol_name = "DNS"
ls(protocol_name)
```

In order to explore existing protocols we can also do:
```python
ls()
```
or if we prefer a fancier version with an ncurses GUI we can launch:
```python
explore()
```

Given a specific protocol, such as TCP, we can list the available attributes we
can set by doing:
```python
ls(TCP)
# Notice that TCP is not in double quotes, since it refers to an object
```

### Generating a packet

We can initialize a new TCP packet by doing:
```python
pkt1 = TCP()
# this packet will have reasonable defaults
```
now we can change the fields we are interested in by doing:
```python
pkt1.<field_name> = <value_name>
# where the list of field names can be retrieved by ls(<protocol_name>)
# as we have shown
```

If we want to unset a specific field, so that it goes back to its reasonable
default value, we can do:
```python
del(pkt1.<field_name>)
```

Let's build more complex packets:
```python
ip = IP(src="192.168.0.1", dst="192.168.0.2")
tcp = TCP(sport=1025, dport=80)
pkt2 = ip/tcp
```

The notation used is to build packets is from the lower layer to the upper
layers, so let's see some examples of reasonable packets:
- `IP()/TCP()`
- `Ether()/IP()/TCP()`
- `IP()/TCP()/"GET / HTTP/1.0\r\n\r\n"`
- `Ether()/Dot1Q()/IP()/TCP()`
- `Ether()/IP(dst="www.slashdot.org")/TCP()/"GET /index.html HTTP/1.0 \n\n"`


## Generating sets of packets


## Create a packet from template

If we sniffed some packets or read packets from a pcapng file, we can do:

```python
pkts[0].command()
```
In order to get the scapy/python command to build the packet 0.


## Visualizing Packets

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


## Sniffing Packets

Let's see an example of packet sniffing:
```python
pkts = sniff(filter="tcp or arp", iface="eth0", count=20)
# we specify a filter in this case catching only tcp or arp traffic
# filters are specified with the BPF notation
# we catch on the network interface eth0
# we sniff 20 packets
```


## Filtering Packets

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





## Sending Packets


send(p)
sr(p)

sr1(p)


## Loading and Saving the Working Environment

```python
save_session("session.scapy")
# to save a scapy session
```

We can load a saved scapy session by doing:
```python
load_session("session.scapy")
# to load an existing scapy session
```

we can check out the defined variables with 
```python
dir()
# shows all the defined variables
```


## Loading and Saving PCAPs

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


## Appendix A: Scapy not working normally on loopback interface

https://scapy.readthedocs.io/en/latest/troubleshooting.html#i-can-t-ping-127-0-0-1-scapy-does-not-work-with-127-0-0-1-or-on-the-loopback-interface

```python
conf.L3socket
<class __main__.L3PacketSocket at 0xb7bdf5fc>
conf.L3socket=L3RawSocket
sr1(IP(dst="127.0.0.1")/ICMP())
```

## Appendix B: Built-in Complex functions

In this section we will see, built-in functions which perform more complex tasks
automatically.

### ARP who-has to find alive hosts on the network

```python
arping("192.168.46.0/24")
```


