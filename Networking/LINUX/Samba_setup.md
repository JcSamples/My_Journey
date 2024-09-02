
# User and Group Setup

```bash
# Add a new user
sudo useradd -m -s /bin/bash john_doe

# Set the password for the new user
sudo passwd john_doe
# Password: SafePass123

# Add the user to the sudo group
sudo usermod -aG sudo john_doe
```

# System Update and Samba Installation

```bash
# Update the package list
sudo apt update

# Install Samba
sudo apt install samba

# Stop and disable unnecessary Samba services
sudo systemctl stop nmbd
sudo systemctl disable nmbd
sudo systemctl stop smbd
```

# Directory and Group Configuration

```bash
# Create directories for shared folders
sudo mkdir -p /shares/purchasing
sudo mkdir -p /shares/finance

# Create groups for each department
sudo groupadd purchasing
sudo groupadd finance

# Change ownership of the directories to the respective groups
sudo chown :purchasing /shares/purchasing
sudo chown :finance /shares/finance

# Set directory permissions
sudo chmod 2770 /shares/purchasing
sudo chmod 2770 /shares/finance
```

# User Setup for Samba

```bash
# Add a new user to the purchasing group without creating a home directory
sudo adduser --home /shares/purchasing --no-create-home --shell /bin/false --ingroup purchasing jane_doe

# Create a Samba user and set the password
sudo smbpasswd -a jane_doe
# Set password during prompt

# Enable the Samba user
sudo smbpasswd -e jane_doe
```

# Samba Configuration

Edit the Samba configuration file (`/etc/samba/smb.conf`) with the following content:

```ini
[global]
server string = server01
workgroup = myworkgroup
security = user
name resolve order = wins bcast host
dns proxy = yes
wins server = 192.168.3.99
log file = /var/log/samba/smb.log
max log size = 10000
log level = 3 passdb:5 auth:5

[purchasing]
path = /shares/purchasing
browsable = yes
read only = no
create mask = 0660
force create mode = 0660
directory mask = 0770
force directory mode = 2770
valid users = @purchasing

[finance]
path = /shares/finance
browsable = yes
read only = no
create mask = 0660
force create mode = 0660
directory mask = 0770
force directory mode = 2770
valid users = @finance
```

# Testing and Finalizing Setup

```bash
# Test the Samba configuration
sudo testparm

# Restart the Samba service
sudo systemctl restart smbd

# Check the status of the Samba service
sudo systemctl status smbd
```

# Firewall Configuration

```bash
# Allow Samba through the firewall
sudo ufw allow 445/tcp
```

# Client Access

To access the shared folders from a client machine, use the following syntax:

```bash
# Accessing the Samba shares
smb://[server_ip_address]
```
