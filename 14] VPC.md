# Virtual Private Cloud
- It is an own private network
- Collection of multiple systems (EC2 Instance)
- It allows you to launch resoureces/services (like EC2, RDS) inside isolated environment
- It contains atleast 1 or multiple subnets (sub-networks)

## Architecture of VPC
![image](https://github.com/user-attachments/assets/03416acb-6cbc-4c63-a2b9-b64f0e58be6b)

### VPC (Compound of College)
- It is like a boundary to your network

### Availability Zones (Buildings in that College)
- Can be multiple
- Consists multiple subnets

### External Network (Outer Environment)
- Internet OR Public Traffic

### Internet Gateway (Gate of Compound)
- Helps External Network to communicate with VPC
- Used to activate internet connectivity for your VPC

### Route Table (Like receptionist/guard at Gate)
- Helps to find the optimal path to the resouces and subnets 
- A route table contains a set of rules, called routes, that determine where network traffic is directed
- When you create a VPC, AWS creates a route table called the main route table.
- You cannot delete the main route table.

### NACL - Optional (Guard at Floor)
- Network Access Control List, Helps to manage incoming traffic
- It is act as firewall at subnet level.
- Used to control inbound and outbound traffic at the subnet level

### Security Group - Compulsory (Guard at Classroom)
- This is also acts as a Firewall for resources like EC2 Instance
- Rules for Traffic:
    - Inbound Rules: Define what kind of incoming traffic (data coming into your server) is allowed. 
    - Outbound Rules: Define what kind of outgoing traffic (data going from your server) is allowed.

### Subnet (Floor)
- A subnet or subnetwork is a segment of a larger network designed to partition and manage traffic more efficiently
- Subnets allow you to divide a VPC's IP address space into smaller, manageable segments
- Types of Subnet
    - Public Subnet - Can access publically with internet
    - Private Subnet - No direct connectivity with internet, used to store backend
        - NAT
            - Network Address Transmission gateway
            - helps to map ip and used to communicate with Private Subnet
            - it hides the ip by exchanging it with broadcast ip.

#### Subnet Calculation
- IP Range - 0.0.0.0 to 255.255.255.255 (8 bits for each part)
- Subnet mask - denoted by "/n" (eg, 10.0.0.0/21)
- Parts of IP
    - Network Part (fixed part/bits)
        - subnet mask is used to identify this (eg, /21 means 21 bits are fixed from 32 bits)
    - Host Part (variable part/bits)
        - remaining bits form subnet is known as host part (eg, 11)
- Number of IPs (eg.)
    - network bits = 21
    - variable bits = 11
    - we get 2048 IPs (from this 2 ips [1st, last] are reserved)

Example 1
- VPC = 10.0.0.0/23
- no. of subnet = 4
- formula: 2<sup>n</sup> >= no of subnet
    - 2<sup>2</sup> = 4 (n = 2)
- 1st Subnet
    - 10.0.0.0/23+n
    - **10.0.0.0/25**
- 2nd Subnet
    - Variable bits = 32 - fixed bits(previous subnet)
    - Variable bits = 32 - 25
    - Variable bits = 7
    - No. of Host = 2<sup>Variable bits</sup>
    - No. of Host = 2<sup>7</sup>
    - No. of Host = 128
    - **10.0.0.128/25**
- 3rd Subnet
    - Add No. of Host again (128)
    - 10.0.0.**128**/25 + 128
    - **10.0.1.0/25**
- 4th Subnet
    - Add No. of Host again (128)
    - 10.0.1.**0**/25 + 128
    
    - **10.0.1.128/25**

Example 2
- VPC = 172.0.0.0/24
- no. of subnet = 3
- formula: 2<sup>n</sup> >= no of subnet
    - 2<sup>2</sup> >= 3 (n = 2)
- 1st Subnet
    - 172.0.0.0/24+n
    - **172.0.0.0/26**
- 2nd Subnet
    - Variable bits = 32 - fixed bits(previous subnet)
    - Variable bits = 32 - 26
    - Variable bits = 6
    - No. of Host = 2<sup>Variable bits</sup>
    - No. of Host = 2<sup>6</sup>
    - No. of Host = 64
    - **172.0.0.64/26**
- 3rd Subnet
    - Add No. of Host again (64)
    - 172.0.0.**64**/26 + 64
    - **172.0.0.128/26**


## Diffrenece Between Security Group and NACl (IMP for Interview)
| **Aspect**                   | **Security Groups**                                                                             | **Network Access Control Lists (NACLs)**                                                            |
|------------------------------|------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| **Rules Supported**          | Supports only **allow** rules. By default, all traffic is denied unless explicitly allowed. Cannot deny specific traffic. | Supports both **allow** and **deny** rules. By default, all traffic is denied unless explicitly allowed or denied. |
| **Statefulness**             | **Stateful:** Inbound rules automatically reflect in outbound traffic. For example, if you allow inbound traffic on port 80, outbound responses are allowed automatically. | **Stateless:** Inbound and outbound rules are independent. Changes in inbound rules do not affect outbound rules. For example, if you add an inbound rule for port 80, you must separately add an outbound rule for port 80. |
| **Association**              | Associated with **EC2 instances**                       | Associated with **subnets** within a VPC.                                                           |
| **Rule Evaluation**          | All rules are evaluated before deciding whether to allow traffic.                              | Rules are evaluated in order, starting from the lowest number. The first matching rule determines the action. |
| **Application**              | Applied to an instance **at launch** or by modifying instance attributes.                      | Automatically applied to all instances **within the subnet**.                                        |

## VPC Limits

| Component                     | Default Limit |
|-------------------------------|---------------|
| VPC                           | 5 per Region  |
| Subnets                       | 200 per VPC   |
| Route Tables                  | 200 per VPC   |
| Internet Gateway              | 5 per VPC     |
| NAT Gateway                   | 5 per AZ      |
| Virtual Private Gateway       | 5 per Region  |
| Customer Gateway              | 50 per Region |
| VPC Peering Connection        | 50 per VPC    |
| Security Groups               | 2,500 per VPC |
| Network ACLs                  | 200 per VPC   |
| Elastic IP Addresses          | 5 per Region  |
| DHCP Option Sets              | 10 per Region |
| Egress-Only Internet Gateway  | 5 per VPC     |
| Transit Gateway               | 5 per Region  |