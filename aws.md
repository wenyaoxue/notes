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
