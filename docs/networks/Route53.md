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


Cantrill

 hosted zone are database which are referenced via delegation using name server record
 
 ![[Screenshot 2025-09-23 at 12.43.04.png]]![[Screenshot 2025-09-23 at 12.44.22.png]]![[Screenshot 2025-09-23 at 12.48.23.png]]![[Screenshot 2025-09-23 at 13.03.51.png]]![[Screenshot 2025-09-23 at 13.05.23.png
 vpc must be accociated with the private zone
 ![[Screenshot 2025-09-23 at 13.08.35.png]]
 same domain name , public is a subset
CNAME and ALIAS
![[Screenshot 2025-09-23 at 13.16.14.png]]![[Screenshot 2025-09-23 at 13.28.53.png]]

single routing![[Screenshot 2025-09-23 at 14.04.51.png]]

health check
![[Screenshot 2025-09-23 at 14.07.52.png]]

failover routing
![[Screenshot 2025-09-23 at 14.15.16.png]]

multi routing
active active
multi service, return random, ![[Screenshot 2025-09-23 at 14.19.44.png]]

weighted routing
testing new soft ware versions
repeated until a healthy record is chosen
![[Screenshot 2025-09-23 at 15.41.58.png]]

latency based routing:
have a latency table
![[Screenshot 2025-09-23 at 15.42.54.png]]

geolocation routing
when create record => tag location ( country, continent )
return relevant record, check the state -> country -> continent -> default
use to restrict content
![[Screenshot 2025-09-23 at 15.57.33.png]]

geppromixity
as close as possible, base on distance
routing is distance based including bias, make the resource larger

![[Screenshot 2025-09-23 at 16.04.18.png]]

interoperability : kha nang tuong tac
![[Screenshot 2025-09-23 at 16.08.11.png]]![[Screenshot 2025-09-23 at 16.10.23.png]]![[Screenshot 2025-09-23 at 16.13.20.png]]![[Screenshot 2025-09-23 at 16.16.22.png]]

DNSSEC with route 53
