##### Install Java
````shell
wget -qO- https://apt.corretto.aws/corretto.key | sudo gpg --dearmor  -o /usr/share/keyrings/corretto.gpg
echo "deb [signed-by=/usr/share/keyrings/corretto.gpg] https://apt.corretto.aws stable main" |  sudo tee -a /etc/apt/sources.list.d/corretto.sources.list

sudo apt update
sudo apt install java-common java-11-amazon-corretto-jdk
echo JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto" | sudo tee -a /etc/environment

export JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto"
`````


## Install prerequisites:
````shell
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg
`````


**Add Elasticsearch GPG key:**

````shell
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-archive-keyring.gpg
`````


**Add Elasticsearch APT repository:**

````shell
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-archive-keyring.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
`````

**Update the package index and install Elasticsearch:**

````shell
sudo apt-get update
sudo apt-get install elasticsearch
`````








`


