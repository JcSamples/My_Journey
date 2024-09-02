
# OSPF Commands (Fictionalized)

## Step-by-Step Configuration

1. **Establish Neighbor Adjacencies**
    - Ensure that the routers can communicate and recognize each other as OSPF neighbors.

2. **Exchange Link-State Advertisements (LSA)**
    - Distribute information about the routers and the network topology.
    - Command: `DDB` (Database Description)

3. **Build the Link-State Database**
    - Collect and store the state information of all routers in the network.
    - Command: `Request` (Querying for additional LSA information)

4. **Execute the SPF Algorithm**
    - Calculate the shortest path to each network using the Link-State Database.
    - Command: `Link state update` (Responding to LSA Requests)

5. **Choose the Best Route**
    - Determine the optimal routing path based on the SPF calculation.
    - Command: `LSAck` (Acknowledgement of LSA updates)

## OSPF Packets

- **Hello Packet**
    - Used to discover and maintain neighbor relationships.
  
- **DDB (Database Description)**
    - Summarizes the router's link-state database to a neighbor during the exchange.

- **Request**
    - Sent to request specific LSAs from a neighbor.

- **Link State Update (Response)**
    - Contains one or more LSAs, sent in response to a Request packet.

- **LSAck (Link State Acknowledgment)**
    - Confirms receipt of a Link State Update.


### Enable OSPF on Router (Example with fictional names)

````
RouterX(config)# router ospf 20
`````
### Set Router ID
RouterX(config-router)# router-id 2.2.2.2

### Define Network and Area

````
RouterX(config-router)# network 192.168.1.0 0.0.0.255 area 0
RouterX(config-router)# network 192.168.2.0 0.0.0.255 area 0
`````

### Suppress Information Exchange on Specific Interface

````
RouterX(config-router)# passive-interface g1/0/0
`````

## Additional Notes

- The `passive-interface` command prevents the router from sending OSPF packets through interfaces where it is unnecessary, such as a network directly connected to a PC.
- The command `show ip ospf neighbor` is used to verify OSPF neighbor relationships.
