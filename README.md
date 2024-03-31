# homelab-wireguard
## Disabling IPv6 on the client
The WG server only has IPv4 connectivity, so only IPv4 traffic will be routed. If the client has IPv6 connectivity, IPv6 traffic might be leaking out. For now the quickest fix is to just disable IPv6 on the client when connected.
Next step should be to take a look at how to fix it via DNS.

Add the following lines to the `.conf` file before `[PEER]`:
```
PostUp = sysctl -w net.ipv6.conf.all.disable_ipv6=1; sysctl -w net.ipv6.conf.default.disable_ipv6=1; sysctl -w net.ipv6.conf.lo.disable_ipv6=1
PostDown = sysctl -w net.ipv6.conf.all.disable_ipv6=0; sysctl -w net.ipv6.conf.default.disable_ipv6=0; sysctl -w net.ipv6.conf.lo.disable_ipv6=0
```
P.S: if not on Linux, cazzi tuoi
