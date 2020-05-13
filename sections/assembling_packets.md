
## Exploring Protocols
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

## Generating a packet

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

