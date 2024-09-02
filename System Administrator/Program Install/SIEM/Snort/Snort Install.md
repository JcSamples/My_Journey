
````shell
mkdir snort
`````

````shell
sudo apt-get update
sudo apt-get install build-essential
sudo dpkg --configure -a


sudo apt-get install build-essential autoconf automake libtool
sudo apt install make
sudo apt install cmake
`````

### **Install gperftools**

wget https://github.com/gperftools/gperftools/releases/download/gperftools-2.9.1.1/gperftools-2.9.1.1.tar.gz


# Set interface to Promisc

![](../../../../Cybersecurity/Imagens/Pasted%20image%2020240616140852.png)
````shell
sudo ip link set ens33 promisc on
`````

![](../../../../Cybersecurity/Imagens/Pasted%20image%2020240616140831.png)


### Run: 

````shell
snort -V
client@client-virtual-machine:/etc/snort$ sudo snort
`````

````shell
client@client-virtual-machine:/etc/snort/rules$ sudo snort -q -l /var/log/snort -i ens33 -A console -c /etc/snort/snort.conf
`````
 
