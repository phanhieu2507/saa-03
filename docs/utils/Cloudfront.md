# CloudFront
- CDN
- data, videos, application and apis delivery
- global
- regional edge caches
- only http based requests
- intergate with [[AWSShield]] and DDOS protection
- 

## Origins

### [[S3]]
- caching
- distributing
- enhanced security with (OAC) Origin Access Control
- Cloudfront can be upload point to S3

### Custom Endpoint
- [[ELB]] ALB
- [[EC2]]
- [[S3]] Website
- Any HTTP backend
#### CloudFront vs S3 region replication
1. Cloud Front: suitable for static data can access over the world
2. S3 region replication: suitable for dynamic data need low latency in some region 

## Geo Restirction
- whitelist countries: allow
- blacklist coutries: deny
- use for copyright laws

## Price Classes
- depends on data transfer, but is different for each edge location
- price goes down if you transfer more data

### All
- all regions - best performance - highest price

### 200
- most regions - exludes most exp

### 100
- only cheapest regions 

## Cache Invalidations
- invalide via api and path
- can choose all (* ) or by path ( images/ *)
- 

###  unicast vs anycast
- unicast: one server- one ip 
- any cast: many server- oneip => routed to nearest one
## Customization at Edge
- serverless
- customize a cdn endpoint
- pay per use

### Use cases
- Website security and privacy
- seo
- intelligent route
- bot mitigation
- real time image transform
- a/b testing
- Dynmaic Web Apps at Edge
- User prio
- tracking ad analytics
- user auth 

### Cloudfront Edge function
- code attached to cloudfront distributions
- runs closer to users for min latency
- lightweight written in js
- high scale latency senstive cns customisations
- sub ms startuptimes
- managed in cloudfront
- millions of request per second

#### Price
- Free tier available
- 1/5 of [[Lambda]] @Edge

#### Use cases
- cache key normalisation (transform request attributes)
- header manipulation
- url rewrites and rediect
- validate jwt tokens

### [[Lambda]] at Edge
- nodeJs or python
- 1ks of request per second
- can change every part of the request (viewer and origin)

#### Price
- no free tier

#### Use cases
- loner exec time
- adjustible cpu memory
- code depends on 3rd party (AWS CLI)
- Network access
- File System Access
- Http Body Access

## Availability
- can setup origin failover
- an origin group may have a primary and a secondary origin