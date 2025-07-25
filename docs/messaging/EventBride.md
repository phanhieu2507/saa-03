![[Pasted image 20221101205129.png]]
# EventBride

## TLDR
Central message service with the most amount of targets. Is used by aws behind the scenes a lot

## Features
- schedule (cron jobs)
- event pattern (email when root user logs in)
- json format ( immutable)
- can archive events
- replay archived events
- event json is typed, can be nice for custom code/lambda
- have rule for filter event to target

## Sources
- [[EC2]]
- Code Build
- [[S3]]
- [[TrustedAdvisor]]
- [[CloudTrail]] (any API call)
- schedule (cron)
- 3rd Party
- ...

## Targets
- [[Lambda]]
- [[Batch]]
- [[ECS]]
- [[SQS]]
- [[SNS]]
- [[StepFunction]]
- pipelines
- [[Kinesis]]
- [[SSM]]
- 3rd Party
- ...
## Event Buses
- supports resource based policies
- can allow events from other accounts

### Default
- AWS Services

### Partner Event bus
- supported 3rd party events

### Custom Event Bus
- for custom apps
### SchemaRegistry
1. register schema for event (event is json)
2. event come -> know what schema of event -> download suitable schema from code biding to handle
- 3 type: default: schema of aws service, custom, discover: auto discover when the event come (total 5)
### Resource base policy
- same as S3 bucket policy but use on Event Bridge
- define who can access into bus, which event can come to the bus ( even in a different account, different region). 
- use case: aggregate all event into one event bus
-