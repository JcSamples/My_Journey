### Binary
https://mitmproxy.org/

### Installation 

````shell
pip install pyOpenSSL==21.0.0
pip install mitmproxy==8.0.0

sudo apt-get install python3-venv
python3 -m venv mitmproxy-env
source mitmproxy-env/bin/activate
pip install mitmproxy
mitmdump --version
`````

### Proxy script

````python
from time import sleep

def request(flow):
    sleep(0.2)  # 0.2 segundos por requisição = 5 requisições por segundo

`````

````
mitmdump -s [nome-do-ficheiro].py
`````

### Access to mitm:

http://mitm.it