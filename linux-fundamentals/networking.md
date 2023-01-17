- When you connect your workstation to the workplace network, the DHCP server in the network automatically allocates a dynamic IP for you
- In servers, however, static IPs are assigned
- You can set and unset the host name of your systems using `hostname` and `hostnamectl` command
- To view the router settings and links use `ip`
- You can add hosts for resolution in `/etc/hosts` in the format `<ip>  <hostname>  <short_name>`
- DNS servers can be configured in `/etc/resolv.conf`
- Name resolution order can be configured in `/etc/nsswitch.conf` under `hosts` section
- To view the services listening on a port, use `ss -tunap`
- Check name resolution (DNS), use `dig <host_name>`
- Use `nmtui` for persistent network configuration
- Use `ping` to check a host
- Use `ip route show` to see the router config
- Use `ip a` for seeing the ip configurations


## Beej's guide to networking
- Everything in linux is a file
- There are basically 2 types of sockets:
      - Stream Socket
      - Datagram Socket

