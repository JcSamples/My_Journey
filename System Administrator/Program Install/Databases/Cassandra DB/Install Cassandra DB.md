
### Install Cassandra:

### Add the Cassandra repository::

````shell
echo "deb http://www.apache.org/dist/cassandra/debian <version> main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list

`````

### Import the repository key:

````shell
curl https://www.apache.org/dist/cassandra/KEYS | sudo apt-key add -
`````

#### Update and Install

````shell
sudo apt-get update
`````

````shell
sudo apt-get install cassandra
`````

### Start Cassandra

````shell
sudo service cassandra start
`````
