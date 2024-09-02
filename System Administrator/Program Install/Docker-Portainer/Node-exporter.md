
````yml
version: '3.8'

services:
  node_exporter:
    image: quay.io/prometheus/node-exporter:v1.8.1
    container_name: node_exporter
    command: "--path.rootfs=/host"
    pid: host
    restart: unless-stopped
    volumes:
      - /:/host:ro,rslave
    networks:
      - monitoring
    labels:
      - "com.example.service=monitoring"
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"

networks:
  monitoring:
    driver: bridge

`````
