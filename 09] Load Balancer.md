# Elastic Load Balancer
- Balances the Traffic accross multiple healthy servers (EC2 Instance OR Lambda).
- Health Monitoring:
    - Load balancers regularly check the health of servers to ensure they can handle requests.
    - If a server is detected as unhealthy or down, the load balancer will stop sending traffic to it until it is back online.
- Uses Target Groups (Group of all targeted instances/servers) to distribute load
- Helps to manage scale by allowing addition and removal of servers/instance

## Difference between TCP & UDP
| TCP | UDP |
|------------------------------------|-------------------------------|
| Transmission Control Protocol | User Datagram Protocol |
| Connection-oriented protocol | Connectionless protocol |
| Establishes a connection using a handshake (3-way handshake) | No connection setup required |
| Reliable: ensures data delivery | Unreliable: no delivery guarantee |
| Provides acknowledgement | No acknowledgement |
| Guarantees packet order | No ordering of packets |
| Error checking and retransmission | Basic error checking only, no retransmission |
| Flow control and congestion control available | No flow or congestion control |
| Higher overhead and slower than UDP | Low overhead and faster than TCP |
| Suitable for applications requiring accuracy and reliability | Suitable for applications requiring speed and low latency |
| Examples: HTTP, HTTPS, FTP, SMTP | Examples: DNS, VoIP, online gaming, streaming, Voice Transmission |

## Types of Load Balancer
1. Application Load Balancer (ALB)
    - ALB operates at layer 7 (Application Layer) of OSI model.
    - ALB suppoerts HTTP and HTTPs protocols for routing.
2. Network Load Balancer(NLB)
    - NLB is a type of load balancer designed to handle high-throughput, low-latency network traffic.
    - Operates at the Layer 4 (transport layer) of the OSI model.
    - Support TCP and UDP protocols for routing.
3. Gateway Load Balancer-
    - Operates at Layer 3 (Network Layer) and Layer 4 (Transport Layer) of the OSI model.
    - Gateway Load Balancer helps you easily deploy, scale, and manage your third-party virtual appliances like firewall.

## Create Load Balancer
1. Create Target Group
    - Go to  EC2 -> Load Balancer -> Target Groups
    - Keep Setting default, and select 'Next'
    - Select Multiple Instances which you want to be included in load balancing
    -  [IMP] -> Select `Include as pending below` to add selected Instances
    - Then select 'Next' and then 'Create target group'
2. Create Load Balancer
    - Select Load Balancer Type:
        - Application Load Balancer (Default)
        - Network Load Balancer
        - Gateway Load Balancer
    - GIve name
    - Scheme:
        - Internet-facing (for public access)
        - Internal (for private access, within the network)
    - Load balancer IP address type:
        - IPv4
        - Dualstack
            - Includes IPv4 and IPv6 addresses
        - Dualstack without public IPv4
            - Includes a public IPv6 address, and private IPv4 and IPv6 addresses
            - Compatible only with internet-facing load balancers
    - Availability Zones (AZ) and subnets
        - Must select those AZ in which our instances are present
        - You can select all the listed AZs
    - Security groups
        - [IMP] -> Select or Create Security group with Inbound Rule of HTTP and HTTPs (0.0.0.0/0)
    - Listeners and routing
        - Select Target group
    - Keep Remaining Settings Default, and Click on Create Load Balancer
