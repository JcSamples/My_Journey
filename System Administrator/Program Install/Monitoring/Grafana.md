````yaml
version: '3.7'

volumes:
  grafana-data:
    driver: local

services:
  grafana:
    image: docker.io/grafana/grafana-oss:11.0.0
    container_name: grafana
    ports:
      - "3000:3000"
    volumes:
      - grafana-data:/var/lib/grafana
    restart: unless-stopped

`````

####Save the file as: docker-compose-yml


### Acess Grafana


````
<ip>:3000
`````

![](Pasted%20image%2020240614013105.png)

Default Credentials : admin:admin



