# Lab - 02 : Mini Web Network

## Objective 
To build a small office network and host a webpage

### Step 1: Building the Topology
- In Cisco Packet Tracker:
    - Added 1x **Cisco 2960 Switch**
    - Added 2x **PCs**
    - Added 1x **Server**
- Connected all the devices to the switch using **Copper Straight-Through** cables
- ![Step 1](/1.Networking-basics/packet-tracer-labs-beginner/Mini%20Web%20Network/step_1.png)
---
### Step 3: Configuring the IP Addresses of the Devices
- **Configurations for PC0:**
    | Setting         | Value         |
    |-----------------|---------------|
    | IP Address      | 192.168.10.10 |
    | Subnet Mask     | 255.255.255.0 |
    | Default Gateway | NA            |
    | DNS Server      | NA            |

- **Configurations for PC1:**
    | Setting         | Value         |
    |-----------------|---------------|
    | IP Address      | 192.168.10.20 |
    | Subnet Mask     | 255.255.255.0 |
    | Default Gateway | NA            |
    | DNS Server      | NA            |

- **Configurations for Web Server:**
    | Setting         | Value         |
    |-----------------|---------------|
    | IP Address      | 192.168.10.100|
    | Subnet Mask     | 255.255.255.0 |
    | Default Gateway | NA            |
    | DNS Server      | NA            |
---
### Step 4: Configuring Web Server Services
- On the web server:
    - Click on **Services** tab
    - Select HTTP
    - Make sure it is set to **ON**
- ![webpage_services](/1.Networking-basics/packet-tracer-labs-beginner/Mini%20Web%20Network/web_server_services.png)
---
### Step 5: Testing Connectivity
- **From PC0, pinging:**
    - PC1
    - Web Server
- ![PC0 Ping](/1.Networking-basics/packet-tracer-labs-beginner/Mini%20Web%20Network/PC0_ping.png)
> Ping Test Successful
- **From PC1, pinging:**
    - PC0
    - Web Server
- ![PC1 Ping](/1.Networking-basics/packet-tracer-labs-beginner/Mini%20Web%20Network/PC1_ping.png)
> Ping Test Successful
- **Visiting the web browser on:**
    - PC0
    - PC1
- ![PC0_web_test](/1.Networking-basics/packet-tracer-labs-beginner/Mini%20Web%20Network/PC0_web_browser_test.png)
- ![PC1_web_test](/1.Networking-basics/packet-tracer-labs-beginner/Mini%20Web%20Network/PC1_web_browser_test.png)
> Both PCs successfully ping the server and displayed the webpage.

