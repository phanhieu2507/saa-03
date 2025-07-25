# Systems Manager Parameter Store
- secure storage for configuration and secrets
- optional encryption using kms
- serverless
- easy sdk
- version tracking
- configuration management using iam and path
- notifications with amazon event bridge
- cloudformation support
## Path
- prod/db/pw e.g.

## Cost

### Standard
- Storage up to 10k parameter free
- max size 4k
- no policies
- higher throughput for api (up to 1k per sec) cost 5 cent per 10k calls

### Advances
- Storage up to 100k
- max size 8kb
- policies can be used
- 0.05 cent per parameter per month
- thoughput the same as standard

## Policies
- assign TTL to a paramter ( force delete sensitive data)
- multi policy possible
- notification possible