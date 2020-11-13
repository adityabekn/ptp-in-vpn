# ptp-in-vpn

sudo iptables -I FORWARD -i tun0 -o eth0 \
    -s 10.8.0.0/24 -d 192.168.0.0/24 \
    -m conntrack --ctstate NEW -j ACCEPT

sudo iptables -I FORWARD -i tun0 -o eth0 \
    -s 10.8.0.0/24 -m conntrack --ctstate NEW -j ACCEPT

sudo iptables -I FORWARD -i eth0 -o eth0 \
    -s 192.168.0.0/24 -m conntrack --ctstate NEW -j ACCEPT

sudo iptables -I FORWARD -m conntrack --ctstate RELATED,ESTABLISHED \
    -j ACCEPT

sudo iptables -t nat -I POSTROUTING -o eth0 \
     -s 10.8.0.0/24 -j MASQUERADE

sudo iptables -t nat -I POSTROUTING -o eth0 \
     -s 192.168.0.0/24 -j MASQUERADE
