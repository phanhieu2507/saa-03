
# AWS Global Accelerator

![[Pasted image 20221101170746.png]]
## TLDR
UDP compatible global endpoint to speed up network traffic to application by using edge locations and aws private network.

## Features
- network layer service
- distribute traffic to optimal endpoints over AWS Network
- two static anycast ip adresses as fixed entrypoints
- Global service
- can use weights to distribute portion of traffic
- good fit for non http use cases
- good fit for http use cases use static ip
- Good for HTTP use cases that required deterministic, fast regional failover


## Targets
- [[ELB]] ALB
- [[ELB]] NLB
- Elastic IP
- [[EC2]]

## Health Checks
- failover less than 1 min unhealty
- good dissater recovery

## Security
- only 2 external ips need to be whitelisted - any cast
- ddos protect by aws shied


### [[Cloudfront]] vs [[GlobalAccelerator]]
- cloudfront :  cache, image, video, .... application layer (7)
- global accelerator: no cache, game, tcp,udp, .. networklayer, 2 any cast ip