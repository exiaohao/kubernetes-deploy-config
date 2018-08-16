# SPOCK Proxy

### Firewall
```bash
iptables -N SPOCK-API-PROXY
iptables -A SPOCK-API-PROXY -s 180.168.57.238/32 -j ACCEPT
iptables -I INPUT -p tcp -m tcp --dport 10101 -j SPOCK-API-PROXY
```
