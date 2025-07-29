# NAT
- used in a public vpc subnet to enable instances in private subnet output ipv4 traffic to the internet
- supports ACLs
- supports flow logs
## Nat Instance
- dedicated ec2 instance
- port forwarding
- can be used as bastion host
- supports SG attachment
## Nat Gateway
- aws service
- higher availabilty
- higher bandwith
- less ops needed
- only use by instance from another subnet
- no SCG needed
- can use elastic IP
- 1 AZ

