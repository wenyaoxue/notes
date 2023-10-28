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
* DDoS only
## WAF - Web Application Firewall set rules, protection from layer 7 (HTTP), eg on ALB, API Gateway, CLoudFront
* WACL Web Access Control List
  * IP addresses, HTTP headers, body, URI strings, SQL injection, Cross Site Scripting, size, geo match, count occurrences (rate-based)
## CloudFront, Route 53, Load Balancer, Scaling - edge
## Network Firewall
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
## AWS Certificate Manager (ACM)
* loads SSL/TLS Certificates onto ALB/CloudFront Distrubutions/API Gateway APIs
* in-flight encryption for websites, enableshttps
## Secrets Manager
* store and rotate
* generate using Lambda
* integrate with RDS - mainly
* encrypted using KMS
* name, key/value
## Artifact
* Global, AWS compliance documentation and agreements
* Reports, auditors, ...
* Agreemenents - BAA, HIPAA
## GuardDuty
* Intelligent Threat Discovery
* machine learning
* input: cloudtrail events logs, vpc flow logs, dns logs, optional features
* can setup to trigger EventBridge which -> lambda or SNS
* dedicated finding for cryptocurrency
## Inspector
* automated security assessments/analyses/identification, when needed, vulnerabilities, risk score
* for ec2 instances, container images push to Amazon ECR, lambda functions
* reporting and integration with AWS security hub
* can send findings to EventBridge
## Config
* auditing and recording compliance
* evaluate and record specific rules (configurations) and its changes over time (+ CloudTrail link) across relevant resources, eg check access
* region-scoped, can be aggregated
* can store to S3 to analyze by Athena, can send to SNS Topic
* not free
## Macie
* data security and data privacy service
* machine learning and pattern matching to discover and protect your sensitive data
* identify and alert you to sensitive data, such as personally identifiable information
* analyze S3 and notify EventBridge
## Security Hub
* manage security and automate checks across accounts
* auto aggregates above services into one hub, must enable Config
* goes to EventBridge, Amazon Detective, Security Hub findings
## Amazon Detective
* quick deep analysis to find root cause
## can contact abuse team if you suspect prohibited behavior
## root user has complete access, only one who can change account settings (close, support plan, restore IAM), register as a seller, some S3 stuff, sign up for GovCloud
## IAM access analyzer
* which resources are shared externally
* define zone of trust, finding = access from outside, + archive or archive rules/actions for intended/not intended
# Machine Learning
* Rekognition - objects, people, text, and scenes in images and videos
* Transcribe - speech to text using Automatic Speech Recognition, incl language, automatically remove PII
* Polly - text to speech
* Translate
* Lex - similar to Alexa, speech recognition, natural language understanding, chatbots/call center bots
* Connect - receive calls, create contact flows, cloud-based contact center
* eg connect -> Lex -> Lambda
* Comprehend - NLP
* SageMaker - used to build ML models
* Forecast - timeseries + features ->
* Kendra - builds a knowledge index, document search service
* Personalize - similar to Amazon.com, personalized recommendations
* Textract - text, handwriting, data from scanned documents
# AWS Organizations
* Global service
* master/management and children accounts
  * benefits: consolidated billing, aggregated usage pricing, pooling of EC2 instances
  * API: automatically create accounts
  * invitation
* send logs to a central account
* eg one account, vpc per dept/project/environment
* Structured with Organization Units and Accounts
* Service Control Policies
  * whitelist or blacklist IAM actions attached at the OU or Account level, does not apply to master account
  * applied to all users/roles of the account, including Root
  * does not affect service linked roles
  * by default all DENY
  * disable services, or force compliance
  * inherited, Deny overrides Authorize
* Backup policies, Tag policies, AI services opt-out policies
## Control Tower
* set up multi-account environment, secure, compliant, best practices, automate
* runs on top of Organizations
* OUs, accounts, guardrails, users
## Resource Access Manager
* share resources with any other account (avoid duplication)
* eg VPC
## Service Catalog
* pre-authorized products predefined by admins (another user)
* CloudFormation Templates in a Portfolio + control
## Pricing models
* pay as you go, save when you reserve, pay less by using more, pay less as AWS grows
* pay for what you use
* savings: commit some amount
## Billing and Costing Tools
* Compute Optimizer - optimal amount of resources
* Pricing Calculator - estimate, + service/configuration
* Billing Dashboard - month-to-date, by service, free tier, forecast
* Billing Dashboard > Cost Allocation Tags - create excel sheet based on tag categories; tagged resources using Resource Groups & Tag Editor
* Billing Dashboard > Cost and Usage Reports - per service per hour, most granular
* Billing Dashboard > Cost Explorer - analyze at high level, total costs and usage across accounts, hourresource info as well, + savings plan, + forecast
* Billing Alarms - stored in CloudWatch, actual
* Budgets - Usage, Cost, Reservation, Savings Plans, SNS, lots of filters, actual and forecasted
* Cost Anomaly Detection - uses ML, report + root-cause analysis, alerts or summary
* Service Quotas - alert limits, request quota increase
## Trusted Advisor - account assessment
* analysis+recommendations on 5 categories: Cost Optimization, Performance, Security, Fault Tolerance, Service Limits
* basic/developer Support plan - 7 core checks: S3 Bucket Permissions, Security Groups, IAM Use, MFA on Root Account, EBS Public Snapshots, RDS Public Snapshots, Service Limits
* business/enterprise support plan - full checks, set alarms, support API
## Support Plans
* Basic - free, customer service, documentation
* Developer - business hours email to Cloud Support Associates
* Business - 24/7 phone, email, chat to cloud support engineers, additional fee for infrastructure event management, production response times
* Enterprise On-Ramp - business critical, Technical Account Managers, Concierge Support Team, Infrastructure event management, well-architected & operations Reviews, business critical system response time
* Enterprise - designated Technical Account Manager, business critical 15 minute response time
# Advanced Identity
## STS Security Token Service
* temporary, limited-privileges credentials
* used for eg IAM roles, or external access
## Cognito
* identity for web/mobile applications users (potentially millions)
* database of users
## Directory Services
* managed Microsoft Active Directory (AD) - database of objects, centralized security, credentials for machines connected to domain controller
* manage users, supports MFA, establish trust connections with on-premises AD
* AD Connector - redirect to on-premise AD
* Simple AD - cannot be joined with AD
## IAM Identity Center
* single sign-on -> links to all AWS accounts in AWS Organizations, Business cloud applications, SAML apps, EC2 Windows instances
* built in identity store, or connect to a 3rd party eg AD, OneLogin, Okta, ...
# Other AWS Services
* WorkSpaces - Desktop As a Service, provision Windows or Linux desktop, cloud VDI, deployed in an AZ
* AppStream 2.0 - Desktop Application Streaming Service, deliver app from within a web browser, can configure instance type
* IoT Core - Internet of Things - connect IoT devices to the cloud, messages
* Elastic Transcoder - convert media files
* AppSync - store/sync data for your application, uses GraphQL, auto generate client code, integrations with dynamo DB and lambda, subscriptions, data synchronization, security, can be used by amplify
* Amplify - set of tools for full stack web/mobile applications; configures the backend
* Device Farm - test against real browsers, mobile devices, tablets - devices you can configure
* Backup - manage and automate data backup, retention periods, lifecycle, policies, regions
* Disaster Recovery - backup and restore is cheapest, pilot light core functions/minimal setup is ready, warm standby full app at minimum size is ready, multi-site/hot-site full app at full size is ready
* Elastic Disaster Recovery, DRS - recover physical, virtual, and cloud-based servers, continuous replication using a Replication Agent, minutes failover, then failback
* DataSync - move data from on-premises to AWS - replicates first full load, and then incremenetal
* Application Discovery Service - gather info about on-premises data centers, data and dependency, plan for migration
	* using Agentless Discovery Connector or Application Discovery Agent, results in Migration Hub
* Application Migration Service (MGN) - lift-and-shift, rehost, simplify migrating applications, continuous replication using a Replication Agent , aupports lots of things, minimal downtime
* DMS Database Migration Service
* Migration Evaluator - Agentless Collector for discovery, take a snapshot, analyze current and define target state, develop plan
* Migration Hub - inventory data for assessment, planning, and tracking of migrations, has Orchestrator feature for templates
* Fault Injection Simulator - for chaos engineering, experiment template, disrupt resources, + results
* Step Functions - visual workflow of Lambda functions - sequence, parallel, conditions, timeouts, error handling, can integrate with other services, can implement human approval feature
* Ground Station - for satellite communications/operations, provides a global network, download and send/process data
* Pinpoint - 2-way marketing message/reply: email, SMS, push, voice, in-app messaging, can segment/personalize, scalable: templates/schedules/campaigns (unlike SNS and SES)
# AWS Architecting & Ecosystem
## Principles
* auto scale instead of guess
* test at production scale
* automate
* allow evolution
* data-informed
* improve
* 6 Design Principles - scalable, disposable, automated, loosely coupled, service-based
* 6 pillars - operational excellence (good, manageable code), security (identity, tracing, encryption), reliability (scaling, recovery), performance efficiency (make use of new services/technologies), cost optimized (resources you need, awareness), sustainable (environmental impact, energy efficiency)
## Well-Architected Tool - review pillars or other metrics, like a survey
## Cloud Adoption Framework - white paper, help you develop a comprehensive plan
* 6 perspectives, each with a set aof capabilities: Business, People (bridge between technology and business), Governance, Platform, Security, Operations
* 4 Transformation Domains - Technology, Process, Organization, Product
* 4 Transformation Phases - Envision, Align, Launch, Scale
## Right sizing, start small, elastic, lowest possible cost
## Resources - Blogs, Forums, Whitepapers, Guides, Quick Starts, Solutions, Knowledge Center
## Marketplace
## Training (Digital, Private, Cert for US Govt or Enterprise), Academy
## Professional Services & Partner Network (APN) - Technology, Consulting, Training, may have Competencies, can become better through Navigate Program
## IQ - contractors (Experts), give secure access to account
## re:Post - forum, Q&A, premium answered by AWS Support engineers
## Managed Services (AMS) - team of experts, manage and operate your infrastructure, handles common activities, implement best practices and maintains your stuff
# Prepare
