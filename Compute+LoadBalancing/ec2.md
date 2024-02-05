## Amazon EC2

**EC2 : Elastic Compute Cloud : Infrastructure as s Service**
- It mainly consist in the capability of : 
- Renting virtual machines (EC2)
- Storing data on virtual drives (EBS)
- Distributing load across machines (ELB)
- Scaling the services using an auto-scaling group (ASG)

**sizing & configuration options**

- Operation System (OS) : Linux, Windows or Mac OS
- Compute Power & Cores (CPU)
- Random-Access Memory (RAM)
- Storage space : 
- Network-attached (EBS & EFS)
- Hardware (EC2 Instance Store)
- Network card : speed of the card, Public IP address
- Firewall rules : security group
- Bootstrap script (configure at first launch) : EC2 User Data

**User Data**

- It is possible to bootstrap our instances using an EC2 User data script
- bootstrapping means launching commands when a machine starts
- That script is only run once at the instance first start
- EC2 user data is used to automate boot tasks such as :
- Installing updates
- Installing software
- Downloading common files from the internet
- Anything you can think of
- The EC2 User Data Script runs with the root user → sudo

**Naming Convention** - for example, m5.2xlarge

- m : instance class
- 5 : generation (AWS improves them over time)
- 2xlarge : size within the instance class

**Instance Types**

1. **General Purpose**
- Great for a diversity of workloads such as web servers or code repositories
- Balance between : 
- Compute
- Memory
- Networking
2. **Compute Optimized**
- Great for compute-intensive tasks that require high performance processors
- Use cases : 
- Batch processing workloads
- Media transcoding
- High performance web servers
- High performance computing (HPC)
- Scientific modeling & machine learning
- Dedicated gaming servers
- Class name : C
3. **Memory Optimized**
- Fast performance for workloads that process large data sets in memory
- Use cases : 
- High performance, relational/non-relational databases
- Distributed web scale cache stores
- In-memory databases optimized for BI (business intelligence)
- Applications performing real-time processing of big unstructured data
- Class name : R
4. **Storage Optimized**
- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
- Use cases :
- High frequency online transaction processing (OLTP) systems
- Relational & NoSQL databases
- Cache for in-memory databases (for example, Redis)
- Data warehousing applications
- Distributed file systems
- Class name : I, ,D, H1

- Recommended EC2 Instance Info Website [Amazon EC2 Instance Comparison](https://instances.vantage.sh/)


**Security Groups Introduction**

- Security Groups art the fundamental of network security in AWS
- They control how traffic is allowed into or out of our EC2 Instances
- Security groups only contain allow rules
- Security groups rules can reference by IP or by security group

**Security Groups Deeper Dive**

- Security groups are acting as a “firewall” on EC2 instances
- They regulate : 
- Access to Ports
- Authorized IP ranges - IPv4 and IPv6
- Control of inbound network (from other to the instance)
- Control of outbound network (from the instance to other)

**Security groups Good to Know**

- Can be attached to multiple instances
- Locked down to a region / VPC combination
- Does live “outside” the EC2 - if traffic is blocked the EC2 instance won’y see it
- It’s good to maintain one separate security group for SSH access
- If your application is not accessible (time out), then it’s a security group issue
- If your application gives a “connection refused” error, then it’s an application error or it’s not launched
- All inbound traffic is blocked by default
- All outbound traffic is authorized by default

**Classic Ports to know**

- 22 = SSH (Secure Shell) - log into a Linux instance
- 21 = FTP (File Transfer Protocol) - upload files into a file share
- 22 = SFTP (Secure File Transfer Protocol) - upload files using SSH
- 80 = HTTP - access unsecured websites
- 443 = HTTPS - access secured websites
- 3389 = RDP (Remote Desktop Protocol) - log into a Windows instance


**Placement Groups**

- Sometimes you want control over the EC2 Instance placement strategy
- That strategy can be defined using placement groups
- When you create a placement group, you specify one of the following strategies for the group

**Type**

**Cluster** :  clusters instances into a low-latency group in a single Availability Zone 

- Pros : 
- Great network
- Cons : 
- If the rack fails, all instances fails at the same tine
- Use cases : 
- Big Data job that needs to complete fast
- Application that needs extremely low latency and high network throughput

**Spread** :  spreads instances across underlying hardware 

- Pros : 
- Can span across Availability Zone
- Reduced risk is simultaneous failure
- EC2 instances are on different physical hardware
- Cons :
- Limited to 7 instances per AZ per placement group
- Use cases : 
- Application that needs to maximize high availability
- Critical Application where each instance must be isolated from failure from each other

**Partition** :  spreads instances across many different partitions

- Pros : 
- Up to 7 partitions per AZ 
- Can span across multiple AZs in the same region
- Up to 100s of EC2 instances
- The instances in a partition do not share racks with the instances in the other partitions
- A partition failure can affect many EC2 but won’t affect other partitions
- EC2 instances get access to the partition information as metadata
- Use cases : 
- HDFS, HBase, Cassandra, Kafka

**EC2 Hibernate**

- Instance terminate do any EBS volumes (root) also set-up to be destroyed is lost
- Restart, the following happens :
- First, OS boot & EC2 User Data script is run
- Following the OS boots up
- Then application starts, caches get warmed up, and that can take time !
- Introducing EC2 Hibernate
- The in-memory (RAM) state is preserver
- The instance boot is much faster (the OS is not stopped, restarted)
- Under the hood : the RAM state is written to a file in the root EBS volume
- The root EBS volume must be encrypted
- Use cases:
- Long-running processing
- Saving the RAM state
- Services that take time to initialize

**EC2 Hibernate - Good to know**

- Supported instance families : C3, C4, C5, I3, M3, M4, R3, R4, T2, T3, …
- Instance RAM size : must be less than 150GB
- Instance size : not supported for bare metal instances
- AMI : Amazon Linux 2, Linux AMI, Ubuntu, RHEL, CentOS & Windows…
- Root volume : must be EBS, encrypted, not instance store, and large
- Available for On-Demand, Reserved and Spot instance
- An instance can not be hibernated more than 60 days
