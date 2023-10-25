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
* weighted routing policy: route 53 chooses which IP address to return based on health
* Latency Routing Policy: route 53 chooses which IP address to return based on latency
* failover routing policy: route 53 chooses which IP address to return based on whether the primary is healthy
## CloudFront
* CDN
* replicate parts to edge locations, + cache
## S3 Transfer Acceleration
## Global Accelerator
