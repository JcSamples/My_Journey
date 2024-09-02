Case: All my VMs have IP addresses, but they can't communicate to the internet. I troubleshooted DNS, firewall, DHCP, network interface, and still couldn't resolve the issue. That's when I found online that it was a problem with the VMware version.

````
sudo nano /etc/NetworkManager/NetworkManager.conf
`````

````shell
dig google.com
nslookup google.com


sudo nmcli dev show | grep 'IP4.DNS'
`````


````shell
sudo iptables -L -v -n
sudo iptables -L -v -n -t nat
`````


````shell
cat /etc/resolv.conf
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf
ip link show eth0
ping -c 4 192.168.1.1
sudo iptables -L
ping -c 4 8.8.8.8
sudo systemctl restart NetworkManager
sudo dhclient -r eth0
sudo dhclient eth0
journalctl -u NetworkManager
sudo systemctl restart networking.service
```````


````shell
sudo ifconfig eth0 up
sudo ip link set eth0 up


sudo ifconfig eth0 down
sudo ip link set eth0 down
`````


### Last case:**

Go to task manager and end the process.

````Windows
VMNAT.EXE 
`````

Or update your VMware to the latest version.