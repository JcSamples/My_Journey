```bash
#!/bin/bash

# Initial configuration
IP_STATIC="192.x.x.x"
NETMASK="24"
GATEWAY="192.x.x.x"
DNS1="8.8.8.8"
DNS2="8.8.4.4"
DOMAIN="zod.domain.local"
HOSTNAME="dczod"
REALM="dc.zond.local"
PASSWORD="strongpassword"
TIMEZONE="Mars/Jupiter"
RESOLV_CONF="/etc/resolv.conf"

# Update the system
sudo apt update -y && sudo apt upgrade -y

# Install SSH if not installed
sudo apt install -y openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh

# Install necessary packages
echo "Installing necessary packages..."
sudo apt install -y samba krb5-config krb5-user winbind

# Verify if the packages were installed correctly
if dpkg -l | grep -qw samba && dpkg -l | grep -qw krb5-user && dpkg -l | grep -qw winbind; then
    echo "All packages installed successfully."
else
    echo "Package installation failed. Exiting script."
    exit 1
fi

# Configure timezone
echo "Configuring timezone..."
sudo timedatectl set-timezone $TIMEZONE

# Set the hostname
echo "Setting hostname..."
sudo hostnamectl set-hostname $HOSTNAME

# Update the /etc/hosts file
echo "Updating /etc/hosts..."
sudo bash -c "echo '$IP_STATIC $DOMAIN $HOSTNAME' >> /etc/hosts"

# Backup the smb.conf file
echo "Backing up original smb.conf..."
sudo mv /etc/samba/smb.conf /etc/samba/smb.conf.bak

# Provision the Samba domain
echo "Provisioning Samba domain..."
sudo samba-tool domain provision --realm=$REALM --domain=${HOSTNAME^^} --server-role=dc --dns-backend=SAMBA_INTERNAL --adminpass=$PASSWORD

# Copy Kerberos configuration
echo "Copying Kerberos configuration..."
sudo cp /var/lib/samba/private/krb5.conf /etc/krb5.conf

# Disable unnecessary services and enable Samba AD DC
echo "Disabling unnecessary services and enabling Samba AD DC..."
sudo systemctl disable --now smbd nmbd winbind systemd-resolved
sudo systemctl unmask samba-ad-dc
sudo systemctl enable samba-ad-dc
sudo systemctl start samba-ad-dc

# Check domain level
echo "Checking domain level..."
sudo samba-tool domain level show

# Configure resolv.conf
echo "Configuring resolv.conf..."
sudo rm -f $RESOLV_CONF
sudo bash -c "cat > $RESOLV_CONF <<EOL
nameserver 127.0.0.1
domain cet15.local
EOL"

# Create users
echo "Creating users..."
sudo samba-tool user create john_doe1 $PASSWORD
sudo samba-tool user create john_doe2 $PASSWORD

# Test DNS configuration
echo "Testing DNS configuration..."
host -t SRV _kerberos._udp.$REALM
host -t SRV _ldap._tcp.$REALM
host -t A example.com

# Configure static IP with Netplan (this step is done last)
echo "Configuring static IP..."
sudo bash -c "cat > /etc/netplan/00-installer-config.yaml <<EOL
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - $IP_STATIC/$NETMASK
      routes:
        - to: 0.0.0.0/0
          via: $GATEWAY
      nameservers:
        addresses:
          - $DNS1
          - $DNS2
EOL"
sudo netplan apply

echo "Active Directory emulation setup completed!"
```

```bash
chmod +x setup_ad_emulation.sh
```

# If an error occurs

If you encounter any issues, you may need to manually remove the Samba configuration file and re-provision the domain:

```bash
sudo rm -f /etc/samba/smb.conf

sudo samba-tool domain provision --realm=sameaskerberos --domain=cantbethesameasrealm --server-role=dc --dns-backend=SAMBA_INTERNAL --adminpass=StrongPassword
```

**Copy the Kerberos Configuration:**

As the message suggests, copy the Kerberos configuration file generated during provisioning:

```bash
sudo cp /var/lib/samba/private/krb5.conf /etc/krb5.conf
```

**Restart the Samba Service:**

Once the provisioning is successfully completed, restart the samba-ad-dc service:

```bash
sudo systemctl status samba-ad-dc
```

```bash
sudo systemctl start samba-ad-dc
```

