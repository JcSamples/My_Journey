
````yaml
version: '3.8'
networks:
  monitoring:
    driver: bridge
volumes:
  prometheus_data: {}
services:
  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    restart: unless-stopped
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    ports:
      - 9100:9100
    networks:
      - monitoring
  prometheus:
    image: prom/prometheus:latest
    user: "1001"
    environment:
      - PUID=1001
      - PGID=1001
    container_name: prometheus
    restart: unless-stopped
    volumes:
      - /home/client/Desktop/Prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
      - /home/client/Desktop/Prometheus/data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'
      - '--web.enable-lifecycle'
    ports:
      - "9090:9090"
    networks:
      - monitoring

`````

# With CADVISOR

![](../../../Cybersecurity/Imagens/Pasted%20image%2020240614025815.png)

##### docker-compose.yml file


````yaml
version: '3'
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    restart: unless-stopped
    volumes:
      - /etc/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'
      - '--web.enable-lifecycle'
    ports:
      - "9090:9090"

  cadvisor:
    image: gcr.io/cadvisor/cadvisor:v0.49.1
    container_name: cadvisor
    restart: unless-stopped
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:ro
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
    ports:
      - "8080:8080"

volumes:
  prometheus_data: {}


`````


### prometheus.yml              (follow the same folder structure)
````yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

`````



##### Grafana =  of host:9090

![](../../../Cybersecurity/Imagens/Pasted%20image%2020240614025724.png)


#### Configurations with CADVISOR

````yaml
  # Example job for cadvisor
  # - job_name: 'cadvisor'
  #   static_configs:
  #     - targets: ['cadvisor:8080']
`````


