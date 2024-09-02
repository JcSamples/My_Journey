

````shell
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install -y docker-ce
````
```
```

**Verificar a instalação do Docker:**
````shell
sudo systemctl status docker
````


**Instalar o Portainer:**
````shell
sudo docker volume create portainer_data
sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

`````

![](Imagens/Pasted%20image%2020240611225257.png)

## Optional
Update Portainer:**

````shell
sudo docker stop portainer
sudo docker rm portainer
sudo docker pull portainer/portainer-ce
sudo docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

`````


