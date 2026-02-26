# Cloud Computing
- Cloud Computing is on-demand delivery of Computing services over the internet.
- These services include servers, storage, compute, databases and networking.
- Cloud Computing also referred as the accessing and storing of data. The data can be anything like images, videos, audios, documents, files etc.
- Cloud providers is the ‘Pay as you go’ principle-based services i.e. you only have to pay for the service which you are using.

## Cloud Service Providers
- Cloud computing is in huge demand so, big organization providing the Cloud services are called as Cloud Service Providers.
- Amazon AWS, Microsoft Azure, Google Cloud, Alibaba cloud, IBM cloud, Oracle cloud and VMware Cloud etc. are some Cloud Computing service Provider.

## On-premises VS Cloud Computing

| Feature                  | On-Premises                                 | Cloud Computing                           |
|--------------------------|---------------------------------------------|-------------------------------------------|
| **Infrastructure Location** | Physical location within the organization | Hosted by cloud service provider, accessed over the internet |
| **Initial Costs**        | High upfront costs for hardware and software | Lower upfront costs, pay-as-you-go model  |
| **Maintenance**          | Handled internally by the organization      | Managed by the cloud provider             |
| **Scalability**          | Requires purchasing and installing hardware | Easily scalable up or down based on demand |
| **Control**              | Complete control over hardware and data     | Less control over hardware, but manage applications and data configurations |
| **Security**             | Managed internally, requires expertise      | Managed by the provider with advanced measures; shared responsibility model |
| **Flexibility**          | Less flexible, changes and upgrades take time | Highly flexible, quick deployment of resources and services |


## Cloud Computing Models-
- Cloud architecture can be divided into:
1. Deployment Model
    - Based on the amount of data you want to store and who has access to the infrastructure.
    - The cloud deployment model identifies the specific type of cloud environment based on ownership, scale, and access, as well as the cloud’s nature and purpose.
    - Depolyment model further divided into :
        a. Public Cloud
            - Anyone can access services or resources from anywhere.
            - Managed by the cloud provider.
            - Highly scalable, as resources are virtually unlimited.
            - Pay-as-you-go model, no need for large upfront investments.
        b. Private Cloud
            - There is no need to share your hardware with anyone else.
            - A cloud environment dedicated to a single organization.
            - Managed internally or by a third-party provider.
            - Less scalable.
            - Higher upfront costs due to the need to purchase and maintain hardware.
        c. Hybrid Cloud
            - A combination of public and private clouds.
            - More costly than public cloud.
            - Managing hybrid cloud is difficult.
        d. Community Cloud (Cost Efficient, More Secure)
            - It allows system or services to be accessible by group of organization.
            - Managed by internally or by third party.
            - Cost efficient, as cost shared between community memebers.

2. Service Model
    a. IaaS
        - Delivers on-demand services or resources.
        - provides underlying os, security, storage and networking.etc
        - Usually works on pay-as-you-go model.
        - You manages everything apart from physical server.
        - Overall, it manages infrastructure, so known as hardware as service.
    b. Paas
        - PaaS provides platform and environment to allow developers to build application or access services.
        - Provides a platform allowing customers to develop, run, and manage applications without dealing with the underlying infrastructure.
        - Customer only manages/control deployed application instead of infrastructure.
    c. Saas
        - It provides sevices or application over the internet.
        - It reduces need of installing and maintaining softwares.
        - Instead of installing softwares, we simply access it via internet.
        - Most SaaS applications can be run directly from a web browser without any downloads or installations required.
        - The SaaS applications are sometimes called Web-based software, on-demand software, or hosted software.

| Feature                  | IaaS                              | PaaS                             | SaaS                           |
|--------------------------|-----------------------------------|----------------------------------|--------------------------------|
| **Definition**           | Virtualized computing resources   | Hardware and software tools for development | Software applications delivered over the internet |
| **Examples**             | AWS, Microsoft Azure, GCP         | Heroku, Google App Engine, Azure App Services | Google Workspace, Office 365, Salesforce |
| **Use Cases**            | Managing own applications, middleware, and data | Application development and deployment | Access to software applications |
| **Control and Flexibility** | Maximum control and flexibility | Less control over infrastructure | Minimal control |
| **Management Responsibility** | Users manage applications, data, runtime, middleware, OS | Users manage applications and data | Service provider manages everything |
| **Provider's Responsibility** | Service provider manages virtualization, servers, storage, networking | Service provider manages runtime, middleware, OS, virtualization, servers, storage, networking | Users interact only with the application |

## Virtualization
### 1. Type 1 Hypervisor (Bare Metal Virtualization)
- Type 1 or “bare-metal” hypervisors are installed directly on the physical hardware of the host machine.
- Type 1 hypervisors interact with the underlying physical resources, replacing the traditional operating system altogether.
- They most commonly appear in virtual server scenarios.

        +--------+   +--------+   +--------+
        | App-3  |   | App-2  |   | App-1  |
        +--------+   +--------+   +--------+
        |  VM-3  |   |  VM-2  |   |  VM-1  |
        +--------+   +--------+   +--------+
        |   OS   |   |   OS   |   |   OS   |
        +----------------------------------+
        |            Hypervisor            |
        +----------------------------------+
        |        Hardware (CPU, Storage)   |
        +----------------------------------+

### 2. Type 2 Hypervisor (Hosted Virtualization)
- Type 2 hypervisors also known as hosted hypervisor.
- It runs on top of a regular operating system (the host).
- This means it relies on the host OS to manage the computer's hardware resources, like CPU, memory, and storage, to create and run virtual machines

        +--------+   +--------+   +--------+
        | App-3  |   | App-2  |   | App-1  |
        +--------+   +--------+   +--------+
        |  VM-3  |   |  VM-2  |   |  VM-1  |
        +--------+   +--------+   +--------+
        |   OS   |   |   OS   |   |   OS   |
        +----------------------------------+
        |            Hypervisor            |
        +----------------------------------+
        |                OS                |
        +----------------------------------+
        |        Hardware (CPU, Storage)   |
        +----------------------------------+

## AWS Global Infrastructure
1. Data Center
    - A data center is a physical location that stores computing machines and their related hardware equipment.
    - These data centers allow businesses to store data, run applications, and access computing power over the internet, without needing to maintain their own hardware.
    - Generally data center infrastructure falls into three broad categories:
        - Compute
        - Storage
        - Network
2. Region
    - 37 regions worldwide
    - Region is a specific geographical area where AWS has multiple data centers.
    - Each region allows you to store and process data closer to your location, providing better performance and reliability.
    - Each Region is isolated from others to ensure fault tolerance and minimize impact from regional failures. 
3. Availability Zone (AZ)
    - Inside each region, there are multiple Availability Zones (eg. 3) which helps to keep data safe with the help of making copies.
    - Each Awailability Zone contains 2 or more Data Centers
    - An Availability Zone is made up of one or more data centers with backup power, networking, and connectivity.

4. Edge Location
    - Same like mini dataset (it is cache storage located nearest user location)