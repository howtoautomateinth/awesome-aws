# Awesome AWS Collection
Categorize awesome things in AWS 

## Elastic Compute Cloude (EC2)

## Virutal Private Cloud
> [Different Between Security Group and Network ACLs](https://medium.com/awesome-aws/aws-difference-between-security-groups-and-network-acls-adc632ea29ae)

- Network ACLs are stateless but Security group are stateful
- Rule order in Network ACLs process top-to-bottom, Security group process based on number the lower number gets processed first
- The allowed block size is between a /16 netmask (65,536 IP addresses) and /28 netmask (16 IP addresses)

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
Interesting Feature
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
	- Bucket Policies
	- Access Control List
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

###### S3 Performance

> Amazon S3 bucket is going to exceed 100 PUT/LIST/DELETE requests per second or 300 GET requests per second
S3 is partitioning based on the key prefix
- Reverse the key name string
	- Normally when doing massive uploads from your application we will increase the sequence by 1 so to prevent partition issues we should reverse the key so it will not be the same
- Adding a hex hash prefix to a key name 
	- [Optimized Performance S3 Naming](https://btuanexpress.net/optimized-performance-s3-naming/)
	- 4-character hex hash will provide 65,536 list so have to aware this too

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
