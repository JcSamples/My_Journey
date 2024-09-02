### Allow DNS traffic through the firewall:

````shell
sudo ufw allow 53
`````

### Checking Logs

To monitor the logs related to DNS (specifically the `named` service), use the following command:

````shell
sudo tail -f /var/log/syslog | grep named
`````

### ## Testing DNS Configuration

To test if DNS resolution is working correctly on the localhost, use these commands:

````shell
dig google.com @localhost
`````

````
nslookup google.com
`````

### ## BIND Configuration

Edit your BIND configuration options (usually found in `/etc/bind/named.conf.options`):

````shell

options {
    directory "/var/cache/bind";

    // Forward queries to pfSense gateway
    forwarders {
        192.168.1.1;
    };

    // Enable recursion for clients
    recursion yes;

    // Allow only internal clients to use the DNS resolver
    allow-recursion { 192.168.1.0/24; };

    // Other options
    dnssec-validation auto;
    auth-nxdomain no;    # conform to RFC1035
    listen-on-v6 { any; };
};

`````


# # Bridge Host Sharing IP

## Checking Network Routes

To view the current routing table:

````shell
ip route
`````


If the expected route doesn't appear, you may need to check and modify the Netplan configuration file.

## Netplan Configuration

If there is a DNS error when pinging, consider setting `dhcp4` to `true` in your Netplan configuration file (usually found in `/etc/netplan/`).

````yaml
network: 
	version: 2 
	renderer: networkd 
	ethernets: 
	 ens33: 
		 dhcp4: true 
		 nameservers: 
		  addresses: 
		     - 8.8.8.8 
		     - 8.8.4.4
`````

After making changes, restart the DHCP client:

````shell
sudo dhclient -r ens33
sudo dhclient ens33
`````


### ## Troubleshooting DNS Resolution

If the host still cannot resolve domain names, inspect the `resolv.conf` file:

````shell
cat /etc/resolv.conf
`````

To get a detailed status of the DNS resolver, use:

````shell
resolvectl status
`````

You can also query DNS directly:

````shell
resolvectl query google.com
`````

### ### Flushing DNS Cache

If you're experiencing DNS issues, try flushing the DNS cache (if applicable):

````shell
sudo systemd-resolve --flush-caches
`````

### ### Debugging with `tcpdump`

Capture DNS traffic to analyze with `tcpdump`

````shell
sudo tcpdump -i ens33 port 53
`````

