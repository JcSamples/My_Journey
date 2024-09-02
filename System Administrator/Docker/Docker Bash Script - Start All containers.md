
````shell
#!/bin/bash

# Listar todos os contêineres parados
stopped_containers=$(sudo docker ps -aq --filter "status=exited")

# Verificar se há contêineres parados
if [ -z "$stopped_containers" ]; then
  echo "Nenhum contêiner parado encontrado."
else
  # Iniciar todos os contêineres parados
  echo "Iniciando os contêineres parados..."
  sudo docker start $stopped_containers
  echo "Contêineres iniciados com sucesso."
fi

# Listar todos os contêineres em execução
echo "Contêineres em execução:"
sudo docker ps
`````