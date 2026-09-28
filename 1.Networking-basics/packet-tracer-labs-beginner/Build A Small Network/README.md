# Lab - 01 : Building and Testing A Small Network

## Objective
To build and test a small networking using Cisco Packet Tracer. 

### Step 1: Build the Topology
- In Packet Tracer:
    - Added one Cisco 3650-24PS Switch
    - Added two PCS
    - Renamed the devices to:
        - `Switch1`
        - `PC1`
        - `PC2`
    - Connected the devices using Copper Straight-Through cable
    - Connected `PC1` (`Fa0`) to `Switch1` (`Gig1/0/1`)
    - Connected `PC2` (`Fa0`) to `Switch1` (`Gig1/0/2`)
- [The Topology can be seen here](/1.Networking-basics/packet-tracer-labs-beginner/Build%20A%20Small%20Network/Topology.png)

### Step 2: Configuring PC1:
- Configured PC1 with:
| Setting         | Value         |
|-----------------|---------------|
| IP Address      | 192.168.10.10 |
| Subnet Mask     | 255.255.255.0 |
| Default Gateway | 192.168.10.1  |
| DNS Server      | 8.8.8.8       |

### Step 3: Configuring PC2:
- Configured PC2 with:
| Setting         | Value         |
|-----------------|---------------|
| IP Address      | 192.168.10.20 |
| Subnet Mask     | 255.255.255.0 |
| Default Gateway | 192.168.10.1  |
| DNS Server      | 8.8.8.8       |

> Both PCs are now in the same subnet: `255.255.255.0`

### Step 4: Verifying Configurations:
- To verify configurations for both`PC1` and `PC2`, we would use `ipconfig` command in the Command Prompt.
- [PC 1 Configurations can be seen here](/1.Networking-basics/packet-tracer-labs-beginner/Build%20A%20Small%20Network/PC1_ipconfig.png)
- [PC 2 Configurations can be seen here](/1.Networking-basics/packet-tracer-labs-beginner/Build%20A%20Small%20Network/PC2_ipconfig.png)

### Step 5: FINAL PING TEST:
- A successful ping tells us that IP connectivity exits between the two PCs.
- To test ping connectivity, we would use the `ping` command followed by the IP address of the PC you want to ping.
- [Pinging `PC2` from `PC1`](/1.Networking-basics/packet-tracer-labs-beginner/Build%20A%20Small%20Network/ping_to_PC2.png)
- [Pinging `PC1` from `PC2`](/1.Networking-basics/packet-tracer-labs-beginner/Build%20A%20Small%20Network/ping_to_PC1.png)

### Conclusion:
- This lab successfully demonstrated how to build and configure a basic network using Cisco Packet Tracer. Two PCs were connected to a Cisco 3650-24PS switch and configured with IP addresses in the same subnet. The configurations were verified using the `ipconfig` command, and successful ping tests between PC1 and PC2 confirmed that IP connectivity was working correctly.

- This lab helped reinforce the basic concepts of network topology, IP addressing, subnetting, switch connectivity, and network connectivity testing.