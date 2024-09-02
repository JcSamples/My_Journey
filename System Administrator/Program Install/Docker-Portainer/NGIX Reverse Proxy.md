

# 1-Install Docker Compose

````bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
`````

## 2. Set up Nginx Proxy Manager

In Stacks, Select Add new Stack

![](../../../Cybersecurity/Imagens/Pasted%20image%2020240611231710.png)

### Paste The docker compose file

````yaml
version: '3'
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    ports:
      - '80:80'
      - '81:81'
      - '8443:8443'
    environment:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "npm"
      DB_MYSQL_PASSWORD: "npm"
      DB_MYSQL_NAME: "npm"
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
  db:
    image: 'jc21/mariadb-aria:latest'
    environment:
      MYSQL_ROOT_PASSWORD: 'npm'
      MYSQL_DATABASE: 'npm'
      MYSQL_USER: 'npm'
      MYSQL_PASSWORD: 'npm'
    volumes:
      - ./mysql:/var/lib/mysql
`````


## 3. Login to the web UI of NGINX proxy manager

[](https://github.com/ChristianLempa/videos/tree/main/nginxproxymanager-tutorial#3-login-to-the-web-ui-of-nginx-proxy-manager)

Now we can log in to the web UI. Simply use your browser to connect to your server by using the IP address or an FQDN and connect on port `81`. Log in with the username `admin@example.com` and the password `changeme`. Next, you should change your username and password, and that’s it!

and then change the user and password

![](../../../Cybersecurity/Imagens/Pasted%20image%2020240612003831.png)

