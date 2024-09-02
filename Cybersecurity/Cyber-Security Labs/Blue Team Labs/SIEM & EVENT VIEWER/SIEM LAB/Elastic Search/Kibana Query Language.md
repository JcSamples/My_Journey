
- `Basic Structure`: KQL queries are composed of `field:value` pairs, with the field representing the data's attribute and the value representing the data you're searching for. For example:

Comandos:
Exemplo
```shell-session
event.code:4625
```

DICA: The KQL query `event.code:4625` filters data in Kibana to show events that have the [Windows event code 4625](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4625). This Windows event code is associated with failed login attempts in a Windows operating system.

By using this query, SOC analysts can identify failed login attempts on Windows machines within the Elasticsearch
This type of query can help identify brute force attacks, password guessing, and other suspicious activities related to login


## FREE QUERY SEARCH

![](../Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/1-Images/Pasted%20image%2020240225185318.png)

Comando
```shell-session
"svc-sql1"

```

AND OR NOT

KQL supports logical operators AND, OR, and NOT

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/1-Images/Pasted%20image%2020240225185540.png)

```shell-session
event.code:4625 AND winlog.event_data.SubStatus:0xC0000072
```

WILDCARDS: 


- `Wildcards and Regular Expressions`: KQL supports wildcards and regular expressions to search for patterns in field values. For example:

  Introduction To The Elastic Stack

```shell-session
event.code:4625 AND user.name: admin*
```

The Kibana KQL query `event.code:4625 AND user.name: admin*`

Com essa query podemos filtrar **"admin", "administrator", "admin123", etc.**

## How To Identify The Available Data

 Identify failed login attempts against disabled accounts that took place between March 3rd 2023 and March 6th 2023 KQL:

  Introduction To The Elastic Stack

```shell-session
event.code:4625 AND winlog.event_data.SubStatus:0xC0000072 AND @timestamp >= "2023-03-03T00:00:00.000Z" AND @timestamp <= "2023-03-06T23:59:59.999Z"
```

**Data and field identification approach 1: Leverage KQL's free text search**

Using KQL's free text search we can search for `"4625"`. In the returned records we notice `event.code:4625`, `winlog.event_id:4625`, and `@timestamp`

- `event.code` is related to the [Elastic Common Schema (ECS)](https://www.elastic.co/guide/en/ecs/current/ecs-event.html#field-event-code)
- `winlog.event_id` is related to [Winlogbeat](https://www.elastic.co/guide/en/beats/winlogbeat/current/exported-fields-winlog.html)
- If the organization we work for is using the Elastic stack across all offices and security departments, it is preferred that we use the ECS fields in our queries for reasons that we will cover at the end of this section.
- `@timestamp` typically contains the time extracted from the original event and it is [different from `event.created`](https://discuss.elastic.co/t/winlogbeat-timestamp-different-with-event-create-time/278160)
