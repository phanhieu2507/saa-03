![[Pasted image 20221101210837.png]]
# Amazon Aurora

## TLDR
AWS Created custom DB tech, very high performance. Useful for global and serverless relational database applications.

## Features
- not open source
- MySQL and Postgre
- global
- self healing
- fault tolerant
- autoscaling up to 64 TB per instance
- is a cluster
- multi az
- each az has a copy of the cluster
- 5x faster than mysql
- 3x fast than postgre
- up to 15 replicas
- faster replication
- 20% more cost than [[RDS]]
- restore to any point in time

## Primary DB
- read and write
- only one per cluster
- if fails a replica will be promoted

## Aurora Replica
- same storage as primary
- multiple per az possible
- only read
- reader endpoint does load balancing
- can enable replica autoscaling

## Custom Endpoints
- subset of aurora instances as custom endpoint(e.g. larger instance type for analytical queries)
- after set custom end point not to read by reader endpoint

## Aurora Serverless
- automated db instantiation and autoscaling
- for unpredictable workloads
- pay per second
- client talks to aurora proxy fleet

## Aurora multi master
- all nodes are read write nodes there is no master
- replication between all nodes
- use for imediate failover

## Global Aurora Database
- 1 primary region for read an write
- up to 5 secondary read regions
- up to 16 read replicas for each read region
- less than 1 second for replication across region (RTO < 1minute)

## Aurora machine learing
- ML based predications to your apps via SQL

### Use cases
- fraud detection
- add targeting
- sentiment analysis
- product recommendations

### Services
- [[SageMaker]]
- [[Comprehend]]
#### Babelfish
- 1 con cá biết dịch
- only for aurora postgre sql ( not for my sql)
- allow aurora postgre sql understan mycrosoft sql server language
- application code not change too much

## Backups

### Automated 
- 1 to 35 days
- can not be disabled
- point in time recovery in that timeframe

### Manual
- triggered by user
- keep as long as user wants

### Restore
- into new database

### Cloning
- create a new aurora cluster from a existing one
- faster than snapshot & restore
- cost effective
- useful to create staging
#### Security
- at rest using [[kms]]
- inflight
- [[IAM]]
- no ssh
- [[SecurityGroup]]
- can audit log
