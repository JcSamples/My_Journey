
## Query index = main and index = *
After uploading the zipped folder, we executed our first query

index = main


![[Pasted image_20240518213938.png]](./Imagens/Pasted%20image%2020240518213938.png)    

We selected "ALL TIME" so that Chronicle could retrieve information related to our uploaded zipped folder.

We noticed that with the query index = main, we obtained various pieces of information
![[Pasted image_20240518213938.png]](./Imagens/Pasted%20image%2020240518214150.png)

## Filtering by Host: Mailsv

Let's filter the information using the query:

![[Pasted image_20240518213938.png]](./Imagens/Pasted%20image%2020240518214628.png)

We observed that we have 9,829 events out of the previous 109,000.

## Mailsv Root Login Attempts


Let's search for failed log attempts on the mailsv server for the user root using the query:

index=main host=mailsv fail* root

![[Pasted image_20240518213938.png]](./Imagens/Pasted%20image%2020240518215206.png)


We found that there were 346 login attempts.
![[Pasted]](./Imagens/Pasted%20image%2020240518215943.png)

# LAB 2

### Scenary

Review the following scenario. Then complete the step-by-step instructions.

You are a security analyst at a financial services company. You receive an alert that an employee received a phishing email in their inbox. You review the alert and identify a suspicious domain name contained in the email's body: signin.office365x24.com. You need to determine whether any other employees have received phishing emails containing this domain and whether they have visited the domain. You will use Chronicle to investigate this domain.



After identifying the suspicious domain: signin.office365x24.com, we conducted a search on the Google Chronicle 'demo' site.

![[Pasted]](./Imagens/Pasted%20image%2020240518221011.png)

![[Pasted]](./Imagens/Pasted%20image%2020240518221302.png)

````
target.hostname = "signin.office365x24.com" OR network.dns.questions.name = "signin.office365x24.com"
`````

### Whois

Out of curiosity, I also searched on the Whois site and found that the domain is registered under the name Alberto, and the server is active with the IP: 104.21.77.241.

![[Pasted]](./Imagens/Pasted%20image%2020240518221438.png)



![[Pasted]](./Imagens/Pasted%20image%2020240518222341.png)

We have by the possibility of using AI in the search engine, which made the query much easier.


![[Pasted]](./Imagens/Pasted%20image%2020240518222905.png)


![[Pasted]](./Imagens/Pasted%20image%2020240518223445.png)

````
metadata.event_type = "NETWORK_HTTP" AND target.url = /signin.office365x24.com/ AND network.http.method = "POST"
`````


I had to modify the AI query, which I didn't expect, as it recommended using AND in the second command. This would have resulted in output only if both conditions were true

````
metadata.event_type = "NETWORK_HTTP" AND target.url = /signin.office365x24.com/ ==OR== network.http.method = "POST"
`````

![[Pasted]](./Imagens/Pasted%20image%2020240518223644.png)

````
network.http.method = "POST" AND target.ip = "40.100.174.34" OR metadata.event_type = "NETWORK_HTTP"
`````
