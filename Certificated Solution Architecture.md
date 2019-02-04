##AWS Certificated Solution Architecture - Associate
###IAM(Identity Access Management)
IAM allows you to manage users and their level of access to the AWS console.		
It is important to understand IAM and how it works, both for the exam and for administrating a company's AWS account in real life.		
<font color="red">IAM feature</font>:		
1. Centralised control of your AWS account	
2. Shared Access to your AWS account	
3. Granular Permissions		
4. Identity Federation(Active Directory, Facebook)	
5. Multifactor Authentication	
6. Provide temporary access for users/devices and services where necessary	
7. Allows you to set up your own password rotation policy	
8. Integrates with many different AWS service	
9. Support PCI DSS Compliance	
######Role, User, Group, Policy

###S3(Simple Storage Service)
S3 provide developers and IT team with secure, durable, highly-scalable object storage. Amazon S3 is easy to use, with a simple web services interface to store and retrieve any amount of data from anywhere on the web.	
<font color="red">S3 Basic idea</font>:		
1. Object based		
2. Files can be from 0 - 5 TB	
3. There is unlimited storage	
4. File are stored in Buckets	
5. S3 is a universal namespace. Unique globally!	
6. https://s3-eu-west-1.amazonaws.com/bucketsname	
7. When you upload a fileto S3, you will receive a HTTP 200 code if upload was successful.	
<font color="blue">S3 - Storage Tiers/Class</font>	
1. S3 Standard	
2. S3 - IA(Infrequently Accessed)		
3. S3 One Zone - IA: lower cost		
4. Glacier: very cheap


###EC2(Amazon Elastic Compute Cloud)
Amazon Elastic Compute Cloud(Amazon EC2) is a web service that provides resizable compute capacity in the cloud. Amazon EC2 reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change.
######On-Demand Reserved Spot Dedicated-Hosts

<font color="red">EC2 Instance Types</font>:		
FIGHT DR MC PX	
1. F1 for FPGA	
2. I3 for IOPS	
3. G3 - Graphics		
4. H1 - High Disk Throughput		
5. T2 cheap general purpose (think T2 micro)		
6. D2 for Density		
7. R4 for RAM	
8. M5 - Main choice for general purpose apps		
9. C5 for Compute	
10. P3 - Graphics (think Pics)	
11. X1 - Extreme Memory		
<font color="blue">My understanding</font>: EC2 is virtual server while <b><em>EBS</em></b>(Elastic Block Storage) is virtual disk	
<b>IOPS</b>: input output per second	
<font color="blue">EBS Volume Types</font>:		
1. General Purpose SSD(GP2): 3 IOPS - 1000 IOPS can have 3000 at 3334 GiB and above		
2. Provisioned IOPS SSD(IO1): large relational or NoSQL database, more than 10000 IOPS, can provision up to 20000 IOPS per volume	
3. Throughput Optimized HDD(ST1): big data, can't be a boot volume	
4. Cold HDD(SC1): lowest cost storage for infrequently accessed workloads, can't be a boot volume	
5. Magnetic(Standard): lowest cost for all bootable EBS, data accessed infrequently.

RAID array: Redundant Array of Independent Disks	
<font color="red"><b>AMI</font></b>: Amazon Machine Image	
Snapshots of encrypted volumes are encrypted automatically.		
Volumes restored from encrypted snapshots are encrypted automatically	
You can share snapshots, but only if they are unencrypted. these snapshots can be shared with other AWS accounts or made public. 

ELB: Load Balancer	
Health Check	

<font color="red">EC2 Placement Group</font>:	
当使用置放群组的时候，AWS会将置放群组中的实例尽可能的启动在同一台物理主机上，以获得实例之间的低延迟行网络连接。	
当置放群组中的某个实例停止后，一旦重新启动，它仍然属于该置放群组，不过由于在重启实例的时候，该实例可能会在别的物理主机上启动，从而和别的实例相分离，所以当置放群组中的实例出现问题，或者是由于容量不足不能启动实例的时候，最好把该置放群组中的所有实例都停止，并且重新启动所有实例，这样能最大程度保证置放群组中的实例都是启动在同一台物理主机上。同时最好所有的实例类型都相同，保证实例指尖的高网络性能。<b>置放群组的名称在同一账户中必须是唯一的</b>；不同的置放群组不能合并在一起；不能将现有的已经启动的实例移动到置放群组中。		
置放群组是同一可用区中的多个EC2实例组成的逻辑分组，置放群组不可以跨可用区	
1. Clustered Placement Group!!!		
2. Spread Placement Group

1. A clustered placement group can't span multiple AZs.
2. A spread placement can.
3. The name you specify for a placement group must be  unique within your AWS account.
4. Only certain types of instances can be launched in a placement group.(Compute Optimize, GPU, Memory Optimized, Storage Optimized).
5. AWS recommend homogenous instance within placement group.
6. You can't merge placement group.
7. You can't move an existing instance into a placement group. You can create an AMI from your existing instance, and then launch a new instance from that AMI into placement group.

EFS
VPC:Amazon Virtual Private Cloud

###Route53	
Routing Policy	
1. Simple routing policy	
2. Weighted routing policy	
3. Latency routing policy	
4. Failover routing policy	
5. Geolocation routing policy	
6. Multivalue Answer routing policy

###Database 101

###VPC(Virtual Private Cloud)
think it as virtual data centre
one subnet can only in one AZ 
one region can have only one internet gateway

one subnet can only be associated with one ACL

Endpoint gateway can implement private的subnet connect internet without NAT gateway
（NAT gateway can implement private subnet connect into internet)	
only private subnet can have endpoint

###Important Concept
<font color="red">SQS</font>(pull-based system): Web service gives you access to message queue that can be used to store message while waiting for computer to process them.	
1. Standard Queue	
2. FIFO Queue	
Long pulling: polls the queue periodically and only returns a reponse when a message is in the queue or  the timeout is reached.( retrive message - save money)
Short polling: return immediately even if no message is in the queue.	
<font color="red">SWF</font>(simple workflow service): is a web service that makes it easy to coordinate work across distributed application components.	 (keep track of the task)		
Workers: are programs that interact with amazon swf to get	task, process received tasks, and return the result.	
Deciders: is a program that controls coordination of  tasks, i.e. their ordering, concurrency, and scheduling according to the application logic.	
#####<font color="blue">The task is assigned only once and is never duplicated.</font>

<font color="red">SNS</font>(simple notification service): is a web service that makes it easy to set up, operate, and send notifications from the cloud. it provides developers with a highly scalable, flexible, and cost-effective capability to publish messages from an application and immediately deliver them to subscribers or other applications.		
<b>SNS subscribers</b>: HTTP, HTTPS, Email, Email-JSON, SQS, Application, Lambda
######SNS is pushed
elastic transcoder -> convert media file to some specific file for device

###Kinesis
Kinesis is a platform on AWS to send your streamming data.
Kinesis Streams, Kinesis Firehose, Kinesis Analytics


###Well Architected Framework
Pillar one: security
	
	1. Data protection(encrypt your data both in 
	   transit and at rest using ELB, EBS, S3, RDS)
	2. Privilege management(IAM,MFA)
	3. Infrastructure protection(VPC,real life cctv)
	4. Detective controls(AWS Cloud Trail-capturing 
	   and analyze AWS logs, AWS Config, Amazon Cloud Watch)
Pillar two: Reliability		
	Reliability:	
	
	1. Foundation(IAM,VPC)
	2. Change management(AWS CloudTrail)
	3. Failure management(AWS CloudFormation)
Pillar three: Performance efficiency	
	
	1. Compute
	2. Storage
	3. Datebase
	4. Space-time Trade-off
Pillar four: Cost Optimazation

	1. Matched supply and demand(Autoscaling) 
	2. Cost-effective resources(EC2 - reserved instances)
	3. Expenditure awareness(CloudWatch alarm, SNS)
	4. Optimizing over time	(AWS blog, AWS Trusted Advisor)
Pillar five: Operational excellence

	1. Perform operations with code
	2. Align operations processes to business objectives
	3. Make regular, small, incremental changes
	4. Test for responses to unexpected events
	5. Learn from operational events and failures
	6. Keep operations procedures current
	
	preparation, operation, responses
	
	
###Q&A

1. The default backup retention period is one day if you create the DB instance using the Amazon RDS API or the AWS CLI, or seven days if you create the DB instance using the AWS Console.
2. If an Amazon EBS volume is the root device of an instance, can I detach it without stopping the instance? NO.
additional EBS volume can
3. Can I move a reserved instance from one region to another? no
4. In RDS, changes to the backup window take effect. Immediately
5. In RDS what is the maximum size for a Microsoft SQL Server DB Instance with SQL Server Express edition? 10GB per Database

<pre>
ForceFailover
When true, the reboot is conducted through a MultiAZ 
failover.	
Constraint: You can't specify true if the instance is
 not configured for MultiAZ.	
Type: Boolean	
Required: No</pre>

6. You can conduct your own vulnerability scans within your own VPC without alerting AWS first? False
7. Reserved instances are available for multi-AZ deployments.
8. If an Amazon EBS volume is an additional partition (ie not the root volume) , can I detach it without stopping the instance? but take sometime
9. You can  not RDP or SSH in to an RDS instance to see what is going on with the operating system.
10. When creating a new security group, all in bound traffic is allowed by default. <b><em>false</em></b>
 outbound is allowed by default
11. What are the four levels of AWS premium support?
	basic, developer, business, enterprise
12. As the AWS platform is PCI DSS 1.0 compliant, I can immediately deploy a website to it that can take and store credit card details. I do not need to get any kind of delta accredditaion from a QSA. <b><em>false</em></b>
13. <font color="red">The service to allow Big Data Processing on the AWS platform is known as AWS "Elastic Big Data". </font><b><em>false</em></b>
14. <font color="blue">Individual instances are provisioned in AZ</font>
15. What is the underlying Hypervisor for EC2? Xen
16. The AWS platform is certified PCI DSS 1.0 compliant
17. The AWS platform consists of how many regions currently? 14
18. How many copies of my data does RDS - Aurora store by default? 6
19. Amazon's product debut conference is held in Las Vegas each year and is known as <font color="red">re-invent</font>

<font color="green">What is the difference between Elastic Beanstalk & CloudFormation?
Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, auto-scaling to application health monitoring based on the code you upload to it, while CloudFormation is an automated provisioning engine designed to deploy entire cloud environment via a JSON script.</font>


1. What is the maximum response time for a Business Level Premium Support Case? 1 hour
2. Auditing user access/API calls etc across the entire AWS estate can be achieved by using; CloudTrail
3. You can add multiple volumes to an EC2 instance and then create your own RAID 5/RAID 10/RAID 0 configurations using those volumes.
4. <font color="blue">Using SAML (Security Assertion Markup Language 2.0) you can give your federated users single sign-on (SSO) access to the AWS Management Console.</font>
5. When you create new subnets within a custom VPC, by default they can communicate with each other, across availability zones.
6. It is possible to transfer a reserved instance from one Availability Zone to another.
7. Amazon's Redshift uses which block size for its columnar storage? 1024kb
8. for all new AWS accounts there is a soft limits of 20 EC2 instances per region
9. With which AWS orchestration service can you implement Chef recipes? Opsworks
10. DynamoDB is automatically redundant across multiple availability zones.
11. AWS help provide protection against some forms of traditional network attacks. Which of the following is protected against by AWS?  port scanning, IP spoofing man in the middle attack
12. Auto Scaling is a tool used to create fault-tolerant and cost-effective architectures.
13. Gateway-Cached volumes retain a copy of frequently accessed data subsets locally. Cached volumes offer a substantial cost savings on primary storage and minimize the need to scale your storage on-premises.
14. With NAT instances, the most common oversight is forgetting to disable Source/Destination Checks. then can do update thing
15. With SQS, you must implement your own application-level tracking, especially if your application uses multiple queues.
16. SQS long polling doesn’t return a response until a message arrives in the queue, reducing your overall cost over time. Short polling WILL return empty responses.
17. Proactive Cyclic Scaling allows you to scale during the desired time window.
18. Route53 has a security feature that prevents internal DNS from being read by external sources. The work around is to create a EC2 hosted DNS instance that does zone transfers from the internal DNS, and allows itself to be queried by external servers.
19. Poor timing of SQS processes can significantly impact the cost effectiveness of the solution.
20. AWS does not copy launch permissions, user-defined tags, or Amazon S3 bucket permissions from the source AMI to the new AMI.
21. DynamoDB allows for the storage of large text and binary objects, but there is a limit of 400 KB.

