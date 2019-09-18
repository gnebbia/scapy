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

## Building Packets

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

## Visualizing Packets


## Sending Packets


## Receiving Packets


## Loading and Saving PCAPs


