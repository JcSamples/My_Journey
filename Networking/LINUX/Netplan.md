
### Access Netplan config file
````shell
sudo nano /etc/netplan/01-netcfg.yaml

sudo nano /etc/netplan/01-network-manager-all.yaml 

`````

#### Config-File : 01-network-manager-all.yaml
````shell
network:
  version: 2
  renderer: networkd
  ethernets:
    ens37:
      dhcp4: no
      addresses:
        - 192.168.192.184/24
      gateway4: 192.168.192.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4

`````


### Apply Configurations:

````shell
sudo netplan apply
`````

#### If an error appears:

````shell
sudo systemctl enable systemd-networkd
sudo systemctl status systemd-networkd
sudo netplan apply
ip addr show ens*
`````




