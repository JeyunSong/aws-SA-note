## Elastic IP

**Private vs Public IP (IPv4) Fundamental Differences**

- Public IP : 
- Public IP means the machine can be identified on the internet (WWW)
- Must be unique across the whole web (not two machines can have the same public IP)
- Can be geo-located easily
- Private IP :
- Private IP means the machine can only be identified on a private network only
- The IP must be unique across the private network
- But two different private networks can have same IPs
- Machines connect to WWW using an internet gateway (a proxy)
- Only a specified range of IPs can be used private IP

**Elastic IP**

- When you stop and then start an EC2 instance, it can change its public iP
- If you need to have a fixed public IP for your instance, you need an Elastic IP
- An Elastic iP is a public IPv4 IP you own as long as you don’t delete it
- You can attach it to one instance at a time

**Elastic IP Deeper Dive**

- With an Elastic IP address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account
- You can only have 5 Elastic IP in your account (you can ask AWS to increase that)
- But, try to avoid using Elastic IP
- They often reflect poor architectural decisions
- Instead, use a random public IP and register a DNS name to it
- Or, use a Load Balancer and don’t use a public IP

**Elastic Network Interface (ENI)**

- Logical component in a VPC that represents a virtual network card
- The ENI can have the following attributes :
- Primary private IPv4, one or more secondary IPv4
- One Elastic IP (IPv4) per private IPv4
- One Elastic IP (IPv4) per public IPv4
- One or more security groups
- a MAC address
- You can create ENI independently and attach them on the fly (move them) on EC2 instances for failover
- Only bound to a specific AZ
- **Ref**. https://aws.amazon.com/ko/blogs/aws/new-elastic-network-interfaces-in-the-virtual-private-cloud/
