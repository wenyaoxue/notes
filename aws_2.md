# Scale
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
* lots of languages, and dockers
* health monitoring
