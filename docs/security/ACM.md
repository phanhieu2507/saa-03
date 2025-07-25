# AWS Certificate Manager

- used for SSL TLS certificate managedment provision and deploy
- provide inflight encryption
- public and private certs
- automatic renewal
- cannot be used on ec2
- will take a few hours to be verified
- can imported but no automatic renewal
- certificate for cloudfront must be in us-east-1
- for api gateway certificate region needs to be  created in same region

## Integrations
- [[ELB]]
- [[Cloudfront]]
- [[APIGateway]]

## Options
- FQDN
- Wildcard

### Valiation Method
- DNS validation
- Email validation

## Exp Check
- Daily Expiration Events to Event Bride
- [[AWSConfig]] acm-certifacte-expiration-check
