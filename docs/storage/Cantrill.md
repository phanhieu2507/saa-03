S3
global platform - regional resilient - auto replicate to another az
public service, unlimited data , multi-user
movies ,audio, photo, ..
accessed viia ai, cli, api , http

bucket > object 

object 
- key indentifies the obj in a bucket
- value = content of obj 0...5 tb
- version id 
- metadata
- access control
- sub resource
bucket:
- never leaves region 
- bucket name must be globally unique
- unlimited obj
- flat structure, evething is root level
- 
![[Screenshot 2025-09-07 at 9.46.34.png]]

window => file base storage
linux => block storage ( hard disk to mount)
![[Screenshot 2025-09-07 at 9.49.45.png]]

offload: suitable for put obj in

S3 practise:
in the UI dont need to select the region 
can copy setting from another bucket
block public access: after uncheck still have to grant access public
ARN : amazon resouse name 
when create a folder => create a obj name as the folder
delete bucket: empty => delete

s3 is private by default

resource perspective permission: quyen nhin tu phia tai nguyen

![[Screenshot 2025-09-10 at 6.45.29.png]]

resource policy have principal field
![[Screenshot 2025-09-10 at 6.53.35.png]]

![[Screenshot 2025-09-10 at 7.00.55.png]]can not you 1 acl to group of obj
![[Screenshot 2025-09-10 at 7.02.28.png]]![[Screenshot 2025-09-10 at 7.05.32.png]]![[Screenshot 2025-09-10 at 7.08.31.png]]

Object Versioning and MFA Delete
can not switch a bucket versioning
![[Screenshot 2025-09-10 at 22.05.07.png]]

versioning disabled: id = null
can get the version by specify id
s3 website dont need versioning
![[Screenshot 2025-09-10 at 22.10.13.png]]![[Screenshot 2025-09-10 at 22.11.21.png]]![[Screenshot 2025-09-10 at 22.12.07.png]]

s3 performmace
singgle put upload
![[Screenshot 2025-09-11 at 21.23.08.png]]

multi part upload
cannot upload bellow 100mb file
![[Screenshot 2025-09-11 at 21.27.41.png]]

s3 accerlerate tranfer
bucket name can not contain "."
dns compatible ( - Chỉ chữ thường a–z, số 0–9, và dấu gạch ngang “-”.
- Độ dài 3–63 ký tự.
- Bắt đầu và kết thúc bằng chữ hoặc số (không bắt đầu/kết thúc bằng “-”).
- Không chứa dấu chấm “.”, không có ký tự đặc biệt khác (không có “_”, khoảng trắng, chữ hoa).
- Không mang dạng địa chỉ IP (ví dụ 192.168.1.1).)
![[Screenshot 2025-09-11 at 21.50.55.png]]

server side encryption
bucket aren't encrypted .. obj are: define encryption in the obj level

![[Screenshot 2025-09-13 at 15.31.08.png]]

![[Screenshot 2025-09-13 at 15.32.59.png]]

![[Screenshot 2025-09-13 at 15.55.48.png]]
sse-c: s3 dont have the key, it discard when every thing done
- using aes-256
- 
![[Screenshot 2025-09-13 at 16.04.29.png]]
sse-s3: each object is encrypted by diiferent key
can not use when:
1. want to manage key
2. want to rotate the key
3. want to role seperation (eg: s3 full access will alway can read the data )
sse-kms
each object is encrypted by diiferent key![[Screenshot 2025-09-13 at 16.13.37.png]]![[Screenshot 2025-09-13 at 16.14.37.png]]

s3 bucket keys
![[Screenshot 2025-09-13 at 17.00.24.png]]![[Pasted image 20250913170603.png]]

s3 storage classes
![[Screenshot 2025-09-14 at 7.53.27.png]]

standard ia: used for long live data, not suitable for data that small ( less than 128 kb obj )
![[Screenshot 2025-09-14 at 8.20.29.png]]

![[Screenshot 2025-09-14 at 8.22.48.png]]![[Screenshot 2025-09-14 at 8.28.16.png]]
access frequency: standard -> standard ia -> glacies instant!

![[Screenshot 2025-09-14 at 8.41.49.png]]![[Screenshot 2025-09-14 at 8.46.54.png]]![[Screenshot 2025-09-14 at 10.18.45.png]]
life cycle configuration![[Screenshot 2025-09-14 at 10.33.26.png]]
can use to delete the obj
one zone ia can not transit to instant retrieval
if use the console or CLI can dirrectly change the class, but with life cycle it must be minium of time ( 30day ...)
![[Screenshot 2025-09-14 at 12.27.23.png]]

s3 replication:
![[Screenshot 2025-09-14 at 12.29.25.png]]

role: read obj on the src bucket, replicate to the des bucket
replicate on the diff account: the role replicate is not trusted by default => add bucket policy on the desc bucket
the versionning must be enabled on the desc and src account
![[Screenshot 2025-09-14 at 12.34.52.png]]

can define the desc bucket storage class
RTC: tùy chọn SLA cho S3 Replication (CRR/SRR) nhằm đảm bảo phần lớn đối tượng được sao chép sang bucket đích trong 15 phút, với cam kết 99.99% đối tượng dưới 15 phút.
![[Screenshot 2025-09-14 at 12.39.53.png]]

retroactive: old obj will not be replicated => use batch replication
only replicate the obj which the source account have permisson
can not replicate the delete marker created by life cycle policy
![[Screenshot 2025-09-14 at 12.45.43.png]]
why use replication
![[Screenshot 2025-09-14 at 12.47.17.png]]

presigned url
![[Screenshot 2025-09-14 at 13.13.17.png]]
can use presigned url to access the private obj
can create a URL for an obj you have no access to but... can not access


![[Screenshot 2025-09-14 at 13.19.09.png]]

presigned practise:
create in the CLI, or the console
the presign permission = the user or role that created it => (syncronus) ( alway have the same permission )
can also create for the not exist obj

s3 select and glacier select



![[Screenshot 2025-09-14 at 13.45.30.png]]![[Screenshot 2025-09-14 at 13.47.08.png]]

s3 event notifications
![[Screenshot 2025-09-14 at 13.49.22.png]]

![[Screenshot 2025-09-14 at 13.57.30.png]]

s3 access logs
many source => 1 target bucket -> OKEE
![[Screenshot 2025-09-14 at 14.03.22.png]]

s3 object log:
can not enable to the exist bucket => contact aws support
can not disable obj lock or versioning
![[Screenshot 2025-09-14 at 14.08.39.png]]
retention mode
compliance: finance, medical data
governance: can make change to the period, ... eg: test before the compliance mode

![[Screenshot 2025-09-14 at 14.12.48.png]]![[Screenshot 2025-09-14 at 14.13.59.png]]![[Screenshot 2025-09-14 at 14.16.19.png]]

- Mặc định: Khi bạn chỉ “Enable Object Lock” cho bucket nhưng không cấu hình “default retention”, các object mới upload sẽ không tự có retention/lock. Bạn phải đặt lock cho từng object (hoặc theo batch/quy tắc ứng dụng) nếu muốn.
    
- Nếu bạn bật default retention ở mức bucket:
    
    - Bạn có thể cấu hình mode mặc định (Governance hoặc Compliance) và thời hạn mặc định.
    - Khi đó, mọi object mới upload vào bucket sẽ tự động nhận lock theo mặc định đó.
    - Bạn vẫn có thể override (tăng/giảm trong Governance, chỉ tăng trong Compliance) cho từng object tùy quyền.
- Legal hold là tùy chọn riêng:
    
    - Không tự bật theo mặc định. Bạn phải đặt legal hold per object nếu cần.
s3 access point
![[Screenshot 2025-09-14 at 14.31.16.png]]![[Screenshot 2025-09-14 at 14.34.56.png]]
access point practise
multi region access point 
offer a global s3 host name that provice access to multiple s3 bucket accross aws regions, with automatic routing and failover between bucket
edit failover: active, passive 
can create replication rule in the access point setting: ![[Screenshot 2025-09-14 at 14.43.21.png]]

can setting that can replicate all or set the scope of obj by filter
replicate the obj can have delay ( consistently lag) -> using RTC option to fix


Database reresher![[Screenshot 2025-09-23 at 16.24.15.png]]

memory catching => key value database
![[Screenshot 2025-09-24 at 21.53.43.png]]![[Screenshot 2025-09-24 at 22.03.45.png]]![[Screenshot 2025-09-24 at 22.04.45.png]]![[Screenshot 2025-09-24 at 22.08.29.png]]


acid vs base
![[Screenshot 2025-09-24 at 22.16.20.png]]![[Screenshot 2025-09-25 at 6.47.17.png]]![[Screenshot 2025-09-25 at 6.50.32.png]]

acid: rds
base: dyamodb

acid, no sql: dyamodb transaction
AWS on ec2
![[Screenshot 2025-09-25 at 6.53.54.png]]
os level access
![[Screenshot 2025-09-25 at 6.56.05.png]]![[Screenshot 2025-09-25 at 7.08.20.png]]

RDS
![[Screenshot 2025-09-27 at 8.32.53.png]]
rds custom have ssh access to os
read replicate: asynchronous replication
standby: sync replication
backup to s3 => resilent![[Screenshot 2025-09-27 at 14.58.55.png]]![[Screenshot 2025-09-27 at 15.01.24.png]]

rds practise
1: create subnet group, ( multi subnet to place instance)
template: production, dev/test, free tier
can setup admin account master in settup( master account)
 db intance type: despite on the template ( free tier is limited)
 type storage: gp2, io1, io2
 can storage autoscaling ( must setting the storage threshhold)
 can set the public access
 can set the security group ( RDS is build on EC2 ) => has sg
every instance has port and endpoint => using to connect to rds

RDS multi AZ
backup orrcur on standby => no extra load on the primary


 
Old architecture ![[Screenshot 2025-09-27 at 15.35.47.png]]![[Screenshot 2025-09-27 at 15.36.29.png]]
![[Screenshot 2025-09-27 at 15.38.03.png]]
New architecture
can have only 2 reader only, aurora can have more
synchronouse replication to reader

![[Screenshot 2025-09-27 at 15.41.44.png]]
![[Screenshot 2025-09-27 at 15.44.35.png]]

backup and store
save backup to s3, region resilent
can snapshot, first is full
multi AZ, snap shot is on the stand by. snapshot is not auto deleted
auto backup is every 5minute, retention 0 to 35 days
delete the instance => take the final snap shot

![[Screenshot 2025-09-27 at 15.50.22.png]]![[Screenshot 2025-09-27 at 15.50.54.png]]

create new fromt snapshot and backup
restore are not fast, take a lot of time not good for RTO


![[Screenshot 2025-09-27 at 15.52.53.png]]

read replicas
![[Screenshot 2025-09-27 at 15.53.40.png]]
only for read
has it own endpoint address => application use it
they no automatic failover
async, have lag
can create read replicate in another region ( cross region read replicate), encrypt in transit
can create read replicate of replicate => lag

![[Screenshot 2025-09-27 at 15.58.35.png]]
can promote quickly, => promoted, can used to write

![[Screenshot 2025-09-27 at 16.01.46.png]]

RDS multi practise
apply the change: next maintenance windown, immediately ( all impact performance), status is modifying. 
when create the standby: create a snapshot => move to the stand by
reboot db intance: (check the reooote with failover) => promote standby
doesn't offer immediate failover ( 60s - 120s )

RDS security


![[Screenshot 2025-09-27 at 17.38.39.png]]![[Screenshot 2025-09-27 at 17.40.00.png]]![[Screenshot 2025-09-27 at 17.43.18.png]]

using iam only authentication, cannot authorisation
![[Screenshot 2025-09-27 at 17.47.26.png]]

RDS custom
![[Screenshot 2025-09-27 at 17.52.14.png]]![[Screenshot 2025-09-27 at 17.54.03.png]]

Amazone Aurora architecture
replicas in aurora: availibility + read performance
one primary can have max 15 read replica

![[Screenshot 2025-09-27 at 18.04.00.png]]![[Screenshot 2025-09-27 at 18.05.48.png]]![[Screenshot 2025-09-27 at 18.11.09.png]]![[Screenshot 2025-09-27 at 18.12.28.png]]![[Screenshot 2025-09-27 at 18.13.57.png]]

fast clone : reference to the original source
![[Screenshot 2025-09-27 at 18.21.23.png]]
aurora server less
![[Screenshot 2025-09-27 at 20.39.48.png]]![[Screenshot 2025-09-27 at 22.09.58.png]]![[Screenshot 2025-09-27 at 22.12.22.png]]

Aurora global database
![[Screenshot 2025-09-27 at 22.17.05.png]]
replication = 1 second
replication no impact on DB performance
![[Screenshot 2025-09-27 at 22.22.09.png]]

multi master
![[Screenshot 2025-09-28 at 6.49.40.png]]
no cluster endpoint to use
no loadbalancing
need a quorum of node agree
![[Screenshot 2025-09-28 at 7.09.18.png]]

RDS proxy
![[Screenshot 2025-09-28 at 7.16.25.png]]
proxy is run inside the vpc![[Screenshot 2025-09-28 at 7.19.51.png]]![[Screenshot 2025-09-28 at 7.21.20.png]]![[Screenshot 2025-09-28 at 7.24.18.png]]

EFS
![[Screenshot 2025-09-28 at 9.18.51.png]]
need to put mount target in multiple AZ
![[Screenshot 2025-09-28 at 9.21.17.png]]

performance mode: general purpose: latency sensitive usecase, web servers, content management systems
max io: high parallel, bigdata media processing, 
throughput mode: bursting: same as gp2
provisionned: io1
lifecycle can move like s3
![[Screenshot 2025-09-28 at 9.26.45.png]]
efs has mount target each az, mount target has the security group
file system policy:

![[Screenshot 2025-09-28 at 9.45.49.png]]

sudo mkdir -p /efs/wp-content
-p : tạo nếu chưa có

Amazone dyamo DB 
public service, ![[Screenshot 2025-10-12 at 16.57.11.png]]
![[Screenshot 2025-10-12 at 21.47.49.png]]![[Screenshot 2025-10-12 at 21.50.37.png]]![[Screenshot 2025-10-12 at 21.51.32.png]]![[Screenshot 2025-10-12 at 21.53.25.png]]
dyamoDB, consistency, performance
when using the ondemand => 5 time cost but reduce admin operrational over head
![[Screenshot 2025-10-12 at 21.57.42.png]]![[Screenshot 2025-10-12 at 22.03.22.png]]![[Screenshot 2025-10-12 at 22.14.38.png]]![[Screenshot 2025-10-13 at 8.56.20.png]]![[Screenshot 2025-10-13 at 9.07.34.png]]![[Screenshot 2025-10-13 at 9.08.12.png]]
![[Screenshot 2025-10-13 at 9.12.53.png]]
can not add local secondary indexes after the tables is created
![[Screenshot 2025-10-13 at 9.15.05.png]]
sparse: thưa thớt
![[Screenshot 2025-10-13 at 9.34.27.png]]![[Screenshot 2025-10-13 at 9.35.45.png]]![[Screenshot 2025-10-13 at 9.38.33.png]]![[Screenshot 2025-10-13 at 9.41.20.png]]![[Screenshot 2025-10-13 at 9.54.27.png]]![[Screenshot 2025-10-13 at 9.57.26.png]]![[Screenshot 2025-10-13 at 9.58.55.png]]![[Screenshot 2025-10-13 at 10.02.16.png]]![[Screenshot 2025-10-13 at 10.06.11.png]]![[Screenshot 2025-10-13 at 10.07.48.png]]![[Screenshot 2025-10-13 at 10.17.12.png]]![[Screenshot 2025-10-13 at 10.19.46.png]]
any application using dax need to be same VPC as DAX
![[Screenshot 2025-10-13 at 10.32.22.png]]![[Screenshot 2025-10-13 at 10.42.50.png]]