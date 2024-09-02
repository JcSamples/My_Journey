
### Debian/Ubuntu:

````
sudo apt-get install libapache2-mod-ssl
`````

````
sudo a2enmod ssl
`````

````
sudo nano /etc/apache2/sites-available/seusite-ssl.conf
`````

````c
<VirtualHost *:443>
    ServerAdmin your@email.com
    ServerName your-domain.com
    DocumentRoot /var/www/yoursite

    SSLEngine on
    SSLCertificateFile /path/to/your_certificate.crt
    SSLCertificateKeyFile /path/to/your_private_key.key
    SSLCertificateChainFile /path/to/ca_file.crt (optional)

    # Other VirtualHost configurations
</VirtualHost>


`````

Replace `/path/to/your_certificate.crt`, `/path/to/your_private_key.key`, and optionally `/path/to/your_ca_file.crt` with the correct paths to your certificate and key files.


````
sudo a2ensite seusite-ssl.conf
`````

````
sudo service apache2 restart
`````

