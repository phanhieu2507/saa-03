# AWS Key Managed Service
- create and manage cryptographic keys
- control use of keys
- FIPS 140-2 valid
- used for ebs encryption ( create from another snapshot to another region => use another KMS key)
- integrated with iam for auth
- Can audit use of keys via CloudTrail
- 3 cent per 10000 api calls
- scoped per region
## Key Types

### Symetric
- AES256 keys
- single key to encrypt and decrypt
- AWS services which use KMS use this
- you can only get this key via api call

### Asymetric
- public key (encrypt)
- private key (decrypt)
- can download public key
- private key only api
- use case: encryption outside of aws which access to api
## Key types
1. AWS managed key: display in the list
2. AWS owned key: not display in the list, all customer use ( default encryped) 
3. customer create by KMS: display in the list
4. customer imported key:  not display in the list, can not auto rotation



### Free
- aws managed => free
- customer managed, create, api call => charge 
### Customer Manged Key (CMK)
- 1 dollar a month
- created or imported in kms

## Key Rotation

### AWS Manged key
- automatic every 1 year

### CustomerManagedKey
- must be enabled
- automatic every year
- if imported only manual rotation with use of alias ( eg: create a new key => change alias from old key to new key)

## Key Policies
- similar to s3 policies
- control access to kms
- default = everyone in this account can use the key
- use for cross account

## Multi Region Keys
- keys are replicated with same id into different region, independent management
- encrypt and dercypt in other keys
- use case to encrypt global services (aurora global, dynamo global tables)