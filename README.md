# aws

General
 
For example, if the guest OS is Linux, after hardening your instance you should utilize certificate- based SSHv2 to access the virtual instance, disable remote
Amazon Web Services – Overview of Security Processes
r use ‘sudo’ for privilege escalation. You should generate your own key pairs in order to guarantee that they are unique, and not shared with other customers or with AWS.
However, getting credentials out to new EC2 instances launched with Auto- Scaling can be challenging for large or elastically scaling fleets. To simplify this process, you can use roles within IAM, so that any new instances launched with a role will be given credentials automatically.
Amazon Web Services – Overview of Security Processes
AWS security credentials with permissions specified by the role will be securely provisioned to the instance and will be made available to your application via the Amazon EC2 Instance Metadata Service.
You can create and attach an additional network interface, known as an elastic network interface (ENI), to any Amazon EC2 instance in your Amazon VPC for a total of two network interfaces per instance.
Amazon Web Services offer 3 different levels of support, which of the below are valid support levels. - Enterprise , Business and Developer. 
info:- Classless Inter-Domain Routing (CIDR) block).
AWS Setup
created IAM Roles
Created Security Groups ( ec2 and rds)
created Application LB
Created s3 bucket
created cloudfront based on s3
provisioned rds instances
point the nd to the application LB. by created Record set
provision ec2 - set the IAM role - set the user data.
URL rewrite for cloudfront.
Draw.io  https://www.draw.io/?libs=aws2&splash=0
https://support.draw.io/display/DO/2014/10/06/Using+AWS+2.0+icons+to+create+free+Amazon+architecture+diagrams+in+draw.io
 https://aws.amazon.com/certification/certified-solutions-architect-associate/
https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS_Certified_Solutions_Architect_Associate_Feb_2018_%20Exam_Guide_v1.5.2.pd017
https://github.com/agasthik/aws-csa-2017
AWS History
started 2003 Chris Pinkham and Benjamin Black
SQS Officially launched in 2004
AWS officially launched in 2006
2007 over 180,000 developers on platform.
2012 was first reinvent conf.
2013 cert launched
AWS 10K Foot Overview
16 Region & 44 AZ
6 more & 17 more on 2018
Region is a geographical area. Each region consists of  AZ - AZ is simply Data Center.
Edge Locations are endpoints for AWS which are used for caching content. Typical this consists - CloudFront, Amazon Content Delivery Network (CDN). Cloud watch is monitoring and cloud trail is logging.
 
 
 
 
 
 

Compute
EC2 Instance Types
EC2
Security Group
EC2-Instance Metadata
EC2 Placement Group
RAID, Volumes & Snapshots
Create AMI
Elastic Load Balancers
EBS Volumes 
Storage
Cloud Watch
Launch Configurations and Auto Scaling Groups.
S3 Bucket
Lifecycle Management
Glacier
EFS - Elastic File Systems 
AWS Command Line
Identity Access Managment Lab
Lambda
 EBS Volumes - Lab
Eastic Beanstalk   PAAS
Databases
Application Integration
Kinesis
API Gateway
Elastic Transcoder
SQS - Simple Queue Service.
SNS Simple Notification Service
SWS - Simple Workflow service
Networking and Content Delivery
VPC --- Virtual Private Cloud
VPC Lab PArt 1
VPC Lab Part2
Network Address Transalation ( NAT )
Network Access Control List vs Security Groups.
Custom VPC's and ELB's
VPC Flow Logs
NAT vs Bastion
VPC Endpoints
Application Services
SQS---
CloudFront – CDN
Security & Encryption.
Amazon Storage Gateway
Migration  - Snowball - reinvent 2015
DNS - Route 53. - uses IPv6
Routing Policies
Compute
EC2 Options:
What are the different types of virtualization available on EC2? - Para-Virtual (PV) & Hardware Virtual Machine (HVM)
On Demand: allow you to pay a fixed rate by hour with no commitment.
reserved - provide you with capacity reservation, offer significant discount on the hourly charge for an instance. 1 year or 3 year.
            	standard RIs' ( up to 75% off on demand)
            	Convertible RI's (up to 54% off on demand)
            	Scheduled RI's available to launch within the time windows you reserve.
spot - enable you to bid whatever price you want for instance, good for applications with flexible start and end times.
   	applications that are feasible to run at very low compute prices.
dedicated host - physical ec2 instances dedicated for your use. allowing to use your existing server-bound software licenses;
            	applications that has regulatory requirements that may not support multi tenant virtualization.
            	applications which needs licensing which does not support multi-tenancy or cloud deployments.
            	can purchase as a reservation for up to 70% off the on demand price.
EC2 Instance Types
D2 - Dense Storage
R4 - Memory Optimized
M4 - General Purpose
C4 - Compute Optimized
G2 - Graphics Intensive
I2 - High Speed Storage - IOPS
F1 - Field Programmable Gate Array
T2 - Lowest Cost, General Purpose
P2 - Graphics/ General Purpose GPU
X1 - Extreme Memory Optimized
DR Mc GIFT PX
EC2 Container Service - Docker to run.
Lightsail - VPC service
Batch - Batch Computing.
EC2
Limits 20 EC2 instances per region.
Security within Amazon EC2 is provided on multiple levels: the operating system (OS) of the host platform, the virtual instance OS or guest OS, a firewall, and signed API calls.
 #! It is called a shebang
 EC2 instances uses ECC Memory – error correcting code.
 By default all accounts are limited to 5 Elastic IP addresses per region.
 EC2 Instance Metadata using CLI - curl http://169.254.169.254/latest/meta-data/
 Launch Instance - (HVM/VM)
            	Amazon Linux AMI
    	t2 micro.  - Request Valid from/to
 	    vpc- virtual private cloud.
    	one subnet is one availability zone
    	shutdown behavior - stop
 Advanced DEtails.
	        	User data - bootstrap.
volume is virtual hard disk
Tags
	Add tags.
Security Group.
  MyWebDMZ
	SSH - TCP 22  - Anywhere / MyIP / Custom 0.0.0.0/0
	HTTP - TCP 80
	HTTPS -
Launch. public key  - private key.
 Create new pair
	name and download.
 Launch Instances
 View instance.
Description
   public ip.
   mac - CHMOD 400 <file.pem>
System Status Checks (infrastructure issue/ hypervisor) / Instance Status Checks ( traffic to the operating system)
Can't encrypt root device volume by default.
Window -- Use Putty and Putty Key Gen - no pem  -> ppk
download putty.exe/ puttygen.exe
  Use Puttykeygen- >load pem -> save private key -> passphrase- yes-> save as ppk
  putty -> copy the ip addr - name - >ec2-user@ipaddress -- SSH -Auth - browse
  Save on top
  Yes.
  sudo su
  yum update -y
  yum install httpd -y
  cd /var/www/html
   ls
  nano index.html
  Ctrl+O Ctrl+X
  service httpd start
  chkconfig httpd on ( to start automatically when ec2 starts)
EC2-Instance Metadata
http://169.254.169.254/latest/meta-data/
Snapshots are moved to s3,
snapshots are incremental, only take the changed blocks in the next snapshots
you  can create AMI both from volume and snapshots
EC2 Placement Group
primarily used for very low network latency and high network throughput, or both
- A Cluster Placement Groups can't span multiple availability zones but Spread Placement Groups can.
-  placement group name must be unique within the AWS account.
 - Only certain types of instances can be launched in a placement group (compute optimized, GPU, memory optimized, storage optimized) not like t2.micro
- recommended homogeneous instances (size and same family) in Cluster Placement Groups but Spread Placement Groups can.
A spread placement group supports a maximum of seven running instances per Availability Zone. For example, in a region that has three Availability Zones, you can have a total of 21 running instances in the group (seven per zone).
Spread placement groups are not supported for Dedicated Instances or Dedicated Hosts.
- you can't merge placement groups
- Logical grouping of instances within a single AZ
- Instances can participate in low latency, 10 GBPs network
------------------
Note: Always create Launch Configurations before creating auto scaling group.
Instances store type root volume mostly use paravirtualization. Data lost post restart of instance
RAID, Volumes & Snapshots
RAID - Redundant Array of Independent Disks
 RAID 0 - Striped, No Redundancy, Good Performance ( Gaming PC's)
 RAID 1 - Mirrored, Redundancy
 RAID 5 - Good for reads, bad of writes, AWS does not recommend ever putting RAID 5's and 6 on EBS ( Three disks or more)
 RAID 10 - Striped & Mirrored, , Good Redundancy, Good Performance
Lab - Security Group add RDP then launch instance

Configuration
Use
Advantages
Disadvantages
RAID 0
When I/O performance is more important than fault tolerance; for example, as in a heavily used database (where data replication is already set up separately).
I/O is distributed across the volumes in a stripe. If you add a volume, you get the straight addition of throughput.
Performance of the stripe is limited to the worst performing volume in the set. Loss of a single volume results in a complete data loss for the array.
RAID 1
When fault tolerance is more important than I/O performance; for example, as in a critical application.
Safer from the standpoint of data durability.
Does not provide a write performance improvement; requires more Amazon EC2 to Amazon EBS bandwidth than non-RAID configurations because the data is written to multiple volumes simultaneously.

Create AMI - Lab
Stop the instance before taking the snapshot.
 snapshots of encrypted volumes are encrypted automatically.
 volumes restored from encrypted snapshots are encrypted automatically
 you can share snapshots, but only if they are unencrypted.
> AMI Types ( EBS vs Instance Store)
   You can select AMI based on.
 	Region, Operating System, Architecture (32-bit or 64), Launch Permissions,
            	Storage for the Root Device
                            	Instance Storage a.k.a Ephemeral Storage -
			Instance store backend volumes are not persistent.can’t be stopped, data will be wiped.
Cannot be detached or reattached to other EC2 instances.
                        Unlike EBS backed volumes, this cannot be stopped, if the underlying host fails, you will lose your data.
                                            	only reboot or terminate, can't detach the volumes from instance
                                            	root device for a ok instance launched from the AMI is an instance store volume created from a template stored in amazon s3
                            	EBS Backed Volumes --
				EBS backed volumes are persistent. Data persist even after its stopped 
				Can be detached or reattached to other EC2 instances. 
                                            	root device for an instance launched from the AMI from an Amazon EBS snapshot
            	                        you can stop and start the instance. can move within the aws data center by stopping and starting your ES. two sinstance, after stopping the server)
Elastic Load Balancers  - X Forwarded For Header 
Classic Load Balancer routes traffic(http/https) based on either application or network level information. Application Load Balancer(layer 7) routes traffic based on advanced application level information that includes the content of the request. Classic Load Balancer is ideal for simple load balancing of traffic across multiple EC2 instances, while the Application Load Balancer is ideal for applications needing advanced routing capabilities, microservices, and container-based architectures. Network Load Balancer operating at the connection level(layer 4)
Classic LB, http/https applications and use layer 7-specific features, such as X-Forwarded and sticky session 
  Response timeout - waiting for the response
  interval - waiting between intervals for the response
  unhealthy threshold - before making instance is down
  healthy - how many consecutive test passed before telling its healthy
EBS Volumes  - only root device vol will be terminated in case of terminating the instance
Types--
 - General Purpose SSD ( GP2)
 - Provisioned IOPS SSD (I01) - good for i/o intensive application such as large relational or nosql db. use for more than 10,000 IOPS
 - throughput optimized HDD (ST1) - good for big data, data warehouse, log processing, cannot be boot volume.
 - Cold HDD (SC1) - lowest cost storage for infrequently accessed workloads. cannot be bot volume
 - magnetic (standard)  lowest of all ebs volume types that is bootable.
root vol - where operating system is.
move ebs vol from one aval zone to another - create snapshot then create a new vol from the snapshot in a new avil zone.
Copy - move snap to new regions.
Create Image-  take from snapshot. then create an AMI/ running ec2 instances then create AMI
Storage
Snowball - is to bring large set of data in to AWS not using internet, such as terabytes
Storage Gateway -
Cloud Watch
Monitoring utilization CPU  -
Monitoring write and reads Disc -
Monitoring network ins and outs Network -
Status
Launch Configurations and Auto Scaling Groups.
Auto Scaling has several schemes or plans that you can use to control how you want Auto Scaling to perform. The Auto Scaling plans are named Maintain Current Instant Levels, Manual Scaling, Scheduled Scaling, and Dynamic Scaling.
Default Termination Policy
If there is more than one Availability Zone with this number of instances, select the availability Zone with the instances that use the oldest launch configuration.
If there is one unprotected instances in the selected Availability Zone use the oldest launch configuration, terminate it.
If there are multiple instances that use the oldest launch configuration, determine which unprotected instances are closest to the next billing hour, terminate it.
If there is more than one unprotected instance closest to the next billing hour, select one of these instances at random.
S3 Bucket (bucket means Foda) Object based storage, supports 0 -5tb
AWS Import/Export allows for the importation of large data sets, using external hard disks which are sent directly to amazon, therefore bypassing the internet.
The valid ways of encryption data on S3 are Server Side Encryption (SSE)-S3, SSE-C, SSE-KMS or a client library such as Amazon S3 Encryption Client
Amazon S3 is secure by default. Use access control mechanisms such as bucket policies and Access Control Lists (ACLs) to selectively grant permissions to users and groups of users
Amazon S3 buckets in all Regions provide which of the following- Read-after-write consistency for PUTS of new objects AND Eventually consistent for overwrite PUTS & DELETES
Buckets are universal namespace
S3 has eventual consistency for which HTTP Methods? --> overwrite PUTS and DELETES
S3 is a safe place to store your files. It is object based store. the data is spread across multiple devices and facilities.
Two type - Object based( video, photo, pdf) like flat files. and block based (used for database, operating system)
S3 is simple key value store.
S3- Versioning-----------
once enabled versioning can be only suspended not disable.
Stores all version of a object- such as writes and delete
great backup tool
integrates with lifecycle rules
versionings MFA delete capability, which uses multi - factor authentication.
Cross REgion replication. 
- requires versioning on source and destination buckets
- regions must be unique
- files in an existing bucket are not replicated default, all subsequent updated files will be replicated automatically.
by default not the existing items will be replicated when new replication in place.
source$ copy the existing using cli - aws s3 cp --recursive s3://destination
cros won't copy permission  by default  ???  yes
cros - file deleted sources will be deleted from destination  ?? yes however deleting individual versions or delete markers will not be replicated.
cros - file update on source will be updated in the destination
bucket --- management - replication
 
CORS - Permission - use website url not s3 bucket url.
Tiered Storage Available
Lifecycle Management. -- object cost saving.
Add lifecycle rules.  --> Ad transition. - > Standard IA  (object has to be alteat over 128 kb for transitioning and min of 30 days after the creating date.)
                            	  	--> Ad transition. - > Glacier ( 30 days after migrated to IA)
Life cycle can be used with or without versioning
            	   can be applied to current version and previous version
            	   permanently delete.
Secure data using Access Control List and Bucket Policies.
Glacier------- -- Glacier - very cheap , but used for archival only.
S3 Storage Tiers/ Classes
 1. S3 ( durable, imme. available, frequently accessed)
 2. S3 - IA (Infrequently Accessed) - Good for less accessed but rapid access when needed. Lesser than s3 but  changed for retrieval.
 3. RRS - Reduced Redundancy Storage.
 4. Glacier - very cheap but used for archival.
S3 Charges - Charged for - Storage - Request - Storage Management Pricing. Data Transfer Pricing (income is free) , Transfer Acceleration (if using Edge Location).
>>>S3 Transfer Acceleration - utilises the cloudfront edge network to accelerate your uploads to s3. amazon uses its own optimisation technology to send from edge to actualy s3 location
>>>S3 Static Web Page creation - if you plan route53 with s3. make domain name and bucket name as same.
  static url is always - <bucketname>.s3-website-region.amazonaws.com
EFS - Elastic File Systems  - block by storage. - used ec2 instances should be on same security groups
EFS is a file storage service for EC2 instances.
supports nfs version 4.
data is stored across multiple AZ's within a region.
solution for current problem- can't mount ebs values with two ec2 instance
same like s3 , read after write consistency.
Exam Tips :  Which of the following is not a valid configuration type for AWS Storage gateway? - Gateway-accessed volumes
AWS Command Line
aws s3 ls
aws configure
access key id from excel
password
region name eu-west-2a
enter for default output
aws s3 ls
aws se help ctrl+C to come out
ec2-user# cd ~
ls
cd .aws
ls
aws ec2 describe-instances
aws ec2 terminate-instances --instance-ids <ID>
Identity Access Management Lab
Centralized control of your aws account.
shared access to aws account
granular permissions
identity federation ( include active directory, fb , linkedin ete)
multi factor authentication
provide temp access for users/devices and services where necessary.
allows to set up own password rotation policy
integrated with many different aws services
supports pci dss compliance
Users - end users
groups - a collection of users under one set of permissions
roles- create roles and can then assign them to aws resources
policies - a document that defines one or more permissions.  users - group and roles can shared the same policy document
billing alert by cloudwatch
Power User Access allows - access to all aws services except for management of groups and users within IAM.
policy documents are written in json.
Lambda
What is Lambda ?
Data Centres.
Hardware
Assembly Code/ Protocols.
High Level Language.
Operating system.
Application Layer/ AWS APIs.
AWS Lambda.
How is lambda priced.
Number of Request. - first million request is free $0.20 per 1 million request thereafter
Duration - duration is calculated from the time your code begins executing until it returns or otherwise terminates.
Tips- Lambda scales out automatically.
            	Lambda function are independent, 1 event 1 function
            	Lambda is serverless.
            	know what services are serverless.
            	lambda functions can trigger another lambda functions,1 event can = x functions
            	use Aws x-ray service to debug issues.
Security Labs.  - A security group is a virtual firewall. All inbound traffic is blocked by default. ec2 instance against
                            	  security groups are many to many relation. Security Groups are stateful. Network access control list are stateless
              	use NACL to block specific ip address, not using security groups
	
Network - Security
            	Security Groups
            	 Select MyWebDMZ
        	See  inbound and outbound - (whatever allowed inbound automatically  added in outbound rule)
      	default
         	RDP
             Mysql/Aurora
  EBS Volumes - Lab
   Ec2- >
   Generic
   EBS- Magentic -- can't upgrade on the fly
   Throughput
   cold HDD
Elastic Beanstalk   PAAS
With Elastic Beanstalk, you can deploy, monitor and scale application quickly
It provides developers or end users with the ability to provision application infrastructure
is an almost transparent way.
 
 
Build A Serverless WebPage
Web Page with API Gateway and Lambda.
Databases
RDS
 SQL Server , Oracle, MySQL Server, PostgreSQL,  Aurora, MariaDB
 
Non RDS
 DynamoDB  (Collection == Table , Document == Row, Key Value == Fields)
 Consistent, single digit millisecond latency.
Fully managed DB – supports both document based & Key-value data models.
Stored on 3 geographically distinct DCs (not AZs). Built in redundancy
RDS v/s DynamoDB
Use DynamoDB for Push button scaling. With RDS – to scale horizontally a new instance must be created.
DynamoDB is cheap for reads and expensive for writes.
Use RDS if data requires joins and relationships.
Elasticache
 Is a web service to in memory cache in the could.
 Supports
            	Memcached
            	Redis
Exam Tips
ElastiCache is used if DB is primarily read-heavy and not frequently changing
Use Redshift – if application is slow due to constant OLAP transactions on top of OLTP focused DB.
Database Migration Services.
Redshift- data warehouse and business intelligence service.

Performance
Redshift is 10 times faster than usual OLAP systems.
It uses Columnar Data Store. Columnar data is stored sequentially on storage system. Hence low I/O required – improving performance
DynamoDB support both document and key value data models. support 35 level of nesting in table
Stored on SSD Storage
DynamoDB allows for the storage of large text and binary objects, but there is a limit of 400 KB.
spread across 3 geo distinct data centers.
Data consistency Model
            	Eventual Cosnsitent Reads - Best Read Performance
            	Strongly Consistent Reads
The Basics.
  Table
  Items ( this a row)
  Attributes( fields)
Pricing.
 First 25 GB stored per month is free
 Storage costs of 0.25 GB per month thereafter.
 Creating a DynamoDB
 Create a role dynamodb - Amazon ec2- dynamodb full access
Application Integration
Kinesis
Kinesis is a platform on AWS to send your streaming data.
3 Major Kinesis Services;
            	Kinesis Streams
                            	using shards, data retains from 24 hours to 7 days
            	Kinesis Firehose
                            	no shards - completely automated, no automatic retention data.
            	Kinesis Analytics
                            	allows to run sql queries on the data
Kinesis is used to stream large amount of social media, news feeds logs etc  in to the cloud.
Process large amounts of data – Redshift for BI and Elastic Map Reduce for Big Data Processing.
API Gateway
Low cost & Efficient.
Scales effortlessly
Caching capabilities to increase performance.
You can throttle requests to prevent attacks.
Enable CORS on API Gateway.
Elastic Transcoder
Media Transcoder in the cloud.
Convert media files from their original source format into different formats that will play on smartphone, tablets , PC's
SQS - Simple Queue Service.
Messages can contain up to 256 KB of text in any format.
Default Visibility timeout is 30 seconds. this is for how long message will no longer be visible in the queue.
Visibility timeout clock starts only when the application server has picked up the message.
Use ChangeMessageVisibility action to specify a new timeout value.
Does not offer FIFO
12 hours visibility timeout.
256kv message size now available
billed at 64 kb chunks.
SQS Messages can be delivered multiple times in any order.
Also need to ensure message is only processed once
Cost saver - SQL Long Polling does not return a response until a message arrives in the que or the long poll timeout. Maximum long polling time out is 20 seconds.
SQS Fanning Out. Whenever a message is sent to the SNS topic, the message will be fanned out to the SQS queues. ie. SNS will deliver the message to all the SQS queues that are subscribed to the topic
SNS Simple Notification Service
Amazon’s SNS has the following subscribers; Lambda, SQS, HTTPS, Email, SMS
SNS is a web service that makes it easy to set up, operate and send notifications from the cloud.
SNS follows the pub sub message paradigm. notification that eliminates the need to periodically check or poll for new info. which is again SQS.
SNS Topics
SNS Benefits
Both Messaging Services in AWS.
SNS - Push
SQS - Polls ( Pulls )
Pricing - pay $0.50 per 1 million Amazon SNS Requests.
            	  	$0.06 per 100,000 notifications deliveries over HTTP
            	  	$0.75 per 100 notification deliveries over SMS.
            	  	$2.00 per 100,000 notification celiveries over Email.
SWF - Simple Workflow service
Is a web service that makes it easy to coordinate work across distributed application components.
SWF a task is assigned only once and is never duplicated. this is the diff from SQS
SWF Worker : Workers are programs that interact with Amazon SWF to get tasks, process received tasks, and return the results.
Workflow starters: An application that can initiate(start) a workflow. 
SWF Decider : The decider is a program that controls the coordination of tasks, ie. their ordering, concurrency and scheduling according to the application logic.
SWF Domains : your workflow and activity types and the workflow execution itself are all scoped to a domain.
SWF vs SQS
SWF presents a task oriented API where SQS offers a message oriented API
Amazon MQ.
Step Functions.
Customer Engagement============== not exam topic
Connect
SES
Networking and Content Delivery
VPC --- Virtual Private Cloud   - subnetting - networking - security networks - (one subnet means one availability zone)
A subnet that's associated with a route table that has a route to an Internet gateway is known as a public subnet.
Route tables basically say which subnet is allowed to which other.
Security groups are stateful ; network access control lists are stateless.
Security groups control inbound and outbound traffic for your instances, and network ACLs control inbound and outbound traffic for your subnets.
How many VPC's am I allowed in each AWS Region by default?  5
VPC is virtual data centre in the cloud
every region in the worlds has default VPC
Connect to VPC by two ways.
 Internet Gateway - unusual internet access - usually has only one internet gateway per VPC
 Virtual Private Gateway. - using VPN
CIDR.xyc 10.0.0.0 28(smallest) - 16 (gives biggest IP ranges possible)
Default VPC vs Custom VPC
Default -
 Each VPC has its own public and private subnets
Each ec2 instances has both public and private ip addresses
 Do not get private subnets in dufault VPC's , we have to set it up.
Custom-
    Default Security group, network ACL & route table are created for each custom VPC    you create.Doesn’t create subnets or internet gateways out of the box.
   You wont get public ip address for the private subnet in the custom vpc.
   Before you can access an instance in your public subnet, you must assign it an Elastic IP address.
VPC Peering.
  Allows you to connect one VPC with another via a direct network route using private IP addresses.
  You can peer VPC's with other AWS accounts as well as with other VPC's in the same account.
VPC Lab PArt 1
Create VPC---
When ever we create a new VPC it creates Routes, Security Groups, Network ACLs - no subnets
Create Subnets--
 10.0.1.0/24 give 251 ip addresses. ( why not 256 ? the first four and last IP address in each subnet CIDR block are not available for you to use, and cannot be assigned to an instance.)
 10.0.2.0/24
Create Internet Gateway.Create and attach to VPC
 Route Tables
  Every single time when you create a new subnet it going to associate to the main route table. And get internet to all those subnets.
  Look for the main route table. - recommended no to have internet
  Create a new route table
            	Enable internet access - Go to Route - Edit > Add another route -> Dest:0.0.0.0/0 , Target: out internet gateway created + ::/0 and IGtway
    	Subnet associations - Edit -> add 10.0.1.0 as public
 Come to the subnet list, pick the one made public, select -> subnet actions -> enable auto-assign public IPv4 address
Create New EC2 Instance - chose the public one first in the network
  Security groups won't span VPC's - the one you have created in the default won't be available. So create one for SSH, HTTP, HTTPS
Create second Ec2 instance choosing the private subnet
  go with the default sec group.

VPC Lab Part2 
Create new security group for the private subnet - SSH, HTTp/s, Mysql/Aurora, ICMP - allow the ping instances in the private security group or private subnet from public subnet.
 Recommended approach to connect private from public - use a bastion host access a gateway between public service and private service.
Modily the second ec2 instance to the newly creay sec group from default.
Enabling Internet access to the private network.
Network Address Translation ( NAT )
solves not running yum update -y in the private subnet where there is no internet.
You will also require a security group for your NAT instance (NATSG), which allows the NAT instance to receive Internet-bound traffic from instances in the private subnet, as well as SSH traffic from your network. By default, the NAT instance is launched using the default security group.
Shortcut - log in to public and then to private.
--> Steps using NAT Instance--
Create new ec2 instance - chome Community AMI - search for nat - pick amzn-ami-vpc-nat-hvm - Use WebDMZ Sec Group. 
After instance up - select the created one - actions - networking - Change source dest/ check (why? each ec2 instance performs source/destination check by default. A NAT instance must be able to send and receive traffic when the source or destination is not itself.)
Go to Route Tables - ? edit the default VPC route created -> Routes , Desti:0.0.0.0/0 Target - chose the nat ec2 instance created.
NAT Instance is one EC2 instance. You are responsible for performance management, scale out and security groups. 
Security groups are always associated with NAT Instances.
Elastic IP has to be added to NAT Instance.
NAT instance is single point of failure. You can place NAT instance behind Auto Scaling group, multiple subnets in different AZs and scripted failover. 
You can use Network ACLs to control traffic for both NAT Instance and Gateway.
Both NAT Instance and NAT Gateways are deployed to public subnet. 
You cannot use NAT instance to SSH / RDP into private subnet.For that Bastion (Jump Box) is required.
NAT instance is used to provide internet connectivity to private subnets.



NAT Gateway. -
-> NAT Gateways.  Operates on IPv4 	|| ingress Operates on IPv6
--------- Use NAT - Gateway instead of NAT- Instance for HA. Also create NAT gateway in different AZ ------
--> Steps using NAT Gateway
NAT Gateway is a managed service.
NAT Gateway is automatically assigned a public IP.
NAT Gateways scale up to 10GBps. No need to disable source/ destination checks on Gateways.
Go to VPC
Create NAT Gateway.
Select the public subnet from the custom VPC.
Create new Elastic IP address.
Edit the default route tables only after the gateway is available
Once up - go to Route tables - select the default route table ( takes 15 mins)
   Modify route
            	Dest: 0.0.0.0/0 and Target is Nat Gateway.
Go to public and connect private thenrun any yum install command it will work
Network Access Control List vs Security Groups.
NACL contains a numbered list of rules that is evaluated in order, starting with the lowest numbered rule.
Your VPC automatically comes a default network ACL, and by default it allows all outbound and inbound traffic.
You can only associate one subnet to one network ACL, not to multiple ACL's; however you can associate a network ACL with multiple subnets.
Security Group
Network ACL
Operates at the instance level (first layer of defense)
Operates at the subnet level (second layer of defense)
Supports allow rules only
Supports allow rules and deny rules
Is stateful: Return traffic is automatically allowed, regardless of any rules
Is stateless: Return traffic must be explicitly allowed by rules
We evaluate all rules before deciding whether to allow traffic
We process rules in number order when deciding whether to allow traffic. Lower order rules take effect in case of conflict with higher order rules.
Applies to an instance only if someone specifies the security group when launching the instance, or associates the security group with the instance later on
Automatically applies to all instances in the subnets it's associated with (backup layer of defense, so you don't have to rely on someone specifying the security group)
With default ACL, all inbound and outbound traffic is allowed automatically
When custom ACL, all inbound and outbound traffic is denied by default
NACL will be evaluated first.
VPC Dashboard
--Network ACL
--- Create a new NACL
----- name and select the default VPC.
 	Each subnet in the VPC must be associated with a network ACL.the subnet is automatically associated with the default network ACL.
 	All inbound and outbound rules are set to deny everything. Whenever you create a private NACL, everything is deny by default
 	Inbound/Outbound Rules :- open http, https inbound and outbound starting 100 as rule# - destination 0.0.0.0/0
 	Subnet associations - tag the public subnet
NACL applies first before Security Groups.
Custom VPC's and ELB's
You need at least 2 public subnets in order to deploy an application load balancer.
-Load Balancer
--Create Load B
---Application LB
AZ - use the VPC
select public subnets. - needs to public subnets-
VPC Flow Logs
A feature that enables to capture information about the IP traffic going to and from network interfaces in VPC. Flow logs data is stored using amazon Cloudwatch logs. 
Flow logs can be created at 3 levels;
            	VPC
            	Subnet
            	Network Interface Level.
 Limitations
            	Cannot enable flow logs for VPC's that are peered with your VPC unless the peer VPC is in your account
            	You cannot tag a flow log
            	After you've created a flowlog, you cannot change its config; ex; can't associate a different IAM role with the flow log.
NAT vs Bastion
NAT is used to provide internet traffic to EC2 instances in private subnets
A Bastion is used to securely administer Ec2 instances(using ssh or Rdp) in private subnets
VPC Endpoints
An Amazon VPC endpoint enables you to create a private connection between your Amazon VPC and another AWS service without requiring access over the Internet or through a NAT instance, a VPN connection, or AWS Direct Connect. Endpoints support services within the region only.
Two different types endpoints - interface( an ENI going to be attached to the ec2 instances and that's going to serve a point of entry for the network) and gateway ( similar to nat gateway - HA) - 
Create a role for ec2 - s3 admin full access
When you launch an instance into a default VPC using EC2-VPC, we do the following to set it up for you:
• Create a default subnet in each Availability Zone
• Create an Internet gateway and connect it to your default VPC
• Create a main route table for your default VPC with a rule that sends all traffic destined for the Internet to the Internet gateway
• Create a default security group and associate it with your default VPC
• Create a default network access control list (ACL) and associate it with your default VPC
• Associate the default DHCP options set for your AWS account with your default VPC
In addition to the default VPC having its own private IP range, EC2 instances launched in a default VPC can also receive a public IP.
Application Services
SQS
            	SQS is a pull base system.
            	Messages are 256 kb in size.
You are billed at 64KB Chunks- 64KB chunk = 1 request. So a message of 256KB = 4 requests.
            	Messages can be kept in the queue from 1 min to 14 days. the default is 4 days.
            	visibility timeout ( max 12 hours) is the amount of time that the message is invisible in the SQS queue after a reader picks up that message.
            	SQS is a web service that gives you access to a message queue.
            	Long Polling, which does not return a response until a message arrives in the queue.- best for cost perspective.
            	Two type of queues:
                            	Standard Queues – Default
                            	Fifo Queues. - guarantees  the order of the message received and delivered.
CloudFront - CDN
Is a system of distributed servers that deliver webpages and other contents to a user based on geographic locations of the user.
Edge Location is where content is going to be cached.Each object stays in an edge location for 24 hours before it expires
Key terminology
Two types of distributions
 1.Web Distribution - typically used for websites
 2.RTMP - used for media streaming. particular with adobe flash
Lab-
Can have multiple origin in same distribution.
Security & Encryption.
by default all newly created buckets are PRIVATE
setup access control to the buckets using:
            	bucket policies
            	access control lists.
Encryption.
  Two types of encryption:
            	In Transit;  ->
                            	SSL/TLS -> when you sent information between your buckets or from pc to buckets
            	At Rest
                            	Server Side
                                            	1. S3 managed keys - SSE-S3 -> each object is encrypted with unique key and strong MF Encryption.
                                            	2. AWS Key Management Service , Managed Keys - SSE-KMS. -> provides audit trail,enabled your manage encryption key.
                                            	3. Server side encryption with customer provided keys - SSE-C ->enabled your manage encryption key and amazon manage the encryption.
                            	Client Side
                                            	You encrypt the data client side and upload to s3.
Amazon Storage Gateway
a hybrid storage service that enables on-prem software appliance with cloud-based storage to provide seamless and secure integration.
File Gateway (NFS)  --> for flat files, word, picture, video, etc, directly stored on s3
AWS File Gateway Architecture
A file gateway provides a simple solution for presenting one or more Amazon S3 buckets and their objects as a mountable Network File System(NFS) to one or more clients on-premises.
A “bucket share” consists of an NFS share hosted from a file gateway across a single Amazon S3 bucket. The file gateway virtual appliance currently supports up to 10 bucket shares.
Volumes Gateway (iSCSI) --> for block based storage good for operating systems. stored in the cloud as amazon EBS snapshots.
            	Stored Volumes - copy entire set from on prem to aws -- stored as ebs snapshots in S3
            	Cached Volumes- copy only those which is most recently accessed.
Tape Gateway (VTL) --> Backup and archiving solutions.
            	leverage your existing tape-based backup application infrastructure to store data on virtual tape cartridges that you create on your tape gateway.
Migration >>>>> Snowball - reinvent 2015
replaces import/export disk that sent to amazon.
 three different:
 snowball
            	petabyte scale data transport solutions
 snowball edge 
            	100TB data transfer and compute coapabilities, you can also run lambda functions.
 snowmobile
    	petabyte  or hexabyte of data transfer.
exam tips:
 snowball can import and export to s3.
API Gateway - way on creating your own API to co
Direct Connect - way of running dedicated line from your own datacenter to AWS data center
DNS - Route 53. - uses IPv6
Route53 has a security feature that prevents internal DNS from being read by external sources. The work around is to create a EC2 hosted DNS instance that does zone transfers from the internal DNS, and allows itself to be queried by external servers.
Two different type of IP addresses.
IPv4 and IPv6
 IPv4 is a 32 bit field and has over 4 billion different address
 IPv6 was created to solve this depletion issue, has 128 bits
Domain Registrars.  Each domain name becomes registered in a central database known as the WhoIS database
A Records - IP Address
TTL - Time to Live
CNAMES - Canonical Name can be used to resolve one domain name to another. for ex. https://..aws and http://aws


Alias Records.
Routing Policies
Simple - good for one web server that serves content for the http://abc.com website.
Weighted -  let you split your traffic based on different weights assigned.
20 % traffic to us-east1 and 80% us-west-1 or could be two different ELB in same region.
Latency
Latency based routing allows you to route your traffic based on the lowest network latency for your end user(region with fastest response time)
Failover
used when you want to create an active/ passive set up. for ex. primary site in eu-west-2 and your sec. DR site in ap-southeast-2
Route 53 will monitor the health of primary using the health check.
Create a health check route 53 using the domain name. ( dns address of the ELB)
Create a health check route 53 in the main production domain.
 Geolocation
routing based on geolocation.
 
Exam Tips.
 OpsWorks  - Orchestration service that uses Chef 
 Current limitation of 20 accounts for consolidated billing. 
Well Architected Framework.
Security Pillar Key AWS Services;
Data protection  :  ELB, EBS, S3 and RDS
Privilege Management: IAM, MFA
Infrastructure Protection: VPC
Detective Controls: Cloud Trail, Config, Cloud Watch
Reliability Pillar
Foundation: IAM, VPC
Change Management: Cloudtrail
Failure Management :- Cloudformation
Performance Efficiency
Democratize advanced technologies
  Media Transcoder, DynamoDB, Machine learning
  go-global in mins.
  cloudformation
use serverless architecture
Definition
 Compute - Autoscaling
 Storage - EBS , S3 , Glacier
 Database - RDS , DynamoDB, Redshift
 space time trade off - cloudfront, elasticache, , direct connect, rds read replicas
 Cost Optimization Pillar.
Definition
 Matched supply and demand - Autoscaling
   Cost-effective resources -  EC2(reserved instances), AWS trusted advisor
   expenditure awareness - Cloudwatch alarms, SNS
   optimizing overtime - AWS Blog , AWS Trusted Advisor
 Operational Excellence Pillar.
  Definition
   Preparation - Runbooks and Playbooks
   Operation  - CI/CD - Code Commit, Code Deploy,  Code Pipeline
   Response - notifications - Cloud watch
Additional  Exam Topics.
Tags - Resource Groups
Resource groups makes it easy to group the resources using the tags that are assigned to them.  Recourse groups contain informations such as - Region, Name, Health Checks


VPC Peering
Is simply a connection between two VPCs that enables to route traffic between them using private IP address. VPC peering can be done between your own VPCs or with a VPC in another AWS account within a single region.  If two VPC having same internal ip range or overlapping CIDR block, its not going to connect. Transitive Peering is NOT supported, means it always needs one to one peering connection. 

​VPC peering does not support edge to edge routing.
Direct Connect - Available in 10Gbps , 1Gbps, Sub 1Gbps  
A dedicated connection from on prem to AWS, which in many cases can reduce network costs, increase bandwidth throughput, and provide more reliability. 
VPN connection can be configured in minutes and are a good solution for immediate need. 
Security Token Service  
Grants users limited and temporary access to AWS resources. Users can come from three sources. 
Federation - typically active directory
Federation with mobile apps - facebook/ amazon / google 
Cross account Access.
----Key Terms--
Federation - combine or join a list of users in one domain with a list of users in another domain.
Identity Broker - a service that allows you to take an identity from point a and join i to point b.
Identity store - services like active directory, fb, google.
Identites - a user of a service like fb. etc

AWS Security Token service returns , access key, a secret access key , actual token and duration (1 -36hrs).

Active Directory Integration.
Workspaces.
It's basically a VDI, a cloud based replacement for a traditional desktop.Workspaces are persistent, all data on the d drive is backed up every 12 hours. 
Elastic Container Service 
An image is a read only template with instructions for creating a docker container. An image is created from a dockerfile. Images are stored in a Registry, such as docker hub or aws ecr ( amazon ec2 container registry) . ECR supports resource based permissions using aws iam so that specific users or amazon ec2 instance can access repositories and images. 
ECS Task Definition. 
	A Task def. Is required to run docker containers in aws ecs.  It's a test file in json format, used to give instructions, such as how much cpu and memory to use with each container, pass env variables, iam rules the task should use for permissions , etc .
ECS Cluster.
An amazon ecs cluster is a logical grouping of container instances that you can place tasks on. A default cluster is created for you when you use the ecs service for first time. Clusters are region specific, can contain multiple different container instance types, Container instance can only be part of one cluster at a time.
ECS Scheduling.
Service Scheduler:
Ensures that the specified number of tasks are constantly running and reschedules tasks when a task fails.Ensures tasks are registered against an ELB.
Custom Scheduler: 
	Own schedulers that meet business needs. 
ECS Container Agent
	Amazon ECS container agent allows container instances to connect to the ec2 cluster ( linux only).
ECS Security 
ECS tasks use an IAM role to access services and resources. Security group operates at the instance level not task or container level. 
EXAM TIPS
What does a 'Domain" refer to in Amazon SWF?
A collection of related Workflows
How many requests per second can Amazon CloudFront handle?
10,000
54. Which of the following metrics can have a CloudWatch Alarm?
EC2 instance status Check Failed
EC2 CPU utilization
Auto Scaling group CPU utilization
If you want to build your own payments application, then you should take advantage of the richness and flexibility of Amazon AWS DevPay and Amazon AWS FPS
Which of the following approaches provides the lowest cost for Amazon elastic block store snapshots while giving you the ability to fully restore data?
Maintain two snapshots: the original snapshot and the latest incremental snapshot.
You try to enable lifecycle policies on one of the S3 buckets created by you, but you are not able to do so on that particular bucket. What could be the reason? Versioning is not enabled on that bucket.
AWS requires __Amazon Resource Names_ when you need to specify a resource uniquely across all of AWS, such as in IAM policies, Amazon Relational Database Service (Amazon RDS) tags, and API calls.
A __Customer gateway_ is a physical device or software application on your side of the VPN connection.
Which ELB component is responsible for monitoring the Load Balancers? Controller service
You have created a custom configured Amazon instance using Linux, containing all your software and applications. If you want to use the same setup again, what is the best way to do it?
Create an EBS Image (AMI)
When an ELB is setup, what is the best way to route a website’s traffic to it?
Generate a CNAME record for the website pointing to the DNS name of the ELB
What happens to data when an EC2 instance terminates (select multiple if more than one is true)?
For EBS backed AMI, any volume attached other than the OS volume is preserved
All the snapshots of the EBS volume with operating system is preserved
For S3 backed AMI, all the data in the local (ephemeral) hard drive is deleted
EXAM TOPICS
Developer Tools========================================== not exam topic
CodeStar -
Codecommit - source controls
CodeBuild - compile and build
Codedeploy - automate deployment to ec2 instances
CodePipeline -
X-Ray- analyzer
Cloud 9 - Web based IDE.
Management Tools==============================
Cloudwatch =- monitoring service CPU/DISK/Network/Status Check default. RAM Custom Metrics
CloudFormation - way of scripting infrastructure. turning your infrastructure to code (i)
CloudTrail - Logs changes in the AWS env. (i)
CloudTrail can help you track all changes made to your AWS environment by all users in all regions.
Config - monitor config of the entire env. (i)
OpsWorks - to automate the env. similar to elastic bean
Service Catalog - manage catalog of IT service, such as images, op, vpc. used for governance or compliance - not for exam
Systems Manager - not for exam
Trusted Advisor- give advice across multiple displiece, advice on opened port, advice on saving more money, (i)
MAnaged Service - scaling the ec2 service etc.
Media Services===================================== Not service
Elastic Transcoder - resizes the video into different devices.
Media Convert
Analytics ==============================================
Athena =  allows to run sql queries in the s3 bucket - server less.
EMR  - used processing large amount of data. (i)
Cloudsearch - search - not for exam
elasticsearch - search - not for exam
Kinesis - way ingesting large amount of data into aws (i)
QuickSight - BI tool - not for exam.
Data Pipeline - move data b/w diff aws service (i)
Glue - used for ETL.(Extract transform load) not for exam
Security & Identity Compliance =================================
IAM -  (i)
When editing permissions (policies and ACLs), to whom does the concept of the "Owner" refer?
The "Owner" refers to the identity and email address used to create the account AWS account.
Cognito - Device authentication, so cognito is a authentication service that gives temporary access to aws for mobile devices
Guard Duty - not for exam
Inspector - run for vulnerables on ec2 (i)
Macie - scan s3 for PII
Certificate Manager - manage SSL certs
CloudHSM - store public/private keys (i)
Directory Service =- to integrate active directory - not for exam
WAF- monitor user actions for sql injection etc
Shield -  (i)
Artifact - downloading and inspecting amazon documentation not exam.
=======================================
Desktop AS A Service-  No SLA from Amazon - Only Persistent Machines.
=======================================
Windows Server 2008 R2 skinned to Windows 7
Major Players
  Amazon WorkSpaces
  VMware Horizon Daas
  Microsoft RemoteApp
  Citrix Workspace Services
