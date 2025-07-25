![[Pasted image 20221101171725.png]]
# Web Application Firewall
- protection against layer 7 exploits (http)

## Deploy Targets
- ALB [[ELB]]
- [[APIGateway]]
- [[Cloudfront]]
- AppSync GraphQL API
- [[Cognito]] User Pool

## Web Access Controller
- up to 10k ips per set/rule
- http header
- http body
- uri strings
- size constraints
- geo matching ( block contries)
- rate based rules ( ddos)
- rules are region, for [[Cloudfront]] they are global