
VPC

![[Screenshot 2025-09-06 at 22.05.48.png]]

default vpc only have 1 in 1 region
custom can have many as you want
default vpc cidr 172.31.0.0/16 - can not change
/20 subnet in each AZ
deploy any services in default vpc alway have public ip v4

route 53
2 main: ![[Screenshot 2025-09-07 at 15.35.33.png]]

zone file is host on 5 managed name servers
can be public or private.. linked to vpc
store records
record type
- ns record: delegation to occur in dns root -> ns -> ...
- a record: host to ipv4
- aaaa record: host to ipv4
- cname: host to host: 
- mx record: ![[Screenshot 2025-09-07 at 15.55.02.png]]
- text record: prove domain ownership, ![[Screenshot 2025-09-07 at 15.56.38.png]]
DNS ttl:
- authoritative answer: query from the root
- non authoritatice answer: query from the cache

vpc sizing and structure
decide the range of cidr
tiers: web, app ...![[Screenshot 2025-09-14 at 15.18.52.png]]![[Screenshot 2025-09-14 at 15.23.05.png]]![[Screenshot 2025-09-14 at 15.27.04.png]]![[Screenshot 2025-09-14 at 15.30.32.png]]
custom vpc
![[Screenshot 2025-09-14 at 15.37.36.png]]

đeicated tenancy: set the vpc to de đeicated hardware => all the service inside the vpc will be in the dedicated hardware => cost premium
![[Screenshot 2025-09-14 at 15.40.59.png]]
all ipv6 is public

dns in a vpc:
vpc ip: 10.0.0.0 => dns ip : 10.0.0.2
- AWS dành sẵn vài địa chỉ đầu của mỗi subnet/VPC cho hạ tầng. Địa chỉ “DNS server” mà instance dùng chính là địa chỉ “Base IP + 2”.
    - Ví dụ subnet `10.0.1.0/24` → địa chỉ DNS sẽ là `10.0.1.2`.
enableDnsHostNames:- give the instance the DNS host name
enableDnsSupport: instances in the vpc can use the dns ip address

![[Pasted image 20250914154556.png]]

aws subnet:
az resilient
![[Screenshot 2025-09-14 at 16.41.06.png]]vpc router: logical network device which move data between subnet. in and out of vpc
has a network interface in every subnet

![[Screenshot 2025-09-14 at 16.45.58.png]]

dhcp: dynamic host configuration protocol
for every VPC, DHCP  options set to linked it, that can be change => create new one
auto asign ip v4,v6

vpc routing
route table:influence what to do with traffic when it leave a subnet Or what the VPC router will do when data leaves that subnet
if subnet dont have route table it will use the vpc main route table
route table can accociate with many subnet but 1 sub net only have one route table


![[Screenshot 2025-09-14 at 17.37.39.png]]
destination: can be ip, cidr, ...
when many route match: higher = more specific = higher priority
target: local - the vpc it self
flow: match des ~> foward to the target

Internet gate way (IGW)
![[Screenshot 2025-09-14 at 17.44.25.png]]![[Screenshot 2025-09-14 at 17.45.45.png]]

ipv4 addresses with a IGW
IGW: 
create a record: link the private ip to the public ip
change the source ip to public ip, and reverse

ec2 instance:
can not see the public ip. in the os
but with ip v6 ip alway the public ip

![[Screenshot 2025-09-14 at 17.51.45.png]]
bastion host
access to the internal VPC![[Screenshot 2025-09-14 at 17.53.16.png]]

statefull and state less
state less: need to allow full port
network access control list ( nacl )
state less
accociate with a subnet
connection within the same subnet aren't impacted by NACLs


![[Screenshot 2025-09-15 at 8.15.18.png]]![[Screenshot 2025-09-15 at 8.17.23.png]]![[Screenshot 2025-09-15 at 8.29.25.png]]

VPC security group ( SG)
sg not attach to instance or subnet, it attach to eni
while attach to instance => attach to the primary network interface

![[Screenshot 2025-09-15 at 8.32.56.png]]![[Screenshot 2025-09-15 at 8.35.15.png]]

![[Screenshot 2025-09-15 at 8.38.53.png]]
![[Screenshot 2025-09-15 at 8.40.12.png]]

Network Address Translation ( NAT ) and Nat gateway
IP masquerading: rather than the one private IP to one public IP process => many private IP to one single IP
ingoing doesnt work![[Screenshot 2025-09-15 at 8.43.36.png]]
nate gateway in the public subnet, have public ip => go to the internet gateway
it actually dont have public ip, also other in the vpc, nothing acctually have public ip => the igw does ![[Screenshot 2025-09-15 at 8.52.22.png]]
public subnet: vpc have igw, subnet configure to allocate public ip v4, have route table routing to the igw
elastic ip: the ip that don't change
more banwidch => more nat gateway
hourly charge
nat is az resilient , igw is region resilient ( attach to vpc )
max resilent => each az have 1 nat gw
![[Screenshot 2025-09-15 at 8.56.19.png]]
![[Screenshot 2025-09-15 at 9.00.17.png]]
nat instance can also use as the bastion host ( nat gw can't) 
with nat instance, can use SG, nat gw only can use NACL

![[Screenshot 2025-09-15 at 9.01.54.png]]
![[Screenshot 2025-09-15 at 9.08.37.png]]
VPC flow log
![[Screenshot 2025-10-05 at 14.59.57.png]]![[Screenshot 2025-10-05 at 15.01.43.png]]![[Screenshot 2025-10-05 at 15.05.39.png]]
Egress -only internet gateway
![[Screenshot 2025-10-05 at 15.09.24.png]]![[Screenshot 2025-10-05 at 15.17.59.png]]

Gateway enpoint
is not belong to subnet
![[Screenshot 2025-10-05 at 15.58.36.png]]![[Screenshot 2025-10-05 at 16.01.05.png]]
interface endpoint

privatelink: is a product that allows external services to be injected into your VPC, be given network interface inside your VPC subnet

![[Screenshot 2025-10-05 at 16.11.05.png]]![[Screenshot 2025-10-05 at 16.22.39.png]]![[Screenshot 2025-10-05 at 16.24.04.png]]![[Screenshot 2025-10-05 at 16.27.09.png]]
VPC peering
can connect into different account
![[Screenshot 2025-10-06 at 22.10.07.png]]![[Screenshot 2025-10-06 at 22.12.59.png]]

site to site vpn
![[Screenshot 2025-10-07 at 22.10.17.png]]
![[Screenshot 2025-10-08 at 7.05.04.png]]![[Screenshot 2025-10-08 at 7.06.11.png]]![[Screenshot 2025-10-08 at 7.09.14.png]]![[Screenshot 2025-10-08 at 7.11.51.png]]
Direct Connect
can not use to access the public internet
![[Screenshot 2025-10-09 at 6.47.56.png]]![[Screenshot 2025-10-09 at 7.20.19.png]]![[Screenshot 2025-10-09 at 7.26.58.png]]![[Screenshot 2025-10-09 at 7.32.12.png]]![[Screenshot 2025-10-09 at 7.34.06.png]]![[Screenshot 2025-10-09 at 7.35.10.png]]![[Screenshot 2025-10-09 at 7.44.33.png]]![[Screenshot 2025-10-09 at 7.46.49.png]]
transit gateway
![[Screenshot 2025-10-09 at 7.53.18.png]]![[Screenshot 2025-10-11 at 7.22.38.png]]
transit gateway can connect to the cross region , cross account transit gateway
![[Screenshot 2025-10-11 at 7.29.53.png]]![[Screenshot 2025-10-11 at 7.31.16.png]]