
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

