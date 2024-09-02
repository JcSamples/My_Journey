Verify Leases "IP Distribution"

````Python
import re

leases_file = "/var/lib/dhcp/dhcpd.leases"

with open(leases_file, "r") as file:
    data = file.read()

leases = re.findall(r"lease (.*?) \{.*?binding state active;", data, re.DOTALL)

for lease in leases:
    ip = re.search(r"lease (.*?) \{", lease).group(1)
    mac = re.search(r"hardware ethernet (.*?);", lease).group(1)
    hostname_match = re.search(r"client-hostname \"(.*?)\";", lease)
    hostname = hostname_match.group(1) if hostname_match else "unknown"
    print(f"IP: {ip}, MAC: {mac}, Hostname: {hostname}")

```

