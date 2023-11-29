# GoogleCloud_Learnings

## Google Cloud Network
### Locations
Google cloud network is divided in Locations.
- North America
- South America
- Europe
- Asia
- Australia

### Regions
Each location is divided in several different regions. Region represent independent geographic areas, that are composed of zones.
e.g. europe-west-2

### Zones
Zones are areas where google cloud resources are deployed.


## Security
### Infrastructure Security
- Hardware design and provenance
- Secure boot stack
- Premises security

### Service Deployment Layer
- Encryption of inter-service communication

### User Identity Layer
- User identity

### Storage Service Layer
- Encryption at rest

### Inter Communication Layer
- Google Front End
- Denial of Service (DoS) protection

### Operation Security Layer
- Intrusion detection
- Reducing insider risk
- Employee Universal Second Factor (U2F) use
- Software development practices

## Functional Structure Of Google Cloud
Organization ---> Folder ---> Project ---> Resources
Project also accuumulate the consumption of all its resources. Each project can have its own billing and reporting.

project can also be a direct child in organization node

## IAM
Administrators can define policies to define **WHO** can do **WHAT** on **WHICH** resources.

IAM Members (The WHO part)
1. Google Accounts - a developer, an administrator, or any other person who interacts with Google Cloud
2. Service Accounts - an account that belongs to your application instead of to an individual end user
3. Google Groups - named collection of Google accounts and service accounts. Every group has a unique email address that is associated with the group
4. Google Workspace domains - a virtual group of all the Google accounts that have been created in an organization's Workspace account
5. Cloud Identity domains


Types of roles in IAM (The WHAT part)
1. Basic - (owner, editor, viewer, billing admin) when applied to a google cloud project, they affect all resources in that project.
2. Predefined - resouces speific roles, predefined actions
3. Custom - least previledge model, permissons for the role needs to defined by the creator.

IAM Policy
A policy is a collection of access statements attached to a resource. Each policy contains a set of roles and role members, with resources inheriting policies from their parent. In case of inheritance, a resource policy is a union of the resource policy and the parent resource policy. In case of conflict less restrictive parent policy will always override a more restrictive resource policy. Also, child policy cannot restrict the access granted at parent level.

*Policy insights are ML-based findings about permission usage in your project, folder, or organization.

 ## Cloud VPN - Connecting Networks to Google VPC
Cloud VPN securely connects on-premise network to google cloud VPC network through an IPsec VPN tunnel.

Traffic travelling between the two networks is encrypted by one VPN gateway, then decrypted by other VPN gateway.
For Cloud VPN, the maximum transmission unit (MTU) for on-premise VPN gateway cannot be greater than 1460 bytes, because of encryption and encapsulation of packets.

### HA VPN
- HA VPN is high availability cloud VPN. 
- HA VPN is a regional per VPC, VPN solution.
- It provides 99.99% service availability.
HA VPN gateways have two interfaces, each with its own public IP address. When you create an HA VPN gateway, two public IP addresses are automatically chosen from different address pools. When HA VPN is configured with two tunnels, Cloud VPN offers a 99.99% service availability uptime.

Various other ways - 
 1. IPsec VPN protocol - connecting over intenet and creating a tunnel connection using this protocol. It uses **cloud router** to make the connection dynamic.
 2. Direct Peering - Puts a router in the same public datacenter as a google Point of Presnce (PoP).
 3. Carrier Peering - gives direct access from an on-premise network through a service provider network. (Not covered by google SLA)
 4. Dedicated Inteconnect - Allows for one or more direct, private connections to google. Can be covered by up to 99.99% SLA
 5. Partner Interconnect - useful if the physical location can't reach a dedicated interconnect colocation facility.

### Cloud Interconnect
- Dedicated : direct physical connection between on-premise network and google cloud VPC network. At a supported co-location facility.
- Shared



## VPC Objects
- Projects : Key organizer of infra resourses in google cloud. A project contain default 15 networks that can be shared/peered.
- Networks (Default, auto mode, custom mode) : The networks do not have IP ranges, Networks are simply construct of all individual IP addresses and services within the network. Google cloud networks are global, spanning all available regions across the world.
  
- Subnetworks : Inside a network, resources can be segregated with regional subnetworks.

  Default VPC - A subnet is allocated for each region with non-overlapping CIDR blocks and firewall rules that allow ingress traffic for ICMP, RDP and SSH traffic from anywhere.

  Auto mode network - one subnet from each region is automatically created within it. The default network is actually an auto mode network. The automatically created subnets use a set of predefined IP ranges with a /20 mask that can be expanded to /16. All of these subnets fall within the 10.128.0.0/9 CIDR block.

  Custom mode network - A custom mode network does not automatically create subnets. It provides complete control over its subnets and IP ranges. The IP ranges can not overlap between subnets of same network.

 
  
- Regions : 
- Zones
- IP addresses
  - Internal, external, range
  In google cloud each virtual machine can have two IP addresses attached - Internal & External. External IP address is optional. The external IP address can be assigned from a pool making it **ephemeral** or it can be assigned from a reserved external IP address, making it **static**

External IP addresses are mapped to internal IP addresses.

- Virtual machines (VMs)

  Network throughput scales 2Gbps per vCPU.
  A vCPU (core) is equal to 1 hardware hyper-thread.

  Linux:SSH requires firewall rules to allow tcp:22
  Windows:SSH requires firewall rules to allow tcp:3389

  VM Lifecycle:
  1. Provisioning
  2. Staging
  3. Running
  4. Stopping

  Every VM stores its metadata on a metadata server.
  
- Routes : Routes let instances in a network send traffic directly to each other.

  Every network has a default route that directs packets to destinations that are outside the network.

  Routes match packets by destination IP address.
  
- Firewall rules : These rules manange the permissions for packets to travel via the routes.

  The default network has pre-configured firewall rules that allow all instances in the network to talk to each other.

  Firewall rules allow bidirectional communication once a session is established.

  Even if all firewall rules are deleted, there is still an implied "**Deny All**" ingress rule and an "**Allow All**" egress rule for the network.

  A firewall rule is composed of following parameters :
  1. direction
  2. source or destination
  3. protocol & port
  4. action
  5. priority
  6. rule assignment
 
## Compute Engine
### Machine Families
1. General Purpose : best price performance, and most flexible vCPU to memory ratios.
   E2 - cost optimized
   N2, N2D, N1 - Balanced price/performance
   Tau T2D - Scale-out optimized (best performance )
   
3. Compute Optimized : highest performance per core. Optimized for compute heavy workloads.
   C2 - Ultra high performance for compute-intensive workloads (e.g. gaming, Ad serving, AI/ML etc.)
   C2D - Ultra high performance for compute-intensive workloads & largest VM sizes (e.g. gaming, High performance computing, media transcoding)
   
5. Memory Optimized : Ideal for higher memory to vCPU ratio.
   M1 - upto 4TB memory (e.g. medium in-memory databases)
   M2 - upto 12TB memory (e.g. large in-memory databases)
   
7. Accelerator Optimized : optimized for high performance computing workloads
   A2 - e.g. ML training and inference, HPC, Massive Parallelized computation.

Apart from these custom machine types can also be created in google cloud.

### Boot Disks
VM comes with a single root persistent disk. 
Image is loaded first in onto root disk during first boot.
1. Bootable : can attach a VM and boot from it
2. Durable: cna survive VM terminate.

Types of disks.
1. Persistent disk
   Attached to a VM through the network interface.
   Durable storage (can survive VM terminate).
   Bootable (can attach to a VM and boot from it)
   Snapshots: incredible emental backups
   Performance: scales with size
   HDD or SDD options

2. RAM disk
   Highest performance

## Google Kubernetes Engine
GKE runs containerized applications in a cloud environment, as opposed to on an individual virtual machine, like Compute Engine.

## App Engine
App Engine is a fully managed PaaS offering, or platform as a service. PaaS offerings bind code to libraries that provide access to the infrastructure application needs. This means developers can just upload code and App Engine will deploy the required infrastructure.

## Cloud Functions
Cloud Functions is a lightweight, event-based, asynchronous compute solution for creating small, single-purpose functions that respond to cloud events, without the need to manage a server or a runtime environment.

It executes code in response to events, like when a new file is uploaded to Cloud Storage. It’s also a completely serverless execution environment.

## Cloud Run
It’s built on Knative, an open API and runtime environment built on Kubernetes that gives you freedom to move your workloads across different environments and platforms.

## Google Storage
### Cloud Storage
Object storage service, it allows world-wide storage and retrieval of any amount of data at any time.
Cloud storage is a collection of buckets in which objects can be placed.

Objects are immuatable.

features - 
- customer-supplied encryption key
- object lifecycle management
- object versioning
- directory synchronization (synchronizes a VM directory with a bucket)
- object change notifications using Pub/Sub

Cloud storage provides object lifecycle management policies. They specify actions to be performed on objects that meet certain rules.
e.g. downgrade storage class on objects older than a year, delete objects created before a specific date.

Cloud storage has four storage classes - 
1. Standard - best for data that is frequently accessed. (most expensive, no minimum storage duration, no retrieval cost)
2. Nearline - infrequently accessed data like data backup, long tail multimedia content and data archiving. (30 days min storage duration)
3. Coldline - inifrequently accessed data that is read at most once a quarter. (90 days minimum storage duration)
4. Archive - Data archiving, online backup, and disaster recovery. (1 year min storage duration)

Each of these storage classes provide 3 location types - 
1. multi-region (large geographic area such as United States)
2. Dual region (specific pair of regions)

Storage bucket should have a unique name globaly and cannot be nested.

For most cases IAM could be sufficient for access control.
Cloud storage also offer **ACL (Access Control List)** for finer access control.
For even more detailed control, **signed URLs** provide a cryptographic keys that gives time-limited access to a bucket or object.

**ACL**
- a mechanism to fine grain access to whom and what level.
- maximum numebr of ACLs for a bucket is 100
- Each ACL can have one or more entries. Each entry has **scope** (WHO) (for example, a specific user or group of users) and **permission** (WHAT) (for example, read or write).

### Filestore
managed file storage service for applications that require a file system interface and a shared file system for data.
Filestore offers native compatibility with existing enterprise applications and supports any NFSV3 compatible clients.

## Cloud Database
### Cloud SQL
A fully managed service of either MySQL, PostgreSQL, or Microsoft SQL Server databases.
Cloud SQL delivers high performance and scalability with up to 64 TB of storage capacity, 60,000 IOPS, and 624 GB of RAM per instance.

### Cloud Spanner
If cloud SQL does not fit a requirement because of horizontal scalability, in that case cloud spanner can be used.

Cloud Spanner is built specifically to combine benefits of relational database structure with non-relational horizontal scale.

It provides petabytes scale capacity and offers transactional consistency at global scale schemas, SQL and automatic synchronous replication for high availability.

e.g. use case financial applications

### Firestore
highly scalable NoSQL database.

fast, fully managed, serverless, cloud native, NoSQL, document databse.

It supports  ACID transactions.

### Cloud Bigtable
Fully managed NoSQL databse with petabyte-scale and very low latency.

It does not guarantee transactional consistency.

It integrates easily with popular big data tools like Hadoop, Cloud Dataflow and Cloud Dataproc.

### Memorystore
Fully managed in-memory data store service built on scalable, secure and highly available infrastructure.

It fully supports Redis protocol.


## Google Cloud Operation Suite
- Monitoring : 
- Logging
- Error Reporting
- Trace
- Profiler

## Load balancing and scaling
### Managed instance group
- collection of identical VM instances that can be controlled as a single entity using instance template.
- All instances can be updated easily by just specifying new template in a rolling update.
- managed instances can scale automatically to the number of instances required in the group.
- can work with load balancing services to distribute traffic to all instances
- can automatically identify and recreate unhealthy instances.
   
### Cloud CDN
Google Cloud CDN (Content Delivery Network) uses google's globally distributed edge points of presence to cache HTTP(S) load-balanced content close to user.
There are over 90 of these cache sites.

It can help in providing faster content delivery to users.

### SSL proxy load balancing
SSL proxy is a global load balancing service for encrypted non-HTTP traffic.

This load balancer terminates the SSL connections at the load balancing layer, then balances the connections across instances using the SSL or TCP protocols.

### Network Load balancing
- regional, non-proxied (all traffic is directly passed through the load balancer) load balancing service.
- Traffic : UDP, TCP/SSL ports

### Internal Load balancing
- regional, private load balancing
- VM instances in the same region
- TCP/UDP traffic
- reduced latency, simpler configuration
- Software defined fully distributed load balancing

## Terraform
Infrastructure as cpde (IaC)
- Terraform is an open source tool that helps to provision google cloud resources.
- In addition to Terraform, google cloud also supports other IaC tools such as Chef, puppet, Ansible, Packer.
- quick provisioning and removing of infrastructure.
- can be part of CI/CD
- deployment complexity is managed in code
- easy replication like for dev and test
- HashiCorp configuration language (HCL)
- can be used on multiple public and private clouds.

## Bigquery
- serverless, highly scalable and cost effective cloud data warehouse.
- petabyte scale
- super-fast queries

## Dataflow
- managed service for executing a wide variety of data processing patterns, transforming and enriching data in stream and batch modes.

## Dataprep
- intelligent data service for visually exploring, cleaning and preparing structured and unstructured data for analysis.
- serverless, works at any scale
- automatic schema, data types, possible joins and anomaly detection
- integrated partner service operated by Trifacta

## Dataproc
- fully managed cloud service for running Apache spark and Apache Hadoop clusters in simpler way.
- super fast to start, scale and shut down
