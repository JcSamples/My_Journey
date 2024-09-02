
# Apache2 Installation and Configuration

### 1. Install Apache2
```bash
sudo apt install apache2
```

### 2. Enable Firewall
```bash
sudo ufw app list
```

### 3. Create SSL Certificate
```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/server.fictionaldomain.key -out /etc/ssl/certs/server.fictionaldomain.crt
```

### 4. Create Directory and HTML File
```bash
# Create a directory inside /var/www/
sudo mkdir /var/www/fictionaldomain

# Create an HTML file inside this directory
sudo touch /var/www/fictionaldomain/index.html
```

### 5. Change Ownership and Permissions (if necessary)
```bash
sudo chown : /var/www/
sudo chmod 755 /var/www/
```

### 6. Edit the HTML File
```bash
# Use your preferred text editor to edit the HTML file
sudo nano /var/www/fictionaldomain/index.html
```

### 7. Create Apache Configuration Files
Navigate to the directory `/etc/apache2/sites-available/` and create the following configuration files:

1. `fictionaldomain.conf`
2. `fictionaldomain-ssl.conf`

```bash
sudo nano /etc/apache2/sites-available/fictionaldomain.conf
```

#### Sample VirtualHost Configuration (HTTP)
```apache
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName fictionaldomain
    ServerAlias www.fictionaldomain
    DocumentRoot /var/www/fictionaldomain
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

### 8. Enable Site and Test Configuration
```bash
sudo a2ensite fictionaldomain.conf
sudo apache2ctl configtest
```

### 9. Enable SSL Module
```bash
sudo a2enmod ssl
```

### 10. Edit SSL and 000-default Configuration Files
Navigate to `/etc/apache2/sites-available/` and edit the SSL and default configurations as necessary.

### 11. Bind Configuration
Navigate to `/var/bind/` or `/etc/bind/` and introduce CNAME and PTR records.

### 12. Access Keys (envvars)
If necessary, change the user:group name in the envvars file.

### 13. Create Password for Webserver Access
```bash
sudo htpasswd -c /etc/apache2/.htpasswd [username]
```

### 14. Add Authentication to Both Configuration Files
Add the following block to both `fictionaldomain.conf` and `apache2.conf`:

```apache
<Directory "/var/www/fictionaldomain">
    AuthType Basic
    AuthName "Restricted Access"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
```

# Postfix Installation and Basic Testing

### 1. After Installing Postfix

```bash
ehlo
mail from: randomemail@example.com
rcpt to: Doomsday@fakeservername
data
Your message goes here.
.
quit
```
