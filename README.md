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
-  Block
	- Instance Store on EC2
	- Elastic Block Storage (EBS)
> [Different Between EBS, S3 and EFS](https://dzone.com/articles/confused-by-aws-storage-options-s3-ebs-amp-efs-explained)

#### ENCRYPTION
two main ways of securing the data
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
	- EBS SSD-backed volume
	- EBS HDD-backed volume

#### OBJECT
##### AWS Simple Storage Services (S3)
- [Optimized Performance S3 Naming](https://btuanexpress.net/optimized-performance-s3-naming/)
	- > In short, Hex Hash Prefix naming help performance in S3 
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
	- Standard Infrequent Access
	- Reduced Redundancy Storage (RRS)
	- S3 One Zone-Infrequent Access
	- Glacier
- S3 Object Lifecycle Management
	- Transition action
	- Expiration action
- S3 Cross-Region Replication

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
