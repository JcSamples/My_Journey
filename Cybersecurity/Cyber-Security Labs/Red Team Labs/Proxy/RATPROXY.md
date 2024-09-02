
````shell
sudo apt install build-essential libssl-dev
`````


https://github.com/streamingrat/ratproxy

````shell
go install github.com/streamingrat/ratproxy@latest
`````

### Search for GO binaries 

````shell
┌──(kali㉿kali)-[~/tools]
└─$ find / -name ratproxy 2>/dev/null
/home/kali/go/pkg/mod/cache/download/github.com/streamingrat/ratproxy
/home/kali/go/bin/ratproxy

`````

### Path

````shell
export PATH=$PATH:/home/kali/go/bin

echo 'export PATH=$PATH:/home/kali/go/bin' >> ~/.bashrc
`````

### Create the YAML file

````yaml
listen: 0.0.0.0:1414
targets:
  - name: server1
    target: http://localhost:10000
    path: /service1/
  - name: server2
    target: http://localhost:1313
    path: /

`````


### Execute [Test] ratproxy

````shell
./ratproxy -c [ratproxy.yaml] -v -w output.log -d example.com

`````

- `-v`: Modo verboso, para obter mais informações sobre o que está acontecendo.
- `-w output.log`: Define o ficheiro de saída onde os resultados serão guardados.
- `-d example.com`: Define o domínio que deseja testar.


### Generate Report

````shell
./ratproxy-report.sh output.log [nome do ficheiro] > report.html
`````

Acess: file:////user/ratreport.html 

### Examples

````
./ratproxy -v -w output.log -d 192.168.1.100 -XClfscm
`````

````shell
./ratproxy -v -w output.log -d 192.168.1.100
`````

### Include cookies:


`````shell
./ratproxy -v -w output.log -d example.com -c "SESSIONID=123456789"`
`````

![[Pasted image 20240703005613.png]]