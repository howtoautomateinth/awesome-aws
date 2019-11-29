# Awesome AWS Collection
Categorize awesome things in AWS 

## Elastic Compute Cloude (EC2)
#### Pricing 
Three categories 
- On-demand instance
	- pay just for the usage on a flat hourly rate or per-second billing
- Reserved instance
	- 75 percent discount compared to an on-demand instance
	- have to know how many resources your workload is going to take and for how long (at least a year)
	- Payment options
		- up-front reserved
		- partial up-front reserved
		- no up-front reserved
	- two subcategories of it
		- standard reserved instance
		- convertible reserved instance
			- have ability and flexibility to exchange the instance from one class of family to another class if your computing need changes
- Spot instance
	- biding
	- 90 percent discount compared to on-demand pricing
	- great for workloads that can restart from where they failed (in other words, can interrupt job)
#### Placement Group
Three categories
- Cluster
	- is a logical grouping of instances within a single Availability Zone
	- To provide the lowest latency and the highest packet-per-second network performance for your placement group
- Partition
	- spreads your instances across logical partitions such that groups of instances in one partition do not share the underlying hardware
	- used by large distributed and replicated workloads, such as Hadoop, Cassandra, and Kafka
- Spread
	- group of instances that are each placed on distinct racks, with each rack having its own network and power source
	- reduces the risk of simultaneous failures that might occur when instances share the same racks

## Virutal Private Cloud
### Amazon VPC Components
#### VPC
- first step of VPC is deciding the IP range by providing a Classless Inter-Domain Routing (CIDR) block, The allowed block size is between a /16 netmask (65,536 IP addresses) and /28 netmask (16 IP addresses)
	- If you create a VPC with a small size and later realize that you need more IP addresses, you can create a new VPC with a bigger IP address range and then migrate your applications from the old VPC to the new one
	- limited to a region
	
#### Subnet
- Subnet is short for subnetwork, With subnetting you can divide a network into multiple networks
- Subnet is tied to only one availability zone, If you have three AZs in a VPC, for example, you need to create a separate subnet in each AZ

#### Route Table
- route table is a table consisting of certain rules known as routes
	- provide information to route when requested
- two columns
	- Destination
		- the destinations specifies the ip range that can be directed to the target
		- Local destination, which indicates internal routing in VPC
	- Target
		- target is where the traffic is directed 

#### Internet Gateway
- allows your VPC to communicate with the Internet

#### Network Address Translation (NAT)
> NAT device, you can enable any instance in a private subnet to connect to the Internet
- two types of NAT devices available withint AWS
	- NAT instances
		- in public subnet to allow private subnet through the internet
		- created in a specific AZ, redundant NAT instances in different AZs
	- NAT gateway
		- same function as that of a NAT instance
		- you must specify an elastic IP address
		- created in a specific AZ, redundant NAT gateway in different AZs
- use case: If you want to do some firmware updates in the database server or if you want to download some database patches, how do you download them? Network Address Translation (NAT) tries to solve that problem

#### Elastic IP Address (EIP)
> Every time you launch a new EC2 instance in AWS, you get a new IP address. Sometimes it becomes a challenge since you need to update all the applications every time there is an IP address change
- an EIP is a static IP address to address that issues
- There is no charge for using an EIP

#### VPC Endpoint
- VPC endpoint does is give you the ability to connect to VPC and AWS services directly using a private connection

#### Drecit Connect
- a dedicated private connection from your corporate data center to your VPC

#### VPC Peering
- VPC peering helps to connect one virtual private cloud to another and route the traffic across the virtual private clouds
- You can’t peer VPCs across regions
- one-to-one relationship two VPCs
- can not use transit point between VPC need to peering itself

#### VPC Flow Logs
- enable you to capture information about the IP traffic going to and from network interfaces in your VPC

#### Accessing and Permission
##### Security Group
- virtual firewall applied at the instance level
- There are no deny rules, so the only way to block traffic is to not allow it
- stateful
	- change inbound (ingress) also applied to outbound (egress)
##### Network Access Control list (NACL)
- firewall at a subnet level for your VPC
- default, each custom NACL denies all inbound and outbound traffic until you add rules
- contain a numbered list of rules that are evaluated in order to decide whether the traffic is allowed to a particular subnet associated with the NACL
	- starting with the lowest numbered rule
	- recommend to start with number 100, highest number is 32766
- stateless
	- have to create rule for inbound and outbound
- [Different Between Security Group and Network ACLs](https://medium.com/awesome-aws/aws-difference-between-security-groups-and-network-acls-adc632ea29ae)

## Storage on Cloud
The storage offerings of AWS can be divided into three major categories

- File
   - Elastic File System (EFS)
- Object
	- Simple Storage Services (S3)
	- Glacier 
- Block
	- Instance Store on EC2
	- Elastic Block Storage (EBS)
> [Different Between EBS, S3 and EFS](https://dzone.com/articles/confused-by-aws-storage-options-s3-ebs-amp-efs-explained)

#### ENCRYPTION
Two main ways of securing the data
- Data in transit
	- HTTPS and use SSL-encrypted
- Data at rest
	- S3 Encryption
	- EBS Encryption

#### BLOCK STORAGE

- Considering information before using block storage type (SSD = Random & HDD = Sequential)
	- [Random VS Sequential 1](https://stackoverflow.com/questions/27180409/what-is-a-sequential-write-and-what-is-random-write?noredirect=1&lq=1)
	- [Random VS Sequential 2](https://insightsblog.violinsystems.com/blog/understanding-io-random-vs-sequential)
- Block Storage Type
	- EC2 instance store
		- the instance store is ephemeral
		- all the data stored in the instance store is gone when EC2 instance is shut down.
		- no snapshot support for instance store
		- available in a solid-state drive (SSD) or hybrid hard dive (HDD)
	- EBS SSD-backed volume
		- 2 major categories 
			- SSD-backed storage
				- random IO
				- transactional workloadssuch as database and boot volumes
				- General-Purpose SSD (gp2)
				- Provisioned IOPS SSD (Provisioned IOPS)
					- for IO-intense workload such as database
			- HDD-backed storage
				- sequential IO
				- throughput-intensive workloads such as log processing and mapreduce
				- Throughput-Optimized HDD (st1)
				- Cold HDD (sc1)
					- for noncritical support infrequently accessed
#### FILE STORAGE
> a file system interface and file system semantics to Amazon EC2 instances

##### Interesting Feature
- Shared storage 
	- shared across thousands of EC2 instances
- Elastic and Scalable
	- can grows to petabyte scale and don't need to specify a provisioned size up front
	
#### STORAGE TOOLS
- AWS SNOWBALL
	- AWS import/export tool, provides a petabyte-scale data transfer service
	- Help transfer TB highspeed to Amazon S3

#### OBJECT
##### AWS Simple Storage Services (S3)
- S3 Encryption
	- SSE with Amazon S3 Key Management (SSE-SE)
		- S3 will manage encryption keys for you. Each object is encrypted using a per-object key
	- SSE with customer-provided keys (SSE-C)
		- Custom will send encryption key in your upload request,S3 doesn’t store your encryption key anywhere
	- SSE with AWS Key Management Service KMS (SSE-KMS)
		- S3 will manage encryption keys in KMS, can seperate permissions in KMS additional layer of control
- S3 Access Control
	- Access Policies
		- IAM policy helps you control who can access your data stored in S3
		- Assign that policy to user,group or a role
	- Bucket Policies
		- Also can create at bucket level, which is called a bucket policy
		- Any object from a particular object will be applied
	- Access Control List
		- Each bucket and and object inside the bucket has an ACL associated
		- Can apply on bucket level and also object level
		- Coarse-grained control, permissions only to other AWS accounts not users in your account
- S3 Storage Class
	- Standard
		- default storage
		- fault tolerance
			- The files in Amazon S3 Standard are synchronously copied across three facilities and designed to sustain the loss of data in two facilities
		- 99.999999999 percent durability (11 nines)
		- 99.99 percent availability
	- Standard Infrequent Access
		- much cheaper than standard
		- same durability with standard
		- 99.9 percent availability
	- Reduced Redundancy Storage (RRS)
		- storage option that is used to store noncritical, nonproduction data
		- 99.99 percent durability
		- 99.99 percent availability
	- S3 One Zone-Infrequent Access
		- accessed less frequently, but requires rapid access when needed
		- single AZ so not fault tolerance
	- Glacier
		- mainly used for data archiving
		- same durability with standard
		- three main options for retrieving data
			- expedited
				- quick retrieval of data in the range of one to five minutes
			- standard
				- standard takes about three to five hours to retrieve the data
			- bulk retrievals
				- retrieve large amounts of data such as petabytes of data in a day (five to twelve hours)
- S3 Object Lifecycle Management
	- Transition action
		- objects can be transitioned to another storage class
	- Expiration action
		- define what is going to happen when the objects expire
- S3 Cross-Region Replication (CRR)
	- replicate the objects in an S3 bucket to a different region
	- use case: compliance requirement and disaster recovery considerations to keep copies of critical data that are hundreds of miles apart

##### S3 Performance

> Amazon S3 bucket is going to exceed 100 PUT/LIST/DELETE requests per second or 300 GET requests per second
S3 is partitioning based on the key prefix
- Reverse the key name string
	- Normally when doing massive uploads from your application we will increase the sequence by 1 so to prevent partition issues we should reverse the key so it will not be the same
- Adding a hex hash prefix to a key name 
	- [Optimized Performance S3 Naming](https://btuanexpress.net/optimized-performance-s3-naming/)
	- 4-character hex hash will provide 65,536 list so have to aware this too

## Identity and Access Management and Security

## Auto Scaling
- [ALB vs NLB](https://medium.com/containers-on-aws/using-aws-application-load-balancer-and-network-load-balancer-with-ec2-container-service-d0cb0b1d5ae5)
- [OSI Model Layer](https://medium.com/@madhavbahl10/osi-model-layers-explained-ee1d43058c1f) of seven layers

## Deploying and Monitoring
- [How DNS Works](https://howdns.works/)
- [How HTTPS Works](https://howhttps.works/)

## Architecture Guideline
- [Microservices Design Guide](https://medium.com/platform-engineer/microservices-design-guide-eca0b799a7e8)
- [Scaling Up to Your First 10 Million Users](https://www.youtube.com/watch?v=Ma3xWDXTxRg)

## Cost Management
- [EC2](https://www.ec2instances.info/) price comaprision

## Tools
- [AWS 2D Diagram](https://www.draw.io) visualize architecture
- [AWS 3D Diagram](https://cloudcraft.co) visualize architecture
- [CIDR RANGE VISUALIZER](http://cidr.xyz/) 
- [Chaos Monkey](https://github.com/Netflix/chaosmonkey) randomly terminates virtual machine instances and containers that run inside of your production environment for testing production server [More](https://medium.com/netflix-techblog/the-netflix-simian-army-16e57fbab116) 

## Reference books 
- [AWS Certified Solutions Architect Associate All-in-One Exam Guide (Exam SAA-C01)](https://www.amazon.com/Certified-Solutions-Architect-Associate-SAA-C01-ebook/dp/B07GL9N75H)
- [AWS Whitepaper](https://aws.amazon.com/whitepapers/?whitepapers-main.sort-by=item.additionalFields.sortDate&whitepapers-main.sort-order=desc)
