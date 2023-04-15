If no DHCP is enabled on the server then you have to configure the gateway by yourself in order to be seen from the Internet, or more precisely, from other networks.

## Finding the default gateway IP

There are a couple of commands to get the gateway IP:

```bash
$ ip route
default via 192.168.0.1 dev ens33 proto dhcp metric 100
192.168.0.0/24 dev ens33 proto kernel scope link src 192.160.0.103 metric 100
```
```bash
$ route -n
# or /sbin/route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         172.17.96.1     0.0.0.0         UG    0      0        0 eth0
172.17.96.0     0.0.0.0         255.255.240.0   U     0      0        0 eth0
```

The flags shown for the `route` command mean the following:
- `M`: Modified- Refers to route modified by a routing redirect.
- `H`: Host – This one here target is a host.
- `D`: Dynamic – This is a route appended by a routing redirect.
- `G`: Gateway – This one shows the route to a gateway.
- `U`: UP – This shows that the route is up and valid.
- `R`: Reject – Set by ARP when an entry is expired.