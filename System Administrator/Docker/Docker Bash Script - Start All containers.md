
````shell
#!/bin/bash

# List all stopped containers
stopped_containers=$(sudo docker ps -aq --filter "status=exited")

# Check if there are any stopped containers
if [ -z "$stopped_containers" ]; then
  echo "No stopped containers found."
else
  # Start all stopped containers
  echo "Starting stopped containers..."
  sudo docker start $stopped_containers
  echo "Containers started successfully."
fi

# List all running containers
echo "Running containers:"
sudo docker ps
`````
