### AWS Resource Access Manager (RAM)

- Share AWS resources that you own with other AWS accounts
- Share with any account or within your Organization
- Avoid resource duplication!
  - VPC Subnets
  - Allow to have all the resources launched in the same subnets
  - Must be from the same AWS Organizations.
  - Cannot share security groups and default VPC
  - Participants can manage their own resources in there
  - Participants can't view, modify, delete resources that belong to other participants or the owner
- AWS Transit Gateway
- Route 53 (Resolver Rules, DNS Firewall Rule Groups)
- License Manager Configurations

### RAM Use Cases

- Aurora DB Clusters
- ACM Private Certificate Authority
- CodeBuild Project
- EC2 (Dedicated Hosts, Capacity Reservation)
- AWS Glue (Catalog, Database,Table)
- AWS Network Firewall Policies
- AWS Resource Groups
- Systems Manager Incident Manager (Contacts, Response Plans) • AWS Outposts (Outpost, Site)
- and more …

### Resource Access Manager – VPC example

- Each account...
  - is responsible for its own resources
  - cannot view, modify or delete other resources in other accounts
- Network is shared so...
  - Anything deployed in the VPC can talk to other resources in the VPC
  - Applications are accessed easily across accounts, using private IP!
  - Security groups from other accounts can be referenced for maximum security
- Use cases
  - Applications within the same trust boundaries
  - Applications with a high degree of interconnectivity

### Resource Access Manager Managed Prefix List

- A set of one or more CIDR blocks
- Makes it easier to configure and maintain Security Groups and Route Tables
- Customer-Managed Prefix List
  - Set of CIDRs that you define and manage by you
  - Can be shared with other AWS accounts or AWS Organization
  - Modify to update many security groups at once
- AWS-Managed Prefix List
  - Set of CIDRs for AWS services
  - You can’t create, modify, share, or delete them

### Resource Access Manager Route 53 Outbound Resolver

- Helps you scale forwarding rules to your DNS in case you have multiple accounts and VPC