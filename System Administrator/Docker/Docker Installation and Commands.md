
### Install and start Docker:

````shell
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
`````

### Manage images:

````shell
docker pull <image>       # Download an image from Docker Hub.
docker images             # List all local images.
docker rmi <image>        # Remove an image.
`````

### Manage containers:

````shell
docker run <image>                     # Run a new container from an image.
docker ps                              # List running containers.
docker ps -a                           # List all containers (including stopped ones).
docker stop <container>                # Stop a running container.
docker start <container>               # Start a stopped container.
docker restart <container>             # Restart a container.
docker rm <container>                  # Remove a container.
docker exec -it <container> /bin/bash  # Access a running container.
`````

### Manage volumes and networks:

````shell
docker volume ls                      # List volumes.
docker volume create <volume>         # Create a volume.
docker volume rm <volume>             # Remove a volume.
docker network ls                     # List networks.
docker network create <network>       # Create a network.
docker network rm <network>           # Remove a network.
`````

### Other useful commands:

````shell
docker inspect <container|image>      # Inspect a container or an image.
docker logs <container>               # View the logs of a container.
docker commit <container> <new_image> # Create a new image from a container.
docker build -t <image> <path>        # Build an image from a Dockerfile.
`````


#### Start all containers

````shell
sudo docker start $(sudo docker ps -aq)
`````

#### Start all containers with exited status

````shell
sudo docker start $(sudo docker ps -aq --filter "status=exited")
`````

#### Start all stopped containers

````shell
sudo docker start $(sudo docker ps -aq --filter "status=exited")
`````

