
The KQL query `event.code:4625` filters data in Kibana to show events that have the [Windows event code 4625](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4625). This Windows event code is associated with failed login attempts in a Windows operating system.

This type of query can help identify brute force attacks, password guessing, and other suspicious activities related to login attempts on Windows systems.


```shell-session
event.code:4625 AND winlog.event_data.SubStatus:0xC0000072
```
A SubStatus value of 0xC0000072 indicates that the account is currently disabled

Using KQL's free text search we can search for `"4625"`. In the returned records we notice `event.code:4625`, `winlog.event_id:4625`, and `@timestamp`

- `event.code` is related to the [Elastic Common Schema (ECS)](https://www.elastic.co/guide/en/ecs/current/ecs-event.html#field-event-code)
- `winlog.event_id` is related to [Winlogbeat](https://www.elastic.co/guide/en/beats/winlogbeat/current/exported-fields-winlog.html)

`@timestamp` typically contains the time extracted from the original event and it is [different from `event.created`](https://discuss.elastic.co/t/winlogbeat-timestamp-different-with-event-create-time/278160)

### TimeStamps Search

```shell-session
event.code:4625 AND winlog.event_data.SubStatus:0xC0000072 AND @timestamp >= "2023-03-03T00:00:00.000Z" AND @timestamp <= "2023-03-06T23:59:59.999Z"
```


### WildCards

- `Wildcards and Regular Expressions`: KQL supports wildcards and regular expressions to search for patterns in field values. For example:

  Introduction To The Elastic Stack

```shell-session
event.code:4625 AND user.name: admin*
```

## SIEM Use Case Development Lifecycle
### STATUS and SUB Status codes

https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4625


1. `Data Points`: Identify all data points within the network where a user account can be used to log in. Gather information about the data sources that generate logs for unauthorized access attempts or login failures. For example, data might come from Windows machines, Linux machines, endpoints, servers, or applications. Ensure logs capture essential details like user, timestamp, source, destination, etc.
    
2. `Log Validation`: Verify and validate the logs, ensuring they contain all crucial information such as user, timestamp, source, destination, machine name, and application name. Confirm all logs are received during various user authentication events for critical data points, including local, web-based, application, VPN, and OWA (Outlook) authentication.

# When creating an SOP and documenting alert handling, consider the following:

- process.name
- process.parent.name
- event.action
- machine where the alert was detected
- user associated with the machine
- user activity within +/- 2 days of the alert's generation
- After gathering this information, defenders should engage with the user and examine the user's machine to analyze system logs, antivirus logs, and proxy logs from the SIEM for full visibility.

The SOC team should document all the above points, along with the Incident Response Plan, so that Incident Handlers can reference them during analysis.


Most of the other pointers remain the same, but the SOP and Incident Response Plan will differ when handling this specific type of alert. Defenders will need to focus on event.action, IP address, and the reputation of the IP, among other factors.


