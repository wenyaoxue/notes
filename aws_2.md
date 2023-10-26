# Manage
## CloudFormation
* outline your AWS infrastructure resources, CloudFormation will create and configure correctly/in-order
* manage infrastructure through code
* easy to destroy and re-create, generate diagrams, understand costs
* Stack - using a template .yaml, can also update/delete
* you can see the resources in their own consoles
## CDK
* Cloud Development Kit - create CloudFormation template in a language like JS, TS, Python, Java, .Net
## Elastic BeanStalk
* developer centric view
* one view to manage EC2, ASG, ELB, RDS, ...
* Platform as a Service
* you're just responsible for application code
* 3 architecture models
  * single instance - good for dev
  * LB + ASG - production/pre-production web applications
  * ASG only - non-web apps in production
* some languages, and docker
* health monitoring
* Create application - environment, platform, code, preset configurations, role
* creates CloudFormation stacks
* see Domain link
## Code services
* CodeDeploy - hybrid - works with existing EC2 instances and on-premises servers, for automatic deployment, upgrading servers
* CodeCommit - analogous to GitHub: repositories, collaborate, versioned
* CodeBuild - compile (eg code from CodeCommit), run tests -> packages (artifact) ready to be deployed to servers
* CodePipeline - define CICD eg CodeCommit -> CodeBuild -> CodeDeploy -> Elastic Beanstalk
* CodeArtifact - artifact management system/infrastructure - store and retrieve code dependencies, software packages
* Cloud9 - cloud IDE, collaborate, uses CloudFormation, git push to CodeCommit
* CodeStar - manage above services + Elastic Beanstalk, CloudFormation, S3 in one place; uses a service role and EC2 instance to create a Project
## Systems Manager (SSM)
* hybrid - manage existing EC2 and on-premises systems at scale - fleet
* auto-patching, run commands across many servers, parameter store
* install SSM agent onto systems (installed by default on some AMI)
  * permission SSMManagedInstanceCore
* Session Manager - SSH without access (closed port, eg no inbound allowed), bastion hosts, keys - better security, log save
* Parameter Store - secure, eg API keys, passwords, configuration, access based on IAM, version tracking, optional encryption
## OpsWorks
* managed Chef & Puppet (eg existing templates) in the cloud (3rd party services to manage EC2 and On-Premises)
* alternative to SSM, but for standard AWS resources - EC2 Instances, Databases, LB, EBS
* stack: load balancer, application server, database
# Global
* regions, availability zones, points of presence
* decreased latency, disaster recovery, defense against attacks
## Route 53
* DNS, closest deployment
* map link to address: A - IPv4, AAAA - IPv6, another link - CNAME, aws resources - alias
* communicates with browser to respond with the ip
* simple routing policy: no health checks
* weighted routing policy: route 53 chooses which IP address to return based on health/specs
* Latency Routing Policy: route 53 chooses which IP address to return based on latency
* failover routing policy: route 53 chooses which IP address to return based on whether the primary is healthy
* register a domain, create EC2 instances in different regions that allow HTTP traffic, hosted zones create record (www, instance address, region, policy)
## CloudFront
* CDN
* replicate parts/cache to edge locations/Points of Presence (216) - users communicate with edge locations all around the world
* protection
* origin - some domain, S3 or HTTP (ALB, EC2, S3 website, ...)
* origin access control
  * eg instead of making bucket public, provides bucket policy to allow CloudFront to access (must update in S3)
  * ingress(upload) - 
* distribution - of objects
* uses WAF and Shield to protect
## S3 Transfer Acceleration
* transfer file to a bucket (bucket is region scoped) that is far away (upload, download)
* transfers to edge location, then uses internal private AWS network to transfer to bucket
## Global Accelerator
* availability and performance
* use 2 static anycast IP to connect to edge location, then uses internal private AWS network to route to server
## Outposts
* server racks that offers AWS infrastructure/services/etc on premises, can migrate to the cloud
* you are responsible for physical security
## WaveLength
* zones, infrastructure deployments embedded within telecommunications providers' datacenters at the edge of the 5G networks
* WaveLength Zone is on telecom carrier 5G network, connected to parent aws region, deploy services to zone
## Local Zones
* extend your VPC to more locations, extension of an AWS Region
* enable, in addition to az
* EC2 settings, zones, use new subnet select as an AZ ? when launching instance
# integrations
* synchronous or asynchronous (event-based) communications
* asynchronous decouples, less risk, more independent - SQS queue, SNS pubsub, Kinesis streaming
## SQS
* Simple Queue Service
* Standard Queue, FIFO Queue
* send message (limitless, but retained for x days), poll for / retrieve and then delete messages (body)
## Kinesis
* real-time big data streaming
* collect, process, analyze
* many sources, SQL, ML, into AWS services
## SNS
* Simple Notification Service
* send one message to many receivers
* Topic receives message (from publisher) and sends to eg many services (to all subscribers, eg SQ, lambda, kinesis, emails, sms notifs, http endpoint)
## MQ
* traditional applications with other protocols, eg MQTT, AMQP, STOMP, Openwire, WSS
* managed message broker service for RabbitMQ, ActiveMQ
* doesn't scale as much, runs on servers, has queue and topic features
# Monitoring
## CloudWatch
* metrics for every service, variable, timestamp, dashboard
* alarms - configure with time and metric, publish message to SNS topic
  * EC2 instance Alarm Status - creates CloudWatch alarm - eg action Recover, Reboot
  * billing alarm: only in us-east-1
* log - can collect from Beanstalk, ECS, Lambda print/exception statements, CloudTrail, EC2 machines or on-premises servers with the CloudWatch Log Agent installed and IAM permissions, Route53
* eg EC2 (CPU, status, network) EBS (reads wrotes), S3 (size, number, requests), billing (est charge), service limits
## EventBridge
* source - eg based on time, based on service event type like sign in
* destination - eg trigger script, send SNS topic
* event rule/schema (can disable/delete), bus, archive
## CloudTrail
* governance, compliance, audit
* enabled by default
* history of events / API calls - any activity
* can send to CloudWatch or S3
* Insights - automated analysis
## X-Ray
* visualize architecture - distributed tracing, services, troubleshooting, SLA's, bottlenecks
## CodeGuru
* ML
* Reviewer - automated code reviews and recommendations, Java, Python, GitHub, CodeCommit, ...
* Profiler - visibility/recommendations about performance during runtime/production, CPU, costs, memory, anomaly detection
## Health Dashboard
* Service History - all regions, all services, historical
* Your Account - alerts and remediation guidance when AWS is experiencing events that may impact you (what you're using)
* relevant and timely, aggregate data, event-resources
* Global service, outages, bell Event Log
# VPC & Networking
* Virtual Private Cloud, logically isolated portion of AWS
## VPC, Subnets, Internet Gateways, NAT Gateways - all VPC features
* AWS creates a default VPC for you
* IP - IPv4 (public, private, keep during unattached/stopped with Elastic IP), IPv6 (public only)
* VPC - private network, region-scoped, range of IPs (CIDR)
* Subnet - private or public (has a route to the gateway), part of VPC, AZ-scoped, range of IPs (CIDR)
* Route Tables - define access to the internet and between subnets: to get to y, use x
* Internet Gateways and NAT Gateways - something in the VPC, connects to subnet to allow Internet to access subnet (Internet) or allow subnet to get info from the internet (NAT, eg for private)
* whenever you're choosing a network, subet
## Security Groups, Network ACL, VPC Flow Logs
* NACL - firewall which controls traffic from and to a subnet, ALLOW and DENY IP addresses, stateless
* Security Groups - firewall which controls traffic from and to an ENI (elastic Network interface) or EC2 instance, ALLOW IP addresses or other security groups, stateful
* VPC, Subnet, and Elastic Network interface Flow Logs
  * check connectivity
## VPC Peering, VPC Endpoints
* VPC peering - connect 2 VPCs (no overlapping CIDR), establish 1 connection at a time
* VPC Endpoints - connect to service using a private network instead of public www network - better security and lower latency, subnet using a VPC Endpoint Gateway (S3 and DynamoDB) or Interface
## PrivateLink, VPC Endpoint Services
* expose a service to thousands of VPCs directly and privately
* Amazon Marketplace Vendor's VPC -> Network Load Balancer <- AWS Private Link-> Elastic Network Interface -> my VPC
## Site to Site VPN and Direct Connect
* Site to Site VPN - on-premises VPN -> customer gateway <-Site to Site VPN-> Virtual Private Gateway -> AWS VPC through encrypted public internet connection
* Direct Connect (DX) - connect an on-premises VPN to AWS VPC through physical connection private network, private secure and fast when established
## Client VPN
* connect from your computer using OpenVPN to your private network in AWS and on-premises
* private IP, as if you were in the private VPC network, connect to your EC2 instances
* computer with OpenVPN connects to AWS VPC over the public internet
## Transit Gateway
* transitive peering between thousands of VPC and on-premises, hub-and-spoke (star) connection
* one single gateway, allows everything to be connected to each other
* Direct Connect, VPN, onpremises, ...
# Security & Compliance
* DDoS - Distributed Denial of Service Attack - send lots of requests
## AWS Shield
* Standard - enabled for all users, protection from layer 3/4 attacks, SYN/UDP, Reflection
* Advanced 24/7, more sophisticated attacks against specific services, response team
* eg on Route 53, on CloudFront, Load Balancer
## WAF - Web Application Firewall set rules, protection from layer 7 (HTTP), eg on ALB, API Gateway, CLoudFront
* WACL Web Access Control List
  * IP addresses, HTTP headers, body, URI strings, SQL injection, Cross Site Scripting, size, geo match, count occurrences (rate-based)
## CloudFront, Route 53, Load Balancer, Scaling - edge
## AWS Network Firewall
* protect entire VPC, layer 3 to 7
* any traffic direction
## Penetration Testing
* allowed without approval for 8 services: EC2, NAT Gateways, ELB, RDS, CloudFront, Aurora, API Gateways, Lambda, Lightsail, Elastic Beanstalk
* except DNS zone, Dos, DDos, ..., port/protocol/request flooding
## Encryption
* at rest and in transit, or both - encryption keys
* KMS Key Management Service - user decides who can access encryption keys
* CloudHSM Hardware Security Module - user manages encryption keys
### CMK Customer Master Keys
* Customer managed: create, manage, use, enable/disable, define rotation policy or bring your own
* AWS managed: AWS creates, manages, and uses (eg through AWS services)
* AWS owned: across multiple accounts, you can't view the keys
* CloudHSM Keys - generated from CloudHSM hardware device
* for EBS, S3, Redshift, RDS, EFS, CloudTrail (auto), Storage Gateway
