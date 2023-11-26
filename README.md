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

project can also be a direct child in organization node

## IAM
Administrators can define policies to define **WHO** can do **WHAT** on **WHICH** resources.
Types of roles in IAM
1. Basic - (owner, editor, viewer, billing admin) when applied to a google cloud project, they affect all resources in that project.
2. Predefined - resouces speific roles, predefined actions
3. Custom - least previledge model, permissons for the role needs to defined by the creator.

 ## Service Account
 accounts which do not belong to a person but a machine or service. Service account is also a resource.

 ## Connecting Networks to Google VPC
 1. IPsec VPN protocol - connecting over intenet and creating a tunnel connection using this protocol. It uses **cloud router** to make the connection dynamic.
 2. Direct Peering - Puts a router in the same public datacenter as a google Point of Presnce (PoP).
 3. Carrier Peering - gives direct access from an on-premise network through a service provider network. (Not covered by google SLA)
 4. Dedicated Inteconnect - Allows for one or more direct, private connections to google. Can be covered by up to 99.99% SLA
 5. Partner Interconnect - useful if the physical location can't reach a dedicated interconnect colocation facility.

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
   
