![[Pasted image 20221101172817.png]]
# Cloudformation

## TLDR
Templates to create [[VPC]]. Allows to create Infrastructre as Code.

## Features
- IaC
- most ressources are supported
- Template versions are stored in [[S3]]

## Cloudformation StackSets
- create stacks in AWS accounts across regions using a single Template
- use the template as the basis for provisioning stakcs
- use with [[AWSOrganisations]]

## Creation Policies
- **`CreationPolicy`** mean a ressource has to be up an running for the next step to continue
### Instance Scheduler
- solution deploy as Cloudformation
- Automatically start/stop your AWS services to reduce costs (up to 70%)
-  Supports EC2 instances, EC2 Auto Scaling Groups, and RDS instances
-  Schedules are managed in a DynamoDB table 
-  Uses resources’ tags and Lambda to stop/start instances 
-  Supports cross -account and cross -region resources