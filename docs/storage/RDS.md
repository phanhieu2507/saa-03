![[Pasted image 20221101124548.png]]
# RDS

## TLDR
- db service
- Various  relational databases, manged by aws. (postgres, mysql, microsoft mysql server, oracle, aurora, ibm db2)
- use sql query language

## Features
- scaling capacity (up to set maximum storage, every 6h max, 5 mins needs to be low storage which is less than 10% remaining) this needs to be enabled.
- os patching
- no ssh
- monitoring dashboards
- Maintenance windows for upgrades
- multi az ( disaster recovery)
- scaling capability

## Read replicas
- up to 15 read replicas (Within AZ, Cross AZ or Cross Region)
- eventually async replication
- can be promoted to their own database
- no cross az network cost
- cross region cost per network traffic
- can be multi AZ
- use case: report analytics

## Multi AZ
- can be upgraded without downtime
- one dns name
- automatic failover to standby database by switching target ip of dns name
- sync replication ( bản gốc và bản sao giống hệt nhau tại mọi thời điểm)
- one db will be standby
- automated backups will be multi region
- zero downtime ( create snapshot -> move to another region (create new db from snapshot) -> sync data)

## RDS Custom
- only for oracle and microsoft ssql
- access to underlying database and os
- ssh possible
- de active automation mode and take snapshot before modify

## Security
- if you need encrypt in transit use ssl/tls by launching the client with the --ssl_ca flag
- can use [[KMS]] to encrypt data at rest

### Option

#### RDS Custom for Oracle
- alllows customisation to host and os

## Maintenance
- maintenence causes downtime even if the db is multi AZ

## Backups
- daily full backup during maintence window
- transactions logs are backed up by rds every 5 mins
- restory any point in time (5 mins aago)
- 1 to 35 days of retention
- if multi az backups span multi region

### Manual Snapshot
- manual trigger
- retention as log as you want

### Savings
- take snapshot and delete database
- if you want rds back just restore with snapshot

### Restore
- restore mysql rds database from [[S3]]

## Security
- encrypt at rest with [[KMS]], must be defined at launch time
- if master is not encrypted, read replicas can not be encrypted
- to change from unencrypt and to encypt use snapshot
- encrypt in flight with tls root certificates client side
- can use [[IAM]] roles to connect to database instead of username and pw
- can use [[SecurityGroup]]
- audit logs can be enabled and be send to [[CloudWatch]]


## RDS Proxy
- fully manged database proxy 
- allows apps to pool and share connection established with the database which allows less connections to database
- improves database performance
- severless
- autoscalling
- high available (multi az)
- reduces rds and aurora failover time by 66%
- enforces iam auth for db and store credentials in aws secrets manager 
- RDS Proxy is never public and can only be used from within the vpc

## Enhanced Monitoring
[[CloudWatch]] feature for RDS
- RDS child processes
- RDS processes
- OS Processes
