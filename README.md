## WireGuard Split Tunnel

I had to do a lot of googling before I found the correct answer. Without a good understanding of WireGuard this can really be annoying to deal with. So I have decided to share my knowledge to hopefully spare someone the headache.

Here is an example of a config file:
```
[Interface]
PrivateKey = <your PrivateKey>
Address = 10.8.2.3/24, <add optional ipv6 adress here if your vpn server suports it>
DNS = 1.1.1.1

[Peer]
PublicKey = <your PublicKey>
PresharedKey = <your PresharedKey>
AllowedIPs = 10.0.0.1/24, 192.168.0.1/24 ::/0
Endpoint = <your server ip or dns>
```

The magic happens in `AllowedIPs`, in this example we are tunneling to a local remote subnet. It's important to specify the full CIDR. The `::/0` is for routing IPv6, in this example it is routing all IPv& traffic through the VPN.

If you want to only route traffic to specific IP adresses;
```
AllowedIPs = 10.0.0.1/32 10.0.0.14/32 10.64.74.2/32 #And so on
```

It is worth noting that if you are connecting from the same internal subnet as the one you want to tunnel to, for example `192.168.1.1/24` you will lose access to your own private network, and all traffic to these adresses wil be tunneled to the remote network.
