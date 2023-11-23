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
- Virtual machines (VMs)
- Routes
- Firewall rules
- 

