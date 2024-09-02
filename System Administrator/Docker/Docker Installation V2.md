
### INSTALL DOCKER

````C#
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
`````

````C#
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y docker-ce
`````

If the following error occurs: `E: Package 'docker-ce' has no installation candidate E: Package 'docker-ce-cli' has no installation candidate E: Unable to locate package containerd.io`

````shell
sudo rm /etc/apt/sources.list.d/docker.list

buster version:
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian buster stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

bullseye version:

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian bullseye stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl start docker && sudo systemctl enable docker

`````

### TEST:

````shell
sudo docker run hello-world
````

### INSTALL DOCKER COMPOSE


```shell
sudo apt-get update 
sudo apt-get install docker-compose-plugin
docker-compose version
`````

### INSTALL DOCKER-COMPOSE WITH BINARY

````shell
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
`````

WITH THIS VERSION THE COMMAND IS `docker compose`, NOT `docker-compose`.