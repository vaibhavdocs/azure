### Azure Compute Services
- Azure VMs
- Azure Container Instances
- Azure App Services
- Azure Functions


#### Virtual Machines
- VMs are IaaS. Just like a physical computer. Better when we need total control over OS and network.

#### VMs Scale sets
- Set of indentical VMs, helpful when autoscaling is required
- Can provide highly available environment for an app/service since load can be shared among identical VMs

#### Container & Kubernetes
- Lightweight, virtualized application environment
- Basically can run multiple instances of such on single host machines
- Single Host - VMs - Single Instance
              - Container - Multiple instance
                - Virtualises the OS instead of Hardware like VMs
- Container Orchestrator
    - Azure Container Instance - PaaS Directly maintain a container
    - Azure Kubernetes Service (AKS) - Kubernetes

#### App Service
- Basically PaaS
- PaaS focuses more on the application management, deployement rather than configuration of OS
    - Web app
    - API app
    - WebJob - a script/trigger
    - Mobile apps

#### Functions
- Basically can help in communciation with other Azure services


#### Azure Batch

- Large scale parallel and high performance computing 
    - Starts a pools of VMs
    - takes a job
    - requeues if any failures 
    - scales down once works completes


#### Azure Functions

- Serverless Computing 
    - Abstraction fo the server, infrastructure and OS 

- Event-driven scale
    - Timer
    - Trigger/API or weebhook
- Micro billing
    - Pay as per the usage

#### Azure logic apps 

- More intelligentt then Azure functions, provides more ways to trigger a particular work based on data comparison helpful in enterprise applicatioon 


#### Azure Virtual Desktop

- Connect ot AVD from any secure internet.
- Centralised on teh azure side since there is no actual system provided to the user's site



### Azure Virtual Networking 

#### Isolation and Segmentation
- Allows to create multiple isolated virtual networks
- Can define private Ip address using space by using Public or Private IP Address
- IP address can be divided into range/subnet
- Name resolution service is built in Azure and DNS server can be internal or external




#### Internet communication
- Incoming connection can be defined by a public IP address or public load balancer


#### Communication between Azure Resources
- Virtual connects VMs and as well as other azure resources - App Service, AKS, VM Scale set.
- We use service endpointsd to connect to other resources such as AzureSQL database and Storage accounts

#### Communication with On-premise resources
- Point to site VPN
    - ![point _to_site](https://user-images.githubusercontent.com/36666451/132384867-18ce2909-7997-4174-a889-0caa24f72111.jpg)
- Site to site
    - Links your VPN gateways to the Azure VPN gateways in a VPN
- Azure Express Route
    - Provide dedicated connectivity to Azure

#### Route Network traffic
- Route Table
- Border Gateway Protocol
    - Propogates on premise BGP to AZ virtual networks

#### Filter Network Traffic
- Network Security Groups -
    - Filtering traffic based on source or destination IP address, port and protocol
- Network virtual appliances 
    - Specialized VM that can be compared to a hardened network appliances
    - Can carry out netework function such as runnign a firewall or performing WAN optimization
- Peering
    - Enables resources in each VNet to communication with each other
- UDR 
    - User defined routing aalwo to control the routing table between subnets within VNets and as well VNets

#### Connect Virtual Network
- Azure VPN gateway fundamentals 
    - Azure VPN gateway instances are deployed in Azure VNet
    - Connect on-premise datacenter to VNet through **site-to-site** connection
        - [data center] ------ [virtual network]
    - Connect Individual devices to VNet through a **point-to-site** connection
        - [device] ------ [virtual network]
    - Network to network
        - [VNet] ------ [VNet]

    - Can have only one gateway in each virtual network, however it can connect multiple Vnets
    - Policy based VPN Gateway
        - IKE (Internet Key Exchange) is used set security association (an agreement of encryption) between encryption
            - Static routing, soruce and destination address control hopw traffic is encrypted and they are not included in the routing table 
        - IPSec uses this association and encrypts and decrypts the data packets in tunnel (VPN Tunnel)
        - IP address is defined statically of packets that should be encrypted through each tunnel 
    - Route Based 
        - IP routing decides which tunnel to use (Static or dynamic routing protocol)
        - Source and destination is not mentioned in every tunnel's end.
        - Supports IKEv2
        - Using any-to-any traffic selection 
        - In case of this, soruce and destination are not statically defined and differetn routing protocols BGP can create dynamic routing tabels and hence data packets are encrypted based on this 

    - Deploy VPN gateways
        - Prequisites before deploying VPN gateways
            - Virtual Network
                - Basically Virtual Network should have enough address to accomodate on-premise network
            - Gateway subnet
                - This is a subnet specifically for VPN gateway
            - Public IP address
                - Acts as address. Public routable IP address as the target for on premise VPN device gateway
            - Local Network Gateway 
                - Create a local network gateway for defining on-premise network config, its public IPv4 and routing table for the VPN gateway to send data packets
            - Virtual Network Gateway
                - Routes traffic between VNet and on-premise datacenter
                - Virtual Network Gateway can be a VPn or ExpressRoute Gateway
            - Connection 
                - Connection made between VPN gateway and local network gateway
                - Connection made to VPN devices IPv4 address on the premise from one or more associated IPs of VPN or Virtual Network Gateway
                - ![VPn](https://user-images.githubusercontent.com/36666451/132390257-166eeff0-6d5d-48ac-b54f-da0b92f3a24e.jpg)
        - Required on on-premise
            - VPN device
            - IPv4 public

    - High Availability Scenarios
        - VPN gateways are deployed as two instances active/standby
        - If active goes for a toss then Standby assumes the responsibility and takes over
        
    - ExpresssRoute Fundamentals 
        - Lets you establish connection to microsoft 365, cloud services
        - Can be used any-to-any/ point-to-point Ethernet
        - Expressroute connection don't go over public internet
        - L2 - Data link layer (Node to Node communication)
        - L3 - Network Layer (Addressing and routing between nodes)

    - Features & Benefits of ExpressRoute
        - L3 connection between on-premise and Microssoft Services through a connectivity provides as mentioned previously
        - Microsoft services across all the regions
        - Dynamic routing using BGP
        - Build In redundancy
        - All geopolitical regions are available
            - Can access
                - Dynamic 365
                - MS Office 365
                - Azure Compute Services
                - Azure Cloud Services
    - Connectivity model 
        - Cloud Exchange Colocation
            - L2 and L3 offered 
            - Can request virtual cross-connection to the microsoft cloud

        - Point to point ethernet
            - [on-premise] ---- [Azure] 

        - Any-to-any 
            - Azure integrates your WAN to provide a connection between datacenter and bracnh offices. l3 connectivity and Azure can be ju8st another office for your organization
            - DNS queries, certificate revocationlist checking and Azure CDN are still send over public internet

### Azure Storage Services

#### Azure Storage Account fundamentals
    - Blob
    - File Storage
    - Disk Storage
    - Table

- Disk storage fundamentals 
    - Allows data to be persistently stored and accessed froma n attached virtual hard disk

- Blob storage
    - Object Storage solution for cloud
    - Stores text and binary
    - unstructured data
    - Access tier
        - Hot access tier
            - optimized for storing data that is accessed frequently
        - Cool
            - infrequent access and stored for 30 days
        - Archive
            - Backups, rarely access and stored for 180 days
        - Only hot and cool at the account level 

- Azure File Fundamentals 
    - Fully managed file share in the cloud and accesible via the industry standard server message block and networkj file system


#### Azure database and analytics services

- Cosmos DB
- Support schema less data
- Support constantly changing data
- Stores data in atom-record-sequence(ARS) format
- Then data is abstracted and projected as as API
- Azure SQL db
    - PaaS
    - MS handles everything
    - You can get control over db administration and optimization activities
    - Can use Azure data migration
- Postgres SQL
    - Offered in 2 manner 
    - Single Server
        - Vertical scaling based model
    - Hyperscale
        - This model option horizontaly sclaes queries across mutliple machine by using sharding

- Azure SQL Managed Instance
    - PaaS
    - Automated provisioning
    - A configurable backup retention period
    - SAerver collation is possible 

- Migration 
    - Azure database mihgraiton service
    - Big data is continuosly increasing data which will not make sense if looked diretly since it is huige in size, will require gathering insights from the same

- Azure Synapse Analytics
    - Data warehousing + big data analytics

- Azure HDInsights
    - Analytics service 
    - Supports ETL
    - Data Warehousing 
    - ML&IOT

- Azure databricks
    - Unlocks insights from all your data