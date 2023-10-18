* for cloud practitioner certification (clf c02)
* https://www.aws.training/Certification
* aws management console https://us-east-2.console.aws.amazon.com/console/home
* other access
  * AWS CLI (command starts with aws)
    * download and use in terminal, or CloudShell - icon in console navbar (uses the credentials you're logged in as; virtual environment - eg cloud files, can upload/download)
    * eg `aws --version`, `aws iam list-users`
    * aws configure > access key > secret access key > region code
  * AWS SDK (set of libraries eg JS, Python, PHP, Java, C++, ...)
# sample questions
* https://d1.awsstatic.com/training-and-certification/docs-cloud-practitioner/AWS-Certified-Cloud-Practitioner_Sample-Questions.pdf
* https://www.udemy.com/course/practice-exams-aws-certified-cloud-practitioner/?couponCode=OCT_23_GET_STARTED
# What is Cloud Computing
## Traditional IT Overview
* server: CPU+RAM, Storage, Database, Network (many servers)
* Network - cables, routers, servers
* Router - data forwarding between networks
* Switch - data forwarding to server
* many servers to meet demand - rent for data center, power, cooling, maintenance, hard to scale, monitor, handle disasters
## Cloud computing
* on-demand delivery of IT resources - eg power, storage, applications
* customized to what you need
* AWS owns and maintains the hardware (their data center)
* eg gmail, dropbox, netflix
* types
  * private cloud - single org, complete control, security, eg provided by rackspace
  * public cloud - owned and operated by a 3rd party, delivered over the internet, eg provided by microsoft azure, google cloud, aws
  * hybrid cloud - some servers on premises, extend some capabilities to the cloud
* 5 characteristics
  * on-demand self service
  * broad network access
  * multi-tenancy and resource pooling
  * rapid elasticity and scalability
  * measured service
* 6 advantages
  * trade capital expense (CAPEX) for operational expense (OPEX)
    * don't own hardware
    * reduce total cost of ownership (TCO) and operational expense (OPEX)
  * benefit from massive economies of scale
  * stop guessing capacity
  * increase speed and agility
  * stop sending money running and maintaining data centers
  * go global in minutes
* s
  * flexible, cost-effective, scalable, elastic, high-availability, fault-tolerant, agile
## Types of Cloud Computing
* Infrastructure as a Service (IaaS)
  * provide networking, computers, storage
  * flexible, easy parallel with traditional
  * eg Amazon EC2
  * eg GCP, Azure, Rackspace, Digital Ocean, Linode
* Platform as a Service (PaaS)
  * removes the need for your organization to manage infrastructure
  * focus on applications
  * eg Elastic BeanStalk
  * eg Heroku, Google App Engine, Windows Azure
* Software as a Service (SaaS)
  * completed product that is run and managed by the service provider
  * eg Rekognition
  * eg Gmail, Dropbox, Zoom
* Serverless - you don't work with servers - Lambda (Function as a Service), S3, DynamoDB, Fargate
* things to manage
  * applications, data, runtime, middleware, os, virtualization, servers, storage, networking
    * traditional: all
    * IaaS: first half, idk
    * PaaS: first 2
    * SaaS: none
* pricing
  * compute time, data storage, data transfer out of the cloud
## AWS Cloud Overview
* launched 2002, market 2004 (SQS), SQS S3 EC2 (2006), dropbox, netflix, airbnb, nasa, mcds, 21st century fox, activision
* 47% market
* use cases
  * build sophisticated, scalable applications
  * enterprise IT, backup/storage, analytics, website hosting, backend for apps, gaming servers
* global
  * regions
    * coded eg us-east-1
    * cluster of data centers
    * most services are region scoped - see [AWS Global Infrastructure > AWS Regional Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)
    * varies by compliance (legality), proximity to customers (latency), available services, pricing 
  * availability zones (AZ)
    * 3-6 per region
    * coded eg us-east-1a
    * one or more data centers
    * each is separated from each other (isolated from disasters) 
  * data centers
  * edge locations / points of presence
    * 400+
## services
* choose region (closer = less latency)
* each service has many features
* global services
  * Identity and Access Management (IAM)
  * Route 53 (DNS service)
  * CloudFront (Content Delivery Network)
  * WAF (Web Application Firewall)
* region scoped services
  * Amazon EC2 (IaaS)
  * Elastic Beanstalk (PaaS)
  * Lambda (Function aaS)
  * Rekognition (SaaS)
## shared responsibility
* customer responsible for security in the cloud
  * customer data
  * platform, applications, identity and access management
  * os, network & firewall config
  * client-side data encryption & data integrity authentication
  * server-side encryption (file system and/or data)
  * networking traffic protection (encryption, integrity, identity)
* aws responsible for the security of the cloud
  * software - compute, storage, database, networking
  * hardware/aws global infrastructure - regions, availability zones, edge locations
* acceptable use policy
  * illegal, harmful, offensive, insecure, network abuse, message abuse
# IAM
* Identity and Access Management
* global
* create users and user groups - used for root account
  * note best to use root account only to set up the AWS account
* sign in to AWS account (account id or alias)
* groups can only contain users
* users can belong to 0-n groups
## policies
* assigned to users (inline) or groups (may inherit from multiple groups)
* JSON document (also can use a visual editor)
  * define permissions, eg on services/features, resources - see access denied or action failed
  * 0+ statements, Effect Allow/Deny, Principal account/user/role, Action API calls or *, Resource or *, Condition
* least privilege principle
* some predefined (AWS managed), can create user-defined - see Policies
## security
* Account Settings > Password Policy - required password pattern, change/expire/reuse
* Profile > Security Credentials > MFA - Multi Factor Authentication
  * password you know + security device you own
  * device:
    * virtual
      * Google Authenticator, Authy, app
      * universal 2nd factor security key (U2F) - physical key, other 3rd party key fobs
  * add and sync device, then added step to sign in process
* access keys - generated through the AWS Console, managed by users
  * eg when protect AWS Management Console with password + MFA, but protect AWS CLI (eg aws configure) and AWS SDK with access keys
  * User > Security Credentials > Create Access Key
* Credential Report - account - credentials metadata
* User > Access Advisor - user - can see service access
## roles
* like a user, can have policies, used by AWS services
* eg EC2 instance, Lambda Function, CloudFormation uses an IAM role to access AWS
## shared responsibility
* you manage and review passwords/mfa/permissions
# Billing Dashboard
* Root Account > Account > IAM user and role access to Billing information > Edit > Activate IAM Access
* IAM User > Billing Dashboard > Bills, Free tier, Budgets, ...
## Cost Management > Budgets
* Create a Budget
* get email cost alerts
# EC2
* Elastic Compute Cloud
* IaaS
* capabilities
  * renting virtual machines (EC2)
  * storing data on virtual drives (EBS)
  * distributing load across machines (ELB)
  * Scaling the services using an auto-scaling group (ASG)
## Instances > Launch Instances
* configure OS
* configure CPU, RAM, storage (EBS, EFS, or EC2), network (choose an instance type - eg t2.micro is part of the AWS free tier)
  * instance types
    * https://aws.amazon.com/ec2/instance-types/ , https://instances.vantage.sh/
    * `instance class` `generation` `.` `size within the instance class`
    * general purpose
      * diversity of workloads
      * balance between compute, memory, networking
      * eg t2.micro
    * compute optimized
      * high performance, dedicated, ...
      * instance class c
    * memory optimized
      * RAM, databases, cache, business intelligence, unstructured data
      * r, x, high
    * storage optimized
      * transaction, databases, cache, data warehousing, distributed file
      * i, t, h
* create a key pair for ssh
* configure other network settings (security)
* configure other storage
* configure EC2 User Data (eg ec2-fundamentals/ec2-user-data.sh)
  * bootstrap
  * run script at forst start
  * updates, software, files, anything
  * runs with the root user
## Instances > Instance
* details, public address (access using this, make sure to use http and not https - may change on each start), private address (stays the same)
* Instance state -> change
  * stopped - server not running, not paying for it
  * terminated - lose all settings, state, etc.
## Network & Security > Security Groups
* allow traffic in/out
* use IP or other security groups
* security group / firewall containing 1+ EC2 instances
  * also, an instance can belong to 1+ security groups
* connection succeeds/times out
* locked down to a region/VPC combo
* good to have a separate one just for SSH
* default: all inbound blocked, all outbound authorised
* ports
  * 22 - eg allow visiting address from Windows PowerShell - TCP 22
    * SSH - log into a Linux instance
    * SFTP - upload files using SSH
  * 21 - FTP - upload files into a file share
  * 80 - HTTP - access unsecured websites - eg allow visiting address from laptop - TCP 80
  * 443 - HTTPS - access secured websites
  * 3389 - RDP - log into a Windows instance
  * can choose a type, defined protocol-port pair
  * source
* ec2 instances purchasing options
  * On-Demand Instances - short, pay by sec, highest cost
  * Reserved - long, specific type, flexible payment/buy sell - 1 or 3 years
    * Convertible Reserved - long + different types
  * Savings - long, commit to type/amount of usage, family, region, otherwise flexible
  * Spot - short, cheap, can lose instances, defined max price, most cost-efficient, must be resilient to failure
  * Dedicated Hosts - physical server, control instance placement - complience requirements - licenses like socket, core, etc. - on demand or reserved, most expensive, lower level visibility
  * Dedicated Instances - no shared hardware with other accounts
  * Capacity Reservations - any duration, on demand whether or not instances are run, no discounts, specific AZ
## SSH
* EC2 Instance Connect - web browser, amazon x2
  * Instances > Instance > Connect button > EC2 Instance Connect
  * uses ssh - eg uploads a temporary ssh key, needs the security group
* PuTTy
* SSH - CLI utility (eg Windows PowerShell or Command Prompt)
  * `ssh -i KEYFILENAME.pem ec2-user@PUBLICIV4ADDRESS`
    * key file
    * properties > security > advanced > owner is you, disable inheritance, select a principal, full permissions, ?
  * `exit`
### commands
* `aws` commands
  * many commands require access:
    * DO NOT aws configure - you'll be entering it into the EC2 instance - anyone who accesses the instance can access the code
    * DO instances > instance > Actions > Security > Modify IAM Role
      * view at Instances > Instance > Security > IAM Role
## shared responsibility
* you're responsible for security groups, os, software, iam, data security
# EC2 Storage
## Elastic Block Store > Volumes
* or Instances > instance > Storage > Block devices 
* EBS
* storage option for EC2 instances
* Elastic Block Store Volumes
* network drives you can attach to your instances while they run - like a USB but not physical, uses network - some latency
* persist data after instance termination, can be deleted on termination (eg root by default)
* mounted to 0-1 instance at a time - can be detached and reattached (note 1 instance can have multiple EBSs attached)
* bound to 1 availability zone
* specific capacity and speed
* Actions > Attach Instance, Delete Volume, Create Snapshot
## Elastic Block Store > Snapshot
* backup of an EBS volume
* recommended (but not necessary) to first detach (clean)
* use to restore, or copy across AZ or region
* EBS Snapshot Archive
  * storage tier - archive tier - 75% cheaper
  * takes 24-72 hours for restoring the archive
* Recycle Bin for EBS Snapshots
  * can be set up, specify retention
* right click > Copy snapshot > choose destination region
* Actions > Create volume from snapshot > ..., can pick AZ
* Actions > Delete snapshot > may go to recycle bin > Resources (and can recover), if rule was created
* Recycle Bin > Retention Rules, Resources
## Images (AMI)
* Amazon Machine Image
* customization of an EC2 instance
  * software, config, os, monitoring, ...
  * faster boot / config - all software is pre-packaged
* built for a specific region, and can be copied across regions
* launch from a Public AMI (AWS provided) or your own (you make and maintain) or an AWS marketplace AMI (someone else makes and potentially sells)
* process (from an EC2 instance)
  * start an EC2 instance and customize it - Launch Instance
  * stop the instance (for data integrity)
  * build an AMI - this will also create EBS snapshots - Instances > instance > right click > Image and Templates > Create Image
  * launch instances from other AMIs (any region) - Images > AMIs > instance > Launch instance from AMI or Instances > Launch Instance > My AMIs (userdata - run after ami userdata - eg this one include comments and file creation)
### EC2 Image Builder
* automated, can be run on a schedule, free service
* process
  * EC2 Image Builder
  * Builder EC2 Instance
    * apply software
  * create new AMI
  * auto test EC2 Instance
  * ami is distributed, can be multiple regions
## EC2 Instance Store
* hardware disk directly attached to the EC2 Instance physical server
* better IO performance
* lose their storage if they're stoped (ephemeral) (or if hardware fails)
* eg buffer, cache, scratch data, temporary content
* your responsibility to backup and replicate
## Elastic File System
* managed Network File System
* can be mounted on hundreds of EC2 instances at a time (in sync)
* works with Linux EC2 instances in multi-AZ
* pay per use
* highly available, scalable, expensive
* in a security group
### EFS-IA
* Infrequent Access
* storage class that is cost-optimized for files not accessed often
* when enabled, files automatically moved based on lifecycle policy
* transparent to the applications - application does not need to know
## shared responsibility
* aws replicates data, make sure it's safe, and secure
* you're responsible for setting up backup/snapshots, data encryption, understanding the risks
## Amazon FSx
* 3rd party file system
* Windows File Server
  * supports protocols like SMB and Windows NTFS
  * integrated with Microsoft Active Directory
* Lustre
  * for high performance computing
  * Linux, cluster
# ELB and ASG
* scalability - larger load
  * vertical - increase the size - common for non-distributed
  * horizontal - increase the number - must be distributed - ELB and ASG
* availability
  * 2+ AZs - in case of disaster - ELB and ASG
* elasticity - auto-scaling based on the load (eg on demand, optimize)
* agility - fast
## ELB
* load balancer: server (single point of access, high availability) that forwards traffic to multiple servers (backend EC2 instances)
* Elastic Load Balancer
* aws manages, guarantees, take care of upgrades/maintenance/etc.
  * more expensive but a lot easier than setting up your own
* 4 types
  * application load balancer - layer 7
    * HTTP / HTTPS / gRPC protocols
    * HTTP Routing features
    * static DNS (URL)
  * network load balancer - layer 4
    * TCP / UDP protocols
    * ultra high performance
    * static IP through elastic IP
  * gateway load balancer - layer 3
    * GENEVE Protocol on IP packets
    * route traffic to firewalls that you manage (back to load balancer, then to application)
    * intrusion detection
  * classic load balancer (retired 2023) - layer 4 and 7
* EC2 > Load Balancing > Load Balancers > Create ...
  * security group: allow HTTP traffic from anywhere
  * target group: includes the downstream EC2 instances
  * visit through load balancer DNS name - will load from one of the healthy instances in the target group
## ASG
* auto scaling group
* scale in and out to match the changing load (add/remove EC2 instances)
  * maintain min/max/desired number of machines running
  * keep load balancer updated with registered machines
  * replace unhealthy instances
* cost savings - optimal capacity
* EC2 > Auto Scaling > Auto Scaling Groups
  * info about instances to create
  * attach to a load balancer / target group
  * enable health check
* can see in Instances, Target Groups
### auto scaling
* manual - ie desired
* dynamic
  * simple/step - eg CPU % triggers
  * target tracking - average CPU
  * scheduled - eg time triggers
* predictive - machine learning to predict traffic, provision in advance
# S3
* infinitely scaling storage (backup, archive)
* can use to host websites, application, media, ...
* global service, regional buckets
* bucket
  * globally unique name
  * created in a region
  * stores objects
  * create, upload, add folder
* objects
  * have a key (full path, including object name) - not really a directory
  * value content - max 5000GB, upload 5GB each
  * metadata, tags, version
  * open (URL includes credentials), object URL (public)
## Security
* eg access object url content, access static website without 403 forbidden error
* user-based: IAM - only my account
* resource-based
  * S3 bucket rules
    * Bucket > Permissions > Block public access (highest priority, can be set at account level), Bucket policy (Action GetObject, BucketARN/*)
  * access control list (ACL)
    * bucket (most common) or object
  * JSON based policies
    * resources, effect (allow/deny), actions (API), principal (account/user)
    * besides access, can also force encrypt at upload
* access if IAM allows or resource allows and there's no expicit DENY
* encryption keys
## static website hosting
* Bucket > Properties > Static website hosting > (html file name - should be in bucket) , link
## Versioning
* enabled at bucket level
  * files not versioned prior to enabling: version = null
  * suspending versioning does not delete previous versions
* upload object with same key = overwrite, new version
* can restore, roll back
* Bucket > Properties > Bucket Versioning OR when you Create Bucket
* Bucket > Objects > Show versions and delete a versioned object = permanently delete
* Bucket > Objects > DO NOT Show versions and delete = adds a delete marker
  * same object, new version = delete marker - ie delete marker can be deleted, but while it's the most recent version, the file will be treated as if it does not exist
## Replication
* 2 buckets
  * versioning must be enabled in both - version IDs are also replicated exactly
  * can be different accounts
  * asynchronous copying
  * S3 needs IAM permissions (read and write buckets)
* Source Bucket > Management > Replication Rules
  * Source scope all objects, Destination bucket name, Create new IAM Role, just new or (also previous objects is a different feature)
* cross or same region - CRR (eg compliance, lower latency access, replication across accounts), SRR (eg log aggregation, live replication between production and test accounts)
## Storage Classes
* Bucket > Upload > Properties > Storage class OR Bucket > Object > Properties > Storage class
* Bucket > Management > Lifecycle rules
  * scope all objects
  * storage class, days after creation
* object has a storage class - can set on creation, modify (manually or using S3 Lifecycle config)
* durability - not lost, same for all storage classes
* availability - readily available (time wise)
* Storage Classes
  * Standard - General Purpose - frequently accessed, low latency, high throughput, can sustain 2 concurrent facility failures
    * eg big data analytics, applications, content distribution
  * Infrequent Access - infrequently accessed, rapid access time, less available, minimum 30 days
    * Standard - Infrequent Access  (eg disaster recovery, backups)
    * One Zone - Infrequent Access - only 1 AZ (eg secondary backup copies)
  * Glacier - low cost, archiving/backup, pay for storage + retrieval 
    * Glacier Instant Retrieval - ms, minimum 90 days, less available
    * Glacier Flexible Retrieval - min/few hrs/many hrs, minimum 90 days
    * Glacier Deep Archive - 12/48 hrs, minimum 180 days
  * Intelligent Tiering - monitoring/auto-tiering fees, no retrieval charges, less available
    * frequent access, infrequent access, archive instant access, archive access, deep archive access
## encryption
* server-side - default
* client-side - encrypt before uploading
## shared responsibility
* aws durability, sustain loss, ...
* you're responsible for versioning, bucket policies, replications, logging/monitoring, storage classes, data encryption at rest and in transit
# AWS Snow Family
* highly secure, portable device
* use cases
  * collect and process data at the edge
    * process data while it's being created on an edge location - limited internet, computing power
    * preprocess, machine elarning, transcoding streams
  * migrate data into and out of AWS - most common
    * connectivity, bandwidth, network cost
    * physical offline devices to load data onto (using client AWS OpsHub), send to plug into infrastructure, import/export to an S3 bucket, then gets wiped
* Snowcone (data migration and edge computing) < 8 TB
  * snowcone and snowcone ssd (bigger)
  * smaller
  * provide your own battery/cable
  * can use AWS DataSync
  * wired or wireless, usb or battery
  * can run EC2 Instances and AWS Lambda Functions and can use for 1-3 years
* Snowball Edge (data migration and edge computing) < 10 PBs
  * data transfers
  * storage optimized or compute optimized
  * large data cloud migrations, DC decomission, disaster recovery
  * can run EC2 Instances and AWS Lambda Functions and can use for 1-3 years
* Snowmobile (data migration)
  * truck
  * huge
  * temperature controlled, GPS, 24/7 video
# Storage Gateway
* for hybrid cloud
  * because might require on data, things might take too long, etc.
  * S3 is proprietary, Storage gateway bridges on-premises to cloud data
# Databases
* note EFS, EBS, EC2 Instance Store, S3 is all on disks
* Relational Databases, using SQL
* NoSQL / non-relational Databases - flexible, scalable, high-0performance, highly functional - eg JSON
* shared responsibility when aws manages different databases
  * aws provisions, makes available, allows scaling, backups/restores, provides operations and upgrades, and handles OS, monitors, alerts
  * storage backed by EBS
  * can't SSH into instances
* EC2 instances reads/writes from a database
## RDS
* SQL
* used for Online Transaction Processing (OLTP) like RDS
* AWS managed databases - engines
  * Postgres, MySQL, MariaDB, Oracle, Microsoft SQL Server, Aurora (AWS Proprietary database - supports PostgreSQL and MySQL, higher performance, costs more)
  * storage autoscaling
* security group
* port
* Databases
* Snapshots
  * Take from database, Restore to new database, Copy to new location snapshot, Share to new account snapshot
* Read Replica - copy of database (up to 15) that application can also read from
  * can be in another region - cost for data transfer
  * only write to main DB
* Multi-AZ
  * Failover in case of AZ outage
  * copy of database in other AZ, if main fails, triggers use of failover
## ElastiCache
* managed Redis or Memcached
* in-memory databases (high performance, low latency)
* reduce load for read intensive
* eg EC2 instance would read/write from both RDS and ElastiCache
## DynamoDB
* NoSQL, partition key -> item with key/value, cannot link separate tables
* distributed serverless database - create Table, create Item in table
* for massive workloads, standard or infrequent access, specialized in-memory cache: DynamoDB (DAX)
* single digit millisecond latency
* integrated with IAM
* Global Tables - synced copies in multiple regions, can read/write to anyt - active/active replication
## RedShift
* based on PostgreSQL
* Online Analytical Processing (OLAP) - analytics and data warehousing, integrate with BI tools eg Quicksight or Tableau
* load data once every hour, pay per instance
* columnar storage (not row based)
* Massively Parallel Query Execution (MPP) engine, using SQL queries
## EMR
* Elastic MapReduce
* creates/manages Hadoop clusters (of up to hundreds of EC2 instances)
* supports Big Data tools - ApacheSpark, HBase, Presto, Flink, ...
* integrated with spot instances
## Athena
* serverless query service to analyze S3 objects (CSV, JSON, ORC, Avro, Parquet - built on Presto), eg logs/trails
* SQL
* pay $5 per TB scanned (eg cheaper if columnar)
## QuickSight
* interactive dashboards from databases, per-session pricing
## DocumentDB
* NoSQL, AWS implementation of MongoDB - JSON data
## Neptune
* graph database
## QLDB
* centralized, verifiable Quantum Ledger Database
* review history of changes to data (eg financial transactions) - cannot remove/modify
* can use SQL
## Amazon Managed Blockchain
* decentralized blockchain network
* compatible with HyperLedger Fabric and Ehetereum
## Glue
* Extract, Transform, Load (ETL) service - serverless pre-processing (eg prepare for Redshift)
* Glue Data Catalog - eg used by Athena, Redshift, EMR to build schemas
## DMS
* Database Migration Service
* EC2 instance running DMS creates a database from a source database (can be different types)
# Other Compute Services
## Docker
* software development platform to deploy apps
* apps are packaged in containers that can be run on any OS
* eg same instance has many dockers running different types of things
* hub.docker.com
* Docker images stored in Docker Repositories
* many containers per docker - ie no separate OS
## ECS
* Elastic Container Service - launch dockers on appropriate EC2 instances
* you provision and maintain infrastructure (EC2 instances)
* AWS starts/stops containers, integrates with ALB
## Fargate
* Fargate - launch dockers serverless-ly - using CPU/RAM
* AWS starts/stops containers, integrates with ALB
## ECR
* Elastic Container Registry
* store Docker images that will be launched/run on ECS/Fargate as a container
## Lambda
* manage virtual functions, not servers
* shorter executions, running on-demand (event-driven), automated scaling
* can monitor and get more resources
* Node.js, Python, Java, C#, Golang, C# Powershell, Ruby, Custom Runtime API
* Lambda Container Image, but must implement Lambda Runtime API, less preferred
* triggered by some event, performs an action eg add to database, upload file, ...
* priced based on calls + duration
* Create Function
  * response, function logs (cloudwatch)
  * Configuration - memory, timeout, role
  * Monitor - metrics, cloudwatch logs
* not by itself publically exposed
* 15min time limit, limited languages, limited storage
## API Gateway
* create a serverless HTTP API, can expose Lambda functions to a client end user
## Batch
* batch job - starts and ends
* dynamically launches EC2 instances or Spot instances
* you just submit or schedule jobs
* AWS Batch provisions resources
* jobs are defined as Docker images and run on ECS, focus less on infrastructure
* creates EC2/Spot instance
* no time limit
## Lightsail
* virtual servers, storage, databases, networking
* simple, low/predictable pricing, for people with little cloud experience
* monitoring
* use cases
  * simple web applications
  * dev/test environment
* no auto-scaling, limited integrations
* 
