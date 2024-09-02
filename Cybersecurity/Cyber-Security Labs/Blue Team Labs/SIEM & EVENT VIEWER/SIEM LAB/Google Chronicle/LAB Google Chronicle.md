
## Query index = main and index = *
Após termos efetuado o Upload da pasta zipada efetuamos a nossa primeira querry

index = main

![[Pasted image 20240518213938.png]]
![[Pasted image_20240518213938.png]](./Imagens/Pasted%20image%2020240518213938.png)    

Selecionamos o "ALL TIME" para que o Chronicle conseguisse obter informação relacionada com a nossa pasta zipada

Verificamos que com a querry index = main obtemos várias informações
![[Pasted image 20240518214150.png]]

## Filtering buy Host: Mailsv
Vamos filtrar as informações usando a query : index=main host=mailsv

![[Pasted image 20240518214628.png]]

Verificamos que temos 9,829 eventos dos 109 mil anteriores.

## Mailsv Root Login Attempts


Vamos pesquisar apartir de log fails do servidor mailsv user root usando a query: index=main host=mailsv fail* root

![[Pasted image 20240518215206.png]]


Verificamos que existem 346 tentativas de login.
![[Pasted image 20240518215943.png]]

# LAB 2

### Scenary

Review the following scenario. Then complete the step-by-step instructions.

You are a security analyst at a financial services company. You receive an alert that an employee received a phishing email in their inbox. You review the alert and identify a suspicious domain name contained in the email's body: signin.office365x24.com. You need to determine whether any other employees have received phishing emails containing this domain and whether they have visited the domain. You will use Chronicle to investigate this domain.



After identifying the suspicious domain: signin.office365x24.com, we conducted a search on the Google Chronicle 'demo' site.

![[Pasted image 20240518221011.png]]

![[Pasted image 20240518221302.png]]

````
target.hostname = "signin.office365x24.com" OR network.dns.questions.name = "signin.office365x24.com"
`````

### Whois

Out of curiosity, I also searched on the Whois site and found that the domain is registered under the name Alberto, and the server is active with the IP: 104.21.77.241.

![[Pasted image 20240518221438.png]]



![[Pasted image 20240518222341.png]]

We have by the possibility of using AI in the search engine, which made the query much easier.


![[Pasted image 20240518222905.png]]


![[Pasted image 20240518223445.png]]

````
metadata.event_type = "NETWORK_HTTP" AND target.url = /signin.office365x24.com/ AND network.http.method = "POST"
`````


I had to modify the AI query, which I didn't expect, as it recommended using AND in the second command. This would have resulted in output only if both conditions were true

````
metadata.event_type = "NETWORK_HTTP" AND target.url = /signin.office365x24.com/ ==OR== network.http.method = "POST"
`````

![[Pasted image 20240518223644.png]]

````
network.http.method = "POST" AND target.ip = "40.100.174.34" OR metadata.event_type = "NETWORK_HTTP"
`````
