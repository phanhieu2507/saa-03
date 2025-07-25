![[Pasted image 20221101114116.png]]
# Route 53

## TLDR
AWS Nameserver and Domain Name register Service.

#### DNS Terminologies
- Domain Registrar: Amazon Route 53, GoDaddy, …
- DNS Records: A, AAAA, CNAME, NS, …
- Zone File: contains DNS records
- Name Server: resolves DNS queries (Authoritative or Non-Authoritative)
- Top Level Domain (TLD): .com, .us, .in, .gov, .org, …
- Second Level Domain (SLD): amazon.com, google.com, …
## Features
- managed
- scalable
- Authoritative dns (can be updated by customer)
- registar ( can register own names)
- 100% availabilty
- health checks


## DNS Record
- domain name
- record Type
- value (ip) ( destination)
- routing policy
- ttl ( time to live)

### Record types

#### A
- hostname to ipv4

#### AAAA
- hostname to ipv6

#### CNAME: 
- hostname to hostname, can not target to  root domain ( cái mà mua ở nhà mạng)
- maps dns querys to another domain or subdomain
- AAAA
- CNAME
- NS

#### Alias
- can target a root domain (cname can not)
- hostname to aws resource
- can only be used for aws ressources
- ttl not mandatory
##### NS: Name server
#### Hosted zone
- container of dns record
####  TTL time to live
- can set up high and low ( high -> down traffic to Route53)
## Endpoint types

### Outbound
- used by ressources in [[VPC]] to resolve dns querys to ressources outside of the [[VPC]]  (e.g. on premise)

## Inbound
- used by ressources outside of aws to resolve name to ressources inside a [[VPC]]

## Routing Policies
Define how Route 53 responds to DNS queries
#### Simple
- Singlevalue
- Multivalue: random value choosen
#### Weighted
- split traffic % to a % to b ( 0% not traffic to)

#### Latency based
- route to record with least latency for user
#### Geolocation 
- base on location, traffic to nearest
- must defind default
- can be accociate with health check
#### Geopromixity
- base on location , and resourse bias
- bias value: -99 -> 99
#### IP based routing 

#### Multi value
- return multi value
- can not change elb

### Health check
- only for public resource
- 15 global healthcheck ( consider healthy or not >18% )
- can check by first 5120 bytes of the response
### 3 rd party 
- If you buy your domain on a 3rd party registrar, you can still use Route 53 as the DNS Service provider