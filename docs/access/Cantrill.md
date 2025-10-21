MFA
Factor: different pieces of evidance which prove identiry
knowledge: some thing you know username , pass 
possesion: some thing you have: bank card
inherent: something you are.. fingerprint, face
location: ...

app MFA alway to be authenticated
 ![[Pasted image 20250826212733.png]]

with production should use hardware token

IAM
only controls local indentites in your account, not from external account

![[Pasted image 20250827055854.png]]
iam policy
statement:
- sid: 
- action: 
- effect: allow or deny
- resource: refer to resource
overlap rule:
- explicit deny -> explicit allow -> default deny: default alway deny
inline and managed policy ( reusable )![[Screenshot 2025-09-07 at 17.19.25.png]]

IAM Group: 
- container for users
- can not login to a group
- also have inline and managed group
- can not have nested group
- 300 group per account
- group are not identity => can not be referencred as a principal in a policy
iam role:
- using when can not indentify the number of principals
- more than 5000 principal
- role are assumed => you become that role
- short term, borrow the permission
- trust policy: which identity can assume that role, same or diff account, service 
- permissions policy:
- sts:asumeRole: generate temporary credential (secure token service)
when to use iam role
cross account access: 

service - linked roles:
- ![[Screenshot 2025-09-07 at 22.08.39.png]]![[Screenshot 2025-09-07 at 22.16.22.png]]
-  policy allow to create a sẻvice linked role
role seperating: give one group of people ability to create role and another group of people the ability to use them


AWS Org
standard aws account: the account not in aws org, use this to create org => management account ( master account )
- use to invite another account to the org
- the joined acc change from standard => member acc
org root: not account root user, it a root container of the org contain the master and member
- can also contain other container => OUs ( org unit)
ous: can contain acc ( master, member ), other ous
consolidated billing: member account's individual billing methods are removed, pass billing to the master acc
- consolidation of reservations and volume discounts

Service Control Policies
inherit from top to bottom
never affect the master account
account permissions boundaries: limit what the account ( include the account root user ) can do
dont grant any permissions
add allow list: delete the default allow list ( allow all) -> add allow list


