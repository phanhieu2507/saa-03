# On Premise options
- download amzon Linux 2 AMI as VM
## VM Import/Export
- migrate existing applications into ec2
- create a DR repository stragegy for your on premise vms
- can export back from ec2 to on premise
## AWS Application Discovery Suite
- Gather Information about your on premise server to plan migration
- server utilzation and dependecy mappings
- track with AWS Migration Hub
## AWS SMS Server migration service
- incremental replication of on premise live servers to AWS
### AWS DMS
can not be migrate between 2 on premise
![[Screenshot 2025-09-28 at 7.27.23.png]]
task move the source to the des endpoint
![[Screenshot 2025-09-28 at 7.32.56.png]]
no downtime migration : choose DMS
![[Screenshot 2025-09-28 at 7.36.31.png]]

migration is using over internet![[Screenshot 2025-09-28 at 7.40.40.png]]