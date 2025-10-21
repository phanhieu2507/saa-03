# Amazon Redshift
- use sql to query
- base on Postgresql not oltp => olap and dataware house
- petabyte Scale Data warehouse
- large scale data storage and analysis
- collumnar ( relative data into a region) store data, paralel query => fast 
- load data to redshift => large are better ( kinesis > s3 copy > ec2 JDBC)
## Cluster
- leader node:  distribute the work
- compute node: excute the work 
- provision mode: reder a mount of compute node => alway charge
## mode
- serverless: pay when have people use
- provisioned: 
### Snapshot
- some Redshift cluster have multiAZ 
- snapshot: auto snap, manual
- can auto copy to another region
- store in s3


## Spectrum
- attach S3 without the data being transfered to Redshift => query data without loading it
- must have redshift cluster to run
- still need redshift cluster
- 
![[Screenshot 2025-10-13 at 11.25.27.png]]![[Screenshot 2025-10-13 at 15.40.07.png]]
enhanced VPC routing: using SG, ACL, VPC endpoint. Customized networking

![[Screenshot 2025-10-13 at 15.44.16.png]]
snapshot is incremental
![[Screenshot 2025-10-13 at 15.48.42.png]]