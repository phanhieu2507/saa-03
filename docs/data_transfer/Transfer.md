![[Pasted image 20221031111028.png]]
# Transfer Family

## TLDR
FTP Server in AWS with additional file processing.

## Features 
- managed infrastructure
- price per provisoned endpoint per hour + tranfers in GBs
- store and manage creds in [[Transfer]]
- integrate with other auth systems ([[Cognito]], Ldap, [[AWSAD]], MS AD ...)
- protocol 
	1. ftp: file tranfer protocol
	2. ftps: file tranfer protocol with ssl
	3. sftp: secure file tranfer

## Use Cases
- ERP
- Public Data
- CRM

## Targets
- [[S3]]
- [[EFS]]