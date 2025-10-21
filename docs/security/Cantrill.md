
KMS
regional & public service: every region is isolated when using KMS
![[Screenshot 2025-09-12 at 21.02.51.png]]![[Screenshot 2025-09-13 at 6.40.27.png]]

permisstion to encrypt, decrypt, create key is different
kms key never leave the kms product
no point that kms store in plaintext form on the disk

![[Screenshot 2025-09-13 at 10.42.41.png]]Data encryption keys
kms doesn't store the dek in any way
you or service do the encryption and decryption of your data, kms just provide the plaintext version key ( after that discard it) and the ciphertext version key ( you and service save in the disk )
service like s3 generate dek for each of obj upload to s3

![[Screenshot 2025-09-13 at 10.55.54.png]]


key concepts:
can not extract the kms key, all be done using api to kms
backing key: data encrupted with old véion can still be decrypted
alias  is per region


![[Screenshot 2025-09-13 at 14.49.43.png]]

key policies and security

key policy (resource) : only on the key
need to grand access to the account want to managed the key

![[Screenshot 2025-09-13 at 14.58.04.png]![[Screenshot 2025-09-13 at 14.58.16.png]]

kms practise
need to specify who manage the key ( role, user)
need to specify who can cryptography the key ( encrypt, decrypt), in this can specify in another account ( role , user)

AWS Systems Manager Parameter Store
save ciphertext using kms
![[Screenshot 2025-09-21 at 17.02.04.png]]
public service
![[Screenshot 2025-09-21 at 17.06.07.png]]
System and application logging on ec2
can not natively capture data in an instance=> cloudwatch agent ( software running insde the instance )
![[Screenshot 2025-09-23 at 8.53.07.png]]![[Screenshot 2025-09-23 at 8.55.40.png]]
can use parameter store to store the configuration
sudo dnf install amazon-cloudwatch-agent to download the cloudwatch agent
role need: ssm full access, cloudwatch agent server policy

ec2 placement group
pps : packet per second
![[Screenshot 2025-09-23 at 9.44.02.png]]![[Screenshot 2025-09-23 at 9.59.06.png]]

![[Screenshot 2025-09-23 at 10.19.49.png]]
7 instance per AZ
![[Screenshot 2025-09-23 at 10.20.39.png]]![[Screenshot 2025-09-23 at 10.22.51.png]]
huge scale parallel processing systems
![[Screenshot 2025-09-23 at 10.28.27.png]]

ec2 đeicated hosts
![[Screenshot 2025-09-23 at 12.07.02.png]]![[Screenshot 2025-09-23 at 12.08.22.png]]![[Screenshot 2025-09-23 at 12.09.01.png]]![[Screenshot 2025-09-23 at 12.12.46.png]]

Enhanced Networking & EBS Optimized
![[Screenshot 2025-09-23 at 12.18.38.png]]![[Screenshot 2025-09-23 at 12.35.34.png]]

AWS Secrets Manager
![[Screenshot 2025-10-11 at 20.45.59.png]]![[Screenshot 2025-10-11 at 20.58.21.png]]

AWS WAF
![[Screenshot 2025-10-12 at 12.09.46.png]]![[Screenshot 2025-10-12 at 12.21.28.png]]
can not accociate cloudfront webacl with an other regional service
![[Screenshot 2025-10-12 at 12.27.41.png]] 
 with rate base rule only have block, count , and captcha
 label are internal to waf only, can be referenced from other rule
 label not stopping processcing 
 ![[Screenshot 2025-10-12 at 12.41.01.png]]
aws shield

![[Screenshot 2025-10-12 at 12.48.57.png]]![[Screenshot 2025-10-12 at 13.47.13.png]]![[Screenshot 2025-10-12 at 13.51.46.png]]
can use to protec group of resource
![[Screenshot 2025-10-12 at 13.58.23.png]]

CloudHSM
HSM: hardware security model
![[Screenshot 2025-10-12 at 14.04.34.png]]
HSM is not HA, need to create a cluster
Client need to install in ec2 to use hsm

![[Screenshot 2025-10-12 at 14.10.43.png]]
![[Screenshot 2025-10-12 at 14.15.14.png]]
utilize industry standard encryption API => choose cloud HSM
AWS Config
![[Screenshot 2025-10-12 at 14.23.20.png]]![[Screenshot 2025-10-12 at 14.27.46.png]]
AWS Macie
![[Screenshot 2025-10-12 at 16.08.56.png]]![[Screenshot 2025-10-12 at 16.10.57.png]]![[Screenshot 2025-10-12 at 16.13.24.png]]![[Screenshot 2025-10-12 at 16.17.50.png]]
classification of data within s3 => marcie


Amazone Inspector
deviations: độ lệch
security report => inspector
![[Screenshot 2025-10-12 at 16.36.34.png]]
need agent for more information
![[Screenshot 2025-10-12 at 16.38.21.png]]![[Screenshot 2025-10-12 at 16.41.18.png]]

AWS Guarduty
support multiple account 
![[Screenshot 2025-10-12 at 16.48.02.png]]![[Screenshot 2025-10-12 at 16.49.10.png]]